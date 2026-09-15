# Prove it, don't trust it: verifying agent-built code with artifacts

**Dated:** 2026-09-15

An agent telling you "done, tests pass, verified" is a claim, not evidence. The gap between "the agent believes it works" and "it actually works" is where most of the embarrassing bugs in agent-built code live — not because the agent lied, but because "looks right" and "is right" diverge more than people expect, especially on UI and integration work an agent can't actually see rendered.

## The pattern: demos as captured, re-runnable artifacts

Instead of accepting a chat message claiming success, require the proof to exist as a committed, re-runnable artifact:

- **Real command output, captured, not summarized.** A markdown demo file that embeds the actual stdout/stderr of the commands it claims to have run — not a paraphrase of what the agent thinks the output was.
- **Screenshots for anything visual.** If a webapp page is supposed to render a certain way, a screenshot committed alongside the change is worth more than a description of the change.
- **An anti-cheat re-run.** The strongest version of this: a verification step that *re-executes* the recorded commands and diffs the output against what was claimed, so a stale or fabricated demo gets caught automatically instead of silently going stale.

## Why this matters more for agentic coding specifically than for human coding

A human who claims "I tested it" usually has some actual memory of clicking the button. An agent's "tests pass" can be a genuine test run, a misread of a green-looking log line, or (more embarrassingly for the vendor asserting it, less so for you if you catch it) an assumption based on what usually happens. You cannot audit the agent's internal confidence. You can audit a screenshot, a diff, or a re-executed command.

## The cheap version if you don't want dedicated tooling

You don't need a full pipeline to get 80% of the benefit:

1. Ask the agent to show you the actual command output in the response, not a summary of it ("ran `pytest`, 12 passed" is a claim; the pasted pytest output is evidence).
2. For UI work, actually open the app and look — or ask the agent to take a screenshot and paste it, not describe what it should look like.
3. Treat "should work now" language as a flag to verify, not a signal to move on.

## What this isn't

Not paranoia about the tool being adversarial — it isn't. It's an acknowledgment that "confidently stated" and "verified" are different epistemic states, for humans and agents alike, and that the fix is cheap: make the proof an artifact instead of a sentence.
