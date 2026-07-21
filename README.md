# Neonmem

Downloads for Neonmem Workspace — a Visual Studio Code fork that works natively with the Neonmem memory format. The editor reads and writes a project's `.neonmem` cartridge directly, so the accumulated experience of a project — its decisions, rules, dead-ends, and plans — is available to you and to the agent while you work.

![Neonmem Workspace with the Brain open](resources/brain.png)

## Download

Get the latest installer from the [Releases](../../releases/latest) page.

- Windows: `neonmem-workspace-Setup.exe`

## The Neonmem cartridge

A `.neonmem` cartridge is a single-file binary memory store with built-in vector storage. It is little-endian, page-aligned to 4096 bytes, and begins with a 64-byte header (magic `ARIN`) followed by a section index. The sections are:

- Nodes. Fixed-size (128-byte) records. Each node holds a type, a tier, flags, a created and a last-accessed timestamp, a confidence and a relevance score, an access count, an edge count, an offset into the string table for its text, and an index into the vector store. Node types are: observation, question, hypothesis, debate, conclusion, resolution (decision), rule, dead-end, plan, procedure.
- Edges. Typed directed relationships between nodes — led-to, blocked-by, supports, contradicts, part-of, and others. A node stores its first edges inline, with an overflow table for high-degree nodes.
- Vector store. One embedding per node, int8-quantized with a per-vector `f32` scale; a value is recovered as `v = q · scale`. Because vectors are L2-normalized, cosine similarity is a dot product.
- String table. Node text, LZ4-compressed.
- Footer. A per-section CRC32 and a content hash, for integrity.

### Layers

Every node lives in one of three tiers: reflex (rules and invariants that always apply), short-term (the current effort), and long-term (retained across sessions).

### Lifecycle

Capture → store → recall → reason → consolidate. A turn of work is split into sentences; each is classified into a node type and scored; those above the salience threshold are written as typed nodes with an embedding vector. A query is embedded and matched by cosine similarity, and PRISM relaxes the local graph into an answer, dead-ends to avoid, and rules that apply. Items move between tiers as they prove durable.

## Mechanics

### Embeddings

Text is embedded with the IBM Granite-30M embedding model, exported to fp16 ONNX and run with onnxruntime inside the app. A string is tokenized (a byte-level BPE tokenizer that reads the model's own `tokenizer.json`), passed through one forward pass, and the last hidden state at the CLS position is taken and L2-normalized to a 384-dimensional unit vector. The same model runs at write and read time.

### Similarity search

Recall is exact cosine over the L2-normalized vectors — equivalent to inner-product (`IndexFlatIP`) — returning the top-k nearest nodes for a query. There is no approximate index and no external vector database; the vectors are part of the cartridge.

### Energy-based capture

Each candidate sentence is scored by an energy-like salience:

```
novelty  = 1 − max cosine similarity to existing memory
L        = novelty · (h_type[t] + h_base) + relief
salience = sigmoid(β · L) · L
store if salience ≥ E_WRITE
```

`h_type[t]` weights the node type, `h_base` combines importance and specificity of the text, and `relief` rewards a resolution that closes an open thread already in memory. Novelty suppresses restating what is known; a plan is a forward-looking commitment and is given a novelty floor so it is kept even when related to existing memory.

### PRISM — reasoning through the graph

Recall answers what is stored; PRISM reasons over how the stored items relate. It is based on Hopfield/Ising energy-based associative memory. For a query, anchor nodes are found by cosine and their neighborhood is expanded into a subgraph. The subgraph's edges define a coupling matrix `J` (supporting edges attract, contradicting and blocking edges repel) and node types define a field bias `h`. The unit states relax by `a ← sigmoid(β · (J·a + h))` until they settle, and the result is read out as attractors (the answer), repelled regions (dead-ends to avoid), and active constraints (rules).

## Releases

Releases 0.7 through 0.9.8.x are the previous Electron application; from 1.0.0 the product is the editor fork. The source is maintained in a separate private repository; this repository hosts the published releases and installers.

## License

Free for personal, hobby, research, educational and nonprofit use under the PolyForm Noncommercial License. Commercial use requires a license.
