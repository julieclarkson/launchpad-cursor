<p align="center">
  <img src="assets/logo.svg" alt="Git Launcher" width="200"/>
</p>

# Git Launcher

![License](https://img.shields.io/github/license/julieclarkson/git-launcher)
![Version](https://img.shields.io/github/package-json/v/julieclarkson/git-launcher)
![Last Commit](https://img.shields.io/github/last-commit/julieclarkson/git-launcher)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?logo=playwright&logoColor=white)

Your project is built. Now ship it properly.

Git Launcher is an AI agent plugin that reads your finished codebase and generates everything you need to launch on GitHub — a polished README, metadata files, screenshots, architecture diagrams, a social preview image, and platform-specific launch posts for Reddit, Hacker News, Twitter/X, Product Hunt, and Dev.to.

**No API keys. No cloud. No cost.** Runs entirely inside your AI IDE (Cursor, Claude Code, Cowork) using the built-in AI.

## Features

- **Codebase Analysis** — Detects your language, framework, dependencies, and project structure automatically
- **README Generation** — Writes a complete README with badges, features, install instructions, and architecture overview
- **Screenshot Capture** — Uses Playwright to photograph your running app at desktop, tablet, and mobile viewports (or generates a preview page for CLI projects)
- **Architecture Diagrams** — Parses your imports to generate Mermaid component diagrams
- **Social Preview Image** — Renders a branded 1200x630 OG image for GitHub and link sharing
- **Multi-Platform Launch Kit** — Generates tailored posts for Reddit, HN, Twitter/X, Product Hunt, and Dev.to
- **Security Hardened** — Input validation, SSRF prevention, secret scanning, path traversal protection, and optional container isolation

## Prerequisites

- **Node.js >= 18** — for screenshot capture, image generation, and codebase analysis
- **AI IDE** — [Cursor](https://cursor.com), Claude Code, or any IDE with AI agent support

## Quick Start

### 1. Add to your project

```bash
git clone https://github.com/julieclarkson/git-launcher.git .git-launcher
```

### 2. Install dependencies

Open **Terminal**, go to your project folder, then run:

```bash
bash .git-launcher/cursor/install.sh
```

This installs Node dependencies and Playwright Chromium for screenshots.

**What install.sh does:**

1. Runs `npm install` inside `.git-launcher/cursor/`
2. Installs Playwright Chromium (`npx playwright install chromium`)
3. Verifies all dependencies are present

**Having trouble?** If the install fails partway through, run these one at a time:

```bash
cd .git-launcher/cursor && npm install
npx playwright install chromium
```

### 3. Run it

Open your project in your AI IDE and say:

> **"run git launcher"** or **"/git-launch"**

Or tell the agent:

> Read `.git-launcher/cursor/prompts/00-MAIN.md` and execute the workflow.

The agent will analyze your project and generate everything into a `git-launch/` folder.

### 4. Capture screenshots

In **Terminal**, from your project folder:

```bash
node .git-launcher/cursor/scripts/screenshot-runner.js . --preview
```

This adds desktop, tablet, and mobile screenshots to `git-launch/images/`. For web apps, start your dev server first and use `--port 3000` (or your port) instead of `--preview`.

## What Gets Generated

```
git-launch/
├── README.md              # Complete, optimized README
├── CONTRIBUTING.md        # Contributor guide
├── CODE_OF_CONDUCT.md     # Code of conduct
├── LICENSE                # License file
├── ARCHITECTURE.md        # Mermaid diagrams + explanation
├── CASE_STUDY.md          # Technical case study (if Case Study Maker data exists)
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   └── PULL_REQUEST_TEMPLATE.md
├── images/
│   ├── desktop.png       # 1440x900 screenshot
│   ├── tablet.png        # 768x1024 screenshot
│   ├── mobile.png        # 375x812 screenshot
│   └── social-preview.png # 1200x630 OG image
└── LAUNCH_KIT/
    ├── reddit-post.md
    ├── hackernews-post.md
    ├── twitter-thread.md
    ├── producthunt-listing.md
    ├── devto-post.md
    └── github-description.md
```

## Sandbox and Permissions

Git Launcher requires **some operations outside the standard sandbox**. Here's what needs approval and why:

| Operation | Sandbox? | Why it needs approval |
|-----------|----------|----------------------|
| Codebase analysis, README/post generation | Standard sandbox | Reads project files, writes to `git-launch/` |
| `npm install` (dependencies) | Standard sandbox | npm registry is an allowed domain |
| `npx playwright install chromium` | **Needs full network** | Downloads Chromium browser binary (~150MB) from Google CDN |
| Screenshot capture | **May need approval** | Playwright headless browser launch can be blocked by sandbox; may need filesystem access to browser cache |
| Social preview image generation | **May need approval** | Uses headless browser (same as screenshots) |
| `apply-launch.sh` (copy to project root) | Standard sandbox | Writes within project folder |

**Your responsibility:** Cursor and Claude may request expanded permissions (like "full network" or "all") when running install scripts or capturing screenshots. Review each permission prompt carefully and approve only what you understand. You can configure scope settings in your IDE to control what the AI agent is allowed to do.

**Tip:** Run `bash .git-launcher/cursor/install.sh` directly in your terminal (not through the AI agent) to avoid sandbox restrictions on the Chromium download.

## How It Works

1. **Analyze** — Scans your codebase to understand what it does, its tech stack, dependencies, and structure
2. **Generate README** — Writes a complete README with badges, features, install instructions, and architecture overview
3. **Capture Screenshots** — Uses Playwright to take screenshots at 3 viewport sizes (or generates a preview for CLI projects)
4. **Map Architecture** — Parses imports to build component diagrams as Mermaid
5. **Create Social Image** — Renders a branded 1200x630 OG image for GitHub
6. **Write Launch Kit** — Generates platform-specific posts for Reddit, HN, Twitter/X, Product Hunt, and Dev.to
7. **Case Study Integration** — If [Case Study Maker](https://github.com/julieclarkson/case-study-maker) data exists, enriches everything with your build narrative
8. **Demo Integration** — If [Demo Maker](https://github.com/julieclarkson/demo-maker) output exists, embeds platform-specific demo videos

## Tech Stack

| Technology | Purpose |
|------------|---------|
| Node.js | Runtime for scripts |
| Playwright | Screenshot capture and headless browser |
| Sharp | Image generation for social preview |
| Marked | README-to-HTML for CLI preview |

## Companion Plugins

Git Launcher is part of a three-plugin ecosystem:

| Plugin | What it does |
|--------|-------------|
| [Case Study Maker](https://github.com/julieclarkson/case-study-maker) | Captures build reflections, generates case studies |
| [Demo Maker](https://github.com/julieclarkson/demo-maker) | Generates narrated video demos from your codebase |
| **Git Launcher** | Generates README, launch posts, and social assets (you are here) |

**Recommended order:** Case Study Maker → Demo Maker → Git Launcher. Each reads the previous plugin's output.

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
