# suggest2-view

Вспомогательный блок `suggest2-view` обеспечивает представление [подсказок саджеста](../suggest2/suggest2.ru.md), переданных из блока [suggest2-model](../suggest2-model/suggest2-model.ru.md) (модели).

Блок получает данные от сервера в JSON-формате и динамически формирует на их основе BEMJSON (структуру верстки), который затем шаблонизирует в HTML-строку. В браузере такая строка будет представлена в виде списка подсказок.

## Обзор

<a name="mods"></a>
### Модификаторы блока

| Модификатор              | Допустимые значения        | Способы установки | Описание |
| ------------------------ | -------------------------- | ------------------| ---------|
| [theme](#mods-theme)     | `normal`, `large`, `flow`  | [initView](#method)| BEMJSON-представление для стилевого оформления саджеста. Значение по умолчанию: `normal` (выставляется из [suggest2](../suggest2/suggest2.ru.md)).|
|[simple](#mods-simple)    | `yes`                      | [initView](#metod) | Финальный BEMJSON для формирования подсказок типа `fact`, `nav`, `traffic`, `weather`,`icon`.
|[advanced](#mods-advanced)| `yes`                      | [initView](#method) | Финальный BEMJSON для формирования подсказок типа `bemjson` и `html`.|
| [group](#mods-group)     | `label`, `type`            | [initView](#method) | Группировка подсказок. Используется совместно с [модификатором theme в значении normal и large](#mods-theme). Значение по умолчанию: `type`. Доступен на deskpad-уровне. |

<a name="method"></a>
**NB** **Способ установки**
Задать нужные значения [модификаторам](#mods) блока `suggest2-view`, можно только пере- или доопределив их в protected-методе [initView](https://github.yandex-team.ru/lego/islands/tree/dev/common.blocks/suggest2/suggest2.js#L232) (инициализирует блок `suggest2-view`) блока [suggest2](../suggest2/suggest2.ru.md) на проектном уровне.


## Подробнее

<a name="mods-theme"></a>
### Модификатор `theme`

<!--- `flow` - `touch-phone`-конструктор BEMJSON-представления для пословного саджеста.B-->

Формирует BEMJSON-представление, которое добавляет особенности для стилевого оформления саджеста.

Способ установки: [initView](#metod).<br>

| Допустимые значения | Описание                           |
| ------------------- | ---------------------------------- |
| `normal`            | Значение по умолчанию. BEMJSON-представление для обычного саджеста. Выставляется из [suggest2](../suggest2/suggest2.ru.md). |
| `large`             | BEMJSON-представление для саджеста, тянущегося на всю ширину страницы. |
| `flow`              | BEMJSON-представление для пословного саджеста. Уровень переопределения: `touch-phone`. Не используется совместно с [модификатором group](#mods-group). |


<a name="mods-simple"></a>
### Модификатор `simple`

Преобразует данные сокращенного [ответа сервера](https://beta.wiki.yandex-team.ru/YandexMobile/Browser/Product/suggest/SuggestStructure/#otvet) в BEMJSON, на основе которого [suggest2](../suggest2/suggest2.ru.md) сформирует подсказки типа `fact`, `nav`, `traffic`, `weather`, `icon`.
Подробное описание [типов подсказок](../suggest2/suggest2.ru.md#mods-type).

Выставляется автоматически при выставлении [модификатора type в значение simple](../suggest2/suggest2.ru.md#mods-type) блока `suggest2`.

Способ установки: [initView](#method).<br>
Допустимое значение: `yes`.

<a name="mods-advanced"></a>
### Модификатор `advanced`

Преобразует данные расширенного [ответа сервера](https://beta.wiki.yandex-team.ru/YandexMobile/Browser/Product/suggest/SuggestStructure/#otvet) в BEMJSON, на основе которых [suggest2](../suggest2/suggest2.ru.md) сформирует подсказки типа `bemjson` и `html`. Подробное описание [типов подсказок](../suggest2/suggest2.ru.md#mods-type).

Выставляется автоматически при выставлении [модификатора type в значение advanced](../suggest2/suggest2.ru.md#mods-type) блока `suggest2`.

Способ установки: [initView](#method).<br>
Допустимое значение: `yes`.


> **NB**  В случае, выставления [модификатора type в значение all](../suggest2/suggest2.ru.md#mods-type) блока `suggest2` модификаторы [simple](#mods-simple) и [advanced](#mods-advanced) будут выставлены одновременно, при этом дополняя друг друга.

> Если модификатор `type` блока `suggest2` не выставлен, отобразятся обычные текстовые подсказки, без типа.

<a name="mods-theme"></a>
### Модификатор `group`

Определяет способ группировки подсказок саджеста.

Способ установки: [initView](#method).<br>
Значение по умолчанию: `type`.<br>
Уровень переопределения: `deskpad`.

| Допустимые значения | Описание |
| ------------------- | ---------|
| `type`              | Группировка подсказок по [типу](https://beta.wiki.yandex-team.ru/serp/suggest/html-items/#avtodopolneniedljatachejjtapaxed). |
| `label`             | Группировка подсказок по сервисам. |
