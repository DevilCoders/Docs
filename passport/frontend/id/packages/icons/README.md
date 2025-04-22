# @yandex-id/icons

Пакет иконок используемых на сервисах [Яндекс.ID](https://passport.yandex.ru/).

## Использование

Установите пакет `npm i @yandex-id/icons`

В коде:

```jsx
import { AkbarsDefaultIcon } from '@yandex-id/components';

<AkbarsDefaultIcon prop="qwerty" />
```

## Технологии

- React
- Typescript

## Разработка

0. (Опционально) Редактируем файлик для выгрузки иконок `tools/figma-extractor/index.ts`
1. Экспортируем иконки из фигмы `npm run figma:extract`
2. Проверять можно в storybook, для этого нужно:
   - запустить storybook – `npm start`
