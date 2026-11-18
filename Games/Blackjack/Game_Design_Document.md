# Blackjack (working title)
### Game Design Document — v0.1 (Notes captured, most details TBD)

## Logline
*Draft:* Blackjack played exactly the way real casinos run it, with real shoes, real rules and real variants, so the only edge is the one you bring yourself.

## Genre & Platform
- **Genre:** Card game / casino simulation (no real money)
- **Perspective:** 2D table, portrait
- **Platform:** Mobile (iOS/Android), portrait
- **Engine:** Godot 4.7 (decided 2026-11-17). Project: `/Users/SpaceSheep/Documents/Godot/blackjack`.
- **Comparable titles:** **TBD.** To research together.

## Core Pillars
1. **Casino-accurate.** The rules, shoe, shuffling and dealing follow real casino procedure at the core.
2. **Countable, but we don't help.** Because the shoe is dealt realistically, card counting works, but the game never shows a count, hints or a counting trainer. Players who want to count do it on their own.
- More pillars TBD.

## Premise
**TBD.** Possibly none; it's a pure table game.

## Core Gameplay Loop
*Decided 2026-11-18 and built in the Godot project the same day. Mockups: `black-jack.fig`, pages "Game Loop" and "UI Theme (Night)".*

1. **Main menu:** one card per mode (blackjack variant). Each mode is saved on its own.
2. **Enter a mode.** A saved mode asks **Continue** (the exact shoe, credits and any hand in progress, for casual players) or **New game** (a fresh shuffle, and credits reset to a new buy-in: 300 free or 5,000 with an ad; for card counters). A mode never played goes straight to the buy-in.
3. **Buy-in:** credits are free. 300 for free, or 5,000 for watching an ad (ad feature comes later). The same offer appears again every time credits run out, and taking it starts a new game (see below).
4. **Shuffle:** a shuffle animation plays in the middle of the table for a new shoe, and again whenever the cut card has come out (the hand in progress finishes first, as in a casino).
5. Place a bet.
6. Play the hand: hit, stand, double, split, and other options depending on the variant.
7. Settle the hand, save, and continue through the shoe until the cut card.

**Decided 2026-11-18**
- **New game resets the credits:** the player goes back to the choice of 300 free or 5,000 with an ad.
- **New game is final only once the credits are taken (decided 2026-11-19):** choosing New game opens the buy-in; the old game is replaced when the player takes the free or ad credits. Going back to the tables from the buy-in, or closing the app there, keeps the old game, so a mistaken tap on New game costs nothing.
- **Leaving in the middle of a hand:** the hand is saved and the player comes back to it on Continue.
- **Out of credits ends the saved game** (2026-11-18): when a round ends and the credits can't cover the minimum bet, the mode's save is deleted, so the menu shows it as new. The buy-in still appears at once. **Buying in starts a new game (decided 2026-11-19, replacing "continues the same shoe"):** the last round's cards are swept away, the shoe is shuffled fresh with the shuffle animation, the credits are set to the buy-in, and there is no bet to repeat. The new game is saved again.
- The shuffle animation runs about 2 seconds (gather, riffle twice, cut card, to the shoe). Modes not built yet show on the menu as dimmer "Coming soon" tiles.
- Watching an ad is a placeholder in the build for now (it grants the 5,000 at once).

## Key Mechanics
- **Multiple modes:** Different real-world blackjack variants. **Decided:** one core game, and each variant is a rules setting picked by the player.
  - **Standard-rules modes: added 2026-11-19** (the user asked for every mode Claude could add with confidence, standard-rules modes first; they are the most played). Each follows the published rule set of that name (source: the Wizard of Odds table of the Microgaming blackjack games, read 2026-11-19; Atlantic City's splitting rules also match New Jersey's regulation N.J.A.C. 13:69F-2.11). All pay blackjack 3:2, offer insurance at 2:1, allow one split of aces, and count any two ten-value cards as a pair.

    | Mode | Decks | Dealer on soft 17 | Hole card | Double on | Double after split | Split up to | Split aces | Surrender | House edge |
    |---|---|---|---|---|---|---|---|---|---|
    | Vegas Strip | 4 | Stands | Yes, dealer peeks | Any two cards | Yes | 4 hands | One card each | No | 0.35% |
    | Atlantic City | 8 | Stands | Yes, dealer peeks | Any two cards | Yes | 4 hands | One card each | Late | 0.35% |
    | European | 2 | Stands | No hole card | Hard 9 to 11 | No | 2 hands | May be hit | No | 0.40% |
    | Vegas Downtown | 2 | Hits | Yes, dealer peeks | Any two cards | Yes | 4 hands | One card each | No | 0.38% |
    | Single Deck | 1 | Hits | Yes, dealer peeks | Hard 9 to 11 | No | 2 hands | One card each | No | 0.31% |

    In European, a dealer blackjack takes doubled and split bets too (there is no hole card to peek at). House edge is with perfect basic strategy, from the same source.
  - **No 6:5 table for now: decided 2026-11-19** (the user left the choice to Claude). The placeholder "Six-to-Five H17" had invented rules and was removed. A real 6:5 table can be added later as its own mode, under a name that tells players it pays less.
  - **Mode info popup: decided and built 2026-11-19.** Each playable tile on the menu has an "i" button that opens a popup with a short description of the mode and every house rule in words (decks, payout, dealer rule, hole card, doubling, splitting, surrender, insurance, bet limits). The tile itself shows two lines that tell the tables apart: decks with the blackjack payout, and what the dealer does on soft 17. *Draft:* the descriptions are Claude's wording. "Coming soon" tiles have no "i" yet.
  - **Double Exposure: added 2026-11-19.** Both of the dealer's cards are dealt face up. In return the dealer wins every tie, except a tied blackjack, which the player wins, and a blackjack pays even money. There is no insurance or surrender. Its rules vary by casino; *Draft (Claude's choice, not yet reviewed):* the Atlantic City set from the Wizard of Odds table of Double Exposure rules: 8 decks, dealer stands on soft 17, double on hard 9 to 11 and soft 19 or 20, double after split, one split only. House edge about 0.66%. Not in the source, standard practice assumed: one card on split aces, and any two ten-value cards count as a pair.
  - **Spanish Blackjack: added 2026-11-19.** The game casinos sell as "Spanish 21". **Decided 2026-11-19: the mode is called "Spanish Blackjack"**, because "Spanish 21" is a registered US trademark of Masque Publishing (checked that day); unlicensed versions of the game use this name. The trademarked name must not appear anywhere in the game. Rules (source: the Wizard of Odds page on the game):
    - Six decks with the four 10s taken out of each (48 cards a deck; Jacks, Queens and Kings stay).
    - A player 21 always wins, even against a dealer 21. A player blackjack beats a dealer blackjack and pays 3 to 2.
    - Bonus 21s: five cards pay 3 to 2, six pay 2 to 1, seven or more 3 to 1. 6-7-8 or 7-7-7 pays 3 to 2 in mixed suits, 2 to 1 in one suit, 3 to 1 in spades. Suited 7-7-7 against a dealer 7 pays a super bonus of 1,000 credits, or 5,000 on bets of 25 and up. No bonus on doubled or split hands.
    - Double on any number of cards, and after a split. After doubling, the player may give the hand up and lose only the original bet (the "double-down rescue"); in the game the doubled hand waits for Stand or Surrender.
    - Split up to four hands, aces included; split aces can be hit and doubled. Late surrender. Insurance pays 2 to 1.
    - *Draft (Claude's choices among the casino variations, not yet reviewed):* the dealer stands on soft 17 (house edge about 0.40%; hitting soft 17 would be 0.76%), no redoubling, and no Match the Dealer side bet (that name is also the trademark owner's).
    - *To revisit with stake levels:* the super bonus is a fixed number of credits, so it will need scaling when bets grow tenfold.
  - **Swap Blackjack: added 2026-11-19.** The game casinos sell as "Blackjack Switch", which is a registered US trademark (checked 2026-11-19), so the game must not use that name. *Draft:* "Swap Blackjack" is Claude's working name; **the name is TBD** until the user confirms it. The US patent on the mechanics is listed as expired on 2025-05-10 (Google Patents; not legal advice). Rules (source: the Las Vegas rules on the Wizard of Odds page for the game, six decks, house edge about 0.58%):
    - The player is dealt two hands with the same bet on each, and before playing may swap the second cards of the two hands. A blackjack made by swapping counts as 21.
    - A dealer 22 is a push against every hand still in, except a blackjack.
    - Blackjack pays even money. A dealer blackjack beats everything except a player blackjack, which pushes; the dealer checks for it before the swap.
    - The dealer hits soft 17. Double on any two cards and after a split. No surrender.
    - *Assumed, not in the source:* insurance is offered and covers both hands; split aces get one card each.
    - *Deliberate difference:* at most four hands on the table in all. Casinos allow four per starting hand (eight in all), which does not fit a phone screen.
  - **Pontoon: added 2026-11-19.** British Pontoon as casinos deal it (the user left the choice between this and Australian Pontoon, which is close to Spanish Blackjack, to Claude). "Pontoon" is a traditional generic name. Rules (source: the default rule set on the Wizard of Odds Pontoon page, shared by several casino software makers; 8 decks, house edge about 0.38%):
    - Both of the dealer's cards are face down; the player sees neither until the dealer plays. The dealer checks for a pontoon first, and a dealer pontoon wins at once.
    - A pontoon (an Ace with a ten-value card) pays 2 to 1, and still counts after a split.
    - A five-card trick (five cards without going over 21, whatever the total) beats everything except a pontoon and pays 2 to 1. The dealer stops on five cards too.
    - The dealer wins every tie, a tied pontoon included. The dealer hits soft 17.
    - The player may not stick (stand) under 15.
    - Buy (double) on two to four cards, once a hand, and keep twisting (hitting) afterwards.
    - Split cards of the same rank only, up to three hands, aces included; split aces can be twisted and bought.
    - No insurance, no surrender.
    - The table uses the game's own words: Twist, Stick, Buy and Pontoon.
  - **All nine modes are in.** Nothing is left on the "coming soon" list.
- **Realistic shoe:** Number of decks, cut card position (penetration) and shuffle timing like a real casino. These should follow the variant's real rules, never be adjusted against the player. *Draft, 2026-11-19 (Claude's estimate of usual casino practice, not sourced):* the cut card comes out after 75% of a 4- or 8-deck shoe, 60% of two decks and 50% of a single deck.
- **House rules per mode:** see the table under "Multiple modes".
- **Betting with chips: decided 2026-11-18** (chips are the only way to bet; the - and + buttons go away and there is no setting to switch). Mockup approved 2026-11-18: `black-jack.fig`, page "Chip Betting (draft)". Built in the game 2026-11-18 (stake levels not yet).
  - A rack of four chips sits at the bottom of the table where the - and + buttons are, next to Deal: **10 (red), 50 (green), 100 (black), 500 (purple)** (values decided 2026-11-18). Every value is a multiple of 10, so 3:2 and 6:5 payouts stay whole numbers.
  - Tap a chip to add it to the bet. It slides to the bet spot.
  - **The bet is a scattered pile of chips** (the user's idea, 2026-11-18; mockup v3 approved 2026-11-18). Each chip lands on the bet spot a little off-centre and turned, like chips tossed on the felt. A pill under the spot shows the total ("Bet 280").
  - **Chips merge** so the pile never gets too big: five 10s become a 50, two 50s become a 100, five 100s become a 500. The pile then never holds more than nine chips.
  - During play the same pile sits under the hand, smaller. A double grows the pile to the doubled bet; after a split each hand has its own pile.
  - Tap the pile to take the last chip back. A small Clear button beside the total empties the spot. Deal is off until the bet reaches the table minimum.
  - A chip in the rack is dimmed when adding it would pass the player's credits or the table maximum.
  - **The credits drop the moment chips go out (decided 2026-11-19):** on Deal, and likewise on Double, Split and Insurance, the credits shown go down at once, before the cards move. Winnings are added when the result shows. A buy-in shows its credits at once too.
  - **After a round (decided 2026-11-18):** the bets are removed (lost, or paid into the credits) and the bet spot is empty for the next round. While the spot is empty, Deal is replaced by **Repeat bet** (showing the amount), which puts last round's bet back on the spot as chips; the player can add to it, then deals. It is greyed out when the credits can't cover it. Placing a chip brings Deal back; clearing the spot brings Repeat bet back. Betting never waits for the last round's cards: they slide away while the player already places chips.
  - **Chip art:** *Draft v2, 2026-11-18* (the user asked for chips that look like poker chips). Seen from above: a coloured disc with six ivory stripes around the rim, a thin ivory ring, and the value in ivory on a slightly darker centre. The small chip beside the credits uses the same look without a value.
  - **Chips that grow with the player's credits: decided 2026-11-18 (stake levels; the player chooses when to move up).** Each level is ten times the last: 10 to 500 with chips 10/50/100/500; 100 to 5,000 with 100/500/1,000/5,000; 1,000 to 50,000 with 1,000/5,000/10,000/50,000. The rack always shows the level's four chips. A level opens when the credits reach 100 times its minimum bet (10,000 for level 2, 100,000 for level 3); the game then offers it and the player decides, as a casino lets you pick your table. **Open (to design):** where the move-up choice appears, moving back down, the colours of the bigger chips, and whether the level is saved per mode.
- **No assistance:** No visible running count, no strategy hints by default. **TBD:** an optional basic-strategy helper for beginners, or none at all?

## Progression & Structure
- **Credits: decided 2026-11-18.** Each mode has its own credits and its own saved shoe. Credits are free (300, or 5,000 with an ad), with no real money.
- **Table limits: TBD.** *Suggested 2026-11-19:* limits belong to the stake level, not to the mode, so every mode has the same limits: 10 to 500 at the first level (a 1 to 50 spread, like a real 10-to-500 table), then 100 to 5,000 and 1,000 to 50,000. The build uses 10 to 500 in every mode today.
- Unlocks, goals: **TBD.**

## Narrative Arc / Social Design
**TBD.**

## Art Direction
Cards must be readable, and a player counting needs to be able to see every card dealt.

- **Cards: decided 2026-11-18.** Draft v1 in `black-jack.fig` (page "Cards"): a classic casino deck on ivory, red and black suits, traditional pip layouts, large top-left index (Roboto Slab), simple framed J/Q/K monograms (Playfair Display), burgundy-and-gold back. In-game cards fan so each earlier card's corner index stays visible.
- **Rest of the look** (table layout, felt, chips, buttons, UI): **TBD.** The "Table Preview" page in the same file is only a mock to judge the cards in context.
- **Table background: decided 2026-11-18.** A casino-felt look: a vignette (bright centre, dark edges) over textured felt. All six colours are kept (Classic Green, Emerald Teal, Royal Blue, Casino Red, Royal Purple, Midnight Charcoal; "Backgrounds" page of `black-jack.fig`) and the player picks one in a setting, one felt for the whole game. Built in the game 2026-11-18 (a shader).
- **UI theme: night mode, decided 2026-11-18** ("it should feel like Black Jack"). Mockups: "UI Theme (Night)" page, approved 2026-11-18; the theme is applied to the prototype table screen. The felt changes and the UI does not: panels and buttons are near-black (#0D0F12 at 80%) with gold (#E2B65B) outlines and titles, ivory (#F3EBD8) text, one solid-gold main action per screen; dialogs are almost solid over a dimmed table; playing cards stay ivory. Modes not built yet are dimmer panels (replacing the face-down card idea); settings opens from a gear.
- **Table action buttons: decided 2026-11-18.** Round buttons, each with a symbol and a word (option B on the "Action Buttons (draft)" page of `black-jack.fig`): Hit and Stand are the big pair in the middle, Double (×2) and Split smaller on either side, and Surrender a small flag at the right end at tables that offer it. Each action has its own colour (Hit green, Stand grey, Double amber, Split blue, Surrender red; added 2026-11-18). They look like physical push buttons: a face lit from above on a thick darker edge, which sinks when pressed (chosen from the "Button Depth" samples, 2026-11-18). An action the hand can't take is dimmed in place, never hidden. The row sits well above the banner ad so players don't tap the ad by accident.
- **Banner ad space: decided 2026-11-18.** Every screen keeps an empty strip at the bottom for a banner ad (150 px on the 1080-wide design, a standard 50dp banner; the real height will come from the ad SDK). Ads themselves come later. The ad network will be **AdMob** (2026-11-18).
- **Safe area: decided 2026-11-18, to build later.** All UI stays inside the phone's safe area (clear of the notch, status bar and home bar); the felt still fills the whole screen. The banner ad sits at the bottom, above the bottom safe-area inset.
- *Suggested, not decided:* a four-colour deck option, illustrated court cards.

## Audio Direction
**TBD.**

## Scope Notes
- Rules engine accuracy is the core. Each variant needs a rules config and tests against known payout tables.
- **Suggested vertical slice:** 1 classic variant with a configurable shoe (decks, penetration), full hand options, bankroll.

## Risks & Open Questions
- **RNG and shuffle integrity:** It must behave like a physically shuffled shoe that's dealt to the cut card, not a fresh random card each draw, or counting won't work.
- Store rules for simulated gambling apps (see the Casino doc).
- The name of the two-hand mode ("Swap Blackjack") is not confirmed. The rule choices Claude made inside each mode (marked *Draft* above) are not yet reviewed.
- Could share a card/table core with the Casino game. Decided: they're separate games for now.

## Next Steps
- *Started 2026-11-17:* Godot prototype with a rules engine, shoe model and GUT tests. Five standard-rules modes are in (2026-11-19).
- Research the variants that need new mechanics and their exact rules together.
- Build a rules engine with a shoe model and unit tests for payouts and dealer behavior.
