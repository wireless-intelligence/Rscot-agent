# Rscot-agent

A self-hosted, multi-vertical AI **coding agent** — runs on your own machine, switchable across LLM providers, code stays local.

🌐 **Live demos** — see what it builds: **<https://learningfind.com/>**

---

## What it is

Rscot-agent (a.k.a. Recot Code Agent) is a full-stack AI coding workbench. You give it a prompt, it plans, edits files, runs commands, reads logs, fixes its own mistakes, and ships working software. It ships in three forms:

| Form factor | What it is | Best for |
|---|---|---|
| **Desktop app (`.msi`)** | Standalone Tauri window, native chrome | Daily driver, full living-UI |
| **VSCode extension (`.vsix`)** | Webview panel inside VSCode | Pair-programming inside your editor |
| **Headless CLI** | Single `cwa` binary | Scripts, CI, batch runs |

All three share the same backend, same tools, same provider routing.

---

## Features

- **5 LLM providers, one interface** — DeepSeek · OpenAI · Anthropic · OpenRouter · Ollama. Per-provider API key storage in OS keychain. Anthropic uses native `/v1/messages` translator; the rest are OpenAI-compatible.
- **Fine-grained permissions** — 5 tool categories × 3 policies (auto / ask / deny). File reads default auto; shell commands and writes default ask; you can lock down or open up per workspace.
- **Cross-session memory** — last week's fix auto-recalled this week in the same workspace.
- **Real web search** — three-way fan-out: You.com → Brave → Wikipedia. Falls back gracefully when any source errors.
- **Knowledge layer** — 17 stack templates (FastAPI / Next.js / Flutter / PyTorch / Rust CLI / …) auto-inject conventions so the agent ships idiomatic code.
- **Session management** — saved conversations with rename / delete / fork / pin / archive / search / Markdown+JSON export.
- **Living UI (desktop edition)** — Memory Bank visualization, Digital Twin orb, streaming particles, tool execution rings, activity heartbeat sparklines. Light + dark themes auto-switch.
- **Git checkpoint** — every session is a non-destructive checkpoint; `done` produces a whitelist-based commit that never touches files the agent didn't write.
- **Local everything** — code, memory database, stack snapshots all stay on your machine. Only the prompt body goes to the LLM API you chose.

---

## What it can build

`41` self-contained HTML demos are live at **<https://learningfind.com/>** — every one was produced by Rscot-agent in a single session. Categories:

- **GPU shaders** — Aurora, fluid sim, raymarching, Mandelbrot, fractal
- **Physics + simulation** — N-body gravity, boids, reaction-diffusion, DNA
- **Games** — 2048, Tetris, Snake3D, Doom, Breakout, Asteroids, Racing, Maze3D
- **3D / WebGL** — voxel worlds, terrain, globe, nebula, ocean, starship
- **Algorithms** — Wave Function Collapse, Lisp interpreter
- **Audio** — synth, audio visualizer, music video, text-morph
- **UI case studies** — TikTok / Instagram / Spotify / Smart-home dashboards
- **Robotics** — Unitree Go2 quadruped 3D viz with real OBJ meshes

Plus full-stack work: API endpoints, test suites, refactors, debugging, devops scripts, container management.

---

## Quick start

```bash
git clone https://github.com/wireless-intelligence/Rscot-agent.git
cd Rscot-agent

# Backend (FastAPI, port 8010)
cd backend && pip install -r requirements.txt
uvicorn app.main:app --port 8010 --reload

# Desktop app
cd desktop/tauri-shell && npm install && npm run tauri:build
# → src-tauri/target/release/bundle/msi/Code\ Workspace\ Agent_*.msi

# VSCode extension
cd desktop/vscode-extension && npm install && npm run build
npx vsce package
# → code-workspace-agent-*.vsix
code --install-extension code-workspace-agent-*.vsix --force

# Headless CLI
cd desktop/vscode-extension
node dist/cli.js "refactor utils/format.py into a dispatch table"
```

Set your LLM key once via the desktop app's `🔑` button or `Code Workspace: Set LLM API Key (Per Provider)` in VSCode.

---

## Architecture

```
┌────────────────────────────────────────────────────────────┐
│  Clients          Desktop (Tauri)   VSCode ext   CLI       │
│                          │              │         │        │
│                          └──────┬───────┴─────────┘        │
│                                 ▼                          │
│                      FastAPI backend  :8010                │
│                                 │                          │
│           ┌─────────────────────┼─────────────────────┐    │
│           ▼                     ▼                     ▼    │
│      Tool runtime        Provider adapter      Knowledge   │
│   (write_file / shell)  (5 providers, 1 API)    (17 stacks)│
└────────────────────────────────────────────────────────────┘
```

- **Frontend**: TypeScript + Preact (VSCode) / React + Tauri (desktop)
- **Backend**: Python 3.11 + FastAPI + httpx
- **LLM transport**: streaming SSE, retry-with-backoff, three-source web search
- **Storage**: local JSON sessions in `.cwa/conversations/`, no database required

---

## Links

- 🌐 **Live demos / showcase**: <https://learningfind.com/>
- 📦 **GitHub**: <https://github.com/wireless-intelligence/Rscot-agent>

---

## License

Open source. Free for personal use.

---

> Rscot-agent — your codebase, your terminal, your agent. Local-first. Provider-agnostic.
