# Snap small tools together instead of building one big one

**Dated:** 2026-09-15

The instinct once you have three related tools is to merge them into one bigger, "properly integrated" app. Resist it longer than feels comfortable. A monolith couples your release cycles, your failure domains, and your mental model together — you can no longer touch one thing without reasoning about all of it.

## The pattern: one tool per job, an optional thin link between them

Build each tool to be fully useful standalone. Then, where two tools *would* benefit from knowing about each other, add a narrow, optional integration — not a merge:

- **One-hop, not deep coupling.** Tool A can hand a well-defined artifact to Tool B (a file path, a structured result, an ID) — it should not need to understand Tool B's internals, and Tool B should not need Tool A installed to function on its own.
- **Soft degradation.** If the peer tool isn't installed or isn't running, Tool A should say so plainly and keep working for everything that doesn't need the peer — not crash, not silently no-op.
- **No forced installs.** Nobody should have to install your whole toolchain to use one piece of it. The integration is a bonus for people who have both, not a tax on people who only want one.

## Why this beats the monolith for a solo dev or small team

- **You can rewrite or replace one tool without a migration project.** A monolith's internal modules drift into load-bearing coupling; separate tools with a thin contract between them don't.
- **Failure is contained.** If the integration breaks, the two tools individually still work — you've lost a convenience, not the whole system.
- **It's easier to open-source or hand off one piece.** A single-purpose tool with a clean, documented interface is something someone else can actually adopt. A tightly coupled module inside your monolith usually isn't.

## The concrete shape this takes with MCP-style tool servers

If you're building agent-callable tools (MCP servers or equivalent), this maps directly: each server owns one domain, exposes its own tools, and where two domains overlap (say, a video tool that wants transitions from an effects tool, or a PR/outreach tool that wants to post through a messaging tool), the caller passes a structured handoff rather than the two servers being merged into one codebase. Each one still runs, and is still useful, alone.

## The trap to watch for

"Loosely coupled" isn't a license to skip designing the interface. A sloppy, undocumented handoff between two tools is just monolith coupling with extra steps and worse error messages. The interface between tools deserves the same care as an API you'd publish for strangers — because eventually, it is one.
