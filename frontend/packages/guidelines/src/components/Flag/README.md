Компонент для отображения флагов различных стран.

### Свойства компонента Flag

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `name` | `blr` `chn` `eur` `gbr` `kaz` `rus` `usa` | Имя флага |
| `size` | `s` `m` | Размер |
| `form` | `round` | Форма |

```jsx
<div>
	<Flag name='usa' size='s' />
	<Flag name='rus' size='m' />
</div>
```

```jsx
<div>
	<Flag name='kaz' size='m' form='round' />
</div>
```

### Добавление флага

Для того, чтобы добавить флаг, нужно добавить файлы `flag_name_НАЗВАНИЕ.post.css` и `flag_name_НАЗВАНИЕ.svg` в директорию `common.blocks/flag/_name`. При коммите запустится таск `generate:flag-config`.


#### Список всех флагов
```js noeditor
const AllFlags = require('../../styleguide/components/AllFlags').default;

<AllFlags />
```
