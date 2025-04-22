#### Кнопка "свернуть \ развернуть"

Скругленная кнопка, использующаяся для разворачивания расширенных фильтров и "моих поисков"

![button](./button.png)

Может быть использована для отображения значений:

![button-value](./button-value.png)

Является ссылкой при передаче пропа `url` или кнопкой при передаче `onClick`

`type` отвечает за то, будет ли отображаться иконка `v` | `^`

Отображает кастомный элемент справа при наличии пропа `rightElem`

Когда `type == 'collapse'`, проп `label` является строкой для кнопки в развернутом состоянии, а `collapsedLabel` - в свернутом.
Если проп `collapsedLabel` не передан, то для текста кнопки в свернутом состоянии используется `label`

Props:
- url: `string`
- onClick: `function`
- label: `string` - required
- type: `'collapse'` | `'value'` defaults to `'value'`
- collapsed: `boolean`
- collapsedLabel: `string`
- value: `string` | `number` | `element`
- rightElem: `element`
- className: `string` - additional className for `Link` wrapper element


