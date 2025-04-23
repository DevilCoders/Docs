# AdaptiveGrid

Компонент-сетка. Позволяет:

- Отобразить элементы в виде сетки из двух колонок.
- Отобразить большее число колонок, если позволяет ширина экрана.
- Растянуть элементы на ширину всех колонок.

## Пример использования

```typescript jsx
import React from 'react';
import { AdaptiveGrid, AdaptiveGridItem } from '@yandex-int/tap-components/AdaptiveGrid';

const App: React.FC = () => {
    return  (
        <AdaptiveGrid className="my-grid">
           <div>Item 1</div>
           <div>Item 2</div>
           <AdaptiveGridItem fullWidth>Banner</AdaptiveGridItem>
           <div>Item 3</div>
           <div>Item 4</div>
        </AdaptiveGrid>
    );
};
```

## Пример

{{%story:::tap-components-components-adaptivegrid--playground%}}

## Свойства

| Свойство   | Тип      | Описание                                      |
| ---------- | -------- | --------------------------------------------- |
| className? | `string` | Дополнительный класс у корневого DOM-элемента |

## AdaptiveGridItem

Вспомогательный компонент-обёртка для элемента сетки, используется, чтобы растянуть элемент на всю ширину сетки.

### Свойства

| Свойство   | Тип       | Описание                                        |
| ---------- | ----------| ----------------------------------------------- |
| fullWidth? | `boolean` | Позволяет растянуть элемент сетки на всю ширину |

### CSS-переменные

| Переменная                     | Тип                     | Описание                                                   |
| ------------------------------ | ----------------------- | ---------------------------------------------------------- |
| --adaptive-grid-column-gap     | `px`                    | Отступ между колонками                                     |
| --adaptive-grid-row-gap        | `px`                    | Отступ между строками                                      |
| --adaptive-grid-item-min-width | <code>px&#124;fr</code> | Минимальная ширина элемента сетки                          |
| --adaptive-grid-item-max-width | <code>px&#124;fr</code> | Максимальная ширина элемента сетки                         |

### Поддержка

Chrome >= 57 \
Safari >= 10.1 \
iOS Safari >= 10.3
