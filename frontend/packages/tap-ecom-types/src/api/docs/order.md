# Сущность `order`

## `createOrder`

```typescript
createOrder: <OrderType = Order>(request: OrderCreateRequest) => Promise<OrderResponse<OrderType>>;
```

Отправляет запрос на оформление заказа. Используется на экране оформления заказа.

## `fetchOrder`

```typescript
fetchOrder: <OrderType = Order>(request: OrderRequest) => Promise<OrderResponse<OrderType>>;
```

Получает заказ пользователя. Используется на экране заказа.

## `fetchOrders`

```typescript
fetchOrders: <OrderType = Order>(request: BaseRequest) => Promise<OrdersResponse<OrderType>>;
```

Получает все заказы пользователя. Используется на экране списка заказов.
