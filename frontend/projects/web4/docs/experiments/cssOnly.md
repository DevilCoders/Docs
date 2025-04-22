# Эксперименты над css

Механизм, который позволяет писать эксперимент над стилями, добавляя на страницу новые стили, значения которых можно вычислять из флагов.

Из-за того что флаг может измениться, стили шаблонизируются в рантайме.

## Создание эксперимента
> Для удобного создания css-only эксперимента реализован кодогенератор, вызвать его можно по команде `npm run generate:exp-css`, подробнее о возможностях кодогенератора можно прочитать в [документации](../generators/README.md)

Для начала создаем файл с именем платформы в папке с экспериментом, где будем писать нужный css.
Можно разбить экспериментальный код на несколько файлов, файловая структура не имеет никакого значения, код исполняется только на сервере.

Существует несколько способов написать css-only эксперимент, применяя различные условия для включения эксперимента.

Самый простой способ, пушить css в эксперименте всегда. В этом случае также можно посмотреть внутрь `context` и не пушить стили при выполненнии какого-то условия (для этого нужно вернуть null).

Пример глобального эксперимента:

```ts
// src/experiments/exp_name/desktop.ts

import type { ICssExperiment } from '@vendors/taburet/experiments';

export const RightColumnMaxWidthExp: ICssExperiment = {
    // Синтаксис указания фичи аналогичен синтаксису эксперимента с компонентом
    features: '*',
    css: (expVal, context) => {
        const [width = 0, minWidth = 0] = String(expVal).split(/:/);
        // Если пользователь незалогинен, то не пушим стили на страницу
        if (context.isLoggedIn) return null;

        // Метод должен вернуть валидный css (желательно как можно меньшего размера)
        // Никакие линтеры и плагины к нему не применяются
        return `class1{width:${width};class2{height:${height}}`;
    },
};
```

Можно добавлять css на страницу, только если на ней есть какая-то конкретная фича.
В случае, если эксперимент применяется для фичи есть возможность посмотреть внутрь сниппета используемого адаптера.
Пример эксперимент с фильтрацией по фиче:

```ts
// src/experiments/exp_name/desktop.ts

import type { ICssExperiment } from '@vendors/taburet/experiments';

// В дженерике указываем тайпинг для сниппета
export const someCssExperiment: ICssExperiment<{ adapterType: string }> = {
    features: [{ type: 'companies' }],
    css: (expVal, context, snippet) => {
        const [width = 0, minWidth = 0] = String(expVal).split(/:/);
        const { isLoggedIn } = context;
        const { adapterType } = snippet;

        // По данным из сниппета мы можем понять, что того или иного элемента
        // колдунщика на странице не будет
        // и не пушить стили для таких случаев
        if (!isLoggedIn || adapterType !== 'companies_carousel') return null;

        return `class1{width:${width};class2{height:${height}}`;
    },
};
```

Также можно добавлять css на страницу в pre-search. Для этого нужно вообще не указывать поле `features`.
Добавлять в pre-search нужно как можно меньше и только в исключительных случаях, например, если нужно модифицировать шапку (чтобы она не прыгала во время загрузки страницы).

```ts
// src/experiments/exp_name/desktop.ts

import type { ICssExperiment } from '@vendors/taburet/experiments';

export const someCssExperiment: ICssExperiment = {
    css: (expVal, context, snippet) => {
        const [width = 0, minWidth = 0] = String(expVal).split(/:/);

        // Метод должен вернуть валидный css (желательно как можно меньшего размера)
        // Никакие линтеры и плагины к нему не применяются
        return `class1{width:${width};class2{height:${height}}`;
    },
};
```

## Реестр logViewRegistry

Существует возможность пушить стили для компонента только тогда, когда он есть на странице. Для этого сначала нужно разметить требуемый компонент вызовом `logViewRegistry`.

В реестр записывается факт рендера компонента при серверной шаблонизации, а после рендера в эксперименте можно посмотреть, вызывался ли рендер того или иного компонент и на основе этого пушить на страницу стили.

В реестр записывается ключ компонента и некие данные:
```ts
logViewRegistry.add(componentName: ILogViewKey, data: Record<string, string>);
```

Ключ отрендеренного компонента типизирован. Прежде чем добавлять логирование, посмотрите, нет ли в [типе ILogViewKey](../../src/typings/logViewRegistry.ts) уже такого ключа. Если такой ключ уже есть, стоит посмотреть где он используется, возможно у вас случится коллизия и вы будете пушить стили не там, где они нужны. В случае отсутствия ключа нужно его добавить.

Можно размечать компоненты как на старом стеке (priv.js), так и на новом.

Например, вы хотите пушить стили только тогда, когда на странице есть `carousel`.

```js
// carousel.priv.js

blocks['carousel'] = function(context, data) {
    RequestCtx.GlobalContext.logViewRegistry.add('carousel', { type: data.type });
    ...
}
```

Аналогичный пример на актуальном стеке для функционального компонента с помощью хука [useLogView](../../src/lib/logView/useLogView.tsx)

```ts
const Carousel = (props): React.FC<P> => {
    useLogView('Carousel', { color: props.color });
}
```

и для классового компонента с помощью HOC withLogView[v](../../src/lib/logView/withLogView.tsx)
```ts
class Component...

withLogView(Component, 'Component', props => { color: props.color });
```

## Эксперимент с использованием фильтрации по компонентам

После разметки компонентов вызовами `logViewRegistry`, можно указать для эксперимента условие с помощью свойства `componentCondition`.

Можно проверять как рендер компонента на всей странице:

```ts
// src/experiments/exp_name/desktop.ts

import type { ICssExperiment } from '@vendors/taburet/experiments';

export const someCssExperiment: ICssExperiment = {
    // Проверяем, что где-нибудь на странице
    // был лог рендера компонента carousel и в данных есть нужный color
    features: '*',
    componentCondition: components => {
        return Boolean(components.carousel && components.carousel.color === 'blue');
    },
    css: (expVal) => {
        const [width = 0, minWidth = 0] = String(expVal).split(/:/);

        return `class1{width:${width};class2{height:${height}}`;
    },
};
```

Либо в отдельном адаптере:

```ts
// src/experiments/exp_name/desktop.ts

import type { ICssExperiment } from '@vendors/taburet/experiments';

export const someCssExperiment: ICssExperiment = {
    // Проверяем, что в органике был лог рендера компонента carousel
    features: [{ type: 'organic' }],
    componentCondition: components => {
        return Boolean(components.carousel);
    },
    css: (expVal) => {
        const [width = 0, minWidth = 0] = String(expVal).split(/:/);

        return `class1{width:${width};class2{height:${height}}`;
    },
};
```

### Добавление эксперимента в реестр

После создания, эксперимент нужно зарегистрировать в реестре нужной платформы `src/experiments/.registry/platform`

Пример регистрации на платформе `desktop`:

```diff
+ import { LinkExp } from '../exp_name/desktop';

+ cssExpRegistry.set('exp_name', [LinkExp]);
```

## FAQ

### Можно ли использовать css из файла
Нет, такой возможности нет. Если в эксперименте вы хотите допушить заранее известный css лучше использовать [эксперимент над компонентом](./components.md)

### Можно ли в глобальном эксперименте заглянуть в snippet
Глобальные эксперименты со стилями (`feature: '*'`) вызываются один раз в конце шаблонизации страницы, поэтому никаких данных о сниппете у него нет.

Эксперименты для фичей вызываются только у конкретных адаптеров, поэтому доступ к сниппету у них есть.

### Что будет, если эксперимент вызывается в нескольких фичах
Эксперимент будет вызываться для всех фичей, которые подходят под условие, но выполнится только первый подходящий под условие адаптер, будьте внимательные при использовании для эксперимента данных из сниппета.
