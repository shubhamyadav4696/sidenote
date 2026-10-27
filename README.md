# Sidenote

A one-page meeting companion for your phone. Paste in context before a call, and it quietly matches what's being said against your notes — with an optional button to ask Claude for a sharper suggestion, including a glance at your screen if you want that.

## Why it needs to be hosted (can't just open the file)

Phones only grant microphone and camera access to pages loaded over **HTTPS** (or `localhost`). Opening `index.html` directly from your file system won't let the mic or camera turn on. You need to put this one file on any free static host. Easiest option — GitHub Pages:

1. Create a new **public** repo on GitHub (any name, e.g. `sidenote`).
2. Upload `index.html` to it (GitHub's web UI → "Add file" → "Upload files" works fine, no git needed).
3. In the repo, go to **Settings → Pages**, set Source to the `main` branch, root folder, and save.
4. After a minute, GitHub shows your live URL (something like `https://yourname.github.io/sidenote/`). Open that on your phone.

Netlify or Vercel's free tiers work the same way if you'd rather use those — drag the single `index.html` file in and you'll get an HTTPS link.

## Using it

1. Open the hosted link on your phone.
2. Paste whatever you might need to reference during the meeting into the notes box — separate distinct points with a blank line, since each one is matched independently.
3. "Answer questions automatically" is on by default — when something said sounds like a question, Sidenote answers it on its own (from your notes always, and from Claude too if you've added a key below). Turn it off if you'd rather trigger answers yourself with the buttons.
4. Optional: turn on the camera toggle if you want AI suggestions that can see your screen. Optional: open "AI-generated suggestions," pick a provider, and paste a key if you want AI-written answers, not just notes-matching (which works with no key at all):
   - **Claude (Anthropic)** — get a key at [console.anthropic.com](https://console.anthropic.com), pick Sonnet (sharper) or Haiku (faster).
   - **ChatGPT (OpenAI)** — get a key at [platform.openai.com](https://platform.openai.com/api-keys). Type in the exact model ID you want to use (check [platform.openai.com/docs/models](https://platform.openai.com/docs/models) for your account's current options — model names change often, so this is a free-text field rather than a fixed list).
   You can fill in both and switch providers from the dropdown any time; each key is remembered separately.
5. Tap **Start session**, allow the microphone (and camera, if enabled) when your phone asks.
6. As the conversation happens, questions get answered on their own — each suggestion card shows the question it's answering. Tap **Ask AI** any time for an on-demand suggestion too, grounded in your notes, the recent transcript, and — if the camera's on — a fresh photo of whatever it's pointed at.
7. If live transcription isn't available (most iOS browsers don't support it), type key lines (including questions) into the box under the transcript — auto-answer and matching both still work from typed lines.

## What stays where

- Your notes and API key(s) are saved only in your phone browser's local storage — never sent anywhere except, if you add a key, directly from your browser to Anthropic's or OpenAI's API (whichever you picked) when a suggestion is requested.
- Nothing is recorded or stored beyond the current browser tab. Ending a session clears the transcript and suggestions; your notes and key stay filled in for next time.
- The API key lives in this browser only. Don't fill it in on a shared or borrowed device, and consider giving it a spending cap in the Anthropic console.

## Limits worth knowing

- Question detection is a heuristic (ends in "?", or opens with a question word like "what/how/can/is…") — it'll occasionally miss a real question or fire on a rhetorical one. A short cooldown stops it from re-answering the same question or firing back-to-back too fast.
- The camera isn't analyzed continuously — each AI answer grabs one fresh frame, not a live video feed. Continuous frame-by-frame analysis isn't something the API is built for (or affordable at that rate).
- Live transcription is Chrome's built-in speech recognition, not Anthropic's — quality varies by accent and background noise, and it needs a live network connection to work.
- The notes-matching (no API key) is simple keyword overlap, not true language understanding — it's a fast, free first pass, not a replacement for an AI-written answer.
