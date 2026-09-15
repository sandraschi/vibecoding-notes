# Demo videos that don't lie about what your tool does

**Dated:** 2026-09-15

The standard indie-dev demo video is a screen recording with royalty-free music slapped under it, narrated in a voice that's clearly reading a script for the first time, showing the one golden-path click sequence that always works. Viewers have learned to distrust this format for good reason — it usually is staging a happy path that doesn't survive contact with a real install.

## The bar to clear

A demo is worth making if it proves the tool works, not if it looks like it proves the tool works. Concretely:

- **Narrate against real output**, not a rehearsed voiceover written before the tool existed. If the narration and the on-screen behavior can drift apart, they will, and someone will notice.
- **Show the actual app**, driven by its actual automation (Playwright for a webapp, real window capture for a native app) — not a mockup, not slides pretending to be the product.
- **Timing should come from the content, not a fixed guess.** A narration line that's too long for its scene either gets cut off or the video looks weirdly padded. Stretch dwell time to match actual spoken length instead of eyeballing it.
- **Keep the boring parts boring.** Background music and transitions are fine polish, but if they're doing more work than the actual feature demo, that's a tell.

## The pattern, tooled

My own version of this: [demo-vid-mcp](https://github.com/sandraschi/demo-vid-mcp) — an MCP server that orchestrates Playwright (record the real webapp page-by-page), TTS narration synced to true speech length (so lines never get cut off or awkwardly padded), FFmpeg composition with real crossfade/wipe transitions between pages, and optional background music/SFX. It can also drive a native desktop app live (OBS window capture) while its own MCP tools actually invoke the app being demoed during the recording — not a staged screencast cut together afterward.

You don't need this specific tool to hit the bar above. The checklist is the point:
1. Record the real thing doing the real thing.
2. Narrate to match what's actually on screen, not a script written in advance of testing.
3. Publish the failure case too, or at least don't imply there isn't one — a demo that only shows the happy path and never mentions an edge case is a slightly more polished version of vendor benchmark cherry-picking (see [bibliography.md](bibliography.md)).

## What kills trust fastest

Cutting away from the screen right before the interesting part ("and then it just works!") is the single biggest tell that something didn't just work. If you have to cut there, fix the bug before you publish the video, not after.
