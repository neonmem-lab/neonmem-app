# Neonmem 0.9.6

Imported knowledge that answers — even after you close and reopen the project.

## Imports that stay answerable
- **The importer's understanding now travels inside the cartridge.** When you import docs, Neonmem trains a small model on *your* material so it can answer "what is X?" from it. That model now rides inside the single `.neonmem` file — so after you close and reopen a project, recall still finds the right answer, not just right after the import.
- **No more dim-mismatch dead recall.** Reopened, imported cartridges search with the same model their memories were built with, so semantic recall keeps working instead of silently falling back to noise.

## Reliability
- **Procedures & rules recall without erroring.** Fetching a saved how-to or rule no longer hits an internal error.
- **Memory survives an auto-compact.** Your memory is saved *before* a session compacts and reloaded after — so a long session never loses its thread.
- **Single, clean memory file.** The cross-process write-lock now lives outside the cartridge folder (keyed by path), so your memory stays one tidy `.neonmem` file while the importer, the agent and the visualizer share it safely.

## Platforms
- Windows, Linux (AppImage), with a Windows Store build in the pipeline. macOS on the way.

---
*Local, private, and yours. Free for personal use.*
