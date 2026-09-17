# Claim-review result, 17 September 2026

The first recorded empirical result for this repository. An external AI review was asked to
evaluate the repo's concepts, structure and claims. It was then told what it had missed, and
one of the two things it was told turned out to be wrong. Later, checking the version it
actually saw found two more defects it had missed, which nobody had told it about.

It missed three factual defects. It was charged with one it did not miss. How that count was
reached, and how often it changed on the way, is in "The count moved three times" below.

**This is not a cold-session test result.** The cold-session test asks whether an agent can
reconstruct a project's state from its files. This asks a different question with different
ground truth: whether an agent reviewing a repository verifies the claims that repository
makes about itself. The cold-session test has still not been run.

The model and vendor are not named in these files, because naming them turns a methodology
note into a model comparison, and nothing here depends on which reviewer it was. The git
history does name the vendor: `review-2026-09-17-original.md` explains where and why.

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

## The three real misses

Each was in `9b89bbb`, the version the review saw, and the review raised none of them. Each
is a violation of the repository's own rule 3, which reads: "Check claims against the
artifact, not the description of it."

### 1. The README's description of `CLAUDE.md` did not match `CLAUDE.md`

The README said the file is short on purpose, that it says to read the state file first and
treat its facts as dated, that the standards live elsewhere, and that it also carries the
writing rules.

The file contained more than that, and one clause of the description was wrong. Five of the
ten standards were restated in it as bullets, with a sentence naming the other five, so the
standards did not live elsewhere. It also held a writing section of sixteen rules and four
working paragraphs: how to work, confirm where you are before acting, do not guess, and do
not start queued work unprompted.

The description was introduced in `38b601f`. **Fixed** in `5531e49`. An earlier version of
this file said it was fixed in the commit that added this file, `e6dbdb9`, which did not
touch the README.

### 2. "Nine of the ten carry the failure that produced them"

The README's section on the standards said this, followed by "The tenth says plainly that it
has none." In the template, eight standards carried a failure. Rule 4 carried two occasions
where it caught something before it was built, which is not a failure, and rule 10 said no
failure sat behind it.

The count was wrong when it was written, in `38b601f`, not made stale by a later change.
**Fixed** in `5531e49`, which says "Eight".

An earlier version of this file quoted "Nine of the ten" as the corrected wording. It had
corrected a worse sentence without being right itself.

### 3. The template claimed every standard carries the failure that produced it

`template/NEXT.md` opened its Standards section with "Each one carries the failure that
produced it", and in the same file rule 10 said "No failure sits behind this one."
`template/CLAUDE.md` said `NEXT.md` has all ten "each with the failure that produced it".
Both sentences were on GitHub from the repository's creation. **Fixed** in `239226f`.

This counts separately from the second miss. It is a different sentence, in different files,
and the two were fixed separately: the README said "Eight" in `5531e49` while both template
files went on saying every one until `239226f`.

## The false charge

The reviewer was told it had also missed that the README claimed every standard in the
template carried the failure that produced it, when only three of ten did.

**The README never published that claim.** The README wording had been changed in
`38b601f`, and the repository was created on GitHub one minute after that commit was made,
so the claim was never the tip of `main` and never on the landing page. What the README said
instead was "Nine of the ten", which was wrong in a different way and is the second miss.

**The charge came from checking a zip of the working tree that predated `38b601f`**, then
reporting the result as a live defect in the published repository. The count was wrong too.
At that earlier state one standard named a failure that had happened, rule 2 and its binary
shipped through four checks that all resolved to a working copy, and one named two occasions
where the rule caught something before it was built, rule 4. The other eight named none.
"Three of ten" was generous by one or two depending on whether an example of the rule
working counts as the failure that produced it.

**A similar claim was public, in the template.** That is the third miss, and it does not make
the charge right. The charge named the README and gave a count of three, and both were wrong.

So the charge was the repository owner's, not a miss by the reviewer.

**What makes it worth recording rather than deleting:** it is a violation of rule 2, which
says never verify through a path that can resolve to your own development copy, committed
while documenting a violation of rule 3, in the record of a review about unchecked claims.
The artifact that was checked was not the artifact under review. That is the same shape as
the binary that passed four checks against a linked working copy, on a different scale and
with nothing at stake, and it happened to the person who wrote the rule, two days after
writing it.

## The count moved three times

The number of defects the review really missed has been stated four times, each time with
confidence, and each change came from opening an artifact the previous number had not been
checked against.

1. **Two.** Told to the reviewer, from a zip of the working tree that predated `38b601f`. The
   reviewer accepted both, in `review-2026-09-17-followup.md`.
2. **One.** In the first version of this file, `e6dbdb9`, after the git history showed the
   second charge had never been published.
3. **Two.** Decided by the owner later the same day, after a session checked the published
   README's "Nine of the ten" against rule 4 in the template. It was recorded as an open
   question in `NEXT.md` in `dd4b5a8`, and the decision itself was never committed.
4. **Three.** After the two template files were checked as they stood at `9b89bbb`.

Every one of those numbers was stated as the answer. A reader would not believe that of a
file unless the file said so itself. It is a stronger argument for the claim-review test
than any single finding here: the test requires ground truth written down before anyone is
asked, and this result never had it. The count has been corrected three times after the
fact, and nothing here guarantees three is final.

## Three readers missed the third miss

The review did not raise it.

The first version of this file said the defect "was not in the repository under review",
having checked the README and not the template.

A session that read the repository cold on 17 September, before the template was fixed, did
find both template sentences and listed them as defects to fix. It did not check whether
they had been public when the review happened, so it treated them as current defects rather
than as something the review had missed. When the same session later argued that the review
had missed a second defect, it cited only the README's "Nine of the ten".

That is recorded as a fact about the defect rather than about any one reader. The one reader
who did catch the claim, the owner checking the zip, caught it in the README. The
`template/CLAUDE.md` committed at every state before `38b601f` carried the same claim, "each
with the failure that produced it", and the charge did not mention it.

## What this result establishes, and what it does not

It establishes that one external review of this repository verified the conceptual argument
and did not verify three factual claims the repository made about its own files.

It does not establish how often that happens, whether a reviewer following this kit would
have caught them, or whether another reviewer would have. One observation is one observation.

It says nothing about the cold-session test, which remains unrun.

## Ground truth for future runs

All three misses are fixed: the `CLAUDE.md` description and the count of standards in
`5531e49`, the template's claim about every standard in `239226f`. The wording behind the
false charge was changed in `38b601f`, before the repository was public.

A future claim-review run cannot be scored against any of these. It needs its own ground
truth, established the same way: check every externally verifiable claim in the README
against the file or artifact it describes, and write the result down before asking anyone
else to. The history of this result is the reason for the second half of that sentence.
