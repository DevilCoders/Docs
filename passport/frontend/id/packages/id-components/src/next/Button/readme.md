# Button

Компонент для создания кнопок в интерфейсе.

## Использование

По умолчанию кнопка будет показана в `variant=default` и `size=m`.

```tsx
import { Button } from '@yandex-id/components/next';

const Feature = () => {
  return <Button>Button</Button>;
};
```

## Модификация

### Список доступных css-переменных

| Токен                             | Описание                                 | Значение по умолчанию           |
| :-------------------------------- | :--------------------------------------- | ------------------------------- |
| `--id-button-height`              | Высота                                   |                                 |
| `--id-button-radius `             | Размер скругления                        |                                 |
| `--id-button-font-size`           | Размера шрифта                           |                                 |
| `--id-button-line-height`         | Высота шрифта                            |                                 |
| `--id-button-inner-gap`           | Отступ между элементами                  |                                 |
| `--id-button-out-gap`             | Отступ от краев                          |                                 |
| `--id-button-gap-compinsation`    | Значение визуальной компенсации отступов |                                 |
| `--id-button-border-color`        | Цвет рамки                               | `--id-color-static-transparent` |
| `--id-button-background`          | Цвет фона                                |                                 |
| `--id-button-shadow`              | Тень                                     |                                 |
| `--id-button-text-color`          | Цвет текста                              |                                 |
| `--id-button-text-color-hovered`  | Цвет текста при наведении                | `--id-button-text-color`        |
| `--id-button-text-color-disabled` | Цвет текста при отключении               |                                 |
| `--id-button-background-hovered`  | Цвет фона при наведении                  |                                 |
| `--id-button-background-pressed`  | Цвет фона при нажатии                    |                                 |
| `--id-button-background-disabled` | Цвет фона при отключении                 |                                 |
| `--id-button-focus-color`         | Цвет рамки фокуса                        |                                 |

### Создание модификатора

1. Создаем файл с модификатором `size` или `variant`:

   ```sh
   touch ./_variant/variant-action.module.css
   ```

1. Описываем набор css-переменных с нужными значениями из пакета `@yandex-id/design-system` в селекторе `root`:

   ```css
   .root {
     --id-button-text-color: var(--id-color-text-on-brand);
     --id-button-text-color-disabled: var(--id-color-text-on-disabled);

     --id-button-background: var(--id-color-bg-brand);
     --id-button-background-hovered: var(--id-color-bg-brand-hovered);
     --id-button-background-pressed: var(--id-color-bg-brand-pressed);
     --id-button-background-disabled: var(--id-color-bg-disabled);
   }
   ```

1. Подключаем модификатор в файл `bundle.ts`:

   ```diff
   + import variantAction from './_variants/variant-action.module.css';

   variant: {
   + action: variantAction.root,
     clear: variantClear.root,
     default: variantDefault.root,
     outline: variantOutline.root,
     raised: variantRaised.root,
     text: variantText.root,
   },
   ```
