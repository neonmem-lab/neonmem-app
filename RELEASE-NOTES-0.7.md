# Neonmem 0.7.0 — Public Beta

**A living memory for your AI agent** — so it learns you and your project and
works like a colleague who actually knows you. Local, private, and you can watch
it think in 3D.

## Highlights
- **Living, procedural memory** — decisions, dead-ends, debates and rules captured
  as a connected graph (13 node types), not a flat log.
- **Works with Claude Code** (full: session-start load **+ passive per-turn
  capture**) and **GitHub Copilot / VS Code** (experimental: the deliberate memory
  tools).
- **3D "cyber-brain" visualizer** — watch memory form, recall, and consolidate.
- **Dreams** — a consolidation pass that decays noise, merges duplicates, and
  promotes what matters.
- **Time-travel recall** — "what did we do three days ago?"
- **Local & private** — offline embeddings, no cloud, no API cost; memory is a
  portable file on your machine.
- **Tamper-proof memory** — binary and agent-write-only by design.
- **Native Windows installer** — Start-menu icons, PATH, clean uninstaller.
- **Safety** — an emergency **disable** switch (`neonmem disable`) and local logs
  (`neonmem logs`).

## Install
Download **Neonmem-Setup-0.7.0.exe** (Windows x64) and run it. It detects Claude
Code (or point it at your install) and registers automatically. Optionally tick
**GitHub Copilot (experimental)** for VS Code.

## Known limitations
- **Windows only** this release (macOS and Linux are on the way).
- **GitHub Copilot is experimental** — the deliberate memory tools work, but
  passive per-turn capture is Claude Code only (Copilot has no session hook).
- This is a **public beta** — please report anything rough (see below).

## Report a bug
Logs: run `neonmem logs` (or `neonmem logs --path`). File it at
https://github.com/stmedvid-ailab/neonmem-app/issues or email support@neonmem.com.
Full instructions: https://neonmem.com/report

## License
Free for personal, hobby, research, educational and nonprofit use under the
**PolyForm Noncommercial License**. Commercial use requires a license —
sales@neonmem.com. Bundled components keep their own licenses; see
THIRD-PARTY-NOTICES.md and ACKNOWLEDGEMENTS.md.
