## MgIcon

<img width="176" alt="drft layouts figma 2019-09-13 10-51-37" src="https://media.github.yandex-team.ru/user/1369/files/888ad280-d614-11e9-9ac0-246607335d9e">

[storybook](https://turbo-docs.si.yandex-team.ru/story/dev/?path=/story/mediaguides-icon--default)

Компонент иконки. Большинство иконок наследует цвет родителя с помощью `currentColor`.

### Props

| Свойство | Тип | По умолчанию | Описание |
| ------- | ------- | ----------- | ---------------------------------------- |
| `type` | `MgIconType` |  | Тип иконки (то есть конкретная иконка). |
| `size` | `MgIconSize` |  | Размер иконки: `xs`, `s`, `m`, `l` (требуется подключить `MgIcon/_Size/`). |
| `className?` | `String` |  | Микс контейнера. |

#### type
Возможные типы см. в [storybook](https://turbo-docs.si.yandex-team.ru/story/dev/?path=/story/mediaguides-icon--default)

#### size
Существует 4 размера контейнера: `xs`, `s`, `m` и `l`. `xs` и `s` используют svg размера `16`. `m` и `l` используют svg
размера `24`. Не гарантируется, что каждый тип иконки есть в обоих размерах (`16` и `24`). Если вам понадобился
отсутствующий размер у существующего типа, обратитесь к owner'у компонента.
