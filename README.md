# Let — AI squash coaching site

A small full-stack starter: a static frontend with a chat coach, backed by an
Express server that proxies chat messages to Claude (Anthropic API).

## What's inside

```
squash-ai/
├── server.js          Express server + /api/chat endpoint
├── package.json
├── .env.example        Copy to .env and add your API key
└── public/
    ├── index.html       Landing page + chat UI
    ├── style.css
    └── script.js        Chat front-end logic
```

## Run it locally

1. Install dependencies:
   ```
   npm install
   ```
2. Copy the env template and add your Anthropic API key:
   ```
   cp .env.example .env
   ```
   Then open `.env` and set `ANTHROPIC_API_KEY=sk-ant-...`
   (Get a key at https://console.anthropic.com if you don't have one.)
3. Start the server:
   ```
   npm start
   ```
4. Open http://localhost:3000

## Why a server at all?

The Anthropic API key must never be exposed in browser code — anyone could
read it from your site's JavaScript and rack up charges on your account.
`server.js` keeps the key server-side and only exposes a narrow `/api/chat`
endpoint that the frontend calls.

## Account linking

Developer mode is protected by the `squashdev` password and requires a secure
public ClubLocker or SquashLevels profile URL during sign-in. Google, Apple,
and Microsoft are shown as provider choices; production OAuth requires each
provider's client credentials and callback configuration.

The site stores only the profile URL and a short-lived in-memory session token
in browser local storage. It does not collect ClubLocker passwords, session
cookies, or private account data.

This project does not invent or proxy a ClubLocker tournaments/rating API.
Live synchronization requires an official ClubLocker API, OAuth flow, or an
authorized export from the club. Once those credentials and endpoint details
are available, add the integration server-side and keep tokens in environment
variables; never place them in `public/` or browser local storage.

## Where to go from here

- **Swap the coaching persona**: edit `COACH_SYSTEM_PROMPT` in `server.js`.
- **Add more pages**: e.g. a drill library, a booking page, player profiles.
- **Persist chat history**: currently it's in-memory in the browser tab only
  — add a database if you want conversations to survive a refresh.
- **Deploy**: this runs on any Node host (Render, Railway, Fly.io, a VPS).
  Set `ANTHROPIC_API_KEY` as an environment variable on whatever platform
  you use — don't commit your `.env` file.
