# The bug depot: one file that remembers what already bit you

**Dated:** 2026-09-15

Every solo dev and every small team rediscovers the same three bugs every quarter, because the fix lived in someone's memory (or a closed PR nobody rereads) instead of somewhere the next debugging session — human or agent — actually looks.

## The pattern

Keep a single running file — `BUGS_DEPOT.md`, `TRAPS_AND_PITFALLS.md`, whatever you call it — that's a flat, numbered, symptom-first log of every bug that cost you more than a few minutes to diagnose. Not a design doc, not an architecture record. A lookup table: symptom → root cause → fix → don't-do-this-again rule.

Two properties make it actually work instead of becoming another abandoned doc:

- **Symptom-first, not chronological.** You (or an agent) hit a weird error and grep the depot for the error text before spending twenty minutes re-diagnosing something that's already been diagnosed.
- **It's a required read before touching the affected area**, not an optional appendix. If your coding agent has a "read before you code" list, the pitfall depot belongs on it — not buried in a wiki nobody opens.

## What earns an entry

Not every bug. A bug earns a depot entry when the fix wasn't obvious from the error message, when it's the kind of thing that will look like a *different* bug the second time it happens, or when it's a footgun baked into a tool/library/platform you'll keep using. "Typo in a variable name" doesn't need a depot entry. "This service respawns under the old code if you kill the process instead of using the service manager" does.

## Concrete example (real, from a fleet of 190+ small repos)

One entry: a Windows service managed by NSSM gets killed and restarted by hand via `taskkill`. NSSM either instantly respawns it with the same old code (so you *think* you restarted, you didn't), or the kill fails silently on an elevated service and the old process keeps holding the port. The depot entry says: always restart via the service manager (`sc.exe stop/start` or `nssm restart`), and verify a new PID actually owns the port afterward. That's a rule that would otherwise get relearned the hard way by every dev who touches that service for the first time.

## Bonus: run a fleet-wide grep when you fix a class of bug, not just an instance

If a bug turns out to be a pattern (same antipattern copy-pasted across several small projects, not a one-off), fix the instance, then grep your other projects for the same shape of mistake before calling it done. A bug fixed in one place and left everywhere else is only half fixed.

## What this isn't

Not a replacement for tests. A depot entry says "here's a thing that will bite you and here's the rule," a test says "this specific case can never regress silently again." Use both — the depot catches the class of mistake, the test catches the instance.
