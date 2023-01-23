ставится на esxi и proxmox из-за необходимости эмуляции интерфейса e1000, vmxnet3
анализатор (сетевого трафика)
хранилище
агент контроля подключений
веб-сервер

![[Pasted image 20221003101130.png]]

Centos7
eng + rus
Разделы:
device type: standart partition
FS: ext4 везде кроме swap
10gb    /
10gb    /tmp
10gb    /var
512mb /boot (всегда 512mb)
4gb      /swap (всегда 4gb)
20gb    /SQL (65%)
15gb    /archive


