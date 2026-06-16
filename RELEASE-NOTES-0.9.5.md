# Neonmem 0.9.5

A tougher importer that understands more — plus multi-process file safety.

## Importer / Memory Builder
- **Clear progress + a real "Done" signal.** Big imports now show a progress bar and only say *Done — memory saved* when the cartridge is fully written and released.
- **Can't be interrupted.** The Builder window won't close mid-build, so an import can never be left half-written or collide with a read.
- **Guidance & Max fields explained** right in the UI.

## Smarter imports (our own, fully offline)
- **Cleaner memory.** The loader now skips tables-of-contents, page numbers and headings, stops mislabelling reference text, and keeps the actual definitions.
- **Imports code, not just docs.** Classes, functions and interfaces become memories you can ask about by name.

## Reliability
- Fixed a `[WinError 183] …app.asar` failure on some setups (all components now run from a safe working directory).
- Cartridges open with share-delete + retry, so reads never collide with a save.
- **Cross-process single-writer lock** so the importer, the agent and the visualizer can safely share one cartridge.

## Platforms
- **Linux (AppImage) available**, alongside Windows. macOS is on the way.

---
*Local, private, and yours. Free for personal use.*
