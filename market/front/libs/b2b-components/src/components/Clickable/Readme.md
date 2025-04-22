Компонент стоит использовать во всех случаях, когда по клику пользователь не переходит на другую страницу.

```jsx
const {close} = require('../Icon');
const AlmostLink = () => (
    <Clickable
        variant="link"
        title="Нажми, ради бога"
        onClick={() => alert('Спасибо что нажали')}
    >
        нажми меня
    </Clickable>
);

const IconWithClick = () => (
    <div style={{position: 'absolute', top: '5px', right: '5px'}}>
        <Clickable title="Удивительно, да?" onClick={() => alert('Круто ты кликаешь!')}>
            <Icon src={close} />
        </Clickable>
    </div>
);

<div style={{padding: '20px', border: '1px solid #333', position: 'relative'}}>
    <Paragraph>Компонент может принимать облик обычной ссылки - <AlmostLink />, это ли не здорово?</Paragraph>

    <Paragraph>Но и это еще не все, если вы используете что-то, на что можно нажать, как крестик в верхнем - правом углу, то это тоже должен быть <code style={{fontSize: 'initial', lineHeight: 'initial'}}>{'<Clickable />'}</code>. По умолчанию не имеет отступов, фона, обводки и других свойств. Но загорается при фокусировании и меняет курсор при наведении.</Paragraph>
    <IconWithClick />
</div>
```
