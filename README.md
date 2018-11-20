# Install dotfiles

```bash
$ echo 'alias dotfiles="/usr/bin/git --git-dir=$HOME/.dotfiles.git --work-tree=$HOME"' >> $HOME/.bashrc
$ source ~/.bashrc
$ echo ".dotfiles.git" >> .gitignore
$ git clone --bare https://www.gitlab.com/smacz/dotfiles.git $HOME/.dotfiles.git
$ dotfiles checkout master
$ dotfiles reset --hard
$ dotfiles config --local status.showUntrackedFiles no
```

# Install Vundle

```bash
$ dotfiles submodule init
$ dotfiles submodule update
$ vim +PluginInstall +qall
```

# Install YCM

```bash
$ sudo dnf install -y cmake gcc-c++ make python-devel
```

# Install tmux

```bash
$ sudo dnf install -y tmux
```
