# Claim-review result, 17 September 2026

The first recorded empirical result for this repository. An external AI review was asked to
evaluate the repo's concepts, structure and claims. It was then told what it had missed, and
one of the two things it was told turned out to be wrong.

**This is not a cold-session test result.** The cold-session test asks whether an agent can
reconstruct a project's state from its files. This asks a different question with different
ground truth: whether an agent reviewing a repository verifies the claims that repository
makes about itself. The cold-session test has still not been run.

The model and vendor are not named. Naming them turns a methodology note into a model
comparison, and nothing here depends on which reviewer it was.

The review is preserved in full at `review-2026-09-17-original.md`, and the exchange after
the correction at `review-2026-09-17-followup.md`. The failed version is kept rather than a
corrected one, so anyone can see what was read and what was concluded.

## What was reviewed

The repository as published on GitHub. `main` was `38b601f` from the moment the repo was
created, and `9b89bbb`, which added the license, was pushed at 14:23 UTC on 17 September.
The review saw `9b89bbb`.

The basis is the review's own statement that the repository "is currently only five
commits". `38b601f` is the fourth commit and `9b89bbb` the fifth. The next push, at 16:21
UTC, took `main` to nine commits and came after the review had been committed here at 15:08
UTC, so five commits matches only `9b89bbb`. Nothing else in the review tells the two states
apart: it does not mention the license. This rests on one assumption, that the reviewer
counted the commits correctly.

**The prompt given to the reviewer is not recorded.** Without it a reader cannot judge how
much of the review's shape was set by the question.

## What the review raised

Conceptual points, none of which required checking a claim against a file:

- The memory rule is the least portable part of the kit, since not every agent has
  persistent memory, and the underlying idea generalises to treating any external context as
  untrusted until reconciled with the repository.
- Rule 10 is about interaction policy rather than verification, and sits oddly beside rules
  that are all about truthfulness.
- Ten rules may be too many for a file that claims to be short, and they could be split into
  always-on rules and procedures invoked when applicable.
- The verification concepts could be formalised into an explicit state model. This was
  rejected: an explicit `verified: true` field produces the appearance of verification
  without producing the adversarial question that catches the problem, and the reviewer
  agreed on reflection that the questions matter more than the fields.
- The project could position itself as a protocol rather than three files. Also rejected, as
  a promise of specification, semantics and conformance that does not exist.

## The one real miss

**The README's description of `CLAUDE.md` did not match `CLAUDE.md`, and still did at the
time of review.**

The README said the file is short on purpose, that it says to read the state file first and
treat its facts as dated, that the standards live elsewhere, and that it also carries the
writing rules.

The file contains more than that, and one clause of the description is wrong. Five of the
ten standards are restated in it as bullets, with a sentence naming the other five, so the
standards do not live elsewhere. It also holds a writing section of sixteen rules and four
working paragraphs: how to work, confirm where you are before acting, do not guess, and do
not start queued work unprompted.

This is a violation of the repository's own rule 3, which reads: "Check claims against the
artifact, not the description of it." The README described its own template from memory of
what it was supposed to contain.

**Fixed** in the commit that adds this file.

## The false charge, which is the more useful half

The reviewer was told it had also missed that the README claimed every standard in the
template carried the failure that produced it, when only three of ten did.

**That defect was not in the repository under review.** It had been fixed in `38b601f`, and
the repository was created on GitHub one minute after that commit was made, so the wording
was never the tip of `main` and was never on the landing page. The README the reviewer could
have read says "Nine of the ten carry the failure that produced them, written out in the
template. The tenth says plainly that it has none."

**The charge came from checking a zip of the working tree that predated the fix**, then
reporting the result as a live defect in the published repository. The count was wrong too.
At that earlier state one standard named a failure that had happened, rule 2 and its binary
shipped through four checks that all resolved to a working copy, and one named two occasions
where the rule caught something before it was built, rule 4. The other eight named none.
"Three of ten" was generous by one or two depending on whether an example of the rule
working counts as the failure that produced it.

So the charge was the repository owner's, not a miss by the reviewer.

**What makes it worth recording rather than deleting:** it is a violation of rule 2, which
says never verify through a path that can resolve to your own development copy, committed
while documenting a violation of rule 3, in the record of a review about unchecked claims.
The artifact that was checked was not the artifact under review. That is the same shape as
the binary that passed four checks against a linked working copy, on a different scale and
with nothing at stake, and it happened to the person who wrote the rule, two days after
writing it.

## What this result establishes, and what it does not

It establishes that one external review of this repository verified the conceptual argument
and did not verify one factual claim the repository made about its own files.

It does not establish how often that happens, whether a reviewer following this kit would
have caught it, or whether another reviewer would have. One observation is one observation.

It says nothing about the cold-session test, which remains unrun.

## Ground truth for future runs

Both discrepancies are now closed. The standards wording was corrected in `38b601f` before
the repo was public, and the `CLAUDE.md` description is corrected in the commit that adds
this file.

A future claim-review run cannot be scored against these two. It needs its own ground truth,
established the same way: check every externally verifiable claim in the README against the
file or artifact it describes, before asking anyone else to.
