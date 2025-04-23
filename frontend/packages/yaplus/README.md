# yaplus

Промо-блок для Яндекс.Плюс.
Представляет собой ссылку, которая, в зависимости от состояния аккаунта (подключен или не подключен Яндекс.Плюс) ведет соответственно либо в пользовательские настройки, либо на страницу Я.Плюс.

Если Яндекс.Плюс не подключен (то есть при наличии модификатора `_available_yes`), блок дополняется промо-тултипом.

<a name="mods"></a>
### Модификаторы блока

|Модификатор | Допустимые значения | Способы установки | Описание |
| -----------| --------------------| ------------------| ---------|
| available | `yes` | BEMJSON | Отсутствие подписки Яндекс.Плюс |

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| headerText | `String` | Заголовок текста внутри тултипа. |
| mainDescription | `String` | Основной текст внутри тултипа. |
| leftButtonText | `String` | Текст левой кнопки внутри тултипа. |
| rigntButtonText | `String` | Текст правой кнопки внутри тултипа. |
| enableText | `String` | Текст подписи к ссылке (для deskpad). |
| plusLinkParams | `String` | Параметры, которые нужно прибавить к ссылке, ведущей на страницу Яндекс.Плюс (для состояния `_available_yes`). Например, '?param=value&param1=value1' |
| zIndexGroupLevel | `Number` | `zIndexGroupLevel` для `tooltip`. |

### Использование с `lego-on-react`

Если вы используете версию `lego-on-react` 1.x, вам необходимо подключить следующие стили:

```
require('lego-on-react/src/components/link/link.css');
require('lego-on-react/src/components/button/button.css');
require('lego-on-react/src/components/tooltip/tooltip.css');
```

Это объясняется особенностями сборки разных версий `lego-on-react`. Подробнее в [задаче](https://st.yandex-team.ru/ISL-4977).

Если вам нужна сборка для `touch-phone`, необходимо подключить из пакета соответствующие стили:

```
require('yaplus/src/levels/touch-phone.blocks/yaplus/__link/yaplus__link.css');
require('yaplus/src/levels/touch-phone.blocks/yaplus/__badge/yaplus__badge.css');
require('yaplus/src/levels/touch-phone.blocks/yaplus/_available/yaplus_available_yes.css');
```

## Подробнее

<a name="Объявление-блока-на-странице"></a>
### Объявление блока на странице

Яндекс.Плюс подключен:

```js
{
    block: 'yaplus',
}
```

Яндекс.Плюс доступен, но не подключен:

```js
{
    block: 'yaplus',
    mods: {available: 'yes'}
}
```
