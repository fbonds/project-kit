# project-kit

Three files you copy into a new repo on day one, plus the reasoning behind them. They set
how an agentic coding session records what it verified, what it only read, and what it never
checked at all.

The failure this addresses is not that the agent is unreliable. It is that it is confidently
wrong in a small number of recognisable shapes, and almost every one reduces to a claim
checked against a description of a thing rather than against the thing.

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
message for a check that ran after the build. It reported success for as long as it existed,
until someone broke the tree on purpose to watch it catch.

A saved note told a future session that four agreed items "were agreed but not restated;
recover them from the original list." The original list was in a chat log. Nothing that
reads that note can read a chat log.

None of those were caught by the agent being careful. They were caught by asking a narrower
question: not "did the check pass" but "have you shown this check failing." Every rule in
the kit came out of one of those moments, and each is written with the reason attached,
because a rule without its reason reads as taste and gets dropped the first time it is
inconvenient.

Those four happened in a private repository. You cannot check them from here, and neither can
I. They are attested by the author rather than verifiable by a reader, which makes them the
weakest evidence in this file, and a file about checking claims should say so rather than let
a reader assume the examples were open to inspection. The claims about this repository, its
files and its history are a different matter: those are checkable, and the second test below
exists to have them checked.

## What the kit contains

Three files, in `template/`.

**`CLAUDE.md`** is read at the start of every session without being asked, which makes it the
only reliable place to put anything. It says to read the state file first and treat its facts
as dated. It then restates the five standards that come up most as bullets, names the other
five in a sentence, and points at `NEXT.md` for all ten with their failures attached. Below
that sit the working rules: how to work, confirm which repo you are in before acting, do not
guess, and do not start queued work unprompted. The writing section comes last, so it can be
deleted without taking anything else with it. The writing rules are preferences rather than
checks, which is why they are kept out of the standards.

**`HOWTOSAVESTATE.md`** is the end-of-session procedure. Check the external world now and
record each fact with its date and method. Write it into the state file. Check stored
memories against the repo, because they load before any file does and a stale one outranks a
correct state file. Commit, then report what could not be verified. It also holds the index
of what every file in the repo is for, which is what stops a document written on Tuesday
from being invisible by Friday.

**`NEXT.md`** is the working state, and the only file that answers "where were we". The
template ships with the ten standards written out and the other sections empty apart from
instructions: Traps, Decided, In flight, Queued, a section answering committed, pushed and
released as three separate questions, and Open. At the top is a block saying every fact below
is dated, with the commands that re-check the moving parts.

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

Numbering is stable, so a rule can be named by number across projects.

## How to use it

```
cp /path/to/project-kit/template/CLAUDE.md .
cp /path/to/project-kit/template/HOWTOSAVESTATE.md .
cp /path/to/project-kit/template/NEXT.md .
grep -rn 'PROJECT\|PROJECT_OWNER\|YYYY-MM-DD' CLAUDE.md HOWTOSAVESTATE.md NEXT.md
git add CLAUDE.md HOWTOSAVESTATE.md NEXT.md
git diff --cached --stat
git commit
```

The `grep` is the fill-in list. Three placeholders, plus one commented line in the block at
the top of `NEXT.md`, reading "add the command that checks what this project publishes or
deploys". Replace it with that command. Until it exists, the staleness warning has nothing
behind it.

Delete any rule you will not enforce. A rule nobody enforces teaches the next reader that the
rest are optional.

## The cold-session test, which has not been run yet

Nothing here has been proven to work on a session that did not help write it. The test is
cheap and it only happens if it is written down, so:

**The next time a session starts cold in a repo using this kit, the owner asks what it
concludes about the state before telling it anything.** Nothing else in the first message: no
context, no correction, no hint about what is in flight.

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
stale claim being trusted, not a missing one. A session can recite the state file perfectly,
be correct as of the date on every line, and still be wrong about the world right now.
Reciting is not the skill being tested.

Record the result below, pass or fail, with the date and what was missing. A fail is worth
more than a pass, because it names what the template does not prompt for.

## The claim-review test, which has been run once

This one can run today, on any repo using the kit, and it does not need a fresh session.

Give an agent the repository and ask it to audit every externally verifiable claim in the
README against the artifact that claim describes. Do not say which claims are suspect, do not
say how many discrepancies there are, and do not say whether there are any.

A claim is externally verifiable when something in or reachable from the repo settles it: a
description of what a file contains, a count, a statement about what the template holds, a
command that is supposed to work, a link that is supposed to resolve.

It passes if it finds the discrepancies that are there and says, for each claim it clears,
which artifact it opened. It fails if it reports the README as accurate without opening the
files, reviews the argument instead of the claims, or accepts a claim because the document
around it is coherent.

**Scoring needs ground truth you establish before you ask.** Go through the README claim by
claim yourself, against the files, and write down which ones are wrong. Check the artifact
the reviewer will see rather than a copy of it: a stale zip or an unpushed working tree will
manufacture a defect that is not there, which is what happened the first time.

The two discrepancies from the first run are both fixed, so they cannot be reused as ground
truth. A later run needs its own.

## Results

No cold-session run yet.

One result of a different kind, from an external AI review on 17 September 2026: it verified
the argument and did not verify one claim the README made about its own template, and one of
the two defects it was then told it had missed turned out to have been fixed before the repo
was public. Written up in
[docs/result-2026-09-17-claim-review.md](docs/result-2026-09-17-claim-review.md), with the
review preserved beside it in [docs/](docs/).

<!-- Cold-session runs: one line per run. Date, repo, pass or fail, what it got wrong, and
     whether anything in NEXT.md was actually stale at the time. A run against a file written
     hours earlier proves much less than one a week later, when the registry or the deploy has
     moved underneath it. Say which it was. -->

## What the kit cannot carry

The kit is the method. It is not the knowledge, and on day one a new project has none of the
second thing.

**The traps list is empty, and it is earned rather than copied.** Every entry in a mature one
is a specific lie a specific tool told: a publish command that rewrites a file it was only
supposed to read, a build that leaves a stale artifact in place so a failed compile reads as
a pass, a page that redirects so a naive fetch compares against an empty body and reports a
false difference. None of those transfer. What transfers is the habit of writing one down the
same session it bites, while the detail is still exact.

**The Decided section is empty, so the first month will re-litigate.** A decision written as
its conclusion alone does not survive contact with a session that has a different opinion.
Write the reasoning and the alternative that was rejected, because that is what makes it a
decision rather than a preference.

**Nobody knows yet which external systems lie, and how.** Dashboards lag. Listings show the
published state and not the pending one. Registries report metadata that is not the artifact.
Caches serve yesterday. Which of those apply here is learned by being burned, and until then
"verified" is softer than it sounds.

**Nobody knows which checks are cheap.** In a mature project the cost of each verification is
known, so the expensive ones run at the right moments and the cheap ones run constantly. On
day one every check looks equally expensive, and the temptation is to skip all of them.

**The environment's own limits are unmapped.** Some checks will not run where the agent runs:
a browser that will not start, a remote that rejects the key, a sandbox that blocks a port.
Each has to be discovered, then written down as "not checkable here" rather than rediscovered
every session.

**And the part that is not a file at all:** a shared sense of what "checked" means. That came
from doing it together, being caught being wrong, and tightening the standard each time. The
kit can tell a new session to show a check failing before believing it. It cannot supply the
history that makes the instruction feel obvious rather than pedantic.

So the honest expectation for day one: the kit prevents the structural failures, a session
resuming blind, state living in a chat log, a list of unpushed commits that rots. It does not
prevent the first ten specific mistakes. It gives them somewhere to be written down.

## License

MIT-0, which is MIT with the attribution clause removed. Copy these files into your own
repo, change them, ship them, and carry no notice. The point is that nobody has to think
about it before pasting a `CLAUDE.md` into a project.

## What I am asking for

Three things, from anyone who has run agents against real repos long enough to have their own
list.

**Which standards are missing.** These ten came out of one project's failures, so the list has
the shape of that project. The failures you hit are the ones I have not.

**Which you would cut.** Some may be ceremony that survived because nobody tested whether
dropping them cost anything. Rule 10 is the one I would defend least: it is the only one that
says outright that nothing went wrong to produce it, and it is there because it suits how I
review. Rule 4 is the next weakest on that test, since what it carries is two occasions where
it caught something rather than a failure that produced it.

**Whether anyone has a better answer for what the kit admits it cannot carry**, particularly
the first two. If you have found a way to give a new project a useful traps list on day one,
or to make a decision record survive a session that disagrees with it, that is worth more
than the ten rules.

Issues and pull requests are fine. So is a comment saying the framing is wrong, if it says
what you do instead.
