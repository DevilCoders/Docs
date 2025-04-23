## MgButton

![image](https://media.github.yandex-team.ru/user/8702/files/412cfd80-dec2-11e9-984c-d02342223b82)

[storybook](https://turbo-docs.si.yandex-team.ru/story/dev/?path=/story/mediaguides-button--default)

Кнопка на основе @lego/Button. Для использования необходимо обернуть в нужные HOC модификаторов. ([см. пример](#Использование)).

### Модификаторы

| Свойство | Тип | HOCs | Описание |
| ------- | ------- | ----------- | ---------------------------------------- |
| `theme` | `MgIconTheme` | `withThemePrimary`, `withThemeSecondary`, `withThemeClear` | Тема кнопки. |
| `size` | `MgIconSize` | `withSizeS`, `withSizeM`, `withSizeL`  | Размер кнопки. |
| `appearance` | `MgButtonAppearance` | `withAppearanceDark` | Внешность кнопки. |
| `pin` | `MgButtonPin` | `withPinCircleCircle` | Тип закругления углов кнопки. Если не задан тип, углы скруглены.|

_Так как кнопка сделана на основе @lego/Button, возможно использование ее HOC'ов, но их корректная работа не
гарантуруется._

### Использование в компонентах
Для использования кнопки необходимо импортировать необходимый набор HOC'ов и сделать композицию через `compose`
из `@bem-react/core`.

_Так как для функционирования кнопки нужен клиентский код, `hasClient` адаптера компонента, в котором используется
кнопка, должен возвращать `true`._

```js
import * as React from 'react';
import { compose, composeU } from '@bem-react/core';

// modifiers
import { withAppearanceDark } from '@yandex-turbo/components/MgButton/_Appearance/MgButton_Appearance_Dark';
import { withSizeM } from '@yandex-turbo/components/MgButton/_Size/MgButton_Size_M';
import { withSizeL } from '@yandex-turbo/components/MgButton/_Size/MgButton_Size_L';
import { withThemePrimary } from '@yandex-turbo/components/MgButton/_Theme/MgButton_Theme_Primary';
import { withPinCircleCircle } from '@yandex-turbo/components/MgButton/_Pin/MgButton_Pin_CircleCircle';
// types for props
import { MgButtonAppearance, MgButtonSize, MgButtonTheme, MgButtonPin } from '@yandex-turbo/components/MgButton/MgButton.types';
// base button
import { MgButton } from "@yandex-turbo/components/MgButton/MgButton";

const Button = compose(
    withAppearanceDark,
    // Чтобы типы корректно определились, при использовании модификтора
    // с разными значениями нужно использовать composeU.
    composeU(
        withSizeM,
        withSizeL),
    withPinCircleCircle,
    withThemePrimary
)(MgButton);

export class MgNewComponentWithButtons extends React.PureComponent {
    public render() {
        return (
            <div>
                <p>Your button, yay:</p>
                <Button
                    theme={MgButtonTheme.PRIMARY}
                    size={MgButtonSize.M}
                    appearance={MgButtonAppearance.DARK}
                    pin={MgButtonPin.CIRCLE_CIRCLE}
                >
                    Click me!
                </Button>
                <p>Yet another button:</p>
                <Button
                    theme={MgButtonTheme.PRIMARY}
                    size={MgButtonSize.L}
                >
                    Bigger button!
                </Button>
            </div>
        );
    }
}
```

**В данный момент в bem-react-core имеется [проблема](https://github.com/bem/bem-react/issues/493), не позволяющая
использовать условные операторы для формирования пропсов. Например, этот код вызовет ошибку типизации:**
```js
<Button {...buttonProps} size={true ? MgButtonSize.M : MgButtonSize.L}>
Кнопка
</Button>
```

Временное решение:
```js
<Button {...buttonProps} size={true ? MgButtonSize.M : MgButtonSize.L as any}>
Кнопка
</Button>
```

### Взаимодействие с иконками
Иконки или другие элементы можно подставить при помощи пропсов `addonBefore` и\или `addonAfter`. При этом выставляются
особые отступы в зависимости от `size`.
![storybook 2019-11-02 15-46-15](https://media.github.yandex-team.ru/user/1369/files/f4252c80-fd87-11e9-898a-1447c3113564)

### Использование в turbojson
Адаптер кнопки возвращает бандл с полным набором хоков. Таким образом в turbojson можно описать весь набор пропсов в
поле `props`, но в случае такого использования в ваш бандл попадет весь css кнопки, поэтому такой сценарий работы НЕ
РЕКОМЕНДУЕТСЯ. Пример:
```json
{
    "block": "mg-button",
    "props": {
        "theme": "primary",
        "size": "s",
        "pin": "circle-circle"
    },
    "content": "Primary CircleCircle S"
}
```
