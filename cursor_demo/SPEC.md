# Character Walking Animation Test — Spec

## Overview
A minimal browser demo, delivered as a single self-contained `index.html` executable in any modern browser. A 2D character sits idle until the user presses a movement key, then plays a walk-cycle animation while moving horizontally inside a fixed play field.

## Deliverable
- **Format:** Single `index.html` file (HTML + CSS + JS inline, no build step, no external dependencies).
- **Runs by:** Double-clicking the file or opening it via `file://` in the browser.

## Assets
Place these image files in the same directory as `index.html`:

| File | Purpose |
|---|---|
| `idle.png` | Shown when the character is stationary |
| `walk_0.png` | Walk cycle frame 1 |
| `walk_1.png` | Walk cycle frame 2 |
| `walk_3.png` | Walk cycle frame 3 |
| `walk_4.png` | Walk cycle frame 4 |

**Note on frame naming:** The walk cycle uses four frames named `walk_0`, `walk_1`, `walk_3`, `walk_4` (there is intentionally no `walk_2`). Cycle through them in that order: 0 → 1 → 3 → 4 → 0 → ...

All source art faces **left**. When the character moves right, horizontally flip the sprite (`transform: scaleX(-1)`). When moving left, render unflipped.

## Play Field
- **Dimensions:** 1560 × 1080 px, fixed size.
- **Background color:** `#AEE0FF`.
- **Centering:** Center the play field in the browser viewport. The area outside the play field can be any neutral color (e.g. black or dark gray) — it is not part of the demo.
- **Character containment:** The character must never leave the play field. Clamp the character's position so its sprite bounding box stays fully inside the 1560 × 1080 area.

## Character
- Render using the PNG assets above. Preserve the source pixel dimensions (do not upscale or downscale the sprite).
- Use nearest-neighbor rendering (`image-rendering: pixelated`) so the art stays crisp.
- Starting position: roughly centered horizontally, resting on the bottom of the play field (no gravity / no jump — feet simply sit at the floor line).

## Controls
Only left/right movement is required. Support both arrow keys and WASD:

| Input | Action |
|---|---|
| `ArrowLeft` or `A` | Move left, face left |
| `ArrowRight` or `D` | Move right, face right (sprite flipped) |
| No key held | Stop, show idle frame |

- Movement speed: ~300 px/sec (tune for feel, but make it constant — no acceleration).
- Holding a key should move continuously, not per-keypress.
- If both left and right are held simultaneously, the character stops and shows idle.

## Animation
- **Idle state:** Display `idle.png`, no animation.
- **Walking state:** Cycle through the four walk frames at ~8 fps (~125 ms per frame). Loop indefinitely while a movement key is held.
- Transition rule: as soon as a movement key is pressed, switch to walking state; as soon as movement stops, reset to the idle frame.

## Out of Scope
- No vertical movement, jumping, or gravity.
- No other game UI (no HUD, score, menu, pause screen, start screen, etc.).
- No audio.
- No sprite-sheet tooling — load PNGs directly.

## Acceptance Criteria
1. Opening `index.html` in a browser shows the 1560 × 1080 play field with background `#AEE0FF`, the character idle and facing left.
2. Pressing and holding `→` or `D` moves the character right with a flipped sprite and a looping 4-frame walk animation.
3. Pressing and holding `←` or `A` moves the character left with an unflipped sprite and a looping 4-frame walk animation.
4. Releasing all keys immediately returns the character to the idle frame.
5. The character cannot move past the left or right edges of the play field.