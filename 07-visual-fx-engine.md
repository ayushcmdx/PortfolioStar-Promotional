# 02 — Visual FX Engine

> **Free Edition** · Part 2 of 7

---

## Overview

Four visual systems drive the portfolio's personality — three canvas-based, one DOM-based. None use Three.js or WebGL; everything runs on vanilla **Canvas2D** with custom math, keeping the bundle lean while looking GPU-accelerated.

| System | File | Technique |
|---|---|---|
| Galaxy Background | `FluidRippleBg.tsx` | Canvas2D particle field |
| Solar System | `SolarSystemBgClient.tsx` | Canvas2D orbital math |
| 3D Tech Globe | `Globe3D.tsx` | Canvas2D 3D projection |
| Glass Cursor | `GlassCursor.tsx` | DOM + CSS transform |

---

## Galaxy Background (`FluidRippleBg`)

A fixed, pointer-events-none fullscreen canvas drawing six layers each frame: a cached static star field, low-alpha nebula orbs, rotating spiral arms (stored in a `Float32Array` for performance), occasional shooting stars, a cursor-following light aura, and click/mousemove ripples that expand and fade.

The star field is drawn once to an offscreen canvas and reused via `drawImage`, and the spiral-arm data avoids per-frame allocations — both are why this stays under budget on the main thread.

---

## 3D Tech Globe (`Globe3D`)

The most math-heavy component: a spinning globe with 24 tech icons orbiting its surface, rendered entirely with 2D canvas math.

**Concept:** each icon's 3D position is computed from spherical coordinates (angle + elevation), rotated by a slow auto-rotation (plus optional mouse drag), then projected orthographically to 2D screen space. Icons closer to the viewer are drawn larger and later (depth sorting), reinforcing the 3D illusion.

The wireframe (12 rings × 16 meridians) is built once at module load and reused across renders — resizing only rescales it, never recomputes it.

> 🔒 **Pro edition adds:** the exact projection formulas, the full `techLabels` data structure, icon-loading lifecycle, and depth-sort implementation.

---

## Glass Cursor (`GlassCursor`)

A DOM `<div>`, not a canvas — tracks `mousemove` and updates its position via direct DOM manipulation (skipping React state to avoid re-renders). It has a cyan ring border, a `backdrop-filter: blur` glass effect, and a short CSS transition that gives it physical lag. It expands on hover over interactive elements, and the native OS cursor is hidden while it's mounted.

---

## Night Mode Overlay

A simple dimming layer toggled via `localStorage`, with a smooth opacity transition — no canvas involved.

---

## Shared Lifecycle Pattern

All canvas systems follow the same mount/cleanup shape: build listeners and cached geometry on mount, run a `requestAnimationFrame` loop, and tear everything down (cancel the frame, remove listeners, remove the canvas) on unmount. All handle `window.resize` by rebuilding size-dependent cached data.

---

## Performance Budget

- No state updates inside animation loops — all mutation is direct DOM/canvas
- Offscreen canvas caching for static elements
- `Float32Array` for hot-path numeric data
- Module-level geometry constants for the globe

Combined, these effects consume well under 2ms of main-thread time per frame on a mid-range device.

> 🔒 **Pro edition adds:** full source for all four systems, tuning parameters for each visual layer, and guidance for adding new canvas effects following the same pattern.

---

*Prev: [01 — Project Structure & Frontend](./01-project-structure-and-frontend.md) · Next: [03 — Visitor Lounge & Real-Time →](./03-visitor-lounge-realtime.md)*
