[[_The Linux Command Line | Back to Home]]

#ls, #less, #cd, #wildcard
___
##  cd Shortcuts
#table2-1
```bash
cd # Changes the working directory to your home directory.

cd - # Changes the working directory to the previous working directory

cd ~user_name
# Changes the working directory to the home directory of user_name.
# For example, typing cd ~bob will change the directory to the home
# directory of the user "bob".
```

## Common ls Options
#table3-1
```bash
-a, --all
# List all files, even those with names that begin with a period,
# which are normally not listed (hidden).

-A, --almost-all
# Like the -a option, except it does not list . (current directory)
# and .. (parent directory).

-d, --directory
# Ordinarily, if a directory is specified, ls will list the contents of the
# directory, not the directory itself. Use this option in conjunction with the
# -l option to see details about the directory rather than its contents.

-F, --classify
# This option will append an indicator character to the end of each listed
# name. For example, it will append a forward slash (/) if the name is
# a directory.

-h, --human-readable
# In long format listings, display file sizes in human-readable format
# rather than in bytes.

-l
# Display results in long format.

-r, --reverse
# Display the results in reverse order. Normally, ls displays its results in 
# ascending alphabetical order.

-S
# Sort results by file size.

-t
# Sort by modification time.
```

`ls -lrt` is a great command to view files sorted with the most recently modified files at the bottom. Useful for seeing the most commonly used log files.

## Wildcard Examples
#Table4-3
```bash
*
# all files

g*
# any file beginning with 'g'

b*.txt
# Any file beginning with 'b' followed by any characters
# and ending with .txt.

Data???
# Any file beginning with Data followed by exactly 3 characters.
```

## less Commands

| Command            | Action                                               |
| ------------------ | ---------------------------------------------------- |
| PAGE UP or B       | Scroll back one page                                 |
| PAGE DOWN or space | Scroll forward one page                              |
| Up arrow           | Scroll up one line                                   |
| Down arrow         | Scroll down one line                                 |
| G                  | Move to the end of the text file                     |
| 1G or g            | Move to the beginning of the text file               |
| /characters        | Search forward to the next occurence of characters   |
| n                  | Search for the next occurence of the previous search |
| h                  | Display help screen                                  |
| q                  | Quit less                                                     |



## Linux Directories
#directories
#linux
![[linux-dir.png]]


___
[[_The Linux Command Line | Back to Home]]