Поле ввода с кнопкой

Примеры:

```jsx

const applySubmitField = (value) => {
    console.log(value);
}

const cancelSubmitField = () => {
    
}


<div>
    <div style={{width:'300px',marginTop: '50px'}}>
        <SubmitField
            status={'success'}
            label={'Заголовок'}
            value={'Применённое значение'}
            onSubmit={applySubmitField}
            onClear={cancelSubmitField}
        />
    </div>
    
    <br />
    <br />

    <div style={{width:'300px'}}>
        <SubmitField
            status={'error'}
            label={'Поле с ошибкой'}
            message={'Текст ошибки'}
            value={'Значение ошибки'}
            onSubmit={applySubmitField}
            onClear={cancelSubmitField}
        />
    </div>
    
    
    <br />
    <br />
    <div style={{width:'300px'}}>
        <SubmitField
            status={'normal'}
            label={'Загружаемое поле'}
            inProgress={true}
            value={'Поле загружается'}
            onSubmit={applySubmitField}
            onClear={cancelSubmitField}
        />
    </div>

</div>
```
