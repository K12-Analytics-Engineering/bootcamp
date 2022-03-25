# Mac setup guide
This guide is meant to help a Mac user configure their development environment.

Open Terminal and run the command below to install Homebrew.
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)";
```

Install Visual Studio Code via Homebrew.
```bash
brew install --cask visual-studio-code;
```

Install iTerm2 via Homebrew.
```bash
brew install --cask iterm2;
```

Install pyenv and python 3.9.10.
```bash
brew install pyenv;
pyenv install 3.9.10;
pyenv global 3.9.10;
```

Install poetry via Homebrew.
```bash
brew install poetry;
```

Install Oh My Zsh and plugin.
```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)";
git clone "https://github.com/MichaelAquilina/zsh-autoswitch-virtualenv.git" "$ZSH_CUSTOM/plugins/autoswitch_virtualenv";
```

Open `~/.zshrc` and add the following to the bottom.
```
plugins=(
    git
    web-search
    gcloud
    dotenv
    autoswitch_virtualenv
)

eval "$(pyenv init --path)"
```
