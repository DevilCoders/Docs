# sovetnik-components

Репозиторий с компонентами Советника

## Что такое компонент?
**Компонент** - штука, которая может быть отрисована отдельно, либо в составе другого компонента
Все компоненты лежат в папке `components`. 


Компонент состоит из трех частей:

1. JS-код компонента (`<название_компонента>.js`)
2. Файл подключение стилей, который использует компонент (`style.js`)
3. Mustache-шаблон компонента (`<название_компонента>.mustache`)

У каждого компонента есть данные, которые он умеет отрисовывать. Они находятся в папке `data`
Все отрисованные компоненты находятся в файле `rendered/component.html`

Все стили лежат в папке `styles`

## Для начала работы

1. клонируем репозиторий 
2. устанавливаем [NodeJS](https://nodejs.org/en/) версии 4 или выше
3. запускаем npm install

## Работа с задачами
Чтобы начать работу с задачей:

1. нужно перейти в бранч `master`: `git checkout master`
2. подтянуть все последние изменения: `git pull`
3. создать свой бранч. название бранча - номер задачи с префиксом `hotfix/`. Т.е. если мы работаем над задачей `SOVETNIK-100500`, то работу ведем в `hotfix/100500`: `git checkout -b hotfix/100500`

Чтобы завершить работу с задачей:

1. приводим стили в правильный формат (пока вручную): `npm run format`
2. находясь в бранче с задачей делаем коммит (`git commit -m 'Номер задачи, над которой работали'`) и пуш (`git push origin НАЗВАНИЕ_БРАНЧА`)
3. в интерфейсе гитхаба создаем Pull Request в ветку `master`


## Сборка компонентов
Мы умеем собирать компоненты с разными данными и смотреть, как они будут выглядеть в этом случае.

Чтобы собрать все компоненты, нужно выполнить команду `npm run build`

Что происходит при сборке:

1. всем стилям добавляется префикс `#sovetnik`
2. все подключения `url(path/to/image)` преобразуются в BASE64
3. для селектора `#sovetnik *` все стили проставляются в дефолтные значения. Список стилей ниже 
5. добавляются вендор-префиксы
6. всем стилям добавляется `!important`


Для сборки отдельного компонента необходимо выполнить следующую команду:

    npm run build <component-name>

или

    node builder/build-component.js <component-name>

> component-name - название компонента

Если необходимо собрать несколько компонентов, то достаточно выполнить следующее:

    npm run build <component-name-1> <component-name-2>

или

    node builder/build-component.js <component-name-1> <component-name-2>

Примеры:

- `npm run build aviabar`
- `npm run build aviabar clothes`
- `node builder/build-component.js aviabar clothes`


#### Дефолтные значения стилей
```css

div#sovetnik * {
    -webkit-animation: none 0s ease 0s 1 normal none running !important;
            animation: none 0s ease 0s 1 normal none running !important;
    -webkit-backface-visibility: visible !important;
            backface-visibility: visible !important;
    background: transparent none repeat 0 0 / auto auto padding-box border-box scroll !important;
    border: medium none currentColor !important;
    border-collapse: separate !important;
    -o-border-image: none !important;
       border-image: none !important;
    border-radius: 0 !important;
    border-spacing: 0 !important;
    bottom: auto !important;
    box-shadow: none !important;
    box-sizing: content-box !important;
    caption-side: top !important;
    clear: none !important;
    clip: auto !important;
    color: #000 !important;
    -webkit-columns: auto !important;
       -moz-columns: auto !important;
            columns: auto !important;
    -webkit-column-count: auto !important;
       -moz-column-count: auto !important;
            column-count: auto !important;
    -webkit-column-fill: balance !important;
       -moz-column-fill: balance !important;
            column-fill: balance !important;
    -webkit-column-gap: normal !important;
       -moz-column-gap: normal !important;
            column-gap: normal !important;
    -webkit-column-rule: medium none currentColor !important;
       -moz-column-rule: medium none currentColor !important;
            column-rule: medium none currentColor !important;
    -webkit-column-span: 1 !important;
       -moz-column-span: 1 !important;
            column-span: 1 !important;
    -webkit-column-width: auto !important;
       -moz-column-width: auto !important;
            column-width: auto !important;
    content: normal !important;
    counter-increment: none !important;
    counter-reset: none !important;
    cursor: auto !important;
    direction: ltr !important;
    display: inline !important;
    empty-cells: show !important;
    float: none !important;
    font-family: serif !important;
    font-size: medium !important;
    font-style: normal !important;
    font-variant: normal !important;
    font-weight: normal !important;
    font-stretch: normal !important;
    line-height: normal !important;
    height: auto !important;
    -webkit-hyphens: none !important;
        -ms-hyphens: none !important;
            hyphens: none !important;
    left: auto !important;
    letter-spacing: normal !important;
    list-style: disc outside none !important;
    margin: 0 !important;
    max-height: none !important;
    max-width: none !important;
    min-height: 0 !important;
    min-width: 0 !important;
    opacity: 1 !important;
    orphans: 2 !important;
    outline: medium none invert !important;
    overflow: visible !important;
    overflow-x: visible !important;
    overflow-y: visible !important;
    padding: 0 !important;
    page-break-after: auto !important;
    page-break-before: auto !important;
    page-break-inside: auto !important;
    -webkit-perspective: none !important;
            perspective: none !important;
    -webkit-perspective-origin: 50% 50% !important;
            perspective-origin: 50% 50% !important;
    position: static !important;
    right: auto !important;
    -moz-tab-size: 8 !important;
      -o-tab-size: 8 !important;
         tab-size: 8 !important;
    table-layout: auto !important;
    text-align: left !important;
    -moz-text-align-last: auto !important;
         text-align-last: auto !important;
    text-decoration: none !important;
    text-indent: 0 !important;
    text-shadow: none !important;
    text-transform: none !important;
    top: auto !important;
    -webkit-transform: none !important;
            transform: none !important;
    -webkit-transform-origin: 50% 50% 0 !important;
            transform-origin: 50% 50% 0 !important;
    -webkit-transform-style: flat !important;
            transform-style: flat !important;
    -webkit-transition: none 0s ease 0s !important;
    transition: none 0s ease 0s !important;
    unicode-bidi: normal !important;
    vertical-align: baseline !important;
    visibility: visible !important;
    white-space: normal !important;
    widows: 2 !important;
    width: auto !important;
    word-spacing: normal !important;
    z-index: auto !important;
    all: initial !important;

    cursor: inherit !important;
    white-space: inherit !important;

    box-sizing: border-box !important;

    color: inherit !important;

    font: inherit !important;
    line-height: normal !important;
    font-family: inherit !important;
    font-size: inherit !important;
    font-weight: inherit !important;
    text-align: inherit !important;
}

```
