Задание: Обновление ядра системы 

Проверка доступа в интернет и работы dns

hello@hellovm:~$ ping ya.ru
PING ya.ru (77.88.55.242) 56(84) bytes of data.
64 bytes from ya.ru (77.88.55.242): icmp_seq=1 ttl=247 time=16.1 ms
64 bytes from ya.ru (77.88.55.242): icmp_seq=2 ttl=247 time=18.7 ms
^C
--- ya.ru ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1000ms
rtt min/avg/max/mdev = 16.122/17.413/18.705/1.291 ms

Получение доступа root-пользователя

hello@hellovm:~$ sudo -i 
[sudo] password for hello: 
root@hellovm:~# 

Проверка текущей версии ядра 
root@hellovm:~#  uname -r
5.15.0-133-generic

Создание директории kernel и переход в нее

root@hellovm:~# mkdir kernel && cd kernel 
root@hellovm:~/kernel# 

Скачивание пакетов на виртуальную машину

root@hellovm:~/kernel# wget https://kernel.ubuntu.com/mainline/v6.14-rc4/amd64/linux-headers-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb
--2025-02-28 23:50:53--  https://kernel.ubuntu.com/mainline/v6.14-rc4/amd64/linux-headers-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb
Resolving kernel.ubuntu.com (kernel.ubuntu.com)... 185.125.189.76, 185.125.189.74, 185.125.189.75
Connecting to kernel.ubuntu.com (kernel.ubuntu.com)|185.125.189.76|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3717780 (3.5M) [application/x-debian-package]
Saving to: ‘linux-headers-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb’

linux-headers-6.14. 100%[===================>]   3.54M  5.18MB/s    in 0.7s    

2025-02-28 23:50:54 (5.18 MB/s) - ‘linux-headers-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb’ saved [3717780/3717780]

root@hellovm:~/kernel# wget https://kernel.ubuntu.com/mainline/v6.14-rc4/amd64/linux-headers-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb
--2025-02-28 23:50:53--  https://kernel.ubuntu.com/mainline/v6.14-rc4/amd64/linux-headers-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb
Resolving kernel.ubuntu.com (kernel.ubuntu.com)... 185.125.189.76, 185.125.189.74, 185.125.189.75
Connecting to kernel.ubuntu.com (kernel.ubuntu.com)|185.125.189.76|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3717780 (3.5M) [application/x-debian-package]
Saving to: ‘linux-headers-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb’

linux-headers-6.14. 100%[===================>]   3.54M  5.18MB/s    in 0.7s    

2025-02-28 23:50:54 (5.18 MB/s) - ‘linux-headers-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb’ saved [3717780/3717780]

root@hellovm:~/kernel# wget https://kernel.ubuntu.com/mainline/v6.14-rc4/amd64/linux-headers-6.14.0-061400rc4_6.14.0-061400rc4.202502232206_all.deb
--2025-02-28 23:52:00--  https://kernel.ubuntu.com/mainline/v6.14-rc4/amd64/linux-headers-6.14.0-061400rc4_6.14.0-061400rc4.202502232206_all.deb
Resolving kernel.ubuntu.com (kernel.ubuntu.com)... 185.125.189.76, 185.125.189.74, 185.125.189.75
Connecting to kernel.ubuntu.com (kernel.ubuntu.com)|185.125.189.76|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 13972552 (13M) [application/x-debian-package]
Saving to: ‘linux-headers-6.14.0-061400rc4_6.14.0-061400rc4.202502232206_all.deb’

linux-headers-6.14.0-061400r 100%[===========================================>]  13.33M  7.07MB/s    in 1.9s    

2025-02-28 23:52:02 (7.07 MB/s) - ‘linux-headers-6.14.0-061400rc4_6.14.0-061400rc4.202502232206_all.deb’ saved [13972552/13972552]

root@hellovm:~/kernel# wget https://kernel.ubuntu.com/mainline/v6.14-rc4/amd64/linux-image-unsigned-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb
--2025-02-28 23:52:19--  https://kernel.ubuntu.com/mainline/v6.14-rc4/amd64/linux-image-unsigned-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb
Resolving kernel.ubuntu.com (kernel.ubuntu.com)... 185.125.189.74, 185.125.189.75, 185.125.189.76
Connecting to kernel.ubuntu.com (kernel.ubuntu.com)|185.125.189.74|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 15718592 (15M) [application/x-debian-package]
Saving to: ‘linux-image-unsigned-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb’

linux-image-unsigned-6.14.0- 100%[===========================================>]  14.99M  6.11MB/s    in 2.5s    

2025-02-28 23:52:22 (6.11 MB/s) - ‘linux-image-unsigned-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb’ saved [15718592/15718592]

root@hellovm:~/kernel# wget https://kernel.ubuntu.com/mainline/v6.14-rc4/amd64/linux-modules-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb
--2025-02-28 23:52:35--  https://kernel.ubuntu.com/mainline/v6.14-rc4/amd64/linux-modules-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb
Resolving kernel.ubuntu.com (kernel.ubuntu.com)... 185.125.189.74, 185.125.189.76, 185.125.189.75
Connecting to kernel.ubuntu.com (kernel.ubuntu.com)|185.125.189.74|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 188580032 (180M) [application/x-debian-package]
Saving to: ‘linux-modules-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb’

linux-modules-6.14.0-061400r 100%[===========================================>] 179.84M  9.16MB/s    in 21s     

2025-02-28 23:52:56 (8.66 MB/s) - ‘linux-modules-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb’ saved [188580032/188580032]

2025-02-28 23:52:56 (8.66 MB/s) - ‘linux-modules-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb’ saved [188580032/188580032]

Установка пакетов: 

root@hellovm:~/kernel# dpkg -i *.deb
Selecting previously unselected package linux-headers-6.14.0-061400rc4.
(Reading database ... 163212 files and directories currently installed.)
Preparing to unpack linux-headers-6.14.0-061400rc4_6.14.0-061400rc4.202502232206_all.deb ...
Unpacking linux-headers-6.14.0-061400rc4 (6.14.0-061400rc4.202502232206) ...
Selecting previously unselected package linux-headers-6.14.0-061400rc4-generic.
Preparing to unpack linux-headers-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb ...
Unpacking linux-headers-6.14.0-061400rc4-generic (6.14.0-061400rc4.202502232206) ...
Selecting previously unselected package linux-image-unsigned-6.14.0-061400rc4-generic.
Preparing to unpack linux-image-unsigned-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb ...
Unpacking linux-image-unsigned-6.14.0-061400rc4-generic (6.14.0-061400rc4.202502232206) ...
Selecting previously unselected package linux-modules-6.14.0-061400rc4-generic.
Preparing to unpack linux-modules-6.14.0-061400rc4-generic_6.14.0-061400rc4.202502232206_amd64.deb ...
Unpacking linux-modules-6.14.0-061400rc4-generic (6.14.0-061400rc4.202502232206) ...
Setting up linux-headers-6.14.0-061400rc4 (6.14.0-061400rc4.202502232206) ...
dpkg: dependency problems prevent configuration of linux-headers-6.14.0-061400rc4-generic:
 linux-headers-6.14.0-061400rc4-generic depends on libc6 (>= 2.38); however:
  Version of libc6:amd64 on system is 2.35-0ubuntu3.9.
 linux-headers-6.14.0-061400rc4-generic depends on libelf1t64 (>= 0.144); however:
  Package libelf1t64 is not installed.
 linux-headers-6.14.0-061400rc4-generic depends on libssl3t64 (>= 3.0.0); however:
  Package libssl3t64 is not installed.

dpkg: error processing package linux-headers-6.14.0-061400rc4-generic (--install):
 dependency problems - leaving unconfigured
Setting up linux-modules-6.14.0-061400rc4-generic (6.14.0-061400rc4.202502232206) ...
Setting up linux-image-unsigned-6.14.0-061400rc4-generic (6.14.0-061400rc4.202502232206) ...
I: /boot/vmlinuz is now a symlink to vmlinuz-6.14.0-061400rc4-generic
I: /boot/initrd.img is now a symlink to initrd.img-6.14.0-061400rc4-generic
Processing triggers for linux-image-unsigned-6.14.0-061400rc4-generic (6.14.0-061400rc4.202502232206) ...
/etc/kernel/postinst.d/initramfs-tools:
update-initramfs: Generating /boot/initrd.img-6.14.0-061400rc4-generic
/etc/kernel/postinst.d/vboxadd:
VirtualBox Guest Additions: Building the modules for kernel 
6.14.0-061400rc4-generic.

This system is currently not set up to build kernel modules.
Please install the gcc make perl packages from your distribution.
/etc/kernel/postinst.d/zz-update-grub:
Sourcing file `/etc/default/grub'
Sourcing file `/etc/default/grub.d/init-select.cfg'
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-6.14.0-061400rc4-generic
Found initrd image: /boot/initrd.img-6.14.0-061400rc4-generic
Found linux image: /boot/vmlinuz-5.15.0-133-generic
Found initrd image: /boot/initrd.img-5.15.0-133-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
Warning: os-prober will not be executed to detect other bootable partitions.
Systems on them will not be added to the GRUB boot configuration.
Check GRUB_DISABLE_OS_PROBER documentation entry.
done
Errors were encountered while processing:
 linux-headers-6.14.0-061400rc4-generic

Проверка, ядра в /boot.

[db@server ~]$ ls -al /boot 

Обновление конфигурации загрузчика:
 
root@hellovm:~/kernel# update-grub
Sourcing file `/etc/default/grub'
Sourcing file `/etc/default/grub.d/init-select.cfg'
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-6.14.0-061400rc4-generic
Found initrd image: /boot/initrd.img-6.14.0-061400rc4-generic
Found linux image: /boot/vmlinuz-5.15.0-133-generic
Found initrd image: /boot/initrd.img-5.15.0-133-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
Warning: os-prober will not be executed to detect other bootable partitions.
Systems on them will not be added to the GRUB boot configuration.
Check GRUB_DISABLE_OS_PROBER documentation entry.
done

Выбор загрузки нового ядра по-умолчанию:

root@hellovm:~/kernel# grub-set-default 0

Перезагрузка

root@hellovm:~/kernel# reboot now

Проверка версии ядра:

hello@hellovm:~$ uname -r
6.14.0-061400rc4-generic
