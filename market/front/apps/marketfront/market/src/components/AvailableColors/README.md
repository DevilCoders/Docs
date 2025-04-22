### Параметры

#### colors

Массив отображаемых цветов.

```jsx
const colors = ['red', '', 'yellow'];

<AvailableColors colors={colors} />
```

#### minColors

Задают минимальное число цветов, необходимое для отображения компонента. Дефолтное значение - 1.


```jsx
const colors = ['red', 'blue', 'yellow'];

<div>
    <AvailableColors minColors={2} colors={colors} />
    <AvailableColors minColors={4} colors={colors} />
</div>
```

#### maxColors

Задают максимальное число цветных точек, отображаемых компонентом. В случае, если colors.length > maxColors, отображаем +{colors.length - maxColors} справа от точек. Дефолтное значение - 5.


```jsx
const colors = ['red', 'blue', 'yellow', 'rebeccapurple', 'black', 'orange'];

<AvailableColors maxColors={4} colors={colors} />
```

 #### view === 'text'	
 
  ```jsx	
 const colors = ['#ffffff', 'red', 'blue', 'yellow', 'rebeccapurple', 'black', 'orange', ];	
 	
 <AvailableColors maxColors={4} colors={colors} diameter={8} view='text'/>	
 ```
