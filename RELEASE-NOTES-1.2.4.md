# Neonmem Workspace 1.2.4

A dropped connection during the first-run model download no longer corrupts the file it was fetching.

## Fixed

**An interrupted download appended the same bytes twice.**

The download resumes with an HTTP Range request, and the offset it asked to resume from came from a counter
that was only advanced when a transfer **succeeded**. A failed attempt has already written whatever it
received before the connection went away, so the retry asked the server to continue from a smaller offset
than the file on disk actually held, and the overlap was appended on top of the bytes already there.

Measured on the 4.68 GB agent model over a real connection: the partial file grew past its expected size to
5.54 GB, failed its checksum, and was discarded — after six minutes in which progress had looked entirely
healthy. Every retry made the file worse, so a connection that dropped more than once could not recover.

The offset is now read from the file itself after every attempt, successful or not. A server that ignores
Range is handled by truncating back to the start of the part currently in flight rather than deleting the
whole file, so parts that already completed and verified are kept — on the three-part agent model that is
gigabytes of correct data that used to be thrown away.

This affects 1.2.3 and every earlier version that downloaded models. If a download failed with a checksum
error, this was why.

## Measured

On a clean install at `D:\Programs\Neonmem Workspace`, from a genuinely fresh installer run:

| Check | Result |
| --- | --- |
| First-time install | executable where the installer says, longest path 193 of 260, 40 to spare |
| Every packaged path | fits within 181 characters, so any reasonable install directory works |
| Application starts | yes, with no models on disk and nothing blocking |
| Models offered | notification with a Download action |
| Interrupted transfer, three parts, two drops | exact file size, checksum matches |
| The same test against the previous code | 3,100,000 bytes reported for a 2,200,000-byte file; checksum fails |

The last two rows are the point: the regression test that now covers this imports the compiled module that
ships, not a copy of its logic. An earlier version of that test reimplemented the algorithm correctly in its
own copy and passed green for as long as the shipping code was wrong.

## Installation

Windows x64, installing to `C:\Programs\Neonmem Workspace` by default. The installer is unsigned, so
SmartScreen will warn on first run.

The download is about 470 MB. The language models (approximately 5.5 GB) are offered on first launch and
written into the install directory, so install on a drive with room for them.
