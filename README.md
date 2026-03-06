# D2 Map Playground ⚔️

A web-based Diablo II dungeon exploration simulator inspired by the **Durance of Hate Level 2** — one of the most notoriously complex maps in D2R.

> **Live Demo:** Open `index.html` in any browser — no server needed!

![Screenshot Placeholder](screenshot.png)

## What Is This?

An interactive dungeon map generator + autonomous explorer. Generate random D2-style dungeon layouts (rooms + corridors), then watch AI algorithms navigate through fog of war to find the exit.

## How to Run

```bash
# Just open the file
open index.html

# Or via GitHub Pages (if enabled)
# https://jonesandjay123.github.io/d2-map-playground/
```

No dependencies. No build step. No npm. Just a browser.

## Features

- **Random Map Generation** — Seeded PRNG generates rooms + corridors (seed displayed for reproducibility)
- **Fog of War** — Vision radius of 5 tiles; unexplored areas hidden
- **3 Navigation Algorithms** — Switch between them in real-time
- **Minimap** — Overview of explored areas in the corner
- **Speed Control** — From step-by-step to full-speed exploration
- **Dark Theme** — D2-inspired aesthetic

## Architecture

Single `index.html` file containing:

| Component | Description |
|-----------|-------------|
| **Map Generator** | Seeded room placement + L-shaped corridor connections |
| **Renderer** | HTML5 Canvas with 5px tile grid + minimap overlay |
| **Fog System** | Circle-based vision reveal (radius 5) with explored/unexplored tracking |
| **Navigation** | 3 pluggable algorithms (see below) |
| **Controls** | Button/slider UI for interactive exploration |

### Grid Encoding
- `0` = Wall (impassable)
- `1` = Walkable floor
- `2` = Entrance/Start (green)
- `3` = Exit/Goal (red)

## Navigation Algorithms

### Frontier Exploration
Scans all explored tiles for those adjacent to unexplored walkable tiles (frontiers). Picks the nearest frontier by Manhattan distance, then A* pathfinds one step toward it. Efficient and thorough.

### Wall Follower (Right-Hand Rule)
Classic maze-solving: always try to turn right, then go straight, then left, then back. Works well in simply-connected mazes but can loop in complex layouts.

### A* to Nearest Unexplored
Finds the closest unexplored walkable tile that borders an explored tile, then A* pathfinds toward it. Similar to frontier but targets the unexplored tile directly.

## Connection to D2R Bot Development

This project is a stepping stone toward D2R map-reading bots:

1. **Map structure understanding** — How D2 generates dungeon layouts (rooms, corridors, waypoints, exits)
2. **Exploration algorithms** — Testing which strategies efficiently find exits in D2-style maps
3. **Fog of war simulation** — Mimics the limited vision a bot has when entering a new area
4. **Pathfinding** — A* implementation reusable for actual bot navigation

The Durance of Hate Level 2 is specifically chosen because it's one of the hardest maps to navigate in D2R speedruns — finding the exit quickly is a key optimization.

## Roadmap

- [ ] Keyboard controls (WASD manual movement)
- [ ] Map presets (Act 1 caves, Act 2 tombs, Act 3 durance)
- [ ] Tileset visuals (replace colored squares with tile sprites)
- [ ] Path visualization (show algorithm's planned route)
- [ ] Performance metrics (compare algorithms side by side)
- [ ] Map sharing via seed URL parameter
- [ ] Waypoint/checkpoint system
- [ ] More realistic D2 map generation rules

## License

MIT
