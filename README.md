# Bootiful

Terminal ambiance engine - beautiful ASCII art scenes for your terminal.

Bootiful displays procedurally generated, animated ASCII art scenes directly in your terminal. Think of it as a screensaver for your shell - twinkling stars, flickering campfires, rising smoke, all rendered in characters.

## Features

- Procedurally generated scenes (never the same twice)
- Layered rendering with transparent compositing
- Entity system with animated sprites and spawners
- Lightweight (~15 FPS, minimal CPU usage)
- Press any key to exit

## Installation

Requires [Rust](https://rustup.rs/) toolchain.

```bash
git clone https://github.com/Lorakszak/Bootiful.git
cd Bootiful
cargo build --release
```

The binary will be at `target/release/bootiful`. Copy it somewhere on your `$PATH`:

```bash
cp target/release/bootiful ~/.local/bin/
```

## Usage

```bash
# Run default scene
bootiful

# Run a specific scene
bootiful --scene campfire

# List available scenes
bootiful --list

# Adjust frame rate
bootiful --fps 10
```

Press any key to exit.

### Auto-start with terminal

Add to your `~/.zshrc` or `~/.bashrc`:

```bash
bootiful -s campfire
```

## Available Scenes

| Scene | Description |
|-------|-------------|
| `campfire` | A knight resting by a campfire in the wilderness |

More scenes coming soon.

## License

MIT
