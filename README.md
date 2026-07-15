# Job Scouts AI

**Free, open source, browser-based AI job search — powered by Google Gemini.**

No backend. No server. No subscriptions. You bring your own free Google AI Studio API key, and everything runs in a single `index.html` file hosted on GitHub Pages.

**Live app:** https://davidfliesen.github.io/jobscoutsai/

---

## What It Does

Job Scouts AI compiles your target companies, skills, locations, preferences, and job sources into a structured AI prompt, sends it to the Google Gemini API directly from your browser, and returns scored job leads as clean, exportable briefing cards.

- **Target lists** — companies, skills & keywords, locations (tag-based, saved automatically)
- **Preferences** — remote/hybrid, relocation, travel, veteran friendly, role types, and more
- **Job sources** — LinkedIn, Indeed, company career pages, ZipRecruiter, Glassdoor, Dice, USAJobs, AngelList/Wellfound, FlexJobs, plus custom sources
- **Resume intelligence** — upload a PDF or paste text; Gemini builds a scoring profile with must-have skills, nice-to-haves, and deal breakers
- **Match scoring** — HOT / WARM / COLD badges, with precise 0–100 numeric scores and score bars when a profile is loaded
- **Live web search** — optional Google Search grounding for real, current postings
- **Exports** — plain text briefing, standalone HTML report, or professional PDF report with live Apply hyperlinks
- **Config portability** — export your full configuration to a `.json` file and import it on another device
- **Debug panel** — inspect the exact prompt, raw API response, and a configuration validation checklist

## Getting Started

1. **Get a free API key** at [Google AI Studio](https://aistudio.google.com/apikey).
2. Open the [live app](https://davidfliesen.github.io/jobscoutsai/).
3. Paste your key into **Settings**, pick a model, and click **Save Settings**.
4. (Optional) Upload or paste your resume to unlock 0–100 numeric scoring.
5. Add companies, skills, and locations. Set your preferences and sources.
6. Click **LAUNCH SCOUT**.

Your API key, settings, and profile are stored only in your browser (localStorage). Nothing is ever sent to any server except Google — using your own key — when you run a scout or analyze a resume.

## Supported Gemini Models

| Option | Model String | Notes |
|---|---|---|
| Recommended | `gemini-3.5-flash` | Best balance of speed and quality (default) |
| Fastest | `gemini-3.1-flash-lite` | High volume, low latency |
| Most detailed | `gemini-2.5-pro` | Slower, best quality |

> **Note:** `gemini-2.0-flash` was shut down on June 1, 2026, and `gemini-2.5-flash` is deprecated for new users. The app automatically migrates old saved model strings to a current model on load.

## Match Scoring

| Badge | Score | Meaning |
|---|---|---|
| 🟢 HOT | 75–100 | Strong match — apply now |
| 🟡 WARM | 50–74 | Good fit — worth a look |
| ⚪ COLD | 0–49 | Partial match — stretch role |

With a resume profile loaded, every lead gets a numeric 0–100 score, a visual score bar, and a brief score breakdown. Without a profile, leads receive qualitative HOT/WARM/COLD ratings only.

## Resume Import

Upload a PDF (parsed natively by Gemini) or paste plain text. If a profile is already loaded, you choose what happens next:

- **Append** — merge new skills, companies, and locations into your existing profile
- **Replace** — overwrite the existing profile completely
- **Cancel** — discard the new resume and keep your current profile

## How It Works

```
Browser (GitHub Pages)
        |
        v
index.html (single static file — all UI, JS, CSS)
        |
        v
Google Gemini API (direct browser call using your own API key)
generativelanguage.googleapis.com/v1beta/models/{model}:generateContent
```

There is no backend and no middleman. The page is pure vanilla HTML/CSS/JavaScript (ES5), hosted free as a static file. Responses are requested as structured JSON (with automatic repair of truncated responses) and rendered as job cards and reports.

## Privacy

- Your API key lives only in your browser's localStorage — never in this repository, never on any server.
- Exported config files contain your API key for portability. Keep them private.
- Your use of the Gemini API is governed by the [Google AI terms of service](https://ai.google.dev/gemini-api/terms).

## Files

| File | Purpose |
|---|---|
| `index.html` | Complete app — all UI, CSS, and JavaScript in one file |
| `logo.png` | Job Scouts AI logo (must sit in the same folder as `index.html`) |
| `README.md` | This documentation |
| `LICENSE` | MIT License |

## Developer

**David Fliesen (SunTzu)** — Hybrid Generative AI & Multimedia Developer, Summerville SC

- Portfolio: https://davidfliesen.github.io
- LinkedIn: https://linkedin.com/in/fliesen/
- GitHub: https://github.com/DavidFliesen
- HuggingFace: https://huggingface.co/SunTzuGamer
- Sisters of Summerville: https://sisters-of-summerville.github.io

## License

Released under the [MIT License](LICENSE). Free to use, copy, modify, and share.

---

*Job Scouts AI — search smarter, not harder.*
