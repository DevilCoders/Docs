# Объекты на карте

В API Яндекс.Карт есть возможность добавлять на карту различные объекты:

- источники данных;
- слои;
- геообъекты;
- маркеры.

## Источники данных {#source}

API Карт разделяет несколько источников данных:

- тайловый источник;
- источник для геообъектов;
- источник для маркеров.

### Тайловый источник данных {#tile-source}

Представляет собой класс `YMapTileDataSource`. Основная задача: хранить данные о том, откуда загружать тайлы и как их отрисовывать.

Основным вариантом использования класса является отображение тайлов по ссылке:

```javascript
const map = new YMap(element, {
  location: {center: [37.588144, 55.733842], zoom: 14},
  mode: 'vector'
});

map.addChild(
  new YMapTileDataSource({
    id: 'myUrlSource',
    raster: {
      // x, y — координаты тайла;
      // z — масштаб (зум);
      // scale — масштабирование для различных DevicePixelRatio.
      tileUrl: 'https://sitename.com/?x={{x}}&y={{y}}&z={{z}}&scale={{scale}}',
      // Опция позволяет дожидаться загрузки всех видимых на экране тайлов до отображения.
      awaitAllTilesOnFirstDisplay: true
    }
  })
);
```

Более расширенным вариантом использования служит ипользование в качестве параметра `raster.tileUrl` асинхронной функции, которая возвращает картинку или `bitmap`:

```javascript
const tileSize = 256;

async function generator(tileX, tileY, tileZ) {
  const canvas = document.createElement('canvas');
  canvas.width = tileSize;
  canvas.height = tileSize;
  const ctx = canvas.getContext('2d');

  ctx.fillStyle = '#000000';
  ctx.fillText(`${tileX}:${tileY}:${tileZ}`, 10, 10);

  return createImageBitmap(canvas);
}

map.addChild(
  new YMapTileDataSource({
    id: 'myTileGeneratorSource',
    raster: {
      tileUrl: generator,
      fetchHotspots: fetchHotspots,
      transparent: true,
      tileRevealDuration: 0,
      size: tileSize
    }
  })
);
```

### Источник данных для геообъектов {#feature-source}

Представляет собой класс `YMapFeatureDataSource`.

Пример создания:

```javascript
map.addChild(
  new YMapFeatureDataSource({
    id: 'myFeatureSource'
  })
);
```

### Источник данных для маркеров {#marker-source}

Представляет собой класс `YMapMarkerDataSource`.

Пример создания:

```javascript
map.addChild(
  new YMapMarkerDataSource({
    id: 'myMarkerSource'
  })
);
```

## Слои {#layers}

Представляют собой аналогию слоеного пирога. Каждый экземпляр `YMapLayer` может отображаться над/под другим экземпляром того же класса.

Очередность отображения можно задавать порядком добавления на карту, а также через параметр `zIndex` (по умолчанию `1500`).

{% note alert "Внимание." %}

Слой является отбражением того или иного источника данных, поэтому источник важно добавлять на карту до добавления слоя.

{% endnote %}

Примеры создания:

```javascript
map.addChild(
  new YMapLayer({
    source: 'myUrlSource',
    // Растровые тайлы доступны только на уровне земли.
    type: 'ground'
  })
);

map.addChild(
  new YMapLayer({
    source: 'myTileGeneratorSource',
    // Тайлы, полученные при помощи функции-генератора, доступны только на уровне земли.
    type: 'ground',
    zIndex: 2000
  })
);

map.addChild(
  new YMapLayer({
    source: 'myMarkerSource',
    type: 'markers',
    zIndex: 2020
  })
);

map.addChild(
  new YMapLayer({
    source: 'myFeatureSource',
    type: 'features',
    zIndex: 2010
  })
);
```

Соответственно, порядок отображения будет следующий:

1. `myUrlSource`
1. `myTileGeneratorSource`
1. `myFeatureSource`
1. `myMarkerSource`

Также для удобства использования предусмотрены слои по умолчанию:

- `YMapDefaultSchemeLayer` — объединяет в себе тайловый источник данных и набор слоев для отображения схематической карты Яндекса.
- `YMapDefaultFeaturesLayer` — объединяет в себе источник данных для геообъектов и слой его отображения.
- `YMapDefaultMarkersLayer` — объединяет в себе источник данных для маркеров и слой его отображения.

## Геообъекты {#geoobjects}

Геообъекты в API представлены двумя типами: ломаная линия и полигон.
Каждый объект описывается геометрией, которая задается типом и координатами, а также стилем отображения. Например, управление цветом фигуры или толщиной линий.

### Ломаная линия {#line}

Тип: `LineString`.

Пример использования:

```javascript
const lineStringFeature = new YMapFeature({
  id: 'myLine',
  source: 'myFeatureSource',
  geometry: {
    type: 'LineString',
    coordinates: [
      [37.40108963847453, 55.70173382087952],
      [37.60954231796791, 55.57717912610197]
    ]
  },
  style: {
    stroke: [{width: 12, color: 'rgb(14, 194, 219)'}]
  }
});

map.addChild(lineStringFeature);
```

### Полигон {#polygon}

Тип: `Polygon`.

Пример использования:

```javascript
const polygonFeature = new YMapFeature({
  id: 'myPolygon',
  source: 'myFeatureSource',
  geometry: {
    type: 'Polygon',
    coordinates: [
      [
        [37.40108963847453, 55.70173382087952],
        [37.60954231796791, 55.57717912610197],
        [37.90954231796791, 55.97717912610197]
      ]
    ]
  },
  style: {
    stroke: [{width: 6, color: 'rgb(14, 194, 219)'}],
    fill: 'rgba(56, 56, 219, 0.5)'
  }
});

map.addChild(polygonFeature);
```

## Маркеры {#markers}

Маркер представляет собой HTML-контейнер, привязанный к точке на карте. Таким образом на карте можно отобразить произвольную верстку.

Пример использования:

```javascript
const myMarkerElement = document.createElement('div');
myMarkerElement.className = 'my-marker-class';
myMarkerElement.innerText = "I'm marker!";

const myMarker = new YMapMarker(
  {
    source: 'myMarkerSource',
    coordinates: [37.631748, 55.737568],
    draggable: true,
    mapFollowsOnDrag: true
  },
  myMarkerElement
);

myMap.addChild(myMarker);
```
