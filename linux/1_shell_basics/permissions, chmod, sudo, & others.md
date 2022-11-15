[[_The Linux Command Line | Back to Home]]

#id, #chmod, #umask, #su, #sudo, #chown, #chgrp, #passwd
___
## Owners, Group Members, and Everybody Else
* Users may "own" files
* Unix has a term called **=="world"==** which refers to **all users** on a unix system.
* Modern Linux practice is to create a unique, single-member group with the same name as the user.

**Directories**
- User accounts are defined in the `/etc/passwd` file
- Groups are defined in the `/etc/group` file
- Password info is defined in `/etc/shadow`
- For each user account, the following details are stored in `/etc/passwd`
	- user (login) name
	- uid
	- gid
	- account's real name
	- home directory
	- login shell

## Reading, Writing, and Executing
* Below shows an example of the syntax of the **file attributes** of a file. The first character is the **file type**. The 9 Characters beyond the file type are the ==**file mode**==.
![[permissions.png]]
==Note that 'user permissions' in the chart above really refers to the the **file owner**==

### Reference Charts
**Table 9-1**: File Types

| Attribute | File Type                                                                                                                                                                                              |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| -         | A regular file                                                                                                                                                                                         |
| d         | A directory                                                                                                                                                                                            |
| l         | A symbolic link. Notice that with symbolic links, the remaining file attributes are always rwxrwxrwx and are dummy values. The real file attributes are those of the file the symbolic link points to. |
| c         | A character special file. This file type refers to a device that handles data as a stream of bytes, such as a terminal or /dev/null.                                                                   |
| b         | A block special file. This file type refers to a device that handles data in blocks, such as a hard drive or DVD.                                                                                      |

**Table 9-2**: Permission Attributes

| Attribute | Files                                                                                                                                                                                            | Directories                                                                                               |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------- |
| r         | Allows a file to be opened and read.                                                                                                                                                             | Allows a directory's contents to be listed if the execute attribute is also set.                          |
| w         | Allows a file to be written to or truncated; however, this attribute does not allow files to be renamed or deleted. The ability to delete or rename files is determined by directory attributes. | Allows files within a directory to be created, deleted, and renamed if the execute attribute is also set. |
| x         | Allows a file to be treated as a program and executed. Program files written in scripting languages must also be set as readable to be executed.                                                 | Allows a directory to be entered, e.g. `cd directory`.                                                      |

![[Pasted image 20220927230221.png]]


### chmod: Change File Mode
* `chmod` can be used to change the mode (permissions) of a file or directory
* Only the file's owner or the superuser can do this.

**`chmod` has 2 methods for specifying changes
1. Octal number representation
1. Symbolic representation

#### Octal Number Representation
* Refer to prior chart for octal examples.
* Octal (base 8) numbering system is just a way to specify a binary number to indicate the file mode in a Linux file system.
```bash
# Let's set a file permission using an octal number!

# Create foo.txt and check it's default file permissions
> foo.txt
ls -l foo.txt
-rw-rw-r-- 1 me me 0 2018-03-06 14:52 foo.txt

# Change the permission to read/write for file owner only
chmod 600 foo.txt
ls -l foo.txt
-rw------ 1 me me 0 2018-03-06 14:52 foo.txt
```

**Table 9-4**: File Modes in Binary and Octal

| Octal | Binary | File Mode |
| ----- | ------ | --------- |
| 0     | 000    | ---       |
| 1     | 001    | --x       |
| 2     | 010    | -w-       |
| 3     | 011    | -wx       |
| 4     | 100    | r--       |
| 5     | 101    | r-x       |
| 6     | 110    | rw-       |
| 7     | 111    | rwx          |

#### Symbolic Notation
**3 Components**
* Who the change will affect
* Which operation will be performed
* What permission will be set

**Table 9-5**: chmod Symbolic Notation

| Symbol | Meaning                                                 |
| ------ | ------------------------------------------------------- |
| u      | Short for "user" but means the file or directory owner. |
| g      | Group owner.                                            |
| o      | Short for "others" but means world.                     |
| a      | Short for "all". This is a combination of u, g, and o.                                                        |
![[Pasted image 20220928111729.png]]
![[Pasted image 20220928111531.png]]

### unmask: Set Default Permissions
* `umask` changes the default ==binary mask== for file permissions, which controls the file permission type for all **new** files created.
- Usually not required to change; but could be helpful for high-security environments.

**Example: Mask `0022`**

| Original file mode | --- rw- rw- rw- |
| ------------------ | --------------- |
| Mask               | 000 000 010 010 |
| Result             | --- rw- r-- r--                |

### Special Permissions
* There are a few special permission settings that utilize all 4 digits
* These settings are less common, but can apply special permissions.

##### setuid bit (octal 4000)
* Can be applied to an executable file
* Changes the *effective user ID* from that of the real user to the program's owner.
* Often its used to give a few programs superuser privileges, regardless of which user runs it.
	* You'll see this if a program is configured with `setuid root`

##### setgid bit (octal 2000)
* Similar to setuid, but used for **groups**
* If set on a directory, newly created files will be given the group ownership of the directory rather than the group ownership of the file's creator.
* Useful in shared directories when members of a common group need access to all files in the directory, regardless of the file owner's primary group.

##### sticky bit (Octal 1000)
* Remenant of ancient Unix
* A little confusing



## Changing Identities
**3 Primary ways to change identity**
1. Log out and back in as alternate user
2. Use the `su` command
3. Use the `sudo` command

### su: Run a Shell with a Subsitute User and Group IDs
* Syntax: `su [-[l]] [user]`
	* `-l` indicates that you want the user's environment to load into the working directory (e.g. home dir)
	* `-l` is optional but usually desired.
	* ==`-l` is often abbreviated to `-`==
	* ==**If a user is ommited, the superuser is assumed**==

```bash
# assuming superuser
[me@linuxbox~]$ su -
Password:

[root@linuxbox ~]#
```

```bash
# execute sudo command for a single command
su -c 'command'

# ensure command is kept within quotes for proper expansion
```

### sudo: Execute a Command as Another User
- Similar to `su` but has added capabilities:
	- Admin can control which commands sudo has access to (for a specific user)
	- `sudo` does not require the superuser password, instead user uses their own.
- `sudo` does **not** start a new shell/environment
* You can still start an interactive superuser session (much like `su -`) using the `-i` option.

```bash
# See what privileges are granted by sudo
sudo -l
```
 
### chown: Change File Owner and Group
* `chown` is used to change the owner and group owner of a file or directory
* Superuser priv is required to run this command
```bash
chown [owner][:[group]] file...
```

In the `chown` command syntax as shown above, there are 3 values:
	1. file owner
	2. group owner
	3. file/directory name

To further demonstrate, here are a couple of examples:
```bash
# Change ownership of file from current owner -> Bob
chown bob $file

# Change ownership of file from current owner to bob. Change file group owner to 'users'
chown bob:users $file

# Change file owner from current owner to bob, change group owner to login group of user bob
chown bob: $file
```

### chgrp: Change Group Ownership
* Used in older versions of Linux
* `chown` replaces this as it can manage both users and groups

## Exercising our Privileges
### Example 1: Create Shared Directory
Requirements:
- Create shared directory
- Allow 2 users (bill and karen) access to store/read music

```bash
# First, use GUI to create a `music` group and add bill/karen to it

# create directory
sudo mkdir /usr/loca/share/Music

# confirm current permissions (owned by root user and group, permissions = 755)
ls -ld /usr/loca/share/Music
drwxr-xr-x 2 root root 4096 2018-03-21 18:05 /usr/local/share/Music

# Change group ownership to music group
sudo chown :music /usr/local/share/Music/test_file
sudo chmod 775 /usr/local/share/Music

# Confirm permissions again (owned by root user and group 'music', permissions = 775)
ls -ld /usr/local/share/Music
drwxrwxr-x 2 root music 4096 2018-03-21 18:05 /usr/local/share/Music

# Set the 'setgid' bit on the directory so that all files/dirs created by a member will inherit group ownership (music) instead of the owner's
sudo chmod g+s /usr/local/share/Music

# set default umask to 0022 to 0002. By default, 0022 will prevent group members from writing files belonging to other members of the group. Note that this change is temporary (lost after session restart). CH11 shows permanent umask changes.
umask 0002

```

## Changing Your Password
* Basic password change syntax: `passwd [user]`
	* `[user]` is optional. Command will otherwise default to changing your own PWD

___
[[_The Linux Command Line | Back to Home]]