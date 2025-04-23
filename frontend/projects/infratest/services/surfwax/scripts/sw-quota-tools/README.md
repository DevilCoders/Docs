# sw-quota-tools
Данный набор скриптов позволяет создавать и удалять квоту в [surfwax](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax), а также управлять браузерами существующих квот.
Для запуска скриптов необходимы токены от [YDB](https://yql.yandex-team.ru/oauth) и [SANDBOX](https://sandbox.yandex-team.ru/oauth). Токены можно положить в файл `.env` или указать в командной строке.

## Использование
### Создание квоты
Для создания квоты используется интерактивный скрипт `create-quota`.
```
YDB_TOKEN=<token> SANDBOX_AUTH_TOKEN=<token> ./bin/sw-quota-tools create-quota
```

Данный скрипт не обладает транзакционностью. Это значит, что если в середине создания квоты что-то пошло не так, то часть действий были записаны в базу. Если такая ситуация произошла, есть отдельный скрипт для удаления квоты.

### Удаление квоты
```
YDB_TOKEN=<token> SANDBOX_AUTH_TOKEN=<token> ./bin/sw-quota-tools delete-quota
```

### Добавление браузеров в квоту
```
YDB_TOKEN=<token> SANDBOX_AUTH_TOKEN=<token> ./bin/sw-quota-tools add-browsers
```

### Удаление браузеров из квоты
```
YDB_TOKEN=<token> SANDBOX_AUTH_TOKEN=<token> ./bin/sw-quota-tools delete-browsers
```
