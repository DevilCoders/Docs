# resolvers

В этой директории хранятся резолверы.

Подробнее о резолверах можно прочитать здесь:
[https://github.yandex-team.ru/market/mandrel/blob/master/src/resolvers](https://github.yandex-team.ru/market/monomarket/tree/master/lib/lib/mandrel/src/resolvers)

Общие соглашения Маркета находятся здесь:
[https://wiki.yandex-team.ru/market/frontend/conventions](https://wiki.yandex-team.ru/market/frontend/conventions)

## Файловая структура

Резолверы, относящиеся к одной сущности, лежат в директории с именем в camelCase, соответствующем этой сущности. В каждой такой директории могут быть следующие файлы:

### `index`

В `index.js` реэкспортятся все резолверы, лежащие в текущей директории.

Пример
```(javascript)
export {default as resolveModifications} from './resolveModifications';
```

### Файл с резолвером

Название файла повторяет название резолвера, название резолвера следует начинать со слова resolve, экспорт - дефолтный

### `__spec__`

Папка с юнит-тестами. Может отсутствовать, если резолверы имеют простую логику или идет разработка в Режиме 1.
Для каждого резолвера, который хотим покрыть тестами, создается одноименный файл
