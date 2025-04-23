# Метрика

Для отправки данных о действиях пользователей на странице используется библиотека [@yandex-market/cia](https://a.yandex-team.ru/arcadia/market/front/monomarket/lib/lib/cia). На текущий момент поддерживается 2 технологии логирования действий пользователей:

- Яндекс.Метрика
- Baobab

## Компонент Zone

`@yandex-market/cia` предоставляет несколько инструментов логирования пользовательских действий. Самый важный из них - это компонент `Zone`.

```tsx
import { Zone } from '@yandex-market/cia';

const Some = () => (
    <Zone name="zone1">
        some content
    </Zone>
)
```

Компоненту `Zone` обязательно необходимо передавать параметр `name`. Имя зоны будет использоваться разными технологиями логирования по-разному. По умолчанию компонент `Zone` оборачивает контент в `div`, в который добавляются data-атрибуты необходимые для работы библиотеки. Для примера выше, будет создана следующая DOM-структура

```html
<div data-zone-name="zone1">some content</div>
```

Часто лишний `<div>` над контентом мешает сделать правильную верстку. Поэтому `Zone` поддерживает 2 легальных способа решения этой проблемы.

__Первый способ__. Компоненту `Zone` можно передать `className`, который он применит к оборачиваемому `<div>`. Этот способ хорошо сработает в той ситуации, если у вас уже есть `<div>`-обертка с каким-то классом.

```tsx
<div className={styles.wrapper}>
    Some content
</div>
```
Заменяется на
```tsx
import { Zone } from '@yandex-market/cia';

<Zone name="zone" className={styles.wrapper}>
    Some content
</Zone>
```

__Второй способ__. Если передать пропс `applyToRootChild` в компонент зоны, то он _постарается_ добавить data-атрибуты в своей дочерний элемент. Если у зоны с атрибутом `applyToRootChild` больше одного дочернего элемента или этот элемент не простой DOM-компоненты (`div`, `span`, `a`, `li`, etc) - `Zone` создаст `<div>` вокруг контент и запишет warning в консоль. Этот способ имеет больше ограничений, но он позволяет не портить верстку, например, там где ее портить нельзя, например, в `<table>`, `<ul>`, `<ol>`

```tsx
<li className={styles.snippet}>
    {...}
</li>
````
Заменяется на
```tsx
import { Zone } from '@yandex-market/cia';

<Zone name="snippet" applyToRootChild>
    <li className={styles.snippet}>
        {...}
    </li>
</Zone>
```

{% note alert "Внимание!" %}

Нельзя использовать `applyToRootChild` с кастомными React-компонентами, даже если они рендерят простые DOM-компоненты внутри - будет создан `<div>` и записан warning в консоль.

```tsx
/** Так делать нельзя! */

import { Zone } from '@yandex-market/cia';

const Snippet = () => (
    <li className={styles.snippet}>
        {...}
    </li>
);

/** Будет созадн div */
<Zone name="snippet" applyToRootChild>
    <Snippet />
</Zone>
```

{% endnote %}

Зона может содержать какие-нибудь данные, которые будут залогированы вместе с пользовательским действием. Для этого в пропс `data` нужно положить сериализуемый JS-объект. 

```tsx
const Snippet = () => {
    const data = { skuId: "id", productId: "id" };
    return (
        <Zone name="snippet" data={data}>
            ...
        </Zone>
    )
}
```

Значение из пропса `data` сериализуется в JSON-строку и будет сохранено в DOM-атрибут `data-zone-data`.

По умолчанию `Zone` не слушает клики на себя и на свои дочерние элементы. Чтобы зона слушала клики, нужно передать пропс `withClickSensor`. Также можно передать `withVisibilitySensor` - тогда зона будет логировать специальное событие с типом `cia/VISIBLE` когда какая-то доля зоны попадет во viewport браузера. Размером доли можно управлять параметром `visibilityThreshold` - значение этого параметра передается в [IntersectionObserver.thresholds](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/thresholds), поэтому у него должен быть соответствующий формат.

```tsx
const Snippet = () => {
    const data = { skuId: "id", productId: "id" };
    return (
        <Zone
            name="snippet"
            data={data}
            withClickSensor
            withVisibilitySensor
        >
            ...
        </Zone>
    )
}
```

Это не все параметры компонента `Zone` - некоторые специфичны для конкретной системы логирования, некоторые мы рассмотрим дальше.

## withZone, withConnectedZone

Вместо прямого использования `Zone` можно воспользоваться HOC-ами `withZone` и `withConnectedZone`. Это полезно, если вы хотите применить зону не привязываясь к конкретному React-компоненту, например, в `compose`.

```typescript
withZone({
    name: 'snippet',
    withClickSensor: true,
})(Snippet);
```

HOC-и принимают почти такой же набор параметров, что и компонент зоны, только в виде объекта. Однако, есть несколько различий между HOC-ами и `Zone`.

1. В настройки HOC-ов нельзя передать свойство `data`. Данные для зоны через HOC-и строятся на основе второго параметра конкретного HOC-а. Об этом ниже
2. Если в настройках зоны есть только название и нет других свойств, то первым параметром HOC-ов можно передать не объект, а сразу название зоны
```typescript
withZone('snippet')(Snippet);
```
3. Свойство `className` в HOC-ах может быть не просто строкой, а функцией вида `(props: Props) => string`, чтобы определить имя классы по каким-либо пропсам оборачиваемого компонента
```typescript
withZone({
    name: 'snippet',
    className: ({active}) => active ? styles.active : undefined,
})
```

Для того чтобы управлять данными зоны, нужно использовать второй параметр HOC-ов. Для `withZone` - это функция вида `(props: Props) => object`, которая по пропсам оборачиваемого компонента определяет объект данных зоны

```typescript
withZone('snippet', ({skuId, productId}) => ({skuId, productId, type: 'product'}))
```

`withConnectedZone` вторым параметром принимает функцию-коннектор, которая создается функцией `connect` Redux или Apiary.

```typescript
withConnectedZone('snippet', connect(mapStateToProps));
```

{% note alert "Внимание!" %}

Нельзя использовать `applyToRootChild` в `withZone` и `withConnectedZone` - это --не работает-- во всех use-case-ах Маркета. То, что оно есть в типизации, реально пробрасывается до зоны и часто используется в коде Маркете - все это ошибки дизайна. Не делай так.

```tsx
/** Так делать нельзя! */

import { withZone } from '@yandex-market/cia';

const Snippet = () => (
    <li className={styles.snippet}>
        {...}
    </li>
);

withZone({
    name: "snippet",
    applyToRootChild: true,
})(Snippet); // компонет не простой DOM элемент - будет обертка <div>
```

{% endnote %}

## Redux и cia

Зоны логируют почти все redux-экшены. Экшен не логируется, если в объекте action-а есть поле `meta`, в котором есть значение `ignoreZones = true`. Все остальные экшены логируются технологиями логирования вместе с payload-ом.

```typescript
const ignoredAction = {
    type: "someActionType",
    payload: {productId: "id"},
    meta: {
        ignoreZones: true,
    },
};
```
