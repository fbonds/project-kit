# How to build

The procedure for taking something new in PROJECT from an idea to built. Read it when work
starts on anything new. The steps below are for a feature. The last section says what a
small fix keeps.

The owner can say what they want. The agent's job is to turn that into work the owner can
judge before and after each step, rather than only at the end.

## 1. Interview

Ask one question at a time until the spec below could be written without guessing. Ask
about what it should do, not how to build it. Stop when every part of the spec has an answer
or an `Open:` line.

One question at a time keeps each answer about one thing, and lets the next question build
on the last answer.

## 2. Write the spec

One file for each piece of work, under `docs/specs/`, named with its date first, and a line
for it wherever `docs/` is indexed. It holds:

- **What should be true** when it is done, in terms the owner can check.
- **What must not change**: the behaviour next to it that has to keep working. A change that
  passes its own check and breaks something beside it is the usual way a fix goes wrong.
- **Out of scope**: what it will not do, so that it does not get built anyway.
- **Checks**: how each line under "what should be true" will be checked against the
  artifact, and how each check will first be shown failing.
- **Tasks**, in order, each small enough that its diff can be read in one sitting, and each
  with its check.
- **`Open:` lines** for anything not settled. A later session treats whatever is written as
  settled, so a guess written without the marker becomes a decision nobody made.

## 3. Approval

The owner approves the spec before any code is written. This is rule 4 applied to a whole
piece of work. Plan mode in Claude Code holds edits until a plan is approved, and can carry
this step. Every `Open:` line is answered, or moved out of scope, before approval.

## 4. Build

Start a fresh session for the build, so that it works from the spec rather than from the
conversation that produced it. Take the tasks one at a time. For each:

1. Write the check first and run it. It must fail, and for the reason the task exists. A
   check that passes before the code is written is not checking the task.
2. Write the code, and run the check until it passes.
3. Run the whole test suite with the command `CLAUDE.md` names, so a task that breaks
   something else is caught at that task and not three tasks later.
4. Show the diff and wait for approval, as rule 10 says.

Where no automated test can run, the check is whatever the spec named for that task, and it
is still shown failing first.

## 5. Review

For work with more than one task, a second session or a subagent reviews the finished diff
against the spec before it is called done. A reviewer that has not seen the reasoning reads
what was built rather than what was meant. Ask it to report gaps that affect correctness and
to skip style, because a reviewer asked to find problems will always find some.

## 6. Done

Done means each check in the spec was run against the artifact and passed, after it had
been seen to fail. Remove the item from In flight in `NEXT.md`. The spec stays in
`docs/specs/` as the record of what was asked for.

## A small fix

A bug or a one-line change skips the interview, the tasks and the review. It keeps a line
saying what must not change, a check that reproduces the problem and fails before the fix,
and a run of the whole suite after it. Write those in its In flight entry in `NEXT.md`
rather than in a spec file.
