### Песочница
```js noeditor
<Helper.Playground
    component={DiscountBadge}
    defaultValues={{percent: 7}}
/>
```

### Примеры
##### Обычная тема 
```jsx
<div style={{display: 'flex'}}>
    <div>
        <DiscountBadge percent='7' size='l'/>
        <DiscountBadge percent='10' size='l'/>
        <DiscountBadge percent='21' size='l'/>
        <DiscountBadge percent='32' size='l'/>
        <DiscountBadge percent='43' size='l'/>
        <DiscountBadge percent='54' size='l'/>
        <DiscountBadge percent='65' size='l'/>
        <DiscountBadge percent='76' size='l'/>
        <DiscountBadge percent='87' size='l'/>
        <DiscountBadge percent='98' size='l'/>
    </div>
    <div style={{marginLeft: '30px'}}>
        <DiscountBadge percent='7' size='s'/>
        <DiscountBadge percent='10' size='s'/>
        <DiscountBadge percent='21' size='s'/>
        <DiscountBadge percent='32' size='s'/>
        <DiscountBadge percent='43' size='s'/>
        <DiscountBadge percent='54' size='s'/>
        <DiscountBadge percent='65' size='s'/>
        <DiscountBadge percent='76' size='s'/>
        <DiscountBadge percent='87' size='s'/>
        <DiscountBadge percent='98' size='s'/>
    </div>
</div>
```

##### Акционная тема

```jsx
<div style={{display: 'flex'}}>
    <div>
        <DiscountBadge percent='7' size='l' theme='black'/>
        <DiscountBadge percent='10' size='l' theme='black'/>
        <DiscountBadge percent='21' size='l' theme='black'/>
        <DiscountBadge percent='32' size='l' theme='black'/>
        <DiscountBadge percent='43' size='l' theme='black'/>
        <DiscountBadge percent='54' size='l' theme='black'/>
        <DiscountBadge percent='65' size='l' theme='black'/>
        <DiscountBadge percent='76' size='l' theme='black'/>
        <DiscountBadge percent='87' size='l' theme='black'/>
        <DiscountBadge percent='98' size='l' theme='black'/>
    </div>
    <div style={{marginLeft: '30px'}}>
        <DiscountBadge percent='7' size='s' theme='black'/>
        <DiscountBadge percent='10' size='s' theme='black'/>
        <DiscountBadge percent='21' size='s' theme='black'/>
        <DiscountBadge percent='32' size='s' theme='black'/>
        <DiscountBadge percent='43' size='s' theme='black'/>
        <DiscountBadge percent='54' size='s' theme='black'/>
        <DiscountBadge percent='65' size='s' theme='black'/>
        <DiscountBadge percent='76' size='s' theme='black'/>
        <DiscountBadge percent='87' size='s' theme='black'/>
        <DiscountBadge percent='98' size='s' theme='black'/>
    </div>
</div>

```
