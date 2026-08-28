# Neonmem Workspace 1.2.8

Importing documents into a project now works: it finishes, it keeps the memories that were already there,
and the agent reads what was imported when it answers.

## Fixed

**An import deleted the memories a session had already captured.**

A project is open in two processes at once — the editor holds one memory engine, the agent another — and
each keeps its own copy of the whole memory file. Saving wrote that copy over the file, so whichever side
saved last erased the other's work. Reproduced exactly: a new project, a turn that captured two memories,
then an import that left one. Saving now records what the file looked like when it was last read and merges
in anything that appeared underneath before writing.

**An import of forty documents would not finish.**

Each fact entering the searchable pool was compared against every fact already in it. Eight thousand facts
took fifty-three seconds and the cost grew with the square of the input, which put a documentation corpus of
a hundred thousand fragments at around three hours. Comparisons are now drawn from a hash of the vector's
direction and capped: the same eight thousand take under a second.

Then it threw the result away. The pool was written as a single document, which has to exist in memory as
one string before it can be saved, and a string has a hard length limit — that corpus produced 630 MB of it.
The import did all of its work and failed on the last step, reporting nothing beyond a progress bar that
never stopped. The pool is now written and read a piece at a time, and stores its vectors with the same
compact encoding the memory file already used.

And confirming an import cost as much as performing one: the preview walked the same path as the real thing
and embedded the whole corpus, so it was processed twice. It now counts what it finds without embedding.

**Imported documents were never read.**

The pool had no reader. Grounding searched the memories alone, and the one tool that could reach the pool was
withheld from the model, so a corpus imported on purpose was stored and never opened again. Grounding now
searches both. Memories rank first — a memory is this project's own conclusion, a passage is only something
the documents say — and a passage already carried by a memory is not repeated.

The agent is also told, now, how to use what it is given: what this project has recorded comes first; then
the imported documents, quoted rather than paraphrased; then its own reasoning, saying plainly that the
project has nothing recorded; and when the question is about this project and the support is thin, to ask
for the missing detail rather than invent one. That order is part of the agent rather than part of each
message, so it applies to every turn.

**Imports filled the memory graph with material nobody had asked about.**

An import minted up to eighty memories, which then outranked real ones at recall. An import now fills the
searchable pool and mints nothing — except two memories for each topic named as a priority, which give a new
project a foothold. Memories of imported material form when they are earned instead: a question answered
from the documents leaves one concise statement ("EAI — Ericsson Adaptive Inventory") linked to the passage
that grounds it, and only about the subject that was asked.

**Documents exported from a manual were read a fragment at a time.**

Such a file carries the page layout with it: prose is wrapped at a fixed column, so one sentence arrives as
three lines. Reading line by line shredded it —

> Single sign-on (SSO) is a token-based authentication process that allows a user
> to access multiple applications with one set of logon credentials.

became two fragments, neither of which answers "what is SSO?". That is why 8.6 MB of documents became
179,780 pieces averaging forty-two characters. Wrapped lines are now rejoined, including words split across
a wrap.

**Searching those documents ignored the words in the question.**

Ranking by meaning alone has no way to prefer the passage that defines a term over a dozen that discuss the
same topic, which is how "what authentication does the API use?" returned a fragment reading "client logs in
using API authentication.)". Keyword ranking is now fused with it, so a passage that is a good match either
way rises, and one that matches both rises further.

**Weights stored inside a memory file were destroyed by opening it.**

A memory file written by the previous engine carries sections this one does not read — trained model
weights among them, including the query model a file's own vectors were built with. They were neither read
nor written, so opening such a file and saving it discarded them. They are now carried through untouched.

**The agent could not read a file it was pointed at.**

When the agent read a file itself, only the first 1,500 characters came back to it. Asked what went wrong
in a 4.7 KB log, it received the first twenty lines — all routine traffic — and reported that every entry
was informational, which was an accurate account of what it had been given. The limit was set for a fixed
context window that no longer applies: the window now grows to fit the work, and what the agent reads grows
with it.

**A question about a file was answered as though it were a request to change one.**

The instructions the agent follows during a task were written entirely around editing code — replace the
file, then reply with a one-line summary. Nothing described how to answer a question, so a question about a
log produced a summary of the log. Questions now have their own instructions: read the file that was named,
quote the line that answers it, and say plainly when the answer is not there.

**"What caused this?" was answered with the loudest line rather than the cause.**

Given a log where an outage began with a configuration change eleven minutes before the first error, the
answer was that the connection pool had been exhausted — true, and the last consequence rather than the
cause. The agent is now told what root-cause analysis means: read in time order, find the first abnormal
line, look before it for something that changed. On the same questions this took both bundled models from
one correct answer in four to three.

This was measured against a general-purpose model as well, in case the coding models were the wrong tool
for prose. They were not: on a requirements document with interacting rules, a constraints table and a
diagram, the bundled models answered four of four and the general-purpose model three of four. No further
model is needed, and none was added.

**A recorded failure produced no verdict, and a recorded decision lost its reason.**

Asked whether an approach was acceptable when the project had already tried and abandoned it, the answer
was "yes" — the warning was in front of the agent, and drawing the conclusion was left to it. And asked why
a decision had been taken, the answer named the decision without the reasoning behind it, which is the half
that no source file records. Both now follow the record: a failure that bears on the question produces a
plain "no" and what went wrong, and a "why did we" answer quotes the reason as it was written down.

## Measured

The forty-file, 8.6 MB documentation corpus that prompted this:

| | 1.2.7 | 1.2.8 |
| --- | --- | --- |
| Import | did not complete | 2.0 min |
| Preview | ~6 min | 0.6 s |
| Searchable pool on disk | 630 MB | 36 MB |
| Memories the import invents | 80 | 0 |
| Questions the documents answer, answerable by the agent | 1 of 3 | 3 of 3 |

On the nineteen-step session from the demo manual, typed into a clean install: eight of eight planning
turns wrote no files, and four of four questions were answered from the project's own record. A new test
points the agent at a log, a source file and a document in turn and asks a question of each whose answer
appears in that file alone: three of three.

Retrieval was measured with a benchmark the corpus builds itself — take a passage that defines a term, ask
what that term is, and require the passage back — so that no wording of ours decides the result. Fusing
keyword ranking with meaning raised it by about seven points at three results.

## Not claimed

One family of weighting from the previous engine was ported, measured, and left out: it reordered results
without finding more of them, on 150 questions. It had never been connected to anything there either.

A memory file whose vectors came from the previous engine's own trained query model is carried through
safely but cannot yet be searched correctly here, because queries would be turned into vectors by a
different model. Nothing this application creates is affected.

## Installation

Windows x64, installing to `C:\Programs\Neonmem Workspace` by default. The installer is unsigned, so
SmartScreen will warn on first run.

The download is about 470 MB. The language models (approximately 5.5 GB) are offered on first launch and
written into the install directory, so install on a drive with room for them.
