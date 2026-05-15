# Meridian Health Services — Digital Health Platform API

Python FastAPI application handling patient records and appointments for 84,000 registered patients.

## Local Development

```bash
cd app
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

API documentation: http://localhost:8000/docs
Health check: http://localhost:8000/health

## Authentication

All endpoints except `/health` require an API key header:
```
x-api-key: dev-key-12345
```

Override valid keys: `VALID_API_KEYS=key1,key2` environment variable.

## Running Tests

```bash
pip install pytest httpx
pytest tests/ -v
```

## Your Task

You do NOT modify the application code.

Your job is to:
1. Add TruffleHog secrets scanning to GitHub Actions — it will find the hardcoded credential
2. Add Bandit SAST scanning — it will find security issues in the code
3. Add pip-audit dependency scanning — it will flag the vulnerable requests version
4. Fix what the tools find and verify the pipeline passes on clean code

See the case study document for full instructions.

## Known Security Issues (for the scanning exercise)

The following issues are intentionally present for Bandit to find:
- **B105** — Hardcoded password in `DEBUG_PASSWORD` variable
- **B101** — Use of `assert` for authentication logic
- **B110** — Bare `except` clause in export endpoint

And for pip-audit:
- `requests==2.25.0` — CVE-2023-32681 (SSRF vulnerability). Fix: update to `requests>=2.31.0`
