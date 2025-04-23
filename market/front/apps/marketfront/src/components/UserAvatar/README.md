### Компонент аватарки юзера

### Песочница
```js noeditor
const src = helper.generateImage({
    w: 64,
    h: 64,
    text: 'Ю',
});

<Helper.Playground
    component={UserAvatar}
    defaultValues={{
        src,
    }}
/>
```

### rounded

```jsx

const src = helper.generateImage({
    w: 64,
    h: 64,
    text: 'А',
});

<div>
    <div style={{padding: 20, display: 'inlineBlock'}}>
        <UserAvatar src={src} round={false} />
    </div>

    <br/>

    <div style={{padding: 20, display: 'inlineBlock'}}>
        <UserAvatar src={src} round />
     </div>
</div>

```
