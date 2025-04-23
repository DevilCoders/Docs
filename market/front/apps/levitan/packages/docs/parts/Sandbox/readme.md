В этой песочнице можно использовать все доступные компоненты из `b2b` и `market`.

При изменении кода обновляется ссылка, которой можно поделиться.

Для использования компонентов из **@yandex-levitan/b2b**:

```js
const {Button, TextField} = await resolve('@yandex-levitan/b2b');
```

Для **@yandex-levitan/market**:

```js
const {Button} = await resolve('@yandex-levitan/market');
```

Можно также импортировать регистры с версиями компонентов `@version` с помощью функции `versions`:

```js
const registry = await versions(
    '@yandex-levitan/b2b/@deprecated',
    {Button, Checkbox}
);

const {[Checkbox]: CheckboxDeprecated} = await versions(
    '@yandex-levitan/b2b/@deprecated',
    {Checkbox}
);
```

Также доступны стандартные реакт-хуки, а также `styled` и `css` функции из [reshadow](https://github.com/lttb/reshadow) для стилизации.

> К сожалению, на данный момент tagged template literals в MDX не доступны
>
> @see [Improve JSX block parsing](https://github.com/mdx-js/mdx/issues/195)

Например:

```js
const styles = css(`
    container { color: red }
`)

return styled(styles)(
    <container>content</container>
)
```
