# passport-libs-checker

Debian-пакет: [yandex-passport-libs-checker](https://c.yandex-team.ru/packages/yandex-passport-libs-checker)

Программа для проверки файлов библиотек `geobse`, `ipreg` и `uatraits`.

Если проходят тесты над файлами, то они копируются в другое место на файловой системе, где уже их ожидает какой либо сервис.

## Сервисы, пользующиеся passport-libs-checker
 * blackbox
 * passport
 * oauth
 
## Как устроено
Проверки выполнены в виде юнит-тестов, которые запускаются по крону, смотри `library_tests`.

В том числе тесты запускаются и по команде `ya make -t`, файлы геобазы и т.п. приезжают из sandbox-ресурсов, смотри `tests`.

## Конфигурация
Конфигурационный файл находится по пути `/etc/yandex/passport_libs_checker.json` и он _не_ приезжает с пакетом.

Формат:
```json
{
  "target_libs": [
    "libgeobase",
    "libipreg",
    "uatraits"
  ]
}
```

Список `target_libs` можно сокращать, убрав ненужное.
