# Spacer

Компонент, который вставляет своих детей с заданным смещением.

## Пример использования

Значения внутренних отступов можно задать с помощью 3 вариантов:

1. С помощью свойства `all`:

    ```typescript jsx
    import React from 'react'
    import { Spacer } from '@yandex-int/tap-components/Spacer'

    const App: React.FC = () => (
        <Spacer all={10}>
          Content
        </Spacer>
    )
    ```

1. С помощью свойства `vertical` и/или `horizontal`:

    ```typescript jsx
    import React from 'react'
    import { Spacer } from '@yandex-int/tap-components/Spacer'

    const App: React.FC = () => (
        <Spacer vertical={10} horizontal={20}>
            Content
        </Spacer>
    )
    ```

1. С помощью свойства `top` и/или `bottom`, и/или `right`, и/или `left`:

    ```typescript jsx
    import React from 'react'
    import { Spacer } from '@yandex-int/tap-components/Spacer'

    const App: React.FC = () => (
        <Spacer top={10}>
            Content
        </Spacer>
    )
    ```

> Можно указать единицы измерения, если передать значение в виде строки, например, `10rem` — по умолчанию будут использованы `px`.

## Пример

{{%story:::tap-components-components-spacer--playground%}}

## Свойства

| Свойство  | Тип                      | По умолчанию | Описание                                  |
| --------- | ------------------------ | ------------ | ----------------------------------------- |
| all? | `string \| number` | — | Отступ со всех сторон, работает как `padding: 1rem;` |
| as? | `"symbol" \| "object" \| "a" \| "abbr" \| "address" \| "area" \| "article" \| "aside" \| "audio" \| "b" \| "base" \| "bdi" \| "bdo" \| "big" \| "blockquote" \| "body" \| "br" \| "button" \| "canvas" \| "caption" \| "cite" \| "code" \| "col" \| "colgroup" \| "data" \| "datalist" \| "dd" \| "del" \| "details" \| "dfn" \| "dialog" \| "div" \| "dl" \| "dt" \| "em" \| "embed" \| "fieldset" \| "figcaption" \| "figure" \| "footer" \| "form" \| "h1" \| "h2" \| "h3" \| "h4" \| "h5" \| "h6" \| "head" \| "header" \| "hgroup" \| "hr" \| "html" \| "i" \| "iframe" \| "img" \| "input" \| "ins" \| "kbd" \| "keygen" \| "label" \| "legend" \| "li" \| "link" \| "main" \| "map" \| "mark" \| "menu" \| "menuitem" \| "meta" \| "meter" \| "nav" \| "noindex" \| "noscript" \| "ol" \| "optgroup" \| "option" \| "output" \| "p" \| "param" \| "picture" \| "pre" \| "progress" \| "q" \| "rp" \| "rt" \| "ruby" \| "s" \| "samp" \| "script" \| "section" \| "select" \| "small" \| "source" \| "span" \| "strong" \| "style" \| "sub" \| "summary" \| "sup" \| "table" \| "tbody" \| "td" \| "textarea" \| "tfoot" \| "th" \| "thead" \| "time" \| "title" \| "tr" \| "track" \| "u" \| "ul" \| "var" \| "video" \| "wbr" \| "webview" \| "svg" \| "animate" \| "animateMotion" \| "animateTransform" \| "circle" \| "clipPath" \| "defs" \| "desc" \| "ellipse" \| "feBlend" \| "feColorMatrix" \| "feComponentTransfer" \| "feComposite" \| "feConvolveMatrix" \| "feDiffuseLighting" \| "feDisplacementMap" \| "feDistantLight" \| "feDropShadow" \| "feFlood" \| "feFuncA" \| "feFuncB" \| "feFuncG" \| "feFuncR" \| "feGaussianBlur" \| "feImage" \| "feMerge" \| "feMergeNode" \| "feMorphology" \| "feOffset" \| "fePointLight" \| "feSpecularLighting" \| "feSpotLight" \| "feTile" \| "feTurbulence" \| "filter" \| "foreignObject" \| "g" \| "image" \| "line" \| "linearGradient" \| "marker" \| "mask" \| "metadata" \| "mpath" \| "path" \| "pattern" \| "polygon" \| "polyline" \| "radialGradient" \| "rect" \| "stop" \| "switch" \| "text" \| "textPath" \| "tspan" \| "use" \| "view" \| ComponentClass<any, any> \| FunctionComponent<any>` | `'div'` | Компонент для рендера |
| bottom? | `string \| number` | — | Отступ снизу, работает как `padding: 0 0 1rem 0;` |
| className? | `string` | — | Дополнительный класс у корневого DOM-элемента |
| horizontal? | `string \| number` | — | Отступ по вертикали, работает как `padding: 0  1rem;` |
| innerRef? | `RefObject<HTMLElement>` | —            | Ссылка на корневой DOM-элемент компонента |
| left? | `string \| number` | — | Отступ слева, работает как `padding: 0 0 0 1rem;` |
| right? | `string \| number` | — | Отступ справа, работает как `padding: 0 1rem 0 0;` |
| style? | `CSSProperties` | — | Пользовательские стили |
| top? | `string \| number` | — | Отступ сверху, работает как `padding: 1rem 0 0 0;` |
| vertical? | `string \| number` | — | Отступ по вертикали, работает как `padding: 1rem 0;`  |




