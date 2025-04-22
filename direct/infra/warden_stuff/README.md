# warden\_stuff
Это всякие скрипты для работы с Warden по API. Чтобы остались на память.

## Токен
Токен можно получить тут: https://nda.ya.ru/t/TCgjin6A3Zcxi5

## Сборка и запуск
```sh
ya make && WARDEN_OAUTH=`cat ~/tokens/warden` ./warden_stuff
```

## Написание кода
Удобно сделать проект в VSCode `ya ide vscode-py ~/repo/arcadia/direct/infra/warden_stuff ~/repo/arcadia/search/mon/warden/proto/structures`,
запускать после пересборки из консоли редактора `WARDEN_OAUTH=`cat ~/tokens/warden` ./warden_stuff`.  
_С отладкой пока есть какие-то проблемы, не подтягиваются нужные импорты_