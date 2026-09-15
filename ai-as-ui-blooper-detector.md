# AI is a genuinely good UI/UX blooper detector — if you ask it to check specific things

**Dated:** 2026-09-15

[ai-dev-is-universal-acid.md](ai-dev-is-universal-acid.md) drew a line between AI dissolving the memorization wall and AI substituting for taste. That line needs narrowing: **recognizing bad UI/UX and generating great original UI/UX are different skills, and AI is much further along on the first one than the caveat implied.** "Urgh, that's ugly and unfriendly" is a real, reliable judgment a model can make when asked to check for it — the trick is asking for specific categories, not an open-ended vibe check.

## The precedent: this is the same move as fakefind, aimed at aesthetics instead of fake data

Auditing a webapp for hardcoded mock data, dead buttons, and placeholder content pretending to work is already a known, reliable pattern — point an agent at the running app with a checklist and let it report, read-only, no auto-fix. The exact same move works for UI/UX quality bloopers: give the agent a checklist of known failure categories and ask it to check the actual rendered app against each one.

## The checklist that actually gets reliable results

Open-ended "is this a good design" invites vague, unreliable output. A checklist of concrete, checkable categories gets specific, useful findings instead:

- **Tiny or low-contrast text** — anything below comfortable reading size, or text-on-background contrast that fails basic accessibility thresholds.
- **Buried or tiny help** — a help affordance that exists technically but is small enough or placed obscurely enough that a real user won't find it.
- **No onboarding for a non-trivial app** — a first-run experience that dumps a new user into a full interface with zero guidance, when the app has enough surface area to warrant a wizard or at least contextual hints.
- **Weak/generic hero section** — stock-photo energy, no clear statement of what the product does or why someone should care, above the fold.
- **Dead-end empty states** — a list, inbox, or dashboard with nothing in it yet and no call-to-action telling the user what to do next.
- **Controls that don't look clickable** — buttons styled like text, links styled like buttons, anything relying on a user's psychic hover-detection instead of a visible affordance.
- **Inconsistent spacing/alignment** — the kind of thing that reads as "cheap" or "unfinished" even to someone who couldn't articulate why.
- **Missing loading and error states** — a blank screen or a frozen spinner standing in for "we didn't design what happens when this fails or takes a while."

Ask an agent to check a screenshot or a live running app against this list specifically, and the findings are concrete and actionable — "the help icon is 12px and in the corner nobody looks" is a real, fixable finding, in a way "does this look professional" isn't.

## Where the line actually is

This doesn't mean the taste gap from the universal-acid note disappeared — it means it was drawn in the wrong place. **Recognizing that an existing hero section is generic and weak is reliable. Originating a genuinely novel, best-in-class hero section from a blank page is still the harder, less reliable half.** Critique is closer to the "dissolved" side of the wall than the original caveat suggested; origination of best-in-class original work is still the part worth double-checking with an actual eye for it, human or otherwise.

## The practical takeaway

Don't ask "does this look good." Ask "check this against tiny fonts, buried help, missing onboarding, weak hero, dead-end empty states, non-obvious controls, inconsistent spacing, and missing loading/error states" — the specificity is what turns a vague aesthetic opinion into a checklist an agent reliably executes, the same way [fix-the-gate-you-find.md](fix-the-gate-you-find.md) and the bugbear docs work better as concrete checks than as "is this quality code" vibes.
