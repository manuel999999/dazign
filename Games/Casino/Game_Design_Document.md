# Casino (working title)
### Game Design Document — v0.1 (Notes captured, most details TBD)

## Logline
*Draft:* A casino game with two ways to play: Classic, where every bankroll refill is a gamble in itself, and Campaign, where you climb through increasingly exclusive casinos by converting your winnings at steep exchange rates.

## Genre & Platform
- **Genre:** Casino / simulated gambling (no real money)
- **Perspective:** 2D UI-driven tables
- **Platform:** Mobile (iOS/Android), portrait; landscape if a game needs it
- **Comparable titles:** **TBD.** Social casino apps. Which games are in it is TBD.

## Core Pillars
- **TBD.**

## Premise
**TBD.** Campaign casinos may have themes or locations.

## Core Gameplay Loop
**Classic:**
1. Start with limited credits.
2. Play casino games.
3. When credits run out, reset and receive x credits. The amount is random each time, like a lottery.

**Campaign:**
1. Play in the Stage 1 casino.
2. Exchange Stage 1 credits for Stage 2 credits at a rate (e.g. X Stage 1 credits = 1 Stage 2 credit).
3. Unlock and visit the next casino, and repeat.

## Key Mechanics
- **Two modes:** Classic and Campaign.
- **Lottery reset (Classic):** Running out lets you reset for a random credit amount. **TBD:** the range and distribution, and is there a cooldown?
- **Casino stages (Campaign):** Different casinos to unlock and visit. **TBD:** what changes per casino (games available, table limits, theme)?
- **Credit exchange:** Lower-stage credits convert to higher-stage credits at a multiplier. **TBD:** the rates per stage, and whether you can convert back down.
- **Games included:** **TBD.** Slots? Poker? Blackjack and Roulette are planned as separate standalone games; should they also appear here?

## Progression & Structure
**TBD.** How many casinos? What happens when you go broke in Campaign? Is there an end goal?

## Narrative Arc / Social Design
**TBD.**

## Art Direction
**TBD.**

## Audio Direction
**TBD.**

## Scope Notes
- Scope depends heavily on which casino games are included. Each table game is its own ruleset to build and test.
- **Suggested vertical slice:** Classic mode with one game, credit reset lottery; then Campaign with 2 casinos and the exchange.

## Risks & Open Questions
- **Store policy:** Apple and Google have specific rules for simulated gambling apps (age rating, no real-money prizes, extra rules if credits can be bought with money). Monetization should be decided with this in mind.
- What keeps players going in Classic when there's no long-term goal?
- More details are to be decided.

## Next Steps
- Decide which casino games are in scope.
- Define the exchange rates and reset lottery in a spreadsheet.
- Check app store guidelines for simulated gambling before deciding on monetization.
