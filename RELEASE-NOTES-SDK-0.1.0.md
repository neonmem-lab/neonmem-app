# Neonmem SDK 0.1.0

`@neonmem/core` — the memory subsystem an agent talks to. A `.neonmem` file holds the memories, the typed
links between them, their vectors and every imported passage; embedding, search, ranking, decay and
consolidation happen inside it.

## Added
- A `.neonmem` file works as an agent's memory over MCP: the server is the package binary, so a client needs one line of configuration.
- The connect handshake states the order to consult memory in, and the rule separating the project's own record from passages quoted out of imported documents.
- A cartridge can declare what it is — name, contents, how to cite it — and a host introduces it by that instead of as a generic tool.
- `neonmem_load` takes a path or an `https` URL, so an agent can take delivery of a memory without reconfiguring anything.
- A `neonmem` command line creates and fills a cartridge: `init`, `describe`, `import`, `ask`, `brief`, `learn`, `decided`, `failed`, `rule`, `rules`, `status`, `consolidate`, `serve`, `model`.
- `--json` on every command, results on stdout and progress on stderr, and exit codes that separate a usage error from a missing model.
- The embedding model is fetched once per machine on first use; `NEONMEM_OFFLINE=1` declines and states how to supply one.
- The facts layer is stored in the file's FACT section, read and written byte-compatibly with the Python engine in both directions.
- An answer-level API: `ask`, `brief`, `remember`, `decided`, `failed`, `alwaysDo`, `describe`, `rules`, `health`. Every value crossing it is text, a score or a count.
- Ships as a portable folder: the runtime, the engine and the native libraries are inside the archive, so unzipping it is the whole installation.
- `neonmem mcp-config <project>` resolves this copy's own paths and prints the client configuration, or merges it into the project's `.mcp.json` with `--write`.
- `NEONMEM_HOME` decides where downloads land. The unzipped archive points it at its own folder, so the model and any fetched cartridges stay with the SDK and deleting the folder removes them.

## Changed
- Recall combines meaning and words, so a rule whose point is one rare term is found by that term.
- A rule recorded through the API is pinned to the tier that applies on every turn.

## Fixed
- A declared rule was written to the tier that standing rules are never read from, so it never applied.
- A recorded failure became a warning only above a fixed similarity score, which the retrieval path can legitimately make small; measured on a 1033-memory store, the most important rule returns first at 0.263. The warning now follows rank.
- An unreadable facts section was overwritten on the next save, so receiving an encrypted cartridge and recording one memory erased its imported corpus.
- A cartridge named outside a `.neonmem` directory resolved to a different path, opened an empty file one level down, and reported success.
- Imported documents were kept in a sidecar file, so a copied cartridge arrived without them.
- CRC32 was taken from a Node 22 API while the package declares Node 20, where reads worked and every write failed.
- Centring subtracted the corpus mean on stores too small to have one, scoring a single memory's own answer zero.

---

Windows x64, 61 MB zipped and 154 MB unpacked. Unzip anywhere and run `neonmem` or `neonmem-mcp` from the
folder — the runtime is inside, nothing is installed, and nothing is added to PATH. The embedding model
(about 121 MB) is fetched on first use into the folder, or supplied with `NEONMEM_MODEL_DIR`; set
`NEONMEM_OFFLINE=1` to keep it off the network. Licensed PolyForm Noncommercial 1.0.0.
