# Divider

Компонент для отделения одной информации от другой. Представлен в виде тонкой линии, по умолчанию высотой `1px`.

## Пример использования

```typescript jsx
import React from 'react';
import { Divider } from '@yandex-int/tap-components/Divider';

const App: React.FC = () => {
    return (
        <>
            Content
            <Divier style={{ margin: '8px 0' }} />
            Content
        </>
    )
}
```

## Пример

{{%story:::tap-components-components-divider--playground%}}

## Свойства

| Свойство   | Тип                         | По умолчанию | Описание                                      |
| ---------- | --------------------------- | ------------ | --------------------------------------------- |
| as?        | `"symbol" \| "object" \| "a" \| "abbr" \| "address" \| "area" \| "article" \| "aside" \| "audio" \| "b" \| "base" \| "bdi" \| "bdo" \| "big" \| "blockquote" \| "body" \| "br" \| "button" \| "canvas" \| "caption" \| "cite" \| "code" \| "col" \| "colgroup" \| "data" \| "datalist" \| "dd" \| "del" \| "details" \| "dfn" \| "dialog" \| "div" \| "dl" \| "dt" \| "em" \| "embed" \| "fieldset" \| "figcaption" \| "figure" \| "footer" \| "form" \| "h1" \| "h2" \| "h3" \| "h4" \| "h5" \| "h6" \| "head" \| "header" \| "hgroup" \| "hr" \| "html" \| "i" \| "iframe" \| "img" \| "input" \| "ins" \| "kbd" \| "keygen" \| "label" \| "legend" \| "li" \| "link" \| "main" \| "map" \| "mark" \| "menu" \| "menuitem" \| "meta" \| "meter" \| "nav" \| "noindex" \| "noscript" \| "ol" \| "optgroup" \| "option" \| "output" \| "p" \| "param" \| "picture" \| "pre" \| "progress" \| "q" \| "rp" \| "rt" \| "ruby" \| "s" \| "samp" \| "script" \| "section" \| "select" \| "small" \| "source" \| "span" \| "strong" \| "style" \| "sub" \| "summary" \| "sup" \| "table" \| "tbody" \| "td" \| "textarea" \| "tfoot" \| "th" \| "thead" \| "time" \| "title" \| "tr" \| "track" \| "u" \| "ul" \| "var" \| "video" \| "wbr" \| "webview" \| "svg" \| "animate" \| "animateMotion" \| "animateTransform" \| "circle" \| "clipPath" \| "defs" \| "desc" \| "ellipse" \| "feBlend" \| "feColorMatrix" \| "feComponentTransfer" \| "feComposite" \| "feConvolveMatrix" \| "feDiffuseLighting" \| "feDisplacementMap" \| "feDistantLight" \| "feDropShadow" \| "feFlood" \| "feFuncA" \| "feFuncB" \| "feFuncG" \| "feFuncR" \| "feGaussianBlur" \| "feImage" \| "feMerge" \| "feMergeNode" \| "feMorphology" \| "feOffset" \| "fePointLight" \| "feSpecularLighting" \| "feSpotLight" \| "feTile" \| "feTurbulence" \| "filter" \| "foreignObject" \| "g" \| "image" \| "line" \| "linearGradient" \| "marker" \| "mask" \| "metadata" \| "mpath" \| "path" \| "pattern" \| "polygon" \| "polyline" \| "radialGradient" \| "rect" \| "stop" \| "switch" \| "text" \| "textPath" \| "tspan" \| "use" \| "view" \| ComponentClass<any, any> \| FunctionComponent<any>` | `'div'` | Компонент для рендера разделителя |
| className? | `string`                    | —            | Дополнительный класс у корневого DOM-элемента |
| color?     | `string`                    | —            | Цвет разделителя                              |
| innerRef?  | `RefObject<HTMLDivElement>` | —            | Ссылка на корневой DOM-элемент компонента     |
| size?      | `number`                    | `1`          | Высота разделителя в пикселях                 |
| style?     | `CSSProperties`             | —            | Пользовательские стили                        |
