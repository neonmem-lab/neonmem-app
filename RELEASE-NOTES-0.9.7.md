# Neonmem 0.9.7

The big one: a **two-level importer** that turns your project into a memory an AI agent can actually answer from — and an offline embedder that makes recall **grounded**, not guessed.

## Two ways in, two kinds of memory
Neonmem now understands that "your stuff" comes in two shapes, and treats each correctly:

- **Folders & files → a searchable knowledge pool.** Your docs, code and notes are vectorised into a lossless, deduplicated facts pool. Ask *"what is EAI?"* and the answer comes from **your documents**, word-grounded — no hallucination.
- **Agent chats → actual memories.** Point Neonmem at a Claude/agent transcript and it extracts the **decisions, dead-ends and rules** from the conversation as clean, typed memories — not a flat dump. A decision stays a decision; a dead-end stays a warning.
- **Links become knowledge.** If a chat references a file on disk, that file is pulled into the pool automatically, with a memory that points back to it.

## Grounded, offline recall
- **IBM Granite-30M embeddings** run as fused **fp16 ONNX** through **ONNX Runtime** — Qdrant-class retrieval quality, on **any CPU**, with **no GPU, no PyTorch, no API key, no cloud**.
- Every prompt checks memory in order — reflexes → short-term → long-term → facts pool — so the agent answers from what you imported, or honestly says it doesn't know.
- **Concept tags that stick.** Tag an import with a topic (e.g. `Site API`) and Neonmem mints one clean, canonical memory linked to the source — even when your docs never name it verbatim.

## Clean by construction
- Memories follow one **golden rule**: a single concise statement (`EAI — Ericsson Adaptive Inventory`) linked to the full source — no messy raw-chunk pile.
- Chat capture filters out process-narration and directives ("I read…", "please check…") and **deduplicates** through the same facts layer, so re-importing never doubles up.

## One durable cartridge
- The importer keeps the **full source corpus** inside the cartridge (content-addressed + compressed) — one file replaces the scattered docs and transcripts, and the facts are always rebuildable from ground truth.
- **Opt-in encryption at rest** (AES-256-GCM) — your whole corpus as a private vault.
- Imported knowledge is long-term and **survives reopening** the project.

## Importer UI
- A clear split: **folders/files** (→ pool) vs **Agent chat** (→ memories), with honest result labels: **Facts loaded** and **Memories created**.
- Click-to-toggle tag chips, a smaller always-open legend, and a Collections view that groups the pool by source.

## Built on (all open, permissively licensed)
- Embeddings: **IBM Granite-30M** (Apache-2.0) via **ONNX Runtime** (MIT). Vector search: **FAISS** (MIT). Agent integration: **Model Context Protocol**. Full attributions ship with every download.

## Platforms
- Windows (signed installer + portable), Linux (AppImage), Windows Store build in the pipeline. macOS on the way.

---
*Local, private, and yours. Free for personal use.*
