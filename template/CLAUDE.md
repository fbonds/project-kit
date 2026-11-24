# Working in this repo

<!-- Fill in PROJECT, and delete any line below that is not true here. Everything left
     should be something you would enforce, because a rule nobody enforces teaches the
     next reader that the rest are optional too. -->

**Read `NEXT.md` first, and say that you have.** It is the working state: what shipped, what
is in flight, what is queued. Then read `DECISIONS.md`, what was decided and ruled out, and
`TRAPS.md`, what has cost time here before. Read all three before proposing anything, then
report what is in flight and what is uncommitted before doing anything else. After the
conversation is compacted, read `NEXT.md` again: Claude Code re-injects this file after
compaction, and not `NEXT.md`.

**Treat its facts as dated, not current.** Every claim in it records what was true when it
was checked. Anything outside this repo moves without a commit here to show it. The block
at the top of `NEXT.md` has the commands that re-check the moving parts. Stored memories
load before any file is read and go stale the same way, so check those against the repo
too.

`HOWTOSAVESTATE.md` has the procedure for verifying state and saving it at the end of a
session, plus what each file here is for.

## Standards

How work is done here, and why. Each one carries its reason, or it reads as taste and gets
dropped under time pressure. In this template the reason is the failure that produced it,
except rule 4, which carries two occasions it caught something before it was built, and rule
10, which says plainly that no failure sits behind it.

The examples below come from the project this kit was built in. **Replace each with your own
the first time this project produces one**, since a local failure argues better than a
borrowed one. Do not delete an example and leave a bare rule behind.

**1. No check counts as verified until it has been shown failing on deliberately broken
input, and the report says what was broken.** A check that cannot fail is not evidence, and
it is indistinguishable from a passing one in the report. Three checks were once reported as
verification when none of them could fail, and a guard test written to catch a drifted
dependency tree was invalid because the build regenerated what had been stripped to break
it.

**2. Never verify through a path that can resolve to your own development copy.** The
failure is not that the check was wrong; it is that the check never looked at the thing
being shipped. A linked or globally installed copy, a symlinked directory, a dev server
still running, a mounted volume, a cached build, a tool that falls back to a local default:
each of these will answer as though it were the artifact. Name the path explicitly, resolve
it, and prove the resolved path is the one you meant, inside the location you meant. A
release once shipped a broken binary through four separate checks, every one of which
silently resolved to the working copy rather than to what users would download.

**3. Check claims against the artifact, not the description of it.** The published file, the
fetched page, the built package. Not a commit message, a changelog, a dashboard label, or
`NEXT.md`. A published page told readers that a shipped file had five entries. It had eight.
The page was correct when written and was falsified by a build change nobody re-read it
against.

**4. Proposal before code, for anything with a surface.** A command, a flag, an API, a
schema, a page, a public string. Show the surface and wait for approval before writing the
implementation. It is cheaper to reject a design than a branch, and it has already caught a
feature that should not have existed and a scope that would have overpromised, both before
anything was built.

**5. Stage explicitly.** Never `git commit -am`, `git add -A` or `git add .`. Run `git add`
with the paths, confirm with `git diff --cached --stat`, then commit. Check first whether the
tree already holds approved but uncommitted work from an earlier step. One commit swept an
unrelated file rewrite in under a message that described neither change, and it took a diff
of the wrong file to notice.

**6. Describe contents and order, not counts and pagination.** A count derived from another
file, or a reference to a page number, goes stale silently when something else changes. Three
sentences describing a document's pagination broke at once when a single table row was added
to a page ahead of them, and one of them sent a reviewer backwards past the thing it cited.

**7. Say what was not checked**, rather than leaving it out, and say where a fact came from.
An omission reads as a verified negative. A disclosure was read off a public listing page
rather than off the form that produces it, and because the source went unstated it produced a
full analysis of a conflict that did not exist.

**8. Never point at the conversation.** A cold session can read every file here and none of
the chat. "As discussed", "per the earlier decision", "recover it from the conversation" are
dead ends. A saved note once told a future session that four agreed items "were agreed but
not restated; recover them from the original list", and the original list was a chat log. The
four were nearly lost and had to be rebuilt from the README, the changelog and the git log.
Write it out where it belongs, or record in plain words that it is lost.

**9. Check stored memories against the repo.** They load before any file is read, so a stale
memory outranks a correct `NEXT.md`. Anything a memory asserts about a file, a branch, a flag
or a version is checkable; check it rather than assuming it still holds. Two were wrong
within one week: one described a branch rebase that had never been done, and the other a tool
setup that had been replaced months earlier.

**10. One item at a time: show the diff, wait for approval.** Commit only when asked, and
never push: the owner pushes. **No failure sits behind this one.** It is a working agreement
rather than a scar: it keeps a wrong direction visible while it is still cheap to change, and
batching removes that moment.

<!-- Add project-specific standards here as they are earned, with the reason. -->

**Report a check in this shape.** Each line holds the evidence in words. A yes or a tick in
place of it leaves the line unanswered. If the check was never shown failing, write that on
its line, and the result does not count as verified.

```
Result: what the output showed, pasted or quoted.
Shown failing: what was broken, and what the check then reported.
Path: the path used, resolved.
Artifact: the thing checked, and where it came from.
Not checked: each thing, named.
```

## Working rules

**How to work.** One item at a time: show the diff and wait for approval before applying
the next. Stage explicitly by path, confirm with `git diff --cached --stat`, and never
`git commit -am`. **Never push.** PROJECT_OWNER pushes, and PROJECT_OWNER deploys and
releases.

**Confirm where you are before acting.** Say which working directory or repo you are in,
and challenge it if it looks like the wrong one for the work being asked for. Two repos with
similar names, or a sibling checkout, are easy to act in by mistake and expensive to undo.

**Do not guess.** Check. If something cannot be checked from here, say that, rather than
reasoning your way to a plausible answer and presenting it as one. "I could not verify this"
is a usable answer; a confident wrong one costs the rest of the session's trust.

**Do not start queued work unprompted.** `NEXT.md` names what is waiting, and `DECISIONS.md`
what was deliberately rejected. Raise it rather than beginning it.

## Writing

Applies to user-facing prose and to how you write to PROJECT_OWNER. **Delete this section
if this project has no prose anyone reads**, and keep it if it has a README, a site, release
notes or a store listing. It is the last section in the file so that deleting it means
deleting from this heading to the end, and nothing else here depends on it.

These are the patterns that read as machine-written. A site rewrite turned on them: the
first item alone appeared dozens of times across a handful of pages.

- **No "not X, it's Y" reframes.** State what it is.
- **No rule-of-three cadence**, three parallel items or three adjectives on everything.
- **No trailing participial clauses** that tack a conclusion onto a fact: "making it easier
  to X", "ensuring Y stays consistent".
- **No "that said" or "with that said" pivots.** Use "but".
- **No "here's the thing" or "the thing is" lead-ins.**
- **No rhetorical questions as transitions.**
- **No bolded mini-header on every bullet** where prose works.
- **No "not only... but also".** Use "and".
- **No summary sentence** restating what was just read.
- **No unprompted "think of it like" analogies.**
- **No "X is where Y matters" constructions.**
- **No emoji or checkmark decoration** in headers or lists.
- **Prefer short declaratives** over clause-heavy sentences.
- **No em dashes**, anywhere: chat, files, commit messages, product copy.
- **Say what a thing does** rather than performing it.
- **No preamble** summarising what you are about to say, and no restating the request
  before answering it.
