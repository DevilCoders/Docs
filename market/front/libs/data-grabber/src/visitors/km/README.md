## Visitors для карточки модели.

Тут собраны visitors (посетители) для сграбливания данных с карточки модели и ее частей.

Пример карточки модели: https://market.yandex.ru/product--smartfon-samsung-galaxy-a50-64gb/394273081

### Про visitors из этот папки

* `do.js` - получение информации по дефолтному офферу.
* `do-and-top6.js` - получение информации по дефолтному офферу и топ-6 для сравнения.
* `top6-list.js` - получение информации по всему списку топ-6.
* `top6-snippets.js` - получение информации по сниппетам из топ-6.

Визитка (детали в папке визиторов визитки)
* `./vizitka/main.js` - получение основной информации по визитке.
* `./vizitka/filter-group.js` - получение информации по филтрам визитки для групповых карточек.
* `./vizitka/filter-clothes.js` - получение информации по филтрам визитки для карточек одежды.

### Как использовать

Опция для использования при cli-вызове data-grabber:

* `do.js`: `--visitor=/km/do`
* `do-and-top6.js`: `--visitor=/km/do-and-top6`
* `top6-list.js`: `--visitor=/km/top6-list`
* `top6-snippets.js`: `--visitor=/km/top6-snippets`

Визитка (детали в папке визиторов визитки)
* `main.js`: `--visitor=/km/vizitka/main`
* `filter-group.js`: `--visitor=/km/vizitka/filter-group`
* `filter-clothes.js`: `--visitor=/km/vizitka/filter-clothes`