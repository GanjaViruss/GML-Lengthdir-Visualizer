# GML Lengthdir Visualizer — GameMaker lengthdir_x / lengthdir_y Generator

> Stop guessing where `lengthdir_x` and `lengthdir_y` land. Click, drag, see it, copy the GameMaker code.

**by [GanjaViruss](https://github.com/GanjaViruss) & Claude Opus 4.8 & Sonnet 4.6**

🔗 **[Live tool](https://ganjaviruss.github.io/GML-Lengthdir-Visualizer/)** 
Part of [GML Tools](https://github.com/GanjaViruss/GML-Tools)

---

A free, open-source **visual `lengthdir` generator** for **GameMaker** (GML). `lengthdir_x(len, dir)` / `lengthdir_y(len, dir)` are powerful but hard to picture in your head — this tool shows you *exactly* where the point lands and hands you ready-to-paste GameMaker Language code.

No install, no dependencies, no server — one `.html` file you open in your browser. Works offline.

---

## What it does

Place points around an object, drag them, and get clean `lengthdir` code:

```gml
var _muzzle_x = x + lengthdir_x(114, image_angle + 5);
var _muzzle_y = y + lengthdir_y(114, image_angle + 5);
```

Perfect for: gun muzzles, shell ejection points, held items, light sources, orbit points, attach points for skeletal-style animation, rotating collision offsets — anything positioned relative to an object's angle.

---

## Features

- **Visual canvas** — click to add a point, drag to move it, see length & direction update live
- **Drop in your own sprite** — upload any sprite as a backdrop (pixel-perfect, no blur), set the origin on your pivot
- **Built-in example sprite** — a top-down soldier so you can start instantly
- **Sprite rotates with facing** — turn the facing arrow and the whole sprite + points rotate together, exactly like `image_angle` in game
- **Movable origin** — drag the origin cross onto your object's pivot; everything is measured from there
- **Draggable facing arrow** — grab it and rotate, or use the slider
- **Chained points (parent/child)** — Shift+click makes a point relative to another point, output chains correctly: `_tip_x = _muzzle_x + lengthdir_x(...)`
- **Collision boxes & lines** — mark a point as a **Line** and output `collision_line` / `collision_rectangle` (or `draw_line` to debug). One set of points works at *every* angle — no more hard-coding a version per `image_angle`. Perfect for rotating hitboxes, car doors, turret arcs.
- **Custom angle variable** — use `image_angle`, `aim_dir`, `cannon_angle` or any variable you have; it's added to each point's direction
- **Pan & zoom** — mouse wheel / pinch / on-screen buttons; middle-mouse or drag to pan
- **Snap to grid** — 4 / 8 / 16 / 32 px, great for pixel-art precision
- **Snap to 15°** — clean angles
- **Undo** (Ctrl+Z) and **duplicate** (Ctrl+D)
- **Auto-save** — your points and settings persist between visits (in your browser)
- **Mobile friendly** — full touch support, lock button to let the page scroll
- **Copy** the generated GML with one click

---

## Usage

1. Open the tool (or `index.html`) in your browser.
2. Upload your sprite (or use the built-in soldier).
3. Drag the white **origin** cross onto your object's pivot.
4. **Tap** empty space to add a point — drag it onto the spot you want (e.g. the gun muzzle).
5. **Shift+tap** to add a child point chained to the active one.
6. Tick **Add direction** and type your angle variable (`image_angle`, `aim_dir`, …).
7. Copy the generated GML.

**Controls**

| Action | Desktop | Mobile |
|---|---|---|
| Add point | tap empty | tap empty |
| Add child point | Shift+tap | "+ Child" button |
| Move point / origin / arrow | drag | drag |
| Pan | drag empty / middle-mouse | drag empty / two fingers |
| Zoom | mouse wheel / + − buttons | pinch / + − buttons |
| Undo | Ctrl+Z | "↶ Undo" button |
| Duplicate | Ctrl+D | "Dup" button |
| Delete point | Delete | "×" in list |
| Let page scroll | — | 🔒 Lock button |

---

## How lengthdir works

`lengthdir_x(len, dir)` and `lengthdir_y(len, dir)` answer: **"if I move `len` pixels in direction `dir`, how far do I move on X and Y?"**

GameMaker directions: `0°` = right, `90°` = up, `180°` = left, `270°` = down (counter-clockwise, because screen Y points down).

To place something that rotates with your object, add the object's angle to the direction:

```gml
var _muzzle_x = x + lengthdir_x(48, image_angle);
var _muzzle_y = y + lengthdir_y(48, image_angle);
```

## Rotating collision boxes

A hitbox that turns with your object (car doors, swinging melee, turret arcs) usually means hard-coding a separate version for `image_angle == 0`, `90`, `180`, `270`. With lengthdir + `image_angle` you don't — **one set of points covers every angle.**

Mark a point as a **Line**, set the output to `collision_line`, and you get:

```gml
var _door_x = x + lengthdir_x(36, image_angle + 153);
var _door_y = y + lengthdir_y(36, image_angle + 153);
var _door_tip_x = _door_x + lengthdir_x(80, image_angle + 90);
var _door_tip_y = _door_y + lengthdir_y(80, image_angle + 90);
var _door_tip_hit = collision_line(_door_x, _door_y, _door_tip_x, _door_tip_y, all, false, true);
```

Use `draw_line` output first to see your boxes in-game, then switch to `collision_line`.

---

## Built with AI

Built with **Claude** (Opus 4.8 & Sonnet 4.6) by a GameMaker developer who got tired of trial-and-error with `lengthdir`. Free and open source — use it, fork it, share it.

The example sprite was generated with ChatGPT.

---

## License

MIT — do whatever you want with it.
