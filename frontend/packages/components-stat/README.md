# components-stat

Инструмент для сбора статистики по компонентам

## Быстрый старт

1. Данные обо всех импортах `lego-on-react`

Файл: `./src/components/TopMenu/TopMenu.tsx`
```js
import { Button as Button2, Header as LegoHeader } from 'lego-on-react';
```

`npx components-stat $(find ./src -name *.tsx) --package=lego-on-react`
```yml
- specifiers:
    - name: Button
      localName: Button2
    - name: Header
      localName: LegoHeader
  filepath: ./src/components/TopMenu/TopMenu.tsx

  ```

2. Данные о Button из `lego-on-react` с используемыми свойствами (ключ `--props`)

Файл: `./src/components/TopMenu/TopMenu.tsx`
```js
import { Button as Button2 } from 'lego-on-react';

// ...
<Button2 size="head" theme="action">Кнопка1</Button2>
<Button2 size="s" theme="clear">Кнопка2</Button2>
// ...
```

`npx components-stat $(find ./src -name *.tsx) --package=lego-on-react --specifier=Button --props`

```yml
  - specifiers:
    - name: Button
      localName: Button2
      props:
        - - name: size
            value: head
          - name: theme
            value: action
        - - name: size
            value: s
          - name: theme
            value: clear
  filepath: ./src/components/TopMenu/TopMenu.tsx
```

3. Выводим все используемые свойства Button из всех найденных файлов в нашем проекте (ключ `--reduce`)

`npx components-stat $(find ./src -name *.tsx) --package=./src/components/Button/Button --specifier=Button --props --reduce`

```yml
- name: Button
  props:
    className:
      - JSXExpressionContainer
    logNode:
      - JSXExpressionContainer
    theme:
      - action
      - JSXExpressionContainer
      - light-gray
      - link
      - white
      - clear
      - normal
      - dark
      - green
      - pseudo
    width:
      - max
      - JSXExpressionContainer
```


## Параметры

* `--import` — путь или названия компонента, для которого необходимо собрать данные (строка или RegExp).
Например: `lego-on-react`, `./components/SomeComponent`, `@yandex-lego/components/.*`
* `--specifier` — название импортируемого компонента (строка или RegExp). Например: `Button`, `Select`
* `--props` — дополнительно парсит используемые свойства из JSX
* `--reduce` — агрегирует данные по компонентам из всех найденных файлов
* `--format=[^yml|json]` — формат данных
* `--concurrency=8` — количество одновременно обрабатываемых файлов
