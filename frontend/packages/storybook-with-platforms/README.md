# Storybook-with-platforms

В [Storybook](https://storybook.js.org)-е нет возможности писать для одного и того же компонента примеры сразу для нескольких платформ. Чтобы добавить такую возможность, предлагается использовать обертку `ComponentStories`.

### Как писать?

#### ComponentStories

Написание примера для одной платформы почти не отличается от стандартного [react/storiesOf](https://storybook.js.org/docs/guides/guide-react/#step-4-write-your-stories):

``` tsx
import React from 'react';
import { ComponentStories } from '@yandex-int/storybook-with-platforms';

import { Button } from './Button';

new ComponentStories(module, 'Button', Button).add('plain', Button => <Button />);
```

Примеры для нескольких платформ пишутся аналогично:

``` jsx
import React from 'react';
import { ComponentStories } from '@yandex-int/storybook-with-platforms';

import { Button as ButtonPad } from './Button@touch-pad';
import { Button as ButtonPhone } from './Button@touch-phone';

new ComponentStories(module, 'Button', {
        'touch-pad': ButtonPad,
        'touch-phone': ButtonPhone,
    })
    .add('plain', Button => <Button />);
```

#### multiPlatformStories

```tsx
import React from 'react';
import { storiesOf } from '@storybook/react';
import { createScopeDecorator, multiPlatformStories } from '@yandex-int/storybook-with-platforms';

import { Button as ButtonPad } from './Button@touch-pad';
import { Button as ButtonPhone } from './Button@touch-phone';

multiPlatformStories({
    'touch-pad': ButtonPad,
    'touch-phone': ButtonPhone,
}, (platform, Button) => {
    storiesOf(`Button/@${platform}`, module)
        .addDecorator(createScopeDecorator(platform, 'scope'))
        .add('plain', Button => <Button />);
});
```

#### [более хитрый] использование декоратора собственной платформы

Платформа "universal", объединяющая в себе все платформы:

```tsx
import { buildScopeDecorator } from '@yandex-int/storybook-with-platforms';
import { TLevel } from '@yandex-int/storybook-with-platforms/lib/platforms';

// платформа для объединения desktop, touch-pad и touch-phone
// вместо common для пересечения
type TAdditionalPlatform = 'universal';
type TAdditionalLevel = 'universal' | TLevel;

export const [withScope, ExtendedPlatformLevels] = buildScopeDecorator<TAdditionalPlatform, TAdditionalLevel>({
  universal: ['universal', 'desktop', 'touch-pad', 'touch-phone'],
});

export type TExtendedPlatform = keyof typeof ExtendedPlatformLevels;

storiesOf('Button', module)
    .addDecorator(withScope('universal', 'scope'))
    .add('plain', () => <Button />);
```

### Что на выходе?

В итоге в Storybook поедет такая структура:

- Button
    - @touch-pad
        - plain
        - active
    - @touch-phone
        - plain
        - active

### Как работает?

Чтобы стили с разных платформ внутри Storybook-приложения не влияли друг на друга, необходимо использовать `postcss-scope-plugin`, если необходимо дополнительно изолировать стили для проекта, то можно задать свой `scope` в настройках плагина.

Пример [доопределения конфигурации webpack](https://storybook.js.org/docs/configurations/custom-webpack-config/):

``` js
// .storybook/webpack.config.js
module.exports = async ({ config }) => (
    { ...config,
        module: {
            rules: [
                {
                    test: /\.scss$/,
                    use: [
                        'style-loader',
                        'css-loader',
                        {
                            loader: require.resolve('postcss-loader'),
                            options: {
                                plugins: [
                                    require('@yandex-int/storybook-with-platforms/lib/plugins/postcss-scope-plugin').default({ scope: 'scope' })
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    }
);
```

`ComponentStories` для всех примеров создает `div`-обертку с классами вида `sb-root-scope__*` (в случае использования `multiPlatformStories` это надо делать руками), а специальный webpack-loader при сборке Storybook-а усиливает селекторы в стилях для платформ.

Общие стили ссылки из `Link.scss` остаются без изменения, а стили desktop-ной ссылки из `Link@desktop.scss` модифицируются:

``` scss
// было:
.Link {
    color: blue;
}

// стало:
.sb-root-scope__desktop {
    .Link {
        color: blue;
    }
}
```

При переходе на "Link@desktop" компонент будет обернут в `<div class="sb-root-scope__deskpad sb-root-scope__desktop">...</div>`. Так для каждой версии компонента применятся только нужные стили.

В случае, если ваши компоненты в стилях упираются на классы страницы, и эти классы находятся по DOM-дереву
раньше, чем классы `sb-root-scope`, при вызове плагина можно воспользоваться опцией `globalClassNames: string[]`.

Например, чтобы селектор

```scss
.i-ua_skin_dark .Text {
    color: '#fff';
}
```

после сборки превратился в

```scss
.i-ua_skin_dark .sb-root-scope__common .Text
```

нужно добавить глобальный класс в конфигурацию плагина

```js
globalClassNames: ['i-ua_skin_dark']
```
