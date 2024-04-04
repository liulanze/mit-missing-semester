# mit-missing-semester

## Lecture 1 Overview + The Shell

- echo Hello\ World
- echo $PATH -> /home/lanzeliu/.local/bin:/home/lanzeliu/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
- `cd -` -> swap between the current dir and the previous one dir.
- `-rwxr-xr-x` under `/usr/bin/` those are file permissions. Sequence: owner, group, any other else. You can see everyone has execute permission under this `/usr/bin/` since it make sense not checking who that is before running `echo` (example).
- `drwxr-xr-x` is permission for a directory for example `/usr`. Sequence also owner, group, any other else. The difference is for directory: 
    - read -> list, are you allowed to see which files are under this directory.
    - write -> rename, delete, move files under this directory.
    - execute -> search, are you allowed to enter / search this directory.
- echo hello > hello.txt -> dump that string into txt file.
- cat < hello.txt -> open right side of `<`, return the content as the input to the left side. `hello` printed. (on the contrary of pipe `|`)
- cat < hello.txt > hello2.txt
- `>>` -> append ops.
- `/sys` contains various Kernel parameters.
- `/sys/class/backlight$`
- `#` -> root, `$` -> usr
- `tee` package -> get an input and write it into a file, also print standard output. `echo 1060 | sudo tee brightness`
- `find -type f -name '*brightness*'` (an example of find)
- `xdg-open <file>` -> open a file with appropriate format. (for instance `.html` file to open a web browser)
