
YUM - #utility  RPM package manager in Centos, RHEL


```bash
yum update # find and install all updates for packages
```

```bash
yum search # find packages in available repositories
```

```bash
yum install <package> # install package
```

```bash
yum remove <package> # remove package with dependencies
```

APT #utility debian package manager

/etc/apt/sources.list - repository list file
```bash
apt-add-repository -r 'deb http://repo-adress.com os_type main contrib non-free'
```

```bash 
apt update # download packege list from repositories to cache
```

```bash
apt upgrade # update all installed packages
```

```bash
apt search <text> # search for packages with text in name or decription
```

```bash
apt install <package> # install deb package from repository
```

```bash
apt purge <package> # remove package with dependencies
```

```bash
apt autoremove # remove unused packages
```
