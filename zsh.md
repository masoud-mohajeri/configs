# Modern Zsh Setup for macOS

A Fish-like shell experience powered by Zsh, with intelligent autosuggestions, interactive completions, fuzzy search, syntax highlighting, and a beautiful Starship prompt.

The goal is to get the best of both worlds:

- Fish-like usability.
- Zsh compatibility and extensibility.
- A lightweight, manually managed configuration.
- A modern developer-friendly terminal experience.

## 1. Tech Stack

| Tool | Purpose |
|---|---|
| Zsh | Shell |
| Starship | Modern, customizable prompt |
| zsh-autosuggestions | Fish-like inline suggestions |
| zsh-syntax-highlighting | Command syntax highlighting |
| zsh-completions | Additional completion definitions |
| fzf | Fuzzy finder |
| fzf-tab | Interactive fuzzy completion |
| zoxide | Smart directory navigation |
| Atuin | Advanced shell history |

## 2. Install Dependencies

Install the core tools using Homebrew:

```bash
brew install starship \
  zsh-autosuggestions \
  zsh-syntax-highlighting \
  zsh-completions \
  fzf \
  zoxide \
  atuin
```

### Install fzf-tab

```bash
mkdir -p ~/.zsh/plugins

git clone https://github.com/Aloxaf/fzf-tab \
  ~/.zsh/plugins/fzf-tab
```

## 3. Configure Zsh

Open your Zsh configuration:

```bash
touch ~/.zshrc
code ~/.zshrc
```

Add the following configuration:

```bash
# ==========================================
# Zsh - Modern Developer Configuration
# ==========================================

# ------------------------------------------
# Completion
# ------------------------------------------

# Additional completion definitions
fpath+=("$(brew --prefix)/share/zsh-completions")

autoload -Uz compinit
compinit

# Completion styling
zstyle ':completion:*' menu no
zstyle ':completion:*:descriptions' format '[%d]'
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Za-z}'


# ------------------------------------------
# FZF - Fuzzy Finder
# ------------------------------------------

source "$(brew --prefix)/opt/fzf/shell/key-bindings.zsh"
source "$(brew --prefix)/opt/fzf/shell/completion.zsh"


# ------------------------------------------
# FZF Tab - Interactive Completion
# ------------------------------------------

source ~/.zsh/plugins/fzf-tab/fzf-tab.plugin.zsh


# ------------------------------------------
# Autosuggestions - Fish-like Experience
# ------------------------------------------

ZSH_AUTOSUGGEST_STRATEGY=(history completion)
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=8'

source "$(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh"


# ------------------------------------------
# Zoxide - Smart Directory Navigation
# ------------------------------------------

eval "$(zoxide init zsh)"


# ------------------------------------------
# Atuin - Advanced Shell History
# ------------------------------------------

eval "$(atuin init zsh)"


# ------------------------------------------
# Starship - Modern Prompt
# ------------------------------------------

eval "$(starship init zsh)"


# ------------------------------------------
# Syntax Highlighting
# MUST BE LOADED LAST
# ------------------------------------------

source "$(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh"
```

Reload your configuration:

```bash
source ~/.zshrc
```

## 4. Features

### 4.1. Autosuggestions

Plugin: [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

Provides Fish-like inline suggestions based on command history and completion.

Example:

```bash
$ git che
```

Zsh suggests:

```bash
$ git checkout main
```

- Gray text represents the suggested command.
- Press `→` to accept the suggestion.
- Continue typing to ignore it.

### 4.2. Interactive Tab Completion

Plugin: [fzf-tab](https://github.com/Aloxaf/fzf-tab)

Replaces the traditional completion list with an interactive fuzzy-search interface.

Instead of browsing a long list of files, directories, or Git branches, you can search and select them interactively.

Press `Tab` to activate completion.

### 4.3. Fuzzy Finder

Tool: [fzf](https://github.com/junegunn/fzf)

Useful keyboard shortcuts:

| Shortcut | Action |
|---|---|
| `Ctrl + R` | Search command history |
| `Ctrl + T` | Search files |
| `Alt + C` | Search directories |

### 4.4. Syntax Highlighting

Plugin: [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

Highlights commands as you type.

- Valid commands are highlighted.
- Invalid commands are visually distinguished.
- Strings and command arguments receive different colors.

### 4.5. Starship Prompt

Tool: [Starship](https://starship.rs/)

Provides a modern, customizable shell prompt.

It can display:

- Current directory.
- Git branch.
- Git working tree status.
- Node.js version.
- Python version.
- Rust version.
- Command execution time.
- Exit status.

Starship is independent of your shell, so you can use the same prompt configuration with Zsh, Bash, and Fish.

### 4.6. Zoxide

Tool: [zoxide](https://github.com/ajeetdsouza/zoxide)

A smarter replacement for `cd`.

Example:

```bash
z projects
```

Instead of navigating through multiple directories, zoxide learns your directory history and takes you to the best matching location.

### 4.7. Atuin

Tool: [Atuin](https://github.com/atuinsh/atuin)

An advanced shell history manager.

Features include:

- Interactive history search.
- Full-text search.
- Command execution time.
- Exit codes.
- Optional history synchronization across machines.

Press `Ctrl + R` to access its interactive history search.

Note: Atuin replaces the default Ctrl+R history binding provided by fzf. If you use Atuin, you can remove or disable fzf's Ctrl+R binding.

## 5. Configuration File Locations

| File | Purpose |
|---|---|
| `~/.zshrc` | Main Zsh configuration |
| `~/.config/starship.toml` | Starship prompt configuration |
| `~/.config/atuin/config.toml` | Atuin configuration |
| `~/.zsh/plugins/` | Manually installed Zsh plugins |

## 6. Recommended Starship Configuration

Create the configuration file:

```bash
mkdir -p ~/.config
touch ~/.config/starship.toml
```

Example configuration:

```toml
add_newline = true

format = """
$username\
$hostname\
$directory\
$git_branch\
$git_status\
$nodejs\
$python\
$rust\
$cmd_duration\
$line_break\
$character
"""

[directory]
truncation_length = 3
truncate_to_repo = true

[git_branch]
symbol = " "
format = "[$symbol$branch]($style) "

[git_status]
format = '([$all_status$ahead_behind]($style) )'

[nodejs]
symbol = " "
format = "[$symbol$version]($style) "

[python]
symbol = " "
format = "[$symbol$version]($style) "

[rust]
symbol = " "
format = "[$symbol$version]($style) "

[cmd_duration]
min_time = 2000
format = "took [$duration]($style) "

[character]
success_symbol = "[❯](bold green)"
error_symbol = "[❯](bold red)"
```

You may need a Nerd Font installed to display all icons correctly.

## 7. Important Notes

### Plugin Loading Order

The order of plugins in `.zshrc` matters.

Recommended order:

1. Completion initialization (`compinit`).
2. FZF integration.
3. fzf-tab.
4. Autosuggestions.
5. Other shell integrations.
6. Starship.
7. Syntax highlighting (last).

### Keep Zsh Lightweight

Avoid installing too many plugins.

Every plugin adds initialization work and can increase shell startup time.

Start with the essentials and add more only when you need them.

### Avoid Oh My Zsh (Optional)

Oh My Zsh is a popular Zsh framework, but it is not required.

For a lightweight and manually managed setup, installing plugins individually gives you more control over your shell.

## 8. Useful Resources

- [Zsh Documentation](https://zsh.sourceforge.io/Doc/)
- [Starship](https://starship.rs/)
- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
- [fzf](https://github.com/junegunn/fzf)
- [fzf-tab](https://github.com/Aloxaf/fzf-tab)
- [zoxide](https://github.com/ajeetdsouza/zoxide)
- [Atuin](https://github.com/atuinsh/atuin)

---

**Goal:** A modern Zsh environment with the usability of Fish, the flexibility of Zsh, and the visual experience of Starship.
