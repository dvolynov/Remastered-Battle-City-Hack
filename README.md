# Battle City Remastered — Hackathon Edition

> A full-featured, modern remake of the 90's arcade classic built **from scratch in just 72 hours** using nothing but **Python 3** and **pygame**.

[![Gameplay Demo](https://img.youtube.com/vi/your-demo-link/hqdefault.jpg)](https://youtu.be/your-demo-link)

---

## Table of Contents
1. [Why This Project?](#why-this-project)
2. [Key Features](#key-features)
3. [Screenshots](#screenshots)
4. [Architecture Overview](#architecture-overview)
5. [Project Structure](#project-structure)
6. [Installation](#installation)
7. [Running the Game](#running-the-game)
8. [Controls](#controls)
9. [Configuration & Modding](#configuration--modding)
10. [Roadmap](#roadmap)
11. [Contributing](#contributing)
12. [License](#license)

---

## Why This Project?

Re-engineering Battle City within tight hackathon constraints is a stress-test of Python's capabilities in real-time graphics, physics, and AI **without** heavyweight game engines. Every system—from sprite batching to finite-state machine AI—was handcrafted to prove that Python can punch above its perceived weight in game dev.

---

## Key Features

* ⚔️ **Core Gameplay**: brick & steel walls, ricocheting shells, power-ups, base defense.
* 🤖 **AI Tanks**: patrol, chase, and flee behaviours via a custom FSM.
* 🎯 **60 FPS Rendering**: double-buffered, V-sync friendly loop with draw-call minimization.
* 🧱 **Destructible Terrain**: tile-accurate damage model.
* 🗺 **Level Loader**: JSON or Tiled `.tmx` maps consumed at runtime.
* 🎮 **Local Multiplayer**: plug in a second controller/keyboard.
* 🖼 **Retro Aesthetic**: pixel-art sprites & CRT-style HUD.
* 🧩 **Mod Ready**: drop new maps, sprites, or Python entities—no engine rebuild required.

---

## Screenshots

<p float="left">
  <img src="docs/screen1.png" width="45%"/>
  <img src="docs/screen2.png" width="45%"/>
</p>

(Place screenshots in `docs/` or change paths accordingly.)

---

## Architecture Overview

```text
┌────────────┐      shoots       ┌──────────┐
│   Player   │ ───────────────▶ │  Bullet  │
└────────────┘◀─────────────────└──────────┘
     ▲   ▲  collisions                ▲
     │   └──────────┐ updates         │
┌────┴─────┐  events│            ┌────┴─────┐
│  Level   │◀───────┘            │  Enemy  │
└──────────┘        spawns       └──────────┘
```

* **Entity-Component System**: lightweight ECS allows >30 active actors with minimal boilerplate.
* **Game Loop**: fixed-time update followed by variable-time render ensuring determinism.
* **Services**: singleton-style helpers (audio, input, resource cache) decouple subsystems.
* **State Machines**: each tank uses an FSM (`units\state.py`) for responsive AI transitions.

---

## Project Structure

```text
/ Battle-City-Remastered
├── assets/         # raw images & sounds (PNG, WAV, OGG)
├── maps/           # level JSON / TMX files
├── objects/        # data-driven static obstacles
├── settings/       # global constants (resolution, FPS, keys)
├── sprites/        # processed/atlased sprite sheets
├── units/          # tank, bullet, power-up classes & AI states
│   └── __init__.py
├── camera.py       # smooth scrolling camera
├── debug.py        # performance overlay & dev utilities
├── hood.py         # heads-up display (health, ammo, score)
├── level.py        # tile map loader & collision grid
├── main.py         # entry point & main loop
├── requirements.txt
└── README.md       # ← you are here
```

> **Note:** folders may be renamed as development continues; see inline docstrings for authoritative API.

---

## Installation

1. **Clone the repo**
   ```bash
   git clone https://github.com/dvolynov/Battle-City-Remastered.git
   cd Battle-City-Remastered
   ```
2. **Create virtual env (recommended)**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   ```
3. **Install dependency**
   ```bash
   pip install -r requirements.txt
   ```
   `pygame` is the *only* external library. Build instructions for pygame can be found [here](https://www.pygame.org/wiki/GettingStarted).

---

## Running the Game

```bash
python main.py
```

Optional CLI flags:
* `--level 2` — start from level #2
* `--scale 3` — pixel scaling factor (CRT effect)

---

## Controls

| Action         | Player 1 | Player 2 (if enabled) |
|----------------|----------|------------------------|
| Move           | W A S D  | Arrow Keys             |
| Shoot          | Space    | Right Ctrl             |
| Pause / Menu   | Esc      | Esc                    |

Gamepad mapping uses SDL's default layout.

---

## Configuration & Modding

* **Levels** — Create a Tiled file with 16×16 tiles, export as `.tmx`, and save to `maps/`. New level appears in the menu automatically.
* **Sprites** — Replace or add PNGs in `sprites/`, then regenerate atlases via `python tools/sprite_packer.py` (coming soon).
* **Gameplay Tweaks** — Tweak `settings/constants.py` (tank speed, bullet damage, power-up frequency).

---

## Roadmap

- [ ] Online multiplayer (WebSockets or ENet-Python)
- [ ] Built-in level editor
- [ ] Procedural arena generator
- [ ] Steam Deck & Raspberry Pi builds

---

## Contributing

Pull requests are welcome! If you plan a major feature, open an issue first to discuss scope. Please abide by the following:

1. **Code Style** — PEP8 via `ruff` & `black` (run `make lint`).
2. **Commits** — Conventional Commits (`feat:`, `fix:`, `docs:`).
3. **Testing** — Unit tests live in `tests/`; new features require coverage.
4. **Assets** — Only include public-domain or original art.

---

## License

*Made with ❤️ and caffeine during Rebuildathon Hackathon 2025.* 