# Cheap insurance before you let an agent touch a lot of files at once

**Dated:** 2026-09-15

The scariest failure mode in agentic coding isn't a bug — it's a *silent* bug across many files at once. A single bad regex in a "quick fleet-wide cleanup" script can corrupt fifty files before anyone notices, because nobody reviews fifty diffs as carefully as they review one.

## Two cheap habits that cover almost all of the risk

**1. Checkpoint commit before anything that touches many files.** Commit (or at minimum `git status` and stash) whatever's in progress before running a batch edit, a recursive find-replace, or handing an agent a "go fix this across the repo" task. If it goes wrong, you want a clean point to diff against and revert to — not a tangle of the batch damage mixed in with your actual in-progress work.

**2. Timestamped `.bak` copies before any mutation touching 3+ files.** Before a script or agent rewrites a batch of files, copy each one aside first (`file.ext.20260915_143000.bak`, gitignored). It sounds redundant with git, and mostly it is — until the mutation happens in a repo without git initialized, or the commit itself gets fumbled, or you want a stupid-simple diff without touching git history at all. Cheap, boring, has saved real work.

**One real incident that justifies both:** a fleet-wide regex replace across 100+ build scripts, no backup, no per-repo review — corrupted them all in one pass, silently, because the regex matched more than intended and nobody was reviewing each file. A checkpoint commit would have made it a one-command revert. `.bak` files would have made it a diff-and-restore. Neither existed, so it was a manual rebuild.

## The actual rule of thumb

If an edit touches 3 or more files and isn't a trivial, individually-reviewed change (like a rename you're doing one file at a time with your own eyes on each diff), treat it as a batch mutation: checkpoint first, review the diff of *every* file after, not just a sample. "It matched the pattern I expected" is not the same as "I looked at what it actually did to each file."

## What this isn't

Not an argument against automation — fleet-wide fixes are often exactly the right call once you've found a bug pattern (see [bug-depot-pattern.md](bug-depot-pattern.md)). It's an argument against running that automation with no safety net and no per-file review, because the failure mode when it's wrong is silent and expensive, not loud and cheap.
