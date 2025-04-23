## aptly

Сервис для поддержания актуальности версий внешних (не собираемых в Вертикалях) пакетов.

docs: https://docs.yandex-team.ru/classifieds-ops-internal/iaas/aptly

### Запуск тестов

Для тестов нужны секреты из [секрета](https://yav.yandex-team.ru/secret/sec-01g63hzvghswkh9qckg7c61zqe/explore/versions) в файле `local.env` в корне проекта кроме `GPG_SECRET_KEY`.

Запуск:
```make test```
