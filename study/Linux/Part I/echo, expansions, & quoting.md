[[_The Linux Command Line | Back to Home]]

#echo, #ch7
___
## Expansion
With expansion, we enter something, and it is expanded into something else before the shell acts upon it. For example, look at the `echo` command:
```bash
echo this is a test
this is a test
```

```bash
echo *
Desktop Documents ls-output.txt Music Pictures Public Templates Videos
```

* Any argument passed to `echo` gets displayed
* `echo` didn't print `*` since the shell expands the wildcard into something else (e.g. names of working directory)
* When `ENTER` is pressed, the shell automatically expands any qualifying characters on the CLI before the command is carried out, so the `echo` command never saw the `*`, only its expanded result.

### pathname Expansion
* Wildcards use **pathname expansion**

**Pathname Expansion Examples**
```bash
echo D*
Desktop Documents

echo *s
Documents Pictures Templates Videos

echo [[:upper:]]*
Desktop Documents Music Pictures Public Templates

echo /usr/*/share
/usr/kerberos/share /usr/loca/share
```

### Tilde Expansion
As discussed earlier in the book, the tilde character (~), when used at the beginning of a word, expands into the name of the home directory of the named user or, if no user is named, the home directory of the current user.
```bash
echo ~
/home/anthony

echo ~foo
/home/foo
```

### Arithmetic Expansion
The shell allows arithmetic to be performed by expansion. We can use it as a makeshift calculator.
```bash
echo $((2+2))
4

# Below is the allowed syntax for arithmetic:
$((expression))
```

==Expansion only supports whole integers (no decimals)==

Expressions can also be nested:
```bash
echo $(($((5**2)) * 3))
# This multiples 5 squared with 3
```

You can also use a single parenthesis to group multiple subexpressions:
```bash
echo $(((5**2) * 3))
```

**Supported Operators**
- Addition (+)
- Subtraction (-)
- Multiplication (\*)
- Division (/)
-  Modulo (%) - Simply means "remainder"
- Exponentiation (\*\*)

### Brace Expansion
- This can be used to create multiple text strings from a pattern containing braces:
```bash
echo Front-{A,B,C}-Back
Front-A-Back Front-B-Back Front-C-Back

echo {01..05}
01 02 03 04 05

# Nested
echo a{A{1,2},B{3,4}}b
aA1b aA2b aB3b aB4b
```

==The use case for this could be for making a list of files or directories with a naming scheme.==

Example:
```bash
mkdir Photos
cd Photos
mkdir {2007..2009}-{01..12}
ls
2007-01
2007-02
2007-03...
2008-01
2008-02
# you get the point...
```

### Parameter Expansion
- Will go more into detail later... but the basics:
```bash
# shows contents of the USER variable
echo $USER

# Lists available variables
printenv | less
```

### Command Substitution
You can also use the output of a command as an expansion: `echo $(ls)`

```bash
ls -l $(which cp)
-rwxr-xr-x 1 root root 7156 2007-12-05 08:58 /bin/cp
```

The above example pases the result of `which cp` as an argument to the `ls` command, thereby getting the listing of the cp program without having to know its full pathname.

## Quoting

Quoting can help for many use cases:
```bash
# below shows how the shell automatically removes whitespace
echo this is a         test
this is a test

# below shows how the shell attempts to return the variable "$1"
echo The total is $100.00
The total is 00.00
```

### Double Quotes
- If we place text inside double quotes, all the special characters used by the shell lose their special meaning (**exceptions are: $, \\, and** `)
```bash
# example how double quotes help
ls -l two words.txt
ls: cannot access two: No such file or directory
ls: cannot access words.txt: No such file or directory

ls -l "two words.txt"
-rw-rw-r--1 me me 18 2018-02-20 13:03 two words.txt
```

==Essentially, putting something in double quotes, tells the shell to treat that command as a single argument.==

### Single Quotes
* Use this if you want to suppress **all** expansion.

### Excape Characters
* A backslash (\\) can be used to selectively prevent an expansion.
```bash
echo "The balance for the user $USER is: \$5.00"
The balance for the user Anthony is $5.00
```

* Another purpose is so you can add special characters (normally those with special meaning in Linux/bash), to filenames.
```bash
mv bad\&filename good_filename
# the backslash here lets you chorrect the "&" character to an underscore
# (remember that the & character is often used to break a command,
# to follow with additional commands.)
```

___
[[_The Linux Command Line | Back to Home]]