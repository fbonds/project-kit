# Working in this repo

<!-- Fill in PROJECT, and delete any line below that is not true here. Everything left
     should be something you would enforce, because a rule nobody enforces teaches the
     next reader that the rest are optional too. -->

**Read `NEXT.md` first.** It is the working state: what shipped, what is in flight, what is
decided, what is queued. Read it before proposing anything.

**Treat its facts as dated, not current.** Every claim in it records what was true when it
was checked. Anything outside this repo moves without a commit here to show it. The block
at the top of `NEXT.md` has the commands that re-check the moving parts. Stored memories
load before any file is read and go stale the same way, so check those against the repo
too.

**The standards are written down.** `NEXT.md` has all ten under "Standards", each with the
failure that produced it, and `HOWTOSAVESTATE.md` has the procedure for verifying state and
saving it at the end of a session, plus what each file here is for. The five that come up
constantly:

- **No check counts as verified until it has been shown failing** on deliberately broken
  input, and the report says what was broken.
- **Never verify through a path that can resolve to your own development copy.** A linked
  or global install, a symlink, a running dev server, a cached build: each will answer as
  though it were the artifact. Name the path, resolve it, prove it is the one you meant.
- **Check claims against the artifact**, not against a description of it: the published
  file, the fetched page, the built package. Not a commit message, a dashboard label, or
  `NEXT.md` itself.
- **Proposal before code, for anything with a surface**: a command, a flag, an API, a
  schema, a page. Show the surface and wait before implementing it.
- **Say what was not checked**, rather than leaving it out. An omission reads as a verified
  negative.

The other five: describe contents and order rather than counts and pagination; stage
explicitly; never point at the conversation, since a cold session reads files and not chat;
check stored memories against the repo, because they load first and a stale one outranks a
correct `NEXT.md`; and one item at a time.

**Writing.** No em dashes, anywhere: chat, files, commit messages, product copy. Say what a
thing does rather than performing it. No summaries of what you are about to say, and no
restating the request back before answering it.

**How to work.** One item at a time: show the diff and wait for approval before applying
the next. Stage explicitly by path, confirm with `git diff --cached --stat`, and never
`git commit -am`. **Never push.** PROJECT_OWNER pushes, and PROJECT_OWNER deploys and
releases.

**Do not start queued work unprompted.** `NEXT.md` names what is waiting and what was
deliberately rejected. Raise it rather than beginning it.
