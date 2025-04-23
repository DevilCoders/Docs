## Visitors для визитки карточки модели.

Тут собраны visitors (посетители) для сграбливания данных с визитки карточки модели и ее частей.

Пример страницы с визиткой карточки модели: https://market.yandex.ru/product--smartfon-samsung-galaxy-a50-64gb/394273081

### Про visitors из этот папки

* `main.js` - получение основной информации по визитке.
* `filter-group.js` - получение информации по филтрам визитки для групповых карточек.
* `filter-clothes.js` - получение информации по филтрам визитки для карточек одежды.

### Как использовать

Опция для использования при cli-вызове data-grabber:

* `main.js`: `--visitor=/km/vizitka/main`
* `filter-group.js`: `--visitor=/km/vizitka/filter-group`
* `filter-clothes.js`: `--visitor=/km/vizitka/filter-clothes`