# React и SVG

## CSS

SVG в CSS загружается через `url-loader` + `image-webpack-loader`. Маленькие файлы инлайнятся прямо в CSS, большие выкатываются на кластер статики.

```css
.foo {
    background-image: url("./foo.svg");
}

/* Если SVG имеет маленький размер, то будет собран как */
.foo {
    background-image: url(data:image/svg+xml;base64,...);
}
/* Если SVG имеет большой размер, то будет собран как */
.foo {
    background-image: url(//yastatic.net/s3/vertis-front-deploy/_autoru-frontend/<name>_<hash>.svg);
}

```

## JS (`svg-sprite-loader`)

Складываем иконки обычными SVG-файлами в папку `auto-core/icons`. Рекомендуется прогнать новый файл через `svgo --pretty file.svg` для удобства чтения и редактирования.
Хранить сжатые файлы не стоит. Собранный спрайт будет оптимизирован через `image-webpack-loader`.

Хорошей схемы контроля дубликатов и похожих иконок пока нет, поэтому надо внимательно следить, чтобы не добавлять похожие иконки. Удобно посмотреть используемые иконки в [сторибуке](http://autoru-front-storybook-web.vrts-slb.test.vertis.yandex.net/?path=/story/icons--svg-sprite), тут лежат все иконки из auto-core/icons.

При сомнениях всегда можно смотреть в [дизайнерский гайд](https://www.figma.com/file/bwnGVVeVHFnB5WZ0t0OvIHM8/Auto-%E2%80%A2-Icons?node-id=0%3A1)

### Несколько советов:
1. **Согласно гайдам все иконки должны быть вписаны в квадрат 24х24px (`<svg viewBox="0 0 24 24">`)** (при добавлении экспортируйте иконку с верхним слоем, как правило он гайдового размера и с осмысленным названием вида `24/more`. При несовпадении можно смело просить дизайнера перезалить в макет иконку в правильном размере)
2. Если уже есть похожая иконка (например, стрелка, плюсик и т.п.), а дизайнер хочет немного другую, стоит настаивать на том, чтобы мы использовали везде или старую или новую, но никак не две сразу.
3. Чтобы проще было искать дубликаты, файлы лучше называть от общего к частному (категория -> подкатегория -> состояния).
Плохо: `verified-vin`, `unverified-vin`, `special-vas-icon`, `rounded-arrow`. Хорошо: `vin-verified`, `vin-unverified`, `vas-icon-special`, `vas-icon-top`, `arrow-rounded`, `arrow-in-circle`.    
4. Одноцветные иконки должны быть не в черном, и не в белом цвете, а должны использовать currentColor (заменяем `fill="currentColor"` или `stroke="currentColor"`), это позволяет иконке отнаследовать нужный цвет и избежать лишнего дублирования иконок между проектами. Для использования просто достаточно передать через className класс с нужныйм цветом `color: #abc`

### Использование:
```js
const IconSvg = require('auto-core/react/components/islands/IconSvg');
const mySVGIcon = require('auto-core/icons/vin-verified.svg');

class Foo extends React.PureComponent {
    render() {
        return <IconSvg id={ mySVGIcon }/>; 
    }
}
```

### Как это работает:
1. SVG-иконка напрямую рекварится в компоненте.
2. `svg-sprite-loader` динамически собирает спрайт из используемых иконок.
3. Созданный спрайт выгружается прямо в HTML на этапе SSR и в бандлы не включается (т.о. мы уменьшаем размер клиентского бандла). 

Результат:
```js
const IconSvg = require('auto-core/react/components/islands/IconSvg');
// const mySVGIcon = require('auto-core/icons/vin-verified.svg');
const mySVGIcon = "svg-in-sprite-ID"; // ID иконки === имя файла

class Foo extends React.PureComponent {
    render() {
        // return <IconSvg id={ mySVGIcon }/>;
        return (
            <svg>
                <use xlinkHref={ `#${ mySVGIcon }` }/>
            </svg>
        ) 
    }
}
```

## JS (`svg-inline-loader`)

Иногда надо заинлайнить SVG прямо в код, для этого подойдет `svg-inline-loader`.
Он заменить require на содержимое файла в виде строки.

Использование:
```js
const Svg = require('auto-core/react/components/common/Svg');
const mySVGIcon = require('!svg-inline-loader!auto-core/icons/vin-verified.svg');

class Foo extends React.PureComponent {
    render() {
        return <Svg src={ mySVGIcon }/>; 
    }
}
```

Результат:
```js
const Svg = require('auto-core/react/components/common/Svg');
// const mySVGIcon = require('!svg-inline-loader!auto-core/icons/vin-verified.svg');
const mySVGIcon = "<svg>....</svg>";

class Foo extends React.PureComponent {
    render() {
        // return <Svg src={ mySVGIcon }/>;
        return (
            <span dangerouslySetInnerHTML={{ __html: src }}/>
        ) 
    }
}
```
