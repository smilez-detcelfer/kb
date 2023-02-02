inode


*hard link* links to **file inode** (descriptor)
*hard link* can be created **only fo file in the same file system**
*hard link* can't link to directory

*soft link* links on **file name**
*soft link* can be created to any mounted fs
*soft link* can link to directory
```bash
ln filename linkname # creates hard link
ln -s filename linkname # creates soft link
```

if original file **renamed**:
* *hard lin*k still work
* *soft link* is broken untill file with the same name is created