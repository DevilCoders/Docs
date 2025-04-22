# События

В API Яндекс.Карт реализован собственный механизм работы с событиями. Для работы с событиями браузера, окна браузера и DOM-дерева, а также для работы с объектами API используется событийная модель API Яндекс.Карт.

Использование событий реализуется через установку обработчиков — изменение состояния экземпляра класса [YMapListener](../../ref/index.md#classesymaplistenermd), который присоединяется в виде потомка корневого объекта карты [YMap](../../ref/index.md#classesymapmd).

## Инициализация слушателя {#listener-init}

```javascript
const clickCallback = () => alert('О, событие!');
const mouseMoveCallback = () => console.log('Я двигаю мышью...');

// Создание объекта-слушателя.
const mapListener = new YMapListener({
  layerId: 'any',
  // Добавление обработчиков на слушатель.
  onClick: clickCallback,
  onMouseMove: mouseMoveCallback
});

// Добавление слушателя на карту.
map.addChild(mapListener);
```

## Интерфейс передаваемого обработчика {#handler-interface}

Передаваемые в слушатель обработчики имеют следующие интерфейсы в зависимости от [типа события](#list-of-events), которое они обрабатывают:

- [MapEventHandler](#handlers-list-map-event-handler)
- [DomEventHandler](#handlers-list-dom-event-handler)
- [BehaviorEventHandler](#handlers-list-behavior-event-handler)

### `MapEventHandler` {#handlers-list-map-event-handler}

Обработчик `MapEventHandler` служит для обработки [событий карты](#events-list-map-event-handler).

Обработчик вызывается со следующими параметрами:

- `camera` — объект камеры [YMapCamera](#);
- `size` — размер контейнера карты в [PixelCoordinates](#).

Пример использования:

```javascript
const updateHandler = (camera, size) => {
  console.log(camera.zoom, camera.worldCenter);

  console.log(size.x, size.y);
};
```

### `DomEventHandler` {#handlers-list-dom-event-handler}

Обработчик `DomEventHandler` служит для обработки [событий DOM](#domeventhandler).

Обработчик вызывается со следующими параметрами:

- `layerId` — уникальное имя слоя;
- `coordinates` — географические координаты места на карте, соответствующего точке DOM, в котором произошло событие;
- `object` — _опциональный параметр_ — объект карты [MapObject](#), на котором произошло событие. Если нажатие было совершено не на объект карты, передается `null`.

Пример использования:

```javascript
const clickHandler = (layerId, coordinates, object) => {
  if (object?.type === 'hotspot') {
    console.log('Clicked on hotspot!');
  }
};
```

При добавлении обработчика DOM-событий в слушатель необходимо задать `layerId` — идентификатор слоя, после возникновения события в котором вызывается соответствующий обработчик:

```javascript
// Создание нового слушателя.
const mapListener = new YMapListener({
  layerId: 'any',
  onClick: clickHandler
});

// Обновление уже существующего слушателя.
mapListener.update({
  onClick: anotherClickHandler
});

// Обновление идентификатора, если необходимо
// или если значение не было передано при инициализации.
mapListener.update({
  layerId: 'ground',
  onClick: clickHandler
});
```

### `BehaviorEventHandler` {#handlers-list-behavior-event-handler}

Обработчик `BehaviorEventHandler` служит для разграничения типов событий, с которыми [можно работать](#events-list-behavior-event-handler) в API Карт.

Обработчик вызывается с параметром `behavior` — [типом поведения](#behavior-type), которое произошло на карте:

```javascript
const behaviorHandler = (behavior) => {
  if (behavior === 'pinchRotate') {
    console.log('Пользователь вращает карту жестами!');
  }
};

mapListener.update({onActionStart: behaviorHandler});
```

Обработчик поведения, привязываемый на `onActionStart`, вызывается перед всеми обработчиками `MapEventHandler` и `DomEventHandler`. В свою очередь, обработчики поведения, привязываемые на `onActionEnd`, вызываются последними:

```javascript
const behaviorStartHandler = (behavior) => {
  if (behavior === 'dblClick') {
    console.log('1. Started double click.');
  }
};

const behaviorEndHandler = (behavior) => {
  if (behavior === 'dblClick') {
    console.log('3. Finished double click.');
  }
};

const dblClickHandler = () => console.log('2. Double click.');

mapListener.update({
  onActionStart: behaviorStartHandler,
  onActionEnd: behaviorEndHandler,
  dblClick: dblClickHandler
});
```

## Удаление обработчиков {#remove}

Все обработчики автоматически отвязываются, когда `YMapListener` перестает быть потомком `YMap`:

```javascript
map.removeChild(mapListener); // mapListener — экземпляр класса YMapListener.
```

Также возможно отвязать лишь некоторые обработчики:

```javascript
mapListener.update({
  onClick: clickHandler,
  dblClick: dblClickHandler,
  onFastClick: fastClickHandler
});

// Позднее, когда один из обработчиков перестал быть нужен.
// Удаление обработчика dblClick.
mapListener.update({
  dblClick: null
});
```

## Поддерживаемые события {#list-of-events}

Конструктор объекта класса `YMapListener` и метод `update()` принимают объект со свойствами ниже. Каждое из этих свойств представляет собой обработчик, который вызывается после срабатывания соотвествующего свойству события.

### `MapEventHandler` {#events-list-map-event-handler}

- `onUpdate` — событие, срабатывающее при изменении состояния карты;
- `onResize` — событие, срабатывающее при изменении размера карты;
- `onIndoorPlansChanged` — событие, срабатывающее при изменении внутреннего отображения здания.

### `DomEventHandler` {#events-list-dom-event-handler}

- `onTouchStart` — событие, аналогичное нативному `'touchstart'`;
- `onTouchMove` — событие, аналогичное нативному `'touchmove'`;
- `onTouchEnd` — событие, аналогичное нативному `'touchend'`;
- `onTouchCancel` — событие, аналогичное нативному `'touchcancel'`;
- `onPointerDown` — событие, аналогичное нативному `'pointerdown'`;
- `onPointerMove` — событие, аналогичное нативному `'pointermove'`;
- `onPointerUp` — событие, аналогичное нативному `'pointerup'`;
- `onPointerCancel` — событие, аналогичное нативному `'pointercancel'`;
- `onClick` — событие, срабатывающее при нажатии левой кнопкой мыши после небольшой задержки _(необходима, чтобы отличить клик от двойного клика)_;
- `onDblClick` — событие, срабатывающее при двойном нажатии левой кнопкой мыши;
- `onFastClick` — событие, аналогичное нативному `'click'`;
- `onRightDblClick` — событие, срабатывающее при двойном нажатии правой кнопкой мыши;
- `onMouseDown` — событие, аналогичное нативному `'mousestart'`;
- `onMouseEnter` — событие, аналогичное нативному `'mouseenter'`;
- `onMouseLeave` — событие, аналогичное нативному `'mouseleave'`;
- `onMouseMove` — событие, аналогичное нативному `'mousemove'`;
- `onContextMenu` — событие, аналогичное нативному `'contextmenu'`.

### `BehaviorEventHandler` {#events-list-behavior-event-handler}

- `onActionStart` — событие, срабатывающее при старте какого-либо действия, связанного с картой;
- `onActionEnd` — событие, срабатывающее после завершения какого-либо действия, связанного с картой.

#### Типы поведений {#behavior-type}

- `drag` — перетаскивание объекта;
- `pinchZoom` — приближение/отдаление жестом (двумя пальцами);
- `scrollZoom` — приближение/отдаление колесом мыши;
- `dblClick` — двойное нажатие мыши;
- `magnifier` — выделение прямоугольной области карты зажатием правой кнопки мыши и приближение карты к выделенному прямоугольнику по следующему принципу: длина выделенного прямоугольника составляет 100% ширины видимой области контейнера карты после приближения;
- `oneFingerZoom` — приближение/отдаление одним пальцем;
- `mouseRotate` — поворот карты мышью;
- `mouseTilt` — наклон карты мышью;
- `pinchRotate` — поворот карты жестом;
- `panTilt` — наклон карты жестом.
