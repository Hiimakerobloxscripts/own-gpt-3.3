# OWN GPT Cloud

Cloud-hosted AI chat with a self-built crawler and SQLite search index. No local model and no training corpus.

## AI provider

The app uses Novin Cloud's OpenAI-compatible API gateway.

Render environment variables:
- `NOVIN_API_KEY` — secret API key from the Novin Cloud console
- `NOVIN_BASE_URL` — defaults to `https://iapi.novin.cloud/v1`
- `NOVIN_MODEL` — defaults to `openai/gpt-4o-mini`

Novin Cloud documents Rial wallet billing based on token usage. It is not an unlimited free API. An adult account holder should review the provider's terms, pricing, and spending limits before creating or funding an account. Never put the API key in source code or GitHub.

## Render

Build command: `pip install -r requirements.txt`
Start command: `gunicorn app:app --workers 1 --threads 4 --timeout 120`
Health check: `/health`

## Search limitations

The app fetches candidate Wikipedia pages discovered through Wikipedia's public search API, extracts page text, and indexes it in its own SQLite FTS index. It is a small independent index, not a Google-scale index or full-web search engine. Respect robots.txt, site terms, and rate limits before expanding crawling.

## Storage

SQLite currently uses `/tmp`; on free Render instances it is temporary and can reset on restart or redeploy. Durable indexing requires persistent storage or an external database.

Never commit API keys.
