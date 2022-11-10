[[_The Linux Command Line | Back to Home]]
#vi #vim #texteditor
___
# vi
* `vi` is found baked into most all Linux distros
* It is extremly lightweight and the most common visual text editor
* It was founded by Bill Joy (UC Berkley), who later cofounded Sun Microsystems
* `vim` is the enhanced replacemement and is a large improvement over `vi`. It is usually symbolically linked (aliased) to the name `vi`.

## Quitting vim
```bash
# You can open vim by simply typing:
vi

:q #this quits vim

:q! #this force quits vim

## if you ever get "lost" in vi, try hitting ESC twice.
```

## Editing Modes
```bash
# You can create a new file by passing the name of a nonexisting file to vim:
rm -f foo.txt
vi foo.txt
```

When you enter into a new file with `vi`, you enter into **command mode.** In this mode, ==every key is a command.==. To actually edit the file, enter **insert mode** by typing `i`.

Press `ESC` to exit insert mode.

To **save** your work, while in command mode, enter an `ex` command by pressing `:` , then type `w` (write) and press `ENTER`.

### vi Movement Commands
![[Pasted image 20221015111736.png]]

### Appending a line
Instead of entering insert mode with `i`, you can always type `a` to enter insert mode but also move the cursor past the end of the line so you can **append** text. `A` works better as it will automatically move the cursor from any point to the end of the line, where `a` only works if you are already at the end of the line.

### Opening a Line
You can use `o` or `O` to insert a blank line and enter insert mode:
![[Pasted image 20221015113440.png]]

>
>Note that while in command mode, the `u` key can **undo** changes made by the user.
>

### Deleting Text
While in command mode, the `x` command will delete a character. The `d` command is similar but more advance in that you can combine it with other keys to delete various aspects of your text.
![[Pasted image 20221015113940.png]]

### Cutting, Copying, and Pasting Text
The `d` command can also "cut" text. Each time we use `d`, the deletion is copied into a paste buffer (e.g. clipboard). We can later recall contents with the `p` command.

The `y` command is used to **yank** text (copy).
![[Pasted image 20221015114504.png]]

### Joining Lines
You can use `J` to join two lines together.

### Searching
You can use `f` to search within a line, and move the cursor to the next instance of the specified character. For example `f5` takes the cursor to the next instance of 5 on the current line.

Use `/` to search the entire file, just like the `less` command. Type `n` within the search to continue to the next matching charater/word.

### Global Search & Replace (Substitution)
```bash
# This command replaces all instances of the word "test", and replaces it with "funny".
:%s/test/funny/g
```

![[Pasted image 20221015121057.png]]

### Editing Multiple Files
```bash
# You can open multiple files at the same time with vim:
vim foo.txt ls-output.txt
```

When multiple files are open, `vim` will always display the first file. You can switch between them using `:bn` (move next), or `:bp` (move back). Use `~` at the end of the command in the case that `vi` prevents you from switching due to unsaved changes.

You can also type `:buffers` to view the list of files at the bottom of the display.

You can type `:buffer #` to select a file to switch to.

### Opening Additional Files for Editing
Use `:e` followed by a filename to open an additional file. For example, type `vi foo.txt` to open foo.txt, then type `e: ls-output.txt` 

### Copying Content from One File into Another
Copying files is easy. Simply use the combination of `y` commands (yank) and `p` (paste). You use these while switching between buffers to copy in-between files.
```bash
# move to first file
:buffer 1

# yank (copy) first line
yy

# switch to second file
:buffer 2

# paste
p
```

### Inserting an Entire File into Another
First, start a new `vi` session.
```bash
vi ls-output.txt
```

Move the curor to the 3rd line, then enter `:r foo.txt`. The `:r` command is short for "read" and inserts the specified file below the cursor position.

### Saving Our Work
* `:w` saves (writes) any changes made. It can optionally specify a filename (like Save As)
*  `:wq` saves & quits
* `zz` saves current file and exits vi

> Note that while `:w` can save a file under a new name, it does not change the name of the file you are editing. As you continue to edit, you will still be editing foo.txt, not foo1.txt.



[[_The Linux Command Line | Back to Home]]