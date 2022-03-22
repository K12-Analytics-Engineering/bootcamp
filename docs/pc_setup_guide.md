# PC setup guide


```bash

# PowerShell as an administrator
wsl --install --distribution Ubuntu;
winget install Microsoft.WindowsTerminal;

# Ubuntu
sudo apt update;
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl \
git zsh;

git clone https://github.com/pyenv/pyenv.git ~/.pyenv;

sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"


```

Edit `~/.zshrc` and add:

```
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
export PATH="$HOME/.poetry/bin:$PATH"

eval "$(pyenv init --path)"
eval "$(pyenv init -)"

```

Restart shell

```bash

pyenv install;

```
