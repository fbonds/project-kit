# Project kit

Three files to copy into a new repo on day one, so a session that starts cold can resume
without asking anything it could determine itself.

It came out of the Bugpacker repos in September 2026, where the method was built by being
wrong in public: claims that turned out to describe behavior that had never shipped, checks
that could not fail, a state file that pointed at a conversation nobody could read any
more. What generalised is here. What was specific to that project is not, and the gap
between those two things is the last section of this file.

## Use

```sh
cp path/to/project-kit/template/{CLAUDE.md,HOWTOSAVESTATE.md,NEXT.md} .
```

Then, in order:

1. **Fill in `PROJECT` and `PROJECT_OWNER`** in `CLAUDE.md` and `NEXT.md`.
2. **Delete any rule you will not enforce.** A rule nobody enforces teaches the next reader
   that the rest are optional.
3. **Add the project's own check** to the block at the top of `NEXT.md`: the one command
   that reads what this project publishes or deploys. Until that line exists, the staleness
   warning has nothing behind it.
4. **Commit all three.** `CLAUDE.md` is read on startup by Claude Code without being asked,
   which is why the method lives there rather than in a file someone has to be pointed at.

## What each file is

**`CLAUDE.md`** is the only genuinely unavoidable slot: it loads at the start of every
session. Keep it short enough to be read every time, and keep it pointing at the other two
rather than duplicating them.

**`HOWTOSAVESTATE.md`** is the end-of-session procedure: check the external world, write it
into `NEXT.md`, check stored memories against the repo, then commit and report what could
not be verified. It also holds the index of what every file in the repo is for, which is
the part that stops a new document from becoming invisible a week after it is written.

**`NEXT.md`** is the working state, and the only file that answers "where were we". The
template carries the headings and the staleness block, with no content: `Standards`,
`Traps`, `Decided, do not redo`, `In flight`, `Queued`, the three-question state section,
and `Open, not blocking`.

## Where the writing rules live

They are in `template/CLAUDE.md`, under "Writing", and not in `NEXT.md`'s Standards.

The distinction is what each file is for. Standards are verification: every one can be
checked, and each carries the failure that produced it. A writing preference cannot fail a
test, and mixing the two weakens the standards, because a reader who disagrees with one
line starts treating the rest as taste.

`CLAUDE.md` is instructions to whoever is working, which is exactly what a writing rule is.
It also travels with the repo, so it applies to a session on another machine, to a
collaborator, and to any agent reading the repo rather than a personal configuration file.
A global instruction file covers only the sessions belonging to the person who wrote it.

Keep both copies if you have a global one. They will drift eventually; when they do, the
repo copy wins for work in that repo, because it is the one a stranger can see.

## The test, which has not been run yet

Nothing here has been proven to work on a session that did not help write it. The test is
cheap and it only happens if it is written down, so:

**The next time a session starts cold in a repo using this kit, the owner asks what it
concludes about the state before telling it anything.** Nothing else in the first message:
no context, no correction, no hint about what is in flight.

It passes if the session names, without being told:

- what the project is and what shipped or published last,
- what is in flight and what is queued but deliberately not started,
- at least one decision that was made and should not be reopened,
- **which of its statements it read and which it verified**, kept apart rather than
  presented as one kind of fact,
- **which specific facts it would re-check before acting**, named individually, not the
  general observation that the file is dated. Better still, it runs those checks first.

It fails if the session asks a question the files answer, restates the last commit message
as though it were the state, acts on a dated fact without re-checking it, or **presents a
dated fact as current without saying when it was checked**.

That last one is the criterion that matters. Every expensive failure in the project this
came from was a stale claim being trusted, not a missing one. A session can recite the
state file perfectly, be correct as of the date on every line, and still be wrong about the
world right now. Reciting is not the skill being tested.

**Record the result here**, pass or fail, with the date and what was missing. A fail is more
useful than a pass: it names the thing the template does not prompt for, which is the only
way this improves. Nobody remembers to run a test that lives in a conversation.

### Results

<!-- One line per run: date, repo, pass or fail, what it got wrong, and whether anything in
     NEXT.md was actually stale at the time. A run against a file written hours earlier
     proves much less than one a week later, when the store, the registry or the deploy has
     moved underneath it. Say which it was. Empty until the first run. -->

## What the kit cannot carry

The kit is the method. It is not the knowledge, and on day one a new project has none of
the second thing.

**The traps list is empty, and it is earned rather than copied.** Every entry in a mature
one is a specific lie a specific tool told: a publish command that rewrites a file it was
only supposed to read, a build that leaves a stale artifact in place so a failed compile
reads as a pass, a page that redirects so a naive fetch compares against an empty body and
reports a false difference. None of those transfer. What transfers is the habit of writing
one down the same session it bites, while the detail is still exact.

**The `Decided` section is empty, so the first month will re-litigate.** A decision written
as its conclusion alone does not survive contact with a session that has a different
opinion. Write the reasoning and the alternative that was rejected, because that is what
makes it a decision rather than a preference.

**Nobody knows yet which external systems lie, and how.** Dashboards lag. Listings show
the published state and not the pending one. Registries report metadata that is not the
artifact. Caches serve yesterday. Which of those apply here is learned by being burned, and
until then "verified" is softer than it sounds.

**Nobody knows which checks are cheap.** In a mature project the cost of each verification
is known, so the expensive ones are run at the right moments and the cheap ones constantly.
On day one every check looks equally expensive, and the temptation is to skip all of them.

**The environment's own limits are unmapped.** Some checks will not run where the agent
runs: a browser that will not start, a remote that rejects the key, a sandbox that blocks a
port. Each of those has to be discovered, and then written down as "not checkable here"
rather than rediscovered every session.

**And the part that is not a file at all:** a shared sense of what "checked" means. That
came from doing it together, being caught being wrong, and tightening the standard each
time. The kit can tell a new session to show a check failing before believing it. It cannot
supply the history that makes that instruction feel obvious rather than pedantic.

**So the honest expectation for day one:** the kit prevents the structural failures, a
session resuming blind, state living in a chat log, an unpushed list that rots. It does not
prevent the first ten specific mistakes. It gives them somewhere to be written down.
