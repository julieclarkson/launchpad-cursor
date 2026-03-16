# Launchpad for Cursor

Three Cursor plugins that work together to build, document, demo, and launch your project.

## What's Included

| Plugin | What It Does |
|--------|-------------|
| **Case Study Maker** | Captures your build decisions and generates marketing pages, portfolio case studies, and pitch decks |
| **Demo Maker** | Creates narrated video demos of your product for every platform |
| **Git Launcher** | Generates launch-ready GitHub assets — README, screenshots, architecture docs, social previews, and multi-platform launch posts |

## Recommended Workflow

```
1. Build your project with Case Study Maker capturing reflections
   /activate-case-study-maker

2. Generate narrated demo videos
   /activate-demo-maker → "make a demo"

3. Generate case study pages (auto-embeds demo videos if available)
   /generate

4. Create launch kit for every platform
   /git-launch
```

## Install

### Option A: Clone this bundle (all three plugins at once)

```bash
cd your-project/
git clone https://github.com/julieclarkson/launchpad-cursor.git .launchpad
```

Then copy the plugin directories you want into your project root.

### Option B: Install individually

```bash
git clone https://github.com/julieclarkson/case-study-maker.git .case-study-maker
# Use: cursor/ directory

git clone https://github.com/julieclarkson/demo-maker.git .demo-maker
# Use: cursor/ directory

git clone https://github.com/julieclarkson/git-launcher.git .git-launcher
# Use: cursor/ directory
```

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
