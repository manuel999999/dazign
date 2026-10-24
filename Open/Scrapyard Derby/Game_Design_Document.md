# Scrapyard Derby
### Game Design Document — v0.1 (Concept)

## Logline
A chaotic 4-8 player party game where you build your vehicle out of scavenged junk mid-race, and it falls apart exactly as fast as you'd expect.

## Genre & Platform
- **Genre:** Multiplayer party / physics-based vehicle combat
- **Perspective:** Third-person chase camera
- **Platform:** PC + consoles, local and online co-op/versus (couch-party first, online as stretch goal)
- **Comparable titles:** *Rocket League* (pick-up-and-play physics), *Trailmakers* (build-your-vehicle), *Fall Guys* (party chaos and elimination format)

## Core Pillars
1. **Build is the game, not the menu** — vehicle construction happens live, on track, under time pressure — never in a pre-race garage screen.
2. **Falling apart is funny, not frustrating** — physics failures are readable, replayable, and shareable (clip-worthy), never a silent "you lose."
3. **Every match tells a different story** — procedurally scattered scrap + destructible tracks mean no two races assemble the same vehicles.

## Premise
Set in a junkyard demolition league on a scrapped-out industrial moon, drivers start each race with a bare chassis and a wrench. Scrap parts (wheels, plating, boosters, weapons) are scattered across the track itself — you drive over them to grab and instantly bolt them on while still moving. The track is part obstacle course, part hardware store.

## Core Gameplay Loop
1. Race starts — every player has an identical bare chassis (frame + 1 wheel set, no armor).
2. Track is littered with scrap pickups; driving through one auto-attaches it to an open slot (front/back/left/right/top).
3. Parts have tradeoffs: armor slows you but blocks hits; boosters speed you up but are fragile; weapons (bumpers, spikes, flamethrowers) let you wreck opponents but weigh you down.
4. Collisions and track hazards can knock parts OFF — they become pickups again for anyone, including you.
5. Race to the finish across 3 laps, or last-vehicle-standing in Demolition mode.
6. End-of-race highlight reel auto-generated from the match's biggest wrecks (shareable clip).

## Key Mechanics
- **Live-Attach:** Driving over scrap within ~1s of contact auto-mounts it to the nearest open slot — no menu, no pause, teaches itself through play.
- **Slot System:** 4 slots per vehicle (front/back/left/right), each accepts different part categories, creating build variety (glass-cannon vs. tank vs. speedster).
- **Knockoff Physics:** Hits above a force threshold detach parts, which fly off and become live pickups again — creates constant risk/reward around aggression.
- **Comeback Scrap:** Last-place drivers spawn extra high-tier scrap nearby, keeping races close without invisible rubber-banding.
- **Modes:** Circuit Race (laps), Demolition (last one moving), King of the Scrapheap (control-point capture with vehicles).

## Progression & Structure
- No permanent unlocks that affect power — cosmetic-only progression (paint jobs, chassis skins, victory horns) to keep matches fair and pick-up-and-play friendly.
- Season-based track rotation (junkyard, frozen scrapfield, flooded dock) to keep scrap layouts fresh.

## Social / Party Design
- Drop-in/drop-out local multiplayer, split-screen up to 4, online up to 8.
- Spectator "wrench cam" for eliminated players to remotely troll opponents (temporarily jam a rival's part, minor comedic sabotage) so no one just watches a black screen.

## Art Direction
Bright, chunky, toy-like proportions (oversized wheels, exaggerated parts) so vehicle silhouettes read instantly even in split-screen chaos. High-contrast part colors so players can tell what they're driving over at a glance.

## Audio Direction
Percussive, junkyard-industrial soundtrack that layers in intensity as more parts attach; heavy, satisfying "clunk/bolt" SFX for attach and a distinct "boing/clatter" for detach so players feel build state through sound alone.

## Scope Notes
- Higher scope than a solo project — needs dedicated physics/netcode engineering; realistic for a small studio (6-12 people) over 18-24 months, or a smaller vertical slice (1 mode, 1 track, local only) achievable by a 3-4 person team in 4-6 months.
- Vertical slice priority: prove Live-Attach + Knockoff Physics feel good before building additional modes/tracks.

## Risks & Open Questions
- Risk: physics-based multiplayer is notoriously hard to net-code well; local-first launch de-risks this.
- Risk: balance between "chaotic fun" and "readable/fair" — needs heavy playtesting on force thresholds for knockoff.
- Open question: monetization model (one-time purchase vs. cosmetic-only live-service).

## Next Steps
- Prototype Live-Attach + Knockoff Physics in a gray-box test track (single mechanic validation).
- Playtest with 4 players locally to check if part-scavenging creates the intended risk/reward tension.
- Scope a 1-track, 1-mode vertical slice for a funding/pitch demo.
