# J.A.R.V.I.S. — Personal AI System

A local-first starter application with a blue HUD, animated core, Grok-compatible streaming chat, SQLite conversation history, user-approved memory, browser speech recognition, and speech synthesis.

## Requirements
- Node.js 20+
- A replacement xAI API key

## Setup
1. Extract the project.
2. In the project folder run `npm install`.
3. Copy `.env.example` to `.env`.
4. Put your **newly generated** xAI key in `AI_API_KEY`. Do not put keys in frontend code or commit `.env`.
5. Check `AI_MODEL` against the models enabled for your xAI account.
6. Run `npm run dev`.
7. Open `http://localhost:5173`.

The frontend runs on port 5173 and the API server on port 3001. SQLite creates `jarvis.sqlite` locally.

## Current functionality
- Animated responsive J.A.R.V.I.S. HUD with IDLE, LISTENING, THINKING, SPEAKING, ERROR and OFFLINE states.
- Server-side xAI-compatible `/chat/completions` streaming. The API key remains on the backend.
- Persistent chat history in SQLite, with clear-history control.
- Explicitly saved, reviewable and deletable memories. The app does not silently store long-term memories.
- Browser speech recognition when supported, activated only by pressing the microphone button.
- Browser speech synthesis fallback, with mute and stop controls.
- Backend health check and configuration status.

## Voice configuration
The supplied voice ID is placed in `.env.example`, but the voice provider is intentionally blank because the provider has not been confirmed. Current speech output uses the browser's installed voice. A provider-specific TTS adapter is the next voice milestone; do not assume a voice ID alone identifies the provider.

## Security notes
- Treat the API key previously pasted into chat as compromised. Revoke it and create a replacement before running this app.
- `.env` is ignored by Git. Never commit it, expose it in browser storage, or paste it into source files.
- This starter is intended for local development. Before exposing it to a network, add authentication, CSRF/origin hardening, rate limiting, and HTTPS.
- Memory is user-triggered. Avoid saving sensitive personal information.

## Next milestones
1. Add provider-specific TTS once the voice provider is confirmed.
2. Add authentication and hardened deployment controls.
3. Add a command router and real integrations (weather, calendar, email, web search, reminders).
4. Add automated backend and UI tests, cancellation controls, and usage/token telemetry.
5. Add configurable HUD/audio preferences and diagnostics.

## Troubleshooting
- `Grok is not configured`: check `.env`, then restart the backend.
- Provider errors: verify the replacement key, account access, base URL, and model name.
- Microphone unavailable: use HTTPS or localhost, grant browser permission, and use a browser supporting Web Speech API.


## Install on iPhone (Home Screen app)
This project is configured as a Progressive Web App (PWA). It must be deployed to an HTTPS address first.

1. Deploy this repository as a Node web service (for example, on a host that supports Node.js persistent services and persistent disks).
2. Set the build command to `npm install && npm run build`.
3. Set the start command to `npm start`.
4. Add environment variables from `.env.example` in the host dashboard. Set `AI_API_KEY` to your newly generated key. Never upload `.env` to Git.
5. Attach persistent storage for `jarvis.sqlite` if the host uses ephemeral filesystems. Mount it at the project working directory or configure a persistent database path.
6. Open the deployed HTTPS URL in Safari on your iPhone.
7. Tap Share → Add to Home Screen → Add.

The J.A.R.V.I.S. icon will appear on your Home Screen and launch in standalone mode. AI chat requires an internet connection. The app shell may load offline, but API-backed chat and memory operations will not work offline.

For temporary testing on the same Wi-Fi network, run the app on your computer and open `http://COMPUTER-LAN-IP:5173` in iPhone Safari. Microphone and speech features may require HTTPS or localhost browser security rules; use a deployed HTTPS address for reliable testing.
