Документация на компонент
------

https://wiki.yandex-team.ru/delivery/development/apps/item-reference-information-storage/

Настройка Idea и запуск проверок code style
------

Выполняется в соответствии с https://clubs.at.yandex-team.ru/arcadia/13516

Локальный запуск
------

Запустить dependency-stubs
```
 docker-compose up
```

Скопировать application-local.properties.dist в
```
 application-local.properties
```

Запустить из IDE со следующими аргументы VM
```
-Denvironment=local
-Dlog.dir=logs
-Dconfigs.path=<локальный путь до properties.d>
```
