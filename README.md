# Homework lesson 2

* Add sata5 to Vagrantfile
```
:sata5 => {                        
    :dfile => './sata5.vdi', # Путь, по которому будет создан файл диска                        
    :size => 250, # Размер диска в мегабайтах      
    :port => 5 # Номер порта на который будет зацеплен диск
    },
```

* Run `vagrant up` command => no error messages 
* `vagrant ssh` => `[vagrant@otuslinux ~]`

Result 
* [Как начать Git](git_quick_start.md)
* [Как начать Vagrant](vagrant_quick_start.md)

## otus-linux

