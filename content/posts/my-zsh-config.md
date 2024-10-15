+++
title = 'My ZSH Config'
date = 2023-10-13T00:00:00+02:00
draft = false
+++

+++
## What is ZSH

Z shell is a command-line shell, alternative to Bash, offering more advanced
features like enhanced autocompletion, spell correction, and improved scripting
capabilities. It's part of my Unix setup for both my work and personal machines.
A good configuration can make all your work station setups consistent 

You can get the latest version of my .zshrc on my Github [Dot Files
Repo](https://github.com/liamattard/Dotfiles)

## My .ZSHRC Config

### The Plugin Manager

This script sets up the [Zinit](https://github.com/zdharma-continuum/zinit)
plugin manager for Zsh. With this you can install plugins like autocomplete and
syntax highliting. It first checks if it is already installed, if not it will
fetch it.

```
ZINIT_HOME="${XDG_DATA_HOME:-${HOME}/.local/share}/zinit/zinit.git"
[ ! -d $ZINIT_HOME ] && mkdir -p "$(dirname $ZINIT_HOME)"
[ ! -d $ZINIT_HOME/.git ] && git clone https://github.com/zdharma-continuum/zinit.git "$ZINIT_HOME"

source "${ZINIT_HOME}/zinit.zsh"
```

### The prompt

![The prompt](/prompt.png)

The prompt is an important part of your setup as you will be interacting with it
whilst usin the terminal. Usually, this is setup with the user and current
working directory.  However, in ZSH you can setup some addittional information,
for example, in my case I set it up to include the branch name when going to a
git repository, as you can see in the screenshot.

To set it up, we can install oh-my-posh and choosing a theme. In my case, I use
the 'catpuccin' theme.
```

if ! command -v oh-my-posh &> /dev/null; then
    echo "oh-my-posh not found. Installing..."
    curl -s https://ohmyposh.dev/install.sh | bash -s
fi

# Oh-My-Posh Theme
THEME="~/Dotfiles/zsh/oh_my_posh/catppuccin.omp.json"

eval "$(oh-my-posh init zsh --config $THEME)"

```

### Options
The configuration includes several useful Zsh options to improve your shell experience. It enables settings like histignorealldups to avoid duplicate entries in your command history and sharehistory to synchronize command history across sessions. 

The history size is increased to 5000 commands, and appendhistory ensures that commands are saved after each execution. Additionally, the configuration manages history-related files and erases duplicates (HISTDUP=erase). 

These settings help maintain an efficient and organized command history, making your terminal workflow smoother and more reliable.
```
# Set options for history
setopt histignorealldups sharehistory appendhistory hist_ignore_space
HISTSIZE=5000
HISTFILE=~/.zsh_history
HISTDUP=erase
```

# Custom scripts
```
if [[ "$WORK_OR_PERSONAL" == "WORK" ]]; then
    . /home/attardl/scripts/ilmt.sh
    . /home/attardl/scripts/mq.sh
    . /home/attardl/scripts/mq-farm.sh

    alias git-bash='/mnt/c/Program\ Files/Git/bin/bash.exe'
else
    alias vim=nvim
fi
```
### Plugins
zinit light zsh-users/zsh-syntax-highlighting
zinit light zsh-users/zsh-completions
zinit light zsh-users/zsh-autosuggestions

```

### Custom scripts
```
. ~/Dotfiles/zsh/vim_mode.sh
. ~/Dotfiles/zsh/completion.sh

```

### Key bindings
```
bindkey "^A" vi-beginning-of-line
bindkey "^E" vi-end-of-line
bindkey "^[[A" history-beginning-search-backward
bindkey "^[[B" history-beginning-search-forward
bindkey '^ ' autosuggest-accept
```