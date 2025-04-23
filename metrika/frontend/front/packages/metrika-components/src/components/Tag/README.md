```(jsx)
    <Tag
        onClick={() => {alert('click')}}
        onRemove={() => {alert('remove')}}
    >
        Установка: от 19 до 25 мар 2018
    </Tag>
```
```(jsx)
    <Tag
        disabled={true}
        onClick={() => {alert('click')}}
        onRemove={() => {alert('remove')}}
    >
        Установка: от 19 до 25 мар 2018
    </Tag>
```
```(jsx)
    <Tag hasClose={false} onClick={() => {alert('click')}}>
        <div style={{
            display: 'inline-block',
            maxWidth: '200px',
            verticalAlign: 'top',
            overflow: 'hidden',            
            textOverflow: 'ellipsis',
            direction: 'rtl',
            textAlign: 'left',
        }}>
            application.attribute1.attribute2.attribute3.attribute4.attribute5
        </div>
    </Tag>
```
```(jsx)
    <Tag
        onClick={() => {alert('click')}}
        onRemove={() => {alert('remove')}}
        hasClose={true}
        selected
    >
        Установка: от 19 до 25 мар 2018
    </Tag>
```
