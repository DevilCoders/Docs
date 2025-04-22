# @yandex-id/components

Пакет общих компонентов используемых на сервисах [Яндекс.ID](https://passport.yandex.ru/).

Список компонентов:

- [Page](./src/components/Page/Page.md) – layout страницы (шапка, навигация)

## Использование

Установите пакет `npm i -S @yandex-id/components`

В коде:

```jsx
import { Page } from '@yandex-id/components';

<Page prop="qwerty">// Content</Page>;
```

## Технологии

- React
- Typescript
- PostCSS

## Разработка

1. Добавляем или изменяем компонент в `src/components`
2. Проверять можно в storybook, для этого нужно:
   - добавить stories ([пример](./src/components/Page/Page.stories.tsx))
   - запустить storybook – `npm start`

## Публикация пакета

Пока публикация руками (приходить к @vladislavteli). Чуть позже нужно настроить автоматическую публикацию при влитии кода в основную ветку.
