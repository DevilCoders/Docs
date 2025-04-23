## Overview

Уменьшенная версия изображения, используется в интерфейсах для отображения медиа контента
(фотографии, постеры, товары). [Примеры](#Thumbs).

По умолчанию **Thumb** ведет себя как изображение, если задать `ratio`, то компонент растянется на ширину контейнера,
но можно ограничить ширину установив параметр `width` или `height` (в это случае `width` будет расчитан в зависимости от
`height` и `ratio`)


## Props

### `ratio`

#### `ratio='original'` (default)

Оригинальные пропорции изображения. По ширине колонок. (`fit='cover'` будет равносилен `fit='contain'`, т.к.
пропорции оригинальные и изображение помещается целиком)

```jsx
<div>
    <Thumb src={helper.generateImage({w: 100, h: 200})} ratio='original'/>
    {' '}
    <Thumb src={helper.generateImage({w: 100, h: 100})} ratio='original'/>
    {' '}
    <Thumb src={helper.generateImage({w: 200, h: 75, text: '200x75 contain'})} ratio='original'/>
    {' '}
    <Thumb src={helper.generateImage({w: 200, h: 75, text: '200x75 cover'})} ratio='original' fit='cover'/>
</div>
```

В сетке. Изображения имеют оригинальные пропорции, но при этом умещаются в ширину колонки.

```jsx
<Helper.Thumbs n='6' rows={[
    [
        <Thumb src={helper.generateImage({w: 200, h: 300})} ratio='original'/>,
        <Thumb src={helper.generateImage({w: 200, h: 200})} ratio='original'/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} ratio='original'/>,
        <Thumb src={helper.generateImage({w: 300, h: 100})} ratio='original'/>,
        <Thumb src={helper.generateImage({w: 300, h: 300})} ratio='original'/>,
        <Thumb src={helper.generateImage({w: 100, h: 300})} ratio='original'/>,
    ],
]}/>
```


#### `ratio={[1, 1]}`

```jsx
<Helper.Thumbs n='6' contrastBg rows={[
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} ratio={[1, 1]}/>,
        <Thumb src={helper.generateImage({w: 100, h: 100})} ratio={[1, 1]}/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} ratio={[1, 1]}/>,
        <Thumb src={helper.generateImage({w: 100, h: 300})} ratio={[1, 1]}/>,
        <Thumb src={helper.generateImage({w: 300, h: 100})} ratio={[1, 1]}/>,
        <Thumb src={helper.generateImage({w: 300, h: 300})} ratio={[1, 1]}/>,
    ],
]}/>
```


#### `ratio={[3, 4]}`

```jsx
<Helper.Thumbs n='6' contrastBg rows={[
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} ratio={[3, 4]}/>,
        <Thumb src={helper.generateImage({w: 100, h: 100})} ratio={[3, 4]}/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} ratio={[3, 4]}/>,
        <Thumb src={helper.generateImage({w: 100, h: 300})} ratio={[3, 4]}/>,
        <Thumb src={helper.generateImage({w: 300, h: 100})} ratio={[3, 4]}/>,
        <Thumb src={helper.generateImage({w: 300, h: 300})} ratio={[3, 4]}/>,
    ],
]}/>
```


#### `ratio={[4, 3]}`

```jsx
<Helper.Thumbs n='6' contrastBg rows={[
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} ratio={[4, 3]}/>,
        <Thumb src={helper.generateImage({w: 100, h: 100})} ratio={[4, 3]}/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} ratio={[4, 3]}/>,
        <Thumb src={helper.generateImage({w: 100, h: 300})} ratio={[4, 3]}/>,
        <Thumb src={helper.generateImage({w: 300, h: 100})} ratio={[4, 3]}/>,
        <Thumb src={helper.generateImage({w: 300, h: 300})} ratio={[4, 3]}/>,
    ],
]}/>
```


### `fit`

#### `fit=contain` (default)

```jsx
<Helper.Thumbs n='6' contrastBg rows={[
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} ratio={[3, 4]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 100, h: 100})} ratio={[3, 4]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} ratio={[3, 4]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 100, h: 300})} ratio={[3, 4]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 300, h: 100})} ratio={[3, 4]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 300, h: 300})} ratio={[3, 4]} fit='contain'/>,
    ],
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} ratio={[1, 1]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 100, h: 100})} ratio={[1, 1]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} ratio={[1, 1]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 100, h: 300})} ratio={[1, 1]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 300, h: 100})} ratio={[1, 1]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 300, h: 300})} ratio={[1, 1]} fit='contain'/>,
    ],
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} ratio={[4, 3]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 100, h: 100})} ratio={[4, 3]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} ratio={[4, 3]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 100, h: 300})} ratio={[4, 3]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 300, h: 100})} ratio={[4, 3]} fit='contain'/>,
        <Thumb src={helper.generateImage({w: 300, h: 300})} ratio={[4, 3]} fit='contain'/>,
    ],
]}/>
```


#### `fit='cover'`

Имеет смысл указывать, если задан параметр `ratio` или задан один из параметров размера (`width`/`height`).
- ratio: Изображение полностью заполняет заданную область и при необходимости растягивается.
- width/height: изображение зафиксирует одну из величин и примет оригинальные пропорции

```jsx
const {$green600} = require('@self/root/src/uikit/palette/colors');

const containerStyles = {
    width: 300,
    height: 100,
    border: '1px solid',
    borderColor: $green600,
    position: 'relative',
};

<Helper.Thumbs n='6' rows={[
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} ratio={[3, 4]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 100, h: 100})} ratio={[3, 4]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} ratio={[3, 4]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 100, h: 300})} ratio={[3, 4]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 300, h: 100})} ratio={[3, 4]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 300, h: 300})} ratio={[3, 4]} fit='cover'/>,
    ],
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} ratio={[1, 1]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 100, h: 100})} ratio={[1, 1]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} ratio={[1, 1]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 100, h: 300})} ratio={[1, 1]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 300, h: 100})} ratio={[1, 1]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 300, h: 300})} ratio={[1, 1]} fit='cover'/>,
    ],
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} ratio={[4, 3]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 100, h: 100})} ratio={[4, 3]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} ratio={[4, 3]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 100, h: 300})} ratio={[4, 3]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 300, h: 100})} ratio={[4, 3]} fit='cover'/>,
        <Thumb src={helper.generateImage({w: 300, h: 300})} ratio={[4, 3]} fit='cover'/>,
    ],
    [
        <div style={containerStyles}>
            <Thumb src={helper.generateImage({w: 300, h: 50})} fit='cover' height='100%'/>
        </div>
    ],[
        <div style={containerStyles}>
            <Thumb src={helper.generateImage({w: 300, h: 200})} fit='cover' height='100%'/>
        </div>
    ],[
        <div style={containerStyles}>
            <Thumb src={helper.generateImage({w: 200, h: 50})} fit='cover' width='100%'/>
        </div>
    ],[
        <div style={containerStyles}>
            <Thumb src={helper.generateImage({w: 400, h: 200})} fit='cover' width='100%'/>
        </div>,
    ],
]}/>
```


### `shade`

#### `shade={false}` (default)

```jsx
<Helper.Thumbs n='6' rows={[
    [
        <Thumb src={helper.generateImage({w: 200, h: 200})} shade={false}  width='100%'/>,
        <Thumb src={helper.generateImage({w: 200, h: 200})} shade={false} shape='circle'  width='100%'/>,
    ],
]}/>
```


#### `shade={true}`

```jsx
<Helper.Thumbs n='6' rows={[
    [
        <Thumb src={helper.generateImage({w: 200, h: 200})} shade={true} width='100%'/>,
        <Thumb src={helper.generateImage({w: 200, h: 200})} shade={true} shape='circle' width='100%'/>,
    ],
]}/>
```


### `shape`

#### `shape='rectangle'` (default)

```jsx
<Helper.Thumbs n='9' rows={[
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} shape='rectangle' width='100%'/>,
        <Thumb src={helper.generateImage({w: 200, h: 200})} shape='rectangle' width='100%'/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} shape='rectangle' width='100%'/>,
    ],
]}/>
```


#### `shape='roundRectangle'`

```jsx
<Helper.Thumbs n='9' rows={[
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} shape='roundRectangle' width='100%'/>,
        <Thumb src={helper.generateImage({w: 200, h: 200})} shape='roundRectangle' width='100%'/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} shape='roundRectangle' width='100%'/>,
    ],
]}/>
```


#### `shape='circle'`

Если `shape='circle'`, то `ratio={[1, 1]}` и `fit='cover'`, ширина по колонкам.

```jsx
<Helper.Thumbs n='9' rows={[
    [
        <Thumb src={helper.generateImage({w: 100, h: 200})} shape='circle'/>,
        <Thumb src={helper.generateImage({w: 200, h: 200})} shape='circle'/>,
        <Thumb src={helper.generateImage({w: 200, h: 100})} shape='circle'/>,
    ],
]}/>
```


#### `shape='circle'`, `width={100}`

Фиксированная ширина, без колонок.

```jsx
<div>
    <Thumb src={helper.generateImage({w: 100, h: 200})} shape='circle' width={100}/>
    {' '}
    <Thumb src={helper.generateImage({w: 200, h: 200})} shape='circle' width={100}/>
    {' '}
    <Thumb src={helper.generateImage({w: 100, h: 200})} shape='circle' width={100}/>
</div>
```


### `width`

#### `width={undefined}`, (default)

Изображение отображается реального размера, если `ratio='original'` (default), иначе растягиваются на всю ширину контейнера.

```jsx
<div>
    <Thumb src={helper.generateImage({w: 200, h: 200})}/>
    <hr style={{border: 'none', margin: '6px 0'}}/>
    <Thumb src={helper.generateImage({w: 500, h: 100})}/>
</div>
```


#### `width='100%'`

```jsx
<Thumb src={helper.generateImage({w: 500, h: 100})} width='100%'/>
```

```jsx
<Thumb src={helper.generateImage({w: 1500, h: 100})} width='100%'/>
```


#### `width='50%'`

```jsx
<Thumb src={helper.generateImage({w: 1500, h: 200})} width='50%'/>
```


#### `width='100%'`, `ratio={[16, 9]}`

```jsx
<Thumb src={helper.generateImage({w: 120, h: 90})} ratio={[16, 9]}/>
```


#### `width={100}`

Значение в `px`.

```jsx
<div>
    <Thumb src={helper.generateImage({w: 200, h: 200})} width={100}/>
    <hr style={{border: 'none', margin: '6px 0'}}/>
    <Thumb src={helper.generateImage({w: 500, h: 100})} width={100}/>
</div>
```


#### `width={100}`, `ratio={[16, 9]}`, `fit='cover'`

Если вместе с `width` указать `ratio`, то высота будет расчитана из `width`.

```jsx
<div>
    <Thumb src={helper.generateImage({w: 200, h: 200})} width={100} ratio={[16, 9]} fit='cover'/>
    <hr style={{border: 'none', margin: '6px 0'}}/>
    <Thumb src={helper.generateImage({w: 500, h: 100})} width={100} ratio={[16, 9]} fit='cover'/>
</div>
```


### `height`

#### `height={undefined}`, (default)

```jsx
<div>
    <Thumb src={helper.generateImage({w: 100, h: 200})}/>
    {' '}
    <Thumb src={helper.generateImage({w: 500, h: 150})}/>
</div>
```


#### `height='100%'`

Высота контейнера `100px`.

```jsx
<div style={{height: 100}}>
    <Thumb src={helper.generateImage({w: 100, h: 200})} height='100%'/>
    {' '}
    <Thumb src={helper.generateImage({w: 500, h: 150})} height='100%'/>
</div>
```


#### `height={100}`

Значение в `px`.

```jsx
<div>
    <Thumb src={helper.generateImage({w: 100, h: 200})} height={100}/>
    {' '}
    <Thumb src={helper.generateImage({w: 500, h: 150})} height={100}/>
</div>
```


#### `height={100}`, `ratio={[16, 9]}`, `fit='cover'`

Если вместе с `height` указать `ratio`, то ширина будет расчитана из `height`.

```jsx
<div>
    <Thumb src={helper.generateImage({w: 200, h: 200})} height={100} ratio={[16, 9]} fit='cover'/>
    {' '}
    <Thumb src={helper.generateImage({w: 500, h: 100})} height={100} ratio={[16, 9]} fit='cover'/>
</div>
```


### `width` + `height` = `ratio='auto'`

#### `width={N}`, `height={N}`

Реальный размер изображений 200x200.

* 1. `width={100}`, `height={200}`
* 2. `width={100}`, `height={100}`
* 3. `width={200}`, `height={100}`

```jsx
<div>
    <Thumb src={helper.generateImage({w: 200, h: 200, text: '1'})} width={100} height={200} fit='cover'/>
    {' '}
    <Thumb src={helper.generateImage({w: 200, h: 200, text: '2'})} width={100} height={100} fit='cover'/>
    {' '}
    <Thumb src={helper.generateImage({w: 200, h: 200, text: '3'})} width={200} height={100} fit='cover'/>
</div>
```


#### `width='100%'`, `height={200}`

```jsx
<Thumb src={helper.generateImage({w: 200, h: 200})} width='100%' height={200} fit='cover'/>
```


#### `width='100%'`, `height='100%'`

Высота контрейнера `200px`.

```jsx
<div style={{height: 200}}>
    <Thumb src={helper.generateImage({w: 200, h: 200})} width='100%' height='100%' fit='cover'/>
</div>
```


### `src`, `srcSet`

```jsx
<Thumb
    src={helper.generateImage({w: 200, h: 200, text: 'src'})}
    srcSet={`${helper.generateImage({w: 200, h: 200, text: '1x'})}`}
/>
{' '}
<Thumb
    src={helper.generateImage({w: 200, h: 200, text: 'src'})}
    srcSet={`${helper.generateImage({w: 200, h: 200, text: '1x'})}, ${helper.generateImage({w: 400, h: 400, text: '2x'})} 2x`}
/>
```
