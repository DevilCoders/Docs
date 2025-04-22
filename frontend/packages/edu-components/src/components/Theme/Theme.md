# Theme

## Использование

Для поддержки тем в **ie11** необходимо использовать [postcss-theme-fold](https://github.com/yarastqt/postcss-theme-fold) плагин.

### На клиенте

Подключение темы для всего приложения:

```typescript
import { configureRootTheme } from '@yandex-int/edu-components/components/Theme';
import { theme } from '@yandex-int/edu-components/components/Theme/presets/pandora-default';

// Без указания root, по умолчанию body
configureRootTheme({ theme });

// С указанием root
configureRootTheme({ theme, root: document.querySelector('#root') });
```

### В рамках фичи

Переопределение темы в рамках конкретного DOM-узла:

```typescript jsx
import { cnTheme } from '@yandex-int/edu-components/components/Theme';
import { theme } from '@yandex-int/edu-components/components/Theme/presets/pandora-pink';

// Переопределение всех параметров:
const Feature = () => (
  <div className={cnTheme(theme)}>
    <Button view="pandora" size="m">
      Handle
    </Button>
  </div>
);

// Переопределение конкретного значения,
// остальные будут взяты через css-контекст из корневой темы:
const Feature = () => (
  <div className={cnTheme({ color: theme.color })}>
    <Button view="pandora" size="m">
      Handle
    </Button>
  </div>
);
```

## Тема

Каждая тема состоит из нескольких частей, ниже проиллюстрировано воздействие каждой из частей на компонент:

![image](https://media.github.yandex-team.ru/user/5546/files/5f3ab900-57e6-11ea-8f61-1447c4c8cfa9)

### color

Содержит переменные цветов, которые используются в модификациях компонентов и типографики, подчёркивая их смысл (пр. — экшен-компонент) или состояние (пр. — недоступный). Все переменные для цветов называются по смыслу, месту их использования, они не должны обозначать значение цвета.

### size

Содержит переменные размера текста и межстрочных интервалов, которые настраиваются для каждого отдельного компонента.

### capacity

Содержит в себе переменные размеров поверхностей компонентов, которые имеют как минимальные или максимальные, так и фиксированные значения.

### space

Содержит переменные отступов, которые используются как для ритма внутри компонента, так и для обозначения уровней вложенности и разделения смысловых сущностей внутри паттернов.

### cosmetic

Содержит переменные, которые используются для декоративной стилизации контролов (пр. — скругление углов, шрифт, размер границ).

## Пресет

Пресет представляет собой файл с подключением нужных CSS и экспортом объекта для установки нужных модификаторов:

```typescript
import { Theme } from '@yandex-int/edu-components/components/Theme';

import './_color/Theme_color_pandora-purple.css';
import './_size/Theme_size_pandora.css';
import './_capacity/Theme_capacity_pandora.css';
import './_space/Theme_space_pandora.css';
import './_cosmetic/Theme_cosmetic_pandora.css';

export const theme: Theme = {
  color: 'yandex-default',
  size: 'default',
  capacity: 'default',
  space: 'default',
  cosmetic: 'default',
};
```

Для удобного использования [postcss-theme-fold](https://github.com/yarastqt/postcss-theme-fold) плагина, пресеты можно собрать в виде CSS-файлов с необходимыми импортами:

```css
@import '../_color/Theme_color_pandora-purple.css';
@import '../_size/Theme_size_pandora.css';
@import '../_capacity/Theme_capacity_pandora.css';
@import '../_space/Theme_space_pandora.css';
@import '../_cosmetic/Theme_cosmetic_pandora.css';
```

### Набор стандартных пресетов

| Пресет               | color             | size       | capacity   | space      | cosmetic   |
| -------------------- | ----------------- | ---------- | ---------- | ---------- | ---------- |
| **pandora-default**  | `pandora-purple`  | `pandora`  | `pandora`  | `pandora`  | `pandora`  |
| **platform-default** | `platform-purple` | `platform` | `platform` | `platform` | `platform` |

## Ссылки

- [Как написать Тему для Лего контролов](https://wiki.yandex-team.ru/lego/2020/Yamoney-Guidelines/Kak-napisat-Temu-dlja-Lego-kontrolov/)
