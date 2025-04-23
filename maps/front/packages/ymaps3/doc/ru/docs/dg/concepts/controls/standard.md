# Стандартные визуальные элементы

## Геолокация {#geolocation}

Позволяет определить местоположение пользователя путем вызова стандартной геолокационной функции браузера
и/или по IP-адресу пользователя.

Класс: `YMapGeolocationControl`.

**Пример**

Добавление кнопки геолокации:

```javascript
const map = new YMap(element, {
  location: {center: [37.588144, 55.733842], zoom: 14}
});

const controls = new YMapControls();
controls.addChild(new YMapGeolocationControl());

map.addChild(controls);
```

## Кнопки масштаба {#zoom}

Позволяет изменять коэффициент масштабирования карты.

Класс: `YMapZoomControl`.

Для настройки масштабирования карты используются следующие параметры:

- `easing`. Возможные значения: `linear`, `ease`, `ease-in`, `ease-out`, `ease-in-out`.
- `zoomRange`. Если текущий масштаб выходит за пределы этой настройки, то кнопки увеличения или уменьшения масштаба блокируются.

**Пример 1**

Использование параметра `easing`:

```javascript
const map = new YMap(element, {
  location: {center: [37.588144, 55.733842], zoom: 14}
});

const controls = new YMapControls();
controls.addChild(
  new YMapZoomControl({
    easing: 'linear'
  })
);

map.addChild(controls);
```

**Пример 2**

Использование параметра `easing` и `zoomRange`:

```javascript
const map = new YMap(element, {
  zoomRange: [1, 5],
  location: {center: [37.588144, 55.733842], zoom: 4}
});

const controls = new YMapControls();
controls.addChild(
  new YMapZoomControl({
    easing: 'linear'
  })
);

map.addChild(controls);
```

## Кнопка {#button}

Позволяет добавить стандартную кнопку и настроить для нее произвольное поведение.

Класс: `YMapButtonControl`.

**Пример**

```javascript
const button = new YMapControlButton({
  text: 'Привет',
  onClick: () => alert('Привет Мир!')
});
```
