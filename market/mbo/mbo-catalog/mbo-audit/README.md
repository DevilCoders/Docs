# mbo-audit
Сервис занимающийся отображением, сбором и обработкой журналируемых данных действий пользователей на mbo.

## Запуск на aida
Для запуска на аиде используйте скрипт из scripts/dev/run-mbo-audit.py

## Локальный запуск интеграционных тестов
Для запуска интеграционных тестов используется команда:
```bash
ya make -ttt
```
Для запуска тестов необходима предварительная настройка etcd, описание лежит в корневом [README.md](../README.md#локальный-запуск-автотестов-через-ya-make)

### Дашборды

#### Прод
[NGINX](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-audit-production)

#### Тестинг
[NGINX](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-audit-testing)
