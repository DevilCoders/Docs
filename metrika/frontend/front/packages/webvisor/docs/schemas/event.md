Структура данных события на странице

```javascript
{
  // Нода с которой было взаимодействие, либо 0, если
  // это рутовая нода aka <html></html>
  target: 123

  // Таймстамп в миллисекундах, отсчет ведется с начала записи
  stamp: 3453

  // Тип события, может принимать одно из следующих значений:
  // mousemove mousedown mouseup focus blur select input change
  // touchmove touchstart touchend touchcancel
  // selection
  // canvasProperty, canvasMethod, zoom, scroll, resize
  type: 'click'

  // Дополнительная информация о событии
  // Структура этого объекта меняется в
  // зависимости от типа. Все описания ниже
  meta: { ... }
}
```

## Описание объекта `meta` для разных типов событий

Для всех событий мыши будут только координаты курсора.

* mousemove
* mousedown
* mouseup
* click

```javascript
  {
    x : 100
    y : 100
  }
```

---

## Событие прокрутки, `x` и `y` будут обозначают горизонтальную и вертикальную прокрутку соответственно. Параметр `page` означает, что была прокрутка непосредственно страница, а не каких-то дочерних элементов.

* scroll

```javascript
  {
    x    : 100
    y    : 100,
    page : false
  }
```

---

#### Для событий выделения текста на странице (кроме выделения текста внутри текстовых полей)

* selection

```javascript
  {
    start     : 10
    end       : 50
    startNode : 213
    endNode   : 215
  }
```

---

#### Для изменения значения инпута или при изменении состояния радио/чекбокса

* input
* change

```javascript
  {
    value   : "hello"
    checked : false
  }
```

---

#### Для тач событий сенсорных экранов

* touchmove
* touchstart
* touchend
* touchcancel
* touchforcechange

```javascript
  {
    touches : [
      {
        id    : "b614d1df-db18-50e4-ea5a-d8a33fe190c5"
        x     : 123.45
        y     : 252.31
        force : 0.0459345
      }
    ]
  }
```

---

#### Событие указывающее, что у элемента canvas нужно вызвать какой-то метод

* canvasMethod

```javascript
  {
    method  : "drawImage"
    args    : ["stringified_blob", "0", "0", "100", "100"]
  }
```

---

#### Событие указывающее, что для элемента canvas нужно установить какое-либо свойство

* canvasProperty

```javascript
  {
    property  : "strokeColor"
    value     : "#0000FF"
  }
```

---

#### Событие изменения масштаба страницы с помощью pinch-to-zoom

* zoom

```javascript
  {
    zoomFrom  : {
      level: 1,
      x: 90,
      y: 30
    },
    zoomTo    : {
      level: 4.754,
      x: 120,
      y: 140
    },
    duration  : 30
  }
```
---

#### Изменение размера окна браузера

* resize

```javascript
  {
    width       : 1400
    height      : 900
    pageWidth   : 1400
    pageHeight  : 1780
  }
```

---

#### Событие указывающее, что у элемента video/audio нужно вызвать какой-то метод

* mediaMethod

```javascript
  {
    method  : "play"
    args    : []
  }
```

---

#### Событие указывающее, что для элемента video/audio нужно установить какое-либо свойство

* mediaProperty

```javascript
  {
    property  : currentTime
    value     : "1345"
  }
```

---

#### Событие комбинаций клавиш

* keystroke

```javascript
  [{
    id        : 93,
    key       : 'Win'
    isMeta    : true,
    modifier  : 'super'
  }]
```

#### События iframe

* framecreate

Содержит в `meta` все данные из [page](./initial_html.md)

* framemutate

Содержит в `meta` все данные их [mutation](./mutation.md)

* frameevent

Может содержать в `meta` любые события, описанные в этом
файле, кроме:

- deviceRotation
- zoom
- window
- resize
