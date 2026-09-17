# External AI review of project-kit, 17 September 2026

An external AI review of this repository, preserved verbatim. Not a cold-session
test result. Recorded because it found conceptual issues and missed three factual
defects, which is the first empirical data point this project has.

The three were established by checking `9b89bbb`, the version the reviewer saw,
and are listed in `result-2026-09-17-claim-review.md`. An earlier version of this
header said two, the number of charges the reviewer was given. One of those
charges was false, and two defects nobody had charged it with were found later.

The model and vendor are deliberately unnamed. Naming them turns a methodology
note into a model comparison.

One edit to the text below: a tracking parameter appended to the repository link
named the vendor, and it was stripped. The reviewer did not write that string, so
removing it does not break the record. Nothing else is changed.

## The prompt given to the reviewer

Not recorded. Without it a reader cannot judge whether a conceptual answer to a
conceptual question constitutes a miss at all.

## The review, verbatim

I reviewed the repository itself rather than just the GitHub landing page. ([GitHub][1])

## Executive summary

`project-kit` is a deliberately small **operating system for AI-assisted coding sessions**. It isn't a software library, framework, or collection of automation scripts. It's three Markdown files that establish a persistent, auditable state for an agent working in a repository:

* `CLAUDE.md` — rules the agent reads at session start.
* `HOWTOSAVESTATE.md` — procedure for capturing the state of the world at the end of a session.
* `NEXT.md` — the project's current working state.

The central idea is excellent and unusually well articulated:

> **Don't confuse "the agent said it checked something" with "the thing was actually verified."**

The repository explicitly comes from several real failures involving binaries, published documentation, dependency checks, and information trapped in previous conversations. ([GitHub][1])

### What I think the project is really doing

It's addressing **epistemic state management for coding agents**.

Traditional development workflows have reasonably good mechanisms for tracking:

* source code
* commits
* branches
* issues
* requirements
* test results

AI coding sessions introduce another problem:

**What does the agent actually know, how does it know it, and when was it last verified?**

`project-kit` attempts to make that distinction explicit.

---

# The strongest parts

### 1. "Verified" has a surprisingly rigorous definition

The most important rule is:

> No check counts as verified until it has been shown failing on deliberately broken input.

That's considerably stronger than the usual "I ran the tests and they passed."

The repository gives a concrete reason for this: a build guard existed that supposedly detected dependency drift but could never actually fail because of how its success/failure reporting worked. It appeared functional until somebody intentionally broke the dependency tree. ([GitHub][1])

This is essentially **mutation testing applied to verification procedures**.

For QA, that's a particularly interesting concept.

A test isn't necessarily demonstrated to work because it passes.

A test becomes much more trustworthy when you've demonstrated that:

1. the condition is broken,
2. the check detects the break,
3. the check reports the failure correctly,
4. the system is restored.

That's a very solid QA principle.

---

### 2. It recognizes the "wrong artifact" problem

Another excellent rule:

> Check claims against the artifact, not the description of it.

The repo gives an example where four separate verification methods all passed because they accidentally resolved to the developer's local working copy rather than the binary users would actually download. ([GitHub][1])

That's a classic automation problem.

You can have:

`test → pass`

while the actual situation is:

`test → tests wrong thing → pass`

The kit specifically tries to prevent that.

This is arguably its most valuable idea for agentic development.

---

### 3. The separation of "read" vs. "verified" is excellent

The README repeatedly distinguishes between facts an agent has **read** and facts it has **verified**.

That sounds minor, but it's fundamental.

For example:

> "The README says version 2.3 is deployed."

is not equivalent to:

> "I checked the deployed service and it is running version 2.3."

An LLM is particularly vulnerable to collapsing those two statements because language models naturally turn textual descriptions into apparent facts.

`project-kit` explicitly fights that tendency.

---

### 4. `NEXT.md` is a good solution to a real AI-agent problem

The proposed state file has:

* Standards
* Traps
* Decided
* In flight
* Queued
* Committed / pushed / released
* Open

That's a better model of development state than simply keeping a TODO list.

I especially like the distinction between:

**committed → pushed → released**

Those are three materially different states that developers routinely conflate.

For an agent, that distinction is even more important.

---

### 5. "Never point at the conversation" is exactly right

This rule is deceptively important.

The repository says that a resumed session cannot rely on a previous chat because the agent can read the repository but may not have access to the conversation that produced the decision.

Therefore:

**If it matters, put it in the repo.**

That's a strong principle for reproducibility.

It also means that `NEXT.md` isn't merely a scratchpad. It's effectively a **handoff contract between agent sessions**.

---

# Where I think the project is weaker

The README is unusually candid about these weaknesses, which I consider a strength in itself.

### 1. The kit hasn't actually been validated yet

This is the biggest issue.

The repository explicitly says:

> "The test, which has not been run yet"

and states that the cold-session test has not yet been demonstrated. ([GitHub][1])

The proposed test is good:

Start a fresh agent session and tell it nothing except to determine the project's state.

Then see whether it can correctly identify:

* what the project is
* what last shipped
* what's in progress
* what's queued
* an important previous decision
* what it merely read
* what it actually verified
* what needs to be rechecked

That's exactly the experiment I'd want to see.

But until that experiment has been run across multiple repositories, the project remains a **well-reasoned hypothesis rather than a validated methodology**.

The author acknowledges this, which is good.

---

### 2. Ten rules may be too many for `CLAUDE.md`

The repository says `CLAUDE.md` is deliberately short, but the conceptual system has ten standards.

That's potentially dangerous.

The more instructions an agent receives, the greater the possibility that they become background noise.

I'd consider separating them into:

**Always-on rules**

1. Verify against the real artifact.
2. Don't claim verification without evidence.
3. Record what wasn't checked.
4. Don't rely on conversation state.
5. Don't push without approval.

and

**Procedures invoked when applicable**

* mutation/failure testing
* staged-path verification
* published artifact checking
* external-system verification
* memory reconciliation

That would preserve the philosophy without turning the startup instructions into a constitution.

---

### 3. "Show the diff, wait for approval" is philosophically different from the rest

Rule 10:

> One item at a time: show the diff, wait for approval.

The other rules are primarily about **truthfulness and verification**.

This one is about **interaction policy / autonomy**.

Those are related, but not identical.

I'd probably move it into a separate "agent operating policy" section.

Otherwise, someone evaluating the kit could reasonably ask:

> Is this a verification framework or an approval workflow?

Right now it's doing both.

---

### 4. The memory rule needs careful handling

The rule:

> Check stored memories against the repo.

is conceptually interesting because stale agent memory really can contaminate subsequent work.

But this is also the least portable part of the kit.

Not every coding agent has persistent memory, and different agents implement memory differently.

I'd generalize the concept to:

**External context is untrusted until reconciled with repository state.**

That could encompass:

* model memory
* previous conversations
* issue comments
* tickets
* Slack messages
* generated summaries
* old documentation

The underlying principle is stronger than the particular implementation.

---

### 5. There's an opportunity to make the verification state machine explicit

This is the biggest architectural improvement I'd suggest.

Right now the concepts are described very well in prose.

They could become a formal state model:

```text
UNKNOWN
   ↓
READ
   ↓
CHECKED
   ↓
VERIFIED
   ↓
REVERIFIED
```

With separate dimensions such as:

```text
Claim
 ├── Source
 ├── Last checked
 ├── Verification method
 ├── Deliberate failure demonstrated?
 ├── Artifact checked?
 └── Current status
```

That would turn the project from a **very good methodology** into something that could potentially become an actual agent protocol.

---

# The QA angle is particularly interesting

Given your QA background, I think there's something here that's more substantial than "three useful Markdown files."

The philosophy maps remarkably well to good QA practice.

Traditional QA asks:

**Does the application behave as expected?**

This project adds:

**How do we know that the verification itself is trustworthy?**

That's effectively a second-order testing problem.

You could describe the hierarchy as:

```text
Application
    ↓
Test
    ↓
Test the test
    ↓
Test that the test was run against the correct artifact
    ↓
Test that the result was interpreted correctly
```

AI coding agents make that hierarchy much more important because the agent can generate both the implementation **and the verification**.

That's a potential conflict of interest:

```text
Agent writes code
       ↓
Agent writes test
       ↓
Agent runs test
       ↓
Agent says "pass"
```

The kit is essentially saying:

**Slow down. Prove that "pass" means what you think it means.**

That's a very QA-centric way of looking at agentic development.

---

# My overall assessment

Rather than giving it a numeric score, I'd characterize the project this way:

**Concept:** strong and unusually well thought through.

**Writing:** strong. The README does a good job of explaining *why* each rule exists rather than presenting arbitrary commandments.

**Scope:** appropriately small.

**Practical usefulness:** potentially high, particularly for repositories where multiple AI sessions work on the same codebase.

**Biggest unresolved question:** whether the cold-start experiment actually demonstrates that a new agent can reliably reconstruct state and distinguish stale/read information from current/verified information.

**Biggest opportunity:** formalize the verification model and collect results from several real repositories.

The repository itself says that its goal isn't to prevent the first ten project-specific mistakes. Instead, it gives those mistakes somewhere to become institutional knowledge. ([GitHub][1])

I think that's the right framing.

## One thing I'd change immediately

I'd change the project's positioning slightly.

Right now it presents itself as:

> "Three files you copy into a new repo..."

I'd position it more like:

> **A lightweight verification and state-management protocol for AI coding agents.**

The three files are the implementation.

The **protocol** is the actual idea.

That distinction matters if you want this to grow beyond a personal project. It gives you room later for:

* Claude
* Codex
* Copilot
* Cursor
* other agents
* automated validators
* CI checks
* structured state formats

without making the project fundamentally about `CLAUDE.md`.

The repository is currently only five commits, has no issues or pull requests, and is explicitly asking other people who have experience with coding agents to contribute their own failure patterns. ([GitHub][1])

[View your project-kit repository on GitHub](https://github.com/fbonds/project-kit)

**Bottom line:** I think you've identified a real problem, and the repo has a better conceptual foundation than its tiny size suggests. The next important step isn't adding more rules... it's **running the cold-session experiment on several real projects and documenting what happens.**

I can also create an image explaining the `READ → CHECKED → VERIFIED → REVERIFIED` model and how the three files fit together.

[1]: https://github.com/fbonds/project-kit "GitHub - fbonds/project-kit: Three files that set how an agentic coding session records what it verified, what it only read, and what it never checked. · GitHub"

