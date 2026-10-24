# Puddle Pals
### Game Design Document — v0.1 (Concept)

## Logline
An idle clicker where you squish, feed, and multiply an ever-growing pile of adorable slime monsters into a thriving, jiggly slime kingdom.

## Genre & Platform
- **Genre:** Idle / incremental clicker
- **Perspective:** 2D, single fixed screen (the "slime pit") with zoom-outs as the kingdom grows
- **Platform:** Mobile (iOS/Android) first, browser/Steam idle-game port feasible
- **Comparable titles:** *Cookie Clicker*, *AdVenture Capitalist*, *Slime Rancher* (tone/creature design reference only, not mechanics)

## Core Pillars
1. **Squish feels good** — every click has satisfying, squishy juice (sound, wobble, particle) — the core action must never get old.
2. **Cute over clever** — no dark twist, no takeover plot; charm and collection are the whole appeal.
3. **Always another slime to meet** — the core incremental hook is "what does the next slime look like," not just "what does the next number look like."

## Premise
You've found a single lonely slime in a puddle behind your house. Click it, feed it, and it multiplies. Soon your yard, then your town, then the whole map is home to a growing family of slimes in every color, shape, and personality — each one just wants pats and snacks.

## Core Gameplay Loop
1. Tap the slime on screen to generate Goo (the core currency).
2. Spend Goo on Feeders (auto-clickers) that generate Goo passively — snack stands, sprinkler bots, lullaby speakers, etc.
3. Goo milestones unlock new slime types, which join the pit visually and each add a small passive bonus or quirk.
4. Periodic "Squish Events" (a slime bounces across the screen, a rain of snacks falls) give bonus taps for active engagement.
5. Prestige loop: once a pit is "full," reset into a new Biome (meadow → beach → volcano → candy land) that keeps a permanent multiplier and unlocks new slime types exclusive to that biome.

## Key Mechanics
- **Squish (tap):** Primary input; each tap has satisfying jiggle animation + escalating combo sound as you tap in rhythm.
- **Feeders:** Idle-clicker staple auto-generators, themed as slime caretakers (butterfly that tickles slimes, sprinkler that waters them) rather than generic factories.
- **Slime Collection (Slimedex):** Each new slime type is a collectible entry with a name, a one-line personality blurb, and a passive bonus — this is the long-term completionist hook.
- **Biome Prestige:** Soft-reset mechanic reframed as "moving the slime family to a new home," avoiding the usual clicker prestige feeling like a punishing restart.
- **Pet & Pat (idle-friendly bonus):** Tapping individual slimes (not just the main pit) occasionally triggers a cute reaction and a small bonus — rewards players who linger rather than just walking away.

## Progression & Structure
- 4-5 Biomes, each with its own 15-20 slime Slimedex page, palette, and Feeder set.
- Early game is fast and generous (dopamine-forward onboarding); later biomes slow the curve and lean on the collection/completionist hook to sustain interest.
- No hard paywalls; optional cosmetic slime "outfits" as monetization (hats, bows) rather than pay-to-progress.

## Social / Cozy Design
- No combat, no fail state, no urgency — designed for short, relaxing sessions (commute, waiting room) as much as long idle-checking sessions.
- Optional (post-launch) "visit a friend's pit" feature — see and pat a friend's slimes, no competitive element, purely social warmth.

## Art Direction
Bright, rounded, candy-colored palette; every slime is a simple blob silhouette differentiated by color, pattern, and a couple of accessory pixels (a bow, a leaf hat, tiny wings) so the art scope per-slime stays small while variety stays high.

## Audio Direction
Soft, bouncy, marimba/xylophone-driven score; the squish SFX is the hero sound and should have several layered variations so repeated tapping doesn't become audibly monotonous. Each slime type gets a tiny unique "voice" blip (boop/squeak) for personality.

## Scope Notes
- Very solo/small-team friendly: idle-clicker mechanics are systems-light, and art scope is controlled via the blob+accessory approach.
- Realistic for 1-2 people over 4-8 months for a launch-ready mobile version with 1-2 biomes, expanding post-launch.
- Biggest cost center is number/economy tuning (Feeder costs, Goo curves) and juice polish (animation/SFX feel), not raw content volume.

## Risks & Open Questions
- Risk: idle-clicker market is crowded — charm/collection hook needs to be genuinely strong to stand out, not just "cute skin on a known formula."
- Risk: monetization without hard paywalls needs a viable ad/cosmetic revenue model — worth prototyping early.
- Open question: how much passive (offline) progress to grant, and how to message it without feeling exploitative.
- Open question: whether social/visiting features are worth the backend cost for a v1, or purely a later addition.

## Next Steps
- Prototype the core Squish loop (tap → Goo → first Feeder) with placeholder art to validate "does tapping feel good."
- Design the first Biome's full Slimedex (15-20 slimes) to test if collection variety is compelling on paper.
- Rough out the Goo/Feeder cost curve in a spreadsheet before building any UI, to catch pacing problems early.
