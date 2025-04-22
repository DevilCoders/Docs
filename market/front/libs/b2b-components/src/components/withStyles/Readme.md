- модификаторы должны именоваться, определяться и использоваться унифицировано
- элементы называются в camelCase
- модификаторы называем как `_modName` (для булевых) и `_modName_modVal` (для значений), для названий используется camelCase
- модификаторы могут быть (и желательно должны быть) абстрактными, используются с элементами через композицию классов. в идеале должны вынесены в абстрактные общие `mods`, и использоваться в компоненте, например, так:
```css
element {
    &._mod_val {
        composes: _mod_val from "mods.css";
    }
}
```
- значение модификатора может быть числом, строкой, булеаном или массивом
- классы можно переопределить через пропсу `styles`
- элемент для рутовой ноды называем `root`
- для переопределения вместо `styles.root` можно использовать `className` (но не вместе)


#### Интерфейс `css`
```js static
css`element1 element2`
css`element1 element2`._({mod1, mod2})
```

#### Стилизация Компонента
```jsx static
import styles from './styles.css'

const Text = ({css, size, theme, children}) => (
  <div className={css`root`}>
    <p className={css`text`._({size, theme})}>{children}</p>
  </div>
)

export default withStyles(styles)(Text)
```

#### Переопределение стилей

```jsx static
<Text size="m" styles={{root: 'mySuperRoot', text: 'myTextClass'}} />

// => <div class="root mySuperRoot"><p class="text _size_m myTextClass" /></div>
```

```jsx noeditor
const {default: withStyles} = require('./')

ctx.withStyles = {
  Text: withStyles({
    root: 'root',
    text: 'text',
    button: 'button',
    _size_m: '_size_m',
    _theme_normal: '_theme_normal',
    _round_left: '_round_left',
    _round_right: '_round_right',
  })(({css, size, theme, round}) => (
    <div>
      <p><b>root</b>: {css`root`}</p>
      <p><b>text</b>: {css`text`._({size, theme})}</p>
      <p><b>button</b>: {css`button`._({round})}</p>
    </div>
  ))
}

null
```

Без модификаторов

```jsx
<ctx.withStyles.Text />
```

С модификаторами `size="m" theme="normal" round={['left', 'right']}`
```jsx
<ctx.withStyles.Text size="m" theme="normal" round={['left', 'right']} />
```

С переопределением `{root: 'myRoot', text: 'myText'}`
```jsx
<ctx.withStyles.Text styles={{root: 'myRoot', text: 'myText'}} />
```

Вместо `styles.root` можно использовать `className`
```jsx
<ctx.withStyles.Text className="myRoot" />
```
