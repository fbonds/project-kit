# Sources re-read for version 2, 23 November 2026

A research agent's report, preserved as written apart from the two edits listed here. It
was asked to re-read nine published methods from their live pages, and to record what each
says about the eight gaps listed under In flight in `NEXT.md` on the `version2` branch at
`44f09a7`. It wrote nothing in this repository.

Two edits, both replacing a local path. In the line beginning "Written 2026-11-23", the
agent's working directory is replaced by "this repository". In the line beginning "The saved
copies", the folder holding the copies saved on 2026-11-18 is replaced by "a folder outside
this repository". Nothing else is changed, and its lines are not rewrapped.

Checked after it was written: 13 of its quotations, chosen by hand rather than at random,
were found on the live pages with curl on 2026-11-23, and a sentence made up for the check
was reported missing. Its other quotations were not checked. Its own reasoning is marked
"Inference" in the text. Nothing in it was tested in Claude Code.

---

# Sources re-read against the eight version 2 gaps

Written 2026-11-23 by a research agent. Read-only on the repo. Working directory: this repository, branch `version2`.

## How this was done, and its limits

- Every page was fetched live on 2026-11-23 with `curl`, printed to stdout, and read. Nothing was saved except this file. (One exception, disclosed: one of this agent's commands redirected `curl` output to `scratchpad/.hooks_tmp` by mistake. It was deleted in the next command. No other file was created, edited or deleted.)
- Claude Code pages were fetched as their Markdown variants, for example `https://code.claude.com/docs/en/best-practices.md`. These are the same docs served as Markdown, and the URL given with each quote is the one fetched. Kiro pages were also fetched as Markdown (`https://kiro.dev/docs/specs.md` and similar), which the Kiro site links as "View as Markdown".
- Other HTML pages were converted to text by stripping tags. Whitespace may be normalised in quotes from them. Curly apostrophes are kept as the page has them.
- Every quotation below comes from the live page unless it is marked "saved copy". No saved copy was needed as a fallback: every live fetch succeeded.
- The saved copies in a folder outside this repository were used only for comparison. Where a quote is said to be "also in the saved copy", that was checked with `grep -F` on the saved `.txt`.
- Quotes were chosen to avoid passages containing em dashes, so they can be quoted in this repo without breaking its writing rule. Where that meant cutting a sentence short, the quote is a contiguous fragment, not a stitched one.
- Notes marked "Inference" are this agent's reasoning, not a source's claim.
- Not checked: whether any hook described here works as documented on the owner's installed Claude Code version. Nothing was run in Claude Code.

## Current kit, for reference

`template/.claude/settings.json` has six deny rules (`git push`, `git add -A/--all/.`, `git commit -a/-am`) and one SessionStart hook with no `matcher`, which prints `git status -sb`, the `origin/main...main` counts and the `Updated` line of `NEXT.md`. Measured today by `wc`: `NEXT.md` in this repo is 531 lines, 6,011 words, 36,427 bytes; the three template Markdown files are 98, 152 and 130 lines (943, 1,510 and 1,238 words).

---

## Gap 1. Nothing covers building: idea to spec, plan, tasks, tests

**Anthropic, best practices** (https://code.claude.com/docs/en/best-practices.md, live)
- "Interview me until you could write the spec, then write it to SPEC.md."
- "Once `SPEC.md` exists, start a fresh session to build from it, so the build begins with a clean context and a written definition of done."
- "write a failing test that reproduces it, then fix it" (from the example prompt for a login bug)
- "Give Claude something it can run that comes back pass or fail. Once it has that, it can keep going on its own and you don't have to watch."
- "If your repo already has one of these, the single most useful line in your `CLAUDE.md` is the command that runs it."
- "use a subagent to review the rate limiter diff against SPEC.md, check every requirement is implemented and the listed edge cases have tests, report gaps that affect correctness and skip style"
- Applies: the smallest building step the kit could add is Anthropic's own: interview to `SPEC.md`, fresh session, failing test first, review the diff against the spec. All of it is prose a solo developer can follow.

**Cline Memory Bank** (https://docs.cline.bot/prompting/cline-memory-bank, redirects to https://docs.cline.bot/best-practices/memory-bank, live)
- `projectbrief.md` is described as "Foundation document with core requirements and goals".
- Applies: a requirements file, but no plan, task or test procedure. Nothing relevant on tests beyond listing "Testing strategies" as an optional extra file.

**Spec Kit** (https://raw.githubusercontent.com/github/spec-kit/main/README.md, live)
- "Define what to build and why, then turn the specification into a plan, tasks,\nand working code." (line break in source)
- "Create a constitution once per project and\nrepeat the remaining steps for each feature."
- "Run these skills in your agent's\nchat, not your terminal, one at a time, reviewing each result before continuing."
- The command sequence: `/speckit-constitution`, `/speckit-specify`, `/speckit-plan`, `/speckit-tasks`, `/speckit-implement`, `/speckit-converge`.

**Spec Kit, spec-driven.md** (https://raw.githubusercontent.com/github/spec-kit/main/spec-driven.md, live)
- "This is NON-NEGOTIABLE: All implementation MUST follow strict Test-Driven Development."
- "1. Unit tests are written\n2. Tests are validated and approved by the user\n3. Tests are confirmed to FAIL (Red phase)"
- "Acceptance scenarios become tests."
- Applies: "Tests are confirmed to FAIL" is the kit's rule 1 applied to building. The kit could state it as the test-writing rule it lacks.

**Kiro** (https://kiro.dev/docs/specs.md, live)
- "Every spec generates three key files that form the foundation of your specification:"
- "**requirements.md** (or **bugfix.md**) - Captures user stories, acceptance criteria, or bug analysis in structured notation"
- "**tasks.md** - Provides a detailed implementation plan with discrete, trackable tasks"
- Applies: three files per feature, with a separate shape for bugs.

**AGENTS.md** (https://agents.md/, live)
- FAQ question: "Will the agent run testing commands found in AGENTS.md automatically?" The answer opens with "Yes" and a qualifier about listing them (not quoted here because the source joins them with an em dash).
- "The agent will attempt to execute relevant programmatic checks and fix failures before finishing the task."
- Applies: the build and test commands belong in the instruction file. No spec or plan process.

**BMAD** (https://docs.bmad-method.org/start/how-bmad-works/, live)
- "BMad\ntakes an intent of any size through four stages, and keeps what was decided in\none place, the ticket, so that each new session builds from the same spec."
- Stage "Clarify" ends with "A clear intent: what should be true, what must not change, what is out of scope".
- "A small fix starts at Build and verify, and a vague idea at Clarify."
- (https://docs.bmad-method.org/start/build-your-first-change/, live) "It clarified the request, presented a plan for your approval, wrote\nthe program, and checked its work before showing you the result."
- Applies: BMAD scales the process to the size of the change. The kit could say which steps a one-line fix skips.

**Agent OS** (https://buildermethods.com/agent-os/shape-spec, live, public part)
- "The /shape-spec command is designed to run in plan mode. It gathers context and structures planning for significant work, creating a spec folder that persists beyond the conversation."
- "The command builds a plan with “Save spec documentation” as Task 1, then presents the full plan."
- "Use plan mode directly when:" followed by "It’s a quick task" and "Context doesn’t need to persist".
- Applies: plan mode plus saving the plan to a dated folder. That is a direct answer to "plan mode output dies with the chat", which the kit's rule 8 cares about.

**Harper Reed** (https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/, live)
- "tl:dr; Brainstorm spec, then plan a plan, then execute using LLM codegen. Discrete loops."
- "Ask me one question at a time so we can develop a thorough, step-by-step spec for this idea."
- "I like to save it as spec.md in the repo."
- "I like to save this as prompt_plan.md in the repo."
- "Your codegen tool should be able to check off the todo.md while processing. This is good for keeping state across sessions."
- Applies: spec.md, prompt_plan.md, todo.md, with a separate per-task method for existing code: "The planning is done per task, not for the entire project."

**Willison** (https://simonwillison.net/2025/Sep/30/designing-agentic-loops/, live)
- "A common theme in all of these is automated tests. The value you can get from coding agents and other LLM coding tools is massively amplified by a good, cleanly passing test suite."
- Applies: tests first as the thing that makes the agent useful. No spec or plan process.

---

## Gap 2. Prose Claude may set aside; enforcement belongs in hooks, deny rules, settings

**Anthropic, best practices** (https://code.claude.com/docs/en/best-practices.md, live; the first two quotes are also in the saved copy)
- "If something has to happen every time, make it a hook, a deny rule, or a managed setting. `CLAUDE.md` is for guidelines, and Claude is allowed to decide a guideline doesn't apply."
- "But no matter how strongly you word it, whether Claude follows that line on a given turn is still Claude's call."
- "If you keep adding emphasis to a `CLAUDE.md` line and Claude still misses it, that's a sign the line belongs in a hook. The reverse holds too: if you have hooks for things that are only preferences, delete them and let Claude decide."
- "Don't overdo it, though: a hook is for a rule with *zero* exceptions"
- "Whatever the scope, keep the enforced set small."
- "A `prompt` or `agent` hook asks *another model* to decide, so it isn't deterministic either."
- "You can also say `don't push until I've reviewed` in the conversation, and the classifier [treats that as a block signal](...). It's still a model reading the transcript, and the sentence can get lost when the conversation compacts, so anything that matters belongs in a deny rule." (link target elided)
- Applies: the page confirms the 2026-11-18 reading. It also argues the other way: preferences should stay prose. The kit has to sort its ten standards into "zero exceptions" and "guideline".

**Anthropic, memory** (https://code.claude.com/docs/en/memory.md, live)
- "Claude treats CLAUDE.md files and auto memory as context. They aren't enforced configuration."
- "CLAUDE.md content is delivered as a user message after the system prompt, not as part of the system prompt itself."
- "If the instruction is something that must run at a specific point, such as before every commit or after each file edit, write it as a [hook](...) instead."
- "Project-root CLAUDE.md survives compaction: after `/compact`, Claude re-reads it from disk and re-injects it into the session."

**Anthropic, hooks reference** (https://code.claude.com/docs/en/hooks.md, live; no saved copy of this page). What each event can carry:
- SessionStart: "**`UserPromptSubmit`, `UserPromptExpansion`, `SessionStart`, and `PostModelSwitch`**: Claude Code adds plain-text stdout as context that Claude can see and act on." Its matchers include "`compact` | Auto or manual compaction".
- Matcher omitted: "`\"*\"`, `\"\"`, or omitted | Match all". So the kit's SessionStart hook, which has no matcher, also runs after compaction.
- PreCompact: "When a PreCompact hook exits 0 and doesn't block, Claude Code uses its stdout as instructions for the compaction summary. Keep that stdout under 10,000 characters per hook." It can also block: "Exit with code 2 to block compaction."
- PostCompact: "PostCompact hooks have no decision control." Its input carries "`compact_summary`".
- Stop: "`decision` | `\"block\"` prevents Claude from stopping." and "Claude Code applies an 8-consecutive-continuation cap". Also: "Does not run if\nthe stoppage occurred due to a user interrupt."
- SessionEnd: "SessionEnd hooks have no decision control. They can't block session termination but can perform cleanup tasks. Claude Code discards their [JSON output fields](...)", and "SessionEnd hooks have a default timeout of 1.5 seconds."
- Exit-code table: "`SessionEnd` | No | Shows stderr to user only".
- Workspace trust: "**Interactive session**: Claude Code holds back hooks from every settings file, including your own `~/.claude/settings.json`, until you accept the [workspace trust dialog](...)".
- Applies, per habit. Inference: "Read NEXT.md first" can be partly carried by SessionStart, which can print the re-check or the top of `NEXT.md` into context, including after compaction. "Save state" cannot be carried by SessionEnd: Claude never sees SessionEnd output and the hook gets 1.5 seconds by default, so it can only run a shell command, not have Claude write `NEXT.md`. A Stop hook can refuse to let a turn end (for example while the tree is dirty and `NEXT.md` is unchanged), but it fires at the end of every turn, so a rule tied to it fires constantly. PreCompact can tell the summariser what to keep. All of this is untested.

**Anthropic, hooks guide** (https://code.claude.com/docs/en/hooks-guide.md, live)
- "Use a `SessionStart` hook with a `compact` matcher to re-inject critical context after every compaction."
- "Hooks are user-defined shell commands. Claude Code runs them at specific points in its lifecycle, which gives you deterministic control"

**Anthropic, permissions** (https://code.claude.com/docs/en/permissions.md, live; no saved copy)
- "It doesn't match the same program invoked in a different form, so a deny or ask rule covers the invocation Claude usually produces and isn't a security boundary around the program."
- Table row: "`Bash(git push *)` | `git push origin main` | `git -C . push origin main`, `git -c push.default=current push origin main`"
- Applies: the kit's six deny rules are the right mechanism but stop only the usual spelling. See new gap N1.

**Cline** (https://docs.cline.bot/prompting/cline-memory-bank, live)
- "I MUST read ALL memory bank files at the start of EVERY task - this is not optional."
- Applies: Cline relies on exactly the emphasised prose Anthropic says not to rely on. It is a counter-example, not support.

**Kiro hooks** (https://kiro.dev/docs/hooks/types.md, live; this subpage was not saved)
- Triggers listed: "Prompt Submit", "Agent Stop", "Session Start", "Session End", "Pre Compaction", "Post Compaction".
- Pre Compaction: "In the IDE, Kiro gives the command's standard output to the summarizer as guidance."
- Applies: Kiro has the same events, so this is not Claude-Code-specific advice.

**AGENTS.md** (https://agents.md/, live): "The closest AGENTS.md to the edited file wins; explicit user chat prompts override everything." Applies: the instruction file ranks below the chat, which is why typed daily habits beat the file.

**Spec Kit** (spec-driven.md, live): "These gates act as compile-time checks for architectural principles. The LLM cannot proceed without either passing the gates or documenting justified exceptions". Applies: Spec Kit's "gates" are checklist prose in templates. It says "cannot proceed", but nothing in the quoted text describes a mechanism that enforces it.

**BMAD, Agent OS, Harper, Willison**: nothing relevant on prose versus enforcement.

---

## Gap 3. Examples and Traps cover only release engineering

**Kiro bugfix specs** (https://kiro.dev/docs/specs/bugfix-specs.md, live; not in the saved set)
- "identify the root cause, understand what should change, and explicitly preserve what shouldn't."
- Section headings: "**Current Behavior (Defect)**", "**Expected Behavior (Correct)**", "**Unchanged Behavior (Regression Prevention)**"
- Listed as a fit: "Situations where previous fix attempts caused regressions"
- Applies: the "fix passes its own test and breaks something else" trap, with a fix: write down what must not change before fixing.

**Kiro correctness** (https://kiro.dev/docs/specs/correctness.md, live)
- "Traditional unit tests only check specific examples, and whoever writes them - human or AI - is limited by their own biases."
- Applies: a trap question: "does the test only cover the example the same session thought of?"

**Spec Kit, spec-driven.md** (live)
- "Prefer real databases over mocks"
- "**Integration Over Isolation**: Test in real environments, not artificial ones"
- Applies: the build-side form of rule 2. A test against a mock is checking a stand-in for the artifact.

**Spec Kit README** (live): "The final verdict is\n`verified`, `partial`, or `failed`; only `verified` confirms a successful fix." Applies: a bug fix is not done until the original symptom is re-checked.

**Anthropic, best practices** (live)
- What belongs in CLAUDE.md includes "Places where the code is misleading: an old pattern that's everywhere but that new code must not copy, or a directory that looks unused but isn't"
- "A reviewer that's asked to find problems will always find *something*. If you fix every finding, you end up with extra abstraction layers and tests for cases that can't happen."
- Applies: two build-side Traps prompts: misleading code, and the review that always finds something.

**BMAD** (how-bmad-works, live): Clarify ends with "what must not change". Same idea as Kiro's unchanged behaviour.

**Willison** (live): "have your agent benchmark the query and then add and drop indexes (in an isolated development environment!)" and "Try to provide credentials to test or staging environments where any damage can be well contained." Applies: the "only works with the developer's data" trap, from the other side: give the agent a separate environment.

**Cline, AGENTS.md, Agent OS, Harper**: nothing relevant. (Harper's "over my skis" is under gap 4.)

---

## Gap 4. Rule 10 asks for diff approval; the README says "You can audit your agent without reading a line of code"

Checked: `README.md` line 24 on `version2` reads "You can audit your agent without reading a line of code. Every check comes back in one shape:".

**Anthropic, best practices** (live)
- "**Manual mode**: you approve every edit and every command that isn't read-only yourself. Safe, but after the tenth prompt you start approving without reading, and nothing moves while you're away from the keyboard."
- "Whichever option you use, ask Claude for *evidence*: the command it ran and its output, or the screenshot. \"All tests pass\" on its own tells you very little, and reading the output is faster than rerunning the check yourself."
- "A second session is also the easiest independent reviewer you can get."
- "Delegate to a subagent for a better answer | Handing the same task to a subagent doesn't make the answer any better. A fresh reviewer does help, because it hasn't seen your reasoning"
- Applies: Anthropic separates approving each action (which goes stale) from reading evidence (which the kit's report shape already asks for). This supports the README's claim for checks and weakens rule 10 only where it means per-command approval. Diff approval is a different thing that this page does not address.

**Spec Kit README** (live): "one at a time, reviewing each result before continuing." Applies: per-step human review of artifacts (spec, plan, tasks), not of code.

**BMAD** (how-bmad-works, live)
- "Reading those is your job, because the next session will treat whatever is written as settled."
- "A build stops at built; you, or a script or AI session you direct, mark a\nstory done."
- Applies: BMAD puts the human read on the written assumptions and on marking done, not on the code.

**Kiro** (https://kiro.dev/docs/specs.md, live): "It opens [Markdown Review](...), where you can comment on exact passages and send your comments to Kiro at once." Applies: review is of spec documents.

**Harper** (live): "you have to aggressively keep track of what’s going on because you can easily get ahead of yourself." and "At least you will have a doc you can double-check against."

**Willison** (live): "Coding agents like Claude Code counter this by defaulting to asking you for approval of almost every command that they run." then "This is kind of tedious, but more importantly, it dramatically reduces their effectiveness at solving problems through brute force."

**Agent OS** (shape-spec, live): "Standards guide, not dictate" and "They inform the plan but aren’t always mandatory".

**Cline, AGENTS.md**: nothing relevant.

---

## Gap 5. No measured evidence

No source read today offers a measurement of its own method's effect. What each does say:

- **Anthropic best practices** (live): no measurement. It points to a usage measure, not an outcome measure: "[`/usage`](...) is the first place to look." The same page states "Every one of these was good advice when it was written" about its retired advice, with no data.
- **Spec Kit, spec-driven.md** (live): time figures with no stated source. "1. Write a PRD in a document (2-3 hours)" through "Total: ~12 hours of documentation work", against "# Step 1: Create the feature specification (5 minutes)".
- **Kiro** (https://kiro.dev/docs/specs.md, live): "For most feature specs, this cuts execution time significantly without any setup." No figure.
- **AGENTS.md** (live): adoption, not effect: "used by over 60k open-source projects."
- **BMAD README** (https://raw.githubusercontent.com/bmad-code-org/BMAD-METHOD/main/README.md, live): a tool for measuring, not a measurement: the Toolsmith module's "`bmad-eval` measures them" (skills, agents and modules).
- **Harper** (live): anecdote: "I have built so so many things using this workflow".
- **Willison** (live): anecdote, and a negative one: "In that particular case the results weren’t useful enough to describe in more detail".
- **Cline, Agent OS**: nothing relevant.
- Applies: the kit is not behind its sources on evidence. A harness that measures would put it ahead, and the README could say plainly that none of the sources measure either.

---

## Gap 6. The state file has no size limit

**Anthropic, memory** (live)
- "**Size**: target under 200 lines per CLAUDE.md file. Longer files consume more context and reduce adherence."
- "[Imports](#import-additional-files) help you organize a long file but don't reduce its context cost, because imported files load together with the CLAUDE.md that imports them."
- On `MEMORY.md`: "If the file is near a limit, Claude Code reminds Claude to shorten it: keep one line per entry, move detail into topic files, and merge or drop stale entries."
- "This limit applies only to `MEMORY.md`. Claude gets the whole of each CLAUDE.md file that loads at launch, as long as the file is 4 MiB or smaller."
- Applies: the 200-line figure is a target for CLAUDE.md and a hard load limit for MEMORY.md. Neither is about a file like NEXT.md, which loads only when read. This confirms the existing gap note's caution.

**Anthropic, context window** (https://code.claude.com/docs/en/context-window.md, live; no saved copy)
- "Right after compaction, Claude Code re-reads up to five of the files Claude has read or edited in the session, choosing the ones modified most recently. A file over 5,000 tokens comes back as a path reference without its content"
- Table row: "Project-root CLAUDE.md and unscoped rules | Re-injected from disk"
- Table row: "Context that hooks added earlier | Summarized with the rest of the conversation"
- Applies: this is a concrete size limit that does touch NEXT.md. After compaction, a NEXT.md over 5,000 tokens is not re-read. Not measured: NEXT.md's token count. At 36,427 bytes it is likely over 5,000 tokens, but that is an estimate.

**Anthropic, best practices** (live)
- "Only write down what Claude can't find by reading the repo, or what it would otherwise spend time rediscovering every session."
- "If the line is getting lost in a long file, the file needs to be shorter."
- "Describe your architecture and file layout in `CLAUDE.md` | Claude reads the repo itself. Only write down what isn't in there."

**Cline** (live): six files rather than one, with "activeContext.md changes most frequently; update it after each session" and "progress.md tracks milestones; review it when resuming work". Applies: split the fast-changing part from the slow-changing part.

**Kiro steering** (https://kiro.dev/docs/steering.md, live): "**Keep Files Focused** - One domain per file". Also conditional loading: "Files are automatically included only when working with files that match the specified pattern."

**BMAD** (how-bmad-works, live): state lives per ticket: "A story is\nusually just an entry in its epic’s tickets.toml: one line of what it\ndelivers and how it is verified." and a build too big for one session writes "the rest to deferred-work.md".

**Agent OS** (shape-spec, live): each spec goes in its own dated folder: "Folder names are auto-generated: YYYY-MM-DD-HHMM-{feature-slug}/". Applies: finished work leaves the state file and lives in a dated record.

**Harper** (live): state is a checklist, `todo.md`. No size guidance.

**Spec Kit, AGENTS.md, Willison**: nothing relevant on size.

---

## Gap 7. The kit ignores plan mode, checkpoints and /rewind, sandboxing, auto memory

**Plan mode** (https://code.claude.com/docs/en/permission-modes.md, live)
- "Plan mode tells Claude to research and propose changes without making them."
- "Except in interactive terminal sessions with [bypass permissions available](...), edits stay blocked until you approve the plan."
- "Press `Ctrl+G` to open the proposed plan in your default text editor and edit it directly before Claude proceeds."
- (https://code.claude.com/docs/en/context-window.md, live) "The plan Claude wrote in [plan mode](...) | Re-injected from disk"
- Applies: plan mode is the harness version of rule 4 ("Proposal before code"), enforced rather than prose. The live best-practices page does not mention plan mode at all (0 matches, and 0 in the saved copy).

**Auto mode is now the default** (best practices, live)
- "Interactive terminal and VS Code sessions start in auto mode."
- "Auto mode is a classifier model judging each action rather than a hard rule. It's good at that, but like any judgment call it can be wrong. You can also tune what it treats as risky, and your org can turn it off entirely, so your \"never\" rules belong in deny rules or hooks."
- Applies: the kit takes no position on permission modes, but a fresh session will be in auto mode. The deny rules still apply: "`deny` rules hold in every permission mode, including auto and `bypassPermissions`".

**Checkpoints** (https://code.claude.com/docs/en/checkpointing.md, live)
- "Every prompt you send that starts a turn creates a new checkpoint"
- "A file that only Bash commands changed isn't tracked and stays as it is. To revert it, use version control, such as Git."
- "Checkpoints are designed for quick, session-level recovery. For permanent version history and collaboration, continue using version control, such as Git, for commits, branches, and long-term history."
- (best practices, live) "That makes it low-risk to try the bolder approach first and rewind if it doesn't work out."
- Applies: `/rewind` is the undo for an unapproved diff inside a session. It does not replace the kit's commit discipline.

**Sandboxing** (https://code.claude.com/docs/en/sandboxing.md, live)
- "The sandbox is off by default."
- "The sandbox covers shell commands only. Claude's file tools, MCP servers, and hooks [run outside it](...)."
- Default reads: "Most of the machine, including credential files such as `~/.ssh` and `~/.aws/credentials`"
- (permission-modes, live) A listed option: "Manual mode plus the Bash sandbox in [auto-allow mode](...)", with "Deny rules still apply, and ask rules that name a command, such as `Bash(git push *)`, still prompt."

**Willison** (live), as recorded in the gap: "If you want to run YOLO mode anyway, you have a few options:" then "Run your agent in a secure sandbox that restricts the files and secrets it can access and the network connections it can make." He also says "Coding agents themselves implement various levels of sandboxing, but so far I’ve not seen convincing enough documentation of these to trust them." Note: that post is dated 2025-09-30. The quote is about documentation at that date.

**Auto memory** (https://code.claude.com/docs/en/memory.md, live)
- "Auto memory is on by default in local sessions."
- Its `project` type stores "ongoing work, deadlines, and decisions that Claude can't derive from the code or git history"
- "It also skips anything your CLAUDE.md files already say."
- "When Claude writes a memory file that begins with YAML frontmatter, Claude Code records the write time in a `modified` frontmatter field as an ISO 8601 timestamp."
- "Auto memory is machine-local."
- Applies: auto memory's `project` type overlaps NEXT.md's Decided and In flight sections. Auto memory skips what CLAUDE.md says, but NEXT.md is not CLAUDE.md. Inference: the same decision can therefore be stored in both places, and the kit's rule 9 is about that drift. The dated `modified` field is the kit's "every fact dated" idea, done by the harness.

**Other sources**: Kiro has the same features ("Plan mode", "Checkpoints and rewind", "Local command sandbox", "Memory", "Compaction" in its docs nav, live), but those subpages were not read. Agent OS uses plan mode (gap 1). Cline lists "Plan & Act Mode" and "Checkpoints" in its nav (not read). Spec Kit, BMAD, AGENTS.md, Harper: nothing relevant.

---

## Gap 8. The re-check assumed `main`

- **Anthropic, settings reference** (https://code.claude.com/docs/en/settings-reference.md, live): "The snapshot holds the current branch, the main branch, `git status` output, and recent commits. Claude Code reads it when a conversation starts." Applies: Claude Code already gives Claude the branch name at start. It does not give ahead and behind counts against the upstream, so the hook still adds something.
- **Anthropic, context window** (live): "If the session started with one, Claude Code reads a fresh one from your repository" (git status snapshot after compaction).
- **Spec Kit, spec-driven.md** (live): `/speckit.specify` "Creates branch \"003-chat-system\"". Applies: a spec workflow puts each feature on its own branch, so a re-check hard-coded to `main` gives the wrong answer for every feature, not only on `version2`.
- **Anthropic, best practices** (live): "the one branch it may push to" (from the unattended-run checklist).
- **Cline, Kiro, AGENTS.md, BMAD, Agent OS, Harper, Willison**: nothing relevant.

---

## New gaps the sources expose

**N1. The deny rules stop only the usual spelling.** (https://code.claude.com/docs/en/permissions.md, live) "a deny or ask rule covers the invocation Claude usually produces and isn't a security boundary around the program." The documented example is the kit's own rule: "`Bash(git push *)` | `git push origin main` | `git -C . push origin main`, `git -c push.default=current push origin main`". It names the alternative: "To inspect the full command text with your own logic before it runs, use a [PreToolUse hook](...)". Applies: the README should not describe the six rules as a guarantee. Not checked: whether the README currently does.

**N2. NEXT.md does not survive compaction the way CLAUDE.md does.** (https://code.claude.com/docs/en/context-window.md, live) "Project-root CLAUDE.md and unscoped rules | Re-injected from disk" against "A file over 5,000 tokens comes back as a path reference without its content". (memory.md, live) "If an instruction disappeared after compaction, it was given only in conversation". Options the docs name: a SessionStart hook with the `compact` matcher, or an import: "CLAUDE.md files can import additional files using `@path/to/import` syntax." Inference: importing NEXT.md would load all 531 lines into every session, which collides with gap 6.

**N3. Hooks do not run until the folder is trusted.** (hooks.md, live) "Claude Code holds back hooks from every settings file, including your own `~/.claude/settings.json`, until you accept the [workspace trust dialog](...)". And for `-p`: "Claude Code never shows the dialog and treats the folder as trusted". Applies: the setup steps should say the SessionStart re-check is silent until trust is accepted.

**N4. No check that the instruction files loaded.** (memory.md, live) "Run `/context all` and check the list under **Memory files** to verify the CLAUDE.md and CLAUDE.local.md files that should load at launch." (best practices, live) "`/doctor prompt-audit` flags instructions that were written for older models, point at files that no longer exist, or [contradict each other](...)." Applies: the kit asks Claude to say it read NEXT.md, which is a claim, not a check. `/context all` is a check the owner can run.

**N5. No rule for when to start a fresh session.** (best practices, live) "`/clear` between unrelated tasks." and "Watch the first minute, press `Esc` the moment Claude drifts, and after two failed corrections run `/clear` and write a better prompt instead of a third." (BMAD how-bmad-works, live) a build session is "One goal: roughly 500 changed lines, not counting tests, in a handful of files, started in a fresh chat". Applies: the kit covers ending a session (save state) but not when to end one.

**N6. No marker for assumptions written into files.** (Spec Kit spec-driven.md, live) "Use [NEEDS CLARIFICATION: specific question]" and "This prevents the common LLM behavior of making plausible but potentially incorrect assumptions." (BMAD how-bmad-works, live) "an [ASSUMPTION] tag in a\ndocument, an Assumption: or Open question: line in a ticket." Applies: rule 7 says to state what was not checked in a report. Neither the rule nor the templates give a marker that survives in a saved file, where BMAD says "the next session will treat whatever is written as settled."

**N7. No independent review step.** (best practices, live) "A fresh reviewer does help, because it hasn't seen your reasoning" and the reviewer prompt ending "report gaps that affect correctness and skip style". Applies: the kit's only reviewer is the owner. A second session reviewing against the spec is cheap and fits one item at a time.

**N8. The kit is CLAUDE.md-only.** (memory.md, live) "Claude Code can read [`AGENTS.md`](...) as your project instructions, so a repository already set up for other coding agents works without adding a `CLAUDE.md`, an import, or a setting." (Kiro steering, live) "Kiro supports providing steering directives via the [AGENTS.md](https://agents.md/) standard." Applies: low priority for a Claude-Code-only methodology. It matters only if the owner uses a second tool.

**N9. Personal preferences sit in the shared file.** (best practices, live) "Your personal preferences go in `CLAUDE.local.md` instead of `CLAUDE.md`, and you add that file to `.gitignore` so it stays out of the repo." Applies: partly. The kit's Writing section governs public prose, which is a project rule. How the owner wants to be written to is personal. Inference only. The owner should decide.

---

## Fetch status and differences from the 2026-11-18 saved copies

| Source | URL fetched | Live | Saved copy comparison |
| :- | :- | :- | :- |
| Claude Code best practices | https://code.claude.com/docs/en/best-practices.md | OK | `bp.txt`: 3 changed lines. Material: live removed "None of this replaces your deterministic controls, because it runs *after* them. Deny and ask rules and `PreToolUse` hooks apply before the classifier sees anything, so a deny rule blocks in auto mode exactly like it does everywhere else." The "deny rules hold in every permission mode" sentence is still live. Minor: "`command` or `http` hook" is now "`command`, `http`, or `mcp_tool` hook". |
| Claude Code memory | https://code.claude.com/docs/en/memory.md | OK | `mem.txt`: material on gap 6. Saved said `MEMORY.md` loads in "Every session (first 200 lines or 25KB)". Live says "Sessions with [auto memory on](...), up to the first 200 lines or 25KB". The "not enforced configuration" sentence was moved and reworded. Same meaning. |
| Claude Code hooks guide | https://code.claude.com/docs/en/hooks-guide.md | OK | `hooks.txt`: 3 minor wording changes. |
| Claude Code hooks reference | https://code.claude.com/docs/en/hooks.md | OK | No saved copy. |
| Claude Code permission modes | https://code.claude.com/docs/en/permission-modes.md | OK | `pm.txt`: wording changes. Saved `default` row "Reads only"; live lists reads in working directories "and other actions that need no approval". Not material to the gaps. |
| Claude Code checkpointing | https://code.claude.com/docs/en/checkpointing.md | OK | No saved copy. |
| Claude Code sandboxing | https://code.claude.com/docs/en/sandboxing.md | OK | No saved copy. |
| Claude Code context window | https://code.claude.com/docs/en/context-window.md | OK | No saved copy. |
| Claude Code permissions | https://code.claude.com/docs/en/permissions.md | OK | No saved copy. |
| Claude Code settings reference | https://code.claude.com/docs/en/settings-reference.md | OK | No saved copy. |
| Claude Code common workflows, settings | https://code.claude.com/docs/en/common-workflows.md, https://code.claude.com/docs/en/settings.md | OK (status only, not read) | Not compared. |
| Cline Memory Bank | https://docs.cline.bot/prompting/cline-memory-bank | OK, redirects to https://docs.cline.bot/best-practices/memory-bank | `cline.txt`: every quote used is also in the saved copy. |
| Spec Kit README | https://raw.githubusercontent.com/github/spec-kit/main/README.md (also https://github.com/github/spec-kit, status only) | OK | Byte-identical to `speckit.txt`. |
| Spec Kit spec-driven.md | https://raw.githubusercontent.com/github/spec-kit/main/spec-driven.md | OK | Byte-identical to `sdd.txt`. |
| Kiro specs | https://kiro.dev/docs/specs.md (HTML https://kiro.dev/docs/specs/ and /feature-specs/ also OK) | OK | `kiro.txt`/`kfeat.txt` saved the HTML. Compared by quote, no difference found. Bugfix and correctness subpages were not saved. |
| Kiro steering | https://kiro.dev/docs/steering.md | OK | `ksteer.txt`: the four quotes checked are all present. |
| Kiro hooks | https://kiro.dev/docs/hooks.md, https://kiro.dev/docs/hooks/types.md | OK | `khooks.txt` has the main page quotes. The types subpage (compaction and stop triggers) was not saved. |
| Kiro bugfix, correctness | https://kiro.dev/docs/specs/bugfix-specs.md, https://kiro.dev/docs/specs/correctness.md | OK | Not saved. |
| AGENTS.md | https://agents.md/ | OK | `agents.txt`: all quotes present, including "used by over 60k". |
| BMAD README | https://raw.githubusercontent.com/bmad-code-org/BMAD-METHOD/main/README.md (also GitHub HTML, status only) | OK | Byte-identical to `bmad.txt`. |
| BMAD docs | https://docs.bmad-method.org/start/how-bmad-works/, https://docs.bmad-method.org/start/build-your-first-change/, https://docs.bmad-method.org/ | OK | `bhow.txt`: quotes checked are present. `bplan.txt` is a redirect stub from /plan/choose-a-planning-path/ to /start/how-bmad-works/. |
| Agent OS | https://buildermethods.com/agent-os, /concepts, /workflow, /shape-spec, /file-structure; https://raw.githubusercontent.com/buildermethods/agent-os/main/README.md | OK | Quotes checked are present. GitHub README byte-identical to `aos_gh.txt`. Setup is behind "Free & open source. Enter your email for instant access." No form was submitted. |
| Harper Reed | https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/ | OK | `harper.txt`: quotes checked are present. |
| Simon Willison | https://simonwillison.net/2025/Sep/30/designing-agentic-loops/ | OK | `sw.txt`: quotes checked are present. |
