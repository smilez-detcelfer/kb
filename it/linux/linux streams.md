**stdout**
```bash
command output > file # stdout to file 'w'
#or 
command output 1> file # stdout to file 'w'

command output >> file # stdout to file '+w' 
#or
command output 1>> file # stdout to file '+w' 
```

**stderr**
```bash
command output 2> file # stderr to file 'w'
command output 2>> file # stderr to file '+w'
```

**stdout** + **stderr**
```bash
command output &> file # stdout and stderr to file 'w'
command output &>> file # stdout and stderr to file '+w'
command output 1>> file 2> /dev/null # stdout to file '+w', stderr to trash
```

**redirect** stdx to stdy
```bash
2>&1 # stderr redirected to stdout
1>&2 # stdout redirected to stderr

ls /dir >> file 2>&1 # stdout and stderr redirected to file '+w'
```

**TEE** & **XARGS**
```bash
ls /dir | tee file # send output to file and console parallel

ls /dir | xargs cat # send output line by line as command arguments
ls /dir | xargs cat | grep word # find 'word' in all files from dir 
```

