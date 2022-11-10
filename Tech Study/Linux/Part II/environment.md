[[_The Linux Command Line | Back to Home]]

#printenv, #set, #export, #alias
___

## What is stored in the environment?
- Most programs use the *configuration files*, but some  use environmental variables.
- There are 2 primary types of data in the environment (although both are indistinguishable!)
	1. **Environment variables**
	2. **Shell variables**

### Examining the Environment

* Use `printenv` to see **environmental variables**
* For any given variable, you can also verify its value by specifying the value:
```bash
printenv USER
aarmijo
```

* Use the `set` command to see **BOTH environmental variables and Shell variables**\*
(*including shell functions)

> Unlike `printenv`, `set` sorts output in alphabetical order

You can also see variable contents with the `echo` command:
```bash
echo $HOME
/home/aarmijo
```

Lastly,  one element of the environment that neither `set` nor `printenv` displays is **aliases**. To view aliases, simply type `alias` without arguments:
```bash
alias
# Below shows what the command returns:
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
#...(remaining output omitted)
```

## How is the Environment Established?
- First, after log-on to system, *bash* program starts and reads series of config scripts called **startup files** which define the default environment (==shared by all users==)
- Second, there are additional startup files ran from the user's home directory

The sequence will depend on type of shell session being started! There are 2 kinds:
1. **A login shell session**
	- e.g. we are prompted for username/pwd (starting a virtual console session)
2. **A non-login shell session**
	- This is when you launch a terminal session from the GUI

With method #1 (**login shell**), the startup files often used include:
**Table 11-2**: Startup Files for Login Shell Session

| File            | Contents                                                                                                          |
| --------------- | ----------------------------------------------------------------------------------------------------------------- |
| /etc/profile    | A global configuration script that applies to all users.                                                          |
| ~/.bash_profile | A User's personal startup file. It can be used to extend or override settings in the global configuration script. |
| ~/.bash_login   | If `~/.bash_profile` is not found, *bash* attempts to read this script.                                             |
| ~/.profile      | If neither `~/.bash_profile` nor `~/.bash_login` is found, bash attempts to read this file. This is the default in Debian-based distributions.                                                                                                                   |

Alternatively, non-login shell sessions read the startup files listed in Table 11-3:
**Table 11-3**: Startup Files for Non-Login Shell Sessions

| File             | Contents                                                 |
| ---------------- | -------------------------------------------------------- |
| /etc/bash.bashrc | A global configuration script that applies to all users. |
| ~/.bashrc        | A user's personal startup file. It can be used to extend or override settings in the global configuration script.                                                         |

## Modifying the Environment?
As a general rule...(to add directories to your *PATH* or define additional env variables)
* Place changes in `.bash_profile` (or `.profile` for Ubuntu)
* For anything else, place changes in `.bashrc`

### Text Editors
* Text editors are used to edit config files and write programs. Some popular ones used in Linux include:
	* GUI Based
		* gedit (GNOME built-in editor)
		* kedit
		* kwrite
		* kate (these 3 are found in KDE Linux)
	* Text Based
		* nano
		* vi (or the newer vim)
		* emacs (written by Richard Stallman)

```bash
# It's always important to backup config files before editing them!
cp .bashrc .bashrc.bak
```

Some changes to config files will not take effect until restarting the terminal session. This is because some config files are read during the beginning of a session.
```bash
# We can optionally force bash to reread a modified file (e.g. .bashrc)
source ~/.bashrc
```


___
[[_The Linux Command Line | Back to Home]]