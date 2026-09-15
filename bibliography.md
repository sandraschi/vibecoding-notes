# Bibliography / link dump

Everything here gets a one-line editorial comment. Not because I think my opinion is gospel, but because a bare link list is useless — you can't tell "essential" from "clicked it once in 2025" without someone saying which is which. Dated 2026-09-15; channels and sites drift, re-check before trusting blindly.

## YouTube — AI coding / model news

- **[Andrej Karpathy](https://www.youtube.com/@AndrejKarpathy)** — if you watch exactly one channel on this list, make it this one. Actual model internals, actual pedagogy, zero hype cadence. The opposite of a thumbnail with a red arrow and an open mouth.
- **[Matthew Berman](https://www.youtube.com/@matthew_berman)** — genuinely fast on new releases, decent hands-on testing. But the enthusiasm dial has been stuck on 9 for a while now — every model is "insane," every week is "the week everything changed." Useful for "what shipped," discount the superlatives by half.
- **[ThePrimeagen](https://www.youtube.com/@ThePrimeagen)** — opinionated, entertaining, occasionally right about tooling before it's cool. Take the trash-talk as flavor, not benchmark data.
- **[Fireship](https://www.youtube.com/@Fireship)** — 100-second explainers are genuinely great for "what is this thing," genuinely useless for "should I switch to it." Know which video you're watching.
- **[AI Explained](https://www.youtube.com/@ai-explained-)** (channel name/branding has shifted around — search current handle) — closest thing to a sober benchmark-literate voice in the space when active. Reads papers instead of press releases.
- **[Matt Wolfe](https://www.youtube.com/@mreflow)** — good weekly aggregator if you want a news digest and don't need depth. Treat as a table of contents, not a review.
- **Cole Medin / LangChain channel** — solid if your interest is agent-building specifically (RAG, tool use, orchestration), less useful for raw model comparisons.

## Independent benchmark sites (check these before trusting a vendor's launch post)

- **[llm-stats.com](https://llm-stats.com/)** — 300+ models, continuously updated from public benchmarks and live API pricing. Good default first stop.
- **[Artificial Analysis](https://artificialanalysis.ai/)** — quality/price/speed/latency in one comparable table. The one I actually check before believing a "beats GPT-X" headline.
- **[Arena](https://arena.ai/)** (formerly LMArena/lmarena.ai, rebranded January 2026) — blind human-preference Elo. Good signal for "which model do humans actually prefer," bad signal for "which model is best at my specific coding task" — vibes-based by design.
- **[CodeSOTA](https://www.codesota.com/llm)** — every score dated, every source linked. If a site can't tell you *when* a score was measured, don't trust the score.
- **[BenchLM](https://benchlm.ai/)** — benchmarks, pricing, runtime signals, context window in one table, pulls from Artificial Analysis data.
- **[Iternal.ai LLM Benchmark Repository](https://iternal.ai/llm-benchmark-repository)** — raw scores (SWE-bench Verified, LiveCodeBench, Aider Polyglot, BFCL, Arena ELO) with daily refresh, no editorializing. Good for cross-checking a vendor's cherry-picked benchmark table against the full spread.
- **[BestLLMfor](https://bestllmfor.com/leaderboard/)** — if you're running local models, this is the more relevant leaderboard than the frontier-model sites above.

## Vendor blogs / docs (primary sources — read past the headline number)

- **[DeepSeek API docs / changelog](https://api-docs.deepseek.com/updates/)** — actually publishes pricing changes and peak/off-peak windows in plain text. More useful than most vendor blogs for operational decisions.
- **[Anthropic news](https://www.anthropic.com/news)**, **[OpenAI news](https://openai.com/news/)**, **[Meta AI blog](https://ai.meta.com/blog/)** — primary sources, but remember a launch post is marketing copy with numbers in it. Cross-check every headline benchmark against an independent site above before repeating it.

## The one meta-rule for all of the above

Vendor self-reported numbers and independently-verified leaderboard numbers are not the same category of fact. A launch post saying "beats Opus 5" is a claim; a dated entry on CodeSOTA or Iternal is (closer to) a measurement. Keep them separate in your head, and be suspicious of anyone (including a YouTuber, including me) who doesn't.
