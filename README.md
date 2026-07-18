# AI Code Reviewer

Structured code review with real line numbers, severity levels, and a schema the model has to obey.

**3 of 10** — part of a GenAI project series. FastAPI backend, vanilla JS frontend.

## What it demonstrates

- Forcing structured JSON output with a response schema — no regex parsing of prose
- Line-numbering source before it reaches the model so citations are real
- Severity triage rather than an undifferentiated wall of suggestions

## Run it

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env             # Windows: copy .env.example .env
# add your key to .env  (skip if this project needs no key)
uvicorn main:app --reload
```

Open http://127.0.0.1:8000

## Keys

| Key | Where to get it | Where it goes |
|---|---|---|
| `GEMINI_API_KEY` | https://aistudio.google.com/apikey (free) | `.env` |

## Stack

FastAPI · google-genai · JSON schema output

## How it works

The source is numbered line by line before it goes into the prompt, so when the model cites line 42 it is pointing at something real. A `response_schema` forces a list of findings with a fixed shape — the parsing is `json.loads`, never a regex over English. Findings are sorted by severity.

---
MIT
