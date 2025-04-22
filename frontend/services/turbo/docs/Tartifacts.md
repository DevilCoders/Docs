
# Сборка статики и динамики

Сборка проекта на реальные машинки осуществляется при помощи сборки пакетов — _static_(debian), _dynamic_(zip).

Описание файлов, которые попадут в той или иной пакет лежат в [tartifacts](https://github.yandex—team.ru/serp/turbo/blob/dev/.config/tartifacts/patterns.json)

 * _static_ — содержит в себе все статичные файлы которые едут на клиент пользователя (`_*.js`, `_*.css` etc)
 * _dynamic_ — содержит _runtime_ исполняемые файлы, шаблоны, core etc.

## Важно!
При добавлении/удалении любых файлов **обязательно** проверьте, попадают ли они в сборку.
Первый признак, что вы забыли поправить конфиг сборки — 'локально тесты проходят, в CI падают со странной ошибкой'.
Это так же касается и добавления npm пакетов которые будут исполнятся runtime, обязательно добавьте их в конфиг.
Если вам необходимо добавить/удалить директорию со статикой, то не забудьте прописать изменения в `.static_package`.

## static
Описание самого пакета лежит в папке [debian](https://github.yandex—team.ru/serp/turbo/tree/dev/debian), ее содержимое можно менять только когда вы **точно** знаете что делаете.

Пример как выглядит сборка статики:
```json
{
    "static": {
        "common": [
            "freeze/*"
        ],
        "pages": [
            "pages/*/_*.{css,js}"
        ],
        "bundles": [
            "bundles/*/_*.{css,js}"
        ],
        "debian": [
            "debian/**",
            ".static_package",
            "version",
            "GNUmakefile",
            "package.json"
        ]
    }
}
```
TODO: расписать секции.

## dynamic
Пример сборки динамики:
```json
{
    "dynamic": {
        "common": [
            "GITHEAD",
            "routes.json",
            "core/**",
            "data—stubs/**",
            "main.renderer.*",
            "blockstat.dict.json",
            "meta.js",
            "node_modules/@yandex—int/**",
            "node_modules/lodash/lodash.js",
            "node_modules/lodash/package.json",
            "node_modules/moment/**",
            "configs/current/**"
        ],
        "pages": [
            "pages/*/*.bemhtml.js",
            "pages/*/_*.css",
            "bundles/*/_*.{css,js}"
        ]
    }
}
```
TODO: расписать секции.

### static_package
Сборка зафриженых файлов.

Сборка отрабатывает внутри сборки debian пакета с основной статикой
