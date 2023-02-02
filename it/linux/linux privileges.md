## file owner attributes
* *Owner 
* *Owner Group*
* *Others*
```bash
chown user file # change owner user
chown :group # change owner group
chown user:group # change owner and owner group
```
**Only root can change file owner**


## file privileges
* *Read* - 4
* *Write* - 2
* *Execute* -1
```bash
chmod +x filename # add execute privileges for all users
chmod 700 filename # set all privs to owner, other users have no privs
chmod u=rwx # add all privs to owner
# chmod XXX: 1st - owner; 2nd - owner group; 3d - other users 
```
* Only root and owner can change file privileges
* root can read and write to file even if he has no such privileges

### file types
**-** - Regular file
**d** Directory
**l** - Link 
**b** - Block file
**p** - Named pipe file
**c** - Character special file
**s** - Socket file

<file_type><owner_privs><group_privs><other_privs>
![[Pasted image 20230130184318.png]]

## directory privileges

**Read**:
* read *list* of objects in directory

**Write**:
* allow add or remove file from directory
* works *only with execute*

**Execute**: 
* allow using commands in directory
* allow read/write contents of existing files and directories
* allow get in subdirectories (and do anything if inner directory and files allow that)

## SUID | GUID | stiky bit

```bash
chmod u+s file # add suid bit to file (always to owner)
chmod g+s # add sgid bit to file (always to group)
chmod +t # add sticky bit to folder (always to other)
```

![[Pasted image 20230130184526.png]]
* **SUID** execute file with owner user id
* **GUID** execute file with as owner group user id
* **GUID** (on folder) file created in directory have the same owner group
* **sticky** (on folder) delete files from directory can only:
	* root
	* directory owner
	* file owner




**umask** - #utility define default file access privileges for user
default is *022* for debian
`umask 000` define new files with access privileges *666* (666 **is max for regular file**, 777 is max for directories)
`umask 777` define new files with access privileges *000*

* this properties **only for session***
* for permanent configuration add `umask 022` in *~/.profile*
