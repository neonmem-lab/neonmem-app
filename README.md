<h1 align="center">Neonmem</h1>

<p align="center"><strong>A living memory for your AI agent.</strong></p>

<p align="center">
So it learns you and your project and works like a colleague who actually knows you —
remembering every decision, idea and dead-end. Local · private · yours.
</p>

<p align="center">
  <a href="https://github.com/stmedvid-ailab/neonmem-app/releases/latest"><strong>⬇ Download for Windows</strong></a>
  ·
  <a href="https://neonmem.com">neonmem.com</a>
  ·
  <a href="https://neonmem.com/#journeys">See the journeys</a>
  ·
  <a href="https://neonmem.com/report">Report a bug</a>
</p>

<p align="center">
  <img src="assets/labyrinth-1.png" alt="Neonmem's living memory, visualized in 3D" width="760">
</p>

> **Public beta (v0.7).** Windows only for now; macOS & Linux are on the way.

---

## What it is

Your agent forgets your project between sessions. Neonmem gives it a **living,
dynamic memory** — it grows as you work, holds the *why* behind decisions, and
turns the assistant into a colleague who's genuinely been there with you.

- 🧠 **A real graph, not a flat log** — decisions, observations, rules and how they connect.
- 🚫 **Remembers dead-ends** — failed approaches stay recorded, so they aren't re-suggested.
- 💬 **Debates & resolutions** — the reasoning, not just the verdict.
- 🌙 **Dreams** — a consolidation pass that decays noise and keeps what matters.
- 🕰️ **Time-travel** — "what did we do three days ago?"
- 👁️ **You can see it** — a real-time 3D view of memory forming, recalling, consolidating.
- 🔒 **Local & private** — offline, no cloud, no API cost; memory is a portable file on your machine.
- 🛡️ **Tamper-proof** — binary and agent-write-only by design.

It isn't just for code: the same agent can run a tricky DevOps migration or help
you write a screenplay — and Neonmem remembers all of it. See the full
[journeys](https://neonmem.com/#journeys).

## Works with

| Agent | Status |
|---|---|
| **Claude Code** | ✅ Full support (deliberate memory **+** passive per-turn capture) |
| **GitHub Copilot / VS Code** | 🧪 Experimental (the deliberate memory tools) |
| More agents | 🔜 Coming soon |

## Install

1. **[Download the installer](https://github.com/stmedvid-ailab/neonmem-app/releases/latest)** (Windows x64).
2. Run it — it detects Claude Code (or point it at your install) and registers
   automatically. Optionally tick **GitHub Copilot (experimental)** for VS Code.
3. Open Claude Code and just work — Neonmem loads your memory at session start.
4. Launch the **Neonmem** app from the Start menu to watch the brain.

Uninstall cleanly from **Add/Remove Programs** (it un-registers itself and keeps
your memory). Misbehaving? `neonmem disable` turns it off without uninstalling.

See [RELEASE-NOTES-0.7.md](RELEASE-NOTES-0.7.md) for what's in this build.

## Report a bug

Full instructions (including where to find your logs) are at
**[neonmem.com/report](https://neonmem.com/report)** — or
[open an issue](https://github.com/stmedvid-ailab/neonmem-app/issues/new/choose),
or email **support@neonmem.com**.

## License

**Free** for personal, hobby, research, educational and nonprofit use under the
[PolyForm Noncommercial License](LICENSE). **Commercial use requires a license** —
see [COMMERCIAL.md](COMMERCIAL.md) or email **sales@neonmem.com**.

Bundled third-party components keep their own licenses — see
[THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md) and
[ACKNOWLEDGEMENTS.md](ACKNOWLEDGEMENTS.md).

> This repository hosts the **downloads and documentation**. The source is not public.
