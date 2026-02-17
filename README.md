# AI Experts Assignment (Python)

This project demonstrates setting up a small Python project to run reliably (locally + in Docker), pinning dependencies for reproducible installs, writing focused tests to reproduce a bug, and implementing a minimal, reviewable fix.

## Project Structure

- `app/` — Application code (`http_client.py`, `tokens.py`)
- `tests/` — Test suite (`test_http_client.py`)
- `dockerfile` — Runs the test suite in a CI-style container
- `requirements.txt` — Pinned dependencies
- `EXPLANATION.md` — Bug analysis and fix explanation

## How to Run Tests Locally

1. **Set up a virtual environment (optional but recommended):**
   ```bash
   python -m venv venv
   .\venv\Scripts\Activate
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run tests:**
   ```bash
   python -m pytest -v
   ```

## How to Build and Run Tests with Docker

1. **Build the Docker image:**
   ```bash
   docker build -t ai-experts-app .
   ```

2. **Run the tests in a container:**
   ```bash
   docker run --rm ai-experts-app
   ```
