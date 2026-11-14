# Wave Defense Auto Chess (working title)

A portrait mobile wave-defense auto battler for iOS and Android. A fenced frontier outpost sits at
the bottom of the screen and monster hordes come from the top. Between waves the player buys
heroes from an auto-chess shop (reroll, lock, 3-star merging, class + faction synergies) and
places them on a grid inside the wall or out on the battlefield. Cute chibi fantasy in pixel art.
Portrait, base resolution 1080x1920 (see **Project setup**).

Built with **Godot 4.7 and GDScript 2.0**. The main scene is `res://main.tscn`.

**The design lives in [Game_Design_Document.md](Game_Design_Document.md), next to this file**
(full path: `/Users/SpaceSheep/Documents/Space Sheep/Clode/Games/Wave Defense Auto Chess/Game_Design_Document.md`; use that path if this file is copied into the Godot project). It is the source of truth
for rules and features. It marks every open question **TBD**, and marks Claude's ideas as
*Draft* or *Suggested*: never build a TBD or Suggested rule as if the user had decided it. Ask,
or build it behind a data value that is easy to change, and say so.

**Where things are:**

| What | Where |
|---|---|
| Design doc | [Game_Design_Document.md](Game_Design_Document.md) — `/Users/SpaceSheep/Documents/Space Sheep/Clode/Games/Wave Defense Auto Chess/Game_Design_Document.md` |
| Source art (Aseprite) | the `*.aseprite` files in the design folder (see **Art and assets**) |
| UI mockups | `wave-defense.fig` in the design folder (OpenPencil) — `/Users/SpaceSheep/Documents/Space Sheep/Clode/Games/Wave Defense Auto Chess/wave-defense.fig` |
| Godot project | `/Users/SpaceSheep/Documents/Godot/merge-wave` (git repo) |

**Keep secrets and store identifiers out of this file**: signing keys and their passwords, store
and console ids, ad unit ids, analytics project ids, API keys, account emails. Keep them in the
platform's export settings, an untracked file, or your own notes. This file is committed and read
by every session.

---

## Keeping this file current: read this first

**This file is the handover between sessions. After making changes, update it in the same session,
before reporting the work as done.** A future session starts with nothing but this file, so
anything left out is lost.

Update it when you:

- **Add, rename, move or delete a system, scene, autoload, signal or resource**: fix the scene
  map and the system's note.
- **Change a seam**: the startup order, what gets injected where, how signals are shaped.
- **Make a non-obvious decision**: record the *why*, not just the what.
- **Hit a trap that cost you time**: add it to **Gotchas**. It is the most valuable section here.
- **Finish or abandon a feature**: keep **Not built yet** honest.

Don't record: routine bug fixes with no lasting lesson, tuning values (they live in the inspector
or in data files), or anything plain from the code or git history. **Edit sections in place
rather than appending a changelog**: this file describes how the project *is*. Prune anything that
has become untrue.

If you are unsure whether a change deserves an entry, write a short one.

---

## Godot 4 and GDScript 2.0 only: never Godot 3 syntax

**This project is Godot 4.7 and GDScript 2.0.** Much of the Godot code online, and in AI training
data, is Godot 3, which looks almost the same and no longer works. Never write the left column:

| Godot 3 (wrong) | Godot 4 (right) |
|---|---|
| `export var x`, `onready var y`, `tool` | `@export var x`, `@onready var y`, `@tool` |
| `yield(get_tree().create_timer(1), "timeout")` | `await get_tree().create_timer(1).timeout` |
| `connect("pressed", self, "_on_pressed")` | `pressed.connect(_on_pressed)` |
| `emit_signal("died", x)` | `died.emit(x)` |
| `var x setget set_x, get_x` | `var x: int: set = set_x, get = get_x` (or inline `set(value):`) |
| `scene.instance()` | `scene.instantiate()` |
| `KinematicBody2D`, `move_and_slide(velocity)` | `CharacterBody2D`, set `velocity`, then `move_and_slide()` |
| `Tween` node, `interpolate_property` | `create_tween().tween_property(...)` |
| `rand_range`, `deg2rad`, `stepify` | `randf_range`, `deg_to_rad`, `snapped` |
| `PoolStringArray`, `PoolVector2Array` | `PackedStringArray`, `PackedVector2Array` |
| `Position2D`, `Spatial`, `YSort` | `Marker2D`, `Node3D`, `y_sort_enabled` on a `Node2D` |
| `get_tree().change_scene("res://x.tscn")` | `get_tree().change_scene_to_file("res://x.tscn")` |
| `OS.get_ticks_msec()`, `OS.window_size` | `Time.get_ticks_msec()`, `DisplayServer.window_get_size()` |
| `TileMap` | `TileMapLayer` (`TileMap` is deprecated since 4.3) |

Newer 4.x features are fine to use: typed dictionaries `Dictionary[String, int]` and `.uid` files
(4.4), `@export_tool_button` (4.4), and `@abstract` classes and variadic `...args` functions
(4.5). For anything newer, check the 4.7 docs or test it rather than trusting memory. **When
unsure of an API, look it up for 4.x** (`docs.godotengine.org/en/stable`) or run it. A parse error
near `export`, `yield` or `connect` usually means Godot 3 syntax.

---

## Project setup

### Checklist (new projects)

Godot's new-project defaults rarely fit. Settle these first, then fill in the table below:

- **The name** (`application/config/name`). **Set it before anything saves to `user://`**: that
  folder is named after the project, so renaming later starts on a fresh save.
- **The display** (`display/window/...`): the base viewport size, `stretch/mode = canvas_items`,
  `stretch/aspect = expand` (so taller and wider phones show more instead of letterboxing), and
  `handheld/orientation`. For a phone game, give the desktop window an override size so it fits
  on screen.
- **The renderer.** **Forward+** is the desktop default. **Mobile** is for modern phones,
  **Compatibility** (OpenGL) for the widest range of devices and the web. Choose before writing
  shaders.
- **Physics**: new projects use Jolt for 3D. It doesn't matter for a 2D game.
- **Input map**: define named actions (`Project Settings → Input Map`) and read those, never raw
  keys or buttons in gameplay code.
- **Static typing warnings**: set `debug/gdscript/warnings/untyped_declaration` to Warn (or
  Error).
- **Autoloads**: register only the ones listed under **Architecture**.
- **Version control**: `git init`. Ignore `.godot/` and keep the `.uid` and `.import` files
  committed.

| Setting | Value | Why |
|---|---|---|
| Project name | `merge-wave` | Names the `user://` folder; don't rename once saves exist |
| Base resolution | 1080x1920, desktop window 540x960 | Matches the mockups; UI text stays crisp. Sprites scale 4x (see **Art and assets**) |
| Orientation | Portrait | Decided in the design doc |
| Stretch mode / aspect | canvas_items / expand | Taller phones show more battlefield |
| Renderer | Mobile | User's choice: modern phones only. Compatibility stays the fallback for old Androids or web |
| Default texture filter | Nearest | Pixel art must stay crisp |
| Texture compression | ETC2/ASTC import on | Needed for mobile exports |
| Input map | `primary_press` (left mouse); touch arrives via `emulate_mouse_from_touch` (on) | One input path, no double taps |
| Minimum target device | <TBD> | |
| Test framework | GUT 9.7.1 in `addons/gut/` (the 9.7 line targets Godot 4.7) | Rule-heavy systems are easy to unit test headless |

**Run the tests:** `/Applications/Godot.app/Contents/MacOS/Godot --headless --path . -s addons/gut/gut_cmdln.gd -gexit`
(config in `.gutconfig.json`; tests are `tests/test_*.gd`, `extends GutTest`). GUT fails a test on any
unexpected `push_error` or engine error; use `assert_push_error_count` / `assert_push_warning_count`
for expected ones.

### Folder layout

```
res://
├── main.tscn            # composition root: builds and initializes the systems
├── main.gd
├── autoload/            # global services only (see Architecture)
├── features/            # one folder per feature: its scenes and their scripts together
│   └── <feature>/
├── ui/                  # screens, HUD, reusable widgets, theme.tres
├── scripts/
│   ├── resources/       # Resource types (class_name ...Data)
│   ├── data/            # plain data classes (RefCounted)
│   └── enums/           # shared enums
├── data/                # .tres instances: tuning tables, content definitions
├── assets/              # imported files only: art/, audio/, fonts/, shaders/
├── tools/               # headless scripts and editor plugins (@tool)
├── tests/               # GUT tests (test_*.gd)
└── addons/gut/          # third-party: don't edit
```

A scene and the script attached to it live side by side. A script used by many features goes in
`scripts/`, sorted by what the type *is*.

---

## Working in this project

### The editor and its tools

- **The `godot` MCP server**, when connected: `get_project_info`, `create_scene`, `add_node`,
  `load_sprite`, `save_scene`, `run_project`, `get_debug_output`, `stop_project`,
  `update_project_uids`, `launch_editor`, `get_godot_version`. Use it to build scenes, run the
  game and read its output.
- **Headless scripts** do asset and data work without the editor UI:
  `/Applications/Godot.app/Contents/MacOS/Godot --headless --path . --script res://tools/x.gd`.
  A `--script` file must `extends SceneTree` (or `MainLoop`), work in `_init()` and call
  `quit()`. Save generated data with `ResourceSaver.save`. Keep one-off probe scripts outside the
  project (in a scratch folder), so they are never imported.
- **`.tscn` and `.tres` are plain text.** Prefer the editor, the MCP tools or a headless script;
  hand-edit only small, well-understood changes, then open the scene in the editor to check that
  it still loads.
- **Moving or renaming a script: move its `.gd.uid` with it.** Scenes refer to scripts and
  resources by `uid://`, so a file moved without its uid breaks every reference. The editor's
  FileSystem dock handles this; `update_project_uids` repairs a move made outside it.
- **Editing `project.godot` while the project is open in the editor**: the editor may write its
  own copy back over yours. Reload the project (Project → Reload Current Project) afterwards.

### Code conventions (GDScript)

- Static typing everywhere: `var gold: int = 0`, `func add_gold(amount: int) -> void:`.
- `snake_case` for functions, variables, files and folders; `PascalCase` for `class_name` and
  node names; `CONSTANT_CASE` for constants. Private members take a leading `_`.
- Script member order: `class_name`, `extends`, doc comment, signals, enums, constants,
  `@export` vars, public vars, private vars, `@onready` vars, `_init`/`_ready`/other built-ins,
  public methods, private methods.
- `@export var` for anything set in the inspector. `@onready var` for child node references.
  Prefer `%UniqueName` for nodes a script reaches often, so moving them in the tree doesn't
  break the path.
- Guard-clause early returns over nested conditionals.
- Comment sparingly: a short `#` above a function or tricky block explaining **why**. Use `##`
  doc comments only on public API that will be called from elsewhere.
- **One `class_name` per file.**
- **Give saved enums explicit values and only append to them**: they are saved as ints.
- Debug prints go behind `if OS.is_debug_build():`.

---

## Architecture

Defaults that have worked well. Drop any that don't fit the game, and record why here.

### Layers

1. **Main** (`main.tscn`): the composition root. It owns the systems, hands each one its
   dependencies, and calls `initialize()` on them in a fixed order.
2. **Systems**: plain nodes under Main, one concern each (e.g. economy, waves, spawning, save).
   A system owns its state and is the only thing that changes it.
3. **Entities**: scenes that are spawned and pooled (units, enemies, projectiles, pickups).
   They know as little as possible about systems: they emit signals and are configured from
   outside.
4. **UI**: Control scenes that *show* state and *request* actions. **UI never owns game state**:
   it listens for changes and calls a system method (or emits an intent signal) for input.

**Call down, signal up**: a parent may call methods on its children; a child talks to its parent
or to the wider game only through signals. Avoid `get_parent()` and long `../..` paths.

### Startup order

`_ready()` runs children before parents, and siblings in tree order, so systems that depend on
each other shouldn't rely on it. Main's root calls `initialize()` on each system in dependency
order. Write that order here:

```
 1. Save.load_game()                      # autoload; systems may read Save.data from here on
 2. Board.initialize()                    # layout first: everything positional asks Board
 3. ViewCamera.initialize(board)          # frames the placing view; before Waves announces the phase
 4. Economy.initialize(roster)           # hero income (Fox Merchant); Roster is read later, not now
 5. Commander.initialize()
 6. HeroLayer.initialize(board, roster, shop_panel)  # before Roster, to hear its first announcement;
                                         # the shop panel is the sell area
 7. Roster.initialize(commander, board)
 8. Synergies.initialize(roster)         # counts the board; before Base and Combat, which read it
 9. Shop.initialize(economy, roster, commander)  # rolls offers, deals the starting pick
10. Base.initialize(economy, synergies)   # fence purchases spend coins; armor and repair bonus
11. KillGauge.initialize(economy, base)   # buffs pay coins and change the fence; before Combat
12. EnemyField.initialize(board, base)
13. Combat.initialize(board, roster, enemy_field, synergies, kill_gauge, base)  # before Waves announces the phase
14. Waves.initialize(enemy_field)
then UI requests → systems:
  ShopPanel buy / reroll / lock / exp / slot_upgrade → Shop.buy / reroll / toggle_lock / buy_exp / upgrade_slots
  ShopPanel repair / fence_upgrade → Base.repair / upgrade_fence
  StartPick.picked → Shop.pick_starting;  HeroLayer.sell_requested → Shop.sell
  BuffPick.picked → KillGauge.pick
  Combat.hero_health_changed → HeroLayer.show_health
  ActionBar.start_wave_pressed → Waves.start_wave;  RunEndOverlay.restart_pressed → Main._restart
```

All calls are in `main.gd` `_ready()`, explicit and typed (no loop over nodes). UI connects to
`Events` in its own `_ready()`, which runs before Main's, so it sees every starting announcement.
A World node that listens to `Events` connects in `initialize()`, so it must come before the
system it listens to. Main is also the one owner of scene changes: `_restart()` reloads the scene.

**Every status system announces its starting state once from `initialize()`**, so a listener
that came up first sees it. Signals have no replay.

### Autoloads

Keep them few, and only for things that are truly global. Registered:

- **`Events`** (`autoload/events.gd`): the game-wide signal bus. Coarse signals, each carrying one
  coherent snapshot (e.g. `coins_changed(total: int)`, not three signals for one change). No logic,
  no state. Current signals: `phase_changed(Phase.Id)`, `wave_changed(wave, wave_count)`,
  `coins_changed(total)`, `commander_changed(level, experience, exp_to_next)`,
  `base_changed(fence_hp, fence_max_hp, base_hp)`, `kill_gauge_changed(kills, kills_needed, banked_picks)`, `buff_pick_offered(options: Array[BuffData], more_after)`,
  `roster_changed(units: Array[HeroUnit], board_count, board_cap)` (listeners treat `units` as
  read only), `run_ended(won: bool)`, `enemy_killed(enemy: EnemyData)` (emitted by EnemyField;
  KillGauge listens), `wave_cleared(wave)` (from Waves
  after every wave except the last; Economy pays out, Commander adds EXP and Shop rolls, all
  before the phase returns to SHOP),
  `shop_changed(offers: Array[HeroData], locked, reroll_cost, exp_cost, slot_upgrade_cost)` (null
  offer = bought; slot cost -1 = maxed), `starting_pick_offered(heroes)` (empty = picked), and `fence_shop_changed(repair_cost,
  repair_amount, upgrade_cost, upgrade_hp)`. `synergies_changed(states)`: one dictionary per synergy, in
  order (`name`, `count` of unique heroes on the board, `breakpoints`, `tier`; 0 = inactive).
  `fence_shop_changed`'s `repair_amount` already includes the Ironhold bonus.
  `commander_changed`'s `exp_to_next` is -1 at the max level.
  The file wraps them in `@warning_ignore_start("unused_signal")`, since they're emitted elsewhere.
- **`Save`** (`autoload/save.gd`): reads and writes the save file (see **Saving**).
- **`Audio`** *(optional, not added yet)*: plays music and pooled one-shot SFX on the right mixer bus.

Game rules don't live in autoloads. A system that only one scene uses belongs in that scene.

### Data

- **Content and tuning live in `Resource`s** (`.tres` in `data/`), with their types in
  `scripts/resources/`. Designers change numbers in the inspector, not in code.
- **Resources loaded from disk are shared and treated as read-only.** Keep per-instance runtime
  state (current HP, cooldowns) in the node or a plain data class, or `duplicate()` once at
  set-up.
- When a tool or spreadsheet owns the numbers, **generate the `.tres` with a script** in
  `tools/`, and never hand-tune a generated resource.

### Scenes and flow

- **One owner for scene changes** (Main, or a small router): screens ask for a change, they don't
  call `change_scene_to_file` themselves.
- **Pooled objects reset per use, not in `_ready`**, and every delayed action aimed at one
  carries an id that changes each time it is reused, so a stale action never hits the object's
  next use.
- **Few `_process` functions**: one per system that moves many things, never one per bullet,
  coin or number.

### Saving

- Save to `user://`, as a versioned dictionary (`{"version": N, ...}`).
- **Write to `<name>.tmp` and rename it over the live file.** Opening the save for writing
  truncates it at once, so a process killed mid-write (normal on mobile) loses the save.
- **Save on `NOTIFICATION_APPLICATION_PAUSED` / `NOTIFICATION_APPLICATION_FOCUS_OUT`.** Quit
  callbacks don't reliably run on mobile.
- **A version bump must migrate, never reject**, and a file newer than the build is left on disk
  untouched.

As built (`autoload/save.gd`, tested in `tests/test_save.gd`): `user://save.json`, one
`Save.data` dictionary that systems read and write by key. It's written with
`JSON.stringify(JSON.from_native(data))` and read back with `JSON.to_native`, which keeps ints exact.
Bump `Save.VERSION` and add a step to `_migrate()` when the layout changes. A newer file sets a
read-only flag so `save_game()` does nothing. An unreadable file is copied to `save.json.corrupt`
and the game starts fresh.

### UI

- Build screens from **containers and anchors**, not hand-placed positions, so they adapt to
  every aspect ratio.
- **One `Theme` resource** (`ui/theme.tres`) for fonts, colors and styles; override per node
  only when there's a reason.
- Respect the notch and rounded corners: keep interactive UI inside
  `DisplayServer.get_display_safe_area()`. It is in screen pixels, so convert it to canvas units,
  and apply it only on mobile (`ui/hud.gd` `_fit_safe_area()` shows how).
- Give HUD controls `mouse_filter = STOP` and read game input in `_unhandled_input`, so a press on
  the UI never reaches the game. Use `IGNORE` on decorative controls, or they swallow presses
  silently.

### Mobile performance

- Test on the minimum target device early, not only in the editor.
- **Keep texture sizes multiples of 4**, so GPU texture compression (ETC2/ASTC) can apply.
- Pack sprites that draw together, avoid allocating in per-frame code, and pool anything spawned
  often.

---

## Gotchas

### This machine and its shell

- **Aseprite is the Steam build.** `~/Applications/Aseprite.app` is only a launcher (`open
  steam://…`), not a CLI. The real binary is
  `~/Library/Application Support/Steam/steamapps/common/Aseprite/Aseprite.app/Contents/MacOS/aseprite`.
- **There is no Python imaging stack on this machine** (no PIL, numpy, ImageMagick or
  `rsvg-convert`). Node + `@resvg/resvg-js` is the image path. resvg **aborts the process** on a
  Rust panic when a group with opacity lands wholly off-canvas.
- **`sed` on macOS is BSD `sed` and has no `\b`**: a rename looks done and isn't. Use `perl -pi -e`.
- **In `perl -pi -e 's|…|…|'`, `\|` is not a literal pipe.** For any edit touching `||`, use the
  Edit tool.
- **An unmatched glob aborts the whole zsh command line.** Quote patterns like `'*.gd'`.
- **A tiling texture must not vary with absolute position**, or its wrapped copies stop matching.

### Godot traps to check

**These haven't been confirmed in this project yet.** When one bites or is disproved, reword it
as fact and move it to **This project**, or delete it.

- **GDScript `int` and `float` are 64-bit, but `Vector2` is 32-bit.**
- **A `Tween` lives until it finishes or its node is freed.** Pooled nodes are hidden, not freed,
  so kill their tweens when they go back to the pool.
- **Shared resources are shared**: changing a material or `LabelSettings` used in many places
  changes all of them. Use `resource_local_to_scene` or `duplicate()` once at set-up.
- **Touch and mouse**: use `emulate_mouse_from_touch` *or* handle `InputEventScreenTouch`, not
  both, or a tap counts twice.
- **`await` on a node that gets freed** never resumes, and code after it is silently skipped.
  Check `is_instance_valid()` after awaiting anything tied to a node's lifetime.

### This project

- **Plain JSON turns every number into a `float`**, and past 2⁵³ an int loses precision. Use
  `JSON.from_native` / `JSON.to_native` (as Save does), which keeps ints exact and refuses objects
  by default.
- **`JSON.parse_string` logs an engine error on bad input**, and GUT fails a test on any unexpected
  engine error. To parse something that may be invalid, use `JSON.new().parse(text)` and check the
  returned `Error`.
- **`--check-only --script` doesn't load autoloads**, so any script that uses `Events` or `Save`
  reports "Identifier not found". That's a false alarm. To check those scripts, run the game
  headless instead: `Godot --headless --path . --quit-after 30`.
- **Screenshots without a phone**: `Godot --path . --write-movie <scratch>/f.png --fixed-fps 10
  --quit-after 3 [scene]` writes PNG frames at the window size (540x960), so they show slightly
  soft pixels.
- **Playtesting by script** (a `--script` driver kept in the scratch folder): the driver
  **must not name game classes** (`Board`, `Roster`…) in its types. A `--script` file compiles
  before the autoloads exist, so any class that uses `Events` fails to compile. Leave those vars
  untyped, and load `main.tscn` on the first `process_frame`, not in `_init()`. To fake taps,
  convert positions to window positions and send them with `Input.parse_input_event`. For a
  **world** point (a cell, the bench) that's `root.get_final_transform() * (root.canvas_transform
  * pos)`, which goes through the camera; for a **UI** point (a button's rect) it's
  `root.get_final_transform() * pos` alone. **Headless, `DisplayServer.window_get_size()` is (0, 0)**,
  so a scale computed from it puts every tap at (0, 0). For `reload_current_scene()` to work, start
  with `change_scene_to_file`, not `root.add_child`.
- **Read pointer positions from the event** (`(event as InputEventMouse).position`, in screen
  or viewport units), not `get_global_mouse_position()`, so HeroLayer works the same for real
  taps and for injected ones. **The World has a camera**, so convert with
  `get_canvas_transform().affine_inverse() * pos` before asking Board (`HeroLayer._to_world`).
  UI rects such as the sell area are in screen units, so compare those with the raw position.
- **A typed array in `.tscn`** is written `prop = Array[ExtResource("<script id>")]([ExtResource("a"), ...])`,
  and needs an `ext_resource` for the element's script (see `main.tscn` `waves` and Shop `heroes`).
- **A drag that ends over UI**: the press is read in `_unhandled_input`, so a tap on a button never
  starts a drag. The motion and release must be read in **`_input`** (and marked handled), or
  the release lands on the Control under the pointer (the shop panel) and the drag never ends.
- **Signals run synchronously, so state can change under a loop.** One kill → `enemy_removed` →
  Waves ends the wave → `phase_changed` → Combat clears its arrays, all inside the call that
  dealt the damage. Code that loops over its own array and calls out (damage, spending, spawning)
  must not assume the array survives the call. Collect first, act after the loop (see
  `Combat._tick_projectiles`; `test_combat.gd` covers it, and needs **two** shots in flight to
  reproduce).
- **Don't list `res://` folders in game code.** In an exported build the files are remapped, so
  `DirAccess.get_files_at("res://data/...")` returns `.remap` names, not the `.tres` you expect.
  Content lists (Shop `heroes`, Synergies, KillGauge `buffs`, Waves) are therefore exported arrays
  set in `main.tscn`; add a new hero or buff there. Tools and tests may list folders (they run in
  the editor).
- **A test `Synergies.new()` has no synergy data.** Load the `.tres` files into `synergies` before
  `initialize`, or every bonus is silently 0 (see `test_abilities.gd`).
- **`breakpoint` is a GDScript keyword** (it pauses the debugger), so `for breakpoint in …` is a
  parse error ("Expected loop variable name after for"). A parse error in one `class_name` file
  shows up as "Could not resolve class X" in every file that uses it; check the file itself with
  `--check-only --script`.
- **`queue_free()` doesn't detach a child until the end of the frame.** When rebuilding a list of
  child controls and then indexing `get_child(i)`, call `remove_child()` first (see
  `ShopPanel._rebuild_cards`).

---

## Art and assets

**All source art is Aseprite pixel art, in the design folder**
(`/Users/SpaceSheep/Documents/Space Sheep/Clode/Games/Wave Defense Auto Chess/`). These are placeholders: the user plans to revise them, so keep the import pipeline easy
to re-run.

| File | What | Size | Tags |
|---|---|---|---|
| `shield_knight.aseprite` | Hero: Kingdom Guardian (melee) | 32x32 | idle |
| `crossbow_squire.aseprite` | Hero: Kingdom Ranger | 32x32 | idle |
| `hedge_wizard.aseprite` | Hero: Kingdom Mage | 32x32 | idle |
| `leaf_archer.aseprite` | Hero: Sylvan Ranger | 32x32 | idle |
| `bloom_druid.aseprite` | Hero: Sylvan Mage | 32x32 | idle |
| `sapling_treant.aseprite` | Hero: Sylvan Guardian (melee) | 32x32 | idle |
| `cannoneer.aseprite` | Hero: Ironhold Ranger | 32x32 | idle |
| `rune_smith.aseprite` | Hero: Ironhold Mage | 32x32 | idle |
| `hammer_brawler.aseprite` | Hero: Ironhold Guardian (melee) | 32x32 | idle |
| `enemy_goblin_scamp.aseprite` | Enemy: fast, walks past melee heroes | 32x32 | idle |
| `enemy_imp.aseprite` | Enemy: tiny, comes in swarms | 32x32 | idle |
| `enemy_orc_bruiser.aseprite` | Enemy: tanky, stops to fight melee heroes | 32x32 | idle |
| `enemy_bog_shaman.aseprite` | Enemy: damage aura | 32x32 | idle |
| `enemy_troll_rammer.aseprite` | Enemy: ignores heroes, hits the fence | 32x32 | idle |
| `boss_goblin_king.aseprite` | Boss: attacks heroes outside, summons Scamps | 48x48 | idle |
| `chapel_cleric`, `royal_snarer` `.aseprite` | Heroes: Kingdom Support, Kingdom Trapper | 32x32 | idle |
| `grove_singer`, `thorn_weaver` `.aseprite` | Heroes: Sylvan Support, Sylvan Trapper | 32x32 | idle |
| `tinker`, `bomb_sapper` `.aseprite` | Heroes: Ironhold Support, Ironhold Trapper | 32x32 | idle |
| `hawk_eye`, `owl_sage`, `bear_warden`, `fox_merchant`, `badger_digger` `.aseprite` | Heroes: Beastfolk Ranger, Mage, Guardian, Support, Trapper | 32x32 | idle |

Hero and enemy names and roles follow the *Draft* roster in the design doc and are placeholders.
Each file has one layer ("Hero" or "Enemy") and an `idle` tag (2 frames, 400 ms each).

**The 11 newer heroes are Claude's drafts**, for the user to redraw. They were drawn by
`tools/draft_heroes.lua` (an Aseprite script: shapes plus an automatic 1 px outline, the
existing palette and proportions, and a 2-frame bob). It refuses to overwrite a file, so a hero
the user has redrawn is safe: `aseprite -b --script-param out="<design folder>" --script
tools/draft_heroes.lua [--script-param only=<name>]`. To check drafts before saving them, draw
into a scratch folder and make a contact sheet with `aseprite -b a.aseprite b.aseprite …
--sheet out.png --sheet-type rows --scale 4`.

### Getting the art into Godot

- **Never edit exported PNGs.** Change the `.aseprite` file and re-export. The `.aseprite`
  files stay in the design folder; only exports go into the Godot project.
- **Re-export everything after the art changes** (three commands, from the project root):
  ```
  tools/export_art.sh
  /Applications/Godot.app/Contents/MacOS/Godot --headless --path . --import
  /Applications/Godot.app/Contents/MacOS/Godot --headless --path . --script res://tools/build_sprite_frames.gd
  ```
  `export_art.sh` exports every `.aseprite` in the design folder as a horizontal sheet + JSON
  (`--format json-array --list-tags`). Files named `enemy_*` and `boss_*` go to
  `assets/art/enemies/`, the rest to `assets/art/heroes/`. Override the paths with `ASEPRITE` and
  `ART_SRC`. A new art file needs no code change.
- `build_sprite_frames.gd` writes `data/sprite_frames/<name>.tres`: one `SpriteFrames` per sheet,
  one animation per tag (forward/reverse/pingpong; it loops unless the tag has a repeat count). The
  FPS comes from the shortest frame, and longer Aseprite frames become relative durations. These
  files are **generated, never hand-edited**. The `--import` pass must come first, or the PNGs
  don't load.
- `tools/art_preview.tscn` (run it on its own) shows every SpriteFrames at 4x, to check an
  export.
- **Pixel-art settings**: default texture filter Nearest, and scale sprites only by whole
  numbers. **Decided: render at 1080x1920 and draw sprites at 4x** (32 px → 128 px, boss 48 →
  192), so UI text stays crisp. Pixels stay even as long as sprites sit on whole-pixel positions.
- Planned later: back or 3/4 views (sprites currently face the camera), and attack, hit and
  walk animations.

### Mockups

UI layout mockups are in OpenPencil (`wave-defense.fig`, in the design folder next to the design
doc). They are layout references only; numbers, names and grid size in them are placeholders.
**The file is empty for now** (as of 2026-10-27, confirmed by the user): no mockup frames exist
yet. Build the UI from the design doc until mockups are added.

---

## Scene map

Nodes marked *(planned)* don't exist yet. Scripts live in `features/<feature>/` with a
`class_name` matching the node, and Main reaches them by `%UniqueName`.

```
Main (main.gd)
├── Systems
│   ├── Economy        # coins, flat income, saving bonus (coins / x)
│   ├── Shop           # 3 slots (upgradeable), reroll, lock, hero odds by commander level
│   ├── Commander      # level + EXP (passive per wave, bought with coins)
│   ├── KillGauge      # fills per kill, growing cost, overflow, banked buff picks
│   ├── Roster         # owned heroes, bench, 3-star merging, synergy counts
│   ├── Waves          # round phase, current wave; wave list ending in a boss; spawning
│   ├── Synergies      # class + faction counts (unique heroes on the board) and active bonuses
│   └── Base           # fence HP, upgrades, repair, base HP, run end
├── World (Node2D, y-sorted)
│   ├── Board          # features/board: layout + placeholder drawing (lane, outside row, fence, grid, bench); z -1
│   ├── ViewCamera     # features/camera: Camera2D easing between the placing and battle views
│   ├── HeroLayer      # features/heroes: a HeroView per owned hero; drag & drop → Roster
│   ├── EnemyField     # features/enemies: spawns, pools, moves and hurts every Enemy in one _process
│   └── Combat         # features/combat: hero attacks, projectiles and hit flashes in one _process; z 5
└── UI (CanvasLayer)
    ├── HUD            # ui/hud.gd: wave · phase, coins, fence/base HP, heroes on board/cap, level/EXP, synergy chips
    ├── ActionBar      # ui/action_bar.gd: "Start wave" button (bottom, 160 px; Board leaves room)
    │   (HUD and ShopPanel sit in a VBoxContainer `TopStack`, so the panel always starts below
    │    the HUD, however many rows of synergy chips it has). With 3 rows of chips
    │    the panel would start to cover the outside row
    ├── ShopPanel      # ui/shop_panel.gd: over the (empty) lane during SHOP: hero cards, Reroll, Lock, +EXP, +Slot, Repair, Fence+; also the sell area
    ├── StartPick      # ui/start_pick.gd: modal "choose your first hero" at run start
    ├── RunEndOverlay  # ui/run_end_overlay.gd: win/lose + Restart
    └── BuffPick       # ui/buff_pick.gd: modal kill-gauge reward, 1 of 3, one per banked pick
```

`ui/hero_card.gd` (`HeroCard`, a Button built in code) is the card used by both the shop and the
starting pick. It shows a portrait (frame 0 of the hero's first animation), the name, and a
caption, tinted by tier. The HUD has no background yet, so its text overlaps enemies at the top
of the lane.

The bench is drawn by Board in world space, not as UI, so one coordinate space covers every drag
between the bench and the grid.

**Board layout (world space, fixed).** Top to bottom: the enemy lane (y 0 .. `lane_length`
1312), the outside row, the fence, the 5×3 inside grid, a gap, and the bench, centered in
`world_width` 1080. Cells are 192 px, so a 4x sprite (128 px) has room. The layout doesn't depend
on the screen; only the camera framing does. Board draws the ground far past the layout
(`GROUND_OVERDRAW`), so a zoomed-out or wide view never shows the clear color.
`view_center(zoom, view_size)` frames the bench just above the action bar (`bottom_margin`, in
screen px), with everything above it filling the screen. ViewCamera uses it for both views.
`spawn_y()` sits just above the battle view's top edge (higher on tall phones), so enemies never
pop into view. A bench wider than 5 slots (5 × 192 = 960 px) would overflow the 1080 placing view.
Board coordinates: a `Vector2i(col, row)` where rows
`0 .. outside_rows-1` are outside the fence and the rest are inside. A bench slot is an index.
`Board.NO_CELL` / `-1` mean "not over a slot". Grid size and the single outside row are
**decided** (design doc); the bench size of 5 is a placeholder.

Shared types:
- `Phase` (`scripts/enums/phase.gd`): `Phase.Id.SHOP = 0`, `COMBAT = 1`
- `HeroClass` and `Faction` (`scripts/enums/`): Ranger/Mage/Guardian and Kingdom/Sylvan/Ironhold, 0..2
- `HeroUnit` (`scripts/data/hero_unit.gd`): one owned hero (id, data, stars, bench_index or cell);
  only Roster changes it

Content (`data/`, hand-tuned `.tres`; the types are in `scripts/resources/`):
- `HeroData` in `data/heroes/`: **20 heroes, 5 classes × 4 factions** (decided). Each has an
  id, name, class, faction, **tier (1–3) and cost**, max HP and SpriteFrames. The placeholder
  tiers spread classes and factions across tiers: tier 1 has 7 heroes (Shield Knight, Leaf
  Archer, Rune Smith, Royal Snarer, Grove Singer, Tinker, Badger Digger), tier 2 has 7 (Sapling
  Treant, Cannoneer, Hedge Wizard, Chapel Cleric, Thorn Weaver, Owl Sage, Fox Merchant), and
  tier 3 has 6 (Hammer Brawler, Crossbow Squire, Bloom Druid, Bomb Sapper, Hawk Eye, Bear
  Warden). Cost = tier. Base stats are set per class: Supports have 0 damage, so they don't
  attack, and Trappers have a light ranged attack. **Abilities are data fields**, mixed per hero:
  - **attack:** range, damage, interval, projectile speed (0 = melee), splash radius;
  - **on hit:** slow, stun, `root_duration`, `poison_dps` with `poison_duration`, and
    `max_hp_damage` (a share of the target's max HP);
  - **support:** `heal_amount` with `heal_interval` and `heal_radius`, `neighbour_attack_speed`,
    `fence_repair_per_second`, `coins_per_wave`.

  Which hero has which ability is in the design doc (*Draft*).
- `EnemyData` in `data/enemies/`: 6 enemies, with hp, speed, fence damage and interval, base damage
- `SynergyData` in `data/synergies/`: the six class and faction bonuses (see Synergies)
- `BuffData` in `data/buffs/`: the 8 placeholder kill-gauge buffs (see KillGauge)
- `WaveData` in `data/waves/`: a list of `SpawnGroup`s (enemy, count, delay, interval), all
  counted from the start of the wave

All the numbers are placeholders. The 10 waves in `data/waves/wave_01..10.tres` are a
placeholder ramp (imps → scamps → bruisers and shamans → trolls → the Goblin King with escorts);
the real wave list is TBD. `EnemyData` also has an optional summon (enemy, count, interval) and threats to
heroes: an aura (`aura_dps`, `aura_radius`) and a hero attack (`hero_damage`, range, interval).

## Systems

Every system owns its state and announces it from `initialize()`. Every `@export` number is a
**placeholder**, because the real values are TBD in the design doc. Tests for the rules are in
`tests/`, one file per system.

### KillGauge

- **Does:** each `enemy_killed` adds one kill. When the gauge is full it banks a pick, and the
  overflow carries over. Each fill needs `kills_growth` more kills than the last (decided: the
  cost grows and overflow carries; the numbers, 10 then +5, are placeholders). Picks are
  **banked during a wave and offered in the shop phase** (decided), **one after another,
  choosing 1 of `choices` 3** (Suggested, built as a placeholder). `pick(i)` applies the buff
  and offers the next banked pick. Picked buffs last the whole run (TBD, placeholder).
- **Buffs** (`BuffData` in `data/buffs/`, 8 *Suggested* placeholders, listed in the design doc).
  A buff can raise a hero stat for the run (`stat` + `stat_value`, using
  `SynergyData.Effect`; it applies to **every** hero and is read by Combat through
  `stat_bonus(effect)`). It can add fence armor for the run (`Base.add_fence_armor`), and it can
  do one-off things: coins (`Economy.add`), `fence_heal` (`Base.heal_fence`), and `fence_max_hp`
  (`Base.add_fence_max_hp`). The offer is a random draw of distinct buffs, and buffs can be
  picked again (they stack).
- **Owns:** `kills`, `banked_picks`, `picked`, `offer`, and the fill count.
- **Emits:** `kill_gauge_changed(kills, kills_needed, banked_picks)` and
  `buff_pick_offered(options, more_after)` (empty options = nothing waiting).
- **Depends on:** Economy and Base. Base doesn't depend on KillGauge: buffs push their fence
  armor into Base instead, which avoids a dependency loop.
- **UI:** `ui/buff_pick.gd` (`BuffPick`, a modal, solid-styled cards) and a gauge line in the
  HUD ("Kill gauge 5/15 · 1 reward ready").

### Economy

- **Does:** coins. `can_afford`, `spend` (refuses and takes nothing when short), `add`. On
  `wave_cleared` it pays `wave_income` plus `saving_bonus()` plus `hero_income()`. The bonus is
  `coins / saving_divisor` rounded down, capped at `saving_cap` (0 = no cap), and is worked out on
  the coins saved before the income lands. `hero_income()` is the `coins_per_wave` of every hero
  on the board (the Fox Merchant). `initialize(roster)` takes the Roster for that; it's optional,
  so tests can leave it out.
- **Emits:** `coins_changed`. The placeholders are 3 starting coins, 5 income, x = 10 and a cap
  of 5.

### Commander

- **Does:** level and EXP. `add_experience` levels up as many times as the EXP covers, using
  `exp_to_next_by_level` (its size + 1 is the max level), and drops EXP past the max. Gains
  `passive_exp_per_wave` on `wave_cleared`. Bought EXP comes through Shop. `board_slots()` comes
  from `board_slots_by_level` (placeholder: 3 at level 1).
- **Emits:** `commander_changed(level, experience, exp_to_next)` (`exp_to_next` is -1 at max).

### Shop

- **Does:** the offers (`starting_slots` = 3, decided), with extra slots bought for
  `slot_upgrade_costs` (the array's size is how many can be added). Each offer picks a tier by
  `tier_weights_by_level[commander level]`, then a random hero of that tier, with no shared pool
  limit. It rolls at the start and on every `wave_cleared` unless locked. **Lock** keeps the
  offers through any number of waves until the player unlocks or rerolls; **reroll** costs
  coins and lifts the lock. These lock details are my choice; the design doc only says that a
  lock carries the offers over.
  `buy(slot)` needs the coins and `Roster.can_accept`. `buy_exp()` turns `exp_cost` into
  `exp_per_purchase` EXP. `sell(unit_id)` refunds `sell_value()` (cost × 3^(stars−1), the
  placeholder "full value of every copy"). The **starting pick** is `starting_choices` (3) random
  tier-1 heroes, and `pick_starting(i)` adds one for free. It only trades in the SHOP phase.
- **Owns:** every coin price: heroes, reroll, slots, EXP and refunds.
- **Depends on:** Economy, Roster and Commander (the level, for odds and EXP).

### Roster

- **Does:** keeps the owned heroes and where each stands, and moves them. `move_to_cell` and
  `move_to_bench` swap with whatever hero is in the target slot. Moves are refused during combat,
  off the board, or when a bench→empty-cell move would go past `board_cap()`. A swap between bench
  and board keeps the count, so it's allowed at the cap. `add_hero` puts a new 1★ copy on the
  bench and **merges automatically** (decided): 3 copies of a hero at the same star level become
  one copy a star higher, cascading up to 3★. The copy kept is one on the board if there is one,
  so a merge never raises the board count. `can_accept` also allows a purchase with a **full
  bench** when it completes a merge; the new copy merges straight in without ever taking a slot.
  `remove_unit` is used for selling.
- **Owns:** `units: Array[HeroUnit]`.
- **Listens to / emits:** `phase_changed` (locks every change during combat) and
  `commander_changed` (the cap follows the level, so it re-announces); emits `roster_changed`
  after every change.
- **Depends on:** Commander (cap) and Board (`has_cell`, `bench_size`).
- **Decisions:** any hero can go in any cell, inside or outside (design doc).

### Base

- **Does:** fence HP, then base HP. `damage_fence` and `damage_base` clamp at 0, and base HP
  reaching 0 emits `run_ended(false)` once. The fence never heals on its own. Two purchases,
  shop phase only: `repair()` restores `repair_amount` HP for `repair_cost`, up to max (decided:
  repair works in chunks, and a broken fence can be repaired); `upgrade_fence()` adds
  `upgrade_hp` to max **and** current HP, for the next entry of `upgrade_costs` (decided: the
  slice's one upgrade is max HP). Placeholders: 200 fence HP, 20 base HP, repair +50 HP for 2
  coins, upgrade +100 HP for 5, 8 or 12 coins.
- **Owns:** `fence_hp`, `fence_max_hp` (it starts at `starting_fence_max_hp` and grows with
  upgrades), `base_hp`, and the fence prices. The fence prices live in Base, not Shop, so later
  Ironhold "cheaper repairs" bonuses have one place to change.
- **Synergies:** every enemy hit on the fence deals `fence_armor()` less (Guardian), but never
  less than `min_fence_damage` 1, a placeholder rule so armor can't make Imps harmless.
  `repair_hp()` is `repair_amount` × (1 + Ironhold bonus). Base re-announces its prices on
  `synergies_changed`, so the repair button shows the current amount.
- **Emits:** `base_changed`, `fence_shop_changed(repair_cost, repair_amount, upgrade_cost,
  upgrade_hp)` (`upgrade_cost` is -1 when maxed), and `run_ended(false)`.
- **Depends on:** Economy and Synergies.

### Waves

- **Does:** the shop/combat phase and the wave counter. `start_wave()` (from the action bar)
  builds a time-sorted spawn schedule from the `WaveData` and feeds it to EnemyField from
  `_process`. The wave ends when the schedule is empty and no enemy is left: back to SHOP, or
  `run_ended(true)` after the last wave. The wave count is `waves.size()`.
- **Listens to / emits:** EnemyField's `enemy_removed`, and `run_ended` (stops for good); emits
  `phase_changed`, `wave_changed`, `run_ended(true)`.
- **Depends on:** EnemyField.

### EnemyField (World)

- **Does:** spawns enemies at a random x in the grid's columns above the screen, and moves them
  all down. They stop just above the fence (`fence_stand_off`) and hit it every
  `attack_interval`. Once the fence is broken they walk on to the bottom of the inside grid, deal
  `base_damage` and are removed. **No enemy stops for heroes**: decided for now, kept for later.
  Enemies are pooled: `Enemy.reset()` runs on each use and bumps `use_id`, so a projectile aimed
  at an earlier use can tell (CLAUDE's pooling rule).
- **Hurting:** `hurt(enemy, hit: Hit)`. `Hit` (`scripts/data/hit.gd`) is one attack's whole
  effect, worked out by Combat when the attack is made; `Hit.of(n)` is a plain hit. Damage is
  `damage` + `max_hp_damage` × the enemy's max HP. At 0 HP the enemy is removed and
  `Events.enemy_killed` fires, and the same goes for a poison kill. Effects:
  - a **stun** stops movement, fence attacks and attacks on heroes;
  - a **root** stops only movement: a rooted enemy still hits the fence and heroes;
  - a **slow** scales speed;
  - **poison** deals `poison_dps` every second in whole points (`poison_carry` keeps the
    fraction).

  Stuns and roots keep the longest time; slows and poisons keep the strongest value and the
  longest time. Tints, in order of priority: yellow for stunned, tan for rooted, blue for
  slowed, green for poisoned. The HP bar shows once an enemy is hurt.
- **Fence line:** an enemy stops at the fence only when it **crosses** the line that frame. An
  enemy already past a fence that a Tinker repairs mid-wave keeps walking, instead of snapping
  back to the fence.
  Queries: `first_in_range(point, reach)` (the enemy furthest down the field) and
  `in_radius(point, radius)`, which allocates a new array per call. That's fine at this scale;
  revisit if waves get big.
- **Summons:** an `EnemyData` with `summon`, `summon_count` and `summon_interval` calls in that
  many of the summoned enemy every interval while it lives, near its position. The first comes
  one interval after it appears. Stunned summoners don't summon. The Goblin King summons 2
  Scamps every 6 s (placeholder). Summons count toward the wave, so it only ends once they're
  dead too. `spawn_at(data, point)` spawns at a given point; `spawn(data)` uses a random lane x.
- **Depends on:** Board (positions) and Base (fence state, damage). Stops when `run_ended` fires.

### Combat (World)

- **Does:** while the phase is COMBAT, every hero on the board counts down its cooldown, then
  attacks the enemy within `attack_range` that is closest to the base. "First" targeting is a
  placeholder; the rule isn't in the design doc. With `projectile_speed` 0 the hit lands on the
  spot (Guardian melee); otherwise a homing projectile flies to the target. If the target dies
  first, the projectile finishes its flight to where the target was: splash still lands there, a
  single-target shot fizzles. `splash_radius` > 0 hits everyone around the point (Mage splash,
  Guardian cleave). Range is measured from the hero's cell center.
- **Owns:** per-hero cooldowns, projectiles and hit flashes, held as plain dictionaries and
  drawn in `_draw()` with no nodes (circles for shots, fading rings for hits). It clears them all
  on every phase change. That clear can happen **in the middle of Combat's own loop** (see the
  re-entrant signals gotcha), so landed shots are collected first and resolved after the loop.
- **Depends on:** Board, Roster (which heroes are on the board), EnemyField, Synergies, KillGauge
  and Base (fence repair).
- **Stars:** damage × `star_damage[stars - 1]` (placeholder 1.0 / 1.8 / 3.2). Range and speed
  don't scale yet.
- **Synergies and buffs**, read per attack through `_bonus` (`Synergies.hero_bonus` +
  `KillGauge.stat_bonus`):
  - damage × (1 + DAMAGE);
  - the cooldown is `attack_interval` / (1 + `attack_speed_bonus(unit)`), which adds up
    ATTACK_SPEED, the Supports in the 8 cells around the hero (`neighbour_attack_speed`), and
    the Beastfolk ramp (RAMP_ATTACK_SPEED × the whole 10 s steps of `_wave_time`);
  - splash radius × (1 + SPLASH);
  - a CRIT_CHANCE roll doubles the damage, and a crit's flash is red;
  - root and poison durations × (1 + CONTROL_DURATION);
  - poison dps × the star multiplier.

  `_make_hit` builds the Hit when the attack is made; a projectile carries it.
- **Supports** (`_tick_support`): heroes with 0 damage don't attack. `heal_amount` × stars ×
  (1 + HEALING) goes every `heal_interval` to the standing hero within `heal_radius` with the
  lowest share of its HP left; only hurt heroes count, so in practice outside heroes. Heals show
  as a green ring. A knocked-out hero can't be healed. `fence_repair_per_second` × (1 + HEALING)
  repairs the fence through `Base.heal_fence`, in whole points.
- **Danger to heroes:** `_tick_threats` runs every frame of a wave. **Only heroes in the outside
  row can be hurt.** That's my reading of the design doc's "exposed", now in the doc as
  *Suggested*. An enemy with `aura_dps` burns every exposed hero within `aura_radius` (the Bog
  Shaman: 10 dps, 170 px). An enemy with `hero_damage` hits the nearest exposed hero within
  `hero_attack_range` every `hero_attack_interval` (the Goblin King: 45 per 2 s, 320 px), with a
  red flash. **Stunned enemies do neither**, so Guardian stuns protect the outside row; keep that
  in mind when testing. Hero HP is `HeroData.max_hp` (Ranger 120, Mage 100, Guardian 300) ×
  `star_hp[stars - 1]`, kept as floats so auras can deal fractional damage.
- **Knockout** (decided): at 0 HP a hero is knocked out for the rest of the wave. It stops
  attacking, can't be targeted, and fades to grey. It's back at full HP on the next phase
  change. It still counts for synergies and for the board cap.
- **Emits:** `hero_health_changed(unit_id, hp_ratio, knocked_out)`, a local signal that Main
  wires to `HeroLayer.show_health`. On every phase change it re-emits full HP for anyone hurt.
- **Not built:** Guardian *skills* (for now stun and slow are on-hit effects of the basic attack).

### HeroLayer (World)

- **Does:** keeps one `HeroView` per `HeroUnit` (created and freed on `roster_changed`) and
  positions it from Board. `HeroView` draws one gold pip per star, an HP bar once hurt, and a
  grey, paused look while knocked out (`HeroLayer.show_health`). HeroLayer turns a
  `primary_press` drag into `Roster.move_to_cell` / `move_to_bench`, or into `sell_requested`
  when the hero is dropped on the visible sell area (the ShopPanel), and snaps the hero back
  when a move is refused. It owns no game state. Pointer positions go through the camera
  (`_to_world`); the sell-area check uses the raw screen position.

### Synergies

- **Does:** counts, for every `SynergyData`, the **unique heroes on the board** that count
  toward it. Two copies of a hero count once, and bench heroes don't count (decided). It turns
  each count into a tier with the **breakpoints 2 and 4** (decided for the 20-hero roster; it
  was 2 and 3 for the first 9). `hero_bonus(hero, effect)` sums the active values of the
  synergies a hero counts toward; `team_bonus(effect)` sums a team-wide effect.
- **The nine (approved by the user; the values are placeholders, in `data/synergies/`):**

  | Synergy | Effect | Values (tier 1 / tier 2) |
  |---|---|---|
  | Ranger | DAMAGE | +20% / +45% |
  | Mage | SPLASH | +25% / +50% |
  | Guardian | FENCE_ARMOR, team-wide | 1 / 2 |
  | Support | HEALING (heals and fence repairs) | +40% / +100% |
  | Trapper | CONTROL_DURATION (roots, poisons) | +30% / +70% |
  | Kingdom | ATTACK_SPEED | +15% / +35% |
  | Sylvan | CRIT_CHANCE (double damage) | 15% / 30% |
  | Ironhold | REPAIR_BONUS, team-wide | +50% / +100% |
  | Beastfolk | RAMP_ATTACK_SPEED, per 10 s of the wave | +4% / +8% |

  A class or faction bonus reaches only heroes of that class or faction. Guardian and Ironhold
  are fence bonuses and apply to the whole team.
- **Listens to / emits:** `roster_changed` → recount → `synergies_changed(states)`.
- **Depends on:** Roster (for the first count).
- **UI:** `ui/hud.gd` shows a chip per synergy with at least one hero on the board ("Guardian
  2/4"): dim while inactive, gold once active, orange at the top tier.
- **Adding one:** make a new `SynergyData` `.tres` (kind, class or faction, breakpoints, effect,
  values) and add it to the Synergies node in `main.tscn`. A new kind of effect needs a value
  in `SynergyData.Effect` (append only) and code where it applies.

### ViewCamera (World)

- **Does:** the two views (decided by the user). The **placing view** (SHOP) uses
  `Board.placing_zoom` 1.0, so sprites are at 4x and cells are big for dragging, framed so the
  bench sits above the action bar. The **battle view** (COMBAT) uses `Board.battle_zoom` 0.75,
  an exact 3x, framed to show the whole lane on 9:16 and more on taller phones. On
  `phase_changed` it eases zoom and position together (`transition_time` 0.45 s, sine
  in-out). It snaps to the right view at start-up and on screen-size changes.
- **Decisions:** zoom steps keep whole-pixel sprite scales, which is why the battle view is 0.75
  and not something like 0.7. The ShopPanel still overlays the top of the screen, because in the
  placing view that part of the lane is empty during the shop phase. After a lost run it stays
  in the battle view, behind the overlay.
- **Depends on:** Board (zooms and `view_center`).

## Not built yet

Done: project setup, the art pipeline, the autoloads, and the grey-box round:
- the board layout (lane, 1 outside row, fence, 5×3 grid, bench)
- dragging heroes between the bench and the grid, with the board cap
- waves that spawn enemies, which hit the fence and then the base
- a win/lose overlay with Restart
- auto-combat: Ranger shots, Mage splash, Guardian cleave with stun or slow, enemy HP and deaths
- the shop loop: a starting pick (1 of 3), a 3-slot shop with tiers and odds by level, reroll,
  lock, +slot, buying EXP, selling by dragging onto the shop, automatic 3-star merging with star
  damage, and per-wave income + saving bonus + passive EXP
- fence repair (chunks) and the max-HP fence upgrade
- 10 placeholder waves ending in the Goblin King, who summons Scamps
- the placing view and battle view camera
- synergies: 3 classes + 3 factions, unique heroes on the board, breakpoints 2/3
- outside-row danger: hero HP, the Bog Shaman's aura, the Goblin King attacking outside heroes,
  knockouts until the next wave
- the kill gauge and buff picks (8 placeholder buffs)
- 20 heroes (5 classes × 4 factions): Support and Trapper classes, the Beastfolk faction, 11
  new heroes with data-driven abilities (heal, neighbour aura, fence repair, coins, root, poison,
  max-HP damage), 2/4 breakpoints, and pixel-art drafts

**Every core mechanic in the design doc is now built**: the slice plus synergies, outside-row
danger and the kill gauge. The user wants to discuss and research (numbers, the buff list, open
TBDs) **after** the core is done (2026-10-27). The numbers are all placeholders. A scripted player wins all 10 waves and the fence
barely takes a hit, so the balance is far too easy, and enemies rarely live long enough to
threaten the outside row (a staged boss wave against one lone outside hero does knock it out).
That's expected until the economy spreadsheet and wave curve exist.

Next (the user picks the order, and said "whatever you recommend" on 2026-10-27). The user also
said on 2026-10-27: no phone tests for now, keep building the game.
- **Discussion and research with the user**: the TBD numbers, the buff list, and the open
  questions in the design doc.
- **Feedback**: coin and income popups, a HUD background, merge, level-up and knockout effects,
  a "boss wave" banner.
- **Balance pass**: harder waves, so the fence, repairs and the outside row matter.
- Enemies that stop to fight melee heroes (deferred by the user).

**Layout (user, 2026-10-27).** The grid used to fill too much of the map. The user chose **a
placing view and a battle view** (built: see ViewCamera). On 9:16 the battle view gives the lane
about half the screen instead of ~37%. Still open: whether the placing view should also give more
room. Fallback options if the play-test says so: smaller cells (144 px, ~+240 px of lane), sprites
at 3x on 128 px cells, a bench drawer, or a visually shrunk grid. Not built: letting the player
scroll up during the shop phase to preview the next wave.

Not handled yet: saving a run in progress (Save exists, but no system writes to it).
