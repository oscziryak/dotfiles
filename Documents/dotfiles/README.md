# Initial Creation

# Separate Git Repo

```bash
echo 'alias dotfiles="/usr/bin/git --git-dir=$HOME/.dotfiles.git --work-tree=$HOME"' >> $HOME/.bashrc;
source $HOME/.bashrc;
echo ".dotfiles.git" >> .gitignore;
git init --separate-git-dir $HOME/.dotfiles.git;
dotfiles config --local status.showUntrackedFiles no;
```

# Add submodule

```bash
cd $HOME;
dotfiles submodule add https://github.com/VundleVim/Vundle.vim.git $HOME/.vim/bundle/Vundle.vim;
dotfiles status;
dotfiles commit -am "Add Vundle.vim Submodule to $HOME/.vim/bundle/Vundle.vim";
dotfiles pull --rebase origin master;
dotfiles push;
```

# Install dotfiles

```bash
#!/bin/bash

echo 'alias dotfiles="/usr/bin/git --git-dir=$HOME/.dotfiles.git --work-tree=$HOME"' >> $HOME/.bashrc;
source $HOME/.bashrc;
echo ".dotfiles.git" >> .gitignore;
git clone --recurse-submodules --separate-git-dir $HOME/.dotfiles.git https://www.gitlab.com/smacz/dotfiles.git;
dotfiles reset --hard;
dotfiles config --local status.showUntrackedFiles no;
dotfiles submodule update;
```

# Extra Installs

## Install Vundle

```bash
dotfiles submodule init;
dotfiles submodule update;
vim +PluginInstall +qall;
```

## Install YCM

### Fedora

```bash
#!/bin/bash

sudo dnf install -y cmake gcc-c++ make python-devel;
$HOME/.vim/bundle/YouCompleteMe/install.py;
```

### Manjaro/Arch

```bash
#!/bin/bash

sudo pamac install -y cmake gcc make;
$HOME/.vim/bundle/YouCompleteMe/install.py;
```

## Install tmux

```bash
sudo dnf install -y tmux;
```
