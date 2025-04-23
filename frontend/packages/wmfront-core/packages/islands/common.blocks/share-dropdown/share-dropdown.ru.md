# share-dropdown

**Статус блока**: **deprecated**

Рекомендуется перейти на использование библиотеки [share2](https://tech.yandex.ru/share/doc/dg/api-docpage/).

Блок `share-dropdown` служит для [блока «Поделиться»](http://api.yandex.ru/share/) БЭМ-оберткой на странице. Реализован блоком [dropdown-menu](../dropdown-menu/dropdown-menu.ru.md). Он состоит из кнопки «Поделиться» (блок `button`) и всплывающего окна (блок `popup`) со списком популярных социальных сервисов.

Текст на кнопке «Поделиться» и названия сервисов постоянны и автоматически локализуются ([Список поддерживаемых локализаций](../common.blocks/share-dropdown/share-dropdown.i18n)). Если язык для текста блока явно не задан, то он будет определен по доменной зоне сайта.

С помощью блока «Поделиться» посетители сайта размещают ссылку на его страницы в коммуникационных сервисах. Ссылки открываются в новом окне, строятся в зависимости от сервиса и различных параметров, могут изменяться динамически. Подробнее блок описан в [Вики](http://wiki.yandex-team.ru/share/) и в [Руководстве разработчика](http://api.yandex.ru/share/doc/dg/concepts/share-button-ov.xml).


## Обзор

### BEMJSON-поля блока

| Поле                             | Тип    | Описание  |
| ---------------------------------| ------ | --------- |
| [buttonMods](#fields-buttonMods) | BEMJSON | Пользовательские модификаторы, передаваемые в блок `button`. Значение по умолчанию `{size: 'm'}`. |
| [share](#fields-share)           | BEMJSON | Параметры, формирующие ссылку c информацией о странице, которой делятся на социальном сервисе. |
| `content`                        | BEMJSON | Содержимое блока со списком социальных сервисов. |


### Элементы блока

| Элемент | Описание |
| ------- | -------- |
| [share-item](#elems-share-item) | Социальный сервис. |


### JS-параметры блока

| Параметр                           | Тип     | Значение по умолчанию | Описание |
| -----------------------------------| ------- | --------------------- | -------- |
| [live](#params-live)               | Boolean | `false`               | Включение отложенной инициализации. |
| [popupParams](#params-popupParams) | BEMJSON | —                     | Пользовательские JS-параметры, передаваемые в блок `popup`. |

## Подробнее

### BEMJSON-поля блока

<a name="fields-buttonMods"></a>
#### Поле `buttonMods`

Определяет модификаторы, пробрасываемые кнопке блока `share-dropdown`.

Тип: BEMJSON.<br>
Значение по умолчанию: `{size: 'm'}`.

Блок с кнопкой по умолчанию

```js
{
    block: 'share-dropdown',
    share: {
        url: 'https://yandex.com/'
    },
    content: [
        {
            elem: 'share-item',
            service: 'facebook'
        },
        {
            elem: 'share-item',
            service: 'pinterest'
        }
    ]
}
```

Блок с заданными значениями модификаторов для кнопки

```js
{
    block: 'share-dropdown',
    buttonMods: {theme: 'pseudo', size: 's'},
    share: {
        url: 'https://yandex.com/'
    },
    content: [
        {
            elem: 'share-item',
            service: 'facebook'
        },
        {
            elem: 'share-item',
            service: 'pinterest'
        }
    ]
}
```

<a name="fields-share"></a>
#### Поле `share`

Определяет параметры, формирующие ссылку с информацией о странице, которой делятся. Информация используется при публикации на сервисе.

Также с помощью параметров можно обновлять кэшированную информацию о странице, которая считывается автоматически (`url`, `title`, `description`, `image`).

Список параметров (все опциональные):

| Параметр      | Тип     | Значение по умолчанию           | Описание            |
| --------------| ------- | ------------------------------- | ------------------- |
| `url`         | String  | `window.location.href`          | URL страницы, которой делятся. |
| `title`       | String  | `document.title`                | Заголовок страницы. |
| `image`       | String  |                                 | Дополнительное изображение для сервисов Facebook, ВКонтакте, Мой Мир и Pinterest. Для Pinterest — обязательный параметр. |
| `description` | String  | Значение метатега `description` | Описание ссылки для Facebook, ВКонтакте, Мой Мир и Живой Журнал. |

Значение для `url` можно задать и в блоке `i-global`:

```javascript
{
    block: 'i-global',
    params: {
        url: '//mysite.com'
    }
}
```

**NB** Параметр `url` в ссылке на `https://tech.yandex.ru/share/` всегда берется из `i-global`.

```js
{
    block: 'share-dropdown',
    share: {
        title: 'Это заголовок страницы (title)',
        description: 'Это описание страницы (description)',
        image: 'https://yastatic.net/lego/_/X31pO5JJJKEifJ7sfvuf3mGeD_8.png'
    },
    content: [
        {
            elem: 'share-item',
            service: 'facebook'
        },
        {
            elem: 'share-item',
            service: 'twitter'
        }
    ]
}
```

### Элементы блока

<a name="elems-share-item"></a>
#### Элемент `share-item`

Определяет сервис для блока «Поделиться».

Сервис добавляется в содержимом блока c помощью BEMJSON-поля элемента `service`. Его значениями являются названия модификаторов элемента `share-item` (идентификаторы сервиса).

Модификаторы элемента:

* `facebook` – Facebook.
* `gplus` – Google+.
* `moimir` – Мой Мир.
* `odnoklassniki` – Одноклассники.
* `pinterest` – Pinterest.
* `twitter` – Twitter.
* `vkontakte` – Vkontakte.


```js
{
    block: 'share-dropdown',
    share: {
        title: 'Это заголовок страницы (title)',
        description: 'Это описание страницы (description)',
        image: 'https://yastatic.net/lego/_/X31pO5JJJKEifJ7sfvuf3mGeD_8.png'
    },
    content: [ // список сервисов
        {
            elem: 'share-item',
            service: 'facebook'
        },
        {
            elem: 'share-item',
            service: 'twitter'
        }
    ]
}
```

Необходимо добавить зависимость в deps.js-файле от нужных модификаторов сервисов (в приведенном выше примере для `facebook` и `twitter`).

```javascript
({
    shouldDeps: [
        {
            elem: 'share-item',
            mods: {
                service: [
                    'facebook',
                    'twitter'
                ]
            }
        }
    ]
});
```

### JS-параметры блока

<a name="params-live"></a>
### Параметр `live`

Отвечает за включение отложенной или live-инициализации блока.

Тип: Boolean.<br>
Значение по умолчанию: `false` (автоматическая инициализация блока при загрузке страницы, то есть при наступлении события `domReady`).

Варианты включения отложенной инициализации:

* **Локально** — для конкретного экземпляра блока `share-dropdown`.<br>
Для этого достаточно во входном BEMJSON блока указать JS-параметр `live` со значением `true`.

```js
{
    block: 'share-dropdown',
    js: {live: true},
    share: {
        url: 'https://yandex.com/'
    },
    content: [
        {
            elem: 'share-item',
            service: 'facebook'
        }
    ]
}
```

* **Глобально** — для всех блоков `share-dropdown` проекта.<br>
В этом случае, на уровне своего проекта нужно доопределить `BEMHTML/BH`-шаблон блока
следующим образом:

**BEMHTML** (`share-dropdown/share-dropdown.bemhtml.js`)

```javascript
block('share-dropdown').js()(function() {
    return this.extend({live: true}, this.ctx.js);
});
```

**BH** (`share-dropdown/share-dropdown.bh.js`)

```javascript
module.exports = function(bh) {
    bh.match('share-dropdown', function(ctx) {
        ctx.js(ctx.extend({live: true}, ctx.js()));
    });
};
```

Все блоки `share-dropdown` проекта станут инициализироваться отложено, кроме блока с явно отключенной live-инициализацией в BEMJSON через JS-параметр `live: false`.


<a name="params-popupParams"></a>
### Параметр `popupParams`

Блок представлен на странице кнопкой с локализованным текстом «Поделиться» и графическим символом «поделиться».
Кнопка (блок [button](../button/button.ru.md)) с обычной темой оформления (модификатор `theme` со значением `normal`) и размером `m` (значение модификатора `size`). При нажатии кнопки всплывает окно (блок [popup](../popup/popup.ru.md)) со списком ссылок с иконками на социальные сети. Иконки – векторные изображения в формате svg и размером 18x18px.

Тип: BEMJSON.

```js
{
    block: 'share-dropdown',
    js: {
        popupParams: {directions: 'right'}
    },
    share: {
        title: 'Это title страницы',
        description: 'Это описание страницы (description)',
        image: 'https://yastatic.net/lego/_/X31pO5JJJKEifJ7sfvuf3mGeD_8.png'
    },
    content: [
        {
            elem: 'share-item',
            service: 'facebook'
        },
        {
            elem: 'share-item',
            service: 'pinterest'
        }
    ]
}
```
