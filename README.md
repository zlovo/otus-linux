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
with command `sudo fdisk -l`


Result 
* [Как начать Git](git_quick_start.md)
* [Как начать Vagrant](vagrant_quick_start.md)

## otus-linux

