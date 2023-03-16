# Command Reference

## Screen command
Create a screen session:
```
screen -S myscreensession
```

Find running screen sessions:
```
$ screen -ls
There is a screen on:
	7115.myscreensession	(12/02/22 02:30:35)	(Detached)
1 Socket in /run/screen/S-iser.
```

Reattach to screen session:
```
screen -r myscreensession
```
OR, if there are multiple sessions with same name then use the id:
```
screen -r 7115.myscreensession
```

To kill that session and all its processes:
```
screen -XS 7115.myscreensession quit
```

Create a screen session with a log file and string of commands all in one (similar to how nohup is used but you can re-attach to the session):
```
screen -L -Logfile ${OUTPUT_DIR}/runRepoStats.log -dmS runRepoStats bash -c "./script.sh; echo \"Script is done running\""
```
