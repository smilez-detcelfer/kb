
Every terminal session presents in system as file
```bash
/dev/ttyx # real terminal devices
/dev/pts/x # pseudo terminal devices
```

*LOGIN* shell configuration files:
```bash
/etc/profile # fistly checking global configuration
/etc/profile.d/*sh # then apply scripts from dir
# apply home folder file configuration
~/.bash_profile
~/.bash_login
~/.profile
#and finally 
~/.bashrc
```
*NO-LOGIN* shell configuration files
```bash
#fistly check
/etc/bash.bashrc
/etc/bashrc
#and finally 
~/.bashrc
```
*check if it's login or no-login shell*:
```bash
echo $0 # '-bash' = login; 'bash' = no-login
```


**/etc/passwd** shows which shell used by defalut for user
