# Как работает Testament. Mirror

Рендеринг виджета происходит в два этапа:

1. Серверный процессинг — виджет обрабатывается при помощи apiary processor, который запускает контроллер виджета и получает разметку
2. Клиентский рантайм - полученная разметка монтируется в JSDOM и выполняется применение apiary-патчей и гидрация react-компонента

Серверный процессинг выполняется в дочернем nodejs процессе (процессе рендеринга), поэтому необходимо убедиться в том,
что среды выполнения в jest-процессе и процессе ренедеринга - одинаковы.

Для этого testament предоставляет mirror - набор методов, позволяющих синхронизировать среды исполнения. Функционалность
которую хочется синхронизировать представлена в виде слоя (layer). Основная идея слоя заключается в том, что вызывая метод в
основном процессе, он автоматически вызывается и в процессе рендеринга.

### Mirror поставляет 4 слоя
* ApiaryLayer - слой для работы с тестируемым виджетом, используется для получения доступа к view виджета
* JestLayer - слой для работы с jest, используется для моков в тесте
* MandrelLayer - слой для инициализации контекста
* KadavrLayer - слой для установки стэйта кадавра (читай моков бекенда), если это необходимо

Примеры кода будем разбирать позже, а пока просто пример, как Mirror и слои выглядят в коде:

```js
import Mirror from '@yandex-market/testament/mirror';
import JestLayer from '@yandex-market/testament/mirror/layers/jest';
import ApiaryLayer from '@yandex-market/testament/mirror/layers/apiary';
import MandrelLayer from '@yandex-market/testament/mirror/layers/mandrel';
import KadavrLayer from '@yandex-market/testament/mirror/layers/kadavr';

const mirror = new Mirror(); // создать mirror
const jestLayer = new JestLayer(__filename, jest); // создать jest-слой
const mandrelLayer = new MandrelLayer(mandrelConfig); // создать mandrel-слой
const apiaryLayer = new ApiaryLayer(); // создать apiary-слой
const kadavrLayer = new KadavrLayer(kadavrConfig); // создать kadavr-слой

// зарегистрировать слои
await mirror.registerRuntime(jestLayer);
await mirror.registerLayer(mandrelLayer);
await mirror.registerLayer(apiaryLayer);
await mirror.registerLayer(kadavrLayer);
```

По факту, в коде Маркета используются [обертки над Mirror](helpers.md#makemirrortouch-i-makemirrordesktop), но об этом чуть позже.

> Все тесты на Testament будут крутиться вокруг Mirror и его четырех слоев. Далее рассмотрим каждый слой подробнее.
