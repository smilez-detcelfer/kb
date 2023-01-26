
Session processes
```bash
sh long_working_process.sh & # make process work in background
jobs # shows background processes (only for current session)
fg %job_id # show process in console Ctrl+Z to suspend
bg %job_id # return process in background from suspend
```
**such processes will be killed at the end of session**

Real background procesess
```bash
nohup sh long_working_process.sh &
```


```bash
ps aux # show all processes from all users
ps alx # also shows process priority
pstree #shows all processes as tree
kill pid # kill process
pgrep -l -u smilez # shows all smilez's processes
top/htop #process list interface
uptime # show uptime
free # show free RAM 



renice
```

```bash
nice -n -20 sh script.sh & # start process with fixed priority in background
```