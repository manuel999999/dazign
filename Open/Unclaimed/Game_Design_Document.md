# Unclaimed
### Game Design Document — v0.1 (Concept)

## Logline
You work the night shift at a train station's lost & found: examine forgotten objects, figure out who they belong to from customers' muddled descriptions, and slowly notice that some items belong to no one who has ever lived.

## Genre & Platform
- **Genre:** Deduction / object-inspection puzzle with a slow-burn mystery
- **Perspective:** 2D, fixed first-person view of the counter (customer in front, shelves behind, inspection tray in the middle)
- **Platform:** Mobile (iOS/Android) first, portrait orientation, one-handed play; Steam/Switch port feasible later
- **Comparable titles:** *Papers, Please* (counter-based shift structure), *Unpacking* (objects tell the story), *Return of the Obra Dinn* (deduction by elimination, lightly), *A Little to the Left* (tactile handling of objects)

## Core Pillars
1. **Objects are the story.** There are no cutscenes and almost no narration. Everything you learn comes from handling things: a receipt in a coat pocket, a name scratched off a thermos, a photo tucked behind a phone case.
2. **Deduce, don't guess.** Every match can be proven from evidence on screen. If a player gets one wrong, they should be able to see why afterwards.
3. **Five-minute shifts.** One customer is one complete puzzle, and a session can stop between any two customers. Built for the bus ride.
4. **Quietly uncanny, never horror.** The mystery deepens through small wrong details, not jump scares. The tone stays warm and a little sad.

## Premise
Kestrel Junction is the last stop on the line, and its lost & found is open only at night. You're the new clerk. Commuters, travelers and the occasional odd regular come to the window to describe what they lost, usually badly ("a bag, kind of brown, it had my stuff in it"). Your shelves are full of unclaimed things. Over the weeks a pattern appears: a few items carry dates that haven't happened yet, tickets for trains that don't run, and letters addressed to the clerk who worked here before you.

## Core Gameplay Loop
1. A customer arrives and describes their lost item. The description is partial, and sometimes wrong in a way that reveals something about them.
2. You search the shelves. Each shelf is a small scrollable grid sorted by the date the item came in, so the date they say they lost it narrows the search.
3. You pull candidates onto the inspection tray and examine them: rotate, open, empty pockets, unfold notes, switch on devices, read labels.
4. You ask the customer one or two verification questions, picked from details you found ("What's written inside the lid?"). Their answers rule candidates in or out.
5. You hand over an item, or refuse if nothing matches or the customer is lying about what's theirs.
6. The shift-end ledger scores you on correct returns, wrong returns, and fraudsters turned away, then shows any items that have quietly changed since the last shift.

## Key Mechanics
- **Tactile inspection:** Each item is a 2D object with layered states: a closed bag opens, an inner pocket unzips, a wallet unfolds. Clues sit on different layers, so a careful look pays off and a quick glance misleads.
- **Verification questions:** You only get two questions per customer, built from clues you've actually found. This turns inspection into strategy: which detail best tells the two umbrellas apart?
- **Claimants who lie:** Some customers are opportunists claiming valuable items. They can describe the outside of an object but not what's inside it. Spotting them is a skill that grows with play.
- **The Ledger:** A running notebook that auto-records facts you've confirmed (names, places, recurring regulars). It works as both a deduction aid and a record of the story.
- **Drift items:** A small set of "impossible" objects sits on the shelves. Between shifts they change slightly: a date shifts by a day, a photo gains a figure. Noticing these drives the mystery, and spotting a change is optional but rewarded.

## Progression & Structure
- **4 "weeks" (chapters) of 5 night shifts each, about 20 shifts total.** Each shift has 4-6 customers, so roughly 2-3 minutes per customer.
- New complications arrive each week: Week 1 is basic matching, Week 2 adds liars, Week 3 adds damaged and partial items (a torn ticket, a phone with a cracked screen), and Week 4 brings customers looking for items that haven't been lost yet.
- Unlockable tools widen the inspection options: a UV lamp for hidden ink, a magnifier, a phone charger that lets you power on dead devices, a translation dictionary for foreign tickets.
- Recurring regulars come back across weeks. Returning the right item to a regular advances a small personal side story.
- Replay value comes from shift ratings and a "perfect week" challenge, not from procedural generation, at least for v1.

## Narrative Arc
- **Act 1 (Week 1): The job.** A mundane, charming routine. Regulars are introduced. The first drift item (a station key tag dated next month) appears without comment.
- **Act 2 (Weeks 2-3): The previous clerk.** Letters and items addressed to "M.," the clerk before you, start showing up. Customers mention her as if she still works here. The Ledger fills with contradictions.
- **Act 3 (Week 4): The last train.** The player works out that the lost & found holds things people *will* lose on a train that hasn't arrived yet. The final shifts ask whether you hand these items back early, changing what happens, or keep them shelved. There are 2-3 endings, decided by a handful of clearly signposted choices, not by hidden stats.
- The story is always optional to engage with. A player who only matches items still gets a satisfying puzzle game, and the mystery rewards those who read pockets closely.

## Art Direction
Muted, warm night palette: sodium-lamp amber, deep teal shadows, and paper creams for tags and receipts. The flat 2D illustration is clean and slightly textured, like gouache on card. Items are the most detailed art in the game and must read clearly on a phone screen. Clue text uses a large, legible handwritten font with a pinch-to-zoom fallback. Customers are drawn as stylized busts with 3-4 expression states, which keeps character art cheap while letting them lie visibly (a glance away, a too-quick smile). Drift items get no special highlight. They just look slightly wrong when compared with the previous shift's snapshot.

## Audio Direction
A sparse, late-night score of soft electric piano, distant brushed percussion, and long pads that rise slightly when a drift item is on the tray. The station ambience is the bed: announcements in the distance, rain on the roof, a train arriving every few minutes, which also marks time passing in the shift. Handling SFX are the hero sounds: zips, Velcro, umbrella snaps, paper rustle, a phone buzzing in a coat. They should be foley-quality because the tactile feel is the core pleasure. Customers speak in short murmured gibberish voice lines with text, no full VO.

## Scope Notes
- **Team:** 1-2 developers plus a contract illustrator. Systems are light; content (items, clue layers, customer scripts) is the real workload.
- **Timeline:** About 8-12 months for the full 4-week game. A vertical slice is about 6-8 weeks.
- **Content budget:** About 120-150 unique items and about 60 customer encounters for the full game. Each item is a small authored puzzle, so a reusable item template (layers + clue slots + tags) is essential. Build it as ScriptableObjects in Unity so items can be authored without touching code.
- **Vertical slice priority:** One full shift (5 customers, about 25 shelf items, including one liar and one drift item), the inspection tray with 3+ layer types, the two-question verification system, and the shift-end ledger. If that shift is fun, the rest is content.
- **Cut first if needed:** Unlockable tools beyond the UV lamp, a third ending, and a regulars' side-story beyond 2-3 characters.

## Risks & Open Questions
- **Risk: authored content doesn't scale.** Every item is hand-built. If each takes more than about 2 hours to author and test, the full game becomes a 2-year project. The authoring pipeline needs to be measured during the slice.
- **Risk: small-screen readability.** Tiny text on receipts and labels is core to the design and fights directly against phone screens. This needs early device testing, not just Editor testing.
- **Risk: deduction difficulty is hard to tune.** Too easy and it's a matching game, too hard and players guess. The "provable from evidence" pillar has to be checked by playtesters, not just the designer.
- **Risk: limited replayability** for a premium, authored game on mobile, where players expect free-to-play. The pricing model is undecided.
- **Open question:** Premium (one-time purchase) or free first week with the rest unlocked by one purchase? Ads clash with the mood, so they're probably out.
- **Open question:** Should a wrong return have story consequences (a customer comes back angry later) or only score consequences? Story consequences are richer but multiply authoring cost.
- **Open question:** How explicit should the time-loop / future-items twist become? It's not yet decided whether the ending explains it or leaves it ambiguous.

## Next Steps
- Paper prototype: print 10 items as cards with "inside" details on the back, write 4 customer scripts, and play a shift with a friend acting as the customer. This tests whether the deduction is fun before any code is written.
- Build the inspection tray in Unity with 3 sample items (bag, wallet, phone) to find the right feel for open/rotate/unfold on touch, and test on a real phone.
- Define the item ScriptableObject template, then time how long one new item takes to author end to end.
- Write the full Week 1 outline (5 shifts, all customers, first drift item) to confirm the pacing of the mundane-to-uncanny shift.
- Playtest the slice with 5 people. Track wrong returns and look for where players guessed instead of deduced.
