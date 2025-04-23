## Компонент для скроллинга до элемента

Компонент, который предоставляет возможность проскроллить экран до обернутого элемента.

Для использования необходимо подключить эпик [scrollTo](https://github.yandex-team.ru/market/MarketNode/blob/master/epics/scrollTo.js).

Возможно 2 варианта использования:
1. Как компонента.
```jsx static
<ScrollTo name="my-component">
    <MyComponentToScroll />
</ScrollTo>
```
Когда появится необходимость проскроллить, нужно будет кинуть экшен [SCROLL_TO](https://github.yandex-team.ru/market/MarketNode/blob/master/actions/scrollTo.js) c payload'ом `{target: 'my-component'}`.

2. Как [контейнера](https://github.yandex-team.ru/market/MarketNode/blob/master/containers/ScrollTo/index.js).
Целевой компонент оборачивается аналогичным образом, но вручную кидать экшен нет необходимости, он кинется сам после маунта компонента в зависимости от значения пропса `isScrollOnMount`.
