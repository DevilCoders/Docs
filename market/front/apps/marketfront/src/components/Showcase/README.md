# Showcase

```jsx static
<Showcase>
    // ...
</Showcase>
```

```jsx static
// default values
<Showcase
     size='m',
     // Если cols не задано, то кол-во колонок рассчитывается
     // в зависимости от текущих брейкпоинтов и size
     cols={undefined},
     rows={2},
     align='auto',
     actionElement={undefined},
>
    // ...
</Showcase>
```

## `size='s'`

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase size='s'>
    {helper.generateImages(14).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```


## `size='m'` (default)

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase size='m'>
    {helper.generateImages(14).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```


## `size='l'`

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase size='l'>
    {helper.generateImages(14).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```

## `size='xl'`

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';
const _ = require('lodash');

<Showcase size='xl'>
    {helper.generateImages(16).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```


## `cols={5}`

Фиксированное кол-во колонок

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase cols={5}>
    {helper.generateImages(8).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```


## `rows={3}`

Фиксированное кол-во колонок

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase rows={3}>
    {helper.generateImages(21).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```


## `align='auto'` (default)

Элементов не хватает в первой строке

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase align='auto'>
    {helper.generateImages(4).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```

Элементов не хватает в последней строке

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase align='auto'>
    {helper.generateImages(8).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```


## `align='left'`

Элементов не хватает в первой строке

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase align='left'>
    {helper.generateImages(4).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```

Элементов не хватает в последней строке

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase align='left'>
    {helper.generateImages(8).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```


## `align='center'`

Элементов не хватает в первой строке

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase align='center'>
    {helper.generateImages(4).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```

Элементов не хватает в последней строке

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';

<Showcase align='center'>
    {helper.generateImages(8).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```


## `actionElement={<Button>Развернуть</Button>}`

Кнопка отображается всегда, т.к. кол-во элементов превышает максимально возможное кол-во
показываемых элементов при `size='m'` (по умолчанию)

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';
import Button from '@self/root/src/uikit/components/Button';

<Showcase actionElement={<Button>Развернуть</Button>}>
    {helper.generateImages(13).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```

Кнопка не отображается при ширине окна большей чем
[$ui-bp-large-screen](https://github.yandex-team.ru/market/levitan-gui/blob/master/styles/vars/grids.styl#L12),
при сужении окна меняется кол-во отображаемых элементов, все не влезают и кнопка показывается

```jsx
import Thumb from '@self/root/src/uikit/components/Thumb';
import Button from '@self/root/src/uikit/components/Button';

<Showcase size="xl" actionElement={<Button>Развернуть</Button>}>
    {helper.generateImages(8).map(src => <Thumb key={src} src={src} fit='cover'/>)}
</Showcase>
```
