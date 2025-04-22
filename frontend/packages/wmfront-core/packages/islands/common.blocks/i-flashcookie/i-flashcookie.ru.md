# i-flashcookie 

Блок-помощник для использования [флэш-куки](http://wiki.yandex-team.ru/JandeksPoisk/IzmerenijaStatistika/FleshKuka).

**Fallback**: У блока есть атрибут `domain`, который нужен для загрузки картинки-fallback в случае, если у пользователя выключен JavaScript. Например, используя значение `ru`, картинка будет загружаться с сервера `.yandex.ru`.

## Модификаторы блока

Модификатор | Описание | Допустимые значения
--- | --- | ---
`autoload` |  Автозагрузка. | `no`: Без автозагрузки. Подразумевается самостоятельный вызов через `Lego.block['i-flashcookie'].load()`.
`type` | Тип. |`iframe`: С созданием `iframe`.<br>`inline`: Встроенная (без создания `iframe`). Работает только для [определённого списка сервисов](http://2-10.lego.yandex-team.ru/blocks-desktop/i-flashcookie/_type/i-flashcookie_type_inline.services.xml).

```javascript
...
{
    block: 'i-flashcookie',
    domain: 'ru',
    mods: { type: 'iframe' }
}
...                
```