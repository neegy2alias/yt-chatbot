# Local AI Chat

A private AI chatbot that runs **entirely in your browser** — no server, no API key, no account,
no usage limits. The model (an open-weight LLM) is downloaded once and runs on your own GPU via
WebGPU.

Live pages:

- `index.html` — the chatbot
- `watch.html` — a YouTube **embed** player (see the note at the bottom)

## Deploy to GitHub Pages

1. Create a **public** repo and push these files (or use *Add file → Upload files*).
2. Repo → **Settings → Pages** → **Build and deployment → Source: GitHub Actions**.
3. Wait for the workflow (Actions tab), then open
   `https://<your-username>.github.io/<repo-name>/`.

> Hosting on Pages is the smoothest path: it serves over **HTTPS**, which the model needs for
> storage and WebGPU. Opening the file by double-clicking (`file://`) will **not** work — browsers
> block ES-module imports from `file://`, and sandboxed previews block the Cache API.

## Requirements

- **Chrome or Edge 113+** on desktop (or Safari 18+). Firefox needs WebGPU enabled in `about:config`.
- A GPU with reasonable memory. On integrated graphics it will work but be slow.
- First **Load model** downloads the weights (roughly 300 MB for a 1B model, up to ~2 GB for a 3B)
  and the browser caches them, so later loads are instant.

## How it works

The page imports [WebLLM](https://github.com/mlc-ai/web-llm) from a CDN and creates an engine for
the model you pick. Inference runs locally through WebGPU; nothing you type is sent anywhere.

## Running locally instead of Pages

```bash
python3 -m http.server 8000
# open http://localhost:8000/
```

## About the YouTube page

`watch.html` **embeds** YouTube videos using YouTube's official player. It does **not** download
them.

Downloading YouTube videos (with yt-dlp or similar) breaks YouTube's Terms of Service, and
infringes copyright unless the video is yours, is Creative-Commons licensed, or you have the
creator's permission. If you need an actual file:

- **Your own uploads** — YouTube Studio → your video → Download.
- **Creative-Commons videos** — the licence permits reuse; filter by it on YouTube.
- **Public-domain / openly licensed media** — the [Internet Archive](https://archive.org/details/movies)
  and Wikimedia Commons distribute files directly.
