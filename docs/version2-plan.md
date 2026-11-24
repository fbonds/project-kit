# Version 2 plan

The gaps the version 2 overhaul works through, on the `version2` branch. This file is edited
as gaps close, unlike the rest of `docs/`, which is a record. It was moved here from
`NEXT.md` on 2026-11-23, unchanged. In the gap text, "this file" means `NEXT.md`, and
"Decided" is now in `DECISIONS.md`.

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
6. The state file had no size limit (found 2026-11-18, closed 2026-11-24). Root `NEXT.md`
   measured about 13,000 tokens on 2026-11-23, against the 5,000 above which Claude Code
   brings a file back after compaction as a path only. It was split into `NEXT.md`,
   `DECISIONS.md` and `TRAPS.md` (`9d524e0`), the template followed (`127e5fc`), and the
   template's `NEXT.md` has a 2,000-word limit (`d122ebf`). To measure a file, copy it as the
   only `CLAUDE.md` in a new folder under the home directory, start a session there, and read
   its line in `/context all`. A copy under `/private/tmp/claude-501` does not load. Up to
   three files load at once, as `CLAUDE.md`, `CLAUDE.local.md` and `.claude/CLAUDE.md`.
   `/context` calls its figures estimates. Measured on 2026-11-24 at `4032610`:
   `template/CLAUDE.md` 2.9k tokens for 1,600 words, `template/HOWTOSAVESTATE.md` 2.4k for
   1,345, and `template/NEXT.md` 898 for 475.
7. The kit does not use what Claude Code provides: plan mode, checkpoints and `/rewind`,
   sandboxing, and auto memory, which the kit treats only as something that goes stale.
   Willison argues that approving every command makes an agent much less effective and that
   the answer is a sandbox. The kit takes no position on any of these.
8. The re-check assumed `main` (found 2026-11-21, closed 2026-11-24). The re-check block,
   the Unpushed paragraph, the template's SessionStart hook, `template/NEXT.md` and
   `template/HOWTOSAVESTATE.md` all count the current branch against its upstream, and the
   README says so. The hook prints a line instead of a count on a branch with no upstream.
9. The deny rules stop only the usual spelling (found 2026-11-23). The README already says
   so, at lines 123 and 124. The permissions page adds the alternative it names: a
   PreToolUse hook that inspects the full command text before it runs. Untested.
10. `NEXT.md` did not survive compaction the way the root `CLAUDE.md` does (found
    2026-11-23, closed 2026-11-24). `CLAUDE.md`, which Claude Code re-injects after
    compaction, now tells the session to re-read `NEXT.md` then, here and in the template,
    and `NEXT.md` is kept under the size that comes back whole. Still untested: whether a
    session follows that instruction, and whether the template's SessionStart hook, which
    has no matcher, runs after compaction.
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
