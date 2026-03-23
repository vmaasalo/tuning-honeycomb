# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

`tuning-honeycomb` is a single self-contained HTML file — no build process, no dependencies, no package manager. Open `tuning-honeycomb.html` directly in any modern browser to run it.

## Architecture

The entire application lives in `tuning-honeycomb.html`. Key sections:

- **Music theory (lines ~30–50):** Pitch naming and frequency calculation for 5-limit just intonation. The grid is 7 fifths × 5 thirds (35 notes total). Base frequency: A4 = 440 Hz.
- **Audio engine (lines ~60–102):** Web Audio API — one `OscillatorNode` per active note, 40 ms attack / 80 ms release envelope, master gain capped at 80%.
- **SVG rendering & interaction (lines ~123–258):** Hexagonal lattice drawn as SVG polygons. Each hexagon is clickable to toggle a pitch; octave-shift buttons appear on hover when a note is active.
- **Styling (lines ~2–16):** Inline CSS. Hex colors are keyed by row (thirds axis).

### Coordinate system

Each note is addressed by `(fx, ty)` where `fx` ∈ `[-3, 3]` (fifths) and `ty` ∈ `[-2, 2]` (major thirds). Pixel position is derived from these coordinates and the hexagon radius (36 px), centered in an SVG viewBox of 780 × 420.
