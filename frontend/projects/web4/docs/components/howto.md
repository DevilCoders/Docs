# React-компоненты. Рецепты и примеры

1. [Заготовка](#1-Заготовка)
2. [Константы](#2-Константы)
3. [Типы](#3-Типы)
4. [Стили](#4-Стили)
5. [Дочерние компоненты и элементы](#5-Дочерние-компоненты-и-элементы)
6. [Переводы](#6-Переводы)
7. [Все вместе](#7-Все-вместе)
8. [Баобаб](#8-Баобаб)
9. [Примеры](#9-Примеры)
10. [Hermione-тесты](#10-Hermione-тесты)
11. [Unit-тесты](#11-Unit-тесты)
12. [Документация](#12-Документация)

### 1. Заготовка
> Для удобного создания компонента реализован кодогенератор, вызвать его можно по команде `npm run generate:conponent`, подробнее о возможностях кодогенератора можно прочитать в [документации](../generators/README.md)

Создаём новый общий компонент `MyComponent`. Компонент может быть [функциональным или классовым](https://ru.reactjs.org/docs/components-and-props.html#function-and-class-components), но в примерах будем использовать только функциональную запись.

Для компонента создается отдельная папка, внутри которой размещается реализация этого компонента. Имя папки должно совпадать с именем компонента. Внутри папки компонента создается такая структура:

```diff
+ ├── MyComponent/ — папка компонента
+ |   ├── MyComponent.const — константы
+ |   ├── MyComponent.typings — типы
+ |   ├── ...
```

Файлы внутри каждой папки именуются по общему правилу:
- если разницы между платформами нет, весь код пишется в файле MyComponent.tsx
- если есть разница в реализации между платформами, то код раскладывается по [уровням переопределения](../../README.md#Уровни-переопределения)

При этом, способ записи имен файлов для корневой папки компонента и вложенных папок немного отличается:
- файлы в корне именуются по шаблону `MyComponent@` + "уровень", например `MyComponent@desktop.tsx`

В примерах будем считать, что компонент создается только для одной платформы "desktop".

### 2. Константы

Минимальный набор констант компонента включает css-классы, используемые в реализации компонента. Эти классы генерируются утилитой [@bem-react/classname](https://github.com/bem/bem-react/tree/master/packages/classname).

```diff
  ├── MyComponent/
  |   ├── MyComponent.const/ — константы
+ |       └── index.ts
```

```ts
/**
 * MyComponent.const/index.ts
 */

import { cn } from '@bem-react/classname';

// Конструктор классов для компонента
export const cnMyComponent = cn('MyComponent');

// Классы, используемые в компоненте. Обычно это классы элементов
export const myComponentCn = cnMyComponent();
export const numCn = cnMyComponent('Num');
export const linkCn = cnMyComponent('Link');
```

### 3. Типы

Минимальный набор типов компонента включает составляет тип `props`-ов компонента. Обычно этот тип расширяет `IClassNameProps` из [@bem-react/core](https://github.com/bem/bem-react/tree/master/packages/core) для удобной реализации БЭМ-примесей (компоненту всегда можно примешать дополнительный css-класс).

```diff
  ├── MyComponent/
  |   ├── MyComponent.typings/ — типы
+ |       └── index.ts
```

```ts
/**
 * MyComponent.typings/index.ts
 */

import { IClassNameProps } from '@bem-react/core';

export interface IMyComponentProps extends IClassNameProps {
    num: number;
    url: string;
}
```

### 4. Стили

Стили для компонента пишутся в scss-файлах в синтаксисе css, расширенном за счет postcss-плагинов (см. [конфиг](../../postcss.config.js)).
Основные расширения:
- нестинг правил
- `$`-переменные
- `@import`-ы

Типографику, иконки и цвета следует брать из [дизайн-системы](https://depot.yandex-team.ru/), новые константы по возможности не плодить.

```diff
  ├── MyComponent/
+ |   └── MyComponent@desktop.scss
```

### 5. Дочерние компоненты и элементы

В коде компонента могут потребоваться другие общие компоненты или более мелкие компоненты, используемые только в этом месте, в терминологии БЭМ — это элементы. Код элементов располагается внутри папки компонента:

```diff
  ├── MyComponent/
+ |   └── Num/ — папка элемента
+ |       └── MyComponent-Num@desktop.tsx — React-реализация элемента
```

```tsx
/**
 * Num/MyComponent-Num@desktop.tsx
 */

import React from 'react';
import { numCn } from '../MyComponent.const';

export interface IMyComponentNumProps {
    num: number;
}

export const MyComponentNum: React.FC<IMyComponentNumProps> = props => (
    <span className={numCn}>{props.num}</span>
);
```

Все реализованные элементы, как и другие используемые в `MyComponent` компоненты регистрируются в Глобальном Реестре, который создается для каждой платформы. Подробнее про него можно прочитать в его [документации](https://a.yandex-team.ru/arcadia/frontend/projects/web4/src/lib/PlatformedRegistry/README.md)

```diff
  ├── MyComponent/
  |   └── Num/ — папка элемента
  |       └── MyComponent-Num@desktop.tsx — React-реализация элемента
+ |       └── index.tsx — Добавление компонентов в реестр
```

```ts
/**
 * index.tsx
 */

import { withPlatform } from '@lib/PlatformedRegistry';
import { MyComponentNum as desktop } from './MyComponent-Num@desktop';

export const MyComponentNum = withPlatform({ desktop, 'touch-phone': () => null });
```

### 6. Переводы

Для хранения переводов компонента создается отдельная папка:

```diff
  ├── MyComponent/ — папка компонента
  |   ├── ...
+ |   └── MyComponent.i18n/ — переводы
+ |       ├── ru.ts — переводы для русского языка
+ │       ├── en.ts — переводы для английского языка
+ │       ├── ... — переводы для других языков
+ │       └── index.ts
```

Подробнее про переводы см. в [Системы/i18n](../systems/i18n.md).

### 7. Все вместе

Минимальная React-реализация компонента, использующего реестр с зависимостями, стили и переводы может выглядеть так:

```diff
  ├── MyComponent/ — папка компонента
  |   ├── MyComponent.const — константы
  |   |   └── index.ts
  |   ├── MyComponent.i18n — переводы
  |   |   ├── ru.ts
  │   |   ├── en.ts
  │   |   ├── ...
  │   |   └── index.ts
  │   ├── MyComponent.typings — типы
  |   |   └── index.ts
  |   ├── Num/ — папка элемента
  |   |   └── MyComponent-Num@desktop.tsx
  |   |   └── index.tsx
  |   ├── desktop
  |   |   ├── index.ts
  │   |   └── package.json
  |   ├── index.ts
  |   ├── package.json
  |   ├── MyComponent@desktop.scss
+ |   └── MyComponent@desktop.tsx
```

```tsx
/**
 * MyComponent@desktop.tsx
 */

import React from 'react';
import i18nFactory from '@yandex-int/i18n';

import { Link } from '@components/Link';
import { cnMyComponent, myComponentCn, linkCn } from './MyComponent.const';
import { MyComponentNum } from './Num';
import * as keyset from './MyComponent.i18n';
import { myComponentRegistry, IMyComponentRegistry } from './MyComponent.registry/desktop';
import { IMyComponentProps } from './MyComponent.typings';

// Импортируем стили компонента
import './MyComponent@desktop.scss';

const i18n = i18nFactory(keyset);

// Реализация компонента
export const MyComponentPresenter: React.FC<IMyComponentProps> = props => (
  <div className={cnMyComponent(undefined, [props.className])}>
      <MyComponentNum num={props.num} />
      <Link
          className={linkCn}
          href={props.url}
      >
          {i18n('Пример ссылки'))}
      </Link>
  </div>
);
```

### 8. Баобаб

Логирование показов и клиентских событий, связанных с компонентами, делается с использованием "Баобаб" счетчиков.

Чтобы начать логировать события компонента, нужно добавить обработчики соответствующих событий в компонент:

```diff
export interface IMyComponentNumProps {
    num: number;
+   onClick?: React.MouseEventHandler;
}
```

Обработчик нужно позвать в нужном месте, и создать с помощью `withBaobab` для компонента узел в дереве логировани.
Для функциональных компонентов предпочтительней использовать хук `useBaobab`.

Пример:

```diff
+ import { ILoggable, useBaobab } from '@yandex-int/react-baobab-logger';
// ...

+ const nodeInfo = { name: 'my-component' };

- export const MyComponent: React.FC<IMyComponentProps> = props => {
+ const MyComponentPresenter = React.FC<ILoggable<IMyComponentProps>> = props => {
+   const { nextContext, node, BaobabProvider } = useBaobab(nodeInfo, props.logNode, props);
+   const onClick = React.useCallback(event => {
+       node.logClick(undefined, [event], props);
+
+       // Порядок важен, сначала логируем, потом кликаем
+       // Из-за того что в логировании происходит подготовка к возможным изменениям DOM / оверлеям / турбо
+       if (props.onClick) props.onClick(event);
+   }, [node, props]);

    return (
        <div className={cnMyComponent(undefined, [props.className])}>
-           <MyComponentNum num={props.num} onClick={props.onClick}>
+           <MyComponentNum num={props.num} onClick={onClick}>
                <Link
                    className={linkCn}
                    href={props.url}
                >
+                   <BaobabProvider value={nextContext}>
                       {props.children}
+                   </BaobabProvider>
                </Link>
        </div>
    );
};
```

#### Lego + withBaobab = withBaobabPure
Если вы используете компоненты из Lego, то следует помнить, что withBaobab добавляет в props свойство baobabNode.
Поэтому, если компонент Lego пробрасывает все неизвестные для себя props в DOM атрибуты, то это приведёт к появлению в верстке `baobabNode="[object Object]"`.
А так же в dev режиме React будет ругаться: "React not recognize the baobabNode on a DOM element".
Чтобы этого не было необходимо обернуть лего компонент в withBaobabPure.

Подробнее про Баобаб см. в [wiki/Баобаб в React](https://wiki.yandex-team.ru/search-interfaces/baobab/#react) и [react-baobab-logger/README](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/react-baobab-logger).

### 9. Примеры

Проверить новый компонент можно через [Storybook](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/storybook-with-platforms)-пример:

```diff
  ├── MyComponent/ — папка компонента
  |   ├── ...
+ |   └── MyComponent.stories@desktop.tsx
```

```tsx
/**
 * MyComponent.stories@desktop.tsx
 */

import { MyComponent } from '.';

// предварительно навешивая все модификаторы

export default {
    title: 'MyComponent',
    component: MyComponent,
    argTypes: {
        theme: {
            control: 'select',
            options: [undefined, 'normal', 'neoblue'],
        },
        // ....
    },
};

const Template: ComponentStory<typeof MyComponent> = args => <MyComponent {...args} />;

export const plain = Template.bind({});

export const notPlain = Template.bind({});
notPlain.args = {
    theme: 'normal',
};
```

Увидеть пример можно локально:
1. Запускаем `npm run examples:build` и `npm run examples:start`
2. Переходим по ссылке `http://localhost:9001`

При написании примеров рекомендуется использовать [правила](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/lego-components/docs/EXAMPLES.md) принятые в [команде Лего](https://abc.yandex-team.ru/services/vteamlego/).

Для того, чтобы storybook не собирал все примеры, можно воспользоваться переменной окружения `STORY_PATH`

```STORY_PATH=path/to/MyComponent npm run examples:build``` или из директории компонента ```STORY_PATH=`pwd` npm run examples:build```

### 10. Hermione-тесты

После того, как компонент готов, нужно написать на него hermione-тест, используя уже написанные Storybook-примеры из [п. 9](#9-Проверяем-что-все-работает). Тест кладется рядом с кодом компонента и пишутся на чистом JavaScript.

```diff
  ├── MyComponent/ — папка компонента
  |   ├── ...
+ |   └── MyComponent.test/ — папка с тестами
+ |       ├── MyComponent.page-object/ — папка с конструкторами селекторов
+ |       |   └── index.js
+ |       └── MyComponent@desktop.hermione.js
```

<details>
<summary>MyComponent.page-object/index.js</summary>

```js
const { ReactEntity, create } = require('../../../../vendors/hermione');

const elems = {};

elems.myComponent = new ReactEntity({ block: 'MyComponent' });

// если селекторы отличаются на разных платформах, то создаются еще файлы index@{platform}.js
// и экспортируется объект вида: { desktop, ... }
module.exports = create(elems);
```
</details>

<details open>
<summary>MyComponent@desktop.hermione.js</summary>

```js
const PO = require('./MyComponent.page-object');

describe('MyComponent', function() {
    it('plain', function() {
        return this.browser
            .yaOpenComponent(PO.myComponent(), 'plain')
            .assertView('plain', PO.myComponent());
    });
});
```
</details>

При изменении кода Storybook-примера необходимо пересобрать статику (вызываем повторно `npm run examples:build`, либо используем `npm run examples:start:watch`).

Подробнее про Hermione см. в [wiki/Hermione](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/).

### 11. Unit-тесты

Если в компоненте есть базнес-логика или другой код, который не меняет верстку, его удобнее тестировать юнит-тестами. Для рендеринга React-компонентов в юнит-тестах используется [Enzyme](https://github.com/airbnb/enzyme). Сам тест кладется рядом с hermione-тестами.

```diff
  ├── MyComponent/ — папка компонента
  |   ├── ...
  |   └── MyComponent.test/ — папка с тестами
  |       ├── MyComponent.page-object
  |       ├── MyComponent@desktop.hermione.js
+ |       └── MyComponent@desktop.test.tsx
```

```tsx
/**
 * MyComponent@desktop.test.tsx
 */

import React from 'react';
import { describe, it } from 'mocha';
import { assert } from 'chai';
import { shallow } from 'enzyme';

import { MyComponent } from '../MyComponent@desktop';

describe('MyComponent', () => {
    // искусственный пример теста, в реальности такой тест был бы бесполезен
    it('should have elements num and title inside', () => {
        const component = shallow(<MyComponent
            num={1}
            href="https://ya.ru"
        />);

        assert.isNotEmpty(component.find('.MyComponent-Num'));
        assert.isNotEmpty(component.find('.MyComponent-Link'));
    });
});
```

Запустить тест можно командой `npm run unit:file MyComponent/MyComponent.test/MyComponent\@desktop.test.tsx`.

### 12. Документация

Документация на компонент пишется в файле `README.md` рядом с кодом компонента. В документации следует использовать "description" и "props" [шаблоны ts-docgen](https://a.yandex-team.ru/arc_vcs/frontend/projects/lego/packages/ts-docgen#2-%D1%80%D0%B0%D0%B7%D0%BC%D0%B5%D1%82%D0%BA%D0%B0-%D0%B2-markdown) (инструмент используется в Лего-компонентах и, скорее всего, будет использован в Серпе)

<details>
<summary>Шаблон документации компонента</summary>

```md
# MyComponent

<!-- description:start -->
<!-- description:end -->

Краткое описание компонента, его продуктовый смысл и сфера применения. Здесь же можно коротко описать особенности реализации (например, зависимости).

## Пример использования

Конфигурация и несколько основных примеров использования с кодом, который потом можно было бы скопировать и запустить без правок.

<!-- props:start -->
<!-- props:end -->

## FAQ

### Один стандартный вопрос про компонент?

### Какой-то другой стандартный вопрос?
```
</details>
