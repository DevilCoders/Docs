# decorator

Блок для применения внутренних и внешних отступов к любым блокам в разметке.

---
**NB** Для использования только в прототипах!

В продакшен БЭМ-сервисах не используется, потому как блок не представляет собой осмысленной сущности.

Для задания отступов для блоков/элементов в БЭМ-проектах необходимо использовать `margin` и `padding` в стилях блока/элемента и задавать их с помощью `CSS Custom Properties` из блока `theme`.

Так же следует помнить, что стоит избегать `margin` у блоков, расположением одного блока внутри другого блока должен управлять родительский блок, через микс элементов.

```css
.yourblock {
	padding: var(--space-m);
}
```

### Модификаторы блока

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `space-t` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер верхнего паддинга |
| `space-r` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер правого паддинга |
| `space-l` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер левого паддинга |
| `space-b` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер нижнего паддинга |
| `space-v` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер вертикального паддинга |
| `space-h` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер горизонтального паддинга |
| `space-a` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер всех паддингов |
| `indent-t` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер верхнего маржина |
| `indent-r` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер правого маржина |
| `indent-l` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер левого маржина |
| `indent-b` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер нижнего маржина |
| `indent-v` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер вертикального маржина |
| `indent-h` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер горизонтального маржина |
| `indent-a` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` `xxxxxl` `xxxxxxl` | Размер всех маржинов |

```js
{
	block: 'yourblock',
	mix: { block: 'decorator', mods: { 'indent-a': 'l', 'space-a': 's' } }
}
```
