# Neonmem Workspace 1.2.3

Installation is now a clean editor, and the local models are offered rather than demanded.

## Changed

**The models are requested from the editor, once it is open.**

Previously the first run put up a modal dialog before any window existed, downloaded into a separate
always-on-top window, and quit the application if you declined. So a fresh install showed nothing at all
until several gigabytes had been agreed to, and saying no meant no editor.

The install now contains no models and starts straight into the workbench. A notification then offers them —
**Download**, **Not Now**, or **Don't Ask Again** — with progress shown in the notification. Declining leaves
the editor completely usable: everything except the offline agent works without the models, and the offer
returns next launch. If the drive cannot hold them, that is said instead of prompting, rather than failing
several gigabytes into a download.

Progress is reported as an absolute percentage rather than in increments, because a resumed download starts
part-way through and an incremental bar would restart at zero.

## Fixed

**Two projects with the same folder name were treated as one project.**

Opening a folder saves it as a workspace file under `~/.neonmem/workspaces/`, and that file was named after
the folder's last path segment alone. Every project called `frontend`, `demo`, `api` or `backend` therefore
shared one file, and opening the second such folder opened **the first one instead** — a different directory,
without saying so, with the agent then reading and writing files there.

Measured: opening `D:/nm-clean-124336/cli-dev` reopened `D:/neonmem-beta/cli-dev`, a folder from an unrelated
session days earlier, with a fresh profile and no leftover processes. Thirty colliding files had accumulated
on that machine, with names as ordinary as `app-1` through `app-4`.

The file name now carries a digest of the full path, so folders sharing a name cannot share a file. Files
written under the previous scheme still exist and still point elsewhere, so a saved workspace is read before
it is used and ignored unless it genuinely describes the folder being opened. Nothing is deleted — a stale
file is simply not followed.

## Measured

On a clean install at `D:\Programs\Neonmem Workspace`:

| Check | Result |
| --- | --- |
| First-time install | executable where the installer says, longest path 193 of 260, 40 to spare |
| Application starts | yes, with no models on disk and nothing blocking |
| Models offered | notification with a Download action |
| Accepting | fetches into the install directory |
| Interrupted download | resumes — 24,050,171 → 36,313,920 bytes, keeping the earlier bytes |
| Same-named projects | separate workspace files; a file describing another folder is refused |

## Installation

Windows x64, installing to `C:\Programs\Neonmem Workspace` by default. The installer is unsigned, so
SmartScreen will warn on first run.

The download is about 449 MB. The language models (approximately 5.5 GB) are offered on first launch and
written into the install directory, so install on a drive with room for them.
