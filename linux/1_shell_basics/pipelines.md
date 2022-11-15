[[_The Linux Command Line | Back to Home]]

#filter, #pipeline, #operator, #ch6
___
## Pipelines
The shell feature called **pipelines** is what enables the flow of data from input to output.
`command1 | command2`

For a demonstration, we can use `less` to display, page by page, the output of any command that sends its results to standard output (==This is extremly handy!==)
```bash
ls -l /usr/bin | less
```

## Filters
Pipelines are often used to perform complex operations on data. When combining multiple commands in a pipeline, you refer to them as **filters**.
> Filters take input, change it somehow, then output it.

*Example*
The below command is helpful because it takes the two seperate outputs of `ls /bin` and `ls /usr/bin`, but then sorts the entire output of both, thus providing a combined list to `less`.
```bash
ls /bin /usr/bin | sort | less
```

### Pipeline, compared to Redirection Operator
Simply put:
* `>` The redirection operator connects a command with a file.
* `|` The pipeline operator connects the output of one command with the input of a second command.

==The redirection operator (`>`) silently creates or overwrites files, so you need to treat it with a lot of respect.==

## Misc. Related Commands
#uniq, #wc, #grep, #head, #tail, #tee 

### uniq: Report or Omit Repeated Lines
* `uniq` is often used with `sort`
* Accepts a sorted list of data from standard input (keyboard) or a single filename, then **removes** any duplicates from the list.

```bash
ls /bin usr/bin | sort | uniq | less

# If we want to see the list of duplicates instead of the remaining output,
# use the -d option to 'uniq'.

ls /bin usr/bin | sort | uniq -d | less
```

### wc: Print Line, Word, and Byte Counts
* `wc` = "Word Count"
* Can accept items in a pipeline
* If executed without arguments, `wc` accepts standard input

```bash
# Below command counts the # of items in sorted list
ls /bin /usr/bin | sort | uniq | wc -l
```

### grep: Print Lines Mathcing a Pattern
* Used to find text patterns within files
`grep 'pattern' 'filename'`

```bash
# For example, use this to find all files with the word 'zip' in the name:
ls /bin /usr/bin | sort | uniq | grep zip
```

Other options include:
* `-i` : Cause grep to ignore case when performing search.
* `-v` : Tell grep to print only those lines that *do not* match the pattern.

### head/tail: Print First/Last Part of Files
* `head` prints only the first 10 lines of command output
* `tail` prints only the last 10 lines.
* The `-n` option can adjust the specific number of lines desired

```bash
# This lists the first 5 lines of output.
head -n 5 ls-output.txt
```

```bash
# When used in a pipeline
ls /usr/bin | tail -n 5
```

One useful option with `tail` is the `-f` argument
* ==This can be used to view files in real time - useful for log files.==
* The file will continue to be monitored, and can be closed out of with `CTRL + C`

### tee: Read from Stdin and Output to Stdout and Files
* `tee` reads standard input and copies it to both standard output (to continue pipeline), as well as one or more files.
* This is useful for capturing a piepleines contents at an intermediate stage of processing.

```bash
# This cmd captures the entire directory listing to the file 'ls.txt' before
# grep filters the pipeline's contents:

ls /usr/bin | tee ls.txt | grep zip
```

___
[[_The Linux Command Line | Back to Home]]