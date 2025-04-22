### Тултип с кнопкой

По умолчанию рисует `InfoOpener` с приаттаченным `Tooltip`


### Песочница
```jsx harmony



<Helper.Playground
    component={TooltipWithOpener}
    props= {{
        position: {
            required: false,
            type: 'enum',
            values: 'top-left,top-center,top-right,right,bottom-left,bottom-center,bottom-right,left'.split(',')
        },
        children: {
            required: false,
            type: 'string',
            values: 'Я тултип с кнопкой!'
        },
        type: {
            required: false,
            type: 'enum',
            values: ['answer', 'info']
        },
        closeOnTooltip: {
            required: false,
            type: 'boolean'
        },  
        isActive: {
            required: false,
            type: 'boolean',
        }
    }}    
/>

```
