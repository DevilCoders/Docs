# Appmetrica Frontend

1) Заводим виртуалку по инструкции:

https://wiki.yandex-team.ru/JandexMetrika/frontend/dev_computer_for_everyone/

2) Ставим зависимости и запускаем:
```
cd ./frontend
npm run bootstrap:appmetrica

cd ./services/appmetrica

LANGS=ru make compose-up
```

Какие страницы ведут в bem, а какие в react можно посмотреть в конфиге nginx - https://a.yandex-team.ru/arc_vcs/metrika/frontend/front/services/appmetrica/nginx/conf.d/default.conf.template

## Переменные окружения

Можно влиять на программу через переменные окружения, например собрать только русский язык:
```
LANGS=ru make compose-up
```

Другое окружение в bishop:
```bash
BISHOP_ENVIRONMENT_NAME=metrika.deploy.frontend.appmetrica.testing.development.rifler make compose-up
```

Все переменные окружения прокидываются в docker-compose.yml, откуда переменную можно прокинуть в нужный сервис

## Структура проекта

```
/app
    /components
    /ducks
    /lib
    /modules
    /sagas
    /selectors
/cloud
/configs
/nginx
/server
/tvm
/vault
```

#### /components

В `components` следует хранить самые простые общие компоненты. `Button`, `Input`, `Menu` – всё это хорошие кандидаты для `components`. Или немного более сложные  – `DateRange`, `BreadCrumbs`, тоже уместны.   `CrashStacktraceViewer`, `PostbackTypeSelect` – для них  `components` не подходит, такие компоненты следует размещать в `modules`, об этом дальше.

В идеальном случае папка `components` должна быть заменена общей библиотекой компонентов (`@metrika/ui`). Иначе говоря, все общие компоненты должны отправляться туда, а не в `components`. Но идеал не достижим, а тем прекрасен.

#### /modules

В `modules` лежат  бизнес-сущности проекта в виде `React` компонентов. Скорее всего такие компоненты будут использовать данные из `redux store` и иметь свои `ducks` или `redux saga`. Однако, компоненты не подключенные к `redux store`, но, представляющие из себя законченную сущность, так же следует размещать тут.

Например, хотим реализовать компонент `Footer`. Допустим, этот компонент содержит только ссылки на разные ресурсы и некоторое количество стилей и разметки, он не использует данные из `redux store` и не реализует никакой логики. Такой компонент стоит разместить в `modules`, так как он реализует конкретную бизнес-сущность, не может быть использован в других компонентах и в перспективе может обзавестись собственной бизнес-логикой, например, функциональностью переключения языка.

`modules` - строительный материал для дерева `React` и `redux store`.

Каждый модуль может состоять из модулей. Модуль уже являющийся дочерним модулем **не может** содержать модули.

```
/modules
    /desktop
        /EventsReport
            /modules
                /Sampling
                ...
        /AudienceReport
            /modules
                /Table
                /TableHeaderCell
                /ChartLegend
                ...
        ...
```

Выше продемонстрирован пример структуры двух отчётов. Отчёт состоит из большого количества модулей. Эти модули могут использовать друг-друга. Например, модуль `Table`  в `AudienceReport` может использовать модуль `TableHeaderCell`. Однако, модуль `Table` не может использовать модули принадлежащие другому модулю, например, `modules/desktop/EventsReport/modules/Sampling`. Иначе говоря, модуль может использовать только модули своего уровня и выше.
Чтобы использовать модуль `Sampling` внутри модуля `modules/desktop/AudienceReport/modules/Table` следует разместить его в `modules/desktop/Sampling`.

Внутри модуль может выглядеть так:

```
/AppsMenu
    /AppsMenu.i18n
    /lib
        metadata.ts
        ...
    /modules
        /AppItem
            duck.ts
            index.tsx (или AppItem.tsx)
            saga.ts
            styles.tsx
        /NewAppButton
        ...
    actions.ts
    ducks.ts
    index.tsx (или AppsMenu.tsx)
    saga.ts
    selectors.ts
    styles.tsx
```

#### /lib
Модули, предоставляющие общие независимые от отображения данные и логику, следует размещать в `/lib`.

Компоненты не могут хранится в `lib`.

#### /ducks
Тут следует располагать те duck, которые не могут быть однозначно связаны с конкретным компонентом для отображения и могут быть использованы в рамках разных модулей. Предполагается, что таких duck будет не много. Примером могут служить `config` и `user`.
