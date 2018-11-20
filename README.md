# Install dotfiles

```bash
$ echo 'alias dotfiles="/usr/bin/git --git-dir=$HOME/.dotfiles.git --work-tree=$HOME"' >> $HOME/.bashrc
$ source ~/.bashrc
$ echo ".dotfiles.git" >> .gitignore
$ git clone --bare https://www.gitlab.com/smacz/dotfiles.git $HOME/.dotfiles.git
$ for i in $(dotfiles checkout 2>&1| sed -n '/The following untracked working tree files/,/Please move or remove them/p' | sed '1d;$d'| sed -e 's/^[ \t]*//'); do dotfiles clean -f ${i}; done; dotfiles checkout
$ dotfiles config --local status.showUntrackedFiles no
```

> Wait...WTF is that `sed` pipe doing?!?

When the files are checked out for the first time, git realizes that they are trying to overwrite untracked files. This produces the following output:

```
$ dotfiles checkout
error: The following untracked working tree files would be overwritten by checkout:
        .bashrc
        .vimrc
Please move or remove them before you can switch branches.
Aborting
```

While there are quite a few places on the internet that mention doing a `git reset --hard`, that does not work in this situation. The untracked files will still be there in their original form. So we have to clean the working directory of them before we can place the version-controlled versions of those files.

This command takes the list of untracked files from `dotfiles checkout` by parsing the stderr of the output, and one-by-one force-cleaning them up, before executing the checkout at the very end, resulting in the correct file versions being placed in the correct places.

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
