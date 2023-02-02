
**Session processes**
```bash
sh long_working_process.sh & # make process work in background
jobs # shows background processes (only for current session)
fg %job_id # show process in console Ctrl+Z to suspend
bg %job_id # return process in background from suspend
```
*such processes will be killed at the end of session*

**Real background procesess**
```bash
nohup sh long_working_process.sh &
```

**Show processes**
```bash
ps aux # show all processes from all users
ps xao pid,ppid,user,nice,comm # show all pids, ppids, user, priority, command
pstree #shows all processes as tree
pgrep -l -u smilez # shows all smilez's processes
top / htop #process list interface
```

**Kill processes**
```bash
kill pid # kill process (normal mode)
kill -9 pid # kill process (rude)
killall <command_name> # kill all processes with the same name
```

**Priority processes**
Process priority from `19 (lowest)` to `-20 (highest)`
```bash
nice -n <priority_level> command.sh #set priority while starting proc
renice <priority_level> -p <pid> # change proc priority on the fly
renice <priority_level> -u <user> # change user process priority
```
