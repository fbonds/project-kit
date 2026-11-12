# project-kit

Get the files at [github.com/fbonds/project-kit](https://github.com/fbonds/project-kit).

For solo developers, not teams.

You can build real software with an AI agent now. You can also lose a week to an agent that
says "done and verified" about something that was never checked.

project-kit is three Markdown files. You copy them into your repo, and your agent starts
working like it has a release checklist and a long memory. Nothing to install. Nothing to
learn but two sentences.

Every session starts by telling you where things stand. You type "Read CLAUDE.md and comply,"
and the agent reads the state file, checks the remote, and reports what's in flight and
what's uncommitted before it touches anything. End each session by telling it to save state.
No more re-explaining your project every morning.

Decisions stay decided. When you reject an idea, it goes in the Decided list with the reason
and the alternative it beat. The next session reads it first, so pitching you the same bad
idea on Thursday means arguing with the written reason. When you do change your mind, the old
decision stays on the record, marked as replaced, so you can see why it changed.

You can audit your agent without reading a line of code. Every check comes back in one shape:
what the result was, what was deliberately broken to prove the check can fail, which path it
used, what it actually looked at, and what it didn't check. Silence never means "verified."
If it didn't look, it has to say so.

"Live" means live. Committed, pushed and released are three separate questions with three
separate answers, each dated. The agent has to answer all three, so a fix still on your
laptop gets reported as uncommitted or unpushed.

You stay in charge of what goes public. The agent never pushes. You do. It stages files by
name, so your API keys and scratch files don't ride along in a lazy `git add .`. An optional
settings file blocks the usual commands that break both rules, and a startup hook shows the
agent how the branch stands against the remote before it opens your notes.

Your traps get written down once. Most projects have a dashboard that lags or a cache that
lies. The kit asks about them on day one, and logs each new one the session it bites you.

Your project isn't trapped in a chat window. The working state lives in files in the repo.
Switch machines, hand it to a friend, come back in a month. The repo knows where you were.

The prose gets better too. There's a writing section that steers the agent away from the
phrases that make text sound machine-written, so your README stops sounding like a brochure.

Delete any rule you won't enforce. Keep the rest.

Copy the three files into whatever you're building today, fill in the placeholders, start
your next session with "Read CLAUDE.md and comply," and watch what it tells you.

The rest of this file is the detail behind all of that.

## Where the rules came from

The agent's mistakes come in a small number of recognisable shapes, and almost every one
reduces to a claim checked against a description of a thing rather than against the thing.
Four from one project, over three days:

A release shipped a binary the shell could not execute. It had been verified four separate
ways. Every one of them silently resolved to the developer's own linked working copy rather
than to what a user downloads, so all four passed and the package was broken for everyone
else.

A published security page told reviewers to unzip the package and read its third-party
notices file, and said the file had five entries. The shipped file had eight. The page had
been correct when written and was falsified by a build change nobody re-read it against.

A build guard, written to fail when the installed dependency tree drifted from the lockfile,
could not fail. The success line printed unconditionally, and the failure path queued a
message for a check that ran after the build. It reported success for as long as it
existed.

A saved note told a future session that four agreed items "were agreed but not restated;
recover them from the original list." The original list was in a chat log. Nothing that
reads that note can read a chat log.

The first three were caught by asking a narrower question than "did the check pass", such as
"have you shown this check failing". Care alone had missed them. The fourth was never caught.
The session that arrived afterward paid for it, went looking for a list that was not there,
and had to rebuild it from the README, the changelog and the git log.

These four come from private repositories. You cannot check them from here, and neither can
I, so they are my account. The claims this repository makes about its own files and history
are checkable.

Each rule in the kit is written with its reason attached, because a rule without its reason
reads as taste and gets dropped the first time it is inconvenient.

## What the kit contains

Three files, in `template/`, and an optional fourth.

**`CLAUDE.md`** is read at the start of every session without being asked, which makes it
the only reliable place to put anything. It says to read the state file first and report
what it found, and to treat its facts as dated. It then restates the five standards that
come up most as bullets, names the other five in a sentence, and points at `NEXT.md` for all
ten with their reasons. Next is a short shape for reporting a check. Below that sit the
working rules: how to work, confirm which repo you are in before acting, do not guess, and do
not start queued work unprompted. The writing section comes last, so it can be deleted
without taking anything else with it. The writing rules are preferences rather than checks,
which is why they are kept out of the standards.

**`HOWTOSAVESTATE.md`** is the end-of-session procedure. Check the external world now and
record each fact with its date and method. Write it into the state file. Check stored
memories against the repo, because they load before any file does and a stale one outranks a
correct state file. Commit, then report what could not be verified. It also holds the index
of what every file in the repo is for, which is what stops a document written on Tuesday
from being invisible by Friday.

**`NEXT.md`** is the working state, and the only file that answers "where were we". The
template ships with the ten standards written out and the other sections holding only
instructions, plus questions to answer under Traps. The sections are Traps, Decided, In
flight, Queued, a section answering committed, pushed and released as three separate
questions, and Open. At the top is a block saying every fact below is dated, with the
commands that re-check the moving parts.

**`.claude/settings.json`** is optional, and is the one part that does not depend on the
agent choosing to comply. Its deny rules block `git push`, `git add -A`, `git add --all`,
`git add .`, `git commit -a` and `git commit -am`. Its SessionStart hook fetches from
`origin` and prints the branch status, the behind and unpushed counts against `origin/main`,
and the `Updated` line of `NEXT.md`, and Claude Code adds that output to the session's
context. A deny rule matches the command as written, so `git -C . push` gets past it: it
stops the usual form and is not a security boundary. Tested on 2026-10-30 in a scratch
repository: the hook's output reached the session; `git push`, the same after `cd . &&`,
`git add -A`, `git add .` and `git commit -am` were blocked; `git -C . push` went through.
The `--all` and `-a` rules were not tested.

### The ten standards

Eight of the ten carry a failure that happened, written out in the template. Rule 4 carries
the opposite, two occasions where it caught something before it was built, and rule 10 says
plainly that nothing sits behind it. The summaries here are shorter than what a repo should
keep, and the template asks you to replace each example with your own the first time this
project produces one.

1. No check counts as verified until it has been shown failing on deliberately broken input,
   and the report says what was broken.
2. Never verify through a path that can resolve to your own development copy: a link, a
   global install, a symlink, a running dev server, a cached build.
3. Check claims against the artifact, not the description of it. The published file, the
   fetched page, the built package. Not a commit message, a changelog or a dashboard label.
4. Proposal before code, for anything with a surface: a command, a flag, an API, a schema, a
   page, a public string.
5. Stage explicitly, by path, and confirm what is staged before committing.
6. Describe contents and order, not counts and pagination. Both go stale silently when
   something else changes.
7. Say what was not checked, rather than leaving it out. An omission reads as a verified
   negative.
8. Never point at the conversation. A resumed session can read every file and none of the
   chat.
9. Check stored memories against the repo. They load first, so a wrong one outranks a correct
   state file.
10. One item at a time: show the diff, wait for approval.

Rule 1 is the step test-driven development requires of a unit test: watch it fail before
trusting it. The rule extends that to anything else that reports a pass, such as a build
guard, a release check or a script that checks a published doc. The build guard under "Where
the rules came from" is the case for it.

Numbering is stable, so a rule can be named by number across projects.

## How to use it

```
cp /path/to/project-kit/template/CLAUDE.md .
cp /path/to/project-kit/template/HOWTOSAVESTATE.md .
cp /path/to/project-kit/template/NEXT.md .
grep -n 'PROJECT\|YYYY-MM-DD' CLAUDE.md HOWTOSAVESTATE.md NEXT.md
git add CLAUDE.md HOWTOSAVESTATE.md NEXT.md
git diff --cached --stat
git commit -m 'Add the working-state files'
```

The `grep` prints every line holding a placeholder: `PROJECT`, `PROJECT_OWNER` or
`YYYY-MM-DD`, where the first pattern also matches the second. Fill each one in. Two more
fill-ins carry no placeholder: the commented line at the top of `NEXT.md` that reads "add the
command that checks what this project publishes or deploys", and the commands for the same
thing in `HOWTOSAVESTATE.md`. Until the first is filled, the staleness warning has nothing
behind it.

Run the `grep` before filling anything in. If it prints nothing for `CLAUDE.md` or `NEXT.md`,
you copied this repository's own working files from its root instead of the ones in
`template/`. Those root files are the kit applied to this repository, a small documentation
project, and they are the only worked example here.

The optional settings file goes in `.claude/`:

```
mkdir -p .claude
cp -n /path/to/project-kit/template/.claude/settings.json .claude/
```

`cp -n` will not overwrite. If the repo already has `.claude/settings.json`, merge the deny
list and the `SessionStart` hook into it by hand. The hook assumes a remote named `origin`, a
branch named `main`, and a line in `NEXT.md` starting `Updated`.

Start every session by telling it to read `CLAUDE.md` and comply. Claude Code loads
`CLAUDE.md` into every session by itself, but a session can still start work without reading
`NEXT.md` first or saying that it has, and the instruction is what makes it do both. End
every session by asking it to save state. `HOWTOSAVESTATE.md` is the procedure it follows.
The cold-session runs under Results passed with both habits in place. If the conversation is
compacted mid-session, tell it to read `CLAUDE.md` again and comply.

Delete any rule you will not enforce. A rule nobody enforces teaches the next reader that the
rest are optional. Leave the gap in the numbering rather than closing it, so rule 7 still
means rule 7 when someone names it across projects.

The kit is written for Claude Code. For another agent, rename `CLAUDE.md` to the file that
agent reads at the start of a session, such as `AGENTS.md`, and change the name in the setup
commands. Claude Code reads `AGENTS.md` too when there is no `CLAUDE.md`, from version
2.1.277. Only Claude Code reads the optional settings file. If the agent keeps no memories
between sessions, delete rule 9 and step 3 of `HOWTOSAVESTATE.md`.

## The cold-session test

It checks whether the kit works on a session that did not help write it. The test is cheap
and it only happens if it is written down, so:

**The next time a session starts cold in a repo using this kit, the owner's first message is
"Read CLAUDE.md and comply."** Nothing else: no context, no correction, no hint about what is
in flight. The session should report the state on its own.

It passes if the session names, without being told:

- what the project is and what shipped or published last,
- what is in flight and what is queued but deliberately not started,
- at least one decision that was made and should not be reopened,
- which of its statements it read and which it verified, kept apart rather than presented as
  one kind of fact,
- which specific facts it would re-check before acting, named individually, not the general
  observation that the file is dated. Better still, it runs those checks first.

It fails if the session asks a question the files answer, restates the last commit message as
though it were the state, acts on a dated fact without re-checking it, or presents a dated
fact as current without saying when it was checked.

That last one is the criterion that matters. Every expensive failure behind this kit was a
stale claim that someone trusted. A session can recite the state file perfectly, be correct
as of the date on every line, and still be wrong about the world right now. Reciting is not
the skill being tested.

## Results

Cold-session runs since 16 September 2026: dozens, on most days of most weeks, including 29
and 30 October, across several private repositories for different projects, all in
development at the same time. All passed when the session before had been told to save state
and the new one was told to read `CLAUDE.md` and comply. Each picked up where the last
session left off. That is my report, and it lacks dates for most runs, the repositories,
which are private, and whether `NEXT.md` was stale at the time.

Record each run here, one line: the date, the repo, pass or fail, what it got wrong, and
whether anything in `NEXT.md` was actually stale at the time. A run against a file written
hours earlier proves much less than one a week later, when the registry or the deploy has
moved underneath it, so say which it was. A fail is worth more than a pass, because it names
what the template does not prompt for.

## What the kit cannot carry

The kit is the method. A new project starts without the knowledge, and the kit cannot copy
that in.

On day one the Traps section holds questions and no answers. Every entry in a mature one is a
specific lie a specific tool told, such as a publish command that rewrites a file it was only
supposed to read, and none of those transfer. The Decided section is empty, so the first
month will re-argue things until each decision is written down with its reasoning and the
alternative it beat. A decision then changes by being replaced in the open, with the old
entry kept, which gives a session that disagrees the reasoning it would have to overturn and
does not stop one from ignoring it. The answers to the Traps questions are learned by being
burned, and so are which checks are cheap and which will not run in this environment at all.

What transfers is the habit of writing each of those down the session it is learned, while
the detail is still exact. The kit gives every one of them a place to go.

## Prior art

These sources shaped later additions to the kit. The wording here is the kit's own and
nothing is quoted. Each link was fetched on 2026-11-06 and confirmed to be the page
described, and the Superpowers links are pinned to the commit read that day.

**Superpowers, by Jesse Vincent.** Its [verification skill][sp-verify] makes an agent run a
check fresh and state the result with the evidence attached, and it lists the shortcuts and
excuses it rejects. The report shape in `template/CLAUDE.md` keeps that requirement and adds
what was broken, the path, the artifact and what was not checked. The shortcut list was the
example for seeding Traps with generic questions, and the questions themselves are the kit's
own. Its [test-driven development skill][sp-tdd] requires watching a test fail before writing
the code. Rule 1 applies the same step beyond unit tests, as the paragraph after the ten
standards says.

**Cline's Memory Bank.** The [page][cline] splits a project's state into files by purpose,
with one that changes most often. I looked at splitting `NEXT.md` the same way and kept one
file, because a session has to read Decided before acting, so a split saves no reading. The
instruction to remove finished items from In flight is the kit's own.

**Michael Nygard, "Documenting Architecture Decisions", 2011.** The [post][nygard] keeps a
reversed decision and marks it superseded. The rule in the template's Decided section takes
that from it.

**Martin Fowler, "Architecture Decision Record".** The [page][fowler] states the stricter
rule that an accepted record is superseded and never changed. It credits Nygard with the term
and with the case for a lightweight document focused on the decision, and does not attribute
the stricter rule to him or to anyone else. The template takes that rule, and allows one
added line on the old entry saying what replaced it and when.

[sp-verify]: https://github.com/obra/superpowers/blob/22f0b463e7a5e579904dd6211a520321035526f7/skills/verification-before-completion/SKILL.md
[sp-tdd]: https://github.com/obra/superpowers/blob/22f0b463e7a5e579904dd6211a520321035526f7/skills/test-driven-development/SKILL.md
[cline]: https://docs.cline.bot/best-practices/memory-bank
[nygard]: https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions
[fowler]: https://www.martinfowler.com/bliki/ArchitectureDecisionRecord.html

## License

MIT-0, which is MIT with the attribution clause removed. Copy these files into your own
repo, change them, ship them, and carry no notice. The point is that nobody has to think
about it before pasting a `CLAUDE.md` into a project.
