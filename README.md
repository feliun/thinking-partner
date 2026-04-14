# Thinking Partner

> A rigorous intellectual sparring partner grounded in your Obsidian vault.
> Finds contradictions, extends positions, and connects themes across your notes.

Not a coach, consultant, or assistant — the voice that says "have you considered..." and "your notes from three months ago contradict what you just said."

## What it does

- **Pressure-tests beliefs** by finding contradictions across your notes
- **Detects idea clusters** approaching critical mass
- **Generates ideas** grounded in your actual vault patterns
- **Answers as you would**, calibrated to your voice and stated positions
- **Maps strategic Power** using Hamilton Helmer's 7 Powers framework
- **Finds leverage points** across your constraints

## Commands

| Command | Description |
|---------|-------------|
| `/challenge {topic}` | Pressure-test your beliefs. Find contradictions, weak assumptions, blind spots. |
| `/emerge` | Detect idea clusters forming in your vault. |
| `/ghost {question}` | Draft a response in your voice, grounded in your notes. |
| `/ideas` | Pattern-driven idea generation across build / people / investigate / write. |
| `/leverage` | Find the 3-7 highest-ROI learning investments based on actual constraints. |
| `/strategise {subject}` | Power-based strategic analysis using Helmer's 7 Powers. |

## Prerequisites

- **[Claude Code](https://claude.com/claude-code)** — the plugin runs inside Claude Code.
- **[Obsidian](https://obsidian.md)** — your notes must live in an Obsidian vault.
- **Obsidian CLI plugin** — commands depend on `obsidian search`, `obsidian orphans`, `obsidian backlinks`, `obsidian tags`, `obsidian files`. Install from the Obsidian community plugin directory and ensure the `obsidian` binary is on your `$PATH`.
- **Obsidian must be running** when you use the commands (the CLI talks to the live app).
- **Optional:** the `obsidian:json-canvas` skill if you want `.canvas` visual outputs.

## Installation

1. Install the plugin into Claude Code (via marketplace or by cloning into `~/.claude/plugins/`).
2. Launch Claude Code from **inside your Obsidian vault directory** — `$WORKSPACE` defaults to the vault root.
3. Customize the reference files (see below). The plugin ships with generic samples so commands work out of the box, but output quality scales with how specific these files are to you.

## Configuration

All external files resolve through `commands/manifest.yaml`. Path tokens:

- `$WORKSPACE` — the directory Claude Code was launched from (typically your vault)
- `~` — your home directory
- bare paths — relative to the plugin root (shipped samples)

The resolver checks paths in order; first match wins. Override any default by placing a file at a higher-priority path.

### Reference files (calibrate the partner to you)

The plugin ships samples in `references/`. Replace them with your own by either:

- placing customized versions at your vault root (`$WORKSPACE/thinking-style.md`, etc.) — recommended, keeps personal content with your notes
- or at `~/.claude/thinking-partner/` — keeps personal content out of the vault

| File | Why it matters |
|------|----------------|
| `thinking-style.md` | Your biases, decision framework, depth calibration |
| `values.md` | Core philosophy, objectives, what to optimize for |
| `identity.md` | Background, role, domain — grounds `/ghost` and scoping |
| `work-style.md` | Capacity, energy management — shapes `/ideas` and `/leverage` |
| `writing-style.md` | Voice DNA — mandatory for `/ghost` to sound like you |

### Optional

- `logs/weekly/` — weekly review files, read by `/leverage`.
- `logs/daily/` — daily notes, read by `/leverage`.

## Output locations

Commands write `.canvas` files (when generated) to `outputs/canvas/` inside your vault by default. Configurable via the `canvas-output` manifest key.

## License

MIT
