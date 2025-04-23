### List item checkboxes example:

```jsx
initialState = {one: false, two: true, three: false};
require('./checkbox/list-item-checkbox.styl');
const {default: ListItemCheckbox} = require('./checkbox/list-item-checkbox');

['one', 'two', 'three'].map((item, i) => (
  <ListItemCheckbox key={i} 
                    checked={state[item]} 
                    onChange={(val) => setState({[val]: !state[val]})}>{item}</ListItemCheckbox>
));
```

### List item images example:

```jsx
require('./image/list-item-image.styl');
const {default: ListItemImage} = require('./image/list-item-image');

const src = 'https://jing.yandex-team.ru/files/luchko-a/google-logo.png'
const items = ['title 1', 'title2', 'title 3'];

<div>
  {
    items.map((item, i) => (
      <ListItemImage key={i} src={src}>
        {item}
      </ListItemImage>
    ))
  }
</div>
```
