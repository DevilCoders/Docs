# m-popup

Используется в `i-splendid` как обертка над `m-editor-popup`.

Возвращает блок `popup2` с элементом `__data` для вставки контента с помощью блока `i-splendid` и набором кнопок в элементе `__buttons`. Набор кнопок зависит от типа `m-popup`.

| Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- |
| [form](#mods-form) | `'yes'` | `BEMJSON`, `JS` |
| [drafts](#mods-drafts) | `'yes'` | `BEMJSON`, `JS` |
| [editor](#mods-editor) | `'yes'` | `BEMJSON` |

<a name="mods-form"></a>

#### Модификатор `form`

Обертка для `m-editor-popup_form_yes`.
Набор кнопок: "Отмена", "Добавить".
Направления для раскрытия `popup2`: `'bottom-center'`, `'bottom-left'`, `'bottom-right'`.

<a name="mods-editor"></a>

#### Модификатор `editor`

Обертка для `m-editor-popup_editor_yes`.
То же, что и для модификатора `form`, но с другим стилевым оформлением.

<a name="mods-drafts"></a>

#### Модификатор `drafts`

Обертка для `m-editor-popup_drafts_yes`.
Набор кнопок: "Вернуть".
Полный набор направлений для раскрытия `popup2`.

