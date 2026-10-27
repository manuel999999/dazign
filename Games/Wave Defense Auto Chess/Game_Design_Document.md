# Wave Defense Auto Chess (working title)
### Game Design Document — v0.2 (Run structure, merging, synergies and fence decided; numbers TBD)

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
3. Surviving the wave earns coins. Commander EXP is gained automatically each wave (and can be bought with coins). Kills fill the kill gauge, and a full gauge gives a buff pick.
4. After the wave, unspent coins earn a bonus: **bonus = saved coins ÷ x** (x TBD; see Key Mechanics).
5. The shop offers a selection of heroes. Buy, reroll with coins, or lock the selection to buy later.
6. Place or rearrange heroes on the grid, optionally upgrade the fence, then start the next wave.

## Key Mechanics
- **Base grid:** The base area at the bottom of the screen is a grid where heroes are placed. Grid size **TBD**.
- **Fence repair:** The fence doesn't heal on its own. Repairing it costs coins, so repair competes with buying heroes and saving for the bonus.
- **Fence + base HP:** The fence protects the base. It has HP and can be upgraded. Behind it is a separate **base HP** (like player HP in TFT). Once the fence breaks, enemies that get through damage base HP, and the run ends when base HP reaches 0. **TBD:** how much does a repair cost, and is it per HP or a full repair? Does base HP ever recover? What do fence upgrades add (HP, armor, thorns)? Do enemies deal different base damage (e.g. bosses deal more)?
- **Coins per wave:** A flat base income each wave. **TBD:** the amount.
- **Commander level (auto chess standard):** Commander level works like TFT / Magic Chess. You gain EXP automatically each wave and can buy more EXP with coins. Higher levels add hero slots on the grid and improve shop odds for rarer heroes. **TBD:** passive EXP per wave, EXP cost per coin, the EXP curve, max level, slots per level, and shop odds per level.
- **Kill gauge (buff pick):** Each monster eliminated fills a gauge. When it's full, you earn a buff pick (*Suggested:* choose 1 of 3).
  - **Banked until the wave ends:** Picks aren't made mid-wave. Combat keeps running, and earned picks are taken after the wave, during the shop phase.
  - **Overflow carries over:** Progress past full isn't lost. The gauge keeps filling toward the next pick.
  - **Growing cost:** Like levels, each fill takes more kills than the last.
  - **TBD:** the starting size and growth curve, the buff list, whether buffs last the whole run, and how multiple picks earned in one wave are shown (*Suggested:* take them one after another).
- **Per-hero EXP (TBD, kept as a possible addition):** Heroes could also gain their own EXP from kills and level up individually. Open question: how that works with 3-star merging (what happens to EXP when copies merge?).
- **Saving bonus (interest):** Coins left after a round earn a bonus of saved coins ÷ x. **TBD:** the value of x, and whether there's a cap (TFT caps interest at 5 per round so hoarding doesn't snowball forever).
- **Hero shop:** Each roll shows **3 heroes**. The number of shop slots can be upgraded with coins. **TBD:** the max slots, the upgrade costs, hero tiers/rarity, and shop odds by wave.
- **Reroll:** Spend coins to refresh the selection. **TBD:** reroll cost, flat or increasing.
- **Lock:** Lock the current selection so it carries over to the next round, for when you can't afford it yet.
- **Hero merging:** 3 copies of the same hero merge into a stronger version: 1★ → 2★ → 3★. **TBD:** do merges happen automatically on purchase?
- **Bench:** A small bench holds heroes that aren't on the grid (e.g. for collecting copies). Copies on the bench count toward merges. **TBD:** bench size (e.g. 5-8 slots).
- **Synergies (classes + factions):** Each hero has a class and a faction, as in TFT. Fielding enough heroes of the same class or faction activates bonuses. **TBD:** the list of classes and factions, the breakpoints (e.g. 2/4/6), and whether synergies count unique heroes only.

## Progression & Structure
- **Run structure:** A run is a fixed number of waves ending with a final boss. Win by beating the boss. **TBD:** wave count (e.g. 20-30), and whether there are mini-bosses along the way.

Still TBD:
- Is there meta-progression between runs (unlock heroes, permanent upgrades) or is every run fresh?
- Difficulty levels or alternate maps after the first win?

## Narrative Arc / Social Design
**TBD.** Probably light or none. Questions: single-player only? Leaderboards for highest wave?

## Art Direction
**TBD.** Must keep heroes and enemies readable on a small portrait screen during busy waves.

## Audio Direction
**TBD.**

## Scope Notes
- Systems-heavy rather than content-heavy. The main work is balancing the economy, hero roster and wave curve.
- **Vertical slice (suggested):** 1 base grid, fence + base HP with 1 fence upgrade, 8-10 heroes covering 2-3 classes and 2-3 factions, 3-star merging, shop with reroll/lock, interest bonus, 10 waves ending in a boss.
- Team size and timeline **TBD**.

## Risks & Open Questions
- Coin economy balance: the interest divisor x decides whether saving dominates spending. It needs a spreadsheet model early.
- Classes + factions is the most content-heavy synergy option: every new hero must fit both systems and stay balanced. Start small (e.g. 3 classes, 3 factions).
- Readability of auto combat on a small screen.
- Kill gauge snowball: a strong board kills more and gets more buffs. Keep buffs moderate (choice-adding perks over raw power).
- Coins now go to heroes, rerolls, shop slots, fence repair, commander EXP, and saving for the bonus. The economy spreadsheet is essential early.
- Commander level, the kill gauge, synergies and merging together make a lot of systems for a small team. The vertical slice might start without the kill gauge and add it later.
- The design isn't complete yet. More mechanics are to be discussed.

## Next Steps
- Discuss the remaining open questions (numbers, buff list, theme, classes/factions, meta-progression).
- Model the coin, interest and reroll economy in a spreadsheet for about 20 waves.
- Grey-box prototype: grid placement, one wave spawner, fence HP, shop UI.
