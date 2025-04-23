hidereferer
===========

[Yandex Hidereferer](https://wiki.yandex-team.ru/intranet/hidereferer/)

## New release
Собрать новую версию и выкатить в тестинг
```
make release v=<new_version>
```

## Build
Собрать образ и запушить его в реестр:
```
make package v=<custom_version>
```

## Run
Запуск контейнера локально:
```
docker run -it -d registry.yandex.net/tools/hidereferer
```

## Shell
Запустить shell с ipython в контейнере
```
hshell
```

## Known issues
* issue: on urls longer than approx. 750 chars uwsgi can crash 'cause of default buffer limit of 4096 bytes
  solution: pass to uwsgi config option "--buffer-size 8192" on init
