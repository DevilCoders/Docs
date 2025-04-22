# Циклические импорты

Циклические зависимости происходят, когда два или больше модулей ссылаются друг на друга. [Подробнее](https://spin.atomicobject.com/2018/06/25/circular-dependencies-javascript/ )

Некоторые циклические зависимости сборщик может разрешить самостоятельно, но иногда они приводят к ошибках в приложении.

## Где возникают?

Чаще всего циклические импорты возникают в слайсах редакса (`src/slices`), так как слайсы регулярно используют селекторы, экшены и thunk'и из других слайсов.

Также иногда библиотеки используют слайсы, поэтому в цепочке зависимостей могут быть библиотеки (`src/lib`).

## Как выглядит ошибка?

Из-за циклической зависимости при сборке мы будем пытаться импортировать файл, с которого начали сборку. Поэтому экспортируемые из этого файла переменные превратятся в `undefined`.

Обычно в приложении ошибка будет выглядеть как-то так:
<details>
  <summary>Скриншоты</summary>
  <img width="400px" src="https://jing.yandex-team.ru/files/kvas/photo_2020-10-28_20-44-06.jpg"> 
  <img width="400px" src="https://jing.yandex-team.ru/files/kvas/photo_2020-10-28_20-48-17.jpg">
</details>
<br>

## Как найти цикл зависимостей?

Обычно можно вспомнить, что и куда вы недавно заимпортировали, скорее всего это часть цикла. Далее можно попробовать пойти по всем зависимостям этих файлов, чтобы найти цикл, но это бывает сложно и трудозатратно.

Чтобы найти все циклы в проекте, можно подключить [circular-dependency-plugin](https://github.com/aackerman/circular-dependency-plugin). Он работает во время сборки проекта и выдает полный список циклических зависимостей. Однако, если проект не новый, таких циклов там скорее всего очень много, так как некоторые не мешают приложению собраться и рабоать без ошибок.

<details>
  <summary>Пример лога работы `circular-dependency-plugin`</summary>
```
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: ../../packages/tap-components/__internal__/src/helpers/index.js -> ../../packages/tap-components/__internal__/src/helpers/lockBodyScroll/lockBodyScroll.js -> ../../packages/tap-components/__internal__/src/helpers/index.js
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: ../../packages/tap-components/__internal__/src/helpers/lockBodyScroll/lockBodyScroll.js -> ../../packages/tap-components/__internal__/src/helpers/index.js -> ../../packages/tap-components/__internal__/src/helpers/lockBodyScroll/lockBodyScroll.js
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: ../../packages/tap-components/__internal__/src/hooks/index.js -> ../../packages/tap-components/__internal__/src/hooks/useBodyScrollEffect/useBodyScrollEffect.js -> ../../packages/tap-components/__internal__/src/hooks/index.js
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: ../../packages/tap-components/__internal__/src/hooks/useBodyScrollEffect/useBodyScrollEffect.js -> ../../packages/tap-components/__internal__/src/hooks/index.js -> ../../packages/tap-components/__internal__/src/hooks/useBodyScrollEffect/useBodyScrollEffect.js
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: ../../packages/tap-components/__internal__/src/hooks/useWindowSize/useWindowSize.js -> ../../packages/tap-components/__internal__/src/hooks/index.js -> ../../packages/tap-components/__internal__/src/hooks/useWindowSize/useWindowSize.js
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/lib/api/index.ts -> src/redux/index.ts -> src/redux/slices/auth/index.ts -> src/lib/metrika.ts -> src/redux/slices/merchant.ts -> src/lib/api/index.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/lib/event-queue.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/helpers/event.ts -> src/lib/event-queue.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/lib/geolocation.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/getAddressByLocation.ts -> src/lib/geolocation.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/lib/metrika.ts -> src/redux/index.ts -> src/redux/slices/auth/index.ts -> src/lib/metrika.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/auth/index.ts -> src/lib/rum.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/helpers/event.ts -> src/lib/event-queue.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/helpers/event.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/helpers/latest-order.ts -> src/redux/helpers/event.ts -> src/lib/event-queue.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/shared-thunks/index.ts -> src/redux/shared-thunks/pay/index.ts -> src/redux/helpers/latest-order.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/index.ts -> src/redux/slices/auth/index.ts -> src/lib/rum.ts -> src/redux/index.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/shared-selectors/empty-fields.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/getAddressByText.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address-suggest.ts -> src/redux/slices/city.ts -> src/redux/shared-thunks/index.ts -> src/redux/shared-thunks/pay/index.ts -> src/redux/shared-selectors/index.ts -> src/redux/shared-selectors/empty-fields.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/shared-selectors/index.ts -> src/redux/shared-selectors/empty-fields.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/getAddressByText.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address-suggest.ts -> src/redux/slices/city.ts -> src/redux/shared-thunks/index.ts -> src/redux/shared-thunks/pay/index.ts -> src/redux/shared-selectors/index.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/shared-thunks/getAddressByLocation.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/getAddressByLocation.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/shared-thunks/getAddressByText.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/getAddressByText.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/shared-thunks/index.ts -> src/redux/shared-thunks/pay/index.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/shared-thunks/index.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/shared-thunks/pay/index.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/shared-thunks/index.ts -> src/redux/shared-thunks/pay/index.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/shared-thunks/restoreCheckoutState.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/shared-thunks/index.ts -> src/redux/shared-thunks/pay/index.ts -> src/redux/slices/latest-order.ts -> src/redux/shared-thunks/restoreCheckoutState.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/shared-thunks/triggerEvent.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/helpers/event.ts -> src/lib/event-queue.ts -> src/redux/shared-thunks/triggerEvent.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/address-suggest.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address-suggest.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/address.ts -> src/redux/shared-thunks/getAddressByText.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/auth/index.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/auth/index.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/city-suggest.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/city-suggest.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/city.ts -> src/lib/metrika.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/common-addresses.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/common-addresses.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/contacts.ts -> src/lib/metrika.ts -> src/redux/index.ts -> src/redux/slices/auth/index.ts -> src/redux/slices/contacts.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/delivery.ts -> src/redux/helpers/event.ts -> src/lib/event-queue.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/shared-thunks/index.ts -> src/redux/shared-thunks/pay/index.ts -> src/redux/slices/delivery.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/general/index.ts -> src/redux/shared-thunks/restoreCheckoutState.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/general/index.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/geolocation.ts -> src/lib/geolocation.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address-suggest.ts -> src/redux/slices/geolocation.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/latest-order.ts -> src/redux/shared-thunks/restoreCheckoutState.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/shared-thunks/index.ts -> src/redux/shared-thunks/pay/index.ts -> src/redux/slices/latest-order.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/merchant.ts -> src/lib/api/index.ts -> src/redux/index.ts -> src/redux/slices/auth/index.ts -> src/lib/metrika.ts -> src/redux/slices/merchant.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/payment-methods.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/helpers/event.ts -> src/redux/slices/payment-methods.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/payment.ts -> src/redux/shared-thunks/pay/index.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/payment.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/profile-addresses/index.ts -> src/lib/metrika.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/city.ts -> src/redux/slices/profile-addresses/index.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/profile-addresses/thunks.ts -> src/lib/rum.ts -> src/redux/index.ts -> src/redux/slices/address.ts -> src/redux/shared-thunks/saveDeliveryAddresses.ts -> src/redux/slices/profile-addresses/thunks.ts
@yandex-int/turboapp-checkout: Circular dependency detected:
@yandex-int/turboapp-checkout: src/redux/slices/validation-errors/index.ts -> src/lib/metrika.ts -> src/redux/index.ts -> src/redux/slices/validation-errors/index.ts
```
</details>
<br>

## Как исправить циклическую зависимость?

Обычно достаточно понять, какая новая зависимость привела к циклу, и выделить ее из этого файла в отдельный.

Например, если мы заимпортировали селектор из слайса:
```
import { citySelector } from './city';
```
Скорее всего будет достаточно разнести слайс на несколько файлов:
- `index.ts` – описание редьюсера
- `selectors.ts` – селекторы слайса (для случая, если к циклу привел импорт селектора)
- `thunks.ts` – thunk'и слайса (для случая, если к циклу привел импорт thunk'а)
- `types.ts` – типы слайса (для случая, если к циклу привел импорт типа)
- `actions.ts` – экшены слайса (для случая, если к циклу привел импорт экшена). Здесь можно создать экшен через `createAction` и использовать его в `index.ts` через `extraReducers`.
