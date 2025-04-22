# test-changes-collector

Инструмент для сбора статистики по частоте изменений тестов в проекте. Статистика хранится в кластере [infra](https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-clickhouse/cluster/mdb93hb3hj9nthd6mme3) в *Clickhouse* базе данных [stats](https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-clickhouse/cluster/mdb93hb3hj9nthd6mme3?section=databases) в таблице `test_changes` (логин и пароль для подключения находятся в [секретнице](https://yav.yandex-team.ru/secret/sec-01dn2bvx4303h4h8azp3evfzh7/explore/versions)).

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Принцип работы инструмента](#%D0%BF%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B-%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0)
- [Данные в таблице](#%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%B5-%D0%B2-%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B5)
  - [Описание событий](#%D0%BE%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D0%B5-%D1%81%D0%BE%D0%B1%D1%8B%D1%82%D0%B8%D0%B9)
- [Установка](#%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0)
- [Использование](#%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)
  - [Опции и аргументы](#%D0%BE%D0%BF%D1%86%D0%B8%D0%B8-%D0%B8-%D0%B0%D1%80%D0%B3%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B)
  - [Переменные среды окружения](#%D0%BF%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5-%D1%81%D1%80%D0%B5%D0%B4%D1%8B-%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F)
- [Задачи в *Sandbox*](#%D0%B7%D0%B0%D0%B4%D0%B0%D1%87%D0%B8-%D0%B2-sandbox)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Принцип работы инструмента

- получаем список произошедших с тестами событий:
  - определяем добавленные/удалённые/модифицированные тесты на основе переданных на вход изменённых файлов:
    - получаем список тестов `A` из изменённых файлов
    - получаем список тестов `B` из таблицы базы данных, который является предыдущей записью про тесты из списка `A`
    - на основе списков `A` и `B` формируем список тестов, которые были добавлены/удалены/модифицированы (тест считается модифицированным, если непосредственно изменился его коллбек)
  - доопределяем список событий по измененным дампам (добавление/удаление/изменение `N` дампов для теста – это `N` событий в таблице изменений)
  - доопределяем список событий по изменённым скриншотам (добавление/удаление/изменение `N` скриншотов для теста – это `N` событий в таблице изменений)
  - доопределяем список событий данными из *Testcop:*
    - получаем список вручную расскипанных тестов с момента последней записи в базу (чтобы отлавливать тесты, которые скипаются по какой-то задаче, а потом просто расскипываются вручную без исправления кода сервиса или кода теста)
    - получаем список тестов, которые должны расскипаться в *Testcop* в рамках переданных в качестве параметров задач (чтобы отлавливать тесты, которые чинятся путём не прямого изменения коллбека самого теста или его артефактов (дампов и скриншотов), а, например, путём изменения только кода сервиса); данное событие имеет меньший приоритет, чем любое другое, что означает, что если инструмент определил, что с тестом произошло хотя бы одно другое событие (модификация теста, изменение артефакта и т. д.), то событие изменения состояния теста в *Testcop* будет проигнорированно и в таблицу изменений не попадёт
- отправляем данные в таблицу после каждого влития пулл-реквеста в основную ветку

## Данные в таблице

Таблица хранит события, которые произошли с тестами, вместе с полной информацией о тестах.

```sql
CREATE TABLE stats.test_changes ON CLUSTER '{cluster}' (
    `datetime` DateTime('UTC'), -- время записи события в таблицу
    `runId` String, -- id-запуска, например, id-задачи в Sandbox
    `project` String,
    `type` String, -- тип теста
    `file` String,
    `id` String,
    `prevId` String, -- id-теста до переименования
    `fullTitle` String,
    `browserId` String,
    `vteam` String,
    `contentHash` String, -- md5 от коллбека теста
    `dumpsDir` String,
    `screenshotsDir` String,
    `event` String, -- added, deleted, modified
    `change` String, -- content, dump, screenshot, testcop
    `source` String -- vcs, user
) ENGINE = ReplicatedMergeTree('/stats.test_changes', '{replica}')
PARTITION BY toYYYYMM(datetime)
ORDER BY (datetime, type, fullTitle, browserId)
SETTINGS index_granularity = 8192
```

### Описание событий

- добавление теста: `event: added`, `change: content`, `source: vcs`, `prevId: <id>` (если тест был "добавлен" через переименование другого теста)
- удаление/изменение теста: `event: deleted/modifed`, `change: content`, `source: vcs`
- добавление/изменение/удаление дампа/скриншота: `event: added/deleted/modified`, `change: dump/screenshot`, `source: vcs`
- ручной расскип теста: `event: modified`, `change: testcop`, `source: user`
- расскип теста по задаче: `event: modified`, `change: testcop`, `source: vcs`

## Установка

```bash
$ npm install @yandex-int/test-changes-collector --registry=http://npm.yandex-team.ru
```

## Использование

```
test-changes-collector [paths...]

A tool for collecting of test changes in a project

Positionals:
  paths  List of file paths  [string] [default: []]

Options:
  --help, -h       Show help  [boolean]
  --version, -v    Show version number  [boolean]
  --run-id         Run id  [string] [default: ""]
  --type           Test type  [array] [required]
  --concurrency    Concurrency of processing of different test types  [number] [default: The number of test types]
  --datetime       Datetime that will be used when writing to the database table  [string] [default: Current UTC datetime]
  --project        Project name  [string] [default: Current dirname]
  --issue          Issue key that forcibly enables tests  [array] [default: []]
  --envs           List of environments to read tests (stringified JSON)  [string]
  --dry-run        Do not modify database table  [boolean] [default: false]
  --changed-files  Path to a list of changed files  [string]
```

### Опции и аргументы

- `--run-id` – id-запуска утилиты
- `--type` – тип тестов (*hermione* или *hermione-e2e*)
- `--concurrency` – параллельность обработки разных типов тестов (параллельное чтение с файловой системы разных типов тестов может конфликтовать друг с другом, поэтому рекомендуется выставлять значение `1`)
- `--datetime` – дата, которая будет использована для записи событий в таблицу
- `--project` – название проекта (используется и для записи событий в таблицу, и для получения данных по *API* из *Testcop*)
- `--issue` – id-задачи в *Startek*, в рамках которой расскипываются тесты
- `--envs` – список окружений в JSON-формате для чтения тестов (опция актуальна для проектов, которые завязаны на переменные среды окружения при чтении тестов) 
- `--dry-run` – запись событий в таблицу не будет произведена
- `--changed-files` – путь к файлу со списком изменнённых файлов в следующем формате (формат совпадает с тем, который отдает `arc log`):
  ```json
  [
      { "path": "some/file1.ext", "status": "new file" },
      { "path": "some/file2.ext", "status": "deleted" },
      { "path": "some/file3.ext", "status": "modified" }
  ]
  ```
- `[paths...]` – список изменённых файлов (не конфликтует с опцией `--changed-files`), который интерпретируется как список файлов со статусом `modified`

### Переменные среды окружения

Переменные среды окружения, которые указаны по умолчанию, находятся в [конфиге](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/test-changes-collector/.config/env) утилиты.

- `CLICKHOUSE_USER` – имя пользователя для подключения к клиенту
- `CLICKHOUSE_PASSWORD` – пароль для подключения к клиенту, который находится в [секретнице](https://yav.yandex-team.ru/secret/sec-01dn2bvx4303h4h8azp3evfzh7/explore/versions)
- `CLICKHOUSE_HOSTS` – список хостов, на которых развёрнут клиент (через запятую)
- `CLICKHOUSE_PORT` – порт для подключения к клиенту
- `CLICKHOUSE_DATABASE` - имя базы данных
- `CLICKHOUSE_TABLE` – имя таблицы
- `HERMIONE_CONFIG_PATH` – путь до конфигурационного файла *hermione*-тестов
- `HERMIONE_E2E_CONFIG_PATH` – путь до конфигурационного файла *hermione-e2e*-тестов
- `PALMSYNC_HERMIONE_SPECS_TYPE` - тип тестовых сценариев для *hermione*-тестов
- `PALMSYNC_HERMIONE_E2E_SPECS_TYPE` – тип тестовых сценариев для *hermione-e2e*-тестов
- `DEBUG` – значение `test-changes-collector:*` запускает утилиту с дополнительным логированием

## Задачи в *Sandbox*

- [SANDBOX_CI_TEST_CHANGES_COLLECTOR](https://sandbox.yandex-team.ru/tasks?page=1&pageCapacity=20&type=SANDBOX_CI_TEST_CHANGES_COLLECTOR&children=true&created=7_days&forPage=tasks) – задача запускается для проектов *web4* и *fiji* в рамках сборки основной ветки
