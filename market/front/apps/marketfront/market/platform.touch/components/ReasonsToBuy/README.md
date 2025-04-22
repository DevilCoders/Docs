### Примеры

```jsx

const reasons = [{
     factor_name: 'Довольно-таки неплохо',
     factor_id: 'bla',
     value: 234,
     factor_priority: 1,
     id: 'best_by_factor',
}, {
    factor_name: 'очень приятно',
    factor_id: 'blabla',
    value: 234,
    factor_priority: 1,
    id: 'best_by_factor',
}];
    
<div>
    <ReasonsToBuy reasonsToBuy={reasons} />
</div>
```
