# levitan

![](https://badger.yandex-team.ru/npm/@yandex-levitan/core/version.svg)
![](https://badger.yandex-team.ru/npm/@yandex-levitan/market/version.svg)
![](https://badger.yandex-team.ru/npm/@yandex-levitan/b2b/version.svg)

## Yandex.Market Design System and Framework

[Документация для **дизайнеров**](https://wiki.yandex-team.ru/levitan/documentation/)

[Документация для **разработчиков** (CONTRIBUTING.MD)](./CONTRIBUTING.md)

### Редактирование документации портала

Для написании документации используется формат [MDX](https://mdxjs.com/), который позволяет в markdown-разметке использовать React-компоненты.

Вся документация хранится в директории [website](/website).
Роутинг строится автоматически в соответствии с файловой иерархией.

Соответственно, если нужно добавить страницу описания принципов дизайна Маркета, то необходимо создать следующий файл:

_website/market/design/design-principles/index.mdx_

```mdx
# Design Principles

Hey!
```

И рендер этой страницы будет доступен по адресу `/market/design/design-principles`

#### Навигация

Навигация в портале определяется автоматически, на основе свойства `menu` в `mdx` файле.

Если нужно добавить в меню ссылку на созданную страницу `Design Principles`, достаточно уровнем выше добавить эту страницу в меню, например:

_website/market/design/index.mdx_

```mdx
---
menu:
    - design-principles
---

# market/design
```
