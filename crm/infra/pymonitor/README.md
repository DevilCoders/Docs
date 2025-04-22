# pymonitor

Python 3.6

# Build

ya package --docker --docker-push --target-platform linux  --docker-repository crm package.json

# Отладка

Собрать проект 
```
ya make
```

Локально появится исполняемый файл ```crm-pymonitor```
Его запустить ./crm-pymonitor
Если вылезет ошибка 
```
    self.socket.bind(self.server_address)
PermissionError: [Errno 13] Permission denied
```
то можно 
- изменить порт, например 8081
- возможно 80 порт занят и надо завершить того кто слушает
- возможно надо гранты дать на запуск