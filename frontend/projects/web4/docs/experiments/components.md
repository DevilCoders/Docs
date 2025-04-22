# Эксперименты. React-компоненты

> **Внимание.** Перед тем как продолжить чтение раздела, ознакомьтесь с работой [bem-react/di](https://github.com/bem/bem-react/tree/master/packages/di).

Эксперимент над компонентами в нескольких фичах реализуется через замену или расширение компонентов в реестрах компонентов этих фичей. При этом писать адаптер для эксперимента над фичами не надо.

- [Создание эксперимента](#Создание-эксперимента)
- [Регистрация](#Регистрация)
- [FAQ](#FAQ)
  - [Можно ли частично переопределить или доопределить компонент](#Можно-ли-частично-переопределить-или-доопределить-компонент)
  - [Как реализовать наложение нескольких экспериментов на один компонент](#Как-реализовать-наложение-нескольких-экспериментов-на-один-компонент)
  - [Как экспериментировать над функциональным компонентом, не переписывая его целиком](#Как-экспериментировать-над-функциональным-компонентом,-не-переписывая-его-целиком)
  - [Можно ли в эксперименте переопределить только стили](#Можно-ли-в-эксперименте-переопределить-только-стили)

## Создание эксперимента
> Для удобного создания эксперимента над компонентом реализован кодогенератор, вызвать его можно по команде `npm run generate:exp-component`, подробнее о возможностях кодогенератора можно прочитать в [документации](../generators/README.md)

Реализация экспериментальной версии компонента:

```ts
// src/experiments/exp_name/components/Link/Link.tsx

export const Link: React.FC<ILinkProps> = props => <>Exp: <Link {...props} /></>;
```

Эксперимент над компонентом требует создания специального entry-файла с описанием эксперимента:

```ts
// src/experiments/exp_name/components.entries/desktop.ts

import { IComponentsExp } from '@vendors/taburet/experiments';
import { createComponentsExperiments } from '@components/Root/Root@desktop';
import { Link } from '@components/Link/Link@desktop';

// Заменяем компонент в одной фиче
export const LinkExp: IComponentsExp = {
    // Имя фичей, для которых нужно применить эксперимент
    features: [{ type: 'FeatureName' }],

    // Если эксперимент сразу для всех фичей, то используйте *
    // features: '*',

    // Условие, при котором нужно применять эксперимент, опциональное поле (context: IGlobalContext)
    condition: context => {
        return context.isLoggedIn;
    },

    patch: [
        {
            // Идентификатор реестра, который модифицируем в эксперименте
            // Можно передать массив строк
            id: 'FeatureRegistryName',
            fill: registry => {
                // Заменяем компонент "ссылка" на экспериментальное представление
                registry.set('Link', Link);
            },
        },
    ],
};

createComponentsExperiments([LinkExp]);
```

Без entry-файла код вашего эксперимента не будет доставлен на клиента.

В проекте есть [пример экспериментов с компонентами](../../src/experiments/learn_serp_components-experiments/README.md).

## Регистрация

Эксперимент над компонентом должен быть зарегистрирован в экспериментальном реестре. Так реестр выглядит на файловой системе:

```bash
src/experiments/.registry
├── desktop.ts
└── touch-phone.ts
```

Пример регистрации на платформе `desktop`:

```diff
+ import { LinkExp } from '../exp_name/components.entries/desktop';

+ componentsExpRegistry.set('exp_name', [LinkExp]);
```

Если эксперимент не зарегистрировать, он не будет применён.

## FAQ

### Можно ли частично переопределить или доопределить компонент?
### Как реализовать наложение нескольких экспериментов на один компонент?

Для корректного наложения экспериментов с компонентами друг на друга (а также частично переопределения или доопределения компонента) необходимо использовать метод `extends` реестра. Пример использования есть в [документации bem-react](https://github.com/bem/bem-react/tree/master/packages/di#extending-components).

### Как экспериментировать над функциональным компонентом, не переписывая его целиком?

Чтобы иметь возможность точечно переопределять поведение функционального компонента в эксперименте, нужно в реестр компонента перенести часть данных или часть кода компонента (см. [Хранение дополнительных функций/данных в реестре](../patterns/components/di.md#Хранение-дополнительных-функций-данных-в-реестре)).

Простейший пример — замена цвета в компоненте. На базовом уровне берем цвет из реестра:

```tsx
const ColoredComponentPresenter = props => {
    const { color } = useRegistry<IColoredComponentRegistry>(coloredComponentCn);

    return <span className={coloredComponentCn} style={{ color }}>{props.text}</span>;
};

export const ColoredComponent = withRegistry(
    // По умолчанию компонент будет использовать черный цвет
    new Registry({ id: coloredComponentCn }).fill({ color: '#000' })
)(ColoredComponentPresenter);
```

В эксперименте заменим цвет на красный:

```ts
export const ColoredComponentExp: IComponentsExp = {
    features: [{ type: 'ColoredComponentFeatureName' }],
    patch: [
        {
            id: coloredComponentCn,
            fill: registry => {
                // Заменяем в реестре цвет на красный
                registry.set('color', '#f00');
            },
        },
    ],
};
```

По аналогии можно заменять и переопределять через `extends` не только значения, но и функции (различные обработчики и хуки).

### Можно ли в эксперименте переопределить только стили?

Если в эксперименте меняются только стили, а компоненты не переопределяются, в entry-файле можно импортировать нужные стили и объявить пустой патч без вызова `createComponentsExperiments(...);`:

```ts
// src/experiments/exp_name/components.entries/desktop.ts
import { IComponentsExp } from '../../../vendors/taburet/experiments';

import '../experimental.scss';

export const ComponentNameNewStyle: IComponentsExp = {
    features: [{ type: 'Overlay' }],
    patch: [],
};
```

Эксперимент со стилями регистрируется так же.
