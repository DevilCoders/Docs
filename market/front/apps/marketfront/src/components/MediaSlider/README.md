## Overview

MediaSlider отображает дочерние элементы в виде интерактивной галереи.


```jsx
    <MediaSlider>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </MediaSlider>
```


## Props

### `autoplay`

#### `autoplay={true}`

```jsx
    <MediaSlider autoplay>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </MediaSlider>
```

### `autoplayInterval`

#### `autoplayInterval={500}`

```jsx
    <MediaSlider autoplay autoplayInterval={500}>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </MediaSlider>
```



### `looped`

#### `looped={true}`

```jsx
    <MediaSlider autoplay looped>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </MediaSlider>
```


### `indicator`

#### `indicator={true}`

```jsx
    <MediaSlider indicator>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </MediaSlider>
```

### `indicatorTheme`

#### `indicatorTheme="default"`

```jsx
    <MediaSlider indicator indicatorTheme="default">
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </MediaSlider>
```

#### `indicatorTheme="purple"`

```jsx
    <MediaSlider indicator indicatorTheme="purple">
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </MediaSlider>
```
