# API

Для интеграции шаблона магазина с конкретным API необходимо реализовать модуль, соответствующий
типу `Api` в файле `src/api/types/index.ts`.
Модуль состоит из набора методов, которые должны будут обращаться к API по параметрам
на входе и отдавать результат, преобразованный в формат, используемый приложением.

Во все запросы добавляется `context`, содержащий информацию о выбранных глобальных фильтрах,
пользователе и выбранном им городе.

## Методы

* [`fetchRootCategory`](./category.md#fetchRootCategory)
* [`fetchCategory`](./category.md#fetchCategory)
* [`fetchProduct`](./product.md#fetchProduct)
* [`fetchProductsByCategory`](./product.md#fetchProductsByCategory)
* [`fetchShops`](./shop.md#fetchShops)
* [`fetchShopsByCart`](./shop.md#fetchShopsByCart)
* [`fetchCity`](./city.md#fetchCity) – пока не используется в шаблоне
* [`fetchCities`](./city.md#fetchCities) – пока не учитывается пагинация в шаблоне
* [`updateCart`](./cart.md#updateCart)
* [`fetchCart`](./cart.md#fetchCart)
* [`createOrder`](./order.md#createOrder)
* [`fetchOrder`](./order.md#fetchOrder) - пока не используется в шаблоне
* [`fetchOrders`](./order.md#fetchOrders) – пока не учитывается пагинация в шаблоне
* [`fetchGlobalFilters` (опциональный)](./filter.md#fetchGlobalFilters) – пока не используется в шаблоне
* [`fetchFilters` (опциональный)](./filter.md#fetchFilters) – пока не используется в шаблоне
* [`fetchBrands` (опциональный)](./brand.md#fetchBrands)
* [`fetchRecommendedProducts` (опциональный)](./product.md#fetchRecommendedProducts)
* [`fetchRelatedProductsByProduct` (опциональный)](./product.md#fetchRelatedProductsByProduct)
* [`fetchRecommendedProductsByProduct` (опциональный)](./product.md#fetchRecommendedProductsByProduct)
* [`fetchRecommendedProductsByCart` (опциональный)](./product.md#fetchRecommendedProductsByCart)
* [`fetchShopsByProduct` (опциональный)](./shop.md#fetchShopsByProduct) – пока не используется в шаблоне
* [`findCityByCoordinates` (опциональный)](./shop.md#findCityByCoordinates)
* [`suggest` (опциональный)](./search.md#suggest)
* [`search` (опциональный)](./search.md#search) – пока не используется в шаблоне

## Пример использования
```typescript
import { Api } from '@yandex/tap-ecom-types';

const api: Api = {
    // реализация методов API
    ...
}; 
```

## Расширение и переопределение типов API

Для случаев, когда необходимо глобально переопределить типы данных в методах API, в типе `Api` предусмотрен набор дженерик-параметров:
```typescript
import {
    Brand,
    Cart,
    Category,
    City,
    Filters,
    Order,
    Product,
    Shop,
} from '@yandex/tap-ecom-types';

type MyApi<Brand, Category, City, Filters, Shop, ShortProduct, Cart, Order, Product>;
```

Например, чтобы добавить поле `rating` товару и отразить это во всех методах API, где используется тип товара,
нужно расширить типы товара и указать новые типы в дженерик-параметрах `Api`, после чего можно будет определить
методы нашего модифицированного `Api` с новыми типами.

Пример:
```typescript
import {
    Api,
    Brand,
    Category,
    City,
    Filters,
    Product,
    SearchItem,
    Shop,
    ShortProduct,
    SuggestItem,
} from '@yandex/tap-ecom-types';

type WithRating = { rating: number; };

type MyProduct = Product & WithRating;
type MyShortProduct = ShortProduct & WithRating;

type MyApi = Api<Brand, Category, City, Filters, GlobalFilters, MyProduct, SearchItem, SuggestItem, Shop, MyShortProduct>;
```

В случаях, когда хочется поменять тип запроса, ответа или метод целиком, удобнее поступить следующим образом:
Исключить из типа `Api` метод, который хочется переопределить, составить новый тип метода, добавить его к `Api` и
получить модифицированный тип `Api`.

Пример:
```typescript
import {
    Api,
    Brand,
    FetchBrands,
    OrderCreateRequest,
    OrderCreateResponse,
} from '@yandex/tap-ecom-types';

# добавляем популярность бренда только в методе fetchBrands
type MyBrand = Brand & { popularity: number; };
type MyFetchBrands = FetchBrands<MyBrand>;

# добавляем промокод в данные запроса для метода createOrder
type WithPromocode = { promocode?: string };
type MyOrderCreateRequest = OrderCreateRequest & WithPromocode;
type MyCreateOrder = (request: MyOrderCreateRequest) => Promise<OrderResponse>; 

type MyApi = Omit<Api, 'fetchBrands' | 'createOrder'> & { fetchBrands: MyFetchBrands; createOrder: MyCreateOrder };
```
