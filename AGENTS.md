# AGENTS.md

This repo is a personal dotfiles setup managed with GNU Stow.

## Layout (important)

- Each top-level folder is a Stow “package” (e.g. `zsh/`, `neovim/`, `tmux/`).
- Files inside each package mirror the target paths in `$HOME`.
  - Example: `neovim/.config/nvim/init.lua` -> `~/.config/nvim/init.lua`
- Do not add files at the repo root unless they’re repo-level helpers.

## Common workflows

- Link / restow everything:
  - `./stow-all.sh`
- Dry run (no changes):
  - `./stow-all.sh -n`
- Remove all symlinks:
  - `./stow-all.sh -D`
- Full bootstrap on macOS (Homebrew + stow + deps):
  - `./install.sh`

## Neovim

- Config entrypoint: `neovim/.config/nvim/init.lua`
- Plugin manager: `lazy.nvim` (plugins declared inside `require("lazy").setup({ ... })`).
- Theme: `twenty` at `neovim/.config/nvim/colors/twenty.lua`

## Zsh

- Main config: `zsh/.zshrc`
- Modular configs: `zsh/.zsh/*.zsh`
- Secrets:
  - Put machine/user secrets in `~/.zsh_secrets` (gitignored)
  - Template: `zsh/.zsh_secrets.example`

## OpenCode Agents

Custom agents live under `opencode/.config/opencode/` and stow to `~/.config/opencode/`.

### Extension types

| Type | Location | Trigger |
|------|----------|---------|
| Skill | `skills/<name>/SKILL.md` | Auto-matched by skill loader |
| Agent | `agents/<name>.md` | Tab to switch, or `@<name>` mention |
| Command | `commands/<name>.md` | `/<name>` in-session |

### Agent Forge

The meta-agent for creating new agents. Use it to go from idea to working agent:

```bash
agent-forge "an agent that reviews PRs for security"   # headless creation
agent-forge --edit steve-jobs                           # iterate on existing
agent-forge --list                                      # see what you have
agent-forge                                             # interactive TUI
```

The skill is at `opencode/.config/opencode/skills/agent-forge/SKILL.md` (via `skills → skill` symlink).
The bin script is at `bin/.local/bin/agent-forge`.

## Conventions / safety

- Keep changes scoped to the relevant package directory.
- Avoid committing machine-specific paths or credentials.
- Prefer small, reversible edits; dotfiles breakages are painful.
