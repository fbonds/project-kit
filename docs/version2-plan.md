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
