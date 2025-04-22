# Общие сведения

JavaScript API 3.0 Яндекс.Карт представляет собой набор JavaScript-классов, предназначенных для размещения интерактивных карт на веб-страницах. API не имеет зависимостей и для работы не требует компиляции или подключения View-движка (React, Vue, Angular).

Для React есть [обертка](#react), которая повторяет JavaScript API.

В API используется следующее соглашение: названия всех классов начинаются с заглавной буквы с префиксом `Y` и пишутся в стиле **CamelCase**. Примеры: `YMap`, `YMapMarker`.

{% note info "Примечание." %}

Для использования JavaScript API Яндекс.Карт необходимо [получить ключ](../../quick-start/index.md#get-api-key).

{% endnote %}

## Пространства имен {#namespaces}

Все компоненты API попадают в единое пространство имен `ymaps3`. После подключения JS&nbsp;API&nbsp;3.0 все объекты доступны как `ymaps3.YMap`, `ymaps3.YMapMarker` и т.д.

Для простоты восприятия в документации все классы упоминаются без пространства имен.

## Верстка {#markup}

При формировании интерактивной карты происходит динамическое формирование HTML-кода и внедрение его в DOM-дерево страницы,
на которой размещена карта.

В большинстве случаев в генерируемом коде используются не стандартные HTML-элементы (`img`, `div` и т. д.), а элемент `ymaps`.
Кроме того, все стилевое оформление генерируемого API кода базируется на CSS-классах, имеющих префикс `ymaps3x0`,
а CSS API использует селекторы только этих классов.

Это позволяет свести вероятность конфликтов верстки к минимуму. Если в HTML-коде пользователя не используется элемент `ymaps`,
а пользовательские CSS-определения не содержат классов с префиксом `ymaps3x0`, конфликтов верстки не будет.
То есть CSS пользователя не будет влиять на отображение карты и ее элементов, а CSS API не будет влиять на верстку пользователя.

## Объекты карты {#objects}

<table>
  <thead>
    <tr>
      <th align="center">Название</th>
      <th align="center">Описание</th>
      <th align="center">Представление в API</th>
    </tr>
    </thead>
  <tbody>
    <tr>
      <td><a href="#map">Карта</a></td>
      <td>Основной объект, который координирует свои составляющие.</td>
      <td>Класс <code>YMap</code></td>
    </tr>
    <tr>
      <td><a href="#layers">Слой</a></td>
      <td>Объект для отображения данных.</td>
      <td>Классы с постфиксом <code>Layer</code></td>
    </tr>
    <tr>
      <td><a href="#source">Источник данных</a></td>
      <td>Объект для загрузки данных, передает их для отображения в слои.</td>
      <td>Классы с постфиксом <code>DataSource</code></td>
    </tr>
    <tr>
      <td><a href="#markers">Маркер</a></td>
      <td>Элемент карты с DOM-содержимым.</td>
      <td>Класс <code>YMapMarker</code></td>
    </tr>
    <tr>
      <td><a href="map-objects.html#geoobjects">Геообъект</a></td>
      <td>Полигон, линия.</td>
      <td>Класс <code>YMapFeature</code></td>
    </tr>
    <tr>
      <td><a href="controls/controls_index-page.html#visual">Визуальные элементы</a></td>
      <td>Объекты, которые используются для управления состоянием карты: кнопка изменения масштаба, кнопка геолокации и т.п.</td>
      <td>Классы с постфиксом <code>Control</code></td>
    </tr>
    <tr>
      <td><a href="controls/controls_index-page.html#behaviors">Поведения</a></td>
      <td>Объекты, которые определяют действия пользователя с помощью мыши и жестов, без визуальных элементов.</td>
      <td>Поле <code>behaviors</code> карты</td>
    </tr>
    <tr>
      <td>Утилиты</td>
      <td>Вспомогательные объекты для работы с API. Например, <code>YMapListener</code> отвечает за подписку на события карты.</td>
      <td>Класс <code>YMapListener</code>, обработчики с постфиксом <code>EventHandler</code></td>
    </tr>
  </tbody>
</table>

## Иерархия объектов карты {#map-hierarchy}

Некоторые объекты карты (например, сама карта) могут содержать внутренние узлы — потомки. Другие же (например, `YMapMarker`) не обладают этой функциональностью.

### Карта {#map}

Корневым элементом в иерархии объектов API является карта. При инициализации карты указывается контейнер, в котором она размещается, и [опции](#object-options).

```html
<div id="root"></div>
```

```javascript
const map = new YMap(document.getElementById('root'), {
  location: {
    zoom: 10,
    center: [37.588144, 55.733842]
  }
});
```

Остальные элементы добавляются в карту с помощью методов `addChild()` и `removeChild()`.

### Слои {#layers}

Карта может содержать произвольное количество слоев. Слой — это визуальный компонент, который отвечает за
отрисовку слоя определенного содержания. Например, слой маркеров отображает точки на карте, а тайловый слой — саму географическую карту.

API никак не ограничивает количество слоев. Разработчик может добавить слой, на котором будут отображены облака (картинка),
и разместить его поверх тайлового слоя, а посередине добавить слой пробок.

{% note alert "Внимание." %}

Порядок добавления слоев важен. Если разместить слой маркеров под тайловым, то конечный пользователь не увидит маркеры.

{% endnote %}

### Источники данных {#source}

Каждый слой для отображения должен откуда-то брать данные — для этого есть объекты с постфиксом `DataSource`. Например, `YMapTileDataSource` используется для загрузки данных по тайлам.

Создание источника данных `YMapTileDataSource`:

```javascript
const ds = new YMapTileDataSource({
  id: 'scheme',
  raster: {
    tileUrl: 'https://sitename.com/?x={{x}}&y={{y}}&z={{z}}&scale={{scale}}'
  }
});
map.addChild(ds);
```

После этого слои могут отобразить информацию с этого источника данных:

```javascript
const ground = new YMapLayer({zIndex: 1, source: 'scheme', type: 'ground'});
const buildings = new YMapLayer({
  zIndex: 2,
  source: 'scheme',
  type: 'buildings'
});
const icons = new YMapLayer({zIndex: 3, source: 'scheme', type: 'icons'});
const labels = new YMapLayer({zIndex: 4, source: 'scheme', type: 'labels'});
map.addChild(ground).addChild(buildings).addChild(icons).addChild(labels);
```

Чтобы не делать это каждый раз вручную, в JS API есть пренастроенные слои:

- `YMapDefaultMarkersLayer` — отображает метки на карте.
- `YMapDefaultFeaturesLayer` — отображает геообъекты: полигоны, линии, точки.
- `YMapDefaultSchemeLayer` — загружает и отображает слои строений, подписей и т.п.

Пример использования:

```javascript
map.addChild(new YMapDefaultSchemeLayer({theme: 'dark'}));
```

### Маркеры {#markers}

Маркеры — это точки на карте, которые можно перетаскивать. Для маркеров можно задать собственный внешний вид.
JS API предоставляет свободу выбора для дизайна: при инициализации объект `YMapMarker` принимает DOM-элемент,
а в нем вы можете отобразить любое HTML-содержимое.

Пример использования:

```javascript
const map = new YMap({...});
map.addChild(new YMapDefaultSchemeLayer()); // Слой дорог, зданий и т.п.
map.addChild(new YMapDefaultMarkersLayer()); // В этом слое будут маркеры.
// DOM-элемент должен быть создан заранее, но его содержимое можно задать в любой момент.
const content = document.createElement('section');
const marker = new YMapMarker({
    coordinates: [37.588144, 55.733842],
    draggable: true
}, content);
map.addChild(marker);
content.innerHTML = '<h1>Этот заголовок можно переносить</h1>';
```

## Опции объектов {#object-options}

В примерах выше каждый созданный объект принимает опции при инициализации. Опции могут быть обязательными и опциональными.
Например, поле `location` для карты — обязательное. Все опции можно изучить в [справочнике](../../ref/index.md).

```javascript
const map = new YMap(document.getElementById('root'), {
  location: {
    zoom: 10,
    center: [37.588144, 55.733842]
  },
  behaviors: ['drag', 'scrollZoom', 'pinchZoom', 'dblClick']
});
```

## React {#react}

Для каждого объекта в JS API есть React-аналог. Иерархия объектов и опции те же самые:

```javascript
<YMap location={{center, zoom}} mode="vector">
  <YMapDefaultSchemeLayer />
  <YMapDefaultMarkersLayer />
  <YMapMarker coordinates={[34, 57]} draggable={true}>
    <div className="marker marker_pill">I'm marker!</div>
  </YMapMarker>
</YMap>
```
