# Neonmem 0.9.0

**Your memory becomes a cartridge — and grows a mind of its own.** Neonmem 0.9 turns
the memory from a graph of notes into a self-contained **memory cartridge**: one local
`.neonmem` file that carries the reasoning graph, a comprehension layer that *understands*
your project, and a small model trained on your own memory — all offline, all yours. And
it renders as a living brain you watch fill in as your agent learns.

## What's new

- **A memory cartridge, not just a graph.** One `.neonmem` file now holds three things
  together: the reasoning graph, the comprehension layer, and a small self-built model.
  Load it and your agent is instantly up to speed — back it up, move it between projects,
  keep it forever.
- **Comprehension layer.** Neonmem clusters every memory into **subsystems** and distils a
  **skeleton + resume cursor** — the shape of the project and the exact thread you left
  open. A fresh session is handed the whole understanding at once, instead of a cold
  scroll-back.
- **Plans — where you're going.** A new **PLAN** node type captures intent (immediate
  next-steps and long-running goals), so your agent knows not just what happened and why,
  but the direction. Plans resist fading while active; when one is achieved, superseded or
  abandoned it settles cleanly into the record.
- **A small mind, built in.** Three compact models — trained on *your* memory, with **no
  third-party LLM** — rank what matters, sense tone, and type what's captured. They travel
  inside the cartridge.
- **Living brain visualization.** Every memory renders as an anatomical brain — two
  hemispheres around a bright reflex core — that starts nearly empty and fills in, neuron
  by neuron. A deep performance pass keeps thousands of nodes loading and orbiting smoothly.
- **Smarter importer.** Point Neonmem at your docs and code and it gathers the important
  facts *and now the plans* (roadmaps, goals, next-steps), building an understanding-ready
  memory from the start.

## Also

- Comprehension is built automatically on consolidation (`dream`) and ingestion, and is
  carried inside the binary cartridge (no sidecar files).
- Offline and private throughout — no cloud calls, no API cost.

## Install

Download **Neonmem-Setup-0.9.0.exe** (Windows x64) and run it, or grab the
**neonmem-0.9.0-portable.tar.gz** for locked-down PCs (no installer, no SmartScreen
prompt). Works with **Claude Code** (full: session-start load + passive capture) and
**GitHub Copilot / VS Code** (experimental).

## License

Free for personal, hobby, research, educational and nonprofit use under the **PolyForm
Noncommercial License**. Commercial use: sales@neonmem.com.
