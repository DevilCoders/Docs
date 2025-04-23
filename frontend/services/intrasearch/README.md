# Внутренний поиск

* внутри Яндекса [https://search.yandex-team.ru/search?text=яндекс](https://search.yandex-team.ru/search?text=яндекс)
* тестинг внутри Яндекс [https://search.test.yandex-team.ru/search?text=яндекс](https://search.test.yandex-team.ru/search?text=яндекс)
* для других компаний (b2b) [https://bisearch.yandex.ru/search/wiki?text=yandex](https://bisearch.yandex.ru/search/wiki?text=yandex)
* тестинг B2b [https://bisearch.test.yandex.ru/search/wiki?text=yandex](https://bisearch.test.yandex.ru/search/wiki?text=yandex)

### Графики

[Риалтаймовый график скорости](https://rum.yandex-team.ru/projects/intrasearch/projectDashboard)

[Информация о фронтовых ошибках](https://error.yandex-team.ru/projects/intrasearch/projectDashboard)

### Чтобы запустить сервис, необходимы:

1. `nginx`
2. `nodejs 14`
4. [docker](https://www.docker.com/get-docker)

Также необходимо состоять в [команде разработки на ABC](https://abc.yandex-team.ru/services/isearch/)

### Как развернуть проект

1. Установить зависимости и собрать проект
    ```sh
    npm i
    npm run build
    ```

1. Настроить окружение с помощью `@yandex-int/make-my-env`, необходимо выполнить
    ```bash
    npx make-my-env
    ```

1. Запустить сервер

    интранет
    ```sh
    npm run start-local
    ```
    или b2b
    ```sh
    npm run start-local-b2b
    ```

1. Открыть в браузере

    интранет https://intrasearch.local.yandex-team.ru/search/?text=yandex

    или b2b https://intrasearch.local.yandex.ru/search/directory?text=yandex

    Для доступов к b2b аккаунты [тут](https://wiki.yandex-team.ru/intranetpoisk/b2b/akkaunty/)

### Разработка

1. Делаем изменения в коде и выполняем `npm run start-local` или `npm run start-local-b2b` для пересборки и запуска сервера

2. Переводы редактируются в [Танкере](https://tanker.yandex-team.ru/?project=isearch&branch=bem), скачиваются на проект командой `npm tanker`

3. Посмотреть дамп данных от бекенда abovemeta `&plainjson=1`

### Проверки (checks) Juggler
Общая конфигурация всех чеков Juggler хранится в `.monitorado.yml`.
Для обновления необходимо:
* поправить конфиг (по необходимости)
* посмотреть отличие от текущего: `npm run monitorado:diff`
* обновить чеки: `npm run monitorado:exec`
https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dtools.isearch&limit=40



### Тесты

*Тесты запускаются автоматически на каждый пулл-реквест*

1. Тесты bemhtml-шаблонов `npm run test:tmpl`

2. Юнит-тесты Express middlewares `npm run ci:unit`.

### Обновление bemhtml-шаблонов для тестов

1. Генерация новых шаблонов `npm run generate-templates`

2. Точечный перенос сгенерированных шаблонов `npm run update-bemspecs -- -E=^YourRegExp` где YourRegExp это regular expression, в соответствии с которым выбираются файлы для переноса.
Пример: `npm run update-bemspecs -- -E=^snippet_page_at-posts`

_Автоматичестки сгенерированные шаблоны не гарантируют прохождения тестов и может возникнуть необходимость править их вручную_

_Второй этап нужен всвязи с тем, что изначально шаблоны генерируются в папке `/node_modules/tools-access-lego`_

## Автотесты

Данные по покрытию гермиона-тестов выгружаются в [Стат](https://stat.yandex-team.ru/search.yandex-team.ru/tests/manual-and-skipped-tests).

[Про управление и запуск заскипанных тестов](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/services/testcop/docs/workflow/view-tests.md)

Ручные тесты с [manual] не используются и не актуализируются.

### Нужные ссылки
[Тестпалм](https://testpalm.yandex-team.ru/intrasearch_palmsync)

[Метрики автоматизации](https://stat.yandex-team.ru/search.yandex-team.ru/tests/manual-and-skipped-tests/)

[Шедулер для выгрузки метрик автоматизации](https://sandbox.yandex-team.ru/scheduler/23075/view)

[Таблица критичной функциональности](https://wiki.yandex-team.ru/Intranet/bugclassifier/)

### Запуск hermione-тестов локально

```bash
npx archon hermione <?any agruments for hermione>
```
Например:
```bash
npx archon hermione gui // режим gui
npx archon hermione --update-refs // перезапись скриншотов
npx archon hermione --retry 0 // без ретраев
```

Запись дампов:
```bash
npx archon hermione --mode read/write/create
```

### Запуск юнит-тестов Express middlewares локально
```bash
npm run unit
```

## Деплой

### В тестинг
Деплой происходит средствами CI Арканума:

Перейти на [страницу CI проекта](https://a.yandex-team.ru/projects/frontend/ci/releases/timeline?dir=frontend%2Fservices%2Fintrasearch&id=release)

Запустить релиз по кнопке "Run Deploy".

> Версия собранного релиза не то же, что версия в package.json, их номера не обязаны совпадать.

После выкатки в продакшен нужно закрыть релизный тикет с резолюцией "Решен".
На релиз должен **автоматически** проставиться релизный тег. 
> Релизный тег - метка, что релиз протестирован и отправлен на раскатку в прод.

При необходимости тег можно проставить вручную - переключиться на релизную ветку и выполнить: 

```bash
 arc push <commit>:tags/releases/frontend/intrasearch/<v.X.Y.Z>
```
где `commit` - HEAD-коммит релизной ветки, `v.X.Y.Z` - версия релиза.


<details><summary>Деплой с локального компьютера [deprecated]</summary><p>

*Иногда требуется задеплоить с локального компьютера. В обычной жизни делать это не рекомендуется.*

1. `npm version patch|minor|major` прогонит тесты, поднимет версию, сгенерирует запись в changelog.md на основе коммитов, сделает тег, запушит изменения
2. npm run release` - соберет и запушит Docker image **registry.yandex.net/tools/intrasearch-www** указанной версии (возьмет из package.json), зальет в [deploy intranet testing](https://deploy.yandex-team.ru/stages/isearch-www-intranet-testing) и [deploy b2b testing](https://deploy.yandex-team.ru/stages/isearch-www-b2b-testing)

</p></details>

### В прод
1. Обновить образ в deploy-стейджах [intranet](https://deploy.yandex-team.ru/stages/isearch-www-intranet-production) и [b2b](https://deploy.yandex-team.ru/stages/isearch-www-b2b-production) на нужную версию.

## Счётчики Яндекс.Метрики

При открытии результатов поиска в yandex-team.ru - логируем события в Яндекс.Метрику. Чтобы увидеть в консоле, какие счётчики были отправлены нужно указать query параметр `&dump_counters=1`

[Описание логируемых параметров](https://wiki.yandex-team.ru/devtoolsui/knowledge-base/intrasearch/logiruemye-v-metriku-sobytija/)
