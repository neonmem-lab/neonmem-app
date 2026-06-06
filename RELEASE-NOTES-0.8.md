# Neonmem 0.8.0

**New: gather facts from your docs and code.** Neonmem can now read your existing
documentation and source and keep the *important* facts as connected memory — so your
agent knows your APIs, config and code structure without re-reading the files.

## What's new

- **Fact ingestion** — `neonmem ingest-facts <path>` (and the agent tool
  `neonmem_ingest_facts`) gather structured facts:
  - **Docs** (Markdown / text): API endpoints **and what they do**, config/data values,
    and field definitions — **filler prose is skipped**.
  - **Code** (Python AST): functions/methods + docstrings, a **call graph**
    (who-calls-whom), plus `defined-in` / `part-of` relationships.
  - **Java** (lightweight): classes, methods, dependencies (imports / extends), calls.
  - **PDF / Word / images**: Claude reads them with its own tools and hands the facts to
    Neonmem — no bulky parsers bundled in the app.
- Facts land in the same 3D graph and are recallable like any other memory. Secrets are
  auto-redacted and near-duplicates are skipped.

## Also

- Includes the Windows import-hang stability fix (faiss/WMI).

## Install

Download **Neonmem-Setup-0.8.0.exe** (Windows x64) and run it. Works with **Claude Code**
(full: session-start load + passive capture) and **GitHub Copilot / VS Code**
(experimental).

## License

Free for personal, hobby, research, educational and nonprofit use under the **PolyForm
Noncommercial License**. Commercial use: sales@neonmem.com.
