# @yandex-id/design-system

## Установка

```sh
npm i -PE @yandex-id/design-system
```

## Использование

Установите провайдер для всего приложения:

```tsx
import { ThemeProvider } from '@yandex-id/design-system';

export const App = () => {
  return <ThemeProvider>...</ThemeProvider>;
};
```

Воспользуйтесь хуком если необходимо установить тему на компоненты, которые располагаются вне корня приложения, либо если необходимо изменить тему в конкретном компоненте:

```tsx
import { useTheme } from '@yandex-id/design-system';

const Popover = () => {
  const { themeProps } = useTheme(/* { colorScheme: 'light' } */);

  return <div {...themeProps}>...</div>;
};
```

## Выгрузка токенов

1. Выгрузить из figma токены с цветами при помощи плагина figma-tokens
1. Положить файл с токенами в `src/raw.json`
1. Запустить `node tools/import-colors.js`
