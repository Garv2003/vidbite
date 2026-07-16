# vidbite

An AI-powered YouTube video summarizer. Paste a YouTube URL, and vidbite pulls the transcript,
generates a concise AI summary, and saves it to your account — with a Markdown-rendered view, an
inline video player, and per-user history and stats.

## Features

- **AI summarization** of any YouTube video from its transcript (Google Gemini).
- **Accounts & auth** — register / login / logout with JWT (access + refresh, token revocation).
- **Saved summaries** — create, view, edit, delete; each tied to the logged-in user.
- **Markdown-rendered summaries**, an embedded video player, and profile stats.
- **Dockerized** — client + API + DB via `docker-compose`.

## Architecture

```
React client ──(JWT)──▶ Flask API ──▶ youtube-transcript-api ──▶ Gemini ──▶ summary
                            │
                            └──▶ SQLAlchemy (SQLite/Postgres): users, summaries
```

- **Client:** React 19 + Vite, React Router 7, TanStack Query, Zustand (auth store),
  React Hook Form + Zod, Tailwind + Radix/shadcn, react-player, showdown (Markdown).
- **Server:** Python Flask + flask-smorest (OpenAPI/Swagger), flask-jwt-extended,
  SQLAlchemy, passlib; `google-generativeai`, `youtube-transcript-api`, `pytube`.

## Getting started

```bash
# with Docker
docker-compose up --build

# or run each side
cd server && pip install -r requirements.txt && flask run
cd client && npm install && npm run dev
```

Set the required env vars (Gemini API key, JWT secret, DB URL) — see `server` config.

## Project structure

```
vidbite/
├── client/   # React 19 + Vite SPA (auth, submit URL, view/edit summaries, stats)
└── server/   # Flask API: JWT auth, summary CRUD, Gemini summarization, Swagger docs
```

## Roadmap

- Stream summaries as they generate; harden auth (move JWT secret to env, persistent token blocklist).
- More robust transcript ingestion; export summaries; deploy a live demo.
