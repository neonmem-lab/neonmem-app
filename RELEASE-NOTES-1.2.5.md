# Neonmem Workspace 1.2.5

Project memory works. In 1.2.4 and every version before it, a session recorded almost nothing and could not
answer a question about its own project.

## Fixed

**A session recorded five memories out of nineteen turns, and the cartridge had no edges at all.**

Three separate defects, each sufficient on its own to make the memory inoperative.

The salience table had no entry for three of the node types the classifier produces. The lookup treats a
missing entry as a weight of zero, so those types were not merely unlikely to be stored — they could not be
stored at any novelty. "Open question: should rooms be plain dictionaries or proper classes?" scored 0.026
against a write threshold of 0.35. No question, no project frame and no standing principle was ever written.
A recorded procedure ranked below a passing guess and did not survive either.

Novelty was measured as one minus the similarity to what the project already held, which reads "about the
same subject" as "already known". Over nineteen turns discussing one small program that similarity climbed
from 0.00 to 0.85, and the decisions, the dead end and the procedure were all scored as things the project
already had. A session was penalised for staying on topic. Similarity now counts as redundancy only once it
is high enough to mean the same statement.

Nothing wired the graph. Memories were appended with no edges, and the routine that creates them was
reachable only from the offline corpus builder — never from the running application. PRISM is a
Hopfield/Ising relaxation whose coupling matrix is built from edges, so with none it held disconnected units
and resolved nothing: no attractor, no suppression of recorded failures. The relations were never missing
information. The salience loop already walks every stored memory, measures its similarity and tests the same
pairing it rewards — a settled memory closing an open one — and then discarded what it found. It now keeps
that pairing as a typed edge.

**Every question about the project's own history was answered with source code.**

There was no routing. While the client offers tools, every turn went to the tool loop, whose work is reading
files and writing them. So "What did we decide today?" was handled by the same path as "write me a parser",
and came back as the contents of the project's files — or, once, as "Task completed. No changes needed."

A question about the project's own record is now answered from its memory, with no file access, warning from
recorded dead-ends where the question touches one. It intercepts only when memory has something to say: when
recall finds nothing the turn returns to the ordinary path, so a misjudged question behaves exactly as it did
before. Asking what was decided no longer files the question alongside its own answer.

## Measured

The same nineteen-step session, typed into a clean install, before and after:

| | 1.2.4 | 1.2.5 |
| --- | --- | --- |
| Memories captured | 5 | 18 |
| Edges in the cartridge | 0 | 61 |
| Questions answered from memory | 0 of 4 | 4 of 4 |

Asked whether game state may be kept in globals, it now refuses and quotes the failure recorded earlier in
the session. Asked what the rule about dependencies is, it gives the rule the session set.

Nothing regressed: the beta suite passes 17 of 17 turns with 6 of 6 projects working, the stress suite 11 of
11 sessions with no unexpected errors, and the engine suite 87 of 87.

## Not claimed

At the size a single session produces, the relaxation is nearly saturated — the graph is close to fully
connected, so the same memories surface for different questions and only the suppression of recorded
dead-ends is clearly sensitive to what was asked. The model also remains a small one: told to plan without
writing code, it writes code anyway. What improved is the memory, not the model.

## Installation

Windows x64, installing to `C:\Programs\Neonmem Workspace` by default. The installer is unsigned, so
SmartScreen will warn on first run.

The download is about 470 MB. The language models (approximately 5.5 GB) are offered on first launch and
written into the install directory, so install on a drive with room for them.
