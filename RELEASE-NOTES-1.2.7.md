# Neonmem Workspace 1.2.7

Two corrections to 1.2.6: the installer no longer fails on its last step, and the agent stops describing
itself as offline.

## Fixed

**The installer ended with "Unknown constant: userprofile".**

The last step of an interactive install ran a check for a Claude installation on the machine, and that check
asked Windows for a path using a name the installer does not define. It failed where every install ends, so
the error was the last thing a first-time user saw.

The check itself was left over from an earlier design and no longer describes what ships. It warned that the
agent, memory-aware prompts and completions "will NOT work until Claude is set up" — untrue for some time
now: the agent is a local model that requires no account, no key and no network. So the check is gone rather
than repaired, and with it a warning that was both broken and wrong.

It survived three releases because it exits early during a silent install, which is how an automated test
installs. Only a person clicking through the wizard could see it.

**The agent described itself as offline.**

"Offline" was the agent's name in the session picker, the heading above every reply, and the word it was
given for itself in its own instructions. It reads as a limitation being disclosed — a service that has
lost its connection. Running entirely on the machine in front of you is this agent's normal condition and
the reason it can read a project's memory without sending it anywhere.

The agent is now called Neonmem, and where the distinction matters the text says the work happens on your
machine.

## Unchanged

Everything measured for 1.2.6 — the planning hold, the reasoning over project memory, and the check that an
answer drawn from memory actually uses it. The nineteen-step session still answers four of four questions
from the project's own record and holds eight of eight planning turns without writing a file.

## Installation

Windows x64, installing to `C:\Programs\Neonmem Workspace` by default. The installer is unsigned, so
SmartScreen will warn on first run.

The download is about 470 MB. The language models (approximately 5.5 GB) are offered on first launch and
written into the install directory, so install on a drive with room for them.
