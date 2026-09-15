# Two boring hygiene rules for anything an LLM writes into a real artifact

**Dated:** 2026-09-15

Neither of these is exciting. Both quietly prevent a specific, recurring class of embarrassing mistake in agent-generated content — commit messages, changelogs, reports, filenames, anything with a date or a character set that matters.

## 1. An LLM has no clock (or map) — never let it guess

A model has no live access to the current date unless something injects it. Left alone, it will confidently produce a date from training-adjacent memory, or silently drift from the actual date the longer a session runs. Same failure shape for location: a model will infer a place by association ("that kind of incident happens in X") instead of reading it from the actual source.

The fix is boundary-level, not vigilance-level — don't rely on remembering to check, make the pipeline incapable of skipping it:

- Anything timestamped (a report title, a log line, a changelog entry, a generated filename) should read the real clock at generation time, not have the model state a date from "knowledge." If no clock is reachable, write it as explicitly unknown rather than guessing — a placeholder you'll notice beats a wrong date you won't.
- If you're building a pipeline that prompts a model for a date, inject the real current date/timezone into the prompt yourself. Never leave "what's today's date" as a question the model answers from memory.
- Same logic for location: take it from the source text or a real lookup, never infer it by association. "Llamas live in the Andes, so this llama story is from Peru" is a fabrication wearing a syllogism as a costume.

## 2. Normalize LLM-generated prose to plain ASCII at the boundary

Models default to em dashes, curly quotes, and other typographically "nice" characters that break downstream systems in ways that are individually rare but collectively common: mis-rendered logs, broken filenames, mojibake in an email client, a diff that looks noisier than it is because every quote mark changed encoding.

The fix, again, is at the boundary, not per-output vigilance:

- Prompt for plain ASCII explicitly when generating anything that becomes a title, filename, log line, or commit message: straight quotes, hyphens instead of em/en dashes, no emoji unless actually wanted.
- Normalize programmatically before the string reaches a log, filename, or external system: em/en dash → `-`, curly quotes → straight, any mojibake replacement character → `-`. Don't trust the prompt instruction alone to hold under all conditions — enforce it in code at the point of use.

## Why bother with either

Both failure modes share a shape: individually small, invisible until the one time they aren't (a wrong date in a shipped report, a broken filename from a stray character), and both are fully preventable by moving the check from "hope the model gets it right" to "the pipeline can't produce the wrong thing." That's a better trade than remembering to proofread every generated artifact by hand.
