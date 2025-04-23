Карточка является носителем для законченных композиций других элементов — текста, изображений, различных лайоутов и элементов управления.

```
const demoContainerStyles = {
    background: '#f3f2f2',
    padding: '20px'
};

<div style={demoContainerStyles}>
    <Card>
        <div style={{height: '100px'}}></div>
    </Card>
</div>
```
## Параметры

### background
Можно передать параметры для настройки фона через соответствующие параметры: backgroundImage, backgroundSize, backgroundPosition, backgroundColor.

```
<Card backgroundColor="#fc0">
    <div style={{height: '100px'}}></div>
</Card>
```

#### backgroundImage

```
const imageUrl = 'https://goo.gl/peYsaH';
const demoContainerStyles = {
    height: '250px'
};

<Card 
    backgroundImage={imageUrl}
    backgroundPosition="50%"
    backgroundSize="cover"
>
    <div style={demoContainerStyles}></div>
</Card>
```

### elevation
Карточки могут находится на разной высоте от основной поверхности (1 – 4). Например, элементы конкретной страницы обычно находятся на одном уровне, тогда как модальные зоны или навигационные элементы располагаются выше.

```
const demoContainerStyles = {
    background: '#f3f2f2',
    padding: '20px'
};

<div style={demoContainerStyles}>
    <Card elevation="4">
        <div style={{height: '100px'}}></div>
    </Card>
</div>
```

### corners
Определяет скругление углов карточки. Для карточек размер менее половины экрана лучше рекомендуем использовать значение 1, для больших карточек 2. Если карточка располагается в край экрана, то скругление лучше не использовать.

```
const demoContainerStyles = {
    background: '#f3f2f2',
    padding: '20px'
};

<div style={demoContainerStyles}>
    <Card corners="2">
        <div style={{height: '100px'}}></div>
    </Card>
</div>
```

### border
В некоторых случаях используется бордюр вместо параметра  elevation для отделения карточки от фона.

```
const demoContainerStyles = {
    background: '#f3f2f2',
    padding: '20px'
};

<div style={demoContainerStyles}>
    <Card border>
        <div style={{height: '100px'}}></div>
    </Card>
</div>
```
