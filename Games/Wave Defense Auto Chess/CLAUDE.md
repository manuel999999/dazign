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
| Source art (Aseprite) | the `*.aseprite` files in this folder (see **Art and assets**) |
| UI mockups | `cloder.fig` at the root of the Clode folder (OpenPencil), frame "Wave Defense - Battle" |
| Godot project | <path, once it exists> |

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
| Base resolution | 1080x1920 (*TBD:* or a low pixel-art base, see **Art and assets**) | Portrait mockups are 1080x1920 |
| Orientation | Portrait | Decided in the design doc |
| Stretch mode / aspect | canvas_items / expand | Taller phones show more battlefield |
| Renderer | *Suggested:* Compatibility | 2D pixel art, widest device range |
| Default texture filter | Nearest | Pixel art must stay crisp |
| Minimum target device | <TBD> | |
| Test framework | <TBD: none / GUT / gdUnit4> | |

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
└── tools/               # headless scripts and editor plugins (@tool)
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
<1. SaveSystem.initialize()
 2. ...>
```

**Every status system announces its starting state once from `initialize()`**, so a listener
that came up first sees it. Signals have no replay.

### Autoloads

Keep them few, and only for things that are truly global. Default set:

- **`Events`**: the game-wide signal bus. Coarse signals, each carrying one coherent snapshot
  (e.g. `gold_changed(new_total: int)`, not three signals for one change). No logic, no state.
- **`Save`**: reads and writes the save file (see **Saving**).
- **`Audio`** *(optional)*: plays music and pooled one-shot SFX on the right mixer bus.

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

### UI

- Build screens from **containers and anchors**, not hand-placed positions, so they adapt to
  every aspect ratio.
- **One `Theme` resource** (`ui/theme.tres`) for fonts, colors and styles; override per node
  only when there's a reason.
- Respect the notch and rounded corners: keep interactive UI inside
  `DisplayServer.get_display_safe_area()`.
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

<Edit for the machine this project is developed on.>

- **There is no Python imaging stack on this machine** (no PIL, numpy, ImageMagick or
  `rsvg-convert`). Node + `@resvg/resvg-js` is the image path. resvg **aborts the process** on a
  Rust panic when a group with opacity lands wholly off-canvas.
- **`sed` on macOS is BSD `sed` and has no `\b`**: a rename looks done and isn't. Use `perl -pi -e`.
- **In `perl -pi -e 's|…|…|'`, `\|` is not a literal pipe.** For any edit touching `||`, use the
  Edit tool.
- **An unmatched glob aborts the whole zsh command line.** Quote patterns like `'*.gd'`.
- **A tiling texture must not vary with absolute position**, or its wrapped copies stop matching.

### Godot traps to check

**None of these has been confirmed in this project.** When one bites or is disproved, reword it
as fact or delete it.

- **`JSON.parse_string` returns every number as a `float`.** Past 2⁵³ (~9×10¹⁵) a 64-bit int loses
  precision. Save large ints as strings (or use `store_var` / `var_to_str`).
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

<Add traps as they are found.>

---

## Art and assets

**All source art is Aseprite pixel art, in this design folder** (`Clode/Games/Wave Defense Auto
Chess/`). These are placeholders: the user plans to revise them, so keep the import pipeline easy
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

Hero and enemy names and roles follow the *Draft* roster in the design doc and are placeholders.
Each file has one layer ("Hero" or "Enemy") and an `idle` tag (2 frames, 400 ms each).

### Getting the art into Godot

- **Never edit exported PNGs.** Change the `.aseprite` file and re-export. The `.aseprite`
  files stay in the design folder; only exports go into the Godot project.
- Export each file as a horizontal sprite sheet plus a JSON data file with tags, into
  `res://assets/art/heroes/` or `res://assets/art/enemies/`, named after the source file
  (e.g. `shield_knight.png` + `shield_knight.json`). With the Aseprite CLI:
  `aseprite -b <file>.aseprite --sheet <out>.png --sheet-type horizontal --data <out>.json --format json-array --list-tags`
  (or the `aseprite` MCP tool `export_spritesheet` with `list_tags`).
- Keep the export in one script (`tools/`), so all art can be re-exported in one go after the
  art is revised.
- Build `SpriteFrames` from the JSON tags (one animation per tag), by script, rather than
  slicing frames by hand in the editor.
- **Pixel-art settings**: default texture filter Nearest, and scale sprites only by whole
  numbers (e.g. 32 px art drawn at 4x = 128 px). *TBD:* render at 1080x1920 and scale each
  sprite 4x, or use a low base resolution (e.g. 270x480, viewport stretch) for perfectly even
  pixels. The second keeps pixels perfect but makes small UI text harder.
- Planned later: back or 3/4 views (sprites currently face the camera), and attack, hit and
  walk animations.

### Mockups

UI layout mockups are in OpenPencil (`cloder.fig`, Clode folder root). They are layout
references only; numbers, names and grid size in them are placeholders.

---

## Scene map

*Planned, not built yet:*

```
Main (main.gd)
├── Systems
│   ├── Economy        # coins, flat income, saving bonus (coins / x)
│   ├── Shop           # 3 slots (upgradeable), reroll, lock, hero odds by commander level
│   ├── Commander      # level + EXP (passive per wave, bought with coins)
│   ├── KillGauge      # fills per kill, growing cost, overflow, banked buff picks
│   ├── Roster         # owned heroes, bench, 3-star merging, synergy counts
│   ├── Waves          # fixed wave list ending in a boss; spawning
│   └── Base           # fence HP, upgrades, repair, base HP, run end
├── World
│   ├── Battlefield    # enemy lane area + outside grid rows
│   ├── Fence
│   ├── HeroGrid       # inside-the-wall grid + outside rows
│   └── <heroes, enemies, projectiles: spawned and pooled>
└── UI (CanvasLayer)
    ├── HUD            # wave, coins, fence/base HP, commander level, kill gauge
    ├── ShopPanel
    ├── Bench
    └── BuffPick       # banked kill-gauge picks, shown after a wave
```

## Systems

<One section per system, in this shape:>

### <SystemName>

- **Does:** <one or two sentences>
- **Owns:** <the state only it changes>
- **Listens to / emits:** <signals>
- **Depends on:** <what initialize() receives>
- **Decisions:** <non-obvious choices and why>

## Not built yet

Everything. The Godot project hasn't been created yet. Follow the **Project setup** checklist
first, then build toward the design doc's vertical slice: one grid, fence + base HP, the 9-hero
roster, shop with reroll/lock, merging, saving bonus, and 10 waves ending in a boss.
