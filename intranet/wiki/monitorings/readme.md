# Мониторинги
Для генерации алертов используется утилита [Monitorado](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/monitorado). Для того, чтобы менять алерты нужно:

1. Установить пакет monitorado `npm i -g @yandex-int/monitorado --registry=https://npm.yandex-team.ru` .
   `-g` означает "глобально", вам наверняка понадобится `sudo`.
   Получить токен [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=171fcece39a04fd0a6b8b74950336008)
   и положить его в переменную окружения `MONITORADO_OAUTH_TOKEN` (например, в `~/.zshrc`).
1. Внести необходимые изменения в файлы конфигурации.
1. Проверить, что получится в результате командой `monitorado diff -v -c monitorings/wiki-back.monitorado.yml`
1. Запустить перегенерацию алертов для каждого измененного файла.
   Пример: `monitorado exec -c monitorings/paste.monitorado.yml`.
