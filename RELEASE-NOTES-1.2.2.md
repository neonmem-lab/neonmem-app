# Neonmem Workspace 1.2.2

Installation and first run. Reported from a real install on another machine, where 1.2.1 failed before the
application ever started.

## Fixed

- **Installation failed with `moveFile failed code 3 (cannot find the file specified)`.** Windows caps a
  full path at 260 characters, and what ships is a relative path with the install directory prepended on
  the user's machine. The package carried `node-llama-cpp`'s local build tree — 1165 object files, MSBuild
  logs and `.lastbuildstate` stamps — plus 150 MB of vendored llama.cpp source, reaching 230 characters
  before any install root was added. None of it is read at runtime; the application uses the prebuilt
  binaries. Removed, the longest path is now 163 characters.

- **The default install location was part of the same sum.** `C:\Users\<name>\AppData\Local\Programs` is 47
  characters before the product name. The default is now `C:\Programs`, which costs 9 and needs no
  administrator rights.

- **An interrupted model download started again from nothing.** There was no retry and no resume: a single
  dropped connection during a multi-gigabyte transfer deleted the partial file and asked the user to start
  over. Each source is now attempted five times with exponential backoff, resuming with an HTTP Range
  request from the bytes already on disk, and a progress record means a closed laptop or a quit application
  also resumes rather than discarding what it had. A stalled connection is treated as a failure after 120
  seconds instead of hanging, and the checksum is taken over the finished file, since a resumed download is
  assembled across attempts.

- **A disk too small to hold the models failed late and unclearly.** The models are written into the install
  directory. Free space is now checked before anything is fetched, and the message states how much is needed
  and how much is available.

## Measured

Verified on a first-time install, with the remembered install location cleared so the installer could not
silently reuse an earlier directory:

| Check | Result |
| --- | --- |
| Longest installed path | 193 of 260 characters, 40 to spare |
| Application present and starts | yes |
| Interrupted download resumes | partial grew from 139,949,269 to 426,342,380 bytes across a restart — the earlier 139 MB was kept |
| Resume correctness | against a server dropping the connection twice: three attempts, resumed at 1,048,576 and 1,747,626 bytes, checksum matched |

The installer is 449 MB (was 522) and the portable archive 681 MB (was 792).

**Why this reached users.** The installer had only ever been tested at `D:\product_tests` — a 17-character
path, on a drive with ample space, with the models already present. All three faults are invisible under
those conditions. `test/neonmem/install-check.ts` now clears the remembered location, installs the way a user
does, and checks that the application starts; `test/neonmem/packaged-layout-check.ts` fails a release whose
paths are too long, that ships build intermediates, or that comes from a build that did not finish.

## Also in this release

Everything from 1.2.1, plus a fix to it: the run-check added there invoked an entry point with no arguments,
so a command-line tool that requires a file path did the correct thing — printed its usage and exited
non-zero — and the agent treated that as a defect and rewrote working code. A program that states what it
needs is now recognised as working.

## Installation

Windows x64, installing to `C:\Programs\Neonmem Workspace` by default. The installer is unsigned, so
SmartScreen will warn on first run.

The language models (about 5.5 GB) are fetched on first launch, once, after an explicit prompt. They are
written into the install directory, so install on a drive with room for them.
