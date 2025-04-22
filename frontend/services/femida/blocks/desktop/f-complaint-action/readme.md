<a name="module_f-complaint-action"></a>

## f-complaint-action
Действие над жалобой

**Author**: olgakozlova  
**Example**  
```js
// Действие кнопка
{
    block: 'f-complaint-action',
    mods: {
        action: 'resolve' | 'reject',
        disabled: true
    },
    js: {
        complaint_id: 1 // Для resolve и reject обязательно нужно передать id жалобы
    }
}
{
    block: 'f-complaint-action',
    mods: {
        action: 'merge-problems'
        disabled: true
    },
    js: {
        problem_id: 1 // Для merge-problem обязательно нужно передать id задач
        original_problem_id: 1
    }
}
```
