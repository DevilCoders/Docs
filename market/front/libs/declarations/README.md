# declarations

## Структура директорий
```sh
declarations/
    flow-typed/npm/     # Декларации из flow-typed, ставятся автоматически и не изменяются
    custom/             # Собственные декларации, пишут вручную с соблюдением кодстайла
    stubs/              # Стабы модулей, например для .css
```

## Подключение в проект
1. Добавить пакет `@yandex-market/declarations` в `package.json` проекта.
2. Добавить в раздел `[libs]` в `.flowconfig` следующие пути
    ```
    node_modules/@yandex-market/declarations/flow-typed
    node_modules/@yandex-market/declarations/custom
    ```
3. Указать нужные стабы в разделе `[options]`:
    ```
    module.name_mapper.extension='styl' -> '@yandex-market/declarations/stubs/css.js'
    ```
4. Использование "explicit type arguments in new and call expressions" потребует обновление версии babel-eslint до версии 9

## Добавление новой зависимости

```sh
npm run add -- dep1 dep2 dep3@0.0.1
```

Таким образом зависимости поставятся как dev, и flow-typed либо скачает декларации для этих зависимостей, если они есть, либо застабает их.

В случае, если приедут декларации для пакетов, для которых раннее были только стабы, то следует удалить стабы.
