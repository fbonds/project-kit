# Where we are

**This is project-kit's own working state, filled in for this repository. It is not the
template.** To use the kit in another repo, copy the three files in `template/`.

> **Read this before acting on anything below.** Every fact in this file is dated and may
> be stale. It records what was true when it was checked, not what is true now. The owner
> pushes, and GitHub moves without a commit here to show it, so re-check first:
>
> ```sh
> git ls-remote --heads --tags origin                    # what GitHub actually has
> git fetch -q origin && git rev-list --left-right --count '@{upstream}...HEAD'   # current branch: left = behind, right = unpushed
> git status -sb
> gh api repos/fbonds/project-kit/activity --jq '.[] | [.timestamp, .activity_type, .after[0:7]] | @tsv' | head
> gh issue list --state all; gh pr list --state all
> ```
>
> The activity log gives push times. A commit's own timestamp is when it was made, not when
> it reached GitHub, and the two have already been confused once here.
>
> The end-of-session procedure is `template/HOWTOSAVESTATE.md`. Stored memories load before
> any file and go stale the same way: check them against the repo rather than trusting them.

Updated 2026-11-24. Working state for project-kit. `README.md` is the public argument and
the only documentation, and the GitHub Pages site renders it. `template/` is the kit
itself. `docs/` is the record of results, indexed in `docs/README.md`. There is no design
document. The version 2 plan is `docs/version2-plan.md`, and this file holds what is queued.

Two more files hold what changes slowly, and a session reads both at the start, after this
one: `DECISIONS.md`, what was decided and rejected, and `TRAPS.md`, this repository's
failures against the standards and the traps it has hit. After compaction, re-read this
file: Claude Code re-injects `CLAUDE.md` then, and not this file.

## In flight

**The version 2 overhaul, on the `version2` branch** (from 2026-11-21). The decision is in
`DECISIONS.md`, "project-kit is the owner's personal methodology". The gaps it works
through are in `docs/version2-plan.md`, and what each source says about them is in
`docs/research-2026-11-23-sources.md`.

Closed on 2026-11-24: gaps 6, 8 and 10. The plan says what each changed and what is still
untested. `DECISIONS.md` and `TRAPS.md` measured 4.8k and 4k tokens at `9d524e0` and have
not been measured since. On 2026-11-24 they were 2,135 and 2,272 words, against 2,294 and
2,078 then.

In progress since 2026-11-24: gap 1, a building procedure. The design is the Decided entry
"The kit gets a building procedure, `HOWTOBUILD.md`" (`f04373b`). The first file item was
drafted and tested on 2026-11-24 and not yet approved, so nothing of it is committed. It adds
`template/HOWTOBUILD.md` (675 words), a pointer to it and a test-command line with a new
placeholder in `template/CLAUDE.md`, a `HOWTOBUILD.md` entry in the file list of
`template/HOWTOSAVESTATE.md`, and in the README six files instead of five, a paragraph on
`HOWTOBUILD.md`, the new file in the setup commands, and the new placeholder in the grep's
list. The README's setup commands were run against it in a scratch repository and copied,
grepped and staged all six files. The draft is in this session's scratchpad, under `g1a/`,
which a reboot can clear. If it is gone, redraft it from the Decided entry and show it for
approval again. After that item: the README's Prior art credits for the new sources, then
closing gaps 1, 13, 14 and 15 in the plan.

Also open: a test only the owner can run, whether the template's SessionStart hook prints
into a real session and runs after compaction. When `version2` is merged, the GitHub
description's "Three Markdown files" becomes wrong, and only the owner can change it.

## Queued, unscheduled, and not to be started unprompted

**Recording cold-session runs.** The README defines the test. The owner reported on
2026-10-26 that it has been run at least once a week since 2026-09-17, in repositories using
the kit, all passing, and on 2026-10-30 that it has been used dozens of times and "works
flawlessly", with the condition that the session before it was told to save state before
quitting. Later the same day the owner added that the runs happen on most days of most
weeks, including 29 and 30 October, across several private repositories for different
projects developed at the same time, and that each picked up where the last session left
off. The README's Results records all of it as attested. No run was recorded with its
repository or with whether `NEXT.md` was stale. On 2026-11-06 the owner said none of those
details exist or will be supplied, and the README's start date had become 16 September in
`e2a3eb4`. No run lines get written for them. What happens when test harness results exist
is in Decided.

**Test harness for the kit** (2026-11-06, owner's request). Fixture repositories with
failures planted before any run, so the ground truth is written first: a stale dated fact, a
wrong count, a pointer to the conversation, a commit message that contradicts the code, a
stale stored memory where the environment allows, and true facts as controls. Each fixture
runs with and without the kit, several times, in an environment with no stored memories.
Grading is mechanical where the tool log can show it, and against the cold-session criteria
where it cannot. Scripted, not manual: settled in github.com/fbonds/project-kit-harness,
under Decided in its `NEXT.md`. The design is `docs/DESIGN.md` there. Open: how many runs,
which that design leaves unset until the owner has read the cost of its smoke run. Read from
GitHub on 2026-11-06 at `ae35382`, when nothing there was built and no session had been run.

## Committed, pushed, released: three separate questions

As of 2026-11-24 23:55 UTC, re-checked against the remote at that time.

**Uncommitted.** Nothing apart from this save's edits, which are in the commit carrying them.
The unapproved draft above is outside the repository.

**Unpushed.** Answer it with `git rev-list --left-right --count '@{upstream}...HEAD'` after a
fetch, on each branch, or `git ls-remote --heads origin` when the remote-tracking ref may be
stale. Snapshot, not to be trusted: GitHub had `main` at `2f30d9f` and `version2` at
`454509a`. Unpushed on `version2`: `18bc1c0`, `d122ebf`, `e3e3c73`, `4032610`, `97c6579`,
`f04373b` and the commit carrying this sentence. The owner pushes, so this moves with no
commit here to record it. A commit ID written into this file is the ID at the time of
writing, and a rebase replaces it.

**Unreleased.** Nothing is released separately. Pushed to `main` is published, and
`version2` is not published by the site. Last published: `2f30d9f`, pushed to `main` at
23:01:51 UTC on 2026-11-21. The last push to `version2` was `454509a` at 21:09:25 UTC on
2026-11-24. Both read from the activity log, and the IDs from `git ls-remote`. No tags, no
GitHub releases, no issues and no pull requests, each read at the time above.

The GitHub Pages site at https://fbonds.github.io/project-kit/ is set to `main`, `/ (root)`.
Its latest build was `built` on `2f30d9f` at 23:02:25 UTC on 2026-11-21, read from the Pages
API at the time above. Every commit from `23edcce` to `2f30d9f` changed only this file, which
the site excludes, so the README it renders is the one in `6ab6386`. The page itself was not
fetched on 2026-11-18, 2026-11-22 or 2026-11-24, at either save.
On 2026-11-12 at 23:44 UTC the page, fetched with a cache buster, had the README's 10
headings in order, all 6 of its links, and the same 3,129 words with none differing; a
planted change to one word was reported as a difference. Excluded files returned 404 on
2026-11-12. The external-link script running inside a frame was tested and passed on
2026-11-12 by the Claude Code session updating fletcherbonds.com, as the owner reported; no
session here saw it. The owner reported the page looks right on desktop and phone the same
day; no session here viewed it.

**Outside the repository.** The GitHub description and topics change with no commit here.
Read from the API at the time above, and unchanged since 2026-11-18, the description is "For
solo developers, not teams. Three Markdown files for Claude Code. Start each session with
one sentence and the agent reports where your project stands. Nothing counts as verified
until it has shown the check can fail." The site's description in `_config.yml` is "A solo
vibe coding methodology", the owner's wording, and it appears in the browser tab after the
title. The topics, read at the same time, are `ai-assisted-coding`, `claude-code`,
`claude-md` and `developer-workflow`.

## Open, not blocking

**Raised by the review, not decided:** whether the memory rule should generalise to any
external context, whether rule 10 belongs in a separate operating-policy section, and whether
the ten should split into always-on rules and procedures. The vendor-neutral note on the
instruction file's name, which the follow-up exchange says the owner proposed, was done in
`973cf51`. The owner's own wording is not in this repository. The only version here is the
reviewer's paraphrase in `docs/review-2026-09-17-followup.md`. None of the other three is
queued.

**Whether rule 1 needs scoping** (raised by the owner on 2026-11-06, undecided). Rule 1 does
not say how it applies to a direct read of the artifact, such as opening a file to confirm a
line, where there is nothing to break. Under the report shape in `template/CLAUDE.md`, every
such read reports "not shown failing" and counts as unverified. Rule 1 and the shape stay as
they are until this is decided. The README's pitch and the GitHub description both depend on
rule 1 as written, so a change to its scope means re-reading both.
