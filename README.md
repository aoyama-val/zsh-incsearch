# Incremental search for zsh

Move cursor with incremental search within current line.

![demo](https://github.com/aoyama-val/zsh-incsearch/assets/13144822/210a4b5c-01f7-474b-bdb8-0674a1f29b49)

## Install (zinit)

```
zplug "aoyama-val/zsh-incsearch"
```

## Install (manual)

Clone this repository and

```
source {PATH_TO_REPO}/zsh-incsearch.plugin.zsh
```

## Configuration

To your ~/.zshrc:

```
# bind to any keys you like
bindkey "^[l" incsearch-forward              # put cursor at the end of match
bindkey "^[h" incsearch-backward             # put cursor at the end of match
bindkey "^[L" incsearch-forward-beginning    # put cursor at the beginning of match
bindkey "^[H" incsearch-backward-beginning   # put cursor at the beginning of match

my_incsearch_hook_enter() {
    if [ "$TERM_PROGRAM" = "iTerm.app" ]; then
        # Change cursor to underline
        echo -ne "\e]50;CursorShape=2\a"
    fi
}

my_incsearch_hook_leave() {
    if [ "$TERM_PROGRAM" = "iTerm.app" ]; then
        # Restore cursor to block
        echo -ne "\e]50;CursorShape=0\a"
    fi
}

incsearch_hooks_enter+="my_incsearch_hook_enter"
incsearch_hooks_leave+="my_incsearch_hook_leave"
```

## Keybindings while incremental search

| Key | Action |
|---|---|
| the key you bound to `accept-line` (usually Enter) | Finish search |
| the key you bound to `backward-delete-char` (usually Backspace) | Delete the last character from the search text |
