# Neonmem Workspace 1.2.0

Generation runs on models built into the editor. A memory slot loads a Neonmem cartridge holding the
accumulated experience of the project, which the agent consults per turn.

This release is the result of two rounds of testing against the installed product, with gates that compile
and run whatever the agent produced. The measured results are stated at the end, including what they do not
cover.

## Added

- **Call-arity guard.** A function called with arguments its own declaration cannot accept is detected and
  repaired. The case that motivated it — `def main(path, limit=5)` called as `main()` — imports cleanly,
  passes a syntax check, and raises `TypeError` when run. Repairs are validated and discarded if they do not
  remove the mismatch.
- **Dependency guard.** Generated Java imports are checked against the dependencies the project's Maven or
  Gradle build actually declares. The agent has no shell and never sees a compiler error, so this is the only
  feedback available to it.
- **Partial-delivery guard.** A task naming several files that produced only some of them now produces the
  rest. Previously a request for a page and its script wrote the page and dropped the script.
- **Extensionless deliverables.** Dockerfile, Makefile, Procfile, Jenkinsfile and similar files can now be
  created; every path rule previously required a known extension.
- **Executable test suites.** `beta-e2e` (six developer personas in continuous multi-turn sessions),
  `stress-e2e` (eleven project shapes including malformed input), and `spring-rp-e2e` (a six-turn build that
  ends in `mvn package`, a booted jar and a polled port).
- **`packaged-bundle-check`.** Asserts each fix by its effect in the installed bundle, not in source.
- **Source-hygiene test.** Rejects collapsed regex escapes — a corruption that had silently disabled three
  separate fixes.

## Fixed

- **Guards did not run on nested project layouts.** File gathering listed the project root only, so on any
  conventional Java or package layout the call-site, arity and dependency guards did nothing at all.
- **The file to create was taken as the first path in the request.** "Create Dockerfile: … copy package.json
  and app.js into /app" resolved to `package.json`, so the rescue path could overwrite a project manifest.
  The deliverable is now the object of the create verb.
- **Ordinary technical prose was classified as garbled input.** `k8s` matched the noise heuristic, as did any
  sentence containing two vowel-less abbreviations such as `svc` or `ctx`.
- **Rewriting a request could discard a filename it stated.** The rewrite of one such "garbled" request
  dropped `k8s/deployment.yaml`, after which the model's invented filename stood. The literal request is now
  recorded before any rewriting, and a rewrite that loses a stated filename is rejected.
- **A locked cartridge left a project with no memory.** An `EBUSY` error opening `memory.neonmem` was fatal
  to memory but not to the turn, so the agent answered normally with nothing to draw on. Lock errors are now
  retried.
- **A word boundary written as `'\b'` inside a string** is a backspace character and matched nothing. The
  affected check had never executed.

## Changed

- **Memory delivery.** Grounding previously emitted whole source files, consuming roughly a third of the
  context window. Retrieved material is now reduced to the declarations relevant to the request, under a
  token budget.
- **Cartridges carry a real graph.** Edges are built at ingest from symbol references, shared namespaces and
  semantic neighbours; tier-0 rules are mined by support and confidence.
- **Rules are retrieved, not asserted.** Reflex rules are matched against the request at a relevance floor
  rather than prepended to every turn.
- **Novelty is measured against experience,** not against the seeded reference library — a seeded project
  previously captured nothing.
- **Project tooling** under `tools/` is TypeScript.

## Measured

Against the installed build, using gates that compile and run the result:

| Suite | Result |
| --- | --- |
| Beta — 6 personas, 17 turns | 17/17 turns, 6/6 projects compile and run |
| Stress — 11 project shapes | 11/11 |
| Spring build — 6 turns | 6/6 turns, 6/6 readiness gates; the built jar serves `/api/greeting` and `/` |
| Unit suites | 32 tests |

Context overflow, tool-loop collapse and sequence exhaustion do not occur in any session of any run.

**Not covered by these results.** The dependency guard has not been observed firing in the product: in both
Spring runs the model produced a plain record rather than the JPA entity that originally caused the failure,
so the guard is verified by unit test only. Output also varies between builds, because the added guard passes
change generation state; repeated runs of the same build reproduce.

## Installation

Windows x64. The installer is unsigned, so SmartScreen will warn on first run.

The download is about 547 MB. The language models (approximately 5.5 GB) are fetched on first launch, once,
after an explicit prompt; nothing is downloaded without consent and nothing is sent to any server.
