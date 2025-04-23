Стандартный вид компонента.

```jsx
const {pictures} = require('./__spec__/index.mock.js');

<OfferCondition
    type='like-new'
    reason='Нет зарядки и не совпадает IMEI'
    pictures={pictures}
    size='m' 
/>
```

С несколькими фотографиями.

```jsx
const {pictures} = require('./__spec__/index.mock.js');

<OfferCondition
    type='previously-used'
    reason='Коробка помялась, кабель пожевала собака на складе'
    pictures={pictures}
    maxPicturesCount={2}
    size='m' 
/>
```

Длинное описание обрезается.

```jsx
const {pictures} = require('./__spec__/index.mock.js');

<div style={{width: '250px'}}>
    <OfferCondition
        type='previously-used'
        reason='Коробка помялась, кабель пожевала собака на складе'
        pictures={pictures}
        size='m' 
    />
</div>
```
