date - shows current date and time
tzselect - shows timezone name
timedatectl - time and date configuration utility 

```bash
timedatectl set-time <time>
timedatectl set-timezone <zone from tzselect>
timedatectl set-ntp true\false # enable \ disable net time sync
```