Хлебные крошки

```(jsx)
const { range } = require('lodash');

<BreadCrumbs
    onItemClick={(...args) => console.log('click', ...args)}
    items={range(4).map((id) => ({
        id: String(id),
        title: `Заголовок N${id}`,
        subtitle: `Подзаголовок N${id}`,
    }))}
/>
```

При сжатии контейнера часть элементов скрывается, по ховеру можно посмотреть список полностью

```(jsx)
const { range } = require('lodash');

<div style={{ width: '400px' }}>
    <BreadCrumbs
        onItemClick={(...args) => console.log('click', ...args)}
        items={range(6).map((id) => ({
            id: String(id),
            title: `Заголовок N${id}`,
            subtitle: `Подзаголовок N${id}`,
        }))}
    />
</div>
```
При необходимости можно не выводить dropdown и убрать градиент

```(jsx)
const { range } = require('lodash');

<div style={{ width: '400px' }}>
    <BreadCrumbs
        onItemClick={(...args) => console.log('click', ...args)}
        withHoverDropdown={false}
        withFade={true}
        items={range(3).map((id) => ({
            id: String(id),
            title: `Заголовок N${id}`,
            subtitle: `Подзаголовок N${id}`,
        }))}
    />
</div>
```

Длинные заголовки обрезаются

```(jsx)
const { range } = require('lodash');

<BreadCrumbs
    onItemClick={(...args) => console.log('click', ...args)}
    items={range(2).map((id) => ({
        id: String(id),
        title: `Заголовок N${id} `.repeat(5),
        subtitle: `Подзаголовок N${id} `.repeat(10),
    }))}
/>
```
