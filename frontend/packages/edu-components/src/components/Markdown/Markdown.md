# Markdown

<!-- description:start -->
Компонент для отображения разметки в формате `markdown`.
<!-- description:end -->

Компонент поставляется с правилами, которыми можно обогащать компонент, благодаря чему он сможет преобразовывать элементы разметки в React-компоненты.

Из коробки есть два вида правил:

1. Простые правила, в которых, не используются компоненты из реестра
2. Более сложные правила, в которых, компонент для рендера достается из реестра

Соответственно, компоненты первого вида стилизуются при помощи миксов, а второго вида можно модифицировать любым образом, после чего нужно вставить его обратно в реестр.

Правила, которых нет в изначальном наборе, можно реализовывать самостоятельно (включая регулярное выражение для матчинга и функцию парсинга). Ниже будет пример создания кастомного правила.

## Примеры

### Пример использования

### Только необходимые правила

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import { withRegistry, Registry } from '@bem-react/di';
import {
  Markdown as MarkdownBase,
  cnMarkdown,
  withRuleBrSign,
  withRuleSpoiler,
} from '@yandex-int/edu-components/Markdown/desktop';
import {
  Spoiler as SpoilerBase,
  withFlavorGrape,
} from '@yandex-int/edu-components/Spoiler/desktop';

import { withYourOwnRule } from './withYourOwnRule';

// Создаем реестр
const markdownRegistry = new Registry({ id: cnMarkdown() });

// Собираем компонент спойлера
const Spoiler = withFlavorGrape(SpoilerBase);
const FlavoredSpoiler = props => <Spoiler {...props} flavor="grape" />;

// Устанавливаем его в реестр
markdownRegistry.set('Spoiler', FlavoredSpoiler);

// Собираем компонент
const Markdown = compose(
  withRegistry(markdownRegistry),
  withRuleBrSign,
  withRuleSpoiler,
  withYourOwnRule,
)(MarkdownBase);

const content = `
!>Спойлер
Внутри скобок стоит знак плюс{br}
поэтому воспользуемся формулой квадрата суммы.{br}
И таким образом мы получим правильный ответ, но если не получилось то это не повод отчаиваться. {br}
!<
`;

// Используем в приложении
const App = () => <Markdown>{content}</Markdown>;
```

### Написание собственного правила

Для того чтобы добавить свое правило, нужно будет написать HOC, который будет дополнять существующий набор правил вашим.

Создадим правило `blue`, которое будет захватывать текст, помеченный меткой `{blue:}`, и красить его в синий цвет.

withRuleBlue.tsx
```typescript jsx
import React, { useMemo } from 'react';
import {
  TMarkdownRuleHOC,
  TMarkdownRules,
} from '@yandex-int/edu-components/Markdown/desktop/bundle';

import { Blue } from './Blue';

export const withRuleBlue: TMarkdownRuleHOC = Markdown => {
  return ({ rules, ...restProps }) => {
    const extendedRules: TMarkdownRules = useMemo(() => {
      return {
        ...rules,
        blue: {
          order: 0,
          match(source) {
            return /^{blue:(*.?)}/.exec(source);
          },
          parse(capture, parse, state) {
            return {
              content: parse(capture[1], state),
            };
          },
          react(node, output, state) {
            return <Blue>{output(node.content, state)}</Blue>;
          },
        },
      };
    }, [rules]);

    return <Markdown {...restProps} rules={extendedRules} />;
  };
};
```

Blue.tsx
```typescript jsx
import React from 'react';

import './Blue.css';

export const Blue = ({ children }) => {
  return <span className="Blue">{children}</span>;
};
```

Blue.css
```css
.Blue {
    color: #00f;
}
```

App.tsx
```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import { Markdown as MarkdownBase } from '@yandex-int/edu-components/Markdown/bundle/desktop';

import { withRuleBlue } from './withRuleBlue';

const Markdown = compose(withRuleBlue)(MarkdownBase);

const content = `{blue:Этот текст будет синим}`;

const App = () => <Markdown>{content}</Markdown>;
```

## Свойства

<!-- props:start -->
| Свойство           | Тип                                                                                                                                                                                                                                                               | Описание                                                                                                                                                                                                                           |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| innerRef?          | `(instance: HTMLDivElement) => void \| RefObject<HTMLDivElement>`                                                                                                                                                                                                 | Ссылка на корневой DOM-элемент.                                                                                                                                                                                                    |
| className?         | `string`                                                                                                                                                                                                                                                          | Дополнительный класс.                                                                                                                                                                                                              |
| state?             | `State`                                                                                                                                                                                                                                                           | Дополнительные параметры или состояния компонентов разметки.<br>Например:<br>- Информация об изображении (размер, ссылка) для `image`<br>- Тип поля, контента для поля ввода `input`<br>- Разметка формул для компонента `formula` |
| children?          | `string`                                                                                                                                                                                                                                                          | Контент с разметкой в формате `markdown`.                                                                                                                                                                                          |
| postParse?         | `(tree: SingleASTNode[]) => SingleASTNode[]`                                                                                                                                                                                                                      | Функция для манипуляции с деревом, полученным после парсинга маркдауном.                                                                                                                                                           |
| additionalContent? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Дополнительный контент, который кладётся в конец корневого компонента.                                                                                                                                                             |
<!-- props:end -->

## Форматы правил
### author
Формат:

`{author:Контент}`

Пример:

`{author:Имя автора}`

### brSign
Формат:

`{br}`

### coloredText
Формат:

`{coloredText:color}Текст{\coloredText}`

Пример:

`{coloredText:graphite}Серый текст{\coloredText}`

Доступные цвета:
- trueblack
- graphite
- jeans
- ashes
- alice
- storm
- avocado
- sand
- brown
- tomato
- white

### formula
Формат:

`{formula:Индекс формулы}`

Вместе с правилом передается объект с кодом в формате LaTeX для всех формул, указанных в разметке.

Пример:

`{formula:1}`

Объект:

```text
{
  formulas: {
    '1': {
      code: '\binom{n}{k}'
    }
  }
}
```

### horizontalAlign
Формат:
```text
align content
align
```
- `align`  <-- | <-> | >-< | --> - группа выравнивания
- `content` Контент и переносы строк

Перед закрывающей группой выравнивания обязательно должен стоять перенос строки.

Пример:
```text
>-< $A = B + C$
>-<
```

### image
Формат:

`![alt](url title){:htmlAttr}`

- `alt` Подпись изображения для скрин-ридеров
- `url` Ссылка на изображение
- `title` Подпись изображения (необязательный)
- `htmlAttr` html-атрибуты изображения, например: style, htmlFor (необязательный)

Пример:

`![Тестовое изображение](https://yastatic.net/www/_/x/Q/xk8YidkhGjIGOrFm_dL5781YA.svg "Заголовок"){:style="margin: 0 auto;display: block;" htmlFor="Test"}`

### imageFloat
Формат:

`!float[alt](url title)`

- `float` < | > - символ обтекания по левому или правому краю
- `alt` Подпись изображения для скрин-ридеров
- `url` Ссылка на изображение
- `title` Подпись изображения (необязательный)

Пример:

`!>[Тестовое изображение](https://yastatic.net/www/_/x/Q/xk8YidkhGjIGOrFm_dL5781YA.svg)`

### sizedText
Формат:

`{sizedText:size}Текст{\sizedText}`

Пример:

`{sizedText:large}Большой текст{\sizedText}`

Доступные размеры:
- small
- helper
- medium
- large

### small
Формат:

`{small:Контент}`

Пример:

`{small:Маленький текст}`

### spoiler
Формат:
```text
!>caption
content
!<
```
- `caption` Заголовок спойлера
- `content` Контент спойлера

После заголовка спойлера (`caption`) и перед закрывающей группой спойлера (`!<`) обязательно должен быть перенос строки.

Пример:
```text
!>Заголовок
Первая строка контента
Последняя строка контента
!<
```

### sub
Формат:

`{sub:Контент}`

Пример:

`{sub:Индекс}`

### sup
Формат:

`{sup:Контент}`

Пример:

`{sup:Степень}`

### tab
Формат:

<code>&#92;&#92;tab Контент</code>

Перед контентом должен стоять пробельный символ.

Пример:

<code>&#92;&#92;tab Текст с отступом</code>

### verticalAlign
Формат:

`{valign:align:content}`

- `align` baseline | top | middle | bottom | sub | text-top - значения свойства `vertical-align`
- `content` Контент

Пример:

`{valign:baseline:Текст}`

### formattedNumber
Формат:

Отрицательные и положительные числа. Могут быть, как целыми, так и десятичными дробями (с запятой или точкой в качестве разделителя).

Числа в тексте должны быть отделены знаками препинания или пробельными символами, либо заключены в фигурные скобки.

Пример:
```text
1234
1234.1
1234,1
-1234
{1234}
```

### youtube
Формат:
`{youtube:url}`

- `url` Ссылка на видео

Пример:

`{youtube:https://www.youtube.com/watch?v=L_dWvTCdDQ4}`

### yandexPlayer
Варианты формата:
```text
1. {yaplayer|url|params}
2. {yaplayer|params}
```
- `url` Ссылка на видео (если отсутствует, то `params` обязателен)
- `params` Параметры видео (среди них может быть `url`), вида `propA=X;propB=Y`

Пример:

`{yaplayer|https://strm.yandex.ru/vh-ugc-converted/vod-content/0b20a66b99082446b48036b2d03ab616.m3u8|autoplay=true}`

### yandexMusic
Формат:
`{yamusic:params}`

- `params` Параметры сниппета музыки. Включает: тип, `track` или `playlist`, и `id` источника.

Пример:
```text
{yamusic:track=21728923/2493089}
{yamusic:playlist=yamusic-daily/26553462}
```

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Markdown)
