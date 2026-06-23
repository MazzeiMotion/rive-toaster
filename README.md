# toaster-game

**Status:** active
**Runtime:** Web (JS runtime)

Simple web demo embedding a single .riv file rendered as a square, dead-center on the page, via the Rive JS/web runtime.

## Production Plan

Render the pre-built `_riv/toaster.riv` in the browser via the Rive **JS/web runtime**,
as a **responsive square** centered in the viewport.

- **Source:** `_riv/toaster.riv` (supplied by operator — not built in this project).
- **Harness:** single self-contained `_demo/index.html`, Rive loaded from CDN
  (`@rive-app/canvas`). No build step.
- **Layout:** square sized to `min(100vw, 100vh)`, flex-centered; re-fits on resize
  with `resizeDrawingSurfaceToCanvas()` for crisp HiDPI rendering.
- **Wiring:** `artboard: "default"` (the complete game — `toaster` is the character-only
  artboard), `autoplay: true`, `stateMachines: "State Machine 1"`, `autoBind: true`
  (binds the default `ToasterVM` instance automatically — no manual property plumbing
  for the basic embed).
- **Aspect note:** the `default` game artboard is **landscape**; under `Fit.Contain` it
  letterboxes (bands top/bottom) inside the square canvas, keeping the square-frame spec.
- **Serve:** root the dev server at the **project folder** (`projects/toaster-game/`),
  not `_demo/`, so `../_riv/toaster.riv` resolves. Use `npx http-server . -p <port> -c-1`
  (avoids the `npx serve` clean-URLs path-rewrite gotcha — see [[js-runtime]]).

### Discovered file structure (from `_riv/toaster.riv`)

| Kind | Names |
|---|---|
| Artboard | `default` (full game), `toaster` (character only) |
| State Machine | `State Machine 1` |
| ViewModel | `ToasterVM` |
| Triggers / inputs | `resetScore`, `tickScore`, `breadDone`, `breadJump`, `activate`, `toasterActivate`, `toasterTimeOut` |
| States / enum | `game-start`, `game-running`, `game-end` |
| Animations | `toaster_idle`, `toaster_pop`, `toaster_eye_loop`, `toaster_bouncing`, `toast_idle`, `button_idle` |

> Names read directly from the binary string table — verify against the live file if the
> embed misbehaves. Out of scope for now: wiring UI controls to the game triggers / score.

## ViewModel Map

The `.riv` already ships with its ViewModel — CW is **not** creating VMs in Rive for this
project (no Path A trigger). `autoBind: true` binds the default `ToasterVM` instance.
Property names/types not yet enumerated — `[TK: confirm ToasterVM properties]` if/when the
demo grows controls.

## Session Notes

_Append session notes as development progresses._

## Debugging Notes

_Record project-specific debugging discoveries here._
