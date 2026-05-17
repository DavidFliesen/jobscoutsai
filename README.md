# Job Scouts AI

> AI-powered personal job search intelligence — free, open source, runs entirely in your browser.

![Job Scouts AI Logo](logo.png)

**Live Demo:** *(add your GitHub Pages URL here)*

---

## What It Does

Job Scouts AI uses Google's Gemini AI to act as your personal job market analyst. Upload your resume, configure your target companies and skills, and let the AI scout for matching opportunities — returning a ranked, scored briefing you can export as TXT, HTML, or PDF.

No servers. No subscriptions. No data collection. Everything runs in your browser.

---

## Features

- **Resume Upload & AI Parsing** — Upload PDF, TXT, DOC, or paste text. Gemini extracts your skills, experience, and preferences automatically.
- **Numeric Scoring (0–100)** — When a profile is loaded, each lead gets a detailed numeric match score with breakdown text. Without a profile, qualitative HOT / WARM / COLD scoring is used.
- **Configurable Targets** — Set target companies, skill keywords, preferred locations, job sources, and search preferences — all in the browser.
- **Optional Live Web Search** — Toggle Google Search Grounding to pull real-time job listings (uses free-tier quota — see note below).
- **Export** — Download results as TXT, HTML report, or print to PDF.
- **Import / Export Config** — Sync your full configuration across devices via clipboard JSON.
- **Privacy First** — Your API key and resume never leave your device. The only external call is directly from your browser to Google's API using your own key.

---

## Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML / CSS / ES5 JavaScript |
| Fonts | Exo 2, Share Tech Mono (Google Fonts) |
| Hosting | GitHub Pages (static) |
| AI Model | Google Gemini 2.5 Flash (via Gemini API) |
| PDF Parsing | Gemini native PDF support (inline base64) |
| Word Export | docx.js 8.5.0 (CDN) |
| Storage | Browser localStorage only |

No backend. No Node.js. No build step. Just open `index.html`.

---

## Setup: Getting Your Free Google AI Studio API Key

Job Scouts AI requires a free Google AI Studio API key. No credit card is required.

### Step-by-Step

1. **Go to Google AI Studio**
   Visit: [https://aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)

2. **Sign In**
   Use any Google account (Gmail, Workspace, etc.).

3. **Create an API Key**
   Click the **"Create API key"** button. If prompted, create a new project or select an existing one.

4. **Copy Your Key**
   The key starts with `AIza` and is around 39 characters long. Copy it.

5. **Paste Into the App**
   Open Job Scouts AI, go to the **API Configuration** panel, paste your key, and click **Save Config**.

6. **Test the Connection**
   Click **Test Connection** to verify the key works.

### Free Tier Limits (as of 2026)

| Resource | Free Tier |
|---|---|
| Requests per day | 1,500 RPD (Gemini 2.5 Flash) |
| Requests per minute | 10–15 RPM |
| Google Search Grounding | ~500 searches/day free |
| Cost | $0 — no credit card required |

> **Note on Live Web Search:** The optional "Enable Live Web Search" toggle uses Google's Search Grounding feature. On the free tier, this is limited to approximately 500 grounding queries per day. A single scout run may trigger multiple search queries. If you hit quota errors (`429 Resource Exhausted`), disable live search — the AI will still generate high-quality job leads from its training knowledge.

---

## Deploying to GitHub Pages

### Option A: Upload via GitHub Web

1. Create a new public repository (e.g. `job-scouts-ai`)
2. Click **Add file → Upload files**
3. Upload `index.html` and `logo.png`
4. Go to **Settings → Pages**
5. Under **Source**, select `main` branch and `/ (root)` folder
6. Click **Save** — your site will be live at `https://yourusername.github.io/job-scouts-ai/`

### Option B: Git CLI

```bash
git init
git add index.html logo.png README.md
git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/job-scouts-ai.git
git branch -M main
git push -u origin main
```

Then enable GitHub Pages in repository Settings.

---

## File Structure

```
job-scouts-ai/
├── index.html      # Complete app — all UI, JS, CSS in one file
├── logo.png        # Job Scouts AI logo (place in same folder)
└── README.md       # This file
```

That's it. No package.json, no build step, no dependencies to install.

---

## Configuration Reference

All settings are saved to `localStorage` automatically. Nothing is stored on any server.

### localStorage Keys

| Key | Contents |
|---|---|
| `jobscouts_apikey` | Your Google AI Studio API key |
| `jobscouts_model` | Selected Gemini model string |
| `jobscouts_search` | Live web search enabled (`"true"` / `"false"`) |
| `jobscouts_state` | Full app state: companies, skills, locations, prefs, sources, profile |

### Export / Import Config

Use **Export Config** (copies JSON to clipboard) to back up or transfer your full configuration including your API key, all targets, and your loaded profile. Use **Import Config** to restore it on another device.

> **Security note:** The exported JSON includes your API key. Treat it like a password — don't share it publicly.

---

## Scoring System

| Badge | Score Range | Meaning |
|---|---|---|
| **HOT** (green) | 75–100 | Strong match — apply now |
| **WARM** (amber) | 50–74 | Good fit — worth a closer look |
| **COLD** (grey) | 0–49 | Partial match — stretch role |

With a resume loaded, each lead also shows:
- A numeric 0–100 score
- A visual score bar
- A 1–2 sentence breakdown explaining the score

Without a resume, scoring is qualitative (HOT/WARM/COLD) based on keyword matching.

---

## Choosing a Gemini Model

| Model | Speed | Quality | Notes |
|---|---|---|---|
| **Gemini 2.5 Flash** (default) | Fast | Excellent | Best for most users |
| Gemini 2.0 Flash | Fastest | Very good | Use if 2.5 Flash is unavailable |
| Gemini 2.5 Pro | Slower | Best | Use for complex profiles |

All models are available on the free tier. Switch models in the **API Configuration** panel.

---

## Privacy Policy

- **Your API key** is stored only in your browser's `localStorage`. It is sent only to `generativelanguage.googleapis.com` (Google's Gemini API) with your requests.
- **Your resume** is processed in-memory and optionally stored in `localStorage` as parsed JSON (not the original file). It is sent to the Gemini API for analysis.
- **No data** is sent to any third-party servers. This project has no backend, no analytics, and no tracking.
- **Google's free tier** may use request data to improve Google products. To opt out, upgrade to a paid API tier or use Google's paid Vertex AI endpoint. See [Google AI terms](https://ai.google.dev/gemini-api/terms).

---

## Known Limitations

- **Live job listings:** The AI generates realistic leads based on its training knowledge of companies, roles, and the job market. With Live Web Search enabled, it can pull real-time listings — but CORS restrictions prevent scraping job boards directly.
- **Apply URLs:** URLs provided by the AI are best-guess links to company career pages. Always verify them before applying.
- **Rate limits:** On the free tier, heavy use may trigger 429 errors. Wait a minute and try again, or disable live search.
- **PDF parsing:** Complex PDF layouts (columns, graphics-heavy resumes) may parse less accurately than plain text.
- **iPad / mobile:** The app works on mobile browsers, but the GitHub web editor workflow is recommended for updates. Use the Upload Files button rather than copy-paste to avoid character corruption.

---

## Development Notes (for contributors)

- All JavaScript uses **ES5** syntax (var, function declarations, string concatenation) for maximum compatibility with the GitHub web editor on iPad/mobile.
- **No CSS custom properties in string values** — the GitHub web editor can corrupt `--variable` syntax in some contexts. Colors are hardcoded as hex values.
- `window.onload` is always the last statement in the script block.
- **No template literals** — single and double quoted strings only.
- The Gemini API is called directly from the browser using the user's key. CORS is supported by Google's Gemini API for browser-based requests.

---

## Roadmap Ideas

- [ ] Multiple saved profiles (toggle between them)
- [ ] Saved search history / past runs
- [ ] Email digest via mailto link
- [ ] Dark/light theme toggle
- [ ] Custom scoring weights
- [ ] CSV export

Pull requests welcome.

---

## License

MIT License — free to use, modify, and distribute.

```
Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
```

---

## Credits

Built with [Google Gemini API](https://ai.google.dev) · Fonts by [Google Fonts](https://fonts.google.com) · [docx.js](https://docx.js.org) for Word export

---

*Job Scouts AI — Open Source — May 2026*
