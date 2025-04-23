# services-table

Блок используется для создания Табло сервисов (набор сервисов Яндекса в табличном виде). API блока позволяет:

* отображать готовые наборы сервисов, тематические и региональные (КУБР, Yandex.com, Турция, Рекламные);
* задавать произвольный набор сервисов;
* добавлять ссылку на региональную страницу [все сервисы](https://yandex.ru/all) Яндекса.

Текст в блоке автоматически локализуется, на основе значения глобального параметра `lang` из [i-global](../i-global/i-global.ru.md) (значение по умолчанию:`ru`).

## Обзор

* [Задание произвольного набора сервисов](#custom-set)
* [Добавление псевдокнопки «Все сервисы»](#add-all)

### Модификаторы блока

| Модификатор        | Допустимые значения          | Способы установки | Описание                 |
| ------------------ | ---------------------------- | ----------------- | ------------------------ |
| [type](#mods-type) | `ru`, `com`, `turkish`, `ad` | BEMJSON           | Готовые наборы сервисов. |
| [size](#mods-size) | `s`, `m`, `l`                | BEMJSON           | Ширина блока.            |

### BEMJSON-поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [items](#custom-set)| Array | Сокращенная запись элементов блока [item](#elems-short) (сервисов). Не используется одновременно с элементами `item` и полем `content`. |
| [all](#add-all) | Boolean | Сокращенная запись [элемента all](#elems-short). Используется только с полем `items`. |
| [content](#custom-set)| BEMJSON | Содержимое Табло. Используется для самостоятельной настройки сервисов, с помощью [элементов блока](#elems-short). Переопределяет значения заданные в полях `all`, `items`. |
| [prefsTarget](#fields-prefsTarget) | String | Значение HTML-атрибута `target` для URL сервисов Почта и Перевод. Используется только для набора с [модификатором type в значении com](#mods-type-com). |
| [contentRegion](#fields-contentRegion) | String | Регион пользователя. Не путать с языком интерфейса. |

<a name="elems-short"></a>
### Элементы блока

| Элемент | Описание |
| --------| -------- |
| [item](#custom-set) | Элемент Табло (сервис), реализованный блоком [service](../service/service.ru.md). |
| [all](#add-all)  | Псевдокнопка «Все сервисы». По умолчанию включена в [региональные наборы сервисов](#mods-type). |

## Подробнее

<a name="custom-set"></a>
### Задание произвольного набора сервисов

Формируется собственный список сервисов одним из следующих способов:

* **C помощью поля `items`** – упрощенный способ задания элементов `item` (сервисов).

 Каждому сервису соответствует набор значений

| Поле | Тип | Описание |
| ---- | --- | -------- |
| `service` | String | ID сервиса в Лего из [i-services](../common.blocks/i-services/__uri/i-services__uri.bemhtml.js).|
| `serviceIconMods` | BEMJSON | Модификаторы для передачи в блок [service-icon](../service-icon/service-icon.ru.md), который миксуется к `service__icon`. |

* **С помощью массива элементов** `item`, помещенных в поле `content`. Позволяет самостоятельно настроить все необходимые параметры сервиса. Элемент `item` реализуется блоком [service](../service/service.ru.md).

---
**NB**  Если в BEMJSON-декларации блока есть поле `content`, значение поля `items` игнорируется.

---

```javascript
{
    block: 'services-table',
    items: [
        {service: 'images', serviceIconMods: {color: 56}},
        {service: 'maps', serviceIconMods: {color: 56}}
    ]
}

// Эквивалентно

{
    block: 'services-table',
    content: [
        {
            elem: 'item',
            content: {
                block: 'service',
                service: 'images',
                iconMods: {color: '56'}
            }
        },
        {
            elem: 'item',
            content: {
                block: 'service',
                service: 'maps',
                iconMods: {color: '56'}
            }
        }
    ]
}
```

_При использовании поля `items` подключите его в зависимость._

_Чтобы иконки сервисов отобразились, подключите зависимость от соответствующих элементов блока `service-icon` (в данном случае , `images`, `maps`)._

Блок [service-icon](../service-icon/service-icon.ru.md) требует указания модификатора `_self_40` или `_color_56` для отображения иконки. [Список поддерживаемых иконок для сервисов](../common.blocks/service-icon/service-icon/).

<a name="add-all"></a>
### Добавление псевдокнопки «Все сервисы»

Псевдокнопка «Все сервисы» выполняет переход на региональную страницу [сервисы Яндекса](http://yandex.ru/all), с учетом локализации. В блоке располагается после основного набора сервисов.

Добавляется псевдокнопка одним из следующих способов:

* **C помощью поля `all`**, упрощенная запись элемента `all`. Используется только с [полем items](#custom-set).
* **С помощью элемента `all`**. Используется только в поле `content` совместно с элементами блока `item`. Поле `all` игнорируется.

```javascript
{
    block: 'services-table',
    items: [
        // набор сервисов
    ],
    all: true
}

// Эквивалентно

{
    block: 'services-table',
    content: [
        // набор сервисов
        {
            elem: 'all'
        }
    ]
}
```

_При использовании поля `all` подключите его в зависимость._

<a name="mods"></a>
### Модификаторы блока

<a name="mods-type"></a>
#### Модификатор `type`

Отвечает за выбор готового набора сервисов. По умолчанию каждый набор содержит ссылку на региональную страницу [«Все сервисы»](#add-all).

Способ установки: BEMJSON.

| Допустимые значения | Описание |
| ------------------- | ---------|
| ['ru'](#mods-type-ru)  | Набор сервисов для русскоязычного региона КУБР (домен `ru`): Картинки, Карты, Новости, Почта, Видео, Перевод, Браузер, Афиша, Диск, Маркет, Словари, Музыка, Такси, Авто, Деньги. |
| ['com'](#mods-type-com) | Набор сервисов для англоязычного региона (домен `com`): Картинки, Видео, Почта, Перевод. Можно задать значение HTML-атрибута `target` для URL сервисов Почта и Переводы с помощью поля [prefsTarget](#prefsTarget).|
| ['turkish'](#mods-type-tr) | Набор сервисов для Турции (домен `tr`): Картинки, Карты, Погода, Новости, Почта, Видео, Перевод, Браузер, Маркет, Диск. |
| ['ad'](#mods-type-ad) | Набор рекламных сервисов: Метрика, Реклама, Директ, Вебмастер, Поиск для сайта, Я.Деньги. Для Турции без Рекламы и Я.Денег.|

<a name="mods-type-ru"></a>
Табло для русскоязычного региона (КУБР):

```js
{
    block: 'services-table',
    mods: {type: 'ru'}
}
```

<a name="mods-type-com"></a>
Табло для англоязычного региона:

```js
{
    block: 'services-table',
    mods: {type: 'com'},
    prefsTarget: 'blank'
}
```

<a name="mods-type-tr"></a>
Табло для Турции:

```js
{
    block: 'services-table',
    mods: {type: 'turkish'}
}
```

<a name="mods-type-ad"></a>
Табло с рекламными сервисами:

```js
{
    block: 'services-table',
    mods: {type: 'ad'}
}
```

<a name="mods-size"></a>
#### Модификатор `size`

Задает ширину блока, которая также регулирует и допустимое количество сервисов в строке.

Способ установки: BEMJSON. <br>
Допустимые значения: `s`, `m`, `l`. <br>
Значение  по умолчанию:<br>
* на уровне `desktop`: ширина блока – 800 px, размеры элемента `item` – 160/100px;<br>
* а уровне `touch-pad`: ширина блока – 700 px, размеры элемента `item` – 140/100px.<br>

Размер s:

```js
{
    block: 'services-table',
    mods: {size: 's'},
    items: [
        {service: 'images', serviceIconMods: {color: '56'}},
        {service: 'maps', serviceIconMods: {color: '56'}},
        {service: 'video', serviceIconMods: {color: '56'}},
        {service: 'market', serviceIconMods: {color: '56'}}
    ]
}
```

Размер m:

```js
{
    block: 'services-table',
    mods: {size: 'm'},
    items: [
        {service: 'images', serviceIconMods: {color: 56}},
        {service: 'maps', serviceIconMods: {color: 56}},
        {service: 'video', serviceIconMods: {color: 56}},
        {service: 'market', serviceIconMods: {color: 56}}
    ]
}
```

Размер l:

```js
{
    block: 'services-table',
    mods: {size: 'l'},
    items: [
        {service: 'images', serviceIconMods: {color: 56}},
        {service: 'maps', serviceIconMods: {color: 56}},
        {service: 'video', serviceIconMods: {color: 56}},
        {service: 'market', serviceIconMods: {color: 56}}
    ]
}
```

_При использовании опционального модификатора `size` подключите его в зависимость c нужными значениями._

<a name="fields"></a>
### BEMJSON-поля блока

<a name="fields-prefsTarget"></a>
#### Поле `prefsTarget`

Тип: String. <br>
Значение по умолчанию: –.

Определяет значение HTML-атрибута `target`. Передается в блок [service](../service/service.ru.md) для ссылок сервисов Почта и Перевод.

Используется только в наборе определенном в модификаторе `type` со значением `com`.

```js
{
    block: 'services-table',
    mods: {type: 'com'},
    prefsTarget: 'blank'
}
```

<a name="fields-contentRegion"></a>
#### Поле `contentRegion`

Тип: String. <br>
Значение по умолчанию: берется из параметра `content-region` блока `i-global`.<br>
Если вы намерены передавать значение таким образом, то блок `i-global` нужно
добавить в зависимости самостоятельно.

Используется только в наборе `_type_ad`, чтобы не показывать некоторые сервисы для Турции.

```js
{
    block: 'services-table',
    mods: {type: 'ad'},
    contentRegion: 'tr'
}
```
