# Neonmem Workspace 1.2.6

Asked to plan without writing code, the agent now plans. And the reasoning over project memory retrieves
what a question is about instead of returning the same memories to every question.

## Fixed

**An instruction not to write files lasted exactly one message.**

Told "don't write any code until I explicitly say implement that — for now just plan with me", the agent
produced a complete program on the very next turn. The refusal existed and worked, but it was tested against
the words of the turn being handled, and by the following message those words were gone. An instruction was
therefore obeyed for as long as it was being repeated, which makes planning impossible: every attempt to
think before building turned into building.

The prohibition now lasts for the session and is lifted only by an explicit request to produce the work.
Lifting is deliberately conservative, because the two mistakes are not equal — failing to lift costs one
more sentence, while lifting early modifies files after a promise not to. A turn that merely contains a
production verb does not qualify: "record the procedure to add a new room" describes adding, it does not ask
for it. The rescue that writes files a reply only printed honours the hold as well, so it cannot be defeated
by another route.

**The reasoning over memory returned the same answers to different questions.**

PRISM is a Hopfield relaxation over the memory graph. Three faults made it incapable of retrieval. The query
reached only the handful of entry memories, so everything else in the neighbourhood was settled purely by
what type of memory it was — a decision outranked the subject of the question. A unit's input grew with how
many edges it happened to have, so on a well-connected graph every activation saturated at 1.000 and the
ordering carried no information at all. And nothing competed: with every bond positive, "everything on" was
the only state the dynamics could reach, which left the result no better than the similarity ranking it
started from.

The query now enters the field of every memory, the neighbourhood term is averaged rather than summed, and
the units compete for a fixed budget of activation. Measured over four questions about one project, the
right memory is now first for all four and the activations span 0.68 to 0.94 where they had spanned 0.017.
Asked "why did we go with a hand-crafted maze again?", similarity returns the debate that phrase appears in
and the relaxation returns the decision that settled it, reached over the link between them.

**A recorded failure was buried instead of raised.**

The relaxation drives a dead end's activation to zero deliberately — it is saying "this is not the answer".
Ordering the evidence by that number read it as "this does not matter": asked whether game state could be
kept in globals, the recorded failure was the second most relevant memory and was placed last, and the reply
was "Yes, it is okay" — the opposite of what the session had recorded. Suppression and relevance are
different questions, and dead ends are now ranked by how much they bear on what was asked.

**An answer drawn from memory was the one thing nothing checked.**

Code this agent writes is executed, and a repair is kept only when the program then runs. An answer about
the project was streamed straight out unread. It showed: asked why a hand-crafted maze had been chosen,
with the decision and its recorded reasoning both ranked first in the evidence, the reply was "because it
allowed for more intricate and creative design" — reasoning the session never contained. Retrieval had done
its job and the model simply wrote something else.

An answer is now produced before it is shown, and checked against the memories it was given: does it share
any distinctive word with them, one the question did not already supply, so that repeating the question back
cannot pass. If not, it is asked for once more with the record quoted back at it. One retry only, and the
check is deliberately generous — a false alarm costs a single regeneration, while being strict would reject
good answers phrased in words nobody predicted. In the run measured below it fired once, on "what did we
decide today?", and the second answer named the decision.

## Measured

The nineteen-step session from the demo manual, typed into a clean install:

| | 1.2.5 | 1.2.6 |
| --- | --- | --- |
| Planning turns that wrote no files | 0 of 8 | 8 of 8 |
| Questions answered from the project's memory | 0 of 4 | 4 of 4 |

The engine suite is 90 tests, the beta suite 17 turns across 6 projects, and the stress suite 11 sessions.

## Not claimed

The retrieval is measured on one project at the scale a single session produces, and the table above is one
run of it. Run-to-run variation is real and is why the check described above exists: builds carrying the
retrieval fixes but not the check answered all four questions in one session and three of four in the next,
the odd one out being an invented reason rather than a failure to retrieve. The planning result was steadier
— eight of eight on every run measured.

## Installation

Windows x64, installing to `C:\Programs\Neonmem Workspace` by default. The installer is unsigned, so
SmartScreen will warn on first run.

The download is about 470 MB. The language models (approximately 5.5 GB) are offered on first launch and
written into the install directory, so install on a drive with room for them.
