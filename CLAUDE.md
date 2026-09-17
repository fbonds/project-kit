# Working in project-kit

**This is project-kit's own working file, filled in for this repository. It is not the
template.** To use the kit in another repo, copy the three files in `template/`, as the
README's "How to use it" section shows.

**Read `NEXT.md` first**, the one in this directory. It is this repository's working state:
what is pushed, what is in flight, what is decided, the traps, and what is open. Every fact
in it is dated. Re-check with the block at its top before acting on any of them.

## What this repository is

A documentation repository. Nothing builds, and there is no package and no release. What a
reader gets is the tip of `main` on GitHub, so that is the artifact a claim is checked
against: not the working tree, not an unpushed commit, and not a zip or copy of either.
`NEXT.md` has the commands that read it.

Every file here is public prose, read by people deciding whether to copy the kit.

## The files, and the rule for each

**`template/`** is what gets copied into other repos. It stays generic: its placeholders
stay intact and nothing about this repository goes in it. A change to a template file means
re-reading the README's description of that file in the same item, and a change to that
description means re-reading the file. The two have disagreed twice.

**`README.md`** is the argument for the kit. Every claim in it that a file or the git
history can settle has to survive being checked against that file. State each fact once: a
claim that appears in two places gets corrected in one of them and survives in the other.

**`docs/`** is the record: results, and the reviews behind them. A preserved review stays
verbatim, and any edit to it is declared in its header. A result that went badly is
corrected with the correction stated, never rewritten to look as though it went well. A new
file gets a line in `docs/README.md` in the same commit.

**`CLAUDE.md` and `NEXT.md` in this directory** are this repository's own working files.
Neither may contain the template's placeholder strings, even when quoting the template. The
README tells someone who copied these two by mistake that the setup grep will print no lines
for them, and that only holds while both files stay free of those strings.

**`LICENSE`** is MIT-0.

## Standards

The ten standards are written out in `template/NEXT.md`, and they apply here as written.
`NEXT.md` in this directory records this repository's own failures against them.

The end-of-session procedure is `template/HOWTOSAVESTATE.md`. There is no copy here, because
two copies drift. Where it asks for a list of the project's files, that list is the section
above.

## Working rules

**How to work.** One item at a time: show the diff and wait for approval before applying the
next. Stage explicitly by path, confirm with `git diff --cached --stat`, and never
`git commit -am`. **Never push.** Fletcher Bonds pushes.

**Confirm where you are before acting.** Say which working directory or repo you are in, and
challenge it if it looks wrong for the work. A scratch repo holding copied template files
has the same file names as this directory.

**Do not guess.** Check. If something cannot be checked from here, say that, rather than
reasoning your way to a plausible answer and presenting it as one.

**Do not start queued work unprompted.** `NEXT.md` names what is waiting, what is open, and
what was deliberately rejected. Raise it rather than beginning it.

## Writing

Every file here is public, so the writing rules apply to all of it and to how you write to
the owner. They are in the Writing section of `template/CLAUDE.md`. Read that section before
writing or editing prose here. They are not repeated in this file, so that there is one
copy.
