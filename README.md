# OWN GPT Cloud

Cloud-hosted AI chat with a self-built crawler and SQLite search index. No local model and no training corpus.

## Render
Build command: `pip install -r requirements.txt`
Start command: `gunicorn app:app --workers 1 --threads 4 --timeout 120`
Health check: `/health`

Set `GEMINI_API_KEY` in Render Environment. `GEMINI_MODEL` defaults to `gemini-2.5-flash`. API availability and free quotas depend on Google's current terms and region.

## Search limitations
The app fetches candidate Wikipedia pages discovered through Wikipedia's public search API, extracts page text, and indexes it in its own SQLite FTS index. It is a small independent index, not a Google-scale index or full-web search engine. Respect robots.txt, site terms, and rate limits before expanding crawling.

## Storage
SQLite currently uses `/tmp`; on free Render instances it is temporary and can reset on restart or redeploy. Durable indexing requires persistent storage or an external database.

Never commit API keys.