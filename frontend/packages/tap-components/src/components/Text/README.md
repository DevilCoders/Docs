# Text

Базовый примитив представления текстовых данных.

## Пример использования

```typescript jsx
import React from 'react'
import { Text } from '@yandex-int/tap-components/Text'

const App: React.FC = () => (
    <Text as="div">
        Hello world!
    </Text>
)
```

## Пример

{{%story:::tap-components-components-text--playground%}}

## Свойства

| Свойство         | Тип        | Описание                                                        |
| ---------------- | ---------- | --------------------------------------------------------------- |
| align? | `"start" \| "end" \| "center" \| "justify"` | Задает выравнивание текста в компоненте. |
| as? | `"symbol" \| "object" \| "a" \| "abbr" \| "address" \| "area" \| "article" \| "aside" \| "audio" \| "b" \| "base" \| "bdi" \| "bdo" \| "big" \| "blockquote" \| "body" \| "br" \| "button" \| "canvas" \| "caption" \| "cite" \| "code" \| "col" \| "colgroup" \| "data" \| "datalist" \| "dd" \| "del" \| "details" \| "dfn" \| "dialog" \| "div" \| "dl" \| "dt" \| "em" \| "embed" \| "fieldset" \| "figcaption" \| "figure" \| "footer" \| "form" \| "h1" \| "h2" \| "h3" \| "h4" \| "h5" \| "h6" \| "head" \| "header" \| "hgroup" \| "hr" \| "html" \| "i" \| "iframe" \| "img" \| "input" \| "ins" \| "kbd" \| "keygen" \| "label" \| "legend" \| "li" \| "link" \| "main" \| "map" \| "mark" \| "menu" \| "menuitem" \| "meta" \| "meter" \| "nav" \| "noindex" \| "noscript" \| "ol" \| "optgroup" \| "option" \| "output" \| "p" \| "param" \| "picture" \| "pre" \| "progress" \| "q" \| "rp" \| "rt" \| "ruby" \| "s" \| "samp" \| "script" \| "section" \| "select" \| "small" \| "source" \| "span" \| "strong" \| "style" \| "sub" \| "summary" \| "sup" \| "table" \| "tbody" \| "td" \| "textarea" \| "tfoot" \| "th" \| "thead" \| "time" \| "title" \| "tr" \| "track" \| "u" \| "ul" \| "var" \| "video" \| "wbr" \| "webview" \| "svg" \| "animate" \| "animateMotion" \| "animateTransform" \| "circle" \| "clipPath" \| "defs" \| "desc" \| "ellipse" \| "feBlend" \| "feColorMatrix" \| "feComponentTransfer" \| "feComposite" \| "feConvolveMatrix" \| "feDiffuseLighting" \| "feDisplacementMap" \| "feDistantLight" \| "feDropShadow" \| "feFlood" \| "feFuncA" \| "feFuncB" \| "feFuncG" \| "feFuncR" \| "feGaussianBlur" \| "feImage" \| "feMerge" \| "feMergeNode" \| "feMorphology" \| "feOffset" \| "fePointLight" \| "feSpecularLighting" \| "feSpotLight" \| "feTile" \| "feTurbulence" \| "filter" \| "foreignObject" \| "g" \| "image" \| "line" \| "linearGradient" \| "marker" \| "mask" \| "metadata" \| "mpath" \| "path" \| "pattern" \| "polygon" \| "polyline" \| "radialGradient" \| "rect" \| "stop" \| "switch" \| "text" \| "textPath" \| "tspan" \| "use" \| "view" \| ComponentClass<any, any> \| FunctionComponent<any>` | Тип элемента для отображения как (строка или компонент). |
| children? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Основной контент |
| className? | `string` | Дополнительный класс у корневого DOM-элемента |
| color? | `"link" \| "brand" \| "inverse" \| "primary" \| "promo" \| "secondary" \| "ghost" \| "control-primary" \| "alert" \| "warning" \| "disable" \| "success" \| "control-secondary" \| "control-passive" \| "control-ghost" \| "control-faint" \| "control-disable" \| "control-link" \| "control-error" \| "link-external" \| "link-minor" \| "link-hover"` | Цвет текста |
| maxLines? | `number` | Максимальное количество строк текста (работает в связке с overflow) |
| overflow? | `"fade" \| "ellipsis" \| "fade-horizontal"` | Задает отображение переполненного текста |
| style? | `CSSProperties` | Дополнительные стили |
| typography? | `"display-xl" \| "display-l" \| "display-m" \| "display-s" \| "headline-xl" \| "headline-l" \| "headline-s" \| "headline-xs" \| "headline-m" \| "subheader-xl" \| "subheader-l" \| "subheader-m" \| "subheader-s" \| "body-short-xl" \| "body-short-l" \| "body-short-m" \| "body-short-s" \| "body-long-xl" \| "body-long-l" \| "body-long-m" \| "body-long-s" \| "caption-xl" \| "caption-l" \| "caption-m" \| "overline-l" \| "overline-m" \| "overline-s" \| "control-xxs" \| "control-xs" \| "control-s" \| "control-l" \| "control-xl" \| "control-m" \| "control-xxl"` | Задает типографику текста в компоненте |
