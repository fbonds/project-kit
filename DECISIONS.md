# Decisions

**This is project-kit's own record of decisions, filled in for this repository. It is not
the template.** It was moved here from `NEXT.md` on 2026-11-23, as the last entry below
records, and the entries were moved unchanged. In an entry written before 2026-11-23, "this
file" means `NEXT.md`.

## Decided, do not redo

**Superseded entries leave this file, from 2026-11-23** (owner's decision). An entry in
force is not rewritten. To change a decision, get the owner's approval, then add a new entry
with its date, its reasoning and what it replaces, and delete the entry it replaces in the
same commit. The git history keeps the old text. This replaces the rule from 2026-11-06 that
entries were never rewritten and a replaced one stayed with a line saying what replaced it.
This file outgrew that rule: on 2026-11-23 it measured 4.8k tokens, near the 5,000 that
Claude Code brings back in full after compaction. That rule and the three entries it had
kept as replaced were removed on 2026-11-23, and the file as it stood before is
`git show 6d50128:DECISIONS.md`. An entry still here that names a removed one is left as
written. `template/NEXT.md` carries the old rule until the template is changed.

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

**The GitHub Pages site is `README.md` alone** (2026-11-12, owner's decision). It is
published from the root with every other file excluded in `_config.yml`, so there is no
second copy to drift. The style files are copied from `fbonds/vibe-coding-howto`. A copy in
`/docs` was rejected, because `/docs` is the record.

**The README's first line links the repository with an absolute URL** (2026-11-12, owner's
decision, `7d77342`). The site has no other way to reach the files. On GitHub the link points
at the page the reader is on, which is redundant there and left in, because the site has no
text of its own. A relative link was rejected: when the page is framed, the script in
`_includes/head-custom.html` only sends links to another host to a new tab, so a relative
link would open the repository inside the frame.

**A five-item proposal from a benchmark article was not taken** (2026-11-18, owner's
decision). On 2026-11-18 the owner pasted a proposal prompted by a Surge AI benchmark of
coding-agent harnesses: amend rule 4 to cover who sees a change and when, make rule 1
re-run the original reproduction for a fix, add guidance on thinking effort, write a
four-arm evaluation plan in `docs/`, and queue a word budget for a filled-in `NEXT.md`. A
session checked it against this file and found four conflicts: naming the source in the
template reverses "Credit lives in the README only", a borrowed failure on rule 4 breaks the
README's "Eight of the ten", a change to rule 1 runs into the open question on its scoping,
and an evaluation plan here would be a second copy of the harness design. The owner then
said not to do any of it and to forget the article. Nothing was written.

**project-kit is the owner's personal methodology** (2026-11-21, owner's decision). It
replaces the entry above. The kit is the method the owner uses, offered to people who work
the same way. A full overhaul goes on a `version2` branch and draws on nine published
methods, read again from their live pages: Anthropic's Claude Code documentation, Cline
Memory Bank, GitHub Spec Kit, Kiro, AGENTS.md, BMAD, Agent OS, Harper Reed's workflow and
Simon Willison's "Designing agentic loops". Copies saved on 2026-11-18, outside this
repository, are the fallback. Version 2 also covers seven gaps found in the kit on
2026-11-18, where they apply. Two of them were written for a reader who does not build. Of
those, the gap that the Traps questions ask only about publishing still applies. The gap that
approving a diff is a formality does not, because the owner reads diffs. The overhaul may
change the rule that entries here are not rewritten, so that a superseded entry can leave
this file for the git history.

**`NEXT.md` is split into state, decisions and traps** (2026-11-23, owner's decision). It
replaces "`NEXT.md` is not split". After compaction Claude Code re-reads up to five recent
files and brings back any file over 5,000 tokens as a path only, and this file measured about
13,000 tokens on 2026-11-23, as gap 6 records. `NEXT.md` keeps the re-check block and the
current state: In flight, Queued, the three questions and Open. Decided moves to
`DECISIONS.md` and Traps, with Standards, to `TRAPS.md`, both at the root. `NEXT.md` names
both, and a session reads both at the start, so the old entry's reason, that a session must
read Decided before acting, still holds. Each of the three files stays under 5,000 tokens.
`CLAUDE.md` tells a session to re-read `NEXT.md` after compaction, because `CLAUDE.md` is
re-injected after compaction and `NEXT.md` is not. Whether that instruction is followed is
untested. Keeping one file and pruning it was rejected, because Decided and Traps alone are
about 3,860 words. A SessionStart hook printing part of the file after compaction was
rejected as the main fix, because it is untested and does nothing for a file too long to
read well. The template takes the same shape in a later item.
