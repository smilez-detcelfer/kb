
### User information in file */etc/passwd* 
```bash
#file format
<username>:<password>:<UID>:<GID>:<user_info>:</user/home/dir>:<default_shell>
```

### Group information if file */etc/group*
```bash
# file format:
<groupname>:<password>:<GID>:<user1,user2,user3>
```

### User and group hashed pasword file */etc/shadow*
```bash
<login>:<hashed_password>:<last_change>:<other_useless_shit>
```

### user and group management utils:
```bash
adduser username # add user username
passwd username # set password to username
# to /home/username will be copied files from /etc/skel
# you can add or remove items of you want
deluser username # delete user

addgroup groupname # create group
delgroup groupname # delete group

usermod -g groupname username #set primary group to user
usermod -G groupname username #add user in group 'groupname'

id # shows  RUID EUID of user

```



![[Pasted image 20230130181847.png]]
![[Pasted image 20230130182118.png]]



## SU
```bash
su -l user # change user to 
su - user #change user to
sudo -u user command # run command as user
```