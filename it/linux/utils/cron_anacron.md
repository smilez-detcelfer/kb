## Config files and dirs

**main** config file */etc/anacrontab*
```bash
#record in anacrontab
<periond_in_days> <delay_in_minutes> <job_identifier> <command>

1 5 anacron.backup backup.sh arg1 arg2
# start backup.sh every day, with 5 minutes delay
# after start make record in /var/spool/anacron/anacron.backup

# !!! when new record has added, new file with job identifier name will 
# 
```
new record in this ^^^  file will create new file:
*/var/spool/anacron/cron.<job_identifier>*
```bash
/var/spool/anacron/cron.daily
/var/spool/anacron/cron.weekly
/var/spool/anacron/cron.monthly
#/var/spool/anacron/anacron.backup
```

anacron default records replace default cron folder jobs
