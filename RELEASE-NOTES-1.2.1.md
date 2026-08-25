# Neonmem Workspace 1.2.1

This release makes the agent check its own work by running it, rather than by reading it.

## Added

- **The agent runs what it wrote.** After a turn, wherever the work declares an entry point — a Python
  `__main__` guard, a Node main/index/app/cli, `javac` for Java — it is executed. The exact failure is
  returned to the model, and a repair is kept only if the program then runs; otherwise the original file is
  restored, because a repair that does not help replaces code you can read and debug with different broken
  code.

  This was previously opt-in: a project that wrote `.neonmem/verify.json` got a real verifier and every
  other project got none, which left the most reliable signal available almost nowhere. Nothing about
  whether a program runs is project-specific, so it no longer needs configuration.

- **A traversal that can never finish is detected statically**, for code that is imported rather than run.
  A worklist algorithm terminates only if an item cannot be enqueued forever — it must be marked as seen
  when pushed, marked unconditionally when popped, or skipped when already seen. Only that one shape is
  recognised; termination in general is undecidable.

## Fixed

- **A file could be written as a single line of escape sequences.** A small model improvising a JSON tool
  call emits the content double-escaped, and `JSON.parse` then produces a string containing backslash-n
  rather than newlines. Measured on a generated Python CLI: the file arrived as one 1042-character line and
  was invalid; repaired it is 33 lines and compiles. The generated code had been correct — it was mangled on
  the way to disk. A genuine one-liner printing `"a\nb"` is left alone.

- **A program that never terminates reported nothing.** `spawnSync` returns a killed process as status null
  with empty output, so an infinite loop produced a blank error that told the model nothing. It now reports
  that the program did not terminate within the timeout.

- **Deterministic guards did not run on conventional project layouts.** File gathering listed the project
  root only, so on any Maven, Gradle or package layout the call-site, arity and dependency guards were
  inactive on exactly the projects they were written for.

## Measured

Four arbitrary requests, each given to a project containing only an empty README, judged by rules that know
nothing about the request — every file valid in its own language, and any declared entry point must run and
terminate:

| Request | Result |
| --- | --- |
| Python CSV statistics tool | runs; states its required arguments |
| Node URL shortener | runs → `Shortened URL 1: 8kmxuk -> https://example.com` |
| Java word-frequency counter | compiles and runs → `This: 2` |
| Python self-playing guessing game | runs → `Guess: 50` |

The earlier suites are unchanged from 1.2.0: 17/17 beta turns with 6/6 projects that compile and run,
11/11 stress sessions, and a Spring build whose jar serves `/api/greeting` and `/`.

**Not covered.** The dependency guard has still not been observed firing in the product — it is verified by
unit test only. A Labyrinth build has not been carried through a complete session on this release: five of
its seven steps pass, and the generator it produced hung until the run-check above existed, which has not
yet been demonstrated end to end.

## Installation

Windows x64. The installer is unsigned, so SmartScreen will warn on first run.

The download is about 522 MB. The language models (approximately 5.5 GB) are fetched on first launch, once,
after an explicit prompt; nothing is downloaded without consent and nothing is sent to any server.
