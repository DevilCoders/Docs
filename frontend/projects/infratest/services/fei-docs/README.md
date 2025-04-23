# SI Infra Docs

> ℹ️ По всем вопросам, связанным с этим таргетом, обращаться к @fenice.

## Требования к документам

Способ генерации TOC диктует следующие правила:

* Первая строка всегда должна быть h1, и она становится тайтлом страницы.
* Все дальнейшие заголовки должны быть h2 и ниже, и они попадают в ТОС.

Форматирование документов определяется правилами [YFM 2.0](https://github.com/yandex-cloud/yfm-transform/blob/master/DOCS.ru.md), кроме загруженных по ссылке документов: для них недоступны экшены в `{% %}`.

## Как выбрать место для документа

Первым делом необходимо определить место добавляемого(ых) документа(ов) в общей структуре проекта.

Документы *для пользователей* размещаются на верхнем уровне. Структура разделов должна быть удобна и понятна для пользователя. 

Документы *для дежурных FEI* размещаются в разделе Duty Knowledge Base, чтобы не смущать пользователей. Структура разделов должна быть удобна дежурным.

## Как добавить документ

Навигация документации генерируется для всех типов документов через запуск скрипта `pre_build.py`, поэтому все документы добавляются в конфигурационный файл `pre_build.json`. Вложенность элементов в конфигурационном файле определяет вложенность элементов в навигации.

Пункты навигации могут включать другие пункты навигации или ссылаться на конкретные документы. 

️⚠️ Рекомендуется использовать пункты только как пункты-документы **или** как пункты с вложенными пунктами во имя единообразия и предсказуемости: в навигации не видно разницы между пунктом с документом и пунктом без.

### Пункт-документ

#### GitHub

Для описания такого документа необходимо указать:

- название пункта в `name`,
- имя md-файла, в который документ будет сохранен, в `path`
- ссылку на raw content документа на GitHub в `url` (поддерживаются ссылки на внешний и внутренний GitHub).

Пример:

```
{
    "name": "hermione-assert-view-extended",
    "path": "hermione_assert_view_extended",
    "url": "https://raw.githubusercontent.com/ruslankhh/hermione-assert-view-extended/master/README.md"
},
{
    "name": "archon",
    "path": "archon",
    "url": "https://raw.github.yandex-team.ru/search-interfaces/infratest/master/packages/archon/README.md"
}
```
#### Arcadia

Для описания документа, который планируется разместить в Аркадии, необходимо указать только имя в `name` и путь на FS в `path`, а сам документ расположить по пути, соответствующему данному пункту.

### Пункт с вложенными пунктами

Для описания данного пункта необходимо указать имя пункта в `name`, имя файла в `path` и список подпунктов в `items` в виде массива объектов:

```
{
    "name": "Отчеты",
    "path": "reports",
    "items": [
        {
            "name": "gui-assistant",
            "path": "gui_assistant",
            "url": "https://raw.github.yandex-team.ru/search-interfaces/infratest/master/packages/gui-assistant/README.md"
        },
        {
            "name": "html-reporter",
            "path": "html_reporter",
            "url": "https://raw.githubusercontent.com/gemini-testing/html-reporter/master/README.md"
        },
        {
            "name": "html-reporter-extender",
            "path": "html_reporter_extender",
            "url": "https://raw.github.yandex-team.ru/search-interfaces/infratest/master/packages/html-reporter-extender/README.md"
        }
    ]
}
```

## Сборка

1. `python pre_build.py` (загружает файлы из GitHub)
2. `ya make` (собирает архив с документацией)

## Деплой

Деплой запускается по коммиту в транк ([код](https://a.yandex-team.ru/arc_vcs/testenv/jobs/sandbox_ci/FEIDocsDeploy.yaml), [testenv](https://beta-testenv.yandex-team.ru/project/sandbox_ci/job/FEI_DOCS_DEPLOY_TO_DAAS/history)) и по расписанию ([шедулер](https://sandbox.yandex-team.ru/scheduler/23409/view)).

В обоих случаях запускается задача `SI_INFRA_DOCS_PUBLISH` ([документация](https://a.yandex-team.ru/arc_vcs/sandbox/projects/sandbox_ci/infratest/si_infra_docs_publish)).

## Тестирование

### Ссылка на тестинг
* [https://si-infra.daas.locdoc-test.yandex-team.ru/](https://si-infra.daas.locdoc-test.yandex-team.ru/)

### Тестирование через ревью-реквест
1. Создать ревью-реквест
1. Склонировать последнюю задачу [шедулера](https://sandbox.yandex-team.ru/scheduler/23409/tasks?hidden=true&all_tags=false&all_hints=false&limit=20)
1. Удалить значение параметра `daas_prod_project`
1. Выставить значение параметра `daas_test_project` в `2014`
1. Выставить значение параметра arcadia_patch в `arc:<номер ревью-реквеста>`, например, `arc:1234567`.
1. Запустить задачу.

### Тестирование локально
1. Закоммитить свои изменения, поскольку код сборки документации с GitHub мутирует файлы.
1. Собрать: 
   - [документация](https://a.yandex-team.ru/arc_vcs/serp/infra/docs/#%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B0)
1. Задеплоить полученный `docs.tar.gz` в тестинг:
   - [документация](https://wiki.yandex-team.ru/doc-and-loc/doc/publish/Deplojj-ruchkojj/#arkadija/yamake/sphinx)
   - ID проекта в тестинге: `2014`

## Как завести похожую документацию

1. Заказать проект в DAAS: [форма](https://forms.yandex-team.ru/surveys/8557/).
    * про публикацию на doc.y-t.ru нужно договориться отдельно.
1. Сформировать аналогичный таргет.
1. Создать навигацию по проекту документации:
    1. Если нужна выгрузка из GitHub, то использовать трюк с `pre_build.py/pre_build.json`.
    1. Иначе, составить вручную.
1. Все имеющиеся документы разложить в Аркадии подходящим способом.
1. Если нужно добавить header/footer на каждую страницу (подключение своей метрики, ссылка на саппортную форму, ...), то использовать трюк с `pre_build.py`.
1. Настроить деплой:
    1. Если нужна выгрузка из GitHub, то деплой по коммиту + шедулер. Иначе, деплой по коммиту.
    1. Если использован трюк с `pre_build.py` перед сборкой, то использовать задачу `SI_INFRA_DOCS_PUBLISH`. Иначе, использовать задачу `YA_MAKE_DAAS`.
1. 🎉 Готово!
