<a name="module_f-problem-assign"></a>

## f-problem-assign ⇐ <code>BEM.DOM</code>
Задать задачу

**Extends**: <code>BEM.DOM</code>  
**Author**: ertema  
**Example**  
```js
{
    block: 'f-problem-assignment',
    data: {…} // Problem,
    mod: {
        assignee: 'preset'
    }
    js: {
        model: {…} // Problem
    }
}
```

* [f-problem-assign](#module_f-problem-assign) ⇐ <code>BEM.DOM</code>
    * [`~_cancelChanges()`](#module_f-problem-assign.._cancelChanges)
    * [`"assign" (model)`](#event_assign)
    * [`"unassign" (model)`](#event_unassign)

<a name="module_f-problem-assign.._cancelChanges"></a>

### `f-problem-assign~\_cancelChanges()`
Отмена изменений из-за ошибки

**Kind**: inner method of [<code>f-problem-assign</code>](#module_f-problem-assign)  
<a name="event_assign"></a>

### `"assign" (model)`
Задать задачу

**Kind**: event emitted by [<code>f-problem-assign</code>](#module_f-problem-assign)  

| Param | Type |
| --- | --- |
| model | <code>Problem</code> | 

<a name="event_unassign"></a>

### `"unassign" (model)`
Убрать задачу

**Kind**: event emitted by [<code>f-problem-assign</code>](#module_f-problem-assign)  

| Param | Type |
| --- | --- |
| model | <code>Problem</code> | 

