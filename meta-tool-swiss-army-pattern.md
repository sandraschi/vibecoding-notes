# The swiss-army meta-tool: build one thing that operates all your other things

**Dated:** 2026-09-15

Two related problems show up at different points in a growing toolkit, and they have the same shape.

## Problem 1: tool explosion inside one tool

A feature-rich tool server exposing sixty individually-named operations (`list_vms`, `get_vm_info`, `create_vm`, `start_vm`, `stop_vm`, `pause_vm`, `resume_vm`, ... forty more) is technically complete and practically unusable. Whoever's calling it — human or agent — gets a wall of near-identical names and no sense of what's actually available. The list itself becomes the UX problem.

**The fix: portmanteau tools.** Collapse a family of related operations into one callable with an action/operation parameter: `vm_management(action: "start"|"stop"|"snapshot"|..., ...)`. One discoverable entry point per domain instead of sixty flat names. This is a well-known pattern for anyone building agent-callable tool servers (MCP or otherwise) and it's worth applying the moment you notice you're naming your fifth `verb_noun` function in the same domain.

## Problem 2: tool sprawl across many tools

The second problem shows up later, once portmanteau design has already saved you from explosion *within* each tool: you now have a dozen, then a hundred, small well-designed tools/repos/servers, each internally consistent but with no consistent way to scaffold a new one, check whether an existing one still meets your own bar, or operate the whole set as a fleet instead of one-by-one.

**The fix: a meta-tool whose domain is your other tools.** Not another domain-specific server — a layer above all of them, with verbs like:

- **scaffold** — generate a new tool/repo to your current standard in one pass, instead of copy-pasting the last one and hoping you remembered every convention
- **wrap** — take something that already exists (a CLI, a library, an API) and harness it into your standard tool shape
- **probe** — certify a release actually boots and installs clean before you ship it
- **audit** — score every tool you own against your own accumulated standards, so drift is measured instead of vibes
- **operate** — register, schedule, and run the fleet as a set, not as N separate manual steps

A real example doing exactly this: a fleet of 180+ small MCP tool-servers gets a single meta-server whose only job is scaffolding, wrapping, probing, auditing, and operating the other 180 — it "does not serve data, it serves the fleet itself."

## Why this is the same pattern at two altitudes

Portmanteau collapses operation sprawl inside one tool. The meta-tool collapses *tool* sprawl across your whole toolkit. Both exist because flat, ungrouped surface area is a discoverability and consistency tax that grows worse the more you have — and both fixes are the same move: introduce one layer of indirection with a small, stable verb set, and push the sprawl underneath it instead of leaving it exposed.

## When not to build the meta layer yet

Don't build the meta-tool before you have the problem it solves. Three tools you maintain by hand is not tool sprawl, it's Tuesday. The signal that it's time: you're about to build your Nth tool and you notice you're re-deriving "what does a new one need to look like" from memory instead of from a written standard — that's the moment scaffold/audit pays for itself. Building it earlier is premature infrastructure for a problem you don't have yet; see [the-real-moat-is-tooling-not-prompts.md](the-real-moat-is-tooling-not-prompts.md) for the general "when does tooling actually pay off" question.

## The trap: the meta-tool becomes the thing that goes stale

A meta-layer that audits everything else needs to also audit itself, and needs someone to actually look at what it flags. A `qualitycheck`/`audit` verb that's been quietly ignored for a few months is worse than no audit at all — it creates the appearance of oversight without the substance. If you build this, put the meta-tool itself on the same accountability hook as everything it watches.
