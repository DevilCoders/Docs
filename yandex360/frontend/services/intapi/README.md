# intapi (ex. APIv3)
Новый клёвый API

## [Приложение в Deploy](https://yd.yandex-team.ru/projects/mail_intapi)

### Окружения
* [Production](https://yd.yandex-team.ru/stages/mail_intapi_production). [Corp](https://yd.yandex-team.ru/stages/mail_intapi_corp). Доступ в эти окружения ограничен.
  * [документация](https://intapi.mail.yandex.net/docs/)
  * [/ping](https://intapi.mail.yandex.net/ping)
* [QA](https://yd.yandex-team.ru/stages/mail_intapi_qa). [Corp-QA](https://yd.yandex-team.ru/stages/mail_intapi_corp-qa). В эти окружения пакеты ставятся вручную перед выкаткой в прод.
  * [документация](https://intapi-qa.mail.yandex.net/docs/)
  * [/ping](https://intapi-qa.mail.yandex.net/ping)
* [Alpha](https://yd.yandex-team.ru/stages/mail_intapi_alpha). [Corp-Alpha](https://yd.yandex-team.ru/stages/mail_intapi_corp-alpha). В эти окружения автоматически ставится новый собранный пакет.
  * [документация](https://intapi-alpha.mail.yandex.net/docs/)
  * [/ping](https://intapi-alpha.mail.yandex.net/ping)


## Cборка
```sh
make
```
Устанавливает зависимости и компилирует конфиги.

## Запуск dev-версии
```sh
make start
```
Выполняет сборку и запускает dev-сервер.

## Сборка Docker-образа
:exclamation: **Важно**: Пакеты собираются только из веток с названием вида
`rc-<имя-релиза>`. Например `rc-ping`, `rc-v2` и т.п.

:exclamation: **Важно**: Тег для образа создаётся автоматически по дате,
имени ветки и номеру билда. Например `v190313.ping.13`.

При сборке первого пакета в ветке нужно обязательно указать версию и тикет в Стартреке.
```sh
make package MAILAPI-123 1.2.3
# или
npm run package major MAILAPI-123
# или
npm run package minor MAILAPI-123
# или
npm run package patch MAILAPI-123
```

Эти команды создают и пушат коммит который запустит сборку Docker-образа в Trendbox.

## Структура

### Зависимости
  * `dependencies` — модули для работы приложения в проде;
  * `devDependencies` — модули необходимые для сборки и тестирования пакета;
  * `optionalDependencies` — модули для разработки (`nodemon`, `duffman` и т.п.).

### Приложение
Express-приложение.

  * `app` — приложение;
  * `middlewares` — глобальные миддлвари, (создание конфига, ядра и т.п.);
  * `lib` — расширение классов Duffman-а;
  * *TODO*

### Настройки (`configs/`)
*TODO*

### Роутер (`routers/`)
Настройка роутинга. При установке пакета создаётся симлинк в папке `/etc/duffman/init.d/`.
