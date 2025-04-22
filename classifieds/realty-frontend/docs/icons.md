# SVG иконки (спрайт)

Все иконки находятся в каталоге `packages/browser/icons` и разделены по блокам-категориям
(как в [Фигме](https://www.figma.com/file/dna5pKOYpAEzYyApTHUzLXJ3/Realty-guide?node-id=0%3A1)).
Все иконки без категории находятся в каталоге `common`.
Именуются иконки с ее размером на конце, например `call-16.svg`.
У всех иконок задан `fill="currentColor"`, что позволяет переопределять цвет через `color` родителя.
Перед добавлением новой иконки необходимо убедиться, что такой иконки еще нет.

## Storybook
Все иконки можно посмотреть в сторибуке в компоненте `IconSvg`.

## Использование
```js
import icon from '@realty-front/icons/common/call-16.svg';
import IconSvg from 'vertis-react/components/IconSvg';

class Foo extends React.PureComponent {
    render() {
        return <IconSvg id={icon} size={IconSvg.SIZES.SIZE_16} />; 
    }
}
```

## Как это работает
1. SVG-иконка напрямую импортится в компоненте (по сути мы импортим только сам id).
см. `webpack-utils/lib/svg-sprite/runtime-generator-ssr.js`
2. `svg-sprite-loader` динамически собирает спрайт из используемых иконок в отдельный файл.
3. Содержимое файла выгружается в HTML на этапе SSR и в бандлы не включается.

Спрайт не попадает в клиентский бандл при использовании SSR
благодаря переопределению рантайма
```js
imagesRule({
    svgSpriteLoaderOptions: {
        runtimeGenerator: require.resolve('./lib/svg-sprite/runtime-generator-ssr.js')
    }
})
```
