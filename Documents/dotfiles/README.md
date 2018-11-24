# Initial Creation

## Separate Git Repo

```bash
echo 'alias dotfiles="/usr/bin/git --git-dir=$HOME/.dotfiles.git --work-tree=$HOME"' >> $HOME/.bashrc;
source $HOME/.bashrc;
echo ".dotfiles.git" >> .gitignore;
git init --separate-git-dir $HOME/.dotfiles.git;
dotfiles config --local status.showUntrackedFiles no;
```

## Add submodule

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
rm -rf $HOME/dotfiles;
dotfiles reset --hard;
dotfiles config --local status.showUntrackedFiles no;
dotfiles submodule update;
```

> Wait, why are we removing the `$HOME/dotfiles` directory? Don't we need that?!?

Well, actually we don't. It's an artifact that's created from the clone. We can't clone into `$HOME`, since there are already files there, and files that we expect to be overridden by the files we are version-controlling. However, since our alias specifies the work tree, it will always use the correct place once we `dotfiles reset --hard`.

And you may say "Well, why don't we use a bare git repo?" The answer is that there are more headaches with a bare git repo, especially regarding submodules, but that it only buys us the removal of that directory, but compounds the issues that are ran into down the road. Trust me, I spent like a week trying to get that to work.

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
