# uset-hat

Баннер на основе данных из Баннерокрутилки. Встраивается в меню блока `user2`.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [fetch-data](#mods-fetch-data) | `'yes'` | `BEMJSON` | Получение данных на клиенте. |

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [banner](#field-banner) | `Object` | Данные баннера. |
| [counters](#field-counters) | `Object` | Поле для счетчиков. |
| fetchUrl | `String` | Ручка Баннерокрутилки. |
| fetchUrlParams | `Object` | Параметры для ручки Баннерокрутилки. |

<a name="elems"></a>

## Подробное описание

### Логика показа

 Баннер показывается только при открытии блока `user2`. Если запрос завершается в момент, когда `user2` уже открыт – баннер показан не будет. Это осознанное решение, чтобы `user2` не прыгал. (На медленных соединениях это может сильно нарушить пользовательский сценарий).

### Модификаторы блока

<a name="mods-fetch-data"></a>

#### Модификатор `fetch-data`

Отвечает за получение данных на клиенте.
Для корректной работы модификатора необходимо передать поле [`fetchUrl`](#field-fetchUrl).

Допустимые значения: `'yes'`.

Способ установки: `BEMJSON`.

```js
{
    block: 'user-hat',
    mods: {'fetch-data': 'yes'},
    fetchUrl: 'https://yabs.yandex.ru/page/280743',
    fetchUrlParams: {lang: 'ru'}
}
```

### Поля блока

<a name="field-banner"></a>

#### Поле `banner`

Определяет текст, который отображается на кнопке.

Тип: `Object`.

> **Примечание.** В поле `banner` передаются поля, необходимые для формирования баннера. Если используется модификатора `fetch-data`, данные будут получены на клиенте, за исключением поля `urlParams` и `closeButtonMix`.

Поля объекта `banner`:

| Поле | Тип | Описание |
| ---- | --- | -------- |
| `background` | `String` | Ссылка на картинку для фона заднего плана. |
| `closeUrl` | `String` | Ссылка в БК, которую необходимо дернуть при нажатии на кнопку закрытия баннера. |
| `foreground` | `String` | Ссылка на картинку для фона переднего плана. |
| `showUrl` | `String` | Ссылка в БК, которую необходимо дернуть при показе баннера. |
| `title` | `String` | Текст заголовка баннера. |
| `text` | `String` | Текст баннера. |
| `transformOrigin` | `String` | `css`-свойство `transform-origin` для фона заднего плана. |
| `url` | `String` | Ссылка баннера. |
| `urlParams` | `Object` | Параметры для ссылки баннера. |
| `сloseButtonMix` | `String` | `mix` для кнопки закрытия. |

```js
{
    block: 'user-hat',
    banner: {
        background: '/common.blocks/user-hat/user-hat.tests/hermione.blocks/user-hat/user-hat.assets/bg.svg', // eslint-disable-line
        foreground: '/common.blocks/user-hat/user-hat.tests/hermione.blocks/user-hat/user-hat.assets/fg.svg', // eslint-disable-line
        transformOrigin: '84% 65%',
        url: '#',
        urlParams: {
            param: 'value'
        },
        title: 'Будьте в Плюсе',
        text: 'Оформите подписку Плюс и получите больше возможностей в разных сервисах Яндекса'
    }
}
```

<a name="field-banner"></a>

#### Поле `counters`

Принимает счетчики для закрывающей кнопки для клика по баннеру. Допустимые свойства - `banner`, `close-button`.
