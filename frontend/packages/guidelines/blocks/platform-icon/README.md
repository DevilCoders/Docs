# platform-icon

Блок для отображения иконок платформ, для маркировки карточек и платежных блоков.

### Модификаторы блока

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `name` | `apple-pay` `apple-pay-brand` | **Обязательный**. Название иконки |
| `size` | `m` `l` | **Обязательный**. Размер иконки |
| `view` | `primary` `ghost` | Цвет отображения иконки |

```js
{
	block: 'platform-icon',
	mods: { name: 'twitter-primary', view: 'primary', size: 'm' }
}
```

### Добавление иконки

Для того, чтобы добавить новую иконку, нужно добавить его в директорию `assets/platform-icon` с именем `platform-icon_name_НАЗВАНИЕ_РАЗМЕР.svg`. При коммите запустится таск `generate:platform-icon-config` и `generate:platform-icon-components`, затем иконки автоматически сгенерируются.
