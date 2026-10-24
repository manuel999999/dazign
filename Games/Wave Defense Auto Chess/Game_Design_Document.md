# Wave Defense Auto Chess (working title)
### Game Design Document — v0.1 (Notes captured, most details TBD)

## Logline
*Draft:* Defend a fenced base at the bottom of the screen against waves of enemies by buying, placing and upgrading heroes auto-chess style, where saving your coins pays interest.

## Genre & Platform
- **Genre:** Wave defense / auto battler (auto chess economy)
- **Perspective:** 2D or 2.5D top-down, fixed portrait screen; enemies come from the top, base at the bottom
- **Platform:** Mobile (iOS/Android), portrait
- **Comparable titles:** *Teamfight Tactics*, *Auto Chess* (shop, reroll, interest economy); *Rush Royale*, *Random Dice* (portrait mobile defense)

## Core Pillars
- **TBD.** *Suggested starting point:* "Economy is a decision": saving and spending should both feel valid every round.
- Questions: what's the one feeling this game must deliver? Tension of holding the fence? Big combo builds?

## Premise
**TBD.** Setting, theme and who's attacking the base aren't decided yet.

## Core Gameplay Loop
1. At the start, pick a starting hero and place it on the base grid.
2. A wave starts. Heroes fight automatically and enemies attack the fence.
3. Surviving the wave earns coins.
4. After the wave, unspent coins earn a bonus: **bonus = saved coins ÷ x** (x TBD; see Key Mechanics).
5. The shop offers a selection of heroes. Buy, reroll with coins, or lock the selection to buy later.
6. Place or rearrange heroes on the grid, optionally upgrade the fence, then start the next wave.

## Key Mechanics
- **Base grid:** The base area at the bottom of the screen is a grid where heroes are placed. Grid size **TBD**.
- **Fence:** The fence protects the base. It has HP and can be upgraded. **TBD:** does the fence heal between waves? What do upgrades add (HP, armor, thorns)? Is it game over when the fence breaks?
- **Coins per wave:** Coins are earned each wave. **TBD:** a flat amount, or scaling with wave number, kills or performance?
- **Saving bonus (interest):** Coins left after a round earn a bonus of saved coins ÷ x. **TBD:** the value of x, and whether there's a cap (TFT caps interest at 5 per round so hoarding doesn't snowball forever).
- **Hero shop:** Each round shows a selection of heroes. **TBD:** how many slots, hero tiers/rarity, and shop odds by wave.
- **Reroll:** Spend coins to refresh the selection. **TBD:** reroll cost, flat or increasing.
- **Lock:** Lock the current selection so it carries over to the next round, for when you can't afford it yet.
- **Hero upgrades/merging:** **TBD.** Combining 3 copies into a stronger hero is the auto chess standard. Is that in?
- **Synergies/traits:** **TBD.** Do heroes share classes or factions that give bonuses when grouped?

## Progression & Structure
**TBD.** Questions:
- Is a run endless waves (high-score) or a fixed number of waves with a boss?
- Is there meta-progression between runs (unlock heroes, permanent upgrades) or is every run fresh?
- Stages/levels, or one endless mode?

## Narrative Arc / Social Design
**TBD.** Probably light or none. Questions: single-player only? Leaderboards for highest wave?

## Art Direction
**TBD.** Must keep heroes and enemies readable on a small portrait screen during busy waves.

## Audio Direction
**TBD.**

## Scope Notes
- Systems-heavy rather than content-heavy. The main work is balancing the economy, hero roster and wave curve.
- **Vertical slice (suggested):** 1 base grid, fence with 1 upgrade, 6-8 heroes, shop with reroll/lock, interest bonus, 10 waves.
- Team size and timeline **TBD**.

## Risks & Open Questions
- Coin economy balance: the interest divisor x decides whether saving dominates spending. It needs a spreadsheet model early.
- Auto-chess games usually depend on synergies to stay interesting. Without them, builds may feel samey.
- Readability of auto combat on a small screen.
- The design isn't complete yet. More mechanics are to be discussed.

## Next Steps
- Discuss the open questions above (fence, merging, synergies, run structure).
- Model the coin, interest and reroll economy in a spreadsheet for about 20 waves.
- Grey-box prototype: grid placement, one wave spawner, fence HP, shop UI.
