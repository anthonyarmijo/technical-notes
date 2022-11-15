[[_The Linux Command Line | Back to Home]]

#operator, #FileDescriptor, #ch6
___
## Redirecting Standard Output
`> `: Write output to a specific file (overwrite)
`>> `: **Append** output to a specific file

```bash
ls -l / >> output.txt
```

## Redirecting Standard Error
In the example below, since the /bin/usr directory doesn't exist, it will return an error code to the screen; BUT it will not write the error output to *ls-error.txt*
```bash
ls -l /bin/usr > ls-error.txt
```

The reason for this is because the **ls** program does not send its error messages to standard output (*stdout*). Most well-written unix programs send error messages to the standard error (*stderr*) file.
___
If you want to write the error output to a file, you need to reference the correct **file descriptors**:
> 0 = Standard Input
> 1 = Standard Output
> 2 = Standard Error
___
Thus, the correct way to redirect Standard Error messages is by specifying its descriptor:
```bash
ls -l /bin/usr 2> ls-error.txt
```

## Redirecting Standard Output & Standard Error to One File
Using this method, we perform two redirections:
1. First, redirct standard output (descriptor 1) to *ls-output.txt*
2. Then, redirect standard error (descriptor 2) to 
3. standard output (descriptor 1).

> Note that redirecting standard output must always come **before** redirecting standard error.

```bash
ls -l /bin/usr > ls-output.txt 2>&1
```

The command below **will not work** due to the incorrect order:
```bash
2>&1 > ls-output.txt
```

Newer versions of bash provide a more streamlined method:
```bash
ls -l /bin/usr &> ls-output.txt
```

You can also combine this with the "append" method so that you combine standard output and standard error streams into a single file:
```bash
ls -l /bin/usr &>> ls-output.txt
```

## Disposing Unwanted Output
You can "throw away" output by redirecting to a special file: `/dev/null`.
> This file is often referred to as a *bit bucket* which accepts input but does nothing with it.

Thus, supressing error messages can be accomplished with:
```bash
ls -l /bin/usr 2> /dev/null
```

## Redirecting Standard Input
The `cat` or **Concatenate** command reads one or more files and copies them to standard output.

Because `cat` can accept more than one argument, it can be used to join files together:
```bash
# example, we have multiple video files:
# movie.mpeg.001 movie.mpeg.002 ... movie.mpeg.099

cat movie.mpeg.0* > movie.mpeg
```

The wildcard above allows `cat` to join the movies together in the correct order.

If `cat` is not given any arguments, it attempts to read from standard input (descriptor 0). Thus, typing `cat` will cause bash to wait for the user to type in something.

You can use `cat` to create text files with content, for example:
```bash
cat > lazy_dog.txt
The quick brown fox jumped over the lazy dog.
```

Once you type in your desired content, you'll need to `Ctrl + D` to tell `cat` that the command has reach EOF (end of file).

==Finally, you can redirect standard input by simply flipping the redirection operator. This simply allows you to change the source of standard input from the keyboard, to a file.==:
```bash
cat < lazy_dog.txt
```

___
[[_The Linux Command Line | Back to Home]]