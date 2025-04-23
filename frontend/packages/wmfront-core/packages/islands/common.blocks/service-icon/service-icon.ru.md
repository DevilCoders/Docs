# service-icon
Блок `service-icon` c иконками сервисов в разных форматах (SVG, PNG) и размерах. 
Включает в себя черно-белые и цветные иконки сервисов, которые используются, например, в левой
навигационной панели и табло сервисов.

Чтобы на черно-белые иконки можно было наложить `.service_hoverable_yes` с фильтром, их нужно сохранять в 8-битном формате.

## Обзор
### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | --------------------- | -------- |
| [self](#mods-type)  | `40` | BEMJSON | Черно-белые иконки сервисов размером `40x40` px.  |
| [color](#mods-size) | `56` | BEMJSON | Цветные иконки сервисов размером `56x56`px.  |

### Элементы блока
Элементом блока является строковый ID сервиса в Лего (из блока [i-services](../i-services/__uri/i-services__uri.bemhtml.js)). [Список элементов блока](../common.blocks/service-icon/).


```js
{
    block: 'service-icon',
    content: [
        {
            elem: 'afisha',
            elemMods: {color: 56}
        },
        {
             elem: 'auto',
             elemMods: {color: 56}
        },
        {
            elem: 'avia',
            elemMods: {color: 56}
        },
        {
            elem: 'browser',
            elemMods: {color: 56}
        }
    ]
}
```

```js
{
    block: 'service-icon',
    content: [
        {
             elem: 'afisha',
             elemMods: {self: 40}
        },
        {
              elem: 'appsearch',
              elemMods: {self: 40}
        },
        {
            elem: 'auto',
            elemMods: {self: 40}
        },
        {
            elem: 'avia',
            elemMods: {self: 40}
        }
    ]
}        
```