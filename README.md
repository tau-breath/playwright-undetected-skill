<p align="center">
  <strong>🚀 Continued in <a href="https://github.com/tau-breath/tauright">TAURIGHT</a></strong>
</p>

> **This project is now consolidated into [TAURIGHT](https://github.com/tau-breath/tauright).**  
> New browser-runtime development, persistent multi-session profiles, same-profile concurrent lanes, fast local snapshots/actions, tab/session management, and automatic stable Patchright updates continue there.  
> This repository remains public as a focused historical/reference implementation.

# Playwright Undetected Skill

A Claude Code skill for browser automation with bot detection bypass. Built on [patchright](https://github.com/AresS31/patchright) (undetected playwright fork).

## Features

- Localhost and private IP support
- Bot detection bypass (Cloudflare, reCAPTCHA, etc.)
- Session persistence via server mode
- Full browser automation (navigate, click, type, screenshot)
- Claude Code skill integration

## Installation

### 1. Install patchright

```bash
pip install patchright
patchright install chromium
```

### 2. Copy skill to Claude Code

```bash
# Copy to your Claude Code skills directory
cp -r playwright-undetected-skill ~/.claude/skills/playwright-undetected
```

### 3. Verify installation

```bash
cd ~/.claude/skills/playwright-undetected
python server.py start &
python server.py status
python server.py stop
```

## Quick Start

```bash
cd ~/.claude/skills/playwright-undetected

# Start server (keeps browser session alive)
python server.py start &
sleep 2

# Navigate to your local dev server
python server.py call '{"tool": "navigate", "args": {"url": "http://localhost:3000"}}'

# Take a screenshot
python server.py call '{"tool": "screenshot", "args": {"path": "screenshot.png", "full_page": true}}'

# Click an element
python server.py call '{"tool": "click", "args": {"selector": "#my-button"}}'

# Type into input
python server.py call '{"tool": "type", "args": {"selector": "#email", "text": "test@example.com"}}'

# Stop server when done
python server.py stop
```

## Server Commands

| Command | Description |
|---------|-------------|
| `python server.py start &` | Start server in background |
| `python server.py stop` | Stop server |
| `python server.py status` | Check server status |
| `python server.py call '{...}'` | Call a tool |

## Available Tools

| Tool | Description | Arguments |
|------|-------------|-----------|
| `navigate` | Go to URL | `url` (required) |
| `screenshot` | Save screenshot | `path`, `full_page` |
| `click` | Click element | `selector` (required) |
| `type` | Type into input | `selector`, `text` (required) |
| `get_text` | Get element text | `selector` (required) |
| `get_url` | Get current URL | - |
| `get_title` | Get page title | - |
| `wait_for` | Wait for element | `selector`, `timeout` |
| `launch` | Start browser | `headless` |
| `close` | Close browser | - |

## Why Server Mode?

The executor.py script runs as a separate process each time, losing browser state between calls. Server mode keeps a persistent browser session:

```
Without server mode:
  Call 1: navigate -> browser opens -> process ends -> browser closes
  Call 2: screenshot -> ERROR: no browser!

With server mode:
  Start server: browser session created
  Call 1: navigate -> works
  Call 2: screenshot -> works (same session!)
  Call 3: click -> works
  ...
  Stop server: browser closes
```

## Use Cases

- Local development testing
- QA automation for internal apps
- E2E testing on localhost
- Screenshot capture for documentation
- Form testing and validation
- UI interaction verification

## Requirements

- Python 3.8+
- patchright
- Google Chrome installed

## License

MIT

## Credits

- [patchright](https://github.com/AresS31/patchright) - Undetected Playwright fork

---

## DPA - Decentralized Protection Alliance

**Freedom without surveillance, protection for everyone.**

[dpa.network](https://dpa.network) | [contact@dpa.network](mailto:contact@dpa.network) | [Matrix](https://matrix.to/#/#dpa_network:matrix.org) | [Telegram](https://t.me/dpa_network)
