# coverage-selector-report

Генератор отчетов для [coverage-selector](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/coverage-selector).

## Установка

```sh
npm install @yandex-int/coverage-selector-report --registry https://npm.yandex-team.ru
```

## Использование

Сгенерировать отчет для тестов "testId1" и "testId2":

```sh
npx coverage-selector-report path/to/log.db --test-ids testId1,testId2
```

HTML-отчет будет лежать в директории ./coverage (настраивается опцией `-r [report-dir]`).
hermione-тесты также можно грепать, для этого необходима локальная установка `coverage-selector-report` в проект.

```sh
npx coverage-selector-report path/to/log.db --grep 'Тест1|Тест2'
```

Промежуточное покрытие в istanbul-совместимом формате можно сохранять в директорию для последующего разбора.
Для этого следует указать опцию `-s [path-to-json-file]`.
