# Neonmem 0.9.0

**Your memory becomes a cartridge — and grows a mind of its own.** Neonmem 0.9 turns the
memory from a graph of notes into a self-contained **memory cartridge**: one local
`.neonmem` file that carries the reasoning graph, a comprehension layer that *understands*
your project, and a small model trained on your own memory — all offline, all yours. And it
renders as a living brain you watch fill in as your agent learns.

## What's new

### 🧩 A memory cartridge, not just a graph
One `.neonmem` file now holds three things together, offline:
- the **reasoning graph** (decisions, dead-ends, rules, plans, and how they connect),
- a **comprehension layer** that understands how it all fits, and
- a **small model** trained on your own memory.

Load it and your agent is instantly up to speed. Back it up, move it between projects, keep
it forever — it's yours, on your disk, not a pile of notes in someone's cloud.

### 🧠 A comprehension layer
Neonmem clusters every memory into **subsystems** and distils a **skeleton + resume cursor** —
the shape of the project and the exact thread you left open. A fresh session is handed the
whole understanding at once, instead of a cold scroll-back. It's built automatically when the
memory consolidates (`dream`) or when you ingest docs, and it travels inside the cartridge.

### 🧭 Plans — where you're going
A new **PLAN** node type captures intent: immediate next-steps and long-running goals. So your
agent knows not just what happened and *why*, but the **direction**. Active plans resist
fading; when a plan is achieved, replaced, or abandoned it settles cleanly into the record
(a win, a superseded note, or a dead-end) — never lost, never confused.

### 🤖 Small models, built in — no third-party LLM
Three compact, **self-built** models — trained on *your* memory — now ride inside the
cartridge:
- **importance** — ranks what actually matters,
- **warmth/tone** — senses frustration and urgency so corrections stick,
- **capture-typing** — types what's worth remembering as you work.

They generalise beyond hand-written rules, stay fully **offline**, and use **no third-party
LLM** — your project never leaves your machine.

### 🌌 Living brain visualization
Every memory renders as an anatomical brain — two hemispheres around a bright reflex core —
that starts nearly empty and fills in, neuron by neuron, as your agent learns. New in 0.9:
colour the brain by **subsystem** to see the comprehension layer, a glowing **coherence core**,
and dendrite arbors on every node. A deep performance pass keeps memories with **thousands of
nodes** loading and orbiting smoothly.

### 📚 A smarter importer
Point Neonmem at your docs and code and it gathers the important facts **and now the plans**
(roadmaps, goals, next-steps) — building an understanding-ready memory from the very first load.

## Also

- **Signed installer & app** — the installer and app executables are now code-signed.
- Offline and private throughout — no cloud calls, no API cost.
- Quality: **461 automated tests** (engine, comprehension, models, the built exe, MCP over
  stdio, and full Electron install/launch smoke tests) pass on this build.

## Install

Download **Neonmem-Setup-0.9.0.exe** (Windows x64) and run it, or grab the
**neonmem-0.9.0-portable.tar.gz** for locked-down PCs (no installer, no SmartScreen prompt).
Works with **Claude Code** (full: session-start load + passive capture) and **GitHub Copilot /
VS Code** (experimental).

## License

Free for personal, hobby, research, educational and nonprofit use under the **PolyForm
Noncommercial License**. Commercial use: sales@neonmem.com.
