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

## The part that doesn't dissolve (same caveat as specialist-in-a-box, worth repeating because it's this important)

Being able to produce a working Blender script or a compiling Swift app doesn't mean you've acquired an artist's eye for composition, or Apple's actual taste for what makes an app worth shipping, or the judgment for which of several technically-valid approaches will actually hold up. The memorization wall and the taste/judgment wall are different walls. AI dev reliably dissolves the first. It does not reliably substitute for the second — you still have to look at the render and know if it's good, still have to use the app and know if it feels right. That's the same distinction [specialist-in-a-box.md](specialist-in-a-box.md) draws for infrastructure, and it holds here for exactly the same reason.

## Sources

- Daniel Dennett, *Darwin's Dangerous Idea* (1995) — origin of the "universal acid" framing, applied there to natural selection; repurposed here by analogy, not a direct claim about AI from that source.
