# Where we are

> **Read this before acting on anything below.** Every fact in this file is dated and may
> be stale. It records what was true when it was checked, not what is true now. Anything
> outside this repo moves without a commit here to show it, so re-check it first:
>
> ```sh
> git ls-remote --heads --tags origin | tail -5   # what the remote actually has
> git rev-list --left-right --count origin/main...main   # left = behind, right = unpushed
> git status -sb
> # add the command that checks what this project publishes or deploys
> ```
>
> The rest of the checks, and the procedure for updating this file at the end of a session,
> are in `HOWTOSAVESTATE.md`. Stored memories load before any file and go stale the same
> way: check them against the repo rather than trusting them.

Updated YYYY-MM-DD. Working state for PROJECT. Say here which file is the design, which is
the roadmap, and which is the public documentation, so this file is not mistaken for any
of them.

## Traps

Things that cost time once and would cost it again: a tool that lies, a check that cannot
fail, an environment that behaves differently here. Add one the same session it bites,
with enough detail to recognise it, not just to remember it happened.

Start with these questions. Answer each for this project. An answer of "none" is a claim like
any other fact in this file, so it carries the date and how it was checked. Write "not known
yet" if you cannot tell. Do not delete one. Specific traps go below them.

- Which dashboard or console here lags, and by how much?
- Which listing shows the published state and hides the pending one?
- Which registry reports metadata that differs from the artifact?
- Which cache can serve an old copy?

## Decided, do not redo

What was settled and why, what was ruled out and why, and anything the owner said not to
do. A resumed session that sees only the remaining tasks will rebuild something already
rejected, or argue for an option already refused.

An entry here is not rewritten. To change a decision, get the owner's approval, then add a
new entry with its date, its reasoning and the entry it replaces. The only edit to the old
entry is one added line saying what replaced it and when.

<!-- Empty on day one. Add a decision the day it is made, with its reasoning, not its
     conclusion alone. -->

## In flight

What is being worked on now, and what state it is in. Remove an item when it is finished,
because the git log holds it. Before removing it, move what the git log cannot hold: a
release or deploy goes to the Committed, pushed, released section, with its date and how it
was checked, and anything else, such as a change made on a hosted service, goes to the
section it belongs in.

## Queued, unscheduled, and not to be started unprompted

What is agreed but waiting, with a pointer to wherever the full proposal is written out.

## Committed, pushed, released: three separate questions

As of YYYY-MM-DD, when this was written.

**Uncommitted.** What is in the working tree and not committed, and whether it was
approved.

**Unpushed.** The command that answers it, plus a dated snapshot marked as not to be
trusted, because the owner pushes and that moves with no commit here to record it.

**Unreleased or undeployed.** What is committed but not yet in front of anyone, and how that
was checked. Also what was last released or deployed, when, and how that was checked.

## Open, not blocking

Anything known, unresolved, and not in the way.
