# Структура

```
metrika-components/src
├───README.md
├───index.ts   
│
├───components
│   ├───Button
│   │   └───...
│   └───...
│   
├───helpers/utils
│   ├───formatNumber
│   │   └───...
│   └───...
│
├───hocs
│   ├──withOutsideClick
│   │  └───...
│   └───...
└───hooks
    ├──useFirstEffect
    │  └───...
    └───...

```

![image](./assets/common.svg)

## internal/external
- internal - вспомогательные компоненты, которые мы не планируем использовать извне;
- external - экспортируемые наружу.

Есть желание все компоненты/хуки и тд разделить на internal/external, но это только усложнит структуру.
Кажется можно обойтись тем, что внутренные компоненты не буду экспортироваться наружу явно.

## Компоненты

```
Button
├───index.ts
├───Button.css
├───Button.stories.tsx
├───Button.test.tsx
├───Button.tsx
└───Button.md
```

У компонента могут быть вспомогательные хуки, hocs или хелперы.

### Базовый компонент

Нужно уметь пробрасывать стандартные атрибуты, можно сделать следующим образом:

```tsx
type ButtonProps = {
} & React.ButtonHTMLAttributes<HTMLButtonElement>;
  
const Button: FC<ButtonProps> = ({children, ...other}) => {
    return <button {...other}>button: {children}</button>;
}

<Button text="text" data-id="1" tabIndex={1} id="log-button"></Button>;
```

Проблема в том, что не проверяются типы при передаче ```{...other}```, туда могут попасть лишние свойства, которые мы указали сами в ButtonProps.

Еще хочется уметь валидировать, что мы в компоненте прокинули куда-то `other` и то, что тип в пропсах `HTMLButtonElement` совпадает c тегом, в который мы прокинули other.

Другой пример: в самом компоненте можем разбить свойства, а какие-то исключить, например, `type`, чтобы не использовать браузерное форматирование:

```tsx
type InputProps = {
} & React.ButtonHTMLAttributes<HTMLInputElement>;
  
const Input: FC<ButtonProps> = ({children, tabIndex, type, ...other}) => {
    // какая-то логика с type
    ...

    return <div tabIndex={tabIndex}><input {...other}/></div>;
}

<Button text="text" data-id="1" tabIndex={1} id="log-button"></Button>;
```

## Хелперы/утилиты

```
formatNumber
├───index.ts
├───formatNumber.stories.ts
├───formatNumber.test.ts
├───formatNumber.tsx
└───formatNumber.md
```

Тут точно не должно быть внутри никаких вспомогательных компонентов, хуков, hocs.

## Хуки

Тут могут быть дополнительные утилиты, но не компоненты/хуки/hocs:

```
useFirstEffect
├───index.ts
├───helpers
│   └───...
├───useFirstEffect.stories.ts
├───useFirstEffect.test.ts
├───useFirstEffect.tsx
└───useFirstEffect.md
```

## Hocs

```
withOutsideClick
├───index.ts
├───helpers
│   └───...
├───withOutsideClick.stories.ts
├───withOutsideClick.test.ts
├───withOutsideClick.tsx
└───withOutsideClick.md
```

Тут могут быть дополнительные утилиты, но не компоненты/хуки/hocs.

## Экспорт

В корне в `index.ts` реэкспортируем всё:

Примеры использования:
```tsx
import {Button} from 'metrika-ui';
import {useUpdateEffect, useFirstEffect} from 'metrika-ui';
import {withOutsideClick} from 'metrika-ui';
import {formatNumber} from 'metrika-ui';
```

## Проверка

Очень хочется написать утилиту, которая будет валидировать файловую структуру, чтобы сохранять порядок.

# Темизация

Значения основных переменных хранятся в css-переменных:

Компонент Theme:
```tsx
interface Theme {
    name: string,
    config: {
        colors: {
            main: string,
            secondary: string,
        },
        ...
    }
}

const ThemeContext = React.createContext(defaultTheme);

export const Theme: FC<{theme: Theme}> = ({children, theme: {name}}) => {
    <ThemeContext.Provider value={theme} className={`theme_type_${name}`}>
        <div>
            {children}
        </div>
    </ThemeContext.Provider>
}
```

В компоненте есть набор стандарных тем в `Theme/themes/` или можно передать снаружи.

На основании конфига генерируем css:
```css
.theme_type_basic {
    --color-main: #b2b2b2;
    --color-secondary: #e3e3e3;
}
```

В компонентах используем css-переменные, но есть возможность в случае чего достать из контекста тему.
В тему можно обернуть приложение или отдельный компонент. 
Могут быть вспомогательные withTheme (пробросить пропс theme в компонет), useTheme (получить тему через useContext).

