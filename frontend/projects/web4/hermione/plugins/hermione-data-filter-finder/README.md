# hermione-data-filter-finder

Плагин для [hermione](https://github.com/gemini-testing/hermione) для поиска адаптеров для фильтрации данных.

## Установка

TODO: Пока что пакет не опубликован, нужно опубликовать

```
npm i -D @yandex-int/hermione-data-filter-finder --registry=http://npm.yandex-team.ru
```

## Использование

### Настройка

Необходимо подключить плагин в конфиге hermione:
```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-data-filter-finder': {
            enabled: false
        }
    },

    // ...
}
```

### Запуск

Запуск тестов с поиском адаптера для фильтрации данных:
```
DEBUG=hermione-data-filter-finder* npx hermione --play --find-data-filter
```
