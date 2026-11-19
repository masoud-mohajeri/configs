# ==========================================
# Completion
# ==========================================

# Load additional completion definitions from Homebrew.
fpath=("$(brew --prefix)/share/zsh-completions" $fpath)

autoload -Uz compinit
compinit

# Case-insensitive completion.
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Za-z}'

# Show descriptions in completion menus.
zstyle ':completion:*:descriptions' format '[%d]'

# ==========================================
# FZF Tab - interactive fuzzy completion
# ==========================================

source ~/.zsh/plugins/fzf-tab/fzf-tab.plugin.zsh

# Optional: use a compact preview window for certain completions.
# Uncomment and customize if you want previews.
# zstyle ':fzf-tab:complete:cd:*' fzf-preview 'ls -la $realpath'

# ==========================================
# Fish-like autosuggestions
# ==========================================

# Try history first, then completion candidates.
ZSH_AUTOSUGGEST_STRATEGY=(history completion)

# Use a subdued gray color for suggestions.
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=8'

source "$(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh"

# ==========================================
# Optional: smart directory navigation
# ==========================================

# Uncomment if you installed zoxide.
# eval "$(zoxide init zsh)"

# ==========================================
# Optional: enhanced shell history
# ==========================================

# Uncomment if you installed Atuin.
# eval "$(atuin init zsh)"

# ==========================================
# Starship prompt
# ==========================================

eval "$(starship init zsh)"

# ==========================================
# Syntax highlighting
# Keep this section LAST.
# ==========================================

source "$(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh"
