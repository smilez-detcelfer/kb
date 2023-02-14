## Config files and dirs

**main** config file */etc/crontab*

*pre-confiigured directories* for cron jobs:
	/etc/cron.*hourly*
	/etc/cron.*daily*
	/etc/cron.*weekly*
	/etc/cron.*monthly*

## /etc/crontab format
![[Pasted image 20230202152653.png]]

user can create cron jobs in /var/spool/cron/crontabs

## CRONTAB

```bash
crontab -e # edit user cron file
crontab -l # show user cron file
crontab -r # remove user cron file
crontab -u user -e/l/r # work with specific user file 
```
crontab generate file with **user cron jobs** in */var/spool/cron/crontabs/<user_name>*

## CRONTAB permitions

*/etc/cron.deny* # user *black list* 
*/etc/cron.allow* # user *white list* with **higher priority** (if exists, access allowed only to users in file)
```bash
# file format
user1
user2
user3
# crontab -u user -l # check user for black list
```