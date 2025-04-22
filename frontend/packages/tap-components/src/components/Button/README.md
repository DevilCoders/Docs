# Button

Компонент для создания кнопок.

## Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import {
    Button as ButtonBase,
    withSizeM,
    withViewDefault,
} from '@yandex-int/tap-components/Button';

const Checkbox = compose(withSizeM, withViewDefault)(ButtonBase);

const App: React.FC = () => {
  return (
    <Button view="default" size="m">
      Button
    </Button>
  );
};
```

## Пример

{{%story:::tap-components-components-button--playground%}}

## Свойства

| Свойство      | Тип | По умолчанию | Описание |
| ------------- | --- | ------------ | -------- |
| addonAfter? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | — | Дополнительный контент после `children` |
| addonBefore? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | — | Дополнительный контент перед `children` |
| as? | `"symbol" \| "object" \| "a" \| "abbr" \| "address" \| "area" \| "article" \| "aside" \| "audio" \| "b" \| "base" \| "bdi" \| "bdo" \| "big" \| "blockquote" \| "body" \| "br" \| "button" \| "canvas" \| "caption" \| "cite" \| "code" \| "col" \| "colgroup" \| "data" \| "datalist" \| "dd" \| "del" \| "details" \| "dfn" \| "dialog" \| "div" \| "dl" \| "dt" \| "em" \| "embed" \| "fieldset" \| "figcaption" \| "figure" \| "footer" \| "form" \| "h1" \| "h2" \| "h3" \| "h4" \| "h5" \| "h6" \| "head" \| "header" \| "hgroup" \| "hr" \| "html" \| "i" \| "iframe" \| "img" \| "input" \| "ins" \| "kbd" \| "keygen" \| "label" \| "legend" \| "li" \| "link" \| "main" \| "map" \| "mark" \| "menu" \| "menuitem" \| "meta" \| "meter" \| "nav" \| "noindex" \| "noscript" \| "ol" \| "optgroup" \| "option" \| "output" \| "p" \| "param" \| "picture" \| "pre" \| "progress" \| "q" \| "rp" \| "rt" \| "ruby" \| "s" \| "samp" \| "script" \| "section" \| "select" \| "small" \| "source" \| "span" \| "strong" \| "style" \| "sub" \| "summary" \| "sup" \| "table" \| "tbody" \| "td" \| "textarea" \| "tfoot" \| "th" \| "thead" \| "time" \| "title" \| "tr" \| "track" \| "u" \| "ul" \| "var" \| "video" \| "wbr" \| "webview" \| "svg" \| "animate" \| "animateMotion" \| "animateTransform" \| "circle" \| "clipPath" \| "defs" \| "desc" \| "ellipse" \| "feBlend" \| "feColorMatrix" \| "feComponentTransfer" \| "feComposite" \| "feConvolveMatrix" \| "feDiffuseLighting" \| "feDisplacementMap" \| "feDistantLight" \| "feDropShadow" \| "feFlood" \| "feFuncA" \| "feFuncB" \| "feFuncG" \| "feFuncR" \| "feGaussianBlur" \| "feImage" \| "feMerge" \| "feMergeNode" \| "feMorphology" \| "feOffset" \| "fePointLight" \| "feSpecularLighting" \| "feSpotLight" \| "feTile" \| "feTurbulence" \| "filter" \| "foreignObject" \| "g" \| "image" \| "line" \| "linearGradient" \| "marker" \| "mask" \| "metadata" \| "mpath" \| "path" \| "pattern" \| "polygon" \| "polyline" \| "radialGradient" \| "rect" \| "stop" \| "switch" \| "text" \| "textPath" \| "tspan" \| "use" \| "view" \| ComponentClass<any, any> \| FunctionComponent<any>` | `'button'` | HTML-атрибут для рендера кнопки |
| checked? | `false \| true` | — | Кнопка нажата |
| children? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | — | Текст кнопки. |
| className? | `string` | — | Дополнительный класс у корневого DOM-элемента |
| controlRef? | `RefObject<ContainerElement>` | — | Ссылка на DOM-элемент нативного контрола |
| disabled? | `false \| true` | — | Неактивное состояние кнопки. Состояние, при котором кнопка отображается, но недоступна для действий пользователя |
| icon? | `(className: string) => ReactElement<IIconProps, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<...>)>` | — | Иконка на кнопке |
| iconLeft? | `(className: string) => ReactElement<IIconProps, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<...>)>` | — | Иконка слева от текста кнопки |
| iconRight? | `(className: string) => ReactElement<IIconProps, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<...>)>` | — | Иконка справа от текста кнопки |
| id? | `string` | — | Уникальный id компонента |
| innerRef? | `(instance: HTMLElement) => void \| RefObject<HTMLElement>` | — | Ссылка на корневой DOM элемент компонента |
| onClick? | `(event: MouseEvent<HTMLElement>) => void` | — | Обработчик клика на кнопку |
| role? | `string` | — | HTML-атрибут `role` |
| title? | `string` | — | Всплывающая подсказка |
| type? | `string` | `'button'` | Тип кнопки |
