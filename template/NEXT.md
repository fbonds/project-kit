# Where we are

> **Read this before acting on anything below.** Every fact in this file is dated and may
> be stale. It records what was true when it was checked, not what is true now. Anything
> outside this repo moves without a commit here to show it, so re-check it first:
>
> ```sh
> git ls-remote --heads --tags origin | tail -5   # what the remote actually has
> git rev-list --left-right --count '@{upstream}...HEAD'   # left = behind, right = unpushed
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

Two more files hold what changes slowly: `DECISIONS.md`, what was decided and ruled out, and
`TRAPS.md`, what has cost time here before. Read both at the start, after this one.

Keep this file under 2,000 words by `wc -w`. After the conversation is compacted, Claude Code
re-reads up to five recently used files, and one over 5,000 tokens comes back as a path
without its content. The word count is a rough stand-in for that: a file heavy with code,
paths or tables uses more tokens per word.

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
