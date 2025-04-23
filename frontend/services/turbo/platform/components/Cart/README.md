## Корзина

`CartData` - компонет реализующий CRUD работы с товарами в корзине. Это singleton, который используется одновременно в `CartIcon`, `ProductAddToCart` и `Cart` . Из-за особенностей сборки его приходится
размещать в одном бандле, чтобы всё работало как надо.

`CartData` одним из параметров принимает storage для корзины, инстанс которого берется из `window.Ya.storage`. На текущий момент реализовано две стратегии хранения: localstorage (компонент `CartDataLS`) и server (компонент `CartDataServer`).

Как это работает:
1. Каждый storage представляет собой отдельную стратегию и реализует интерфейс `IStorage`
2. Для каждого storage есть соответствубщий бандл в `src/bundles`, при пуше которого в `window.Ya.storage` записывается его инстанс.
```ts
import { CartDataLS } from '@yandex-turbo/components/CartData/CartDataLS';

window.Registry({
    CartDataLS
});

window.Ya.storage = new CartDataLS();
```
3. Компоненты `CartIcon`, `ProductAddToCart` и `Cart` получают на вход json, в котором может быть явно указан storage через поле `"storage": "localstorage"`. Если его нет, то по умолчанию используется server storage.
4. В адаптере этих компонетов мы пушим соответствующий storage через контекст
```ts
this.context.assets.pushBundleReact('CartDataLS');
```
5. В самих компонентах инициализируем `CartData`, передавая storage из `window.Ya.storage`
```ts
    const cartData = new CartData({
        shopId: this.props.shopId,
        storage: window.Ya.storage
    });
```

Такая реализация позволяет не тащить лишний код разных storage на клиент, хотя и не является достаточно отказоустойчивым решением.
Если компонент наследует какой-либо из `CartIcon`, `ProductAddToCart` и `Cart` и мы хотим по умолчанию задать другой storage, то его нужно просто запушить в адаптере.
