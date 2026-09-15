# Run your own Discord guild for your project (and don't do it manually)

**Dated:** 2026-09-15

If you ship open-source tools solo, you eventually want a Discord server so users stop DMing you at odd hours. Fine. But running one manually — checking channels, answering the same "how do I install this" question for the fortieth time, moderating — is a part-time job you didn't sign up for.

## The pattern

Wrap the Discord bot API in an MCP server so your coding agent can drive it the same way it drives your codebase: [discord-mcp](https://github.com/sandraschi/discord-mcp) — messages, guild/channel management, roles, moderation, and RAG-backed search over your own message history, all as agent-callable tools instead of manual clicking.

What that buys you in practice:

- **Ask your agent about your own server history.** "Has anyone asked about the Windows install path before?" becomes a RAG query over indexed message history instead of Ctrl-F through channels.
- **Draft moderation and welcome flows as code**, version them, review them — instead of hand-configuring a bot dashboard you'll forget how you set up in six months.
- **Agentic triage**: point it at a goal ("check for unanswered support questions in #help") and let it use sampling + tools to work through it, escalating anything it's not confident about rather than guessing.

## The honest caveat

A bot with 43 operations and moderation powers is also a bot that can do 43 kinds of damage if you let an agent run unsupervised. Keep destructive actions (bans, mass-deletes, role changes) behind an explicit human-approval step — don't hand an LLM standing write access to your community and walk away. This is the same "agents act, humans approve" rule that should apply to anything with real-world blast radius, not just Discord.

## If you don't want to build your own

You don't need a bespoke MCP server to get 80% of the value — a scheduled bot script hitting the Discord REST API directly, plus a cron job that pings you for anything unanswered after 24h, covers most solo-maintainer needs. The MCP wrapper pays off once you want your coding agent to reason about server state alongside your codebase in the same session, not before.
