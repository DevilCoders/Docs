# HitArea
<!-- description:start -->
Компонент для зоны выбора ответа.
<!-- description:end -->

## Свойства
<!-- props:start -->
| Свойство   | Тип                                                             | По умолчанию | Описание                                                                                                                                                                     |
| ---------- | --------------------------------------------------------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| status?    | `"initial" \| "correct" \| "incorrect" \| "accepted"`           | `'initial'`  | Статус зоны выбора. При статусе 'initial' элемент является интерактивным. Остальные статусы являются финальными и убирают возможность взаимодействовать с элементом.         |
| checked?   | `false \| true`                                                 | —            | Проверена ли зона.                                                                                                                                                           |
| disabled?  | `false \| true`                                                 | —            | Отключает интерактивность компонента.                                                                                                                                        |
| readOnly?  | `false \| true`                                                 | —            | Режим просмотра.<br>Компонент не дает изменять значение.                                                                                                                     |
| areaStyles | `{ height: number; width: number; left: number; top: number; }` | —            | Стили для зоны, определяют ее: _ `width` - ширину _ `height` - высоту _ `top` - расстояние от верхней границы изображения _ `left` - расстояние от левой границы изображения |
| onChange?  | `(event: ChangeEvent<HTMLInputElement>) => void`                | —            | Обработчик переключения выбора зоны.                                                                                                                                         |
| value      | `string`                                                        | —            | Значение ответа текущей зоны.                                                                                                                                                |
| className? | `string`                                                        | —            | Дополнительный className.                                                                                                                                                    |
| innerRef?  | `RefObject<HTMLLabelElement>`                                   | —            | Ссылка на корневой DOM-элемент компонента.                                                                                                                                   |
| style?     | `CSSProperties`                                                 | —            | Стили зоны выбора ответа.                                                                                                                                                    |
<!-- props:end -->

<!-- modifiers:start -->
### flavor

Отвечает за стилевое оформление зоны варианта.

#### banana

{{%story::desktop:edu-components-hitarea-banana--states%}}

#### blueberry

{{%story::desktop:edu-components-hitarea-blueberry--states%}}

**Допустимые значения:** `"banana"`, `"blueberry"`.

### hasBadge

Задает зоне значок статуса. В качестве значка по-умолчанию ставится компонент [StatusBadge](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/StatusBadge).

| Свойство        | Тип                                                                        | По умолчанию | Описание                      |
| --------------- | -------------------------------------------------------------------------- | ------------ | ----------------------------- |
| hasBadge?       | `false \| true`                                                            | —            | Наличие значка статуса.       |
| badgeAlignment? | `"top-right" \| "bottom-right" \| "center" \| "top-left" \| "bottom-left"` | `'top-left'` | Расположение значка статуса.  |
| badgeOffset?    | `number`                                                                   | `8`          | Отступ значка от границ зоны. |
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/HitArea)
