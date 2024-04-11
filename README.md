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

example `~/.vimrc` MIT gives:
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

## Lecture 4
