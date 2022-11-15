[[_The Linux Command Line | Back to Home]]

#help, #ch5, #apropos, #man, #whatis, #info, #alias
___
# Help & Aliases

## Identifying Commands
### type
* Shell builtin that display's a command's type
```bash
type type
'type is a shell builtin'

type ls
'ls is aliased to "ls --color=tty"'
```
### which
* Display's an executable's location
* Useful on servers, where an executable might have more than one version of an exe.
* ==This only works on executibles, not builtins or alises==
```bash
which ls
/bin/ls
```

## Getting a Command's Documentation
### help
* Built-in help for bash - available on each of the shell builtins.
```bash
help cd
output here...
```

Sometimes, programs also support a `--help` argument that displays a description of the command's supported syntac and options.

### man
* Display a program's manual or *man* page
* Man pages do not usually include examples, and are used for reference.
* `man` uses `less` to display the manual.

```bash
man ls
```

You can specify a specific section of the *man* page:
```bash
man 5 passwd
# This specifies the 'File formats' section of the man page.
```

**Table 5-1**: Man Page Organization
| Section | Contents                                       |
| ------- | ---------------------------------------------- |
| 1       | User commands                                  |
| 2       | Programming interfaces for kernal system calls |
| 3       | Programming interfaces for the C library       |
| 4       | Special files such as device nodes and drivers |
| 5       | File formats                                   |
| 6       | Games and amusements such as screen savers     |
| 7       | Miscellanrous                                  |
| 8       | System administration commands                                               |

### apropos
* Searches the list of man pages for possible matches based on a search term
* Crude, but can be helpful
```bash
apropos partition
# Returns list of all commands with 'partition' found in man page.
```

### whatis
* Displays the name and a one-line description of a man page
```bash
whatis ls
ls (1) - list directory contents
```

### info
* Alternative to man page, created by GNU projects
* `info` pages are hyperlinked, much like web pages
* The `info` program reads info files, which are tree structured individual **nodes**
* You can click on hyperlinks, or move cursor and hit `Enter`

### README & Other Docs
* Often found in ``/usr/share/doc`
	* Stored as HTML, txt, or gz (compressed)
	* gz (gzip) can be viewed with the `zless` command

## Creating Our own Commands with alias
==adding notes later==

___
[[_The Linux Command Line | Back to Home]]
