## Как отлаживать linux из под macOS

* Установить [Vagrant](https://www.vagrantup.com/downloads.html)
* Установить [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

Поправить плейбук `playbooks/dev-local.yml`
```
...
- hosts: ubuntu16
  connection: ssh
...
```

Находясь в папке ansible запустить vagrant
```
vagrant up
```

Запуск ansible
```
vagrant provision
```

Если нужно подключиться к машинке по ssh
```
vagrant ssh
```

Остановка машинки
```
vagrant halt
```
