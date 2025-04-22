# Настроить executer

Основная страница: <https://wiki.yandex-team.ru/executer/>  
Короткая Директовая теория: [{#T}](../things/executer.md)  
Раньше эта инструкция жила на [wiki](https://wiki.yandex-team.ru/jeri/app-duty/executer/).

Установлен на ppcback-ах.

Перед использованием прописать в `~/.executer.conf`:  
```
default_user = <доменный логин>
# раньше тут была настройка "sudo = 1", но
# 1) этот конфиг не у всех везде может быть, и тогда лучше в инструкциях явно указывать команды с sudo (по умолчанию в executer sudo = 0)
# 2) с sudo = 1 введённая команда вида "cmd1; cmd2" выполнится как "sudo cmd1; cmd2", что может привести к неожиданностям
sudo = 0
project_filter = direct
rtc_disabled = 1
qloud_disabled = 1
```
