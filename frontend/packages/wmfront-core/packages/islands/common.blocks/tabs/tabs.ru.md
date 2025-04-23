# tabs

Блок содержит контролы, для создания вкладок: в виде меню, кнопок. Позволяет реализовать собственный контрол для вкладок нужного вида. 

Для всех реализаций контролов блок предоставляет унифицированный API (JS и BEMJSON), что обеспечивает удобный переход с одной реализации на другую, без переписывания кода.


## Обзор

[Реализация собственного контрола вкладок](#custom-tabs)

### Модификаторы блока

| Модификатор              | Допустимые значения | Способы установки | Описание             |
| ------------------------ | --------------------| ------------------| -------------------- |
| [control](#mods-control) | `menu`, `buttons`   | BEMJSON           | Тип вкладок.


### BEMJSON-поля блока

| Поле                                           | Тип      | Описание                       |
| ---------------------------------------------- | -------- | ------------------------------ |
| [panes](#tabs-panes)                                          | String   | Строковый идентификатор, для связи `tabs` и [tabs-panes](../tabs-panes/tabs-panes.ru.md). |


### Элементы блока

| Элемент           | Описание  |
| ----------------- | --------- |
| `tab`             | Вкладка.  |  

#### Модификаторы элемента

| Модификатор              | Допустимые значения | Способы установки | Описание             |
| ------------------------ | --------------------| ------------------| -------------------- |
| `active`                 | `yes`               | BEMJSON, JS       | Активная вкладка.    |
| `disabled`               | `yes`               | BEMJSON, JS       | Не доступная вкладка.|



## Подробнее

### Модификаторы блока

<a name="mods-control"></a>
#### Модификатор `control`

Задает тип вкладок.

Способ установки: BEMJSON. <br>

| Допустимые значения | Описание                                                     |
| ------------------- | ------------------------------------------------------------ |
| `menu`              | Вкладки в виде меню, реализованы на основе блока [tabs-menu](../tabs-menu/tabs-menu.ru.md). Содержимое блока `tabs` передается в `соntent` блока `tabs-menu`. При этом все элементы и модификаторы будут находиться в контексте `tabs-menu`, а не `tabs`.<br> **NB** Для блока `tabs-menu` нужно самостоятельно передать модификаторы `size`, `theme` и `layout` и добавить их зависимости.
| `buttons`           | Вкладки в виде кнопок-переключателей, реализованы на основе блока [rudio-button](../radio-button/radio-button.ru.md). Содержимое элементов `tab` преобразуется в элементы `radio` блока `radio-button`. В контексте элементов `tab` можно передать любые параметры, специфичные для `radio`. По умолчанию для `value` радиокнопки выставляется его порядковый номер (начиная с 0). Также в BEMJSON блока `tabs` можно передать `name` для `radio-button`, иначе он будет сгенерирован автоматически.<br> **NB** Для блока `radio-button` нужно самостоятельно передать модификаторы `size`, `theme` и добавить их в зависимости.


```js
[
    {
        block: 'tabs',
        mods: {control: 'menu', size: 'm', theme: 'normal', layout: 'horiz'},
        panes: 'oh-my-tabs',
        content: [
            {elem: 'tab', content: 'Tab 1', elemMods: {active: 'yes'}},
            {elem: 'tab', content: 'Tab 2'},
            {elem: 'tab', content: 'Tab 3', elemMods: {disabled: 'yes'}},
            {elem: 'tab', content: 'Tab 4'}
        ]
    },
    {
        block: 'tabs-panes',
        id: 'oh-my-tabs',
        content: [
            {elem: 'pane', content: 'Pane 1', elemMods: {active: 'yes'}},
            {elem: 'pane', content: 'Pane 2'},
            {elem: 'pane', content: 'Pane 3'},
            {elem: 'pane', content: 'Pane 4'}
        ]
    },

    {
        block: 'x-deps',
        content: {block: 'tabs-menu', mods: {theme: 'normal', size: 'm', layout: 'horiz'}}
    }
]
```

```js
[
    {
        block: 'tabs',
        panes: 'oh-my-tabs',
        mods: {control: 'buttons', size: 'm'},
        content: [
            {elem: 'tab', content: 'Tab 1', elemMods: {active: 'yes'}},
            {elem: 'tab', content: 'Tab 2'},
            {elem: 'tab', content: 'Tab 3', elemMods: {disabled: 'yes'}},
            {elem: 'tab', content: 'Tab 4'}
        ]
    },
    {
        block: 'tabs-panes',
        id: 'oh-my-tabs',
        content: [
            {elem: 'pane', content: 'Pane 1', elemMods: {active: 'yes'}},
            {elem: 'pane', content: 'Pane 2'},
            {elem: 'pane', content: 'Pane 3'},
            {elem: 'pane', content: 'Pane 4'}
        ]
    },

    {
        block: 'x-deps',
        content: {block: 'radio-button', mods: {theme: 'normal', size: 'm'}}
    }
]
```

### BEMJSON-поля блока

<a name="fields-panes"></a>
#### Поле `panes`

Тип: String.

Используется для взаимосвязи `tabs` и блока `tabs-panes`. Чтобы `tabs-panes` переключал панели вкладок в зависимости от активного `tabs`, значения поля `panes` и `id` (блока `tabs-panes`) должны совпадать.

[tabs-panes](../tabs-panes/tabs-panes.ru.md) — панель для вкладок. Эта функциональность была вынесена в отдельный блок для удобства верстки, чтобы можно было разнести по разным DOM-узлам контрол и панель вкладок. 

```javascript
{
    block: 'tabs',
    panes: 'oh-my-tabs-id'
    // ...
},
{
    block: 'tabs-panes',
    id: 'oh-my-tabs-id'
    // ...
},
```

В BEMHTML эти поля раскрываются в примешивание блока `tabs-panes` со связью через одинаковые `id` в поле `js`. Подробнее можно посмотреть в примерах.



<a name="custom-name"></a>
### Реализация собственного контрола вкладок

Чтобы создать свой контрол вкладок, нужно добавить значение для модификатора `control` и реализовать для него:

* BEMHTML/BH шаблоны с преобразованием исходного универсального BEMJSON в необходимый, для желаемого контрола.
* JavaScript с определенным API (пример заглушки в [tabs.js](https://github.yandex-team.ru/lego/islands/blob/dev/common.blocks/tabs/tabs.js)).

