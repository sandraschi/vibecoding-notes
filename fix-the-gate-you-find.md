# If you broke the build gate discovering it, it's yours now

**Dated:** 2026-09-15

You open a repo to fix one small thing. `tsc --noEmit` is already red. The test suite already has three failing tests unrelated to what you came to do. Easy to think: not my problem, I'm just here for the one-line fix.

It's your problem the moment you need that gate green to verify your own change.

## The rule

If a pre-existing failure (typecheck, lint, test suite, a broken build script, a stale import path) would cause *any* verification gate to fail while you're in the repo, fix it — not because you broke it, but because you cannot verify your own change without a working gate, and shipping a change on top of a gate you know is broken means the next person inherits a repo that looks tested and isn't.

## Where this rule has an edge, and where it doesn't

**In scope, always:** anything blocking the build/lint/test pipeline you need to run to check your own work. A wrong import path, a syntax error, a broken CI script — fix the actual defect, not the architecture around it. Don't use "I found a bigger problem" as license to redesign the module; fix the specific thing that's red.

**Out of scope, with judgment:** something broken in a completely unrelated area, not in any file you touched, not in the build chain your change depends on, and expensive enough to fix that it would dwarf the original task. Flag it, don't silently absorb it — tell whoever you're working with/for, and let them decide whether it's now in scope.

The distinguishing question: *does this failure block me from verifying my own change?* If yes, it's not optional cleanup, it's a precondition for you being able to claim your change works at all.

## Why this is worth writing down explicitly

Without the explicit rule, the default incentive runs the wrong way — the fastest path to "done" is to ignore the red gate and ship anyway, especially under any kind of time pressure. Writing the rule down (for yourself, or as an instruction to an agent) converts "technically not my job" into "obviously blocks my job," which is the actual truth of the situation.

## The failure mode this prevents

A repo where every contributor reasonably decides the existing red gate isn't their problem accumulates red gates until the gate is red by default and nobody trusts it — at which point the gate has stopped doing its job for anyone, including the person who eventually needs it.
