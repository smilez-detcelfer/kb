listening ports:

```bash
echo <arg> # print arg to console
cat <file> # print file to console
ls -a; cat <file> # ; split commands
ls -p | grep -v / #shows only files
cp file1 /path/filename  # copy file
mv file1 file2 #move or rename file

head -n 5 file # shows  first 5 strings of file
tail -n 5 file # shows last 5 strings of file
tail -f show last strings and update
less # scroll long file (Pg Up/Down)

dd if=/dev/sdx of=/path/to/backup.img
```


```bash
find /path -name ".*" # find by name
find . -size +1G # find by size
find /path -type f
find 
```
[find cheatsheet](https://devhints.io/find)



`ps -u # user processes`
`netstat -anpt | grep LISTEN`


