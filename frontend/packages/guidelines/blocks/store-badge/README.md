# store-badge

Блок для отображения бейджей сторов мобильных приложений.

### Модификаторы блока

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `name` | `app-store` `google-play` | **Обязательный**. Имя стора приложений |
| `view` | `primary` | Тип отображения |
| `size` | `m` | **Обязательный**. Размер |

```js
{
	block: 'store-badge',
	mods: { name: 'app-store', view: 'primary', size: 'm' } 
}
```

### Добавление иконки

Для того, чтобы добавить новый бейдж, нужно добавить его в директорию `assets/store-badge` с именем `store-badge_name_НАЗВАНИЕ_РАЗМЕР.svg`. При коммите запустится таск `generate:store-badge-config` и иконки автоматически сгенерируются.
