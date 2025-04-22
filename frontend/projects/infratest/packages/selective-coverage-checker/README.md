# coverage-coverage-checker

Производит выборку тестов для запуска на основе данных из лога селективности и списка изменений.

## Установка

```sh
npm install @yandex-int/selective-coverage-checker --registry https://npm.yandex-team.ru
```

Для использования с git selective-coverage-checker необходимо установить и запускать в директории проекта.

## CLI

Вывести список тестов, которые должны быть запущены для изменений в диапазоне коммитов 8821926b..01bf2fd4:

```sh
npx @yandex-int/selective-coverage-checker 8821926b 01bf2fd4 -s selective-coverage-log
```

Использование подготовленного списка изменений (см. [diff-to-lines](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/diff-to-lines)):

```sh
npx @yandex-int/selective-coverage-checker -d diff-lines.json -s selective-coverage-log > selective-coverage-selection.json
```

## Hermione-плагин

Плагин для валидации и составления отчета по ошибкам селективности на основе покрытия.
В отчет будут включены упавшие тесты, не попавшие в выборку (`selective-coverage-selection.json`).

Пример конфигурации:
        
```javascript
module.exports = {
    plugins: {
        '@yandex-int/selective-coverage-checker/hermione': {
            enabled: true,
            selectionPath: 'selective-coverage-selection.json',
            reportPath: 'selective-coverage-fails.json'
        }
    }
};
```
