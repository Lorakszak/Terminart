# Bootiful - Claude Code Instructions

## Project Overview
Terminal ambiance engine in Rust. Displays procedurally generated ASCII art scenes with animated entities. First scene: campfire (knight, fire, smoke, twinkling stars, trees).

## Tech Stack
- Rust (edition 2024)
- crossterm - terminal control (raw mode, input, resize)
- ratatui - rendering (buffer diffing, styled cells)
- clap - CLI argument parsing (derive macros)
- rand - random number generation

## Architecture
```
CLI (main.rs) -> Engine (engine.rs) -> Scene trait (scene.rs)
                                          |
                                    CampfireScene (scenes/campfire/)
```

- **Engine** - main loop: poll input, tick scene, render via ratatui, sleep
- **Scene trait** - `setup()`, `tick(dt, rng)`, `render(frame)`, `resize()`
- **Layer** - 2D grid of optional styled cells, composited back-to-front
- **Entity** - animated object with position, velocity, art frames, layer assignment

Scenes own their layers (background, midground, foreground, overlay), entities, and spawners.

## Building and Running
```bash
cargo build           # build
cargo run             # run default scene
cargo run -- --list   # list scenes
cargo run -- -s campfire --fps 15
```
Press any key to exit.

## Conventions
- Each scene lives in `src/scenes/<name>/` with `mod.rs` + `art.rs`
- New scenes implement the `Scene` trait
- Entity frames use `Vec<String>`, not `&'static str` (no Box::leak)
- ASCII art constants use `r#"..."#` string literals (draw_ascii strips leading/trailing newlines)
- Scratch layers are pre-allocated and reused via `.clear()`, never allocated per-frame

## Adding a New Scene
1. Create `src/scenes/<name>/mod.rs` implementing `Scene` trait
2. Create `src/scenes/<name>/art.rs` with ASCII art constants
3. Add `pub mod <name>;` to `src/scenes/mod.rs`
4. Add `SceneInfo` entry to `SCENES` array in `src/scenes/mod.rs`
5. Add variant to `SceneName` enum in `main.rs`
6. Add match arm in `main.rs`
