# Traps

**This is project-kit's own record of its traps and its failures against the standards,
filled in for this repository. It is not the template.** It was moved here from `NEXT.md` on
2026-11-23, as `DECISIONS.md` records. One change was made in the move: in "A check that
cannot stop what it is checking", "this file" now reads `NEXT.md`.

## Standards

The ten are in `template/CLAUDE.md` and apply here as written. This repository's own failures
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
three times. Two were introduced in the README rewrite in `38b601f`: "the standards live
elsewhere" about a `template/CLAUDE.md` that already restated five of them, and "Nine of the
ten" when rule 4 carried saves. The third was introduced in `8dcb360` and fixed in
`ecd858d`: the README said two fill-ins in `HOWTOSAVESTATE.md` carry no placeholder string,
when one of the two is the numbered line naming the project's own files, which is the only
line the setup grep prints for that file. It nearly happened a fourth time from the other
direction in `eda6f3e`, where moving the working rules above the Writing section reversed
the order the README describes, and was caught before commit. Recognise it: any diff
touching `template/`, or the README's "What the kit contains" section, gets the other read
beside it before it is shown for approval. The third was in neither. It is in "How to use
it", and it was found by running the command that section gives rather than by reading the
sentence, so the rule now covers every README sentence that describes a template file, and
a command the README gives is run rather than read.

`8dcb360` was itself a pass correcting other claims, which is the shape the next entry
records for claims about the standards. Its message states the same wrong count as one of
its fixes: "The grep was called the fill-in list when two fill-ins carry no placeholder." A
reader who follows that ID will find it. It cannot be corrected, because a commit message
changes only by rewriting history, which is rejected here for the reason in Decided. The
same already applies to the count in `38b601f`'s message.

**Correcting a claim about the standards has created it somewhere else, five times.**
`38b601f` introduced two: the README's description of `template/CLAUDE.md`, and "Nine of the
ten carry the failure that produced them". `5531e49` fixed both and introduced a third in
the same commit, "points at `NEXT.md` for all ten with their failures attached". Both
template files had carried "each carries the failure that produced it" since creation.
`239226f` fixed the template files and two more README lines, and left the one `5531e49` had
introduced. `8dcb360` fixed that one, and replaced the result doc's summary of the gap,
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
write-up departs from the reviewer's draft are "all listed in the result file". They were
not in it. They were in the message of commit `e6dbdb9`, and the result file now lists them,
so the pointer is true. Recognise it: "listed in", "see", "recorded in"; open the target and
find the thing.

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

**A check that cannot stop what it is checking.** A script rewrote `NEXT.md` and asserted on
the text before writing, so a wrong assumption about the line wrapping would abort the
write. The assertion tripped, the write never happened, and the `git commit` after it ran
anyway, because the two were separated by a newline rather than chained. The commit went in
with the edit missing, and the reply that described the edit was wrong until the file was
read back. This is rule 1 in the tooling rather than in the product: the guard could not
fail in a way that stopped anything. Recognise it: any command chain where a verification
step and the action it guards are separated by `;` or a newline rather than `&&`, and any
edit whose success is reported from the writing step rather than by re-reading the file.

**An edit inside a wrapped paragraph leaves the wrapping wrong.** `7b83542` replaced the
first lines of a Results paragraph and left one line far past the file's width, so the
committed file did not match the approved diff, though the words did. Fixed in `e473d0a`.
Recognise it: after editing inside a wrapped paragraph, run
`awk '!/^\|/ && !/^\[[^]]*\]: / && length>93' README.md` before staging. It skips table rows
and link definitions, which cannot wrap, and nothing else, because a prose line can start
with a link.

**A session here cannot start a second Claude session to test with.** On 2026-10-30 the
auto-mode classifier refused `claude -p --permission-mode bypassPermissions`, run from a
session here, as creating an unsafe agent. The owner ran the same command with `!` instead.
Recognise it: any test that needs a second Claude session goes to the owner.

**Loading `CLAUDE.md` does not mean it is followed.** Claude Code put this repository's
`CLAUDE.md` into the 2026-10-30 session's context, and the session neither said so nor read
`NEXT.md` first. It read `NEXT.md` later, as part of an evaluation the owner asked for.
Recognise it: a session whose first reply does not say it has read `NEXT.md` and what is in
flight. The owner's opener, "Read CLAUDE.md and comply", is the fix (`1b902ff`).

**A source credited for more than it says.** On 2026-11-06 the brief for the README's Prior
art said Cline's page teaches keeping the active file to current state rather than a log, and
that Nygard's post says records are never edited. Cline's page does not say that, and lists
recent changes in that file. Nygard's post says to keep a reversed decision and mark it
superseded. The never-edit rule was on Fowler's page. Recognise it: a lesson attributed to a
source before the source has been opened.

**A brief can be staler than the repository.** The same brief asked for edits to README text
that had gone: "has not been run yet" was removed in `967ac7b` and "What I am asking for" in
`5e3415c`, by the owner's own decision. Recognise it: any instruction that names existing
text. Search for the text before planning the edit.

**A pitch claims what the reference half qualifies.** On 2026-11-06 ten claims in the brief's
pitch text did not survive being read against the README and the template. "The agent can't
tell you" and "makes both of those rules mechanical" were absolutes the kit does not enforce,
and the README itself records `git -C . push` getting through. "Every project has" was a
universal the template's Traps questions allow an answer of "none" to. "Two sentences" named
one, and the one missing, save state, is a condition of the attested runs. All ten were
reworded or cut before commit. Recognise it: any absolute in the opening or the GitHub
description, such as "can't", "never", "every" or "first day". Read it against "What the kit
contains" and "What the kit cannot carry".

**A result recorded before the check ran.** On 2026-11-12 the owner asked for the framed-link
test of the Pages site to be marked tested and passed by another session, in the same message
that said that session would run it. It was not written. The owner then reported it had run
and passed, and the record says it was reported and not seen here. Recognise it: "mark it
passed" or "record it as done" about something described in the future tense.

**A claim called wrong before it was measured against the version it described.** On
2026-11-21 a draft of gap 6 said the 2026-11-18 evaluation's count of 4,758 words for this
file was wrong, because `wc -w` on `3d56ac0:NEXT.md` gave 5,341. `23edcce:NEXT.md`, the
version before that day's save, gives exactly 4,758. It was caught before commit. Recognise
it: a number from an earlier reading checked against a later commit than the one it was
taken from.

**A draft written into the repository before it was approved.** On 2026-11-23 the proposed
`docs/` record was written into `docs/` while it was being shown for approval. It was moved
back to the scratchpad when noticed. Recognise it: a draft whose path is inside the
repository. Draft in the scratchpad and copy on approval.

**A check's warning explained away.** In `62dc27d` a 94-character line went in because the
line-length check flagged it and the flag was put down to the diff's `+` prefix. Fixed in
`9d524e0`. Recognise it: any reason given for ignoring what a check printed. Read the number.

**A limit written in the same commit as an estimate of meeting it.** `9d524e0` told
`CLAUDE.md` that each state file stays under 5,000 tokens, on an estimate of about 4,800 for
`NEXT.md`. `/context` measured 5.2k. Recognise it: a size rule whose only evidence is
arithmetic. Measure before stating it.

**Claude Code did not load a `CLAUDE.md` from its own scratchpad folder.** On 2026-11-23 a
copy under `/private/tmp/claude-501` did not load and `/context` listed only the global file.
The same copy under the home directory loaded. Recognise it: a `/context` measurement that
lists only `~/.claude/CLAUDE.md`.

**A root file naming a template placeholder.** On 2026-11-24 a draft Decided entry named the
new test-command placeholder, which would have made the setup grep print a line for
`DECISIONS.md` and broken the check for root files copied by mistake. The grep caught it
before commit. Recognise it: any root file that describes a template fill-in by its name.
Run the setup grep on the four root files before staging.
