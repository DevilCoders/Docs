# map

Блок для построения карты, а также получения API карт.

## Обзор блока

### Модификаторы блока

| Модификатор | Допустимые значения | Способы использования | Описание |
| ----------- | ------------------- | -------------------- | -------- |
| <a href="#init">init</a> | <code>auto</code> | <code>BEMJSON</code> | Автоматическая инициализация карты. |

### Специализированные поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| <a href="#state">state</a> | <code>Object</code> | Начальное состояние карты, передаваемое в [конструктор](https://tech.yandex.ru/maps/doc/jsapi/2.1/ref/reference/Map-docpage/#param-state) |
| <a href="#options">options</a> | <code>Object</code> | [Опции](https://tech.yandex.ru/maps/doc/jsapi/2.1/ref/reference/Map-docpage/#param-options) инициализации карты |
| <a href="#elems">elems</a> | <code>String[]</code> | Список подключаемых плагинов |

## Описание блока

Блок создает карту на основе АПИ Яндекс Карт, а также предоставляет доступ к этому АПИ.

### Модификаторы блока

<a name="init"></a>

#### Модификатор `init`

Допустимое значение: `auto`.

Способы использования: `BEMJSON`.

Отвечает за автоматическую инициализацию карты, после загрузки страницы.

```js
{
    block: 'map',
    mods: { theme: 'islands', init: 'auto' }
}
```

### Специализированные поля блока

<a name="state"></a>

#### Поле `state`

Тип: `Object`.

Определяет начальное состояние карты. [Подробнее]().

```js
{
    block: 'map',
    state: {
        zoom: 7,
        controls: ['zoom']
    }
}
```

<a name="options"></a>

#### Поле `options`

Тип: `Object`.

Определяет опции инициализации карты. [Подробнее](https://tech.yandex.ru/maps/doc/jsapi/2.1/ref/reference/Map-docpage/#param-options)

```js
{
    block: 'map',
    options: {
        yandexMapDisablePoiInteractivity: true,
        suppressMapOpenBlock: true
    }
}
```

<a name="elems"></a>

#### Поле `elems`

Тип: `String[]`.

Определяет набор подключенных плагинов.

* heatmap - плагин тепловой карты. [Подробнее](https://github.com/yandex/mapsapi-heatmap)

```js
{
    block: 'map',
    elems: ['heatmap']
}
```
