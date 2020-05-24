# Homework lesson 2

* Clone otus-linux into working directory
* Add sata5 to Vagrantfile
```
:sata5 => {                        
    :dfile => './sata5.vdi', # Путь, по которому будет создан файл диска                        
    :size => 250, # Размер диска в мегабайтах      
    :port => 5 # Номер порта на который будет зацеплен диск
    },
```

* Run `vagrant up` command => no error messages ==> VM up and running 
* ssh to vagrant `vagrant ssh` => `[vagrant@otuslinux ~]`
* check disk devices list and their info 
with command `lshw -short | grep disk`
```
[vagrant@otuslinux ~]$ sudo lshw -short | grep disk
/0/100/1.1/0.0.0    /dev/sda   disk        42GB VBOX HARDDISK
/0/100/d/0          /dev/sdb   disk        262MB VBOX HARDDISK
/0/100/d/1          /dev/sdc   disk        262MB VBOX HARDDISK
/0/100/d/2          /dev/sdd   disk        262MB VBOX HARDDISK
/0/100/d/3          /dev/sde   disk        262MB VBOX HARDDISK
/0/100/d/0.0.0      /dev/sdf   disk        262MB VBOX HARDDISK
```
* Execute superblocks zero-ing with `mdadm --zero-superblock --force /dev/sd{b,c,d,e,f}`
* Create RAID6 
```
[vagrant@otuslinux ~]$ sudo mdadm --create --verbose /dev/md0 -l 6 -n 5 /dev/sd{b,c,d,e,f}
mdadm: layout defaults to left-symmetric
mdadm: layout defaults to left-symmetric
mdadm: chunk size defaults to 512K
mdadm: size set to 253952K
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
```
* chech if the RAID6 mounted and is ok
```
[vagrant@otuslinux ~]$ cat /proc/mdstat
Personalities : [raid6] [raid5] [raid4] 
md0 : active raid6 sdf[4] sde[3] sdd[2] sdc[1] sdb[0]
      761856 blocks super 1.2 level 6, 512k chunk, algorithm 2 [5/5] [UUUUU]
      
unused devices: <none>
```
```
[vagrant@otuslinux ~]$ mdadm -D /dev/md0
mdadm: must be super-user to perform this action
[vagrant@otuslinux ~]$ sudo mdadm -D /dev/md0
/dev/md0:
           Version : 1.2
     Creation Time : Sun May 24 17:09:40 2020
        Raid Level : raid6
        Array Size : 761856 (744.00 MiB 780.14 MB)
     Used Dev Size : 253952 (248.00 MiB 260.05 MB)
      Raid Devices : 5
     Total Devices : 5
       Persistence : Superblock is persistent

       Update Time : Sun May 24 17:09:44 2020
             State : clean 
    Active Devices : 5
   Working Devices : 5
    Failed Devices : 0
     Spare Devices : 0

            Layout : left-symmetric
        Chunk Size : 512K

Consistency Policy : resync

              Name : otuslinux:0  (local to host otuslinux)
              UUID : 69c21eeb:d82eb529:2295cdad:237c74f4
            Events : 17

    Number   Major   Minor   RaidDevice State
       0       8       16        0      active sync   /dev/sdb
       1       8       32        1      active sync   /dev/sdc
       2       8       48        2      active sync   /dev/sdd
       3       8       64        3      active sync   /dev/sde
       4       8       80        4      active sync   /dev/sdf
```
* ## creating mdadm.conf
* check the information is correct 
```[vagrant@otuslinux ~]$ sudo mdadm --detail --scan --verbose
ARRAY /dev/md0 level=raid6 num-devices=5 metadata=1.2 name=otuslinux:0 UUID=69c21eeb:d82eb529:2295cdad:237c74f4
   devices=/dev/sdb,/dev/sdc,/dev/sdd,/dev/sde,/dev/sdf```
   

