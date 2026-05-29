# jura

Terminal Jira client with git and Claude Code integration.

## Installation

Requires a Rust toolchain ([rustup.rs](https://rustup.rs)).

```sh
cargo install --git https://github.com/palmensimon/jura.git
```

## Configuration

```sh
jura init
```

Edit the generated `config.yaml` with your Jira credentials (`base_url`, `token`). Config is stored in the platform default location:

- **Linux:** `~/.config/jura/`
- **macOS:** `~/Library/Application Support/jura/`
- **Windows:** `%APPDATA%\jura\`

## Usage

| Command | Description |
|---|---|
| `jura` | Open the TUI |
| `jura tickets` | List assigned tickets (JSON, reads local cache) |
| `jura ticket <KEY>` | Full details for a ticket |
| `jura init` | Write example config files |

The local cache is populated when you open the Mine tab in the TUI.

## AI Integration

Install `jira-mcp.skill` to give your AI agent access to your Jira tickets via the CLI commands above.
