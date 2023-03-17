## now
```bash
# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.

if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi


## oh-my-zsh
export ZSH="$HOME/.oh-my-zsh"

export NVM_DIR="$HOME/.nvm"
## source $(brew --prefix nvm)/nvm.sh

[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \. "/opt/homebrew/opt/nvm/nvm.sh"
# This loads nvm

ZSH_THEME="powerlevel10k/powerlevel10k"

plugins=(git autojump)

source $ZSH/oh-my-zsh.sh

## autojump config

[ -f /opt/homebrew/etc/profile.d/autojump.sh ] && . /opt/homebrew/etc/profile.d/autojump.sh

# User configuration

## shell
alias la="ls -al"

## git
alias gc='git clone'
alias gs='git status'
alias gd='git diff'
alias ga='git add .'
alias gap='git add -p'
alias gcm='git commit -m'
alias gb='git branch'
alias gba='git branch -a'
alias gp='git pull'
alias gpr='git pull --rebase'
alias gpu='git push'
alias gl='git log'

## npm
alias dev="npm run dev"
alias test="npm run test"
alias test:ui="npm run test:ui"
alias build="npm run build"
alias coverage="npm run coverage"
alias vitepress="yarn docs:dev"

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh


# Environment PATH

export PATH=/usr/local/mysql-8.0.31-macos12-arm64/bin:$PATH
export PATH="$HOME/.jenv/bin:$PATH"
eval "$(jenv init -)"
export PATH="/opt/homebrew/opt/curl/bin:$PATH"

```


## backup
```bash
export NVM_DIR="$HOME/.nvm"

# source $(brew --prefix nvm)/nvm.sh

  

[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \. "/opt/homebrew/opt/nvm/nvm.sh"

# This loads nvm

  
  

# shell alias

## shell

alias la="ls -al"

## git

alias gc='git clone'

alias gs='git status'

alias gd='git diff'

alias ga='git add .'

alias gap='git add -p'

alias gcm='git commit -m'

alias gb='git branch'

alias gba='git branch -a'

alias gp='git pull'

alias gpr='git pull --rebase'

alias gpu='git push'

alias gl='git log'

## npm

alias dev="npm run dev"

alias test="npm run test"

alias test:ui="npm run test:ui"

alias build="npm run build"

alias coverage="npm run coverage"

alias vitepress="yarn docs:dev"

  

# Add wisely, as too many plugins slow down shell startup.

plugins=(

git

)

  

# Environment PATH

export PATH=/usr/local/mysql-8.0.31-macos12-arm64/bin:$PATH

export PATH="$HOME/.jenv/bin:$PATH"

eval "$(jenv init -)"

export PATH="/opt/homebrew/opt/curl/bin:$PATH"
```
