# Getting GitHub stars and traction without turning into a hype account

**Dated:** 2026-09-15

Nobody tells you this part: shipping the tool is maybe 40% of the work. The other 60% is "does anyone find out it exists," and most solo devs are bad at this on purpose, because the alternative — sounding like a growth-hacker — feels worse than obscurity. Fair. But there's a middle ground between silence and "🚀🔥 GAME CHANGER dropped, RT if you're not ready 🔥🚀".

## What actually works, in order of how little it costs your dignity

1. **Answer real questions where they already happen.** Reddit threads, forum posts, Discord servers where someone is stuck on the exact problem your tool solves. Reply like a person solving their problem, mention your tool once, don't lead with it.
2. **Honest release notes.** No superlatives, no "revolutionary," just what changed and why someone would care. People trust boring changelogs more than they trust hype — boring reads as "this person is telling the truth."
3. **A demo that shows the thing working**, not a slide deck about the thing. See the demo-video note in this repo.
4. **Show up consistently, not in bursts.** A GitHub repo that gets a burst of README polish once a quarter reads as abandoned between bursts. Small, frequent, real commits beat a big splashy relaunch.

## The pattern, automated (with the obvious caveat)

I run a private internal tool (`fleet-public-relations-mcp`, not published — it's tuned to my own repo fleet and isn't something you can `pip install`) that does the boring parts of step 1 and 2 for me: monitors registered forum/Reddit threads, scores incoming discussion for whether someone there is a good-faith technical question worth answering, drafts a reply for me to review, and has a **tone linter that bans hype words** before anything goes out. Nothing posts without my explicit approval — the tool drafts, I gate.

That last part — a hype-word linter that runs on your own drafts before you hit send — is the piece worth stealing even if you never automate anything else. Write your own release note or forum reply, then grep it for "revolutionary," "game-changing," "10x," "insane," and cut every one you find. You'll sound more credible immediately, for free, with no tooling at all.

## What doesn't work

- Posting your own tool into threads where nobody asked. It reads as spam because it is spam, structurally, regardless of your intent.
- Vanity metrics theater (star-count screenshots, "X users and counting" with no context). Nobody's first star came from seeing someone else's star count.
- Cross-posting the identical announcement to five platforms simultaneously. Different communities can tell, and it reads as broadcast, not participation.
