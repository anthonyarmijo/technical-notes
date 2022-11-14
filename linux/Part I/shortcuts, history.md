[[_The Linux Command Line | Back to Home]]

#historyexpansion, #shortcuts
___

## Shortcuts
refer to #ch8

![[shortcuts.png]]

## History Expansion
* Command history is stored in **home directory** in a file called `.bash_history`
	* Be default, bash stored the last 500 commands here
	* Ch11 shows how to adjust this value
```bash
# you can search your command history, like below, which searches for past
# commands that involved the /usr/bin directory
history | grep/usr/bin 
88 ls -l /usr/bin > ls-output.txt
```

You can then use something called ==history expansion (!)== by referencing the line number in your history, which will call that command specifically: `!88`

Using `!88` would use history expansion to expand the 88th line in our command history to `ls -l /usr/bin > ls-output.txt`

You can use `Ctrl+R` to perform a ==reverse incremental search== which will immediately return past commands up as you type/search for a command.

___
[[_The Linux Command Line | Back to Home]]