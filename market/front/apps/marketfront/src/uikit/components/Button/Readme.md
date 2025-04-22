### Песочница
```js noeditor
<Helper.Playground
    component={Button}
    settings={{background: 'transparent'}}
    defaultValues={{children: 'беру!'}}
/>
```

Используйте кнопки для отображения различных действий, которые можно активировать с помощью клика или нажатия.

### Параметры

#### `theme`

Стиль кнопки помогает пользователяем идентифицировать статус и важность действия. Для ключевых действий используйте `action`.
Кнопка из состояния `disabled` может стать любой другой, в зависимости от важности действия.

##### `action`
```jsx
<Button theme="action">Action</Button>
```
##### `normal`
```jsx
<Button theme="normal">Normal</Button>
```
##### `pseudo`
```jsx
<Button theme="pseudo">Pseudo</Button>
```
##### `minor`
```jsx
<Button theme="minor">Minor</Button>
```
##### `danger`
```jsx
<Button theme="danger">Danger</Button>
```
##### `primary`
```jsx
<Button theme="primary">Primary</Button>
```
##### `medium`
```jsx
<Button theme="medium">medium</Button>
```

#### `size`

Кнопка может быть разных размеров в зависимости от того, где и в каком контексте вы хотите её использовать. Размеры подобраны для удобного взаимодействия на различных устройствах.

##### `extra large`
```jsx
<Button theme="action" size="xl">Extra large</Button>
```
##### `large`
```jsx
<Button theme="action" size="l">Large</Button>
```
##### `medium`
```jsx
<Button theme="action" size="m">Medium</Button>
```
##### `small`
```jsx
<Button theme="action" size="s">Small</Button>
```
##### `extra small`
```jsx
<Button theme="action" size="xs">Extra small</Button>
```

##### `Все размеры сразу, сплошная кнопка`
```jsx
    <div style={{display: 'flex', 'justify-content': 'flex-start', 'align-items': 'flex-end'}}>
        <div>
            <Button theme="action" size="xl">Extra large</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button theme="action" size="l">Large</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button theme="action" size="m">Medium</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button theme="action" size="s">Small</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button theme="action" size="xs">Extra small</Button>
        </div>
    </div>
```

##### `Все размеры сразу, сплошная кнопка с прелоадером`
```jsx
    <div style={{display: 'flex', 'justify-content': 'flex-start', 'align-items': 'flex-end'}}>
        <div>
            <Button inProgress={true} theme="action" size="xl">Extra large</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button inProgress={true} theme="action" size="l">Large</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button inProgress={true} theme="action" size="m">Medium</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button inProgress={true} theme="action" size="s">Small</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button inProgress={true} theme="action" size="xs">Extra small</Button>
        </div>
    </div>
```


##### `Все размеры сразу, кнопка с бордером`
```jsx
    <div style={{display: 'flex', 'justify-content': 'flex-start', 'align-items': 'flex-end'}}>
        <div>
            <Button theme="minor" size="xl">Extra large</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button theme="minor" size="l">Large</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button theme="minor" size="m">Medium</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button theme="minor" size="s">Small</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button theme="minor" size="xs">Extra small</Button>
        </div>
    </div>
```


##### `Все размеры сразу, кнопка с бордером с прелоадером`
```jsx
    <div style={{display: 'flex', 'justify-content': 'flex-start', 'align-items': 'flex-end'}}>
        <div>
            <Button inProgress={true} theme="minor" size="xl">Extra large</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button inProgress={true} theme="minor" size="l">Large</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button inProgress={true} theme="minor" size="m">Medium</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button inProgress={true} theme="minor" size="s">Small</Button>
        </div>
        <div style={{'margin-left': '10px'}}>
            <Button inProgress={true} theme="minor" size="xs">Extra small</Button>
        </div>
    </div>
```

#### `width`

Ширина кнопки по умолчанию зависит от текста, но ей можно установить фиксированное значение в пикселях. Установив ширину `auto`, кнопка будет занимать всё доступное ей пространство.

##### `100`
```jsx
<Button width="100">Fixed</Button>
```
##### `auto`
```jsx
<Button width="auto">Fullwidth</Button>
```

#### `disabled`
Boolean параметр, который включает неактивное состояние кнопки.
```jsx
<div>
    <Button disabled="true">I'm disabled</Button>
    <Button disabled="true" theme="action">I'm action disabled</Button>
    <Button disabled="true" theme="minor">I'm minor disabled</Button>
    <Button disabled="true" theme="pseudo">I'm pseudo disabled</Button>
    <Button disabled="true" theme="medium">I'm medium disabled</Button>
</div>
```

#### `type`
Тип кнопки как HTML элемента: `button` (по умолчанию), `submit`, `reset`

#### `icon`

```jsx
<Button size="s" icon="attachment">Добавить</Button>
```

```jsx
<Button icon="attachment">Добавить</Button>
```

```jsx
<Button size="l" icon="attachment">Добавить</Button>
```

```jsx
<Button disabled="true" icon="attachment">Добавить</Button>
```

```jsx
<Button width="auto" icon="attachment">Добавить</Button>
```

#### `circle`

```jsx
<div>
    <Button size="xxs" theme="action" circle="arrow-up" />
    <Button size="s" circle="arrow-up" />
    <Button circle="arrow-up" />
    <Button size="l" circle="arrow-up" />
    <Button theme="action" circle="arrow-up" />
    <Button disabled="true" circle="arrow-up" />
    <Button theme="minor" circle="arrow-up" />
    <Button theme="danger" circle="arrow-up" />
    <Button theme="medium" circle="arrow-up" />
</div>
```

#### `pin`

Задает форму кнопке. Используется для группировки с другими блоками.

```jsx
<div>
    <div><Button theme="minor" size="m" pin="round-brick">Кнопка `round-brick`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="brick-round">Кнопка `brick-round`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="brick-round-vertical">Кнопка `brick-round-vertical`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="round-brick-vertical">Кнопка `brick-round-vertical`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="brick-brick">Кнопка `brick-brick`</Button></div>
</div>
```

```jsx
<div>
    <div><Button theme="minor" size="m" pin="round-circle">Кнопка `round-circle`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="circle-round">Кнопка `circle-round`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="round-circle-vertical">Кнопка `round-circle-vertical`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="circle-round-vertical">Кнопка `circle-round-vertical`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="circle-circle">Кнопка `circle-circle`</Button></div>
</div>
```

```jsx
<div>
    <div><Button theme="minor" size="m" pin="round-clear">Кнопка `round-clear`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="clear-round">Кнопка `clear-round`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="round-clear-vertical">Кнопка `round-clear-vertical`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="clear-round-vertical">Кнопка `clear-round-vertical`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="clear-clear">Кнопка `clear-clear`</Button></div>
    <br/>
    <div><Button theme="minor" size="m" pin="clear-clear-vertical">Кнопка `clear-clear-vertical`</Button></div>
</div>
```



В сборе

```jsx
<div>
    <div>
        <Button theme="action" size="m" pin="circle-clear">Левая кнопка</Button>
        <Button theme="minor" size="m" pin="clear-brick">Средняя кнопка</Button>
        <Button theme="minor" size="m" pin="clear-circle">Правая кнопка</Button>
    </div>
    <br/>
    <div>
        <Button theme="minor" size="m" pin="round-clear">Левая кнопка</Button>
        <Button theme="action" size="m" pin="clear-brick">Средняя кнопка</Button>
        <Button theme="minor" size="m" pin="clear-round">Правая кнопка</Button>
    </div>
</div>
```

У псевдо-темы другие размеры (по-размеру иконок)

```jsx
<div>
<Button size="s" theme="pseudo" circle="arrow-up" />
<Button theme="pseudo" circle="arrow-up" />
<Button size="l" theme="pseudo" circle="arrow-up" />
</div>
```
