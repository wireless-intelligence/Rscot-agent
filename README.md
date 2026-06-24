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

Rscot-agent is released under a dual-license model.

Community License

The open-source community version is licensed under the GNU Affero General Public License v3.0 (AGPL-3.0).

You may use, study, modify, and redistribute Rscot-agent under the terms of the AGPL-3.0. If you modify Rscot-agent and make it available as a network service or hosted product, you must make the corresponding source code available under the same license.

Commercial License

A commercial license is available for individuals, teams, and companies that want to use Rscot-agent in proprietary, closed-source, enterprise, SaaS, consulting, or commercial products without the obligations of the AGPL-3.0.

For commercial licensing, please contact us

Trademark Notice

“Rscot-agent” and “Recot Code Agent” are project names of the original author. The license does not grant permission to use these names, logos, or branding to imply endorsement or official affiliation.
