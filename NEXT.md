# Where we are

**This is project-kit's own working state, filled in for this repository. It is not the
template.** To use the kit in another repo, copy the three files in `template/`.

> **Read this before acting on anything below.** Every fact in this file is dated and may
> be stale. It records what was true when it was checked, not what is true now. The owner
> pushes, and GitHub moves without a commit here to show it, so re-check first:
>
> ```sh
> git ls-remote --heads --tags origin                    # what GitHub actually has
> git fetch -q origin && git rev-list --left-right --count origin/main...main   # left = behind, right = unpushed
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

Updated 2026-09-17. Working state for project-kit. `README.md` is the public argument and
the only documentation. `template/` is the kit itself. `docs/` is the record of results,
indexed in `docs/README.md`. There is no design document and no roadmap; this file holds
what is queued.

## Standards

The ten are in `template/NEXT.md` and apply here as written. This repository's own failures
against them, where it has one:

**Rule 2, never verify through a path that can resolve to your own development copy.** A
charge that the published README claimed every standard carried its failure was made by
checking a zip of the working tree that predated the fix, and reported as a live defect in
the published repository. The README never published it. A similar claim was published in
the template, and is counted separately as a real miss. Recorded in
`docs/result-2026-09-17-claim-review.md`.

**Rule 3, check claims against the artifact.** Three times, all on GitHub from repo
creation, and all missed by the external review. The README's description of
`template/CLAUDE.md` did not match the file, until `5531e49`. The README said "Nine of the
ten carry the failure that produced them" while rule 4 in the template carried two saves
rather than a failure, which was wrong when written, not stale, until `5531e49`. And both
template files said every standard carries the failure that produced it, while rule 10 in
`template/NEXT.md` said none sits behind it, until `239226f`.

## Traps

Each of these has happened in this repository. The detail is there to recognise the next
one.

**The working tree is not what a reader sees.** A zip, a local checkout or an unpushed
commit can differ from the tip of `main` on GitHub, and a check against it reports a defect
that is not published, or misses one that is. Recognise it: evidence that came from a file
rather than from `git show origin/main:<path>` after a fetch, or from GitHub itself. Caused
the false charge in the first result.

**The README's description of the template does not match the template.** It has happened
twice, both introduced in the README rewrite in `38b601f`: "the standards live elsewhere"
about a `template/CLAUDE.md` that already restated five of them, and "Nine of the ten" when
rule 4 carried saves. It nearly happened a third time from the other direction in `eda6f3e`,
where moving the working rules above the Writing section reversed the order the README
describes, and was caught before commit. Recognise it: any diff touching `template/`, or the
README's "What the kit contains" section, gets the other read beside it before it is shown
for approval.

**Correcting a claim about the standards has created it somewhere else, five times.**
`38b601f` introduced two: the README's description of `template/CLAUDE.md`, and "Nine of the
ten carry the failure that produced them". `5531e49` fixed both and introduced a third in
the same commit, "points at `NEXT.md` for all ten with their failures attached". Both
template files had carried "each carries the failure that produced it" since creation.
`239226f` fixed the template files and two more README lines, and left the one `5531e49` had
introduced. This pass fixed that one, and replaced the result doc's summary of the gap,
which had overstated it in the same shape. Recognise it: after correcting any claim about
the ten standards, read every sentence in the README, the template and `docs/` that
describes them as a group, and check it against the members one by one. The pattern is not
that the claim is hard to fix. It is that fixing it in one place writes it somewhere else.

**A claim corrected in one file survives in another.** "Every standard carries the failure
that produced it" was corrected in the README and survived in `template/CLAUDE.md`,
`template/NEXT.md` and two more README lines, until `239226f`. Recognise it: after
correcting a wording, search the whole repository for the claim, not the sentence, since
the survivors are phrased differently ("each with the failure", "every rule came out of",
"came out of one project's failures").

**Universal claims about the rules or the incidents.** Two defects here were a claim about a
whole set with an exception in it. "Every standard carries the failure that produced it"
missed rule 10, which has none, and rule 4, which has saves. "None of those were caught by
the agent being careful. They were caught by asking a narrower question" covered all four of
the README's failures, and the chat-log note was never caught by any question. Recognise it:
any sentence quantifying over the ten rules or the four failures gets checked against each
member.

**A pointer to where something is listed, when the target does not list it.**
`docs/README.md`, in its entry for the follow-up exchange, says the four ways the recorded
write-up departs from the reviewer's draft are "all listed in the result file". They are not
in it. They are in the message of commit `e6dbdb9`. Recognise it: "listed in", "see",
"recorded in"; open the target and find the thing. Still unfixed.

**Framing around a verbatim record goes stale when the conclusion changes.** The header of
`docs/review-2026-09-17-original.md` said the review "missed two factual ones", written when
two was the count. The count then became one, then two, then three, and the header was not
re-read at any of those moves. The review text must not change, and the header around it is
easy to forget for that reason. Recognise it: a change to what a result concludes means
re-reading every header and index entry that states the conclusion, including the headers of
the preserved records.

**Removing text from a file in a public git repository does not remove it.** The preserved
review's header said a tracking parameter naming the vendor was stripped, which read as
anonymity while the diff in `e6dbdb9` still showed it. The header now says the history shows
the vendor. Recognise it: any claim that an edit hides, redacts or anonymises something
already committed.

**A section the template says to delete held rules that must not be deleted.** The working
rules, including never push, sat under the Writing heading that tells a project with no
prose to delete the section. Fixed in `eda6f3e`. Recognise it: any instruction to delete a
section gets tested by deleting it and searching for what was lost.

**Commit time is not push time.** The result doc gave `9b89bbb`'s commit time, 14:22 UTC, as
its push time, which the activity log records as 14:23:12 UTC. Fixed in `029310d`.

**A check that cannot stop what it is checking.** A script rewrote this file and asserted on
the text before writing, so a wrong assumption about the line wrapping would abort the
write. The assertion tripped, the write never happened, and the `git commit` after it ran
anyway, because the two were separated by a newline rather than chained. The commit went in
with the edit missing, and the reply that described the edit was wrong until the file was
read back. This is rule 1 in the tooling rather than in the product: the guard could not
fail in a way that stopped anything. Recognise it: any command chain where a verification
step and the action it guards are separated by `;` or a newline rather than `&&`, and any
edit whose success is reported from the writing step rather than by re-reading the file.

## Decided, do not redo

**No explicit state model or `verified: true` field.** Proposed by the external review and
rejected: a field produces the appearance of verification without the adversarial question
("have you shown that failing") that catches the problem. The reviewer agreed on reflection.
Recorded in `docs/result-2026-09-17-claim-review.md`.

**Not positioned as a protocol.** Also proposed by the review and rejected: "protocol"
promises a specification, semantics and conformance that do not exist.

**The review's model and vendor are not named in the prose**, because naming them turns a
methodology note into a model comparison. That is a scope, not anonymity: the stripped
tracking parameter that named the vendor is still in the diff of `e6dbdb9`, in a public
repository, and the files now say so. Rewriting the history to remove it was rejected: it
would change every commit ID from `e6dbdb9` onward, invalidate the IDs cited throughout
these files, need a force push, and still not reach clones, forks or caches.

**The failed review is preserved verbatim, not corrected.** Any edit is declared in its
header. The prompt that produced it was not kept, and the files say so rather than
reconstructing it.

**The README's four opening failures are stated as attested, not checkable.** They happened
in a private repository (`70aa935`).

**The template's exception sentences say "in this template".** A sentence naming rules 4
and 10 as exceptions goes stale in every copy once its examples are replaced, and that
sentence is not itself an example, so replacing examples does not fix it (`239226f`).

**The review saw `9b89bbb`**, on the basis of its own "five commits", assuming it counted
correctly (`029310d`).

**The review missed three real defects and was charged with one it did not miss.** The three
are the README's description of `template/CLAUDE.md`, the README's "Nine of the ten", and
the template's claim that every standard carries its failure. Separate findings count
separately even when they touch the same claim. The false charge stays false: it named the
README and gave a count of three, and both were wrong, and a similar claim elsewhere does
not make a wrong charge right. The count moved from two to one to two to three before this,
and `docs/result-2026-09-17-claim-review.md` says so.

**The external review is not a run of the claim-review test.** The test asks for ground
truth written down before anyone is asked. Here it was written afterwards and moved four
times, so calling it a run is the overclaim the rest of these files avoid. The README's
heading, its scoring paragraph and its Results section now all say so, and the question is
off the open list.

**The README tells the guard, and the template tells the test of the guard.** Two moments in
one attested incident: the guard could not fail, and separately a test of that guard ran
against a stale build and reported a pass. The README's "someone broke the tree on purpose"
clause was cut, because it belongs to the test rather than to the guard.

**How the first three failures were caught is left partly unsaid.** The release was caught
by asking whether the check had been shown failing, and the notices count by opening the
published file. No single question covers all three, so the README keeps "such as" and no
question is invented for the third.

**Root working files are named `CLAUDE.md` and `NEXT.md`**, the names the kit tells users to
use, so this repository uses the kit the way a copier would. Each opens with a visible
notice that it is not the template, in plain text rather than an HTML comment, which Claude
Code strips and GitHub hides. Neither contains the template's placeholder strings, so the
README's setup grep prints no lines for them if they are copied by mistake. It still prints
one for `HOWTOSAVESTATE.md`, because there is no root copy of that file and whoever copies
these two by mistake has to take it from `template/`. Renaming, and moving `CLAUDE.md` to
`.claude/CLAUDE.md`, were rejected: both mean the repository does not use its own kit as
written.

**No `claudeMdExcludes` setting for `template/CLAUDE.md`.** Claude Code loads a
subdirectory's `CLAUDE.md` when a session reads files there, so a session editing
`template/` gets both files. Excluding it was rejected: it mitigates something that has not
happened, and whether it took effect cannot be observed from inside a session. If a session
working on `template/` misbehaves because both loaded, that goes in Traps with the detail.

**No `HOWTOSAVESTATE.md` at the root, and the writing rules are a pointer.** Both would be
second copies of files in `template/`, and two copies of a fact drift. The root `CLAUDE.md`
points at `template/HOWTOSAVESTATE.md` and at the Writing section of `template/CLAUDE.md`.

## In flight

A pass fixing defects found by a session that read the repository cold on 2026-09-17, one
item at a time with approval:

1. Working rules moved out of the deletable Writing section of `template/CLAUDE.md`. Done,
   `eda6f3e`.
2. The "every standard carries its failure" claim, in the templates and the README, and the
   README's claim that all four opening failures were caught by a narrower question. Done,
   `239226f`.
3. Which state the review saw, and the push timestamp, in the result doc. Done, `029310d`.
4. These two root files and the README sentence about copying them by mistake. Done,
   `dd4b5a8`.
5. The count of real misses corrected to three, with one false charge, everywhere it is
   stated. Done, `76108c2`.
6. The vendor-stripping claim in `docs/review-2026-09-17-original.md`, narrowed to what is
   true and paired with a plain statement that the history shows the vendor. Done,
   `3a8f006`.
7. What two cold reads of the README and the result doc found, fixed in both files. Done,
   `8dcb360`.

Nothing is left in this pass. What the pass did not touch is in Open.

## Queued, unscheduled, and not to be started unprompted

**The cold-session test.** The README defines it. It has not been run. A session asked the
question on 2026-09-17 before this file existed, which does not count: the repository did
not use its own kit then. A run means a session that starts cold with this file in place,
and it proves more if this file is days old and something has moved underneath it.

**A second claim-review run.** It needs its own ground truth, written down before anyone is
asked, checked against GitHub rather than a local copy. The discrepancies found so far are
all known and cannot be reused.

## Committed, pushed, released: three separate questions

As of 2026-09-17 19:20 UTC, re-checked against the remote at that time.

**Uncommitted.** Nothing. The working tree is clean.

**Unpushed.** Answer it with `git rev-list --left-right --count origin/main...main` after a
fetch, or `git ls-remote --heads origin main` when the remote-tracking ref may be stale.
Snapshot, not to be trusted: at 19:20 UTC GitHub `main` and local `main` were both
`8dcb360`, and the commits carrying this sentence and the one before it are the only ones
ahead of that. The owner pushes, so this moves with no commit here to record it.

**Unreleased.** Nothing is released separately. Pushed to `main` is published. No tags, no
GitHub releases, no issues and no pull requests, each read at 19:20 UTC.

## Open, not blocking

**`docs/README.md` points at a list that is not there.** Its entry for the follow-up
exchange says the four departures from the reviewer's draft are listed in the result file.
They are only in the message of commit `e6dbdb9`: separating the real miss from the false
charge, quoting rule 3 correctly, using the count the artifact supports, and recording fix
status.

**The follow-up file's header miscounts its own messages.**
`docs/review-2026-09-17-followup.md` says "Two messages, verbatim", and its sections are
headed "Second message" and "Third message", with no first. Noticed while correcting the
count of misses. Not checked against the original exchange, which is not in this repository.

**Raised by the review, not decided:** whether the memory rule should generalise to any
external context, whether rule 10 belongs in a separate operating-policy section, and
whether the ten should split into always-on rules and procedures. The follow-up exchange
also mentions a vendor-neutral note on the instruction file's name, proposed by the owner.
The owner's own wording is not in this repository. The only version here is the reviewer's
paraphrase in `docs/review-2026-09-17-followup.md`. None of these is queued.
