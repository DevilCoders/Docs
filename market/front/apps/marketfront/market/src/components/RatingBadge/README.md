### Примеры

```jsx

const ratings = [{
    value: 0,
    text: 'empty'
}, {
    value: '1',
    text: '0 – 1.5'
}, {
    value: '2',
    text: '1.5 – 2.5'
}, {
    value: '3',
    text: '2.5 – 3.5'
}, {
   value: '4',
   text: '3.5 – 4.5'
}, {
   value: '4.5',
}, {
  value: '5',
  text: '4.5 – 5'
}];

<div>
    {ratings.map(({value, text}) => (
        <div style={{marginBottom: '10px', display: 'flex', alignItems: 'center'}}>
            <RatingBadge rating={value}/>

            {text && <div style={{marginLeft: '20px'}}>{text}</div>}
        </div>
    ))}
</div>
```
