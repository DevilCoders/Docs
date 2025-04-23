# ReactBus

__В React-коде не должно быть прямых обращений в i-bem, только через события на шине `ReactBus`__

## Реализация

Шина реализована поверх [TinyEmitter](https://github.com/scottcorgan/tiny-emitter)-а.

## Использование

Код шины доставляется на страницу в виде бандла "i-react-bus".

В i-bem шина доступна как `Ya.reactBus`, а в коде React-компонента через [метод reactBus()](./ReactBus.ts):

```ts
import { reactBus } from '../components/ReactBus/ReactBus';
```

## FAQ

### Как передать данные из React в i-bem?

1. В i-bem подписываемся на события от React-компонента:

```js
Ya.reactBus.on('popup:open', function(data) {
    // ...
});
```

2. В React-компоненте отправляем событие с данными:

```ts
reactBus().emit('popup:open', data);
```

### Как запросить данные из i-bem в React?

1. В i-bem подписываемся на события и передаём данные в callback:

```js
Ya.reactBus.on('something:get-by-id', params, function(callback) {
    callback(storage.get(params.id));
});
```

2. В React-компоненте запрашиваем данные через событие:

```ts
reactBus().emit('something:get-by-id', { id }, response => {
    // ...
});
```

### Как передать данные из i-bem в React?

1. В React-компоненте подписываемся на события от i-bem:

```ts
reactBus().on('react:do-something', data => {
    // ...
});
```

2. В i-bem отправляем событие с данными:

```js
Ya.reactBus.emit('react:do-something', data);
```

### Куда писать i-bem код про работу с шиной?

Если ваш код должен приезжать для всех React-фичей, то пишем его прямо в [i-react-bus.js](../../../blocks-common/i-react-bus/i-react-bus.js) после объявления шины.

Если ваш код используется не всеми React-фичами или есть только под экспериментом, то пишем его, где удобнее. Но не забываем, что бандл самой шины должен попасть на страницу раньше вашего кода.

### Куда писать React-код про работу с шиной?

Ограничений нет. Бандл с шиной всегда оказывается на странице раньше ассетов с React-компонентами.
