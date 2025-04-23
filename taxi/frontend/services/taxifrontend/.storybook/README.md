# Storybook

Позволяет отлаживать и разработывать компоненты локально. Так же служит документацией к компонентам

[storybook.js.org](https://storybook.js.org)

## Как написать свою историю

1. Создаём файл `*.stories.js` в папке с компонентом, который нужно описать
2. Болванка шаблона

```(js)
import React from 'react';
import {action} from '@storybook/addon-actions';
import * as storybook from '@storybook/react';
import * as knobs from '@storybook/addon-knobs';
import * as info from '@storybook/addon-info';
import {Decorator} from '_storybook/addon-config';

// Описываемый компонент
import Component from './Component';

storybook.storiesOf('Component', module)
    .addDecorator(Decorator()) // optional
    .add('base',
        info.withInfo()(() => (
            <Component
                disabled={knobs.boolean('disabled', false)}
                text={knobs.text('label', 'test')}
                onClick={actions('onClick')}
            />
        ))
    );
```

- `Decorator` - Оборачивает описываем компонент в обёртку позволяющей поменять режим отображения
- `info.withInfo` - [addon-info](https://github.com/storybooks/storybook/tree/master/addons/info)
- `knobs` - [addon-knobs](https://github.com/storybooks/storybook/tree/master/addons/knobs)


## Запуск
    npm run storybook
    open http://localhost:9001/

## Публикация
    npm run build:storybook
    cd gh-pages && git init && git checkout -b gh-pages && git add . && git commit -m "documentation" && git remote add origin git@github.yandex-team.ru:taxi/taxi-frontend.git && git push origin gh-pages -f
