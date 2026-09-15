# AI dev is universal acid: it dissolves learning-curve walls, not just devops ones

**Dated:** 2026-09-15

[specialist-in-a-box.md](specialist-in-a-box.md) made this argument for devops specifically — Docker/Kubernetes, Grafana, Traefik, Tailscale, CI/CD. The same mechanism turns out to generalize far beyond infrastructure, to basically any tool or platform whose difficulty was mostly *memorization and onboarding cost* rather than raw conceptual depth.

## The old cost of entry, concretely

**Blender**: notoriously hypercomplicated. The traditional path to competence was months of dedicated practice, a thousand-plus pages of documentation, workshops, and a personal shortlist of trusted YouTubers, because the tool's difficulty lived largely in an enormous hotkey/menu/API surface that nobody memorizes quickly and everybody initially fights.

**iOS development**: Swift as a language, plus Apple's SDK/framework ecosystem, plus platform conventions (HIG, App Store review rules, the toolchain quirks) traditionally represented something like a six-month onboarding course before someone with general dev skills could ship a real app confidently.

Neither of these was "hard" in the sense of requiring genius — they were hard in the sense of requiring a large, specific, memorized surface area before you could be productive at all. That's exactly the kind of wall a model with broad pattern recall across that entire ecosystem doesn't have to climb the way a human does.

## What actually dissolves

- **The API/CLI surface stops being something you personally have to memorize.** The model already "knows" the tool's operations, argument shapes, and common invocation patterns — you don't need three months of muscle memory before you can ask for the right thing.
- **Comparative research becomes instant instead of a research project.** "Should I use MuJoCo or Isaac Sim for this robotics task" used to mean reading docs, forum threads, and benchmark comparisons over days; a model can lay out the actual tradeoffs (physics fidelity, GPU parallelism, ecosystem maturity, licensing) on request.
- **Known traps and bugbears get surfaced proactively**, the same job a human specialist's scar tissue used to do — instead of you discovering them the hard way over your first few months with the tool.
- **Finding the plugin/library ecosystem stops being "ask around and hope someone mentions the right repo."** A model that's ingested the ecosystem's landscape can point you at the actively-maintained option instead of the abandoned one with better SEO.

## Why "universal acid" is the right metaphor, not hyperbole

The term is borrowed from Daniel Dennett's description of natural selection as an idea that "dissolves" the traditional boundaries and assumptions of whatever domain it's applied to. The reason it fits here: this isn't a Blender-specific trick or an iOS-specific trick, it's a single underlying mechanism (broad pattern recall standing in for personally-memorized specialist knowledge) that applies to *any* domain whose difficulty was mostly the size and obscurity of its knowledge surface. It corrodes the same wall wherever that wall's material is "nobody documents this well and you just have to have done it a lot" — which turns out to be most walls.

## The part that doesn't dissolve — narrower than it first looks

Being able to produce a working Blender script or a compiling Swift app doesn't automatically mean the result is good. But "AI can't judge taste" turns out to be the wrong-sized claim — it needs splitting into two different skills that dissolve at very different rates:

- **Recognizing bad taste is much further along than the blanket caveat suggests.** Given a checklist of concrete failure categories, a model can reliably say "this hero section is generic, this help text is buried, this contrast fails accessibility" — see [ai-as-ui-blooper-detector.md](ai-as-ui-blooper-detector.md) for the actual checklist. That's real critique, not a coin flip.
- **Originating genuinely novel, best-in-class work from a blank page is the part that's still meaningfully behind.** Telling you the existing design is weak is not the same skill as producing the design that replaces it with something excellent and original.

So the honest version isn't "AI has no taste, you still need a human eye for everything." It's: **recognition of quality problems is close to solved when you ask for specific things; origination of exceptional original work is where the gap actually still lives.** Same distinction [specialist-in-a-box.md](specialist-in-a-box.md) draws for infrastructure judgment, just drawn at the right line for design specifically.

## Sources

- Daniel Dennett, *Darwin's Dangerous Idea* (1995) — origin of the "universal acid" framing, applied there to natural selection; repurposed here by analogy, not a direct claim about AI from that source.
