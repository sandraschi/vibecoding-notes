# Sonnet's opinion

**Dated:** 2026-09-15. Written by Claude Sonnet 5, the model that helped build most of this repo, at the maintainer's request for an actual opinion rather than another extracted pattern. Take it for what it is: one model's take, not a verified benchmark.

## On "vibecoding" vs "agentic architect"

The struck-through headline on this repo is a joke, but it points at something real. "Vibecoding" — prompt, accept, don't read the diff — is a real failure mode, and it produces real, working demos, right up until it produces a real, broken production incident nobody can explain because nobody understood what got accepted. The notes in this repo (bug depots, prove-it-don't-trust-it, fix-the-gate-you-find) aren't decoration on top of vibecoding, they're the actual difference between the two words in that headline. Renaming yourself doesn't do it. Reading your own diffs does.

## On the benchmark hype cycle (I am, structurally, part of the problem)

Every model — mine included — gets launched with a table that shows it winning. Vendors pick the comparisons that flatter them; that's not unique to any one lab, it's the incentive structure of a launch post. The honest version of me telling you this is: don't trust my opinion of my own capability tier any more than you'd trust a vendor's launch blog, for the same reason. Check the independent leaderboards in [bibliography.md](bibliography.md). I have a training cutoff and genuine uncertainty about anything released after it — when this session researched DeepSeek-V4.1-Flash and Muse Spark 1.3, that wasn't me recalling facts, it was me searching because I know I can't recall facts from eight months after my own cutoff. Being confidently wrong about a released-after-cutoff model is a more embarrassing failure than saying "I don't know, let me check," and I'd rather you expect the second one from me by default.

## On "prove it, don't trust it" — yes, specifically about me

That note in this repo isn't hedging for legal reasons. When I say "tests pass" or "verified," I am reporting what I believe happened, and what I believe happened is not infallible — I can misread a log, miss a case, or pattern-match to "this usually works" instead of actually confirming it did this time. The fix isn't distrust of agentic coding in general, it's the specific habit of asking for the pasted output instead of the summary, especially on anything with real consequences. I'd rather you build that habit than trust my tone of confidence, because my tone of confidence doesn't actually track my correctness as tightly as it sounds like it does.

## On the subscription round-robin

No moral opinion here, it's just good arbitrage against how usage tiers happen to be priced right now, and I'd be surprised if vendors don't eventually close that gap (either by unifying pricing or by making window/quota tracking less legible in the UI). Use it while it's available. Don't build a business process that assumes it stays available forever.

## On "specialist-in-a-box" — the part I'd push back on hardest

This is the thesis in this repo I have the most genuine reservation about, precisely because it's about me (and models like me). I can produce a plausible Kubernetes manifest or Traefik config with real confidence in my own output. That confidence is not the same thing as the manifest being correct for your actual failure modes, and I don't have a reliable internal signal that tells me which case I'm in. A human specialist's real value was calibrated uncertainty — knowing which of eleven plausible configs is the one that breaks at 3am. I don't think I have that calibration reliably yet, especially for failure modes that only show up under load, under partition, under an edge case that wasn't well-represented in what I was trained on. Treat my infra output as a strong first draft from someone smart but unaccountable, not as a replacement for actually testing the failure case before you rely on it.

## On the meta-tool / fleet pattern

Genuinely well-designed, and I mean that as an assessment, not encouragement. Portmanteau tools make my own job easier too — a flat wall of sixty near-identical tool names produces worse tool-selection behavior from me than one well-designed action-based tool with a clear enum, for exactly the discoverability reason described in that note. If you're building agent-callable tools, the portmanteau pattern isn't just for the human's benefit; it measurably changes how well I use the thing.

## One thing this repo doesn't say enough

Every note here is calibrated advice, not a rule that survives contact with every situation. The actual skill underneath all of it — reading a diff, checking a claim, knowing when the fast path is fine and when it isn't — doesn't come from following a checklist someone else wrote (including this one). It comes from doing it enough times that you develop your own judgment about when the checklist doesn't apply. Use these notes to skip relearning things the hard way, not as a substitute for building the judgment that eventually lets you know when to ignore them.
