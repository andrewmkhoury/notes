# Command Reference

## Screen command
Create a screen session:
```bash
screen -S myscreensession
```

Find running screen sessions:
```bash
$ screen -ls
There is a screen on:
	7115.myscreensession	(12/02/22 02:30:35)	(Detached)
1 Socket in /run/screen/S-iser.
```

Reattach to screen session:
```bash
screen -r myscreensession
```
OR, if there are multiple sessions with same name then use the id:
```bash
screen -r 7115.myscreensession
```

To kill that session and all its processes:
```bash
screen -XS 7115.myscreensession quit
```

Create a screen session with a log file and string of commands all in one (similar to how nohup is used but you can re-attach to the session):
```bash
screen -L -Logfile ${OUTPUT_DIR}/runRepoStats.log -dmS runRepoStats bash -c "./script.sh; echo \"Script is done running\""
```

## Various Commands
http://www.pixelbeat.org/cmdline.html 

## RHEL Commands
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/4/html/introduction_to_system_administration/s1-resource-rhlspec

## Display OS Version
### All Linux Distros
```bash
%> head -n1 /etc/issue 
```

### RHEL
```
%> cat /etc/redhat-release 
```

### Solaris Commands
https://docs.oracle.com/en/database/oracle/oracle-database/19/ssdbi/verifying-operating-system-version-on-oracle-solaris.html#GUID-DCEE5C3B-B26B-450E-9DD1-846476D2A2CF
```bash
%> cat /etc/release
Oracle Solaris 11.4 SPARC
```

## System Information

### Display Kernel Ver. and System Info
*Kernel version:*
```bash
uname -r
5.4.0.26-generic
```

*Display all system info:*
```bash
%> uname -a 
```

### Display Processor Spec
```conasole
%> cat /proc/cpuinfo
```


## User Management
### Add User
```bash
%> useradd 
```

### Limit Resources Available to User
```bash
%> ulimit 
```

## View Memory Usage
### Display the memory usage in MB
```bash
%> free -m
Poll Memory Usage
```
### Display the memory usage polling every 2 seconds 
```bash
%> watch free -m 
```

### List all active processes with their memory usage and cpu usage
```bash
%> top 
M - will sort by memory usage (highest to lowest) 
P - will sort by CPU percentage (highest to lowest) 
```

## Debugging OS Level Issues
### Output the system calls that are made by a command: 
```bash
%> strace <command> e.g. %> strace java MainClassName
```

* `-p` parameter takes the pid instead of the actual command
e.g.
```bash
strace -p 111
```

## Adding a Swap File (Redhat Ent.)
1. Determine the size of the new swap file in megabytes and multiply by 1024 to determine the number of blocks. For example, the block size of a 64 MB swap file is 65536. 
2. At a shell prompt as root, type the following command with count being equal to the desired block size: 
    ```bash
    dd if=/dev/zero of=/swapfile bs=1024 count=65536 
    ```
3. Setup the swap file with the command: 
    ```bash
    mkswap /swapfile 
    ```
4. Enable swap file immediately (will not be enabled at boot) 
swapon /swapfile 
5. Enable swap file at reboot, edit /etc/fstab 
    ```
    /swapfile swap swap defaults 0 0 
    ```
6. Verify it is enabled 
    ```bash
    cat /proc/swaps
    ```

## Disk Utilization
### Display Free Disk Space
*Display free disk space in a human readable format:*
%> df -h 

*Display The Size of a File or Directory*
`-h` option makes it human-readable instead of just bytes
```bash
%> du -h /path/to/file 
```

## Open Files
### List Open Files
#### List the open files: 
```bash
%> lsof
```
Lists of all disk files, pipes, network sockets and devices opened by all processes

```bash
$> PID=1234
%> lsof -p $PID > lsofoutput.txt
```
Lists all open files held by process with `$PID`

```bash
$> PID=1234
%> lsof -p $PID | wc -l
```
Lists number of files open and held by a specific process with $PID

## Increase Open File Limit in RHEL

```bash
ulimit -n 8092
```
Sets the user limit for allowable open files 


## Find all Subdirectories and Run a Command on Them

Find all subdirectories of the current directory and set the permissions to allow listing: %> find . -type d -exec chmod 711 '{}' \; 
Search for all occurrences of a string within a directory and its subdirectories


```bash
%> find . \( -name "*.xml" \) -exec grep 3873 '{}' \; -print 
```
The command above will search in all xml files in the current directory and all subdirectories for occurences of the string "3873". Matches will be printed along with filenames. 

```bash
%> find . \( -name "*.xml" \) -type f -exec sed -i 's/3873/3874/g' '{}' \; -print
```
The command above will search in all xml files in the current directory and all subdirectories for occurences of the string "3873" and replace these occurences with "3874". 

## Load the US Keymap
```bash
%> loadkeys us.map.gz 
```

## File Operations
### Securely Copy Files Between 2 Servers
To copy a file or folder from hostB to hostA home dir, while logged in to hostB: %> scp filename username@hostA.com:. 
```bash
%> scp -r folder username@hostA.com:. 
```

To copy a file or folder from hostA to hostB home dir, while logged in to hostB: %> scp username@hostA.com:filename . 
```bash
%> scp -r username@hostA.com:folder . 
```

## Zip/Unzip Files Using Zip
```bash
%> zip -r foo foo 
```
zip all files in dir foo to foo.zip 

```bash
%> unzip -l foo.zip 
```
list contents of foo.zip 

```bash
%> unzip foo.zip -d foo 
```
unzip all files in foo.zip to dir foo

## Zip/Unzip Files Using Tar Gzip


```bash
%> tar -czf /path/to/output/folder/filename.tar.gz /path/to/folder 
```
Zip the archive to the specified output tar.gz file path 

```bash
%> tar -tzf /path/to/archive/filename.tar.gz 
```
List the contents of the archive

```bash
%> tar -zxvf /path/to/folder/filename.tar.gz
# or
%> gunzip -c /path/to/folder/filename.tar.gz
```
Unzip the archive to the current directory 


Create a Symbolic Link



ln -s < target dir or file> ./<SHORTCUT> 
e.g. %> ln -s /usr/local/apache/logs ./logs 
Remove Symbolic Link
```bash
%> unlink <symlink> 
```


## Find out where an executable is (if on PATH)
```bash
%> whereis java
 /usr/bin/java 
```

## Bash Tutorial
## Bash Tutorial 
Command Ctrl & Alt Shortcuts
1. `Ctrl-C` (usually) sends the kill signal, which terminates a process abruptly. 
2. `Ctrl-Z` sends the stop signal, which stops process execution immediately, without terminating. Use “fg” or “bg” after that to restart the process of send it to the background. Ctrl-Y is an interesting variant, which stops process execution only when the process tries to read user input from the console. 
3. `Ctrl-S` is the scroll lock: when you have too much output scrolling quickly, you can use Ctrl-S to stop process output. You can then use Shift-PageUp/PageDown to scroll up and down and read it. `Ctrl-Q` resumes. Technically speaking, Ctrl-S and Ctrl-Q send the XON/XOFF terminal commands, that may be ignored in some cases. The Bash shell translates `Ctrl-S` to "search", so it depends on where you are working. 
4. `Ctrl-L` clears the screen and positions the prompt at the top left corner. Use this if your screen has become garbled. 
5. `Ctrl-A` and Ctrl-E take you to the beginning and the end of the line, respectively. Home and End also work, but not always. 
6. `Ctrl-D` deletes the character under the cursor. 
7. `Alt-F` and Alt-B take you to the next or previous word, very useful if you're typing a long sequence of commands or a command with many arguments. 
8. `[Tab]` is probably the most useful key when using the shell. Tab will do filename completion, but also hostname completion, variable name completion and other useful things. 
