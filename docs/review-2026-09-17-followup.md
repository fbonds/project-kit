# External AI review of project-kit, follow-up exchange, 17 September 2026

The same reviewer, after being told what it missed. Two messages, verbatim.
The second contains a write-up it drafted for recording this result.

Companion to review-2026-09-17-original.md.

## What it was told it missed

Two factual claims in the README that did not survive checking against the
files:

1. The README's description of CLAUDE.md did not match CLAUDE.md. The file
   also carried five standards as bullets and three working paragraphs the
   description did not mention.
2. The README stated that every standard in the template carried the failure
   that produced it. Three of ten did.

Both are failures of the repository's own rule 3: check claims against the
artifact, not the description of it.

## Second message, verbatim

That's a very useful correction, and I think your distinction between **conceptual review** and **artifact verification** is the important takeaway.

I also think your response changes how I'd characterize the repo after a second look.

The strongest thing in `project-kit` may actually be that it **doesn't try to turn epistemic discipline into a data model**. My state-machine suggestion was me reaching for something that looks rigorous because it is explicit. But your objection is stronger: the explicitness itself can become a failure mode. A checkbox that says `verified: true` can create the appearance of verification without producing the question that uncovered the problem in the first place.

Your examples make the distinction very clear:

> "Have you shown that failing?"

and

> "Where did that number come from?"

Those are **adversarial questions**, not fields.

That's probably a deeper insight than the state-machine idea I suggested.

### The thing I missed is particularly interesting

You gave me two concrete failures:

1. The README's description of `CLAUDE.md` doesn't match `CLAUDE.md`.
2. The README says every standard has a failure behind it, while only three of ten did when checked.

Both are violations of the kit's own standard:

> Don't claim what you haven't checked.

And I missed both while evaluating a project whose central thesis is precisely that claims need to be checked against artifacts.

That's a much better test of my review than whether I correctly understood the philosophy.

It suggests at least two distinct review modes:

**Conceptual review**

> Does this idea make sense?
> Are there contradictions?
> Is the methodology coherent?
> What are its conceptual weaknesses?

versus

**Artifact review**

> Does the README accurately describe the files?
> Does every claim in the README survive inspection?
> Does the template actually contain what the README says it contains?
> Do the examples correspond to actual repository history?

I did the first and inadequately did the second.

And, frankly, **that is exactly the sort of failure your project is trying to expose.**

### I would therefore modify my earlier assessment

I wouldn't call the project's biggest unresolved question merely "does the cold test work?"

I'd put a more fundamental question ahead of it:

> **Can an agent applying `project-kit` reliably catch discrepancies that an otherwise competent agent reviewing `project-kit` itself might miss?**

That's a much more interesting experiment.

Because the project isn't really trying to make agents *know more*. It's trying to make them **behave differently when they don't know**.

Your response demonstrates the distinction nicely:

I understood the repository's *argument*.

I didn't adequately verify the repository's *claims*.

Those are different capabilities.

### And I agree with your positioning correction

"Protocol" was too grand.

Your modesty is part of the project's credibility. Calling it a protocol implicitly promises:

* a specification
* defined semantics
* interoperability
* conformance
* probably tooling

when the actual artifact is currently:

**a small set of instructions and working-state conventions derived from specific failures.**

I'd retain that.

The vendor-neutral change you propose is also better than abstracting the whole thing upward. Something like:

> The startup instruction file is named according to the agent being used; the filename is not important, but its contents are.

That preserves the practical nature of the kit without pretending there's an agent-neutral standard underneath it.

### One thing I'd now be inclined to add

Not another rule.

A **review question**.

Something along the lines of:

> **What does this document claim that you have not actually checked?**

Not necessarily as a tenth/eleventh standard. It could simply become part of the project's own maintenance practice.

Because your two catches are especially nasty precisely because they're **meta-level failures**. The README makes claims about the reliability of the kit, and those claims themselves weren't subjected to the kit's discipline.

That gives you a potential recursive test:

```text
project
  ↓
project-kit
  ↓
agent uses project-kit
  ↓
agent reviews project
  ↓
agent reviews project-kit
  ↓
agent checks claims made by project-kit
```

And the last step is where I failed.

I think that's considerably more interesting than adding a schema.

And, as feedback on the original review: **you caught me doing exactly the thing your repository warns about.** I inferred that the conceptual consistency of the artifact implied a degree of factual consistency that I hadn't actually established. That's worth preserving as a failure case when you start running the cold tests.

## Third message, verbatim

No objection. In fact, I think that's the most honest way to record it.

I'd make two distinctions explicit:

1. **It is not a result of the cold-session test.** It is a separate observation from an external review of the repository. The cold-session methodology would need its own test to determine whether a fresh agent can reconstruct state.

2. **It is evidence of a failure, not evidence that the general problem is solved.** One observed miss establishes that this review approach failed to catch two factual inconsistencies. It doesn't establish how often that happens, whether `project-kit` would prevent it, or whether another reviewer would have caught them.

The write-up could be very simple:

Initial Review Failure

Date: September 17, 2026
Source: External AI review

An external review of project-kit was conducted to evaluate the repository's concepts, structure, and claims.

The review correctly identified several conceptual issues, including the vendor-specific wording of the memory rule, the distinction between verification standards and operating policy, and the risk of over-formalizing the project's state tracking.

It failed to identify two factual inconsistencies that were present in the repository:

1. The README's description of CLAUDE.md did not match the contents of CLAUDE.md.
2. The README stated that every standard in the template carried the failure that produced it. At the time of review, only three of the ten standards had such a documented failure.

Both omissions are significant because they violate the project's own Rule 3: "Don't claim what you haven't checked."

This is therefore recorded as a failure of the review, not as evidence that the repository was internally consistent.

The result does not test the cold-session methodology. A cold-session test evaluates whether an agent can reconstruct project state from a repository; this observation instead concerns whether an agent reviewing a repository can verify claims made by the repository itself.

This is the first recorded empirical result associated with project-kit. No inference is made from a single result about the general reliability of AI review or the effectiveness of project-kit.

I'd actually preserve the **original failed review**, rather than correcting it and only recording the corrected version. The failure is more valuable if someone can reproduce exactly what I saw, what I concluded, and what I missed.

And I agree with your broader principle: **if a fail is worth more than a pass, then the project's first result shouldn't be cleaned up because it's embarrassing.** It should be made unusually easy to inspect.

One further thought: this gives you a natural second experiment that is *not* the cold-session test: **claim-review testing**. Give an agent the repository and ask it to audit every externally verifiable claim in the README against the actual artifacts, without telling it which claims are suspect. That's a different test with a different ground truth.

