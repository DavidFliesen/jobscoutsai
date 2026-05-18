# Job Scouts AI

> AI-powered personal job search intelligence — free, open source, runs entirely in your browser.

![Job Scouts AI Logo](logo.png)

**Live Demo:** [https://davidfliesen.github.io/jobscoutsai/](https://davidfliesen.github.io/jobscoutsai/)
**Repository:** [https://github.com/DavidFliesen/jobscoutsai](https://github.com/DavidFliesen/jobscoutsai)

---

## What It Does

Job Scouts AI uses Google's Gemini AI to act as your personal job market analyst. Upload your resume, configure your target companies and skills, and let the AI scout for matching opportunities — returning a ranked, scored briefing you can export as TXT, HTML, or PDF.

No servers. No subscriptions. No data collection. Everything runs in your browser.

---

## Features

- **Resume Upload & AI Parsing** — Upload PDF, TXT, DOC, or paste text. Gemini extracts your skills, experience, and preferences automatically. When a profile is already loaded, a modal dialog offers three options: Append (merge), Replace (overwrite), or Cancel.
- **Numeric Scoring (0–100)** — When a profile is loaded, each lead gets a numeric match score with a visual bar and breakdown text. Without a profile, qualitative HOT / WARM / COLD scoring is used.
- **Configurable Targets** — Set target companies, skill keywords, preferred locations, job sources, and search preferences — all within the browser, no file editing required.
- **Optional Live Web Search** — Toggle Google Search Grounding to pull real-time job listings (uses free-tier quota — see note below). Off by default.
- **Export Results** — Download as TXT (plain text), HTML Report (standalone file), or PDF Report (opens in a new tab with professional layout, score bars, skill tags, and clickable Apply links — print or save as PDF from your browser).
- **Export / Import Config** — Export saves a `.json` file to your downloads folder. Import loads from that file. Includes your API key, all targets, and loaded profile.
- **Privacy First** — Your API key and resume never leave your device. The only external call is directly from your browser to Google's Gemini API using your own key.

---

## Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML / CSS / ES5 JavaScript |
| Fonts | Exo 2, Share Tech Mono (Google Fonts) |
| Hosting | GitHub Pages (static) |
| AI Model | Google Gemini 2.5 Flash (via Gemini API) |
| PDF Parsing | Gemini native PDF support (inline base64) |
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
   Click **Test Connection** to verify the key works before running a scout.

### Free Tier Limits (as of May 2026)

| Resource | Free Tier |
|---|---|
| Requests per day | 1,500 RPD (Gemini 2.5 Flash) |
| Requests per minute | 10–15 RPM |
| Google Search Grounding | ~500 grounding queries/day |
| Cost | $0 — no credit card required |

> **Note on Live Web Search:** The optional "Enable Live Web Search" toggle uses Google's Search Grounding feature. On the free tier this is limited to approximately 500 grounding queries per day, and a single scout run may consume several. If you hit quota errors (`429 Resource Exhausted`), disable live search — the AI will still generate high-quality leads from its training knowledge of companies and the job market.

---

## Deploying to GitHub Pages

### Option A: Upload via GitHub Web (no command line needed)

1. Create a new public repository (e.g. `jobscoutsai`)
2. On the empty repo page, click **"uploading an existing file"**
3. Drag and drop `index.html`, `logo.png`, `LICENSE`, and `README.md` onto the upload area
4. Click **Commit changes**
5. Go to **Settings → Pages**
6. Under **Source**, select **Deploy from a branch**, set branch to `main` and folder to `/ (root)`
7. Click **Save** — your site will be live at `https://yourusername.github.io/jobscoutsai/` within 1–2 minutes

### Option B: Git CLI

```bash
git init
git add index.html logo.png LICENSE README.md
git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/jobscoutsai.git
git branch -M main
git push -u origin main
```

Then enable GitHub Pages in repository Settings → Pages.

---

## File Structure

```
jobscoutsai/
├── index.html      # Complete app — all UI, JS, CSS in one file
├── logo.png        # Job Scouts AI logo (must be in same folder as index.html)
├── LICENSE         # MIT License
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

Use **Export Config** to download a `jobscouts-config-YYYY-MM-DD.json` file to your downloads folder. Use **Import Config** to load from that file on any device — no clipboard needed.

> **Security note:** The exported JSON file includes your API key. Treat it like a password — don't share it publicly, post it online, or commit it to a repository.

---

## Scoring System

| Badge | Score Range | Meaning |
|---|---|---|
| **HOT** (green) | 75–100 | Strong match — apply now |
| **WARM** (amber) | 50–74 | Good fit — worth a closer look |
| **COLD** (grey) | 0–49 | Partial match — stretch role |

With a resume loaded, each lead also shows a numeric 0–100 score, a visual bar, and a 1–2 sentence breakdown explaining why it scored that way.

Without a resume, scoring is qualitative (HOT / WARM / COLD) based on keyword and preference matching.

---

## Choosing a Gemini Model

| Model | Speed | Quality | Notes |
|---|---|---|---|
| **gemini-2.5-flash** (default) | Fast | Excellent | Best for most users |
| **gemini-2.0-flash** | Fastest | Very good | Fallback if 2.5 Flash hits limits |
| **gemini-2.5-pro** | Slower | Best | Use for complex profiles or detailed results |

All three models are available on the free tier. Switch models in the **API Configuration** panel — no restart required.

---

## Troubleshooting

**"Model not found" error**
Make sure you are using one of the three model strings listed above. Old preview model strings (e.g. `gemini-2.5-flash-preview-05-20`) are retired. The app automatically migrates any saved old strings on load.

**"Scout error: Unterminated string in JSON"**
The AI response was truncated before it finished. The app will attempt to repair and display whatever leads completed successfully. To prevent this: reduce the number of target companies and skill keywords, or switch from Gemini 2.5 Pro to Gemini 2.5 Flash.

**"429 Resource Exhausted"**
You have hit the free tier rate limit. Wait 60 seconds and try again. If it persists, disable Live Web Search in the API Configuration panel.

**Results are slow to appear**
Gemini 2.5 Flash typically responds in 10–20 seconds. Gemini 2.5 Pro may take 30–60 seconds for complex profiles. The radar animation confirms the scout is running.

**Logo not showing**
The `logo.png` file must be in the same folder as `index.html`. The nav bar text "JOB SCOUTS AI" is always visible as a fallback and links back to the top of the page.

---

## Privacy

- **Your API key** is stored only in your browser's `localStorage` and sent only to `generativelanguage.googleapis.com` — Google's Gemini API — with your requests.
- **Your resume** is processed in-memory. The parsed profile data (not the original file) is optionally stored in `localStorage`. Resume content is sent to the Gemini API for analysis.
- **No data** is sent to any third-party servers. This project has no backend, no analytics, and no tracking of any kind.
- **Google's free tier** may use request data to improve Google products. To opt out, upgrade to a paid Gemini API plan. See [Google AI terms](https://ai.google.dev/gemini-api/terms).

---

## Development Notes (for contributors)

- All JavaScript uses **ES5** syntax — `var`, `function(){}`, string concatenation — for maximum compatibility with the GitHub web editor on iPad and mobile.
- **No CSS custom properties** (`--variable`) in hardcoded color strings — hex values are used throughout to avoid corruption by the GitHub web editor.
- `window.onload` is always the last statement in the `<script>` block.
- **No template literals** — single and double quoted strings only.
- The Gemini API supports browser-based CORS requests, so no backend proxy is needed.
- All configuration is in-browser. Users never need to edit the source file directly.

---

## Roadmap Ideas

- [ ] Multiple saved profiles (switch between them)
- [ ] Saved search history / past runs
- [ ] CSV export
- [ ] Custom scoring weights per skill
- [ ] Dark mode toggle
- [ ] Email digest via mailto link

Pull requests welcome.

---

## License

MIT License — free to use, modify, and distribute.

```
MIT License

Copyright (c) 2026 David Fliesen
https://github.com/DavidFliesen/jobscoutsai

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Developer

**David Fliesen** — Hybrid Generative AI & Multimedia Developer, Summerville, SC

David has 20+ years in multimedia production, U.S. Navy Combat Camera service, and DoD simulation and virtual agent work. He now builds AI-powered tools at the intersection of generative AI, multimedia, and defense/enterprise applications — including agentic pipelines, conversational avatars, and open source utilities like Job Scouts AI.

| | |
|---|---|
| 🌐 Portfolio | [davidfliesen.github.io](https://davidfliesen.github.io) |
| 💼 LinkedIn | [linkedin.com/in/fliesen](https://linkedin.com/in/fliesen/) |
| 🐙 GitHub | [github.com/DavidFliesen](https://github.com/DavidFliesen) |
| 🐾 Sisters of Summerville | [sisters-of-summerville.github.io](https://sisters-of-summerville.github.io) |

---

## Credits

Built with [Google Gemini API](https://ai.google.dev) · Fonts by [Google Fonts](https://fonts.google.com)

---

*Job Scouts AI — Open Source — May 2026*
