# Metrics (https://metrics.yandex-team.ru)

## Запуск dev-сервера
- `yarn` для установки зависимостей
- `yarn dev:init` для инициализации необходимых для локального запуска файлов
- `yarn dev` для запуска локального dev-сервера

## Hermione тесты (<a href="https://wiki.yandex-team.ru/metrics/frontend/#novyehermionetesty">wiki</a>)
- `yarn hermione`  - прогоняет все тесты (ответы ручек читаются из кеша), сравнивает скриншоты
- `yarn hermione:update`  - перезаписывает скриншоты, существующие дампы не перезаписывются, но записываются дампы новых ручек
- `yarn hermione:update:dumps`  - перезаписывает и скриншоты, и дампы ручек

#### Доступные флаги
- Запуск без дев-сервера - `--hermione-no-server`  (Нужно будет запустить дев-сервер вручную - `yarn acceptance:init && yarn acceptance`)
- Запуск тестов по названию - `--hermione-grep "ComparePage should open 1 serpset"`
- Запуск тестов в конкретном браузере - `--hermione-browser "chrome"`

#### Отчёт по пройденным тестам
- `yarn hermione:gui`
