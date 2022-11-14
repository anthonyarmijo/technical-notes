[[_The Linux Command Line | Back to Home]]

#process, #ps, #top, #jobs, #bg, #fg, #kill, #killall, #shutdown, #ch10
___
## Process Basics
* `init` is the primary program which can initialize shell scripts (from `/etc`) - these scripts are called **init scripts**
* Many of these services are implemented as *daemon programs*, which are programs that sit in the background
* When a program launches another program, the first one is referred to as a **parent process** and the second, a **child process**

## Viewing Processes
```bash
# Here, ps provides running processes.
	# TTY = "teletype" and refers to the controlling terminal.
	# TIME = Amount of CPU time consumed by the process
ps
PID   TTY        TIME     CMD
5198  pts/1      00:00:00 bash
10129 pts/1      00:00:00 ps
```

As seen below, you can use `ps x` to get more comprehensive info since it shows all processes, regardless of which terminal (if any) they are controlled by. The presence of a `?` indicates there is no controlling terminal. `STAT` refers to the state of the process (see table for meanings.)
![[Pasted image 20220929114621.png]]

**Table 10-1**: Common Process States

| State | Meaning                                                                                                                                                                                                                                                                                             |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| R     | Running. This means the process is running or ready to run.                                                                                                                                                                                                                                         |
| S     | Sleeping. The process is not running; rather, it is waiting for an event, such as a keystroke or network packet.                                                                                                                                                                                    |
| D     | Uninterruptiple sleep. The process is waiting for I/O such as a disk drive.                                                                                                                                                                                                                         |
| T     | Stopped. The process has been instructed to stop. You'll learn more about this later in the chapter.                                                                                                                                                                                                |
| Z     | A defunct or "zombie" process. This is a child process that has terminated but has not been cleaned up by its parent.                                                                                                                                                                               |
| <     | A high-priority process. It's possible to grant more importance to a process, giving it more time on the CPU. This property of a process is called niceness. A process with high priority is said to be less nice because it's taking more of the CPU's time, which leaves less for everybody else. |
| N     | A low-priority process. A process with low priority (a nice process) will get processor time only after processes with higher priority have been services.                                                                                                                                                                                                                                                                                                    |

`ps aux` will go into even further detail by providing processes from every user on the host, as well as other percentage details:
![[Pasted image 20220929132550.png]]

### Viewing Processes Dynamically with top
* `top` provides a more dynamic view of processes
* Updates every 3 seconds by default
* Composed of 2 parts:
	* System sumary at the "top"
	* Followed by table of CPU processes (sorted by activity %)
![[Pasted image 20220929132912.png]]

## Controlling Processes
You can launch a program by simply typing the name:
```bash
xlogo
# Note that this program is included in most linux distros, and is useful for testing. It should being up a resizable window with an "X" in it.

```
### Interrupting a Process
* Simply use  `Ctrl + C`

### Putting a Process in the Background
==To launch a program so that it is immediately placed in the background, we follow the command with an amersand (&) character.==
```bash
xlogo &
[1] 28236
# this return is part of shell's "job control" feature which returns the PID.

# As you can see below, we have access to the shell, but xlogo is still running in the background allowing you to continue working.
ps
PID   TTY        TIME     CMD
5198  pts/1      00:00:00 bash
10129 pts/1      00:00:00 ps
28236 pts/1      00:00:00 xlogo
```

The shell's job control facility can also let us see jobs we've launched:
```bash
jobs
[1]+   Running       xlogo &
```

### Returning a Process to the Foreground
- Simply use the `fg` command and then a `%` + the job number (oficially called **jobspec**)
- In the previous example, the jobspec is the first number listed ==[1]==
```bash
fg %1
```

### Stopping (Pausing) a Process
* Simply use `Ctrl + Z` to temporarily stop a process, **without** terminating it.
* You can then either:
	* Use the `bg %[#]` command to continue the program's execution in the background **OR**
	* Use the `fg %[#]` command to continue the program's execution in the foreground.

## Signals
- The `kill` commmand sends a specific **signal** to the program
- ==If no specific **signal** is specified, it will send a TERM (terminate) command==

```bash
xlogo &
[1] 28236

kill 28236
# OR
kill %1
```

### Sending Signals to Processes with kill
* The syntax for kill is: `kill -signal PID`
* You can specify the signal to something other than the default terminate command as well (see chart below)
* Unlike the terminate signal, you can specify `-9` to *forecfully* kill a process.
	* **==When this is used, rather than a signal being sent, the kernal immediately terminates the program without allowing any time for the program to gracefully shutdown/cleanup.**==

![[Pasted image 20220930101219.png]]
*See pg. 143 for more definitions of these signals.*

```bash
xlogo &
[1] 28236

# FINISH HIM!
kill -9 %1

# FATALITY...

# Another example...
kill -SIGINT 28236 # you can use the signal name instead of the value if desired
```

### Sending Signals to Multiple Processes with killall
* `killall` simply lets you shutdown multiple processes with the same name - by referencing the name: `killall xlogo`

### Shutting Down the System
4 Possible commands:
	1. `halt`
	2. `poweroff`
	3. `reboot`
	4. `shutdown`

* Reboot is self explanatory.
* The `shutdown` command has many options, including using delay, more reboot options, and warning messages to users.

```bash
# This immediately shuts down system:
sudo shutdown -h now
```

*Refer to `man shutdown` for more options*


### More Process-Related Commands
| Command | Description                                                                                                                                                                                                                                    |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| pstree  | Outputs a process list arranged in a tree-like-pattern showing the parent-child relationships b/w processes.                                                                                                                                   |
| vmstat  | Outputs a snapshot of a system resource usage including memory, swa, and disk I/O. To see a contiuous display, follow the command with a time delay (in seconds) for updates. Here's an example: vmstat 5. Terminate the output with CTRL + C. |
| xload   | A graphical program that draws a graph showing system load over time.                                                                                                                                                                          |
| tload   | Similar to xload program but draws the graph in the terminal. Terminate the output with CTRL + C.                                                                                                                                                                                                                                               |

___
[[_The Linux Command Line | Back to Home]]