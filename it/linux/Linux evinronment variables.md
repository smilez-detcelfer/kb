
```bash
var1=var_value #create local variable
```

```bash
export var1 # add variable to environment
export var2=var_value2 # declare variable and add to environment 
```

```bash
env #show all variables in environment
set | less # show variables and declared functions in environment
unset <variable> # delete variable from environment
```

add variable for **all users**:  `/etc/profile`
```bash
sudo nano /etc/profile
	#in file
	export variable_name=variable_value
```
add variable for **user** `/home/user/.profile`
```bash
sudo nano /home/user/.profile #or .bash_profile
	#in file
	export variable_name=variable_value
```

usefull variables:
**HOME** - set user home dierctory
**PATH** - set directory list for bin searching when it called
**PID** - process id
**PPID** - parent process id
**LANG** and other locale variables see in [[linux locale and encoding]]