# webhook-handler

`RUN_CRON_JOBS` - Регистрирует cron задач. Задача: [FEI-2423](https://st.yandex-team.ru/FEI-2423)

`RUN_SELECTIVE_TESTS` - Запускает селективные тесты в пулл-реквесте при изменении статуса задачи в Стартреке. Задачи: [FEI-633](https://st.yandex-team.ru/FEI-633) и [INFRADUTY-116](https://st.yandex-team.ru/INFRADUTY-116)

## API

### Обработка изменения статуса коммита

```
/v1/github/pull-request-status-change
```

#### Описание

Подписываемся на вебхук установки статуса коммита, смотрим, все ли нужные статусы прокрасились, и если да, то вычитаем из текущего времени время пулл-реквеста в свойстве pushed_at. Полученное значение отправляем в `stat.yandex-team.ru`.

Время прокраски всех статусов записывается только один раз на коммит, перезапуск сборки не учитывается.


### Закрытие задач после релиза

```
/v1/nanny/release-request-status-change
```

#### Описание

Закрывает связанные с релизом шаблонов задачи при переходе релиза в состояние CLOSED (Завершен).

### Закрытие связанных задач после релиза

```
/v1/nanny/release-ticket-status-change
```

#### Описание

Закрываем упомянутые в описании релизы шаблонов при переходе тикетов в отслеживаемых очередях в Няне в DEPLOY_SUCCESS (релиз раскатился).

### Закрытие задач после релиза (v2)

```
/v1/nanny/release-request-tickets-status-change
```
#### Описание
Закрывает связанные с релиз-реквестом задачи при переходе релиза в состояние CLOSED (Завершен) и всех его тикетов с тайтлом production в DEPLOY_SUCCESS

### Проставление поля «TestPalm Yaml File»

```
/v1/startrek/testpalm-issue-link
```
#### Описание

При появлении новой связи с TestPalm в тикете добавляем в поле "TestPalm Yaml File" путь до yaml-файла с тестсьютом из соответствующего тесткейса. Нужно для построения срезов багов по тестсьютам.

#### Как подключить свой сервис

- убедиться, что установлен `@yandex-int/palmsync` версии не ниже **4.9.0**. В этой версии добавлена ссылка на фильтр багов в описание тесткейса.
- подписать свою очередь на Startrek-вебхук об изменениях тикетов по определённому фильтру, чтобы подключить вебхук нужно заполнить [форму](https://wiki.yandex-team.ru/tracker/vodstvo/webhooks/#podkljucheniewebhook):
  - в качестве endpoint нужно указать следующий адрес: `https://webhook-handler.si.yandex-team.ru/v1/startrek/testpalm-issue-link?queue=<ИМЯ ВАШЕЙ ОЧЕРЕДИ>` (здесь имя очереди нужно для логирования).
  - ссылка на фильтр обычно выглядит так: `https://st.yandex-team.ru/filters/filter?query=Queue%3A%20<ИМЯ ВАШЕЙ ОЧЕРЕДИ>`.
  - в результате заявки будет создан тикет в очереди `TOOLS`, как только он закроется — всё готово.

### Удаление релизной ветки в GitHub
```
/v1/startrek/github-delete-release-branch
```
#### Описание
Удаляет релизную ветку в соответствии с `summary` в трекере. Условия выполнения настраиваются непосредственно в настройках триггера в трекере.
Структура пейлоада:
```json
{
  "issue": {
      "summary": "{{ issue.summary }}",
      "key": "{{ issue.key }}"
   },
   "comment": {
      "template": "searel-release-branch-deleted",
      "prefix": "Привет!",
      "postfix": "Пока!"
   }
}
```
Поля `comment.prefix` и `comment.postfix` опциональны.

### Создание релизного тега в Арке
```
/v1/startrek/create-arc-release-tag
```
#### Описание
Тег ставится на HEAD коммит релизной ветки, которая хранится в поле `branch` релизного тикета в Трекере. После создания релизного тега в тикет пишется комментарий, шаблон которого указывается в пейлоаде. Доступные шаблоны можно посмотреть в [ejs/templates].  Структура пейлоада:
```json
{
  "issue": {
      "key": "{{ issue.key }}",
      "branch": "{{ issue.branch }}",
   },
   "comment": {
      "template": "some-template",
      "prefix": "Привет!",
      "postfix": "Пока!"
   }
}
```
Поля `comment.prefix` и `comment.postfix` опциональны.

[ejs/templates]: https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/ejs/templates

### Сбор статистики по "плохим" ямлам

```
/v1/step/testpalm-testrun-finished
```

#### Описание
Все тест-кейсы из тест-рана фильтруются только по "плохим" статусам, а затем группируются по YAML-файлам.
Далее в рамках YAML-файла для каждого статуса считается количество тест-кейсов. Затем все это выгружается в Stat.

"плохие" YAML-файлы — YAML-файлы, в которых присутствуют тест-кейсы, у которых есть один из статусов:

```
'FAILED', 'BROKEN', 'SKIPPED', 'KNOWNBUG', 'BLOCKED'
```

Запись в Stat (таблица с секундным скейлом):

```json
{
    "fielddate": "2019-03-25 15:52:53",
    "project": "web4",
    "vteam": "GEO",
    "broken": 2,
    "failed": 2,
    "knownbug": 1,
    "skipped": 0,
    "blocked": 0,
    "yaml": "features/common/adapter-buy-tickets-pp-form-modern/adapter-buy-tickets-pp-form-modern-query-company.testpalm.yml"
}
```

Структура пейлоада:

```json5
{
  "project_id": "serp-js-100500", // проект в TestPalm
  "testrun_id": "5b9286daca6d354f21c760c8" // id тест-рана
}
```
## Разработка

- [Тестирование с arcanum](../merge-queue/docs/development/how-to-test-in-arcanum.md)
