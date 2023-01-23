
sda1-4 - primary partitions
sda5-n - logical partitions

**fdisk** - #utility for disk partition configuration
```bash
fdisk -l # show partitions
```

```bash
fdisk /dev/sdxn # open partition menu
```



**mkfs** - #utility  for formating file system on disk partitions 

```bash
mkfs.<file_system_type> /dev/sdxn # formatin partition
```

```bash
mkfs.<file_system_type> /dev/vg_name/lv_name # formating logical volume in LVM
```


**mount** & **umount** - #utility which mounts partitions, shows mounted disk partitions

```bash
mount /dev/sdxn /mount/path # mount partition to directory
```

```bash
umount /mount/path # unmount partition
```

/etc/fstab - file system mounting #config_file

blkid # shows partition UUID

swapon & swapoff # commands for swap configuration
mkswp - # #utility  swap creation 

### LVM
![[Pasted image 20230123232745.png]]
pvdisplay #utility show physical volumes
pvcreate /dev/sdxn #utility create physical volume

vgdisplay #utility  show volume groups
vgcreate /dev/sdx1 /dev/sdx2 #utility  create volume group

lvdisplay #utility  show logical volumes
lvcreate  -n <lv_name> -L <lv_size> #utility  create logical volume
lvresize -L 4G vg_name/lv_name  #utility change logical volume size


### GRUB2 ###

/etc/default/grub # grub config file
/etc/grub.d # directory with scripts