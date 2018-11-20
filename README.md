# Install dotfiles

```bash
$ echo 'alias dotfiles="/usr/bin/git --git-dir=$HOME/.dotfiles.git --work-tree=$HOME"' >> $HOME/.bashrc
$ source ~/.bashrc
$ echo ".dotfiles.git" >> .gitignore
$ git clone --bare https://www.gitlab.com/smacz/dotfiles.git $HOME/.dotfiles.git
$ for i in $(dotfiles pull 2>&1| sed -n '/The following untracked working tree files/,/Please move or remove them/p' | sed '1d;$d'| sed -e 's/^[ \t]*//'); do dotfiles clean -f ${i}; done; dotfiles pull
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
for i in ; do dotfiles clean -f README.md; done; dotfiles pull
