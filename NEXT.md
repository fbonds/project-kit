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

Updated 2026-11-22. Working state for project-kit. `README.md` is the public argument and
the only documentation, and the GitHub Pages site renders it. `template/` is the kit
itself. `docs/` is the record of results, indexed in `docs/README.md`. There is no design
document and no roadmap; this file holds what is queued.

Two more files hold what changes slowly, and a session reads both at the start, after this
one: `DECISIONS.md`, what was decided and rejected, and `TRAPS.md`, this repository's
failures against the standards and the traps it has hit. After compaction, re-read this
file: Claude Code re-injects `CLAUDE.md` then, and not this file.

## In flight

**The version 2 overhaul, on the `version2` branch** (from 2026-11-21). The decision is under
Decided, "project-kit is the owner's personal methodology". The first seven gaps below were
found on 2026-11-18. On 2026-11-23 a research agent re-read the nine sources from their live
pages against gaps 1 to 8. Its report, with exact quotations and URLs, is
`docs/research-2026-11-23-sources.md`, and its header says which quotations were checked.
Gaps 9 to 17 come from that report. Gaps found during the work are added at the end with
their date.

1. Nothing in the kit covers building. It keeps state and checks work, but nothing takes an
   idea to a specification, a plan and a list of tasks, and nothing says how tests are
   written or run. Spec Kit, Kiro, BMAD, Agent OS and Harper Reed's workflow all start there.
2. Almost all of it is prose that Claude may decide does not apply. Anthropic's
   best-practices page was read as saying that `CLAUDE.md` holds guidelines Claude may set
   aside, and that what must happen every time belongs in a hook, a deny rule or a managed
   setting. `template/.claude/settings.json` has six deny rules and one SessionStart hook.
   Both daily habits, "Read CLAUDE.md and comply" and "save state", depend on the owner
   typing them. Claude Code also has PreCompact, PostCompact, Stop and SessionEnd hooks, and
   the kit uses none of them. Whether each can carry part of a habit is untested.
3. The examples come from one project's release engineering, and the Traps questions in
   `template/NEXT.md` ask only about publishing: dashboards, registries, caches. None asks
   about failures such as a feature that works only with the developer's data, or a fix that
   passes its own test and breaks something else. The original gap also said a new builder
   may not recognise the release examples. That part was written for a reader who does not
   build, and is dropped.
4. The gap that approving a diff is a formality is dropped, because it was written for a
   reader who does not read diffs. What stays is the tension it found: rule 10 asks for diff
   approval, and the README says at line 24 "You can audit your agent without reading a line
   of code."
5. There is no measured evidence. The README's Results are the owner's account of runs in
   private repositories. The harness in github.com/fbonds/project-kit-harness is queued and
   not built. The 2026-11-18 reading found no measured evidence for any of the nine sources
   either.
6. The state file has no size limit. This file was 5,178 words, 466 lines and 31,273 bytes
   on 2026-11-21 by `wc`, against 3,691 words for the three Markdown files in `template/`
   together. The 2026-11-18 evaluation's 4,758 words matches `23edcce:NEXT.md`, the version
   before that day's save. On 2026-11-23, at `44f09a7`, it was 6,011 words, 531 lines and
   36,427 bytes. The 200-line figure on Anthropic's memory page is a target for `CLAUDE.md`
   and a load limit for `MEMORY.md`, and neither applies to this file. A limit that does
   apply is on the context-window page: right after compaction Claude Code re-reads up to
   five recently used files, and "A file over 5,000 tokens comes back as a path reference
   without its content". On 2026-11-23 this file measured about 13,000 tokens, roughly 2.6
   times that limit. Method: a copy of it at `62dc27d`, byte-identical by `cmp`, was the only
   `CLAUDE.md` in a new folder under the home directory, and `/context` in a Claude Code
   session there showed 13.2k tokens of memory files, less the 223 of the owner's global
   `CLAUDE.md`. `/context` calls its figures estimates and rounds to 0.1k. The same copy in a
   folder under `/private/tmp/claude-501` did not load at all, and `/context` showed only the
   223. No per-file figure was read, and no file of known size was measured.
7. The kit does not use what Claude Code provides: plan mode, checkpoints and `/rewind`,
   sandboxing, and auto memory, which the kit treats only as something that goes stale.
   Willison argues that approving every command makes an agent much less effective and that
   the answer is a sandbox. The kit takes no position on any of these.
8. The re-check assumed `main` (found 2026-11-21). The block at the top of this file counted
   `origin/main...main`, so on `version2` it reported on `main`. It now counts the current
   branch against its upstream, and so does the Unpushed paragraph below. The same
   `origin/main...main` is still in the SessionStart hook in
   `template/.claude/settings.json`, in `template/NEXT.md` line 9 and in
   `template/HOWTOSAVESTATE.md` line 68. The README's description of the hook, at line 121,
   says it counts against `origin/main`.
9. The deny rules stop only the usual spelling (found 2026-11-23). The README already says
   so, at lines 123 and 124. The permissions page adds the alternative it names: a
   PreToolUse hook that inspects the full command text before it runs. Untested.
10. This file does not survive compaction the way the root `CLAUDE.md` does (found
    2026-11-23). The root `CLAUDE.md` is re-injected from disk after compaction. This file
    comes back only if it was used recently and is under 5,000 tokens, as gap 6 says. The
    hooks guide names a SessionStart hook with the `compact` matcher for re-injecting
    context. The template's hook has no matcher, which the hooks reference says matches
    compaction too. Untested.
11. Hooks do not run until the workspace trust dialog is accepted (found 2026-11-23). The
    setup steps do not say that the SessionStart re-check is silent until then.
12. Nothing checks that the instruction files loaded (found 2026-11-23). The kit asks Claude
    to say it has read `NEXT.md`, which is a claim. `/context all` lists the memory files
    that loaded, and the owner can run it.
13. No rule for when to start a fresh session (found 2026-11-23). The kit covers ending one.
    Anthropic's best practices say to `/clear` between unrelated tasks and after two failed
    corrections.
14. No marker for an assumption written into a file (found 2026-11-23). Spec Kit uses
    `[NEEDS CLARIFICATION: ...]` and BMAD an `[ASSUMPTION]` tag. Rule 7 covers what a report
    leaves unchecked, not what a saved file assumes.
15. No independent review step (found 2026-11-23). Anthropic's best practices describe a
    second session or a subagent reviewing a diff against the spec.
16. The kit is written for `CLAUDE.md` only (found 2026-11-23). Claude Code can read
    `AGENTS.md` as project instructions. Low priority, since Decided keeps the kit written
    for Claude Code, unless the owner uses a second tool.
17. Personal preferences may belong in `CLAUDE.local.md`, kept out of git (found 2026-11-23).
    The report marks this as its own inference. The owner decides.

Next: not chosen. The owner picks which gap to take first.

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

As of 2026-11-23 03:52 UTC, the evening of 2026-11-22 locally, re-checked against the
remote at that time.

**Uncommitted.** Nothing apart from this file's edit, which is in the commit carrying it.

**Unpushed.** Answer it with `git rev-list --left-right --count '@{upstream}...HEAD'` after a
fetch, on each branch, or `git ls-remote --heads origin` when the remote-tracking ref may be
stale. Snapshot, not to be trusted: GitHub had `main` and `version2` both at `2f30d9f`.
`main` had nothing unpushed. `version2` had `2e12e31`, `a3fa913` and the commit carrying
this sentence unpushed. The owner pushes, so this moves with no commit here to record it. A
commit ID written into this file is the ID at the time of writing, and a rebase replaces it.

**Unreleased.** Nothing is released separately. Pushed to `main` is published, and
`version2` is not published by the site. Last published: `2f30d9f`, pushed to `main` at
23:01:51 UTC on 2026-11-21. `version2` was created on GitHub at 23:02:15 UTC the same day.
Both read from the activity log, and the IDs from `git ls-remote`. No tags, no GitHub
releases, no issues and no pull requests, each read at the time above.

The GitHub Pages site at https://fbonds.github.io/project-kit/ is set to `main`, `/ (root)`.
Its latest build was `built` on `2f30d9f` at 23:02:25 UTC on 2026-11-21, read from the Pages
API at the time above. Every commit from `23edcce` to `2f30d9f` changed only this file, which
the site excludes, so the README it renders is the one in `6ab6386`. The page itself was not
fetched on 2026-11-18 or 2026-11-22.
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
