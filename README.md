# mit-missing-semester note

## Lecture 1 Overview + The Shell

- echo Hello\ World
- echo $PATH ->
  /home/lanzeliu/.local/bin:/home/lanzeliu/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
- `cd -` -> swap between the current dir and the previous one dir.
- `-rwxr-xr-x` under `/usr/bin/` those are file permissions. Sequence: owner,
  group, any other else. You can see everyone has execute permission under this
  `/usr/bin/` since it make sense not checking who that is before running `echo`
  (example).
- `drwxr-xr-x` is permission for a directory for example `/usr`. Sequence also
  owner, group, any other else. The difference is for directory: 
    - read -> list, are you allowed to see which files are under this directory.
    - write -> rename, delete, move files under this directory.
    - execute -> search, are you allowed to enter / search this directory.
- echo hello > hello.txt -> dump that string into txt file.
- cat < hello.txt -> open right side of `<`, return the content as the input to
  the left side. `hello` printed. (on the contrary of pipe `|`)
- cat < hello.txt > hello2.txt
- `>>` -> append ops.
- `/sys` contains various Kernel parameters.
- `/sys/class/backlight$`
- `#` -> root, `$` -> usr
- `tee` package -> get an input and write it into a file, also print standard
  output. `echo 1060 | sudo tee brightness`
- `find -type f -name '*brightness*'` (an example of find)
- `xdg-open <file>` -> open a file with appropriate format. (for instance
  `.html` file to open a web browser)

## Lecture 2 Shell Tools and Scripting..

- `source xyz.sh` -> automatically add bin to source for shall to execute.
- `/dev/null` -> discard message often used in output and any error messages.
- `find . -name src -type d`
- `find . -path "**/test/*.py' -type f`
- `locate README.md` -> similiar to `find`.
- ctrl + R and keep typing it for scrolling.

## Lecture 3 Editors (vim)

- normal mode and insert mode.
- `:sp` -> split a mirror terminal, `c + w` to switch screens.
- `:qa` -> quit all windows.
- `0` -> move to the beginning of the current line.
- `^` -> move to the first non-space bit of the current line.
- `$` -> move to the end of the current line.
- `c + u` -> goes up. `c + d` goes down.
- `G` -> goes the end of the file. `gg` -> goes the beginning of the file.
- `f<>` -> find the first char, for example `fo` find the first `o` in the line.
- `u` -> revert / undo. `c + r` redo.
- `5dd` -> delete 5 lines beginning from the current cursor. `dw` -> delete the
  following word.
- `y` -> copy. `p` -> paste.
- `yy` -> copy the line. `yw` -> copy the word.
- `v` -> visual mode, this mode allows many common functions like regular
  editor. For example you can use `c + arrows` to select lines.
- `4j`, `1k`, `2h`, `3l` -> move number of steps.
- `/` -> search / find. `n` -> next matched one. `N` -> previous matched one.

example `~/.vimrc` MIT gives (rc stands for run commands):
```
" Comments in Vimscript start with a `"`.

" If you open this file in Vim, it'll be syntax highlighted for you.

" Vim is based on Vi. Setting `nocompatible` switches from the default
" Vi-compatibility mode and enables useful Vim functionality. This
" configuration option turns out not to be necessary for the file named
" '~/.vimrc', because Vim automatically enters nocompatible mode if that file
" is present. But we're including it here just in case this config file is
" loaded some other way (e.g. saved as `foo`, and then Vim started with
" `vim -u foo`).
set nocompatible

" Turn on syntax highlighting.
syntax on

" Disable the default Vim startup message.
set shortmess+=I

" Show line numbers.
set number

" This enables relative line numbering mode. With both number and
" relativenumber enabled, the current line shows the true line number, while
" all other lines (above and below) are numbered relative to the current line.
" This is useful because you can tell, at a glance, what count is needed to
" jump up or down to a particular line, by {count}k to go up or {count}j to go
" down.
set relativenumber

" Always show the status line at the bottom, even if you only have one window open.
set laststatus=2

" The backspace key has slightly unintuitive behavior by default. For example,
" by default, you can't backspace before the insertion point set with 'i'.
" This configuration makes backspace behave more reasonably, in that you can
" backspace over anything.
set backspace=indent,eol,start

" By default, Vim doesn't let you hide a buffer (i.e. have a buffer that isn't
" shown in any window) that has unsaved changes. This is to prevent you from "
" forgetting about unsaved changes and then quitting e.g. via `:qa!`. We find
" hidden buffers helpful enough to disable this protection. See `:help hidden`
" for more information on this.
set hidden

" This setting makes search case-insensitive when all characters in the string
" being searched are lowercase. However, the search becomes case-sensitive if
" it contains any capital letters. This makes searching more convenient.
set ignorecase
set smartcase

" Enable searching as you type, rather than waiting till you press enter.
set incsearch

" Unbind some useless/annoying default key bindings.
nmap Q <Nop> " 'Q' in normal mode enters Ex mode. You almost never want this.

" Disable audible bell because it's annoying.
set noerrorbells visualbell t_vb=

" Enable mouse support. You should avoid relying on this too much, but it can
" sometimes be convenient.
set mouse+=a

" Try to prevent bad habits like using the arrow keys for movement. This is
" not the only possible bad habit. For example, holding down the h/j/k/l keys
" for movement, rather than using more efficient movement commands, is also a
" bad habit. The former is enforceable through a .vimrc, while we don't know
" how to prevent the latter.
" Do this in normal mode...
" nnoremap <Left>  :echoe "Use h"<CR>
" nnoremap <Right> :echoe "Use l"<CR>
" nnoremap <Up>    :echoe "Use k"<CR>
" nnoremap <Down>  :echoe "Use j"<CR>
" ...and in insert mode
" inoremap <Left>  <ESC>:echoe "Use h"<CR>
" inoremap <Right> <ESC>:echoe "Use l"<CR>
" inoremap <Up>    <ESC>:echoe "Use k"<CR>
" inoremap <Down>  <ESC>:echoe "Use j"<CR>
```

## Lecture 4 Data Wrangling

- one code style suggestion: change `ssh <remote_server> journalctl | grep ssh |
  grep "Disconnected from" | less` => `ssh <remote_server> 'journalctl | grep
  ssh | grep "Disconnected from"' | less`

  By this way, make all required ops only happens in the server, not the host.
- `sed` -> modify content of course.
- regular expression: `.` -> any characters. `*` -> 0 or any previous
  characters. `.*` -> any number of any characters.
- `[ab]` -> a or b character. So, `s/[ab]//` (aba / bba) => (ba). `s/[ab]//g` =>
  ().
- `(ab)` -> ab string.
- `s/(ab|bc)*//g` -> remove ab or bc. - one good example: `cat ssh.log | sed -E
's/^.*Disconnected from (invalid |authenticating )?user (.*) [0-9.]+ port [0-9]+
( \[preauth\])?$/\2/'`

  - `^` -> beginning of the text. `$` -> end of the text.
  - `?` -> 0 or 1.
  - `(..)` represent a group, you can see there are three groups in the example,
    note that the second group does not do any ops from sed, but for the
    replacement `\2`, it put the second group content string `(.*)` here.
- material: regular expression 101 -> https://regex101.com/
- `.*?Disconnected from ... ()` -> that `?` will make sure once it finds the
  first that pattern, it will treat the rest of content as group in this case.
- `wc -l` count the lines of an output or a file.
  - `wc` -> word count.
  - `-l` -> lines.
- `sort`
- `uniq -c` -> unique count.
- `awk` -> column based stream processor. `awk` has lots of functions and it is
  a programming language.
  - `awk '$1 ==1 && $2 ~ /^c.*e$/ {print $0}` => print the columns that second
    column matches starts with c and end with e.
- `bc` -> berkerly count. `bc -l` calculate probably two string plus, like "1+1"
  | bc -l => 2.
- `xargs`: organize output and put them as arguments.
  - example: `rustup toolchain list | grep nightly | grep -v 'nightly-x86' |
    grep 2019 | sed 's/-x86.*//' | xargs rustup toolchain uninstall` => `rustup
    toolchain uninstall <> <> <> ... <>
- `ffmpeg` -> tool converting audio / video.
- `tee` -> dump / write the output to file(s) in the meantime print the output.

## Lecture 5 Command-line Environment

- `signal` package - catch some terminal operations. Like if you have `ctr + c`
  it can catch that user ops.
- `alias <>`. Example `alias ll` => `ls -lah`.
- `alias gs=git status`, however, I think this might cause conflict, sometimes
  giving full context won't hurt the thing too much, or make things mess.
- This `alias` can also be put into `.bashrc` file to make it work.
- dotfile.
- How to generate a ssh connection:
  - `ssh-keygen` => generate key pair under `~/.ssh`: `id_rsa` & `id_rsa.pub`.
  - `sudo apt install openssh-server`
  - `sudo systemctl start sshd` => `systemctl` supported by `systemd` to enable
    the sshd server daemon.
- An example of `~/.ssh/config`:
  ```
  Host vm1
    User user1
    HostName 192.168.xxx.xxx
    IdentityFile ~/.ssh/id_rsa
    RemoteForward 9999 localhost:8888
  ```
- `tmux` -> manage multiple terminal sessions within a single window, useful? Or
  make it more complex?

## Lecture 6 Version Control (git)

- `git remote add <remote name> <remote repository URL>` -> `<remote name>`:
  This is the shorthand name you assign to the remote repository. Common names
  include `origin` for the primary or default remote, and `upstream` typically
  used for the original repository when you have forked a project.

## Lecture 7 Debugging and Profiling

- n/a on note.

## Lecture 8 Metaprogramming (build system / Makefile / make / release version)

- `%` stands for any string file name.
- `$*` -> display the stem, base name of the file without the extension.
- `$@` -> represent the target of the rule.
- `$<` -> represent the first prerequisite of the rule.
- `version` for break debugging purpose mainly. Remember major version, minor
  version, and patch / release version.
- A lock file in software development is NOT primarily for version control in
  the traditional sense, like Git. Instead, it's used in dependency management
  systems within various programming environments to control and manage the
  exact versions of packages and dependencies used in a project. This ensures
  consistency across different development environments and production, and
  helps avoid "it works on my machine" issues. Freeze the ecosystem.
- `Continuous Integration` (those bars under README Github project repo) -> like
  when you push PR there will be a PR pipeline testing run. <- achieved by event
  triggered actions.
- `cmake` -> generate make file for c project. Usually if the make file is
  large, sometimes they have a template build tool for all for general usage.
- `maven` / `ant` help to build Java env / eco.

## Lecture 9
