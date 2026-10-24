# Clode Folder — Game Ideas Workflow

This folder collects original game concepts. Each idea gets its own folder containing one design doc.

## Structure

- `Games/`: games the user plans to work on in the near future (the active list). One folder per game, using a plain working name that's easy to rename once a real title exists.
- `Open/`: earlier concept docs that aren't on the active list (Puddle Pals, Unclaimed, Scrapyard Derby, The Lantern Keeper).
- `cloder.fig`: OpenPencil design file for mockups and illustrations (see "Design mockups" below).
- Each game folder contains exactly one file: `Game_Design_Document.md`. Don't put mockups or other files in game folders.
- Don't nest ideas inside one another or mix multiple concepts into a single doc.

## Active games (`Games/`)

All are portrait mobile games (Unity) unless noted. Docs are at v0.1: the user's notes are captured in the template, and gaps are marked **TBD** with questions to discuss. Anything Claude suggested is labeled "Draft" or "Suggested". Never present a suggestion as a user decision.

1. `Wave Defense Auto Chess`: fenced base at the bottom with a hero grid, waves from the top, auto-chess shop (buy, reroll, lock), saved coins earn a bonus (coins / x). The user said this design isn't complete yet and wants to discuss more. **Currently the main focus; has mockups.**
2. `Auto RPG`: one auto-fighting character, stage maps that unlock by threshold (unlocked doesn't mean survivable).
3. `Maze Tower Defense`: fine grid, 4x4 heroes, must always leave a 1x1 path, practice area for saving maze guides, random obstacles. Reference: Tropical Tower Wars (WC3), single-player.
4. `Casino`: Classic mode (limited credits, lottery-style reset) and Campaign mode (casino stages, credit exchange at multipliers). Portrait, landscape if needed.
5. `Blackjack`: casino-accurate rules and shoe. Card counting is possible but never assisted. Variants still to research together.
6. `Roulette`: multiple variants, to research together.
7. `Spell Wiring Hero`: deep spell building/wiring. Reference: God Eater bullet customization.
8. `Programming Puzzle`: command-based (forward, rotate, loops) puzzle stages.
9. `MU-like RPG`: single-player MU-style (maps, leveling, resets, wings). Earlier decisions: no timed events, about 3 months, queued after Slimebane. Portrait vs. landscape TBD. Keep MU's names, art and story out of it.
10. `Skill Copy RPG`: copy skills and traits from monsters (OP manga inspiration).

The user chose to keep Casino, Blackjack and Roulette as three separate games.

## Game_Design_Document.md template

Each doc follows this section order:

1. **Title + logline** — one-sentence hook at the top.
2. **Genre & Platform** — genre, perspective/camera, target platform(s), 2-4 comparable titles.
3. **Core Pillars** — 2-4 short design principles the concept won't compromise on.
4. **Premise** — a short paragraph of setting/scenario.
5. **Core Gameplay Loop** — numbered steps describing one play cycle start to finish.
6. **Key Mechanics** — bolded mechanic names with 1-2 sentence explanations.
7. **Progression & Structure** — how the game unfolds over its length (chapters, seasons, unlocks).
8. **Narrative Arc / Social Design** — story arc for narrative games, or social/party design for multiplayer games.
9. **Art Direction** — palette, style, and how it serves readability or mood.
10. **Audio Direction** — score approach and key SFX design choices.
11. **Scope Notes** — realistic team size/timeline, and what to prioritize for a vertical slice.
12. **Risks & Open Questions** — honest list of what could go wrong or is undecided.
13. **Next Steps** — concrete first prototyping/playtesting actions.

## Style notes

- Ideas should be genuinely distinct from each other (different genre, scope, or tone), not variations on one theme.
- Favor a clear, ownable hook over generic "it's like X but Y" pitches.
- Keep each doc scoped to something buildable by a small team — call out real risks and scope tradeoffs rather than glossing over them.

## Design mockups (OpenPencil)

- Mockups live in `cloder.fig`, opened in OpenPencil (the user calls the tab "cloder"). Claude can edit it directly through the OpenPencil tools.
- **Draw natively, not by importing SVG.** The user prefers native layers. Use `render` with JSX (`Frame`, `Rectangle`, `Ellipse`, `Text`; props like `w`, `h`, `x`, `y`, `bg`, `color`, `size`, `weight`, `rounded`, `stroke`, `strokeWidth`, `opacity`, `flex="row|col"`, `gap`, `p`, `items`, `justify`, `grow`, `w="fill"`).
- What doesn't work: dashed strokes, and `align` on Text (center text with an auto-layout parent frame instead). Inline `<svg>` inside `render` comes out at the wrong scale.
- For lines and arrows, `import_svg` into a temporary spot, reparent the group into a native transparent frame, then delete the import wrapper. The wrapper frame gets a white fill that would cover the screen.
- Screen size: **1080x1920** portrait. Use the 8px grid, text sizes of 20px and up, and keep text contrast at 4.5:1 or better. Use `describe` to check for warnings.
- Give layers clear, unique names (e.g. "Card - Cannon (selected)", "Cell r2c3").
- Don't export images unless the user asks. Ask before drawing if the target app has no direct connection; the user declined screen control.
- Current contents: "Mobile Screen" frame (1080x1920) holding "Wave Defense - Battle" (HUD, battlefield, fence HP, 6x3 base grid, shop with reroll/lock/upgrade fence). The "Hero Pick" screen was removed by the user. All numbers, hero names and grid size are placeholders.
- pen.app: no connection to it yet. Options are pen.app's own MCP server, or a `.pen` file opened through OpenPencil.

## Git

- Repo remote: `git@github.com:manuel999999/dazign.git` (branch `main`). The user pushes from their own terminal.
- Commit author: `doge999999 <nuel999999@gmail.com>` (set in the repo config).
- `.gitignore` excludes `.DS_Store` and `._*`.
- Only commit or push when the user asks.
