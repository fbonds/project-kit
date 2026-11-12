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

Updated 2026-11-06. Working state for project-kit. `README.md` is the public argument and
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

**A check that cannot stop what it is checking.** A script rewrote this file and asserted on
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

## Decided, do not redo

**Entries in this section are not rewritten, from 2026-11-06.** To change a decision, get the
owner's approval, then add a new entry with its date, its reasoning and the entry it
replaces. The only edit to the old entry is one added line saying what replaced it and when.
Entries already here are not backfilled. The template carries the same rule (`f8ed21f`).

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

**The README's four failures, under "Where the rules came from", are stated as attested,
not checkable.** They happened in a private repository (`70aa935`).

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
truth written down before anyone is asked. Here it was written afterwards and moved three
times, so calling it a run is the overclaim the rest of these files avoid. The result doc
says so.

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

**The settings file is optional and lives only in `template/`.** It is the one part of the
kit that enforces anything without the agent's cooperation. A deny rule matches command
text, so it stops the usual form of a command and not every form, and the README says so.
There is no root copy, for the reason there is no root `HOWTOSAVESTATE.md` (`e1c68ed`).

**The kit stays written for Claude Code.** Shipping `AGENTS.md` as the main file, with
`CLAUDE.md` importing it, was considered and not done: it adds a file and changes the setup
grep and the check for copying the root files by mistake. The README says what to rename
instead (`973cf51`).

**The 2026-09-17 result doc still says the cold-session test is unrun**, as a dated record,
with a note pointing at the README's Results (`ba231a4`).

**The README no longer mentions the September review, and `docs/` carries all of it.**
`e473d0a` cut it to one paragraph, and `5e3415c` removed that.

**The README presents the kit as complete** (2026-10-31, owner's decision). The claim-review
test, never run, and "What I am asking for", which invited issues and pull requests, were
removed. The result and both reviews stay in `docs/` as the record.

**The README speaks in the owner's first person and states the private-repository caveat
once** (`e2a3eb4`). Its success claims are the owner's experience. Repeating the caveat in
every section made them read as doubted.
Replaced on 2026-11-06 by "The README's opening speaks to the reader as a pitch", below.

**`NEXT.md` is not split** (2026-11-06, owner's decision). Moving Standards and Decided into
their own files was rejected. A session has to read Decided before acting, so a split saves
no reading, Traps is the largest section here and would stay, and the attested runs all used
the current layout. Instead a finished item leaves In flight (`cd98ebe`).

**Credit lives in the README only** (2026-11-06, owner's decision). The template files are
copied under MIT-0 with no notice required, and nothing is quoted from any source. Each
source is credited only for what it says: Nygard for marking a reversed decision superseded,
Fowler for the rule that an accepted record is never changed, and Cline for the split that
was looked at and not taken.

**The attested cold-session runs get no run lines** (2026-11-06, owner's decision). The owner
has no dates, repositories or details for them and none will be supplied. The owner's notes
also said the test ran twice in two repositories and that claim-review was attempted. A
search of this repository's history that day, by commit message and by phrase in the diffs,
found no record of either. Claim-review stays out of the README. When the first test harness
results exist, one commit will:

- move the attested paragraph from the README's Results into a dated note in `docs/`, with a
  line in `docs/README.md`,
- state in that note that the README says runs began 16 September and
  `docs/result-2026-09-17-claim-review.md`, at line 26 on 2026-11-06, says none had happened
  as of 17 September, without picking one,
- put the harness results in Results,
- rewrite the sentence in the README's How to use it that points at the attested runs, "The
  cold-session runs under Results passed with both habits in place."

**The README's opening speaks to the reader as a pitch** (2026-11-06, owner's decision). It
replaces "The README speaks in the owner's first person and states the private-repository
caveat once". The opening should make a newcomer want to try the kit and find out for
themselves how it works. The reference half, from "Where the rules came from" on, keeps the
owner's first person and the single private-repository caveat. The opening it replaced,
including the Before and after section, is at `b9b192e:README.md`.

**Never push, in every file** (2026-11-12, owner's decision). Rule 10 in `template/NEXT.md`
said "Commit and push only when asked", which allowed a push when asked, against "Never
push" in `template/CLAUDE.md`, `template/HOWTOSAVESTATE.md` and the README. Rule 10 now says
the owner pushes.

## In flight

Nothing. The 2026-11-06 pitch pass rewrote the README's opening and replaced the GitHub
description, and its commits are `2040b50`, `882a749` and `957603b`. The owner waived one
item at a time for its last two items, which is why they share a commit. The description is
under Outside the repository.

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

As of 2026-11-06 22:56 UTC, re-checked against the remote at that time.

**Uncommitted.** Nothing apart from this file's edit, which is in the commit carrying it.

**Unpushed.** Answer it with `git rev-list --left-right --count origin/main...main` after a
fetch, or `git ls-remote --heads origin main` when the remote-tracking ref may be stale.
Snapshot, not to be trusted: at that time GitHub `main` was `b9b192e`, and local `main` had
`2040b50`, `882a749` and `957603b` ahead of it, plus the commit carrying this sentence. The
owner pushes, so this moves with no commit here to record it. A commit ID written into this
file is the ID at the time of writing, and a rebase replaces it.

**Unreleased.** Nothing is released separately. Pushed to `main` is published, so what is
unpushed above is what is unpublished. Last published: `b9b192e`, pushed at 20:16:23 UTC on
2026-11-06, read from the activity log and `git ls-remote`. No tags, no GitHub releases, no
issues and no pull requests, each read at the time above.

**Outside the repository.** The GitHub description and topics change with no commit here. Set
on the owner's instruction and read back from the API at 22:55:19 UTC on 2026-11-06, the
description is "Three Markdown files for Claude Code. Start each session with one sentence
and the agent reports where your project stands. Nothing counts as verified until it has
shown the check can fail." The topics, unchanged and read at the same time, are
`ai-assisted-coding`, `claude-code`, `claude-md` and `developer-workflow`.

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
