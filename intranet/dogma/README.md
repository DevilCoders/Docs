# DOGMA

**Dogma** - это интерфейс доступа к репозиториям компании

## Полезные ссылки
* [Wiki страница](https://beta.wiki.yandex-team.ru/IntranetPoisk/Projects/codesearch-infra/dev)
* [Стартрек](https://st.yandex-team.ru/DOGMA)
* [Планер](https://planner.yandex-team.ru/services/762)
* [Github](https://github.yandex-team.ru/tools/dogma)

## Требования
Для запуска команд Makefile и команд вида releaser(https://github.yandex-team.ru/tools/releaser) ...нужно установить
утилиту `releaser` версии `>=0.14`.
Запускать эти команды нужно из корневой директории проекта.

## Общая информация
Используемые параметры команд make`:
* `-i` - `(production | testing)` окружение куда осуществляется выкладка

##Выкладка новой версии

1. Выкладываем тестинг

`make release i=testing`

2. Выкладываем продакшен

`make deploy i=production`

## Запуск тестов
```bash
fab test
```
