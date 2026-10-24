# Maze Tower Defense (working title)
### Game Design Document — v0.1 (Notes captured, most details TBD)

## Logline
*Draft:* Build your own maze out of heroes on an open grid. Enemies always need a path through, so the skill is making that path as long and deadly as possible.

## Genre & Platform
- **Genre:** Mazing tower defense
- **Perspective:** 2D top-down grid, portrait
- **Platform:** Mobile (iOS/Android), portrait
- **Comparable titles:** *Tropical Tower Wars* (Warcraft III custom map, main reference, but this is single-player), *Desktop Tower Defense*, *Green TD*-style mazing maps

## Core Pillars
- **TBD.** *Suggested starting point:* "The maze is the player's creation": no fixed paths. Every level's best layout is discovered by the player.

## Premise
**TBD.**

## Core Gameplay Loop
1. A level opens with a grid map, possibly with random stones or obstacles.
2. Place heroes (4×4 cells each) anywhere on the grid. You must always leave at least a 1×1 path from enemy entrance to exit.
3. Enemies walk the shortest available path through your maze while heroes attack them.
4. Between waves, extend or adjust the maze. **TBD:** can you sell or move heroes?
5. Clear all waves to beat the level.

## Key Mechanics
- **Fine grid, big heroes:** The map is a grid of small squares. Each hero takes 4×4 cells, so placement offsets of 1 cell matter for tight mazing.
- **Path rule:** Placement must always leave a 1×1 pathway for enemies. Blocking is never allowed. **TBD:** show the live path preview while placing?
- **Obstacles:** Some levels have random stones or obstacles that hinder building. Skilled players can use them as part of their maze.
- **Practice area:** A sandbox where players can build a maze and save it as a quick guide for a level, to plan before playing for real. **TBD:** can saved guides be shown as a ghost overlay in the real level?
- **Heroes:** **TBD.** Roster, attack types (single target, splash, slow), upgrades, cost.
- **Economy:** **TBD.** Gold per kill or per wave, interest?

## Progression & Structure
**TBD.** Questions: how many levels? Star ratings? Unlocking new heroes? Do random obstacles mean a level changes each attempt, or is it fixed per level?

## Narrative Arc / Social Design
Single-player. **TBD:** sharing maze guides with other players later?

## Art Direction
**TBD.** Grid and path must be very readable on a phone screen. The tap precision of 4×4 placement on small cells is a key UX concern.

## Audio Direction
**TBD.**

## Scope Notes
- The core tech is grid placement plus pathfinding that recalculates and validates instantly on each placement. Build that first.
- **Suggested vertical slice:** 1 level with obstacles, 4 hero types, 10 waves, the practice area with save/load of one guide.
- Team size and timeline **TBD**.

## Risks & Open Questions
- **Touch precision:** placing 4×4 heroes on a fine grid with a finger needs a good drag/snap/preview UX.
- **Random obstacles vs. guides:** if obstacles are random, a saved practice guide may not fit. How do these two features work together?
- Balancing open mazing so there's no single "solved" layout.
- More details are to be decided.

## Next Steps
- Discuss: hero roster, economy, random vs. fixed obstacles.
- Prototype grid, 4×4 placement and the path-must-exist check with live path preview, tested on a real phone.
- Prototype the practice area save/load.
