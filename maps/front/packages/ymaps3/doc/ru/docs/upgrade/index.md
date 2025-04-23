# Руководство по переходу на JS API 3.0

Руководство содержит примеры, демонстрирующие различия между JavaScript API версий 3.0 и 2.1.
Так как API отличны в корне, в этом разделе освещены лишь различия в базовых компонентах и подходах.

## Подключение API {#load-api}

## Версия 2.1 {#load-api-2-1}

```html
<!DOCTYPE html>
  <head>
    <!-- Загружаем API -->
    <script src="https://api-maps.yandex.ru/2.1/?apikey=<ваш API-ключ>&lang=ru_RU"
    type="text/javascript"></script>
    <script type="text/javascript">
      // При успешной загрузке API выполняется
      // соответствующая функция.
      ymaps.ready(function () {
         …
      });
    </script>
   </head>
  ...
</html>
```

## Версия 3.0 {#load-api-3-0}

```html
<!DOCTYPE html>
  <head>
    <!-- Загружаем API -->
    <script src="https://api-maps.yandex.ru/3.0-beta/?apikey=<ваш API-ключ>&lang=ru_RU"
    type="text/javascript"></script>
    <script type="text/javascript">
      // При успешной загрузке API доступен промис `ymaps3.ready`
      ymaps3.ready.then(() => {
         …
      });
    </script>
   </head>
  ...
</html>
```

Обязательные параметры:

- `apikey` — API-ключ. [Как получить ключ](../quick-start/index.md#get-api-key);
- `lang` — язык.

{% note alert "Важно." %}

В API 3.0 раздельная подзагрузка модулей по требованию отсутствует.
Нет параметра `onload`. Единственный способ выполнить код после готовности API — это промис `ymaps3.ready`.

{% endnote %}

## Создание карты {#create-map}

### Версия 2.1 {#create-map-2-1}

```js
// Создание экземпляра карты
// и его привязка к
// контейнеру с id="YMapsID".
const myMap = new ymaps.Map('YMapsID', {
  center: [55.76, 37.64],
  zoom: 10,
  type: 'yandex#satellite',
  // Карта будет создана без
  // элементов управления.
  controls: []
});
```

### Версия 3.0 {#create-map-3-0}

```js
// Создание экземпляра карты.
const myMap = new ymaps3.YMap(document.getElementById('YMapsID'), {
  location: {
    center: [37.64, 55.76],
    zoom: 10
  }
});
```

{% note info "Примечание." %}

В API 3.0 нет слоя со спутниковыми данными. Если вам необходим такой слой, то вы можете создать его сами,
указав url для получения тайлов.

{% endnote %}

## Поведения {#behaviors}

### Версия 2.1 {#behaviors-2-1}

По умолчанию включены следующие поведения: `drag`, `multiTouch`, `dblClickZoom`, `rightMouseButtonMagnifier`, `scrollZoom`.

### Версия 3.0 {#behaviors-3-0}

Полный список поведений приведен в разделе [События](../dg/concepts/events.md#behavior-type).

По умолчанию включены следующие поведения: `drag`, `scrollZoom`, `pinchZoom`, `dblClick`, `magnifier`.

## Геообъекты {#geoobjects}

### Задание стиля метки {#style}

#### Версия 2.1 {#style-2-1}

```js
// Метка с одним из стандартных значков.
// Список стандартных стилей приведен
// в справочнике в разделе
// option.preset.storage.
var myPlacemark = new ymaps.Placemark(
  [55.8, 37.6],
  {},
  {
    preset: 'islands#greenCircleIcon'
  }
);

// Создание метки с собственным значком.
var myPlacemark2 = new ymaps.Placemark(
  [55.8, 37.6],
  {},
  {
    // Один из двух стандартных макетов
    // меток со значком-картинкой:
    // - default#image - без содержимого;
    // - default#imageWithContent - с текстовым
    // содержимым в значке.
    iconLayout: 'default#image',
    iconImageHref: '/path/to/icon.png',
    iconImageSize: [20, 30],
    iconImageOffset: [-10, -20]
  }
);
```

#### Версия 3.0 {#style-3-0}

```js
const defaultMarker = new ymaps3.YMapDefaultMarker({
  title: 'Привет мир!',
  subtitle: 'Добрый и светлый',
  color: 'blue'
});

const content = document.createElement('div');
const marker = new ymaps3.YMapMarker(content);
content.innerHTML = '<div>Тут может быть все что угодно</div>';

const map = new ymaps3.YMap(document.getElementById('map-root'), {
  location: INITIAL_LOCATION
})
  .addChild(new ymaps3.YMapDefaultSchemeLayer())
  .addChild(new ymaps3.YMapDefaultMarkersLayer({zIndex: 1800}))
  .addChild(defaultMarker)
  .addChild(marker);
```

В API 3.0 есть лишь один дефолтный тип маркеров: `YMapDefaultMarker`.

Для кастомных маркеров используйте `YMapMarker`. Он позволяет использовать любые HTML внутри.

## Кластеризация {#clusterer}

### Версия 3.0 {#clusterer-3-0}

В API 3.0 нет механизма кластеризации.

## Элементы управления картой {#controls}

### Версия 3.0 {#controls-3-0}

По умолчанию карта создается без стандартных элементов управления: полноэкранный режим, кнопки масштаба, геолокация.
О том, как добавить на карту необходимые элементы управления, см. в разделе [Элементы управления](../dg/concepts/controls/controls_index-page.md).

В API 3.0 остались только три элемента управления: геолокация, кнопки масштаба и обычная кнопка. [Подробнее](../dg/concepts/controls/standard.md)

## Балун {#balloon}

### Версия 3.0 {#balloon-3-0}

В API 3.0 нет встроенного всплывающего окна. Вместо этого вы можете самостоятельно управлять содержимым HTML-элемента маркера.
