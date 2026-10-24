# Blackjack (working title)
### Game Design Document — v0.1 (Notes captured, most details TBD)

## Logline
*Draft:* Blackjack played exactly the way real casinos run it, with real shoes, real rules and real variants, so the only edge is the one you bring yourself.

## Genre & Platform
- **Genre:** Card game / casino simulation (no real money)
- **Perspective:** 2D table, portrait
- **Platform:** Mobile (iOS/Android), portrait
- **Comparable titles:** **TBD.** To research together.

## Core Pillars
1. **Casino-accurate.** The rules, shoe, shuffling and dealing follow real casino procedure at the core.
2. **Countable, but we don't help.** Because the shoe is dealt realistically, card counting works, but the game never shows a count, hints or a counting trainer. Players who want to count do it on their own.
- More pillars TBD.

## Premise
**TBD.** Possibly none; it's a pure table game.

## Core Gameplay Loop
1. Choose a mode (blackjack variant).
2. Place a bet.
3. Play the hand: hit, stand, double, split, and other options depending on the variant.
4. Settle the hand and continue through the shoe until reshuffle.

## Key Mechanics
- **Multiple modes:** Different real-world blackjack variants. **TBD; research together.** Candidates to look into include classic Vegas Strip, Atlantic City, European (no hole card), Spanish 21, Blackjack Switch, Double Exposure and Pontoon.
- **Realistic shoe:** Number of decks, cut card position (penetration) and shuffle timing like a real casino. These should follow the variant's real rules, never be adjusted against the player.
- **House rules per mode:** **TBD.** Dealer hits or stands on soft 17, blackjack pays 3:2 or 6:5, double after split, surrender, insurance.
- **No assistance:** No visible running count, no strategy hints by default. **TBD:** an optional basic-strategy helper for beginners, or none at all?

## Progression & Structure
**TBD.** Bankroll, table limits, unlocks?

## Narrative Arc / Social Design
**TBD.**

## Art Direction
**TBD.** Cards must be readable, and a player counting needs to be able to see every card dealt.

## Audio Direction
**TBD.**

## Scope Notes
- Rules engine accuracy is the core. Each variant needs a rules config and tests against known payout tables.
- **Suggested vertical slice:** 1 classic variant with a configurable shoe (decks, penetration), full hand options, bankroll.

## Risks & Open Questions
- **RNG and shuffle integrity:** It must behave like a physically shuffled shoe that's dealt to the cut card, not a fresh random card each draw, or counting won't work.
- Store rules for simulated gambling apps (see the Casino doc).
- Which variants to include: research pending.
- Could share a card/table core with the Casino game. Decided: they're separate games for now.

## Next Steps
- Research blackjack variants and their exact rules together.
- Build a rules engine with a shoe model and unit tests for payouts and dealer behavior.
