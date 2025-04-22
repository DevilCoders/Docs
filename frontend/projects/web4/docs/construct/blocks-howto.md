# Блоки. Рецепты и примеры

1. [Заготовка](#1-Заготовка)
2. [Бандл](#2-Бандл)
3. [Документация API](#3-Документация-API)
4. [Поддержка полной/краткой формы API](#4-Поддержка-полнойкраткой-формы-API)
5. [Переводы](#5-Переводы)
6. [Примеры](#6-Примеры)
7. [Hermione-тесты](#7-Hermione-тесты)

## Как сделать свой блок?
### 1. Заготовка
Создаём новый блок на файловой системе в папке [construct](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct) на соответствующем уровне переопределения.

Обязательно добавляем:

  1. `if (!dataset) return;`
  2. `context.reportData.pushBundle('my-block')`

**пример:**
```js
/* construct/blocks-common/my-block/my-block.priv.js */
blocks['my-block'] = function(context, dataset) {
  if (!dataset) return;

  context.reportData.pushBundle('my-block');

  /* ... */
};

```

### 2. Бандл

Создаем бандлы на нужных платформах (desktop/touch-phone). `'Имя бандла === Имя блока'`. В `bemdecl.js` бандла должен быть указан также только этот блок.

**пример для desktop:**
```js
/* bundles-desktop/my-block/my-block.bemdecl.js */
exports.blocks = [
    { name: 'my-block' }
];
```

Для остальных платформ нужно сделать аналогично.

### 3. Документация API

Документируем наш блок. Описание параметра `dataset`, то есть API блока, нужно взять из задачи с верификацией API, ссылка на которую должна быть у вас в стартреке.

**пример:**
```js
/* construct/blocks-common/my-block/my-block.priv.js */
/**
 * Мой блок, который делает и то, и другое, и пятое и десятое.
 *
 * @param {Context} context
 * @param {MyBlock} dataset,
 *
 * @returns {Bemjson}
 */
blocks['my-block'] = function(context, dataset) {
  /* ... */
};

/**
 * @typedef {MyBlockObject|Text} MyBlock
 */

/**
 * @typedef {Object} MyBlockObject
 *
 * @property {Boolean} [isItTrue=true] - если true, то делает только то и другое.
 * @property {Text} text - Текст с важной информацией для пользователя.
 */
```

### 4. Поддержка полной/краткой формы API

Если в качестве обязательного поля у вас выступает `text` или `items`, можно воспользоваться соответствующим хелпером.

**пример:**
```js
/* construct/blocks-common/my-block/my-block.priv.js */
/* ... */
blocks['my-block'] = function(context, dataset) {
  if (!dataset) return;

  context.reportData.pushBundle('my-block');

  /* --> */  dataset = blocks['construct__preapre-text'](dataset);

};
/* ... */
```

### 5. Переводы

См. [документацию на wiki](https://wiki.yandex-team.ru/search-interfaces/tanker/tanker-kit/).

### 6. Примеры

Проверять новый блок можно через [примеры](https://wiki.yandex-team.ru/serp/constructor/block-examples/).
Пример данных:

```js
/* construct/blocks-common/my-block/my-block.examples/my-block.example.json */
{
  "adapter": "test",
  "block": "test-layout",
  "preventLegacy": true,
  "godMode": true,
  "blocks": [{
    /* Данные */
  }]
}
```

Тут используется тестовые адаптер и набор магических параметров (которые мы всегда повторяем). Они пробрасывают данные из поля `my-block` в блок с таким названием,
и то что получилось показывают на Серпе.

Увидеть пример можно локально: `http://localhost:{port}/search?blocksdata=my-block.example.json`

### 7. Hermione-тесты

После того, как блок готов, нужно написать на него hermione-тест, используя в качестве данных example.json-ы из [п. 6](#6-Проверяем-что-все-работает). Тест кладется рядом с кодом блока в `construct/blocks-common/my-block/my-block.hermione.js` и выглядит так:

```js
specs('Блок my-block', function() {
    it('Внешний вид', function() {
        const PO = this.PO;

        return this.browser
            .yaOpenSerp({ blocksdata: 'my-block.example' }, '.my-block')
            .assertView('plain', '.serp-item');
    });
});
```
