# Explanation

## What was the bug?

When `oauth2_token` was set to a plain `dict` (instead of an `OAuth2Token` instance), the `Client.request` method in `http_client.py` neither refreshed the token nor set the `Authorization` header. The API request was sent unauthenticated.

## Why did it happen?

The refresh condition on line 30 only triggered when the token was falsy (`None`) or when it was an `OAuth2Token` instance that had expired. A non-empty dict is truthy, so `not self.oauth2_token` evaluated to `False`. The `isinstance` check also returned `False` because a dict is not an `OAuth2Token`. Both branches were skipped, leaving no header set.

## Why does the fix solve it?

Adding `not isinstance(self.oauth2_token, OAuth2Token)` as a condition ensures that any token value that is not a proper `OAuth2Token` instance (such as a raw dict) triggers a refresh. After `refresh_oauth2()` runs, the token becomes a valid `OAuth2Token`, and the existing `as_header()` logic sets the `Authorization` header correctly.

## One case the tests don't cover

The tests don't cover a scenario where `refresh_oauth2` itself fails (e.g., due to a network error). The client would raise an unhandled exception mid-request, and there is no fallback or retry logic.
