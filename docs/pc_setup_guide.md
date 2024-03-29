# Windows setup guide
This guide is meant to help a Windows user configure their development environment. This takes the approach of using Microsoft's Windows Subsystem for Linux (WSL2).

Open PowerShell as an administrator and run the commands below.
```sh
# install WSL2
wsl --install --distribution Ubuntu;

winget install Microsoft.WindowsTerminal;
winget install Microsoft.VisualStudioCode;
winget install Git.Git;
winget install GitHub.cli;
```

Open PowerShell and run the command below to install the [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) extension. This allows you to open code in Visual Studio Code that resides in WSL2.

```sh
code --install-extension ms-vscode-remote.vscode-remote-extensionpack;
```


## Ubuntu
Within Ubuntu you will install pyenv to manage your python version, poetry to manage your python virtual environments, and Oh My Zsh, a great framework that runs in the Zsh shell. Oh My Zsh allows for the use of plugins that simplify many workflows. For example, `autoswitch_virtualenv` is a plugin that automatically enters a poetry environment whenever you cd into a directory that has one.

Open Windows Terminal to an Ubuntu shell and run the commands below.
```bash
# update apt package manager
sudo apt update;

# install dependencies for pyenv and poetry
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl \
git zsh libpq-dev unixodbc-dev;

# install pyenv
git clone https://github.com/pyenv/pyenv.git ~/.pyenv;

# install oh my zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)";

git clone "https://github.com/MichaelAquilina/zsh-autoswitch-virtualenv.git" "$ZSH_CUSTOM/plugins/autoswitch_virtualenv";
```

Run `code ~/.zshrc` to open Oh My Zsh's config file, delete the line `plugins=(git)`, and add the code below to the bottom of the file.
```
alias python=python3
alias pip=pip3

plugins=(
    git
    web-search
    gcloud
    dotenv
    autoswitch_virtualenv
)

source $ZSH/oh-my-zsh.sh

export PATH="$HOME/.pyenv/bin:$PATH"
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
export PATH="$HOME/.local/bin:$PATH"

eval "$(pyenv init --path)"
eval "$(pyenv init -)"
eval "$(enable_autoswitch_virtualenv)"
```

Close and reopen Windows Terminal.

Run the commands below to install python 3.9.10 and poetry.
```bash
# install python 3.9.10
pyenv install 3.9.10;
pyenv global 3.9.10;

# install poetry
curl -sSL https://install.python-poetry.org | python3 -
```


## Git
Time to configure git and authenticate with GitHub.

In PowerShell:
```sh
gh auth login;
```

In Ubuntu:
```sh
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager-core.exe"
```

## Workflow
From within Ubuntu, you can now clone a repo via `git clone` onto your Linux filesystem, `cd` into it, and run `code .` to open that folder in Visual Studio Code.

If you run `poetry init` or `poetry install` in a folder to create a python virtual environment, that environment will automatically be enabled every time you `cd` into the folder.
