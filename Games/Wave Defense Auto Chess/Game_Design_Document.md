# Wave Defense Auto Chess (working title)
### Game Design Document — v0.3 (Run structure, merging, synergies, fence and meta-progression decided; numbers TBD)

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
**Theme: fantasy frontier, cute/chibi tone.** A walled frontier outpost holds back monster hordes coming down from the wilds. Heroes are fantasy adventurers (knights, mages, rangers and the like).

*Draft:* the base is a small frontier village at the bottom of the screen, the fence is its wooden-and-stone palisade, and each run is one siege ending with a horde boss. **TBD:** who leads the horde, why it attacks, and whether there's any story at all.

## Core Gameplay Loop
1. At the start, pick a starting hero (**choose 1 of 3** tier-1 heroes; the number offered is TBD) and place it on the base grid. **Decided (2026-10-28): the starting heroes offered all deal damage** (no Supports, and no Trapper whose traps only hold enemies), and **a wave can't start without a hero on the board that deals damage**, so the board can always win a wave. Stage 1's races have only two such tier-1 heroes (Leaf Archer, Shield Knight), so it offers 1 of 2 (decided 2026-10-28: fine, since decks will widen the choice later).
2. A wave starts. Heroes fight automatically and enemies attack the fence.
3. Surviving the wave earns coins. Commander EXP is gained automatically each wave (and can be bought with coins). Kills fill the kill gauge, and a full gauge gives a buff pick.
4. After the wave, unspent coins earn a bonus: **bonus = saved coins ÷ x** (x TBD; see Key Mechanics).
5. The shop offers a selection of heroes. Buy, reroll with coins, or lock the selection to buy later.
6. Place or rearrange heroes on the grid, optionally upgrade the fence, then start the next wave.

## Key Mechanics
- **Base grid:** The base area at the bottom of the screen is a grid where heroes are placed: **5 columns × 3 rows**.
- **Outside row:** **One** grid row (5 cells) in front of the fence, out on the battlefield. Heroes placed there slow down attackers and attack them freely, but they're exposed: some attackers have damage auras (or similar), and some bosses can attack them. Melee heroes hold enemies up with skills that **stun or slow**, and they deal **cleave** (or similar area) attacks. **Enemies stop to fight heroes in their range (decided 2026-10-27):** an enemy that attacks heroes and has one in range stands still and fights it, without walking or hitting the fence, until the hero is knocked out or leaves its range. Then it walks on. Enemies that don't attack heroes (*Draft:* Goblin Scamp, Troll Rammer) walk past. **TBD:** each enemy's hero damage, range and attack speed (placeholders: Imp 4 dmg / short range, Orc Bruiser 12 / melee, Bog Shaman 6 / long range, Goblin King 45 / long range).
- **Spawn area and wave preview (decided 2026-10-27):** The field extends above the lane into a **spawn area**. Each wave lines up there in a **formation arranged automatically by role**: tanks in front, then fighters, with casters and bosses at the back. **During the shop phase, the next wave's whole formation is shown there as a spoiler**, so the player can plan where to place heroes. A **Scout** button on the action bar moves the camera up to look at it, and pressing it again comes back. When the wave starts, enemies still arrive over time; each appears at its own spot in the formation when its time comes. **Scattered spots (user, 2026-10-29):** the neat rows looked like a parade, so each rank now stands at random spots within its band (front rank still nearest the lane); the spots are fixed per wave, so the preview shows exactly where they appear. *Suggested (built this way as a placeholder):* rows of up to 6, and the spawn area is 2.5 cells tall. During a wave, the battle view shows the front of the spawn area, and more of it on taller phones.
- **Placement:** Any hero can be placed anywhere, inside the wall or outside. The rules are the same for all heroes, and every hero counts toward the same commander-level hero cap. Melee heroes are built for outside; ranged heroes outside are possible but exposed.
- **Heroes move on their own during a wave (auto chess style; decided 2026-10-27).** The cell where a hero is placed is its starting post. When no enemy is in range, a hero walks to get one in range, then stops and attacks.
  - **Melee heroes** close in for close combat (hit, slow, stun, cleave), and **can walk out through the fence**, even from inside the wall.
  - **Ranged heroes** (and every non-melee attacker) reposition to get a shot, but **stay on the side of the fence where they were placed**: placed inside, they move only within the inside grid; placed outside, only in the outside area.
  - **Enemy territory (decided 2026-10-28, replacing "the outside area is the whole field"):** the top part of the lane belongs to the enemies, and heroes can't walk into it. Melee heroes chased enemies so far up the lane that the ranged heroes inside the wall couldn't reach the fight. Now they wait at its edge, and fights happen where everyone can hit. The edge is drawn on the field. **Decided (2026-10-28):** a smaller territory with **longer ranges** for ranged classes, so outside heroes get room and the fight stays in reach. Ranged heroes placed outside can follow the fight further, at the risk of being exposed. *Suggested (built as placeholders):* the top 3 cells of the lane are enemy territory; ranges are Ranger 1600, Mage 1400, Trapper 1300 (were 1000 / 800 / 700; the user asked for more range, balance later). Rangers and Mages reach the edge fights from every inside row, Trappers from the front two; a front-row Ranger covers the whole lane. **TBD:** each hero's walking speed (placeholder: 240 px/s for every hero).
  - Enemies that attack heroes stop to fight one in their range (see **Outside row**).
  - Any hero standing outside the fence, whether it was placed there or walked out, is exposed to auras and boss attacks.
  - *Suggested (built this way as placeholders):* a hero chases the nearest enemy it can get in range of from its area, and walks back to its post when nothing is reachable. Every hero is back on its post when the wave ends. Supports don't attack, so they don't move. The Support speed aura still counts the 8 cells around where heroes were *placed*. Heroes push apart so they don't stack on one spot.
- **Knockout:** A hero knocked out outside is out for the rest of the wave and returns automatically next wave (TFT-style).
  - **A wave could stall forever (found 2026-10-28).** If every hero that can hurt an enemy is knocked out, and the enemy is fighting a hero it can't kill (e.g. a Chapel Cleric that heals itself faster than an Imp hurts it), nobody wins and the wave never ends. Knock-backs and chained roots or stuns can also hold a slow, armored boss in place for a very long time, and two fence-repairing Supports can out-heal weak enemies that nothing on the board can kill. **Decided (2026-10-28): overtime.** A while after a wave's last enemy appears, the remaining enemies enrage: they stop fighting heroes, walk faster, and hit the fence and base harder the longer overtime lasts. A warning shows on the wave bar and enraged enemies glow red. *Suggested (placeholders):* overtime starts 45 s after the last enemy appears; enraged enemies walk 1.5x as fast and their fence and base damage grows by +5% of normal per second of overtime (double after 20 s). *Suggested, switched off:* enraged enemies could also shrug off stuns, roots, slows, knock-backs and pulls (one switch in the game). A test bot then lost almost every run on stages 2–4, and overtime ended every stall without it. Auras still burn heroes. Built 2026-10-28. (Other options were a hard time limit, enemies giving up a fight, or Supports that can't heal themselves.)
  - **Decided (2026-10-27):** only heroes standing outside the fence can be hurt while the fence stands. **Once the fence is broken, heroes inside can be hurt too.**
  - *Suggested (built this way as a placeholder):* Every hero starts each wave at full HP, and HP grows with stars. Damage auras (Bog Shaman) hurt exposed heroes near them, and enemies that attack heroes hit the nearest exposed hero in range. Stunned enemies do neither. **TBD:** hero HP values and the aura numbers.
- **Fence protection (four sources):** (1) **fence upgrades** bought with coins (*Suggested* tracks: max HP, armor, thorns); (2) a **Guardian class bonus** (*Suggested:* 2 Guardians: fence gains armor); (3) the **Support class bonus** (stronger heals and fence repairs) and the Tinker's repairs; (4) some **kill gauge buffs** that repair or strengthen the fence. (Until 2026-11-09 the Ironhold race bonus was a repair bonus too; it is now an ability-charge bonus, see **Synergies**, so Guardian and Support are the fence synergies.)
- **Fence repair:** The fence doesn't heal on its own. Repairing it costs coins, so repair competes with buying heroes and saving for the bonus. **Repair works in chunks:** each purchase restores a fixed amount of HP for a fixed cost, and can be bought again. **TBD:** the amount and the cost.
- **Vertical-slice fence upgrade: max HP.** Each purchase raises the fence's max HP (and its current HP by the same amount). **TBD:** the amount, the costs and the number of purchases. Armor and thorns stay as possible later tracks.
- **Fence + base HP:** The fence protects the base. It has HP and can be upgraded. Behind it is a separate **base HP** (like player HP in TFT). Once the fence breaks, enemies that get through damage base HP, and the run ends when base HP reaches 0. **TBD:** how much does a repair cost, and is it per HP or a full repair? Does base HP ever recover? What do fence upgrades add (HP, armor, thorns)? Do enemies deal different base damage (e.g. bosses deal more)?
- **Coins per wave:** A flat base income each wave. **TBD:** the amount.
- **Commander level (auto chess standard):** Commander level works like TFT / Magic Chess. You gain EXP automatically each wave and can buy more EXP with coins. Higher levels add hero slots on the grid and improve shop odds for rarer heroes. **TBD:** passive EXP per wave, EXP cost per coin, the EXP curve, max level, slots per level, and shop odds per level.
- **Kill gauge (buff pick):** Each monster eliminated fills a gauge. When it's full, you earn a buff pick (*Suggested:* choose 1 of 3).
  - **Banked until the wave ends:** Picks aren't made mid-wave. Combat keeps running, and earned picks are taken after the wave, during the shop phase.
  - **Overflow carries over:** Progress past full isn't lost. The gauge keeps filling toward the next pick.
  - **Growing cost:** Like levels, each fill takes more kills than the last.
  - **TBD:** the starting size and growth curve, the buff list, whether buffs last the whole run, and how multiple picks earned in one wave are shown (*Suggested:* take them one after another).
  - *Built as placeholders until those are discussed:* the first pick takes 10 kills and each later one 5 more; buffs last the whole run; several picks are taken one after another, choosing 1 of 3 each time. *Suggested* starter buff list (all values are placeholders):
    - **Sharpened Arms:** all heroes +10% damage.
    - **Quick Hands:** all heroes attack 10% faster.
    - **Keen Eyes:** all heroes +8% crit chance.
    - **Bigger Blasts:** splash and cleave +15% reach.
    - **Thick Planks:** fence armor +1.
    - **Reinforced Fence:** fence +60 max HP.
    - **Mason Crew:** free fence repair of 150 HP.
    - **War Chest:** +6 coins.
- **Per-hero EXP (TBD, kept as a possible addition):** Heroes could also gain their own EXP from kills and level up individually. Open question: how that works with 3-star merging (what happens to EXP when copies merge?).
- **Saving bonus (interest):** Coins left after a round earn a bonus of saved coins ÷ x. **TBD:** the value of x, and whether there's a cap (TFT caps interest at 5 per round so hoarding doesn't snowball forever).
- **Hero shop:** Each roll shows **3 heroes**. The number of shop slots can be upgraded with coins. **Heroes have 3 tiers** with different costs, and higher commander levels make higher tiers more likely in the shop. **TBD:** which hero is which tier, the costs, the odds per level, the max slots and the upgrade costs.
- **Selling:** Drag a hero onto the shop to sell it for coins. **TBD:** the refund (e.g. the full cost of every copy merged into it).
- **Reroll:** Spend coins to refresh the selection. **TBD:** reroll cost, flat or increasing.
- **Lock:** Lock the current selection so it carries over to the next round, for when you can't afford it yet.
- **Hero merging:** 3 copies of the same hero merge into a stronger version: 1★ → 2★ → 3★. **Merges happen automatically** the moment the third copy is bought, even when the bench is full.
- **Bench:** A small bench holds heroes that aren't on the grid (e.g. for collecting copies). Copies on the bench count toward merges. **TBD:** bench size (e.g. 5-8 slots).
- **Synergies (classes + factions):** Each hero has a class and a faction, as in TFT. Fielding enough heroes of the same class or faction activates bonuses. **Synergies count unique heroes on the board** (two copies of one hero count once; bench heroes don't count). **Breakpoints are 2 and 4** for every class and faction, on the 20-hero roster (they were 2 and 3 for the first 9 heroes).
  - **Roster: 5 classes × 4 factions = 20 heroes**, one per pair (decided). Hero names and abilities are *Draft*.
  - **Classes (what a hero does):** **Ranger** (long range, single target; good against fast enemies and bosses), **Mage** (area damage against groups, slower attacks), **Guardian** (melee: walks out to fight enemies up close, stuns or slows attackers with skills and hits groups with cleave attacks; takes hits from damage auras and bosses), **Support** (helps allies or the base instead of attacking), **Trapper** (roots and poisons enemies).
  - **Races (who a hero is):** **Kingdom** (humans), **Sylvan** (elves), **Ironhold** (dwarves), **Beastfolk** (animal folk; stronger the longer a wave lasts). Earlier versions of this doc called these "factions"; the code still does.
  - **Traits (decided 2026-10-28, TFT / Underlords / Magic Chess style):** every hero has **a race and a class**. **Some heroes also get a faction**: a small group of 3–4 heroes that crosses races, with a low breakpoint (2–3), like TFT's secondary traits. Factions are the hook for heroes added in later updates. **TBD:** the factions, their members and bonuses.
  - **Names and looks:** fine as placeholders for now; to be finalized later.
  - **The 11 newer heroes (*Draft*):**
    - **Kingdom:** Chapel Cleric (Support: heals hurt allies; its ability gives mana), Royal Snarer (Trapper).
    - **Sylvan:** Grove Singer (Support: mana to the 8 heroes around it), Thorn Weaver (Trapper).
    - **Ironhold:** Tinker (Support: repairs the fence during waves), Bomb Sapper (Trapper).
    - **Beastfolk:** Hawk Eye (Ranger: extra damage equal to a share of the target's max HP, against tanks and bosses), Owl Sage (Mage: splash that poisons), Bear Warden (Guardian: huge HP, cleave and root), Fox Merchant (Support: +2 coins after each wave), Badger Digger (Trapper).
  - **Bonuses (approved; the numbers are placeholders).** Class bonuses apply to heroes of that class, and race bonuses to heroes of that race:
    - **Ranger:** (2) +20% damage, (4) +45% damage.
    - **Mage:** (2) +25% splash size, (4) +50% splash size.
    - **Guardian:** (2) fence armor 1, (4) fence armor 2. Armor means less damage per enemy hit on the fence.
    - **Support:** (2) heals and repairs +40%, (4) +100%.
    - **Trapper:** (2) roots and poisons last +30%, (4) +70%.
    - **Kingdom:** (2) +15% attack speed, (4) +35% attack speed.
    - **Sylvan:** (2) 15% crit chance, (4) 30% crit chance. A crit deals double damage.
    - **Ironhold:** (2) abilities charge 25% faster, (4) 60% faster (every source: hits, hits taken, time, mana). **Changed 2026-11-09 (user's decision, Claude's proposal):** it was "repairs restore +50% / +100% HP", the only race bonus that did nothing during a wave, and it overlapped with the Support bonus, which already boosts fence repairs; an Ironhold-only board won 0–33% of runs against 50–75% for Kingdom. Numbers are placeholders.
    - **Beastfolk:** (2) +4%, (4) +8% attack speed for every 10 seconds the wave has lasted.
- **Hero abilities (decided 2026-10-28):** every hero has **one unique ability**, cast **automatically** (the AI aims it, e.g. at the biggest group). Stars scale abilities **the TFT way**: a 3★ ability is dramatically bigger, not just a little stronger. **Built in the game (2026-10-28)**, with placeholder numbers and visuals; the Guardians' on-hit stuns and slows moved into their abilities.
  - **Charge = hits (decided):** each ability's "cooldown" is a **number of hits**, its own per ability (e.g. 8 shots for one hero, 15 swings for another). Each basic attack fills the hero's ability bar by one step. Basic attacks don't give mana.
  - **Heroes that don't attack:** a Support's bar fills over time. Each small trap a Trapper places counts as a hit (decided).
  - **Getting hit also charges the bar, for Guardians only** (decided), so they cast their taunt or slam when it matters.
  - **Mana comes only from some Supports** (decided), so Supports become something to build around. Not every Support gives mana. Each mana Support gives mana **on its own cooldown**, to one target or an area depending on the hero.
  - **Copies of the same Support share one mana cooldown** (decided 2026-10-28): fielding two Grove Singers gives no more mana than one, only more reach. Different Support heroes do stack on the same target. The way to more mana is merging (stars), like synergies, which also ignore duplicates. This replaces the "mana sickness" idea (diminishing returns), which was dropped.
  - **The mana Supports (decided 2026-10-28):** **Grove Singer** (Sylvan) pulses mana to the 8 heroes around it, replacing its +15% attack-speed aura. **Chapel Cleric** (Kingdom) keeps its heals, and its ability, *Blessing*, gives a burst of mana to nearby heroes. The Tinker and Fox Merchant don't give mana.
  - **One bar (decided 2026-10-28):** mana adds extra steps to the same bar, like free hits, so mana always helps and each hero shows a single bar. It's easier to balance than two gates (a full hit bar *and* full mana), where only the slower of the two matters. The shared Support cooldown (below) keeps mana from stacking.
  - **TBD:** each hero's ability, hit count and mana cooldown.
- **Trappers (decided 2026-10-28):** ranged, and they **don't shoot**. Their basic attack is **placing a small trap** on the lane ahead of the enemies; their ability is a big signature trap. Traps sit on the ground until triggered or until they expire, which keeps them distinct from Mages (instant damage): Trappers decide *where* enemies die, Mages make them die there. Small traps differ per race; some deal damage, some only hinder. *Suggested:* a limit on how many small traps each Trapper has out at once, if the lane gets cluttered.

  | Trapper | Small trap (basic attack) | Signature trap (ability) |
  |---|---|---|
  | Royal Snarer (Kingdom) | **Snare:** holds the first enemy that steps on it briefly. No damage | **Net:** binds everything in an area |
  | Thorn Weaver (Sylvan) | **Thorn patch:** poisons anything walking through. No hindrance | **Thorn Bind:** roots an area, and the thorns poison |
  | Bomb Sapper (Ironhold) | **Mini mine:** a small blast. Damage only | **Vacuum Bomb:** pulls enemies into one spot (a set-up for Mages) |
  | Badger Digger (Beastfolk) | **Mud hole:** slows anything walking through. No damage | **Pit Trap:** enemies fall in and are out of action for a few seconds |

- **Supports stay as they are for now** (decided): they don't attack; each helps allies or the base.
- **Abilities for the other 14 heroes (approved by the user 2026-10-28; names and numbers are placeholders).** Charge is in hits, or seconds for Supports; all numbers are placeholders. The 3★ column shows the TFT-style jump.

  | Hero | Tier | Ability | What it does | Charge | At 3★ |
  |---|---|---|---|---|---|
  | **Rangers** | | | | | |
  | Leaf Archer (Sylvan) | 1 | **Volley** | Fires 3 arrows at 3 different enemies; each can crit | 6 hits | 8 arrows |
  | Cannoneer (Ironhold) | 2 | **Big Shot** | A cannonball rolls down the lane, hitting everything in a line and knocking it back | 8 hits | Fires 3 lines |
  | Crossbow Squire (Kingdom) | 3 | **Rapid Fire** | Attacks 3× faster for 4 s | 10 hits | 5× faster for 6 s, bolts pierce |
  | Hawk Eye (Beastfolk) | 2 | **Hunter's Mark** | The hawk dives on the enemy with the most HP: big % max-HP damage, and the target takes +25% damage from all heroes for 5 s | 10 hits | Marks the 3 biggest enemies |
  | **Mages** | | | | | |
  | Rune Smith (Ironhold) | 1 | **Spark Rune** | Lightning that bounces between 3 enemies | 6 hits | Bounces 8 times |
  | Hedge Wizard (Kingdom) | 2 | **Fireball** | A big blast on the largest group | 8 hits | A huge blast that leaves the ground burning |
  | Owl Sage (Beastfolk) | 1 | **Plague Feathers** | Rains feathers over a wide area, poisoning everything; the poison is stronger the longer the wave has lasted | 8 hits | Covers most of the lane |
  | Bloom Druid (Sylvan) | 3 | **Wild Bloom** | A giant flower erupts under the largest group: heavy damage and a brief stun | 10 hits | Three blooms |
  | **Guardians** (charge also when hit) | | | | | |
  | Shield Knight (Kingdom) | 1 | **Shield Bash** | Stuns its target and those around it for 1.5 s | 6 hits | 3 s, wider |
  | Sapling Treant (Sylvan) | 2 | **Taproot** | Roots itself and **taunts**: enemies nearby stop to attack it, even ones that usually walk past; it regenerates HP meanwhile | 8 hits | Taunts a huge area, heals much more |
  | Hammer Brawler (Ironhold) | 3 | **Earthshaker** | Slams the ground: heavy damage and a stun in a wide circle | 12 hits | Three slams in a row |
  | Bear Warden (Beastfolk) | 3 | **Rampage** | Charges up the lane, knocking enemies back toward the spawn and slowing them | 12 hits | Charges the whole lane |
  | **Supports** (charge over time) | | | | | |
  | Tinker (Ironhold) | 1 | **Patch Job** | Instantly repairs a chunk of the fence and gives it +2 armor for 5 s (on top of its steady repair) | 15 s | Big repair, +5 armor |
  | Fox Merchant (Beastfolk) | 2 | **Lucky Find** | Marks a random enemy; killing it drops bonus coins (on top of +2 coins per wave) | 12 s | Marks 3 enemies |

  New mechanics these need: **taunt** (forces even walk-past enemies to stop), **knock-back**, a **line** shot, **chain bounces**, **marks** (bonus damage, bonus coins), and **burning ground**.

## Progression & Structure
- **Run structure:** A run is a fixed number of waves ending with a final boss. Win by beating the boss. **Decided (2026-10-28):** the wave count **grows from stage to stage** (short early stages, full runs later), and every stage has a **mini-boss at its halfway wave**. **TBD:** the final counts (placeholders: 10 / 12 / 15 / 20 / 24).
- **Stages:** the game is a series of stages, each one run with its own waves and boss. Clearing a stage unlocks the next. **Decided (2026-10-28):** each stage has **its own boss and 1–2 signature enemies** with their own mechanic, and reuses enemies from earlier stages. **TBD:** how many stages, map look and rule twists, and whether there are difficulty levels after the last one.
  - *Built as placeholders (2026-10-28):* stages differ in their waves, enemies and the races in the shop (user's choice; map look and rule twists can come later). Stage stars and saving a run in progress come later.
  - *Draft* enemies per stage (names, mechanics and numbers are placeholders; the new art is Claude's drafts):

    | Stage | Races in the shop | Waves | Signature enemies | Mini-boss | Boss |
    |---|---|---|---|---|---|
    | Greenwood Road | Kingdom, Sylvan | 10 | the goblins: Imp, Goblin Scamp, Orc Bruiser (Bog Shaman late) | Orc Warchief (a big Orc that calls in Imps) | Goblin King (summons Scamps) |
    | Iron Pass | + Ironhold | 12 | **Shieldbearer** (armor: every hit deals a flat amount less, at least 1; poison ignores it), **Rock Slinger** (hits the fence from far up the lane) | Iron Sergeant (a big, heavily armored Shieldbearer) | Mountain Troll (armored, throws boulders at the fence from range) |
    | Wild Hills | + Beastfolk | 15 | **Moss Mender** (heals the enemies around it, not itself), **Tunnel Grub** (travels underground, where heroes, traps and spells can't reach it, and surfaces near the fence) | Elder Mender (a big Mender with a wide heal) | Briar Witch (heals, summons Grubs, damage aura) |
    | Goblin Keep | all four | 20 | **Goblin Sapper** (fast; blows up on reaching the fence for heavy damage) plus every enemy so far | Goblin King returns | Goblin Warlord (armored, summons Sappers, attacks heroes) |
    | Frozen Reach *(built 2026-11-09, Claude's proposal accepted; numbers Draft)* | all four | 24 | **Frost Wisp** (freezes the hero it reaches for a few seconds: no attacks, movement or casts, instead of hurting it), **Ice Golem** (heavy armor that sheds a point with every hit it takes, so focus fire strips it) plus every enemy so far | Glacier Golem (a big Ice Golem) | Frost Wyrm (summons Wisps, attacks heroes, and every few seconds breathes on every hero within its reach, inside the wall or not: the first threat to inside heroes while the fence stands) |

  - *Suggested (built as a placeholder):* enemy HP grows along each wave list (×1.05–1.58 at wave 1, +9–12% per wave), tuned with a scripted player so it wins roughly 75% / 70% / 65% / 60% of runs on the four stages. Mini-bosses reuse an enemy's art at a bigger size. **Fairness pass (2026-11-09, Claude's numbers, all still placeholders):** the goblins' base HP went up ×1.6 so an enemy is as tough in stage 4 as in stage 1 (before, stage 1 needed a far steeper curve than the others, so a stage-4 Orc had less HP than a stage-1 one); the four stage bosses lost a fifth of their HP because boss waves ran 100–190 s and took most of the losses; and the later stages start flatter and grow faster, so a run isn't lost on wave 3 to bad shop luck (Goblin Keep's wave 3 also lost an Orc Bruiser for the same reason: a wipe that early on a 20-wave stage feels unfair, and that is a wave-composition fix, not an HP one). Also: Owl Sage is tier 1 and Hawk Eye and Bomb Sapper tier 2 (every race now has two tier-1 heroes, two tier-2 and one tier-3, and four tier-1 heroes deal damage), the Sapling Treant has 420 HP and the Hammer Brawler 400 (tier-2/3 Guardians that taunt or fight up close were knocked out almost every wave at the Knight's 300), and the Tunnel Grub surfaces earlier and hits the fence for 3 (it did 56–77% of all fence damage on stages 3–4). Measured with the scripted player: a race-only board now wins 58% on its stages as Beastfolk (was 0–25%); Ironhold is still the weakest race (its bonus only improves repairs: **TBD** whether it should do something during the wave).
  - **Loss screen (built 2026-11-09, Claude's draft; mockup `15 Run end · loss` added afterwards, look not approved yet):** a lost run's window says how far it got ("Fell on wave 8 of 12"), which two enemies took most HP off the fence (as shares), which got through to the base (HP), and a **tip** about the enemy that hurt the base most: one or two sentences on what to try next (every enemy has one, *Draft* texts). The goal: a player who loses sees why and what to change.

### Meta-progression (decided: three systems)
What makes the player stronger between runs. Three systems, each a different kind of reward:

1. **Hero unlocks (decided):** clearing a stage adds new heroes to the shop pool. Early stages use a smaller pool, so synergies are learned a few at a time. **Unlock by race (decided for now):** e.g. stage 1 has Kingdom + Sylvan, then Ironhold, then Beastfolk; each unlock is a whole new synergy. **TBD:** the exact stages.
   - **Deck (later, not designed yet):** once there are more heroes than one run should use, the player picks a deck of heroes for the run's shop pool, with a **minimum per race**. New heroes in updates then become new choices instead of diluting the shop. **TBD:** deck size, the per-race minimum, tier rules, and default and saved decks. *Suggested:* a deck must hold at least 2 tier-1 heroes that deal damage, so the starting pick (damage dealers only) is never empty.
2. **Talent spin (decided):** permanent stat upgrades. A spin shows **3 random talents and the player picks 1** to level up. **Each spin costs more** than the last. Talents have rarity tiers (rarer ones show up less often) and a max level each. The permanent fence upgrades live here. Inspired by the talent spin in *Heroes vs Hordes*, but with our own list, sized for weeks of play, not an endless grind. **TBD:** the spin cost curve, the tier odds, and the max levels.
3. **Talent tree (decided):** deliberate choices for **synergies and quality of life**. Its nodes may also unlock commanders or relics picked before a run (the "starting perks" idea). **Decided (2026-11-08, Claude's recommendations accepted):** tree points are the player's **total stage stars**, which are never spent; a **reset is free** and gives every point back; **three branches** (Quality of Life, Synergies, Endgame); deeper nodes need the node before them; the tree is a SPIN | TREE toggle on the Talents tab. *Built with placeholders* (costs and values TBD).

**Keep in-run power central:** the spin's flat stat talents stay small (most of its value is in the fence, economy and conditional bonuses), so the shop, merges and synergies stay the main way to win.

**Decided (2026-10-28): a run currency pays for spins**, earned from every run (per wave cleared, plus a bonus for a win, so a loss pays less). *Built with placeholders:* called "gems", 3 per wave cleared, +30 for a win; spins cost 40, +20 for each spin after. **Decided (2026-10-28): stage stars, at most 3 per stage, also unlock bonus chests.** **Decided (2026-10-30):** the stars are ★ clear the stage, ★ clear it without the base losing any HP, ★ clear it without the fence ever breaking; every star needs a win, and stars add up across runs (each is kept the first time it is earned). Stars are never spent. Chests open at totals of stars across all stages and are claimed once; they hold **gems, free talent spins, or both** (a free spin doesn't raise the price of the next bought spin). *Built with placeholders:* chests at 3 / 6 / 9 / 12 stars: 40 gems; 1 free spin; 80 gems; 100 gems + 1 free spin. **TBD:** the currency's name and amounts, the chest totals and contents once there are more stages, and the tree's node costs.

*Draft:* talent spin list (all values TBD; **built 2026-10-28 as 19 placeholder talents**, with "damage to stunned / slowed / poisoned / rooted enemies" as one talent and "cheaper fence repairs" as more HP per repair):

| Tier | Talents |
|---|---|
| Common | Hero damage +%, hero HP +%, fence max HP, base HP, starting coins, wave income; *added 2026-11-09:* attack speed +%, saving bonus cap +1 |
| Great | Damage to stunned / slowed / poisoned / rooted enemies, splash radius, healing; *added:* ability bars fill faster, bosses drop coins, hero range +% |
| Rare | Crit chance, control duration, fence armor, cheaper fence repairs, kill gauge fills faster; *added:* the commander starts with EXP, crits deal more |
| Epic | Damage to bosses, rerolls cost 1 less, +1 bench slot; *added:* hits ignore armor, fence thorns (enemies hitting the fence take damage) |
| Legendary | Start with an extra shop slot, an extra buff pick at the start of a run; *added:* kill-gauge picks offer 4 choices |

*The ten added on 2026-11-09 are Claude's list, accepted by the user; numbers are placeholders (29 talents in all).*

*Draft:* talent tree nodes:
- **QoL (requested by the user):** free rerolls (e.g. 1 free reroll per wave), free lock, 1 free EXP purchase per wave, choose the starting hero from 4 instead of 3, see one more wave ahead while scouting, full sell refund for heroes bought this shop phase, a free fence repair between waves. *Built (2026-11-08):* Free Reroll (1 point), Free EXP (2, needs Free Reroll), Free Repair (1), Starting Pick from 4 (1), Scout Ahead +1 wave (2). Free lock and the full refund were dropped: locking is already free and selling already refunds the full cost. Starting Pick has no effect until there are more than 3 tier-1 damage dealers.
- **Synergy nodes:** one small branch per synergy, e.g. "Sylvan crits deal ×2.5", "Guardian armor also reduces aura damage". Breakpoint changes ("counts from 1 fewer hero") are strong: rare, at the end of a branch. *Built (2026-11-08), the same two nodes for every synergy:* "+25% bonus" (1 point), then "1 fewer hero at every breakpoint" (3 points, needs the bonus). **Synergy signature nodes (built 2026-11-09, Claude's list accepted by the user; names and numbers *Draft*):** one per synergy, 2 points, needs the "+25% bonus" node, and adds an effect to the synergy while it is active: Ranger *Longshot* (+20% range), Mage *Aftershock* (splash hits slow 30% for 1.5 s), Guardian *Bulwark* (the team takes 50% less aura damage), Support *Medic's Reach* (heal and Blessing radius +50%), Trapper *Trap Line* (+1 trap out per Trapper), Kingdom *Royal Guard* (+30% max HP), Sylvan *Deep Wounds* (crits ×2.5), Ironhold *Forge-Tempered* (hits ignore 2 armor), Beastfolk *Frenzy* (+3% damage per 10 s of the wave, with the ramp).
- **Endgame / OP nodes (built 2026-11-09, Claude's proposal accepted by the user; names and numbers are *Draft*):** expensive, independent, build-defining choices rather than more flat stats (tree points are stage stars, 12 today, so owning them all is a long way off). **Second Wind** (4 points): once per run, when the base would fall, it holds on with 1 HP and the fence is rebuilt to full. **Late Bloomer** (3): heroes deal +2% damage for every wave cleared this run. **Boss Hunter** (3): bosses and mini-bosses take +30% damage and drop 10 coins. **Lucky Start** (3): the starting hero arrives as a 2★ copy. **Full House** (4): one more hero on the board at every commander level. The user is still collecting ideas for more.

### Hero levels and ranks (shape decided 2026-11-13, Claude's proposal accepted; numbers and perks *Draft*; not built)
A fourth system: every hero gets permanently stronger between runs. The user asked for hero levels in the style of *Heroes vs Hordes* ("the more they level the stronger they are, and maybe unlock skill effects and buffs"). All names and numbers are placeholders.

**Two layers, two kinds of reward:**

- **Level (1–60): small and frequent.** Each level above 1 gives the hero **+1%** damage, max HP, healing, fence repair and trap damage (level 60 = +59%). Paid with a new currency, **scrolls** (placeholder name), earned from every run like gems. Every copy of the hero in a run has the hero's level, and it multiplies with the in-run stars.
- **Rank (1–6): rare and exciting.** Paid with **that hero's shards**. Each rank raises the level cap by 10 and unlocks one thing:

  | Rank | Shards | Level cap | Unlocks |
  |---|---|---|---|
  | 1 | — | 10 | (every hero starts here, when its race unlocks) |
  | 2 | 20 | 20 | **Class passive**: a small always-on buff, one per class (5 to design) |
  | 3 | 40 | 30 | **Ability I**: the ability's main value +25% at every star (the same rule for every hero) |
  | 4 | 80 | 40 | **Ability effect**: a new effect on the ability, unique to the hero (20 to design) |
  | 5 | 120 | 50 | **Quick start**: starts every wave with the ability bar half full (the same rule for every hero) |
  | 6 | 160 | 60 | **Mastery**: a signature perk unique to the hero (20 to design) |

#### Perks (Claude's list, **accepted by the user 2026-11-13**; every name and number is a placeholder)

**How big a perk may be:** rank 2 is worth about +5% of a hero's power, rank 4 about +10%, rank 6 about +15%. A perk changes *how* the hero plays more than how hard it hits; raw numbers belong to levels. Every perk below uses an effect the game already has (slow, stun, root, poison, mark, taunt, armor, mana, traps), so none needs a new system.

**Rank 2, class passives** (one per class, the same for its four heroes):

| Class | Passive |
|---|---|
| Ranger | *Double Shot:* every 5th attack hits twice |
| Mage | *Singe:* splash hits burn for 20% of the hit's damage over 2 s |
| Guardian | *Stand Firm:* takes 15% less damage while outside the fence |
| Support | *Uplift:* a hero it heals or feeds mana attacks 10% faster for 3 s; the Tinker and the Fox, who do neither, give it to the heroes in the 8 cells around them when they cast |
| Trapper | *Wide Jaws:* its traps are 20% wider |

**Rank 3 and rank 5** stay one rule for every hero: the ability's main value +25% at every star, and the ability bar starts each wave half full.

**Rank 4 (the ability gains an effect) and rank 6 (mastery, a perk for the hero itself):**

| Hero | Rank 4: ability effect | Rank 6: mastery |
|---|---|---|
| Shield Knight | *Brace:* after Shield Bash it takes 30% less damage for 4 s | *Last Stand:* once per wave, a hit that would knock it out leaves it at 1 HP and sets off a free Shield Bash |
| Crossbow Squire | *Piercing Bolts:* during Rapid Fire each bolt also hits the enemy behind its target | *Steady Aim:* every hit on the same target deals 5% more, up to +50% |
| Hedge Wizard | *Scorched Earth:* Fireball leaves burning ground at every star (at 3★ it burns twice as long) | *Twin Flame:* every third Fireball is cast twice |
| Chapel Cleric | *Benediction:* Blessing also heals every hero in its radius for 10% of their max HP | *Sanctuary:* heroes within its radius take 15% less damage |
| Royal Snarer | *Barbed Net:* enemies held by the Net take 20% more damage | *Wide Cast:* its small traps catch two enemies instead of one |
| Leaf Archer | *Pinning Arrows:* Volley arrows slow by 30% for 2 s | *Eagle Eye:* a crit halves the wait for its next attack |
| Bloom Druid | *Pollen:* enemies hit by Wild Bloom are poisoned for 4 s | *Life Spring:* each cast also heals the most hurt hero for 15% of its max HP |
| Sapling Treant | *Thorn Bark:* while rooted, enemies that hit it take damage back | *Deep Roots:* regenerates 1% of its max HP every second |
| Grove Singer | *Encore:* Mana Song also gives those heroes +15% attack speed for 4 s | *Chorus:* Mana Song also reaches every Sylvan hero, wherever it stands |
| Thorn Weaver | *Spreading Thorns:* an enemy that dies in Thorn Bind passes its poison to the nearest enemy | *Withering Venom:* enemies it has poisoned are healed 50% less (an answer to Menders) |
| Cannoneer | *Grapeshot:* Big Shot's line is twice as wide | *Heavy Rounds:* basic shots splash in a small radius |
| Rune Smith | *Overload:* the last bounce of Spark Rune stuns for 1.5 s | *Static:* every 4th basic attack chains to 2 more enemies |
| Hammer Brawler | *Aftershock:* the last slam of Earthshaker is twice as wide | *Momentum:* +10% attack speed per enemy in reach, up to +50% |
| Tinker | *Spiked Plating:* while Patch Job's armor lasts, enemies that hit the fence take 10 damage | *Stubborn Fence:* once per wave, a hit that would break the fence leaves it at 1 HP and nothing can hurt it for 3 s |
| Bomb Sapper | *Cluster:* after the Vacuum Bomb, 3 small bombs go off for 30% of its damage each | *Stockpile:* keeps one more small trap out |
| Hawk Eye | *Open Season:* when a marked enemy dies, the mark jumps to the nearest enemy for the time left | *Predator:* basic attacks also deal 1% of the target's max HP (half against bosses) |
| Owl Sage | *Miasma:* enemies poisoned by Plague Feathers are slowed by 20% | *Venom Quills:* its basic attacks poison too |
| Bear Warden | *Roar:* at the end of Rampage it taunts every enemy within 250 px for 3 s | *Thick Hide:* every hit on it deals 3 less, at least 1 |
| Fox Merchant | *Jackpot:* one of the enemies Lucky Find marks drops triple | *Haggle:* the first reroll of every shop phase is free while it is on the board |
| Badger Digger | *Deeper Pit:* enemies climbing out of the Pit Trap lose 10% of their max HP (half for bosses) | *Home Turf:* a Tunnel Grub that surfaces within its range is stunned for 2 s; other enemies crossing any of its traps are slowed by 20% |

*Kept (user, 2026-11-13, on Claude's recommendation):* three rank-6 perks protect a star or change the shop (Tinker's fence save makes the "fence never broke" star easier; the Fox's free reroll stacks with the tree's). They are the kind of perk a rank 6 should feel like, but they are the ones to cut first if the stars or the economy get too easy.

#### Currencies (Claude's proposal, **accepted by the user 2026-11-13**; numbers are placeholders; replaces the first sketch)

**One job per currency**, so a reward always says what it is for:

| Currency | Pays for | Comes from |
|---|---|---|
| **Gems** | talent spins | every run, as today (3 per wave, +30 for a win); chests |
| **Scrolls** | hero levels | every run: **10 per wave cleared, +50 for a win**; night pays double; some chests |
| **Hero shards** | that hero's ranks | **the first clear of a run** (a fixed hero, shown on the card) and **every win** (the heroes on the final board) |
| **Wild shards** | any hero's rank | the first clear of a chapter's boss run, chests, the first clear of a night run |
| **Stars** | talent tree points (never spent) | as today |

**No random shard drops anywhere.** **Decided (2026-11-13):** the user wants a forgiving economy, unlike *Heroes vs Hordes*, whose currencies push players to buy. Every shard source is either fixed and visible beforehand, or follows what the player chose to play, so luck never blocks a favourite and no chest can disappoint.

- **Scrolls.** A level costs 5 × the current level: 225 to reach level 10, 950 to 20, 2,175 to 30, 8,850 to 60. A loss still pays for its waves.
- **Hero shards from a first clear:** 10 shards of one hero from the run's races, printed on the stage card as its reward ("First clear: 10 × Leaf Archer"). 34 runs give 340 shards; every hero is featured at least once. The five chapter boss runs give **20 wild shards** instead.
- **Hero shards from every win, "veterans":** each hero on the board when the run is won earns **1 shard per star it has** (2 per star at night). Play a hero and it ranks up. The scripted player's winning boards hold 7–9 heroes and about 13 stars on a chapter's boss run, about 5 on a five-wave run, so longer and harder runs pay more per minute and there is no reason to grind 1-1.
- **Chests** (the star track, extended to the 132 stars now possible): the five built chests stay; after 15 stars, one chest every 6 stars up to 129 (19 more), cycling through 100 gems, 15 wild shards, 300 scrolls, and 1 free spin with 10 wild shards. *Built (2026-11-13):* all of them; the last two, at 123 (15 wild shards) and 129 (300 scrolls), need night stars, since the day runs give 117.
- **When it opens:** hero levels appear after the first clear of 1-2, so the first session is only the shop and the fence.

**What that adds up to** (to be checked in a spreadsheet; a "regular day" is about 45 minutes, 4 runs, 3 wins):

| Moment | Scrolls | Shards | Where the roster stands |
|---|---|---|---|
| The day ladder cleared once (39 runs, 434 waves, about 8–10 hours) | about 6,300 from a clean pass, 8,000–9,000 with losses and replays | 340 fixed + about 350–450 from wins + about 100 wild + chests | most heroes level 12–14 at rank 2 (their class passive), two or three favourites at rank 3 |
| Each regular day after that, mostly night runs | about 1,200 | about 60–80, plus chests | a favourite gains a rank every few days |
| Totals needed | 8,850 per hero to level 60 | 20 / 60 / 140 / 260 / 420 in all for ranks 2–6 | a first favourite at rank 6 about two weeks after the day ladder (the wild shards go to it); a regular board of 8 heroes at rank 5–6 in about two months |

*Honest limits of this draft:* the whole roster at rank 6 would take far longer (8,400 shards) and is not a goal. If two months for a board feels slow, the lever is the veterans rate, or daily quests later; if gems pile up once the talents are maxed, a gem price for wild shards is the obvious sink. Neither is proposed now.

**Why 60 and not 120:** the total power is what matters, not the number of steps. *Heroes vs Hordes* has one hero on screen, so 120 levels all go into what the player sees. Here a run uses 8–20 different heroes from the shop, so levels are spread over the whole roster: 60 levels × 20 heroes is already 1,200 level-ups, and at 120 each one would be +0.5%, too small to feel. The cap is data, so it can grow (rank 7 and up) when there is content that needs it.

**Rules that protect the rest of the design:**
- **In-run power stays central** (see above): +59% at max is less than one in-run star (×1.8). Levels help; the shop, merges and synergies still decide a run.
- **Unlocking stays by race** (decided): the current 20 heroes are never locked one by one, because a stage's shop pool is already small (10 heroes on stage 1). Heroes added after the first 20 can be unlocked with shards, once the deck system exists.
- **Nightmare absorbs the power:** Normal is tuned for ranks 1–2 (today's numbers); Nightmare climbs from about rank 3 on the first stage to rank 5–6 on the last (see **Difficulty: day and night** below). Hero levels and Nightmare should ship together, or the five stages become too easy.
- **Build order:** levels, ranks and the three rule-based unlocks (ranks 2, 3, 5) first, which needs only 5 new perks; the 40 hero-specific perks (ranks 4 and 6, drafted under **Perks** above) in a later pass.
- **UI (needs a mockup first):** the Heroes tab card gets a level badge, rank pips and a shard bar; the hero window gets LEVEL UP and RANK UP buttons and the rank list with locked rows greyed out.

**Decided (2026-11-13):** the two layers (levels and ranks); a level cap of **60**; levels are paid with **a new currency**, not gems; the names "scrolls", "shards" and "rank" are kept for now. **TBD:** every number above, the perk lists, and the final names.

*Built (2026-11-13), all numbers placeholders:* levels and ranks, scrolls, hero shards and wild shards, the rule-based ranks (2, 3 and 5), the Heroes tab cards and the hero window's UPGRADE side (mockups 20 and 21), the first-clear reward on the stage card (mockup 18) and the chests from 21 to 117 stars. Choices Claude made while building, for the user to confirm or change:
- **A level scales ability damage too**, not only basic attacks: the design says "damage", and Mages and Trappers do most of theirs through abilities and traps. It also scales every poison, heals, fence repair and the Tinker's patch. It doesn't scale mana, coins, durations or the Hawk Eye's share of max HP.
- **The "main value" rank 3 raises** is the ability's damage for most heroes; attack speed for the Crossbow Squire, the max-HP share for the Hawk Eye, the poison for the Owl Sage, the heal for the Sapling Treant, the repair for the Tinker, the coins for the Fox Merchant, the mana for the Grove Singer and Chapel Cleric; and for Trappers the signature trap's damage and poison, or its hold time when it deals neither (Royal Snarer, Badger Digger).
- **A first-clear reward is paid on the next win of a run that was cleared before rewards existed**, so older saves miss nothing.
- **Which hero each run pays** (Draft): 1-1 Shield Knight, 1-2 Leaf Archer, 1-3 Hedge Wizard, 1-4 Sapling Treant; 2-1 Rune Smith, 2-2 Cannoneer, 2-3 Tinker, 2-4 Hammer Brawler, 2-5 Bomb Sapper; 3-1 Owl Sage, 3-2 Badger Digger, 3-3 Hawk Eye, 3-4 Fox Merchant, 3-5 Bear Warden, 3-6 Thorn Weaver, 3-7 Chapel Cleric; 4-1 Royal Snarer, 4-2 Grove Singer, 4-3 Crossbow Squire, 4-4 Bloom Druid, 4-5 Shield Knight, 4-6 Leaf Archer, 4-7 Rune Smith, 4-8 Owl Sage, 4-9 Cannoneer; 5-1 Hedge Wizard, 5-2 Sapling Treant, 5-3 Hawk Eye, 5-4 Tinker, 5-5 Thorn Weaver, 5-6 Chapel Cleric, 5-7 Hammer Brawler, 5-8 Bear Warden, 5-9 Bloom Druid. Every hero is named once before any is named twice; the boss runs pay 20 wild shards.
- **Singe is built as a poison** (the game has no separate burn), so it shows the green poison tint and counts for the talent that raises damage to poisoned enemies.

*Not built:* the 40 hero perks of ranks 4 and 6 (those ranks raise the level cap only, and the window says they come later), buying several levels in one press, a use for shards past rank 6. Night's double scrolls and shards are built (see **Difficulty: day and night**). *Measured with the scripted player (16 seeds, so ±12%):* with every hero at level 13 and rank 2, about where the day ladder should leave a player, it wins Frozen Reach's boss run 14 of 16 times against 56% without levels, so the later day runs will need a retune.

### Difficulty: day and night (user's idea 2026-11-13; **night runs built 2026-11-13**, numbers placeholders; the night rule per stage is not built)
**Decided by the user (2026-11-13):** two difficulties only, **Normal and Nightmare**, switched with a **toggle**. Normal is **daytime**, Nightmare is **night**. A stage's night **opens when its day is cleared**. At night enemies are **stronger, more numerous and faster**. The **darkness** rule (hidden preview) is in. Special night rules per stage are **for later** (not decided; the table below is kept as ideas).

*Draft* details (Claude's proposal; the numbers and looks are not decided):

- **The toggle:** a sun / moon switch on the Battle tab. At night the stage cards, the menu background and the battlefield take a dark blue night look (one colour tint over the world, so no new art is needed), and enemies get glowing eyes or a purple tint so the mode is never in doubt. The choice is remembered.
- **Unlocking:** a stage's night opens when its day is cleared. The moon is greyed out with "Clear this stage by day first" until then.
- **What night changes, three layers:**
  1. **Stronger, more and faster enemies (decided):** more HP and more fence, base and hero damage (the per-stage `enemy_hp_scale` knob exists for this), bigger groups in every wave, and a higher walking speed. Placeholders: HP ×2, damage ×1.5, counts ×1.5 and speed ×1.2 on the first stage, growing per stage. Bosses and mini-bosses stay single.
  2. **One night rule per stage (later, not decided)**, which would turn up that stage's own mechanic, so night plays differently and isn't only bigger numbers:

     | Stage | Night rule (first ideas) |
     |---|---|
     | Greenwood Road | *Swarm:* half again as many Imps and Scamps |
     | Iron Pass | *Tempered:* every armored enemy has +1 armor |
     | Wild Hills | *Deep roots:* healers heal twice as often, Grubs surface closer to the fence |
     | Goblin Keep | *Short fuses:* Sappers run faster and come in pairs |
     | Frozen Reach | *Long night:* freezes last longer, the Wyrm breathes more often |

  3. **Darkness (decided):** the next-wave preview shows only the front rank; the rest are dark shapes until they walk in. Scouting matters more at night.
- **Rewards:** night has **its own 3 stars per stage** (30 stars over the five stages instead of 15), pays more gems and scrolls per wave (placeholder ×2), and its first clear gives hero shards. New chests continue the star track past 15.
- **One night run per stage (decided 2026-11-13, the user's idea):** night is **a single long, difficult run per stage**, not a night version of every sub-stage. It opens when the stage's **last** sub-stage is cleared by day, and uses the full stage's wave count with the night changes above. This replaces "its own 3 stars per sub-stage" wherever this section says so: stars are 39 day runs × 3 + 5 night runs × 3 = **132**, against the tree's 78 points, so the tree no longer needs a big rescale. Only 5 night runs need tuning instead of 39, and each becomes an event: the stage's hardest challenge, with the best rewards (shards, a big gem and scroll payout). **It depends on saving a run in progress:** the longest night run is 24 waves, well over 20 minutes on a phone, so a run must survive the app closing. In the story it is a bonus episode per stage (see `Story_Draft.md`).
- **Night in numbers (Claude's proposal, accepted by the user 2026-11-13; starting values; replaces the placeholders in layer 1 and the Rewards line above):**

  | Night run | Waves | Enemy HP | Group sizes | Walking speed | Enemy damage | Heroes it expects | First clear |
  |---|---|---|---|---|---|---|---|
  | Greenwood Road | 10 | **×1.6** (started at ×1.3) | ×1.25 | ×1.1 | ×1.25 | rank 3, about level 25 | 40 wild shards |
  | Iron Pass | 12 | **×1.4** | ×1.3 | ×1.1 | ×1.3 | rank 3–4 | 50 |
  | Wild Hills | 15 | **×1.35** (started at ×1.5) | ×1.35 | ×1.15 | ×1.35 | rank 4 | 60 |
  | Goblin Keep | 20 | **×1.2** (started at ×1.65) | ×1.4 | ×1.15 | ×1.4 | rank 4–5 | 70 |
  | Frozen Reach | 24 | **×1.47** (started at ×1.8) | ×1.5 | ×1.2 | ×1.5 | rank 5–6, level 50+ | 80 |

  - **Tuned HP (2026-11-13, replaces the table's HP column; the other columns are built as written):** enemy HP **×1.6 / ×1.4 / ×1.35 / ×1.2 / ×1.47** on nights 1–5. Measured with the scripted player, 48 seeds a value (about ±7%), every hero at one level and rank per night: 25 / rank 3, 30 / rank 3, 35 / rank 4, 40 / rank 4, 50 / rank 5 (*Claude's reading* of the "Heroes it expects" column: a range such as "rank 3–4" is played at its lower rank's level cap). Wins: **60% / 56% / 46% / 42% / 33% (29, 27, 22, 20 and 16 of 48)** against the targets below. Night 5 is noisy around its target: 48% at ×1.45, 33% at ×1.47 and 31% at ×1.5 (38% over the three), so ×1.47 stands. The design's starting HP was too low for night 1 (7 of 8 wins at ×1.3) and too high for nights 3–5 (31% at ×1.5, 6% at ×1.65 and 19% at ×1.8, 16 seeds each): bigger and faster groups cost the bot more than hero levels give back. **Early wipes:** many night losses come early, not late: night 3 lost 8 of its 26 on wave 4 (Orc Bruisers against a small board, the stage's old weak spot), night 4 lost 11 of 28 by wave 5 and night 5 lost 8 of 32 by wave 6, each with two on wave 1. HP alone can't move those without making the late waves easy; the levers would be those waves' composition or a night HP scale that starts lower and rises over the run. Not decided, not built.
  - **These are starting values, not tuned ones.** The earlier placeholder (HP ×2 and counts ×1.5 on the first night) meant three times the HP to chew through against heroes about 40% stronger, so it is lowered. Group sizes and speed set how night *feels* and stay as written; **HP is the knob the scripted player tunes**, with a prepared save at the expected ranks.
  - **Win-rate target:** 60 / 55 / 50 / 45 / 40% for the scripted player, lower than day on purpose: a night run is an event, a loss still pays double, and a saved run means nobody loses 20 minutes to a phone call. **Decided (2026-11-13): night should be much harder than day; more rewards can be added to it later.**
  - **Bosses and mini-bosses** stay single and get the HP and damage factors only. Summoned enemies are not multiplied (the summoner's count already is).
  - **Kill gauge:** its cost grows by the same factor as the group sizes, so buff picks come at the day pace.
  - **Rewards:** gems and scrolls per wave ×2 and the win bonus ×2; veterans shards 2 per star; the first clear pays the wild shards in the table; **its own 3 stars** by the day rules (15 night stars in all).
  - **Darkness, exactly:** in the shop phase the preview draws the front rank as usual and every other enemy as a dark shape of its size, so a boss is still a big shadow. The Next wave card lists the front-rank enemies with counts and one "+ ? more" line. The boss banner still names the boss when the wave starts. The tree's Scout Ahead shows the wave after next under the same rule.
  - **One saved run at a time**, day or night: the Battle tab's CONTINUE and abandon window work the same.
  - **What night does not change:** the shop, prices, income, the stage's races, the wave tables' order. A night run is the same stage, harder and darker, so what the player learned by day still applies.
- ***Built (2026-11-13), placeholders:*** the sun / moon switch on the Battle tab (remembered) and the night card (mockups 18 and 19); the five night runs with the table's group sizes, speed and damage and the tuned HP above; darkness; the night look in battle; night's own stars, double gems, scrolls and veterans shards, and its first-clear wild shards; the chests at 123 and 129 stars; saved runs for night as for day. **Choices Claude made while building, for the user to confirm:**
  - **"Enemy damage" covers every kind:** fence hits, base hits, and everything that hurts heroes (attacks, the Bog Shaman's and Briar Witch's aura, the Frost Wyrm's breath). Freeze times are unchanged. Small fence damage keeps its fraction (an Imp's 1 damage at ×1.25 is 1, 1, 1, 2).
  - **"The front rank" is the foremost rank the wave has:** its tanks when it has any, otherwise its middle rank, otherwise its back rank. Read strictly (tanks only), an all-Imp wave would show nothing but shadows. The Next wave card then lists those enemies, "+ ? more", and "8 in front" in place of the wave's size.
  - **The night look:** one dark blue tint over the whole battlefield (heroes included) and a brighter purple tint on enemies; the HUD, shop and pop-ups keep their day colours. No mockup; shown as screenshots.
  - **A locked night says** "Clear 1-5 by day first" (the stage's boss run), and the switch itself always works, so a player can look at the nights before opening one.
  - **After a night run** the run-end window offers Play again and Main menu, not "Next stage".
  - **The menu at night** uses mockup 19's flat colours; there is no night background art.
- **Balance target:** Nightmare is a second ladder after Normal. Night stage 1 is tuned for heroes around rank 3, night stage 5 for rank 5–6, each at the same win rates as the day stages (measured with the scripted player and a prepared save).
- **Tree points:** the talent tree costs 78 points and day + night give 6 stars per stage (30 over the five stages). **More stages close the gap** (user's direction, 2026-11-13): 13 stages give 78. **Sub-stages (user's idea, 2026-11-13; details *Draft*):** every stage is split into sub-stages, numbered 1-1, 1-2, 1-3. *Draft:* **three per stage** (15 runs = 90 stars with night); the last sub-stage is today's full stage with its boss; the earlier ones use the same enemies in new wave tables, are shorter (about 60% and 80% of the stage's waves, e.g. 6 / 8 / 10 on Greenwood Road) and end on the stage's mini-boss, so they need no new art and give quicker sessions. Each sub-stage is its own run with its own 3 day stars and 3 night stars; clearing one opens the next, and clearing the last opens the next stage's first. A stage's new race unlocks on its first sub-stage, as today. The Battle tab keeps one card per stage, with a row of sub-stage markers showing each one's stars. The count per stage is data, so a stage can get more later. **TBD:** the count, the wave lengths, and the card's look (needs a mockup).
  - **Decided (2026-11-13): the sub-stage counts are 5 / 6 / 8 / 10 / 10** (39 runs; this replaces "three per stage" above), and each stage gets a story (see **Narrative Arc**).
  - *Built (2026-11-13), placeholders:* the 34 new runs and the unlock chain. Wave counts are 5 / 6 / 7 / 8 / 10 on Greenwood Road, 6–12 on Iron Pass, 7–15 on Wild Hills, 8–20 on Goblin Keep and 9–24 on Frozen Reach. Each new run's waves are **composed by a script** from its stage's hand-made wave table: only the enemies that run is about appear (the "New to play" column of the story draft), its featured enemy comes in bigger groups, and its last wave is written by hand (the mini-boss runs end on the mini-boss). Enemy HP follows the stage's own curve by wave number. The Battle tab showed one card per run at first; **the stage card with a circle per sub-stage is built (2026-11-13, mockup `18 Battle tab · sub-stages`, approved; 8 or 10 sub-stages take two rows)**, and since then its first-clear reward row and the day / night switch (both built 2026-11-13). Not built: the story text on screen and the stage intros and endings. The chest track now runs to 129 stars.
  - **Story and longer stages (user's idea, 2026-11-13; the discussion behind that decision):** give each stage a story, told across its sub-stages, and go up to about **10 sub-stages per stage**, with some stages longer than others. *Claude's advice:* yes, with two conditions. (1) **Every sub-stage needs something new to play**, not only new text: a new enemy joining, a new mix, a mini-boss, a twist. Greenwood Road has six such things (Imp, Scamp, Orc, Shaman, Warchief, King), so it carries about 5–6 sub-stages; later stages reuse every earlier enemy and can carry 10. *Suggested counts:* 5 / 6 / 8 / 10 / 10 (39 runs, 234 stars with night). Early sub-stages introduce enemies one at a time, which also teaches the game. (2) **A short first stage keeps the first race unlock close**: at 10 sub-stages a new player would play ten runs with two races before Ironhold appears. *Story format, suggested:* one or two lines of text per sub-stage on its card, and a short intro and ending per stage; no cutscenes or new art. **Follow-ups:** with 200+ stars the tree's costs must be rescaled (or the tree grown) and the chest track extended; and Normal can no longer be tuned for rank 1–2 heroes throughout: the day ladder itself must expect hero levels to grow along it.

Still TBD:
- Alternate maps after the last stage?
- Is there monetization, and does it touch any of these systems?

### Connected sub-stages (user's idea 2026-11-13; rules decided, details *Draft*; prototype built and retuned on Greenwood Road 2026-11-14)
**The problem (user):** starting from one hero and 3 coins on every short run is tiring. In *Heroes vs Hordes* the sub-levels of a stage are connected: what the player gained in the first is kept until the stage's boss.

**Decided by the user (2026-11-13):**
- **A stage's sub-stages are one connected run.** Heroes, coins, bonuses and everything else the player built carry from one sub-stage to the next, up to the stage's boss. (Since 2026-11-14 a long stage is two or three such runs, called chains: see "Chains" below.)
- **The fence starts every sub-stage at full HP**, so each sub-stage's three stars keep their meaning. **The base starts every sub-stage at full HP too**, as at the start of any stage.
- **A loss retries the sub-stage**, with the progress made up to the end of the one before it (a checkpoint). It does not send the player back to the start of the stage.
- With a built board carried in, **later sub-stages can be made more challenging**.
- It is built **on its own branch** (`feature/connected-sub-stages`), so the separate runs stay intact on `develop` until this is judged.

***Draft* (Claude's plan; the user left the scope to Claude):**
- **Prototype on Greenwood Road only** (1-1 to 1-5, 36 waves); the other stages stay separate runs until the prototype is played and measured. Which stages are connected is one data flag per stage.
- **What carries:** every hero and its stars and place, coins, the commander's level and EXP, bought shop slots, bought fence upgrades (the higher max HP), the kill gauge and every buff picked, the shop's lock. **What starts fresh each sub-stage:** fence HP (full, at its upgraded max), base HP, the two star conditions, free repairs and rerolls, the wave counter, the loss report. The starting pick appears only on the stage's first sub-stage.
- **Checkpoints:** when a sub-stage is cleared, the build is stored as the next sub-stage's starting point. A loss retries the current sub-stage from it. A sub-stage with no checkpoint (a save from before this) starts as a fresh run.
- **Going back means restarting the stage (decided by the user 2026-11-13):** a player on 1-3 who wants to play 1-2 again restarts the whole stage from 1-1. Only the stage's furthest sub-stage reached can be played from its checkpoint; an earlier one can't be picked on its own. So there is only ever one checkpoint per stage, and the question of a worse replay overwriting a better build doesn't arise. A stuck player's way out is the same: restart from 1-1. *Draft:* restarting asks first (it drops the stage's checkpoint), and once the boss is beaten the stage is replayed from 1-1, for missed stars too.
- **Rewards, stars, first clears and saved runs** stay per sub-stage, as today.
- **Night** stays one long run per stage, started fresh.

**Decided by the user while building (2026-11-13):**
- **The last wave of a sub-stage pays like any other wave:** its income, the commander's EXP and a fresh shop roll (unless locked) reach the next sub-stage. (Before, the last wave of a run paid nothing, since the run ended.)
- **Late Bloomer and Second Wind count across the whole stage:** Late Bloomer keeps growing to the boss, and Second Wind saves the base once per stage, not once per sub-stage.
- **The Battle tab works as the plan says**, built from existing pieces and shown as screenshots rather than mocked up first.

**Decided by the user (2026-11-14; Claude's recommendation accepted; every number still to be tuned):** how difficulty rises across a connected stage.
- **A sawtooth, not one long curve.** Each sub-stage keeps its own short ramp, from an easy first wave to its finale, and one multiplier per sub-stage sets its level. A win is followed by a breather, which fits the fence starting full, and a retry starts gently.
- **More enemies and more HP together.** Groups grow over the stage (to about ×1.5–1.75 by the boss sub-stage, *Draft*), and enemy HP covers the rest. HP alone was measured: it makes waves long before it makes them dangerous.
- **A boss is scaled less than the waves before it**, with a factor of its own, so it doesn't become a wall. Bosses and mini-bosses stay single, as at night.

**Chains (decided by the user 2026-11-14; not built).** The stages get long: their sub-stages add up to 36 / 52 / 80 / 124 / 142 waves, and on Greenwood Road the board already stops growing in size around wave 20. So a long stage is split into **chains**, and only the sub-stages of one chain are connected.
- **A chain is about 40–55 waves.** The limit is counted in waves, not sub-stages, because sub-stages get longer through the game.
- **A stage is split at a mini-boss sub-stage**, so every chain ends on a climax, and **the last chain holds the stage's boss**.
- **A new chain starts like any run today**: the starting pick, 3 coins, a fresh fence. Its first sub-stage is already tuned for that.
- Everything decided for a connected stage holds per chain: checkpoints, retrying a lost sub-stage, and going back (which restarts the chain from its first sub-stage, not the stage from its first).
- **The layout** (*Draft*: the user left the chain lengths to Claude):

| Stage | Chains | Waves | Each chain ends on |
|---|---|---|---|
| 1 Greenwood Road | 1-1 to 1-5 | 36 | the Goblin King |
| 2 Iron Pass | 2-1 to 2-6 | 52 | the Mountain Troll |
| 3 Wild Hills | 3-1 to 3-5 · 3-6 to 3-8 | 42 · 38 | the Elder Mender · the Briar Witch |
| 4 Goblin Keep | 4-1 to 4-5 · 4-6 to 4-8 · 4-9 to 4-10 | 49 · 39 · 36 | the Goblin King · The Sick Ward · the Goblin Warlord |
| 5 Frozen Reach | 5-1 to 5-5 · 5-6 to 5-8 · 5-9 to 5-10 | 55 · 45 · 42 | the Glacier Golem · the Elder Mender · the Frost Wyrm |

- *Draft:* 4-8 The Sick Ward is the one chain end without a mini-boss. The Elder Mender would fit its last wave ("Menders by the dozen"). The other way to cut stage 4, 4-6 to 4-9 and then 4-10 alone, ends on the Warchief and the Sergeant but leaves the Warlord as a fresh 20-wave run with no carried build.
- *Draft (Claude's reading):* **Second Wind is once per chain and Late Bloomer grows across a chain.** The user's 2026-11-13 decision said "per stage", when a stage was one connected run.
- *Banked, not decided:* **shorter late sub-stages.** 4-10 has 20 waves and 5-10 has 24 because a fresh run needs that long to build up; a carried board doesn't. It would let chains hold more sub-stages, but it changes the waves, the rewards per wave and the pacing. Look at it after a split stage has been played.

**What to tune a chain to (accepted by the user 2026-11-14 as a first target; "more balancing later").** Measured with the scripted player, no talents:

| | 1-1 | 1-2 | 1-3 | 1-4 | 1-5 (boss) |
|---|---|---|---|---|---|
| Won on the first try | 100% | 95% | 90% | 85% | 75% |

- **Stuck rate:** at most about 1 playthrough in 20 fails the same sub-stage three times in a row. A stuck build is the expensive failure of a chain, since its only way out is restarting the chain.
- **Wave length** stays where it is: regular waves 25–55 seconds, a boss wave 70–160, overtime under about one per boss run. Harder must not mean longer. **For now the bar is the two time bands, not the overtime count (user, 2026-11-14):** Greenwood Road's boss run already has about two overtimes as a separate run, and about three once retuned for a carried board.
- **The fence takes real damage** from a chain's third sub-stage on, so the stars mean something.
- *Draft for the other chains:* the first sub-stage as it is today; a chain that ends on a mini-boss ends at about 80–85%; a chain that ends on the stage's boss ends at the stage's old target (75 / 70 / 65 / 60 / 55%). Stages 3–5 are tuned with the hero levels a player is expected to have there.
- *Not decided:* **a small help on retry** (for example a few coins each time a sub-stage is retried). Only if tuning alone can't get the stuck rate under 1 in 20. **On Greenwood Road it can't, with the scripted player** (below): the first-try targets for 1-4 and 1-5 and the stuck rate can't both be met, so this is the open lever.

***Built (2026-11-14), on the branch, placeholders:***
- Greenwood Road's five runs are connected; every other stage is unchanged.
- **The Battle tab:** the stage's card opens on the sub-stage it is played from. At a checkpoint it says "Your build from 1-2 carries on". Any other circle says "Starts the stage over from 1-1", and PLAY reads RESTART / FROM 1-1. When a build is waiting at the checkpoint, PLAY asks first, in the abandon window: "RESTART THE STAGE?", with KEEP MY BUILD or RESTART FROM 1-1.
- **The run-end window:** after a connected sub-stage's win it offers Next stage and Main menu, with no Play again, since replaying would mean restarting the stage. After the boss it offers "Replay from 1-1". After a loss, Retry starts the sub-stage from its checkpoint again.

**First measurement (2026-11-14; the scripted player, no talents, 48 playthroughs of 1-1 to 1-5, retrying a lost sub-stage up to 3 times):** all 48 beat the Goblin King. Every sub-stage was won on the first try, and with all three stars. Played as separate runs, the same five are won 100 / 94 / 88 / 81 / 81% of the time. What the player carries in:

| Entering | Heroes on the board | Stars on the board | Commander level | Fence max HP |
|---|---|---|---|---|
| 1-2 | 6.0 | 8.7 | 4.1 | 221 |
| 1-3 | 7.7 | 14 | 5.7 | 256 |
| 1-4 | 8.8 | 18 | 7.0 | 285 |
| 1-5 | 9.8 | 21 | 7.9 | 304 |

The commander reaches the max level (8, ten heroes on the board) about two waves into 1-4, around wave 20 of 36, so the whole boss run is played with a full board. The fence takes no damage after 1-2. 1-3 to 1-5 also take about half as long as separate runs (156 / 175 / 216 seconds instead of 256 / 280 / 399). **As tuned for separate runs, connected Greenwood Road was far too easy.**

**Retuned (2026-11-14; placeholders, measured with the scripted player, no talents, 48 playthroughs, up to two retries per sub-stage).** Each sub-stage keeps its waves and gets one level, as decided: bigger groups, more HP, and a smaller factor for the boss.

| | 1-1 | 1-2 | 1-3 | 1-4 | 1-5 (boss) |
|---|---|---|---|---|---|
| Group sizes | ×1 | ×1.15 | ×1.3 | ×1.45 | ×1.6 |
| Enemy HP | ×1 | ×2.8 | ×2.9 | ×5.0 | ×5.5 |
| Boss and mini-boss HP, on top | | | | | ×0.5 (×2.75 in all) |
| Won on the first try (target) | 100% (100) | 98% (95) | 92% (90) | 96% (85) | 87% (75) |
| Won with three stars | 100% | 81% | 93% | 89% | 78% |
| Fence HP lost per run | 1 | 149 | 103 | 122 | 203 |

- **Stuck:** 3 of 48 playthroughs (6%, target about 5%); 45 of 48 beat the Goblin King.
- **Wave length:** regular waves average 18–40 seconds (the slowest tenth up to about 64), the boss wave 100 seconds, so both stay in their bands. The late waves of each sub-stage get longer (1-5's waves 8–9 from about 52 to 60–65 seconds) while the early ones get shorter, since a carried board crushes them.
- **Why 1-4 and 1-5 are easier than their targets:** about half of the scripted player's first-try losses end stuck, because the same weak build loses again. With 1-4 and 1-5 at HP ×5.4 and ×5.8, 1-4 reached its 85% but 7 of 48 playthroughs got stuck, 4 of them on 1-4. The stuck rate was kept, and the first-try targets for 1-4 and 1-5 wait on a decision: a small help on retry, or a play-test showing that players rebuild better than the scripted player. (Before a retry the scripted player now puts damage dealers first, as a player who lost would; that didn't measurably lower the stuck rate.)
- **1-3 is the spike:** "The Big Ones" brings 12 and then 10 Orc Bruisers at once in its last two waves (16 and 13 with bigger groups), a wall for a board short on damage, however often it retries. Its HP is held just above 1-2's for that reason. A chain's featured-enemy finale may need the same care on other stages.
- **A save from before checkpoints starts its furthest sub-stage fresh**, with one hero against HP tuned for a carried board, so enemies barely take damage. **Left as is (user, 2026-11-14):** only saves from before the branch meet it, and the player restarts the stage from 1-1.

**First play-test (user, 2026-11-14):** beat the Goblin King without losing a sub-stage: "overpowered, but in a good way", strong from 1-4 on, saving coins through 1-5 with nothing left to buy, and no wave dragged. So no help on retry for now, and the chain needs to be harder for a real player from 1-4 on. **But the shape is confusing** ("I like it but it's confusing"): what carries and what resets was not clear.

**Redesign decided by the user (2026-11-14; mockups approved, not built): one run with acts.** The rules above stay. What changes is how a stage is shown, so there is one thing to understand instead of four (stage, sub-stage, checkpoint, saved run):
- **A stage is one run, and its sub-stages are acts inside it.** The Battle tab shows the acts as a path, not as levels to pick: ticks and stars behind, a marker where the player is, the boss at the end. One button: PLAY, or CONTINUE with the act and wave. Start over is a small separate button and asks first.
- **Clearing an act happens inside the run.** A window shows the act's stars and rewards and then two lists: **carries on** (heroes and stars, coins, level and EXP, buffs and upgrades) and **starts fresh** (fence, base, three new stars, wave 1). Then on to the next act, with no trip to the menu.
- **Losing an act** shows what broke through, and where a retry starts: the start of that act, with the army as it was then. Main menu keeps the place; Start over begins a new army at Act 1.
- **In the run** the wave pill names the act ("ACT 3 · WAVE 1/7"), a track shows the acts, and a banner names each act as it starts.
- **Clearing the stage** shows every act's stars in one row.
- **The long stages are one card per run (decided 2026-11-14):** ten cards in all, Greenwood Road · Iron Pass · Wild Hills Part 1–2 · Goblin Keep Part 1–3 · Frozen Reach Part 1–3, split as in "Chains" above. Acts are numbered from 1 on every card, and each card has its own army and its own final fight, so one card is always one army. (Not chosen: one card with a camp in its path where the army ends.)
- **What doesn't change:** an act is a sub-stage as it exists today, so each keeps its three stars, its first-clear reward and its place in the unlock order; the star total, the chests and the tree's points are untouched. Night stays one long run per stage.
- *Draft wording in the game:* "Act" and "Part"; the words sub-stage, checkpoint and chain are not shown to the player.
- *Next:* new difficulty targets. The scripted player's targets were met and a real player was still overpowered from the fourth act on, so the targets need to be set harder before the cards are tuned.
- Mockups: page "Stage runs and acts" of `wave-defense.fig`, frames 22–27 (28 is the option not chosen).

**Open questions to answer with the prototype:**
- **The board maxes out**: its size does, by about wave 20 of Greenwood Road's 36 (the commander's max level). Its stars don't within this stage: at the end of 1-5 the scripted player's ten heroes hold 22.6 of 30 stars (2.9 heroes at 3★), and it ends each sub-stage with only 11–21 coins, so there is still something to buy. The economy was sized for 10–24 waves, and Frozen Reach's sub-stages add up to about 140 waves, so the longer stages are where this bites. **Answered 2026-11-14 by chains** (above): no connected run is longer than about 55 waves. If a chain still feels finished before its end, the next levers are a higher level cap, more board slots or more to spend coins on.
- **How much harder** later sub-stages must be once a board is carried in. The table above is the first answer: much harder. The board entering 1-3 (7.7 heroes, 14 stars) is already bigger than the one a separate run of the boss stage 1-5 ends with (7.4 heroes, 12.5 stars, on average over 8 runs). The levers are enemy HP per sub-stage, bigger groups, or both. **Second measurement (2026-11-14, 24 playthroughs each, enemy HP multiplied per sub-stage):** at ×1 / 2 / 3 / 4 / 5 over 1-1 to 1-5 every playthrough still beats the boss and only 2 of 24 need a retry on 1-5; at ×1 / 2.5 / 4 / 6 / 8 the first four sub-stages are still won on the first try, but 1-5 is won first try by 11 of 24, six playthroughs never clear it in three retries, and nearly every loss is on the boss wave, in runs of over 8 minutes with four overtimes. So 1-2 to 1-4 haven't reached their limit even at ×2.5, ×4 and ×6 (the fence only starts to take damage there), and 1-5 breaks somewhere between ×5 and ×8, on its boss alone. HP alone makes waves long before it makes them dangerous, and a boss has to be scaled less than the waves before it. **Answered for Greenwood Road 2026-11-14** by the retune above: about ×3 enemy HP from 1-2 on, ×5 for 1-4 and 1-5, with groups up to ×1.6.
- **Late Bloomer** (+2% damage per wave cleared this run) grows across the whole stage (decided 2026-11-13). The measurement above had no tree nodes, so its effect isn't measured yet.
- **The day ladder's retune for hero levels** is paused for this: measured 2026-11-13, a player's expected levels are worth about ×1.2 enemy HP in stage 3, ×1.2–1.25 in stage 4 and ×1.35 or a little more in stage 5 (chapters 1–2 need nothing). Connected sub-stages would replace the per-run tuning, but that finding carries over.

## Narrative Arc / Social Design
**Story (user, 2026-11-13: a story behind each stage, told across its sub-stages).** **Decided (2026-11-13): the tone is light and funny, like an anime, and the speaking heroes get personal names** (Claude's suggested names are placeholders); **enemies and bosses are called by their title** ("the Goblin King" is the name). *Draft,* Claude's, not approved: **[Story_Draft.md](Story_Draft.md)**, "The Long Winter": text only, an intro and ending per stage and one or two lines per sub-stage (39), with a first idea of what is new to play in each. The goblins raid because a Frost Wyrm's winter is driving them south; Ironhold and the Beastfolk join along the way.

Social design **TBD.** Probably light or none. Questions: single-player only? Leaderboards for highest wave?

## Art Direction
- **Tone:** cute / chibi fantasy. Round shapes, big heads, bright colors.
- Must keep heroes and enemies readable on a small portrait screen during busy waves. Chibi proportions help: silhouettes stay clear at small sizes.
- **TBD:** 2D sprites or 2.5D, palette, and how star levels (1★/2★/3★) look on a hero.

## Audio Direction
**TBD.**

## Scope Notes
- Systems-heavy rather than content-heavy. The main work is balancing the economy, hero roster and wave curve.
- **Vertical slice (suggested):** 1 base grid, fence + base HP with 1 fence upgrade, 9 heroes, one for each class + faction pair (3 classes x 3 factions), 3-star merging, shop with reroll/lock, interest bonus, 10 waves ending in a boss.
- Team size and timeline **TBD**.

## Banked Ideas (not decided, not to be built yet)
- **Open field with a crystal instead of a wall** (user, 2026-10-28, banked). Drop the fence: the field is open, the team protects a base or crystal, and every hero moves freely. **TBD whether to adopt it at all.** Notes from the discussion: the code already has most of the pieces (heroes roam and walk to enemies, enemies stop to fight heroes in range, knockouts). What would change: fence HP, repair and the fence upgrade go away or become crystal HP and upgrades; the Guardian and Ironhold fence bonuses and the Tinker's fence abilities need new jobs; "outside row danger" becomes "every hero is always exposed"; placement matters less once everyone walks, so the grid's role needs rethinking (e.g. it sets the starting spot and a leash). Risks: losing the inside/outside choice, which is the game's main placement decision, and a busier field that's harder to read on a phone.

- **Predetermined formations** (user, 2026-10-29, banked). Hand-made wave shapes (a wedge, a wall of tanks, a pincer on both flanks) instead of random spots, maybe per stage or for boss waves. **TBD whether to adopt it.** The random scatter is built behind a switch (`scatter_formation`), so a shape could replace it per wave later.

## Risks & Open Questions
- Coin economy balance: the interest divisor x decides whether saving dominates spending. It needs a spreadsheet model early.
- Classes + factions is the most content-heavy synergy option: every new hero must fit both systems and stay balanced. Start small (e.g. 3 classes, 3 factions).
- Readability of auto combat on a small screen. Heroes fighting outside the wall make the field busier.
- Outside heroes need enemies that stop or slow to fight them, plus targeting rules (who attacks heroes, who walks past). More AI and balance work than a pure wall defense.
- Kill gauge snowball: a strong board kills more and gets more buffs. Keep buffs moderate (choice-adding perks over raw power).
- Coins now go to heroes, rerolls, shop slots, fence repair, commander EXP, and saving for the bonus. The economy spreadsheet is essential early.
- Commander level, the kill gauge, synergies and merging together make a lot of systems for a small team. The vertical slice might start without the kill gauge and add it later.
- The design isn't complete yet. More mechanics are to be discussed.

## Next Steps
- Discuss the remaining open questions (numbers, buff list, theme, classes/factions, stages, the talent lists).
- Model the coin, interest and reroll economy in a spreadsheet for about 20 waves.
- Grey-box prototype: grid placement, one wave spawner, fence HP, shop UI.
