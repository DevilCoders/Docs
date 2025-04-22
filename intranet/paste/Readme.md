# Разработка
https://wiki.yandex-team.ru/wiki/dev/pycharm/

# Запуск тестов в pycharm
```
make rebuild-testrunner
make testenv &
```
В качестве интерпретатора выбираем ./tests/python3
Тесты подгружают переменные окружения из ./tests/dotenv

# Сборка
```
make bump-patch
make bump-minor
make bump-major
```
Увеличит версию и раскатит на тестинг

# Деплой
Мониторинги: https://yasm.yandex-team.ru/panel/neofelis.paste

```
make deploy-prod v=1.23.45
```

# Мониторинги
Для генерации алертов используется утилита [Monitorado](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/monitorado). Для того, чтобы менять алерты нужно:

1. Установить пакет monitorado `npm i -g @yandex-int/monitorado --registry=https://npm.yandex-team.ru` .
   `-g` означает "глобально", вам наверняка понадобится `sudo`.
   Получить токен [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=171fcece39a04fd0a6b8b74950336008)
   и положить его в переменную окружения `MONITORADO_OAUTH_TOKEN` (например, в `~/.zshrc`).
1. Внести необходимые изменения в файлы конфигурации.
1. Проверить, что получится в результате командой `monitorado diff -v -c monitorings/paste.monitorado.yml`
1. Запустить перегенерацию алертов для каждого измененного файла.
   Пример: `monitorado exec -c monitorings/paste.monitorado.yml`.


### Сорцы утилиты ya paste

https://a.yandex-team.ru/arc_vcs/devtools/ya/handlers/paste/
