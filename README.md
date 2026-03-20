# Launchpad for Cursor

**Three Cursor plugins that work together to document, demo, and launch your project.**

Build your app normally. Case Study Maker captures your decisions. Demo Maker generates narrated videos. Git Launcher creates everything you need to ship on GitHub. Each plugin feeds into the next — install all three and they integrate automatically.

## What's Included

| Plugin | What it does | Activate |
|--------|-------------|----------|
| **[Case Study Maker](https://github.com/julieclarkson/case-study-maker)** | Captures build decisions in real time and generates portfolio case studies, marketing pages, and embeddable cards | `bash .launchpad/case-study-maker/csm-init` then **"activate case study maker"** |
| **[Demo Maker](https://github.com/julieclarkson/demo-maker)** | Generates 7 platform-ready narrated video demos (Full, GitHub, Twitter, Product Hunt, Instagram, TikTok, GIF) | Copy rule, then **"make a demo"** |
| **[Git Launcher](https://github.com/julieclarkson/git-launcher)** | Generates README, screenshots, architecture diagrams, social preview, and launch posts for Reddit, HN, Twitter, Product Hunt, Dev.to | `bash .launchpad/git-launcher/gl-init` then **"run git launcher"** |

## Install

> **Important:** Clone this bundle _inside_ the project you want to launch.

### Quick Start (all three plugins)

```bash
cd ~/my-awesome-app
git clone https://github.com/julieclarkson/launchpad-cursor.git .launchpad

# 1. Case Study Maker
bash .launchpad/case-study-maker/csm-init

# 2. Demo Maker
mkdir -p .cursor/rules
cp .launchpad/demo-maker/.cursor/rules/demo-maker.mdc .cursor/rules/

# 3. Git Launcher
bash .launchpad/git-launcher/gl-init
```

### Or install individually

```bash
git clone https://github.com/julieclarkson/case-study-maker.git .case-study-maker
bash .case-study-maker/cursor/csm-init

git clone https://github.com/julieclarkson/demo-maker.git .demo-maker-plugin
mkdir -p .cursor/rules
cp .demo-maker-plugin/cursor/.cursor/rules/demo-maker.mdc .cursor/rules/

git clone https://github.com/julieclarkson/git-launcher.git .git-launcher
bash .git-launcher/cursor/gl-init
```

## Recommended Workflow

| Step | Command | What happens |
|------|---------|-------------|
| **1. Build** | Say **"activate case study maker"** | AI partner watches your coding sessions, prompts reflection questions at decision moments |
| **2. Capture** | `/capture` or `/auto-capture` | Save reflections about constraints, tradeoffs, risks, security, and iteration |
| **3. Demo** | Say **"make a demo"** | 9-step pipeline: analyze → script → storyboard → capture → narrate → render → cutdowns |
| **4. Generate** | `/generate` | Choose template, theme, tone → get portfolio and marketing pages with embedded demo videos |
| **5. Launch** | Say **"run git launcher"** or `/gl` | README, screenshots, architecture, social preview, launch posts for 5 platforms |
| **6. Deploy** | `/send-to-pages` | Push case study pages to GitHub Pages |

## All Commands

### Case Study Maker

| Command | What it does |
|---------|-------------|
| `/csm` | Show all commands and current status |
| `/activate` | Initialize case study tracking |
| `/capture` | Capture a reflection |
| `/auto-capture` | Draft reflections from conversation and commits |
| `/review` | Review coverage and identify gaps |
| `/generate` | Generate a case study page |
| `/generate-portfolio-card` | Generate an embeddable portfolio card |
| `/generate-custom` | Generate for any installed category |
| `/customize` | Change template, theme, tone, colors, fonts |
| `/install-template` | Install premium or custom template packs |
| `/send-to-pages` | Copy outputs to GitHub Pages |

### Demo Maker

| Command | What it does |
|---------|-------------|
| **"make a demo"** | Start the full 9-step demo pipeline |
| **"dm-init"** | Initialize Demo Maker without starting a demo |

### Git Launcher

| Command | What it does |
|---------|-------------|
| **"run git launcher"** | Start the full pipeline |
| `/git-launch` | Start the full pipeline |
| `/gl` | Alias for `/git-launch` |

## Requirements

| Requirement | Used by | Required? |
|------------|---------|-----------|
| **Node.js 18+** | All three plugins | Yes |
| **FFmpeg** | Demo Maker | Yes (for video) |
| **Playwright Chromium** | Demo Maker, Git Launcher | Yes (installed by init scripts) |
| **ElevenLabs API key** | Demo Maker | Optional (skip for caption-only mode) |
| **GitHub CLI (`gh`)** | Demo Maker | Optional (for GitHub Release publish) |

## Security

All three plugins run locally. No data leaves your machine unless you explicitly publish.

**Safeguards across all plugins:**

- **Scope boundary** — all reads and writes are confined to the project root
- **Zero dependencies** (Case Study Maker) — no npm packages, no supply chain risk
- **Secret scanning** (Git Launcher) — blocks `.env`, credentials, and API keys from generated output
- **SSRF prevention** (Demo Maker, Git Launcher) — capture URLs restricted to localhost only
- **CSP headers** — all generated HTML includes Content-Security-Policy meta tags
- **Shell safety** — hook scripts use `execFileSync` with argv arrays to prevent injection

**Your responsibility:**

- **Manage IDE scope and permissions.** Cursor will request expanded permissions for Playwright downloads, narration API calls, headless browser rendering, and GitHub publishing. Review each prompt and approve only what you understand.
- **Store API keys securely.** Use `.demo-maker/.env` (gitignored) or a secrets manager like 1Password CLI (`op read`). Never paste keys into chat.
- **Install system dependencies in your terminal.** Run init scripts and `brew install ffmpeg` directly — not through the AI agent — to avoid unnecessary sandbox escalation.
- **Review generated content before publishing.** Launch kit posts and README are AI-generated. Case study reflections are your own words, but generated pages should be checked.

## Structure

```
case-study-maker/   — Cursor plugin for case studies and portfolios
demo-maker/         — Cursor plugin for narrated video demos
git-launcher/       — Cursor plugin for GitHub launch assets
```

## Links

- [Case Study Maker](https://github.com/julieclarkson/case-study-maker)
- [Demo Maker](https://github.com/julieclarkson/demo-maker)
- [Git Launcher](https://github.com/julieclarkson/git-launcher)
- [Claude version of this bundle](https://github.com/julieclarkson/launchpad-claude)
