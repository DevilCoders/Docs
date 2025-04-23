# `@yandex-market/tsconfig` [![npm version](https://badger.yandex-team.ru/npm/@yandex-market/tsconfig/version.svg)](https://github.yandex-team.ru/market/tsconfig) [![oko health](https://badger.yandex-team.ru/oko/repo/market/tsconfig/health.svg)](https://oko.yandex-team.ru/repo/market/tsconfig)

Общие конфиги TypeScript для Маркета, сформированные и одобренные [комитетом](https://wiki.yandex-team.ru/Market/frontend/workgroups/Typescript/).

## Установка

Для использования общих конфигов Маркета и деклараций следует установить пакет:

```shell
$ npm install @yandex-market/tsconfig --save-dev
```

## Подключение

Для подключения общего конфига Маркета используйте директиву `extends`
в локальном файле `tsconfig.json` вашего проекта.

Маркетные конфиги TypeScript поддерживают 2 модульные системы: **ECMAScript** и **CommonJS**.
Вы можете использовать подходящий конфиг для вашего проекта.

### ECMAScript

Если в проекте используются ES-модули, то подключите базовый конфиг следующим способом:

```json
{
    "extends": "@yandex-market/tsconfig/esm"
}
```

### CommonJS

Если в проекте используются CJS-модули, то подключите базовый конфиг следующим способом:

```json
{
    "extends": "@yandex-market/tsconfig/cjs"
}
```

### Отладочный конфиг

При нужде использовать отладочный конфиг с инлайном source-maps, следует воспользоваться `debug`-конфигом:

```json
{
    "extends": "@yandex-market/tsconfig/[esm|cjs]-debug"
}
```

Где `[esm|cjs]` — выбрать нужный.

## Декларации

Для Маркета были также написаны общие декларации, которые рекомендованы к использованию в проектах (при надобности).

### CSS Modules

По умолчанию TypeScript не поддерживает [CSS Modules](https://github.com/css-modules/css-modules) и при компиляции сообщает о каждом импорте как об ошибке. Чтобы этого избежать, для проектов, использующих эту функциональность, написана [общая декларация](./declarations/CSSModules.d.ts). Для её работы следует подключить файл с декларациями (`d.ts`) в `tsconfig.json`:

```json
{
    "files": [
        "node_modules/@yandex-market/tsconfig/declarations/CSSModules.d.ts"
    ]
}
```

После подключения этой декларации, TypeScript начнёт понимать импорты CSS-модулей и перестанет определять их как ошибку в коде.

Для валидации используемых стилей из CSS-модулей следует расширить настройки компилятора, подключив плагин [`typescript-plugin-css-modules`](https://github.com/mrmckeb/typescript-plugin-css-modules):

```shell
$ npm install typescript-plugin-css-modules --save-dev
```

Далее следует расширить директиву `compilerOptions` в конфиге TypeScript проекта:

```json
{
    "compilerOptions": {
        "plugins": [
            {
                "name": "typescript-plugin-css-modules"
            }
        ]
    }
}
```

Подробную информацию о плагине и его функциональности читайте в [репозитории](https://github.com/mrmckeb/typescript-plugin-css-modules).

### SVG Modules

По умолчанию TypeScript так же не поддерживает импорт SVG-файлов и на этапе компиляции выбрасывает ошибку типов. Для разрешения этой проблемы существует [общая декларация](./declarations/SVG.d.ts). Для её работы следует подключить файл с декларациями (`d.ts`) в `tsconfig.json`:

```json
{
    "files": [
        "node_modules/@yandex-market/tsconfig/declarations/SVG.d.ts"
    ]
}
```

## Рабочая группа

- [Александр Лукин](https://staff.yandex-team.ru/crewman)
- [Александр Феоктистов](https://staff.yandex-team.ru/feoktistov)
- [Владимир Руденко](https://staff.yandex-team.ru/hurtsok)
- [Даниял Гулиев](https://staff.yandex-team.ru/tzota)
- [Егор Быховцев](https://staff.yandex-team.ru/bykhovtsev)
- [Максим Афанасьев](https://staff.yandex-team.ru/afmn)
- [Михаил Силаев](https://staff.yandex-team.ru/gheljenor)
- [Олег Тамаринцев](https://staff.yandex-team.ru/tamarintsev)
- [Тамерлан Локьяев](https://staff.yandex-team.ru/yatamik)

Команда на [GitHub](https://github.yandex-team.ru/orgs/market/teams/typescript).
