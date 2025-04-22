## Описание

Блок `slider` («слайдер») —  управляющий элемент интерфейса для удобного и наглядного выбора диапазона значений.
Позволяет создавать следующие разновидности слайдеров:

* **с одним ползунком** — для выбора одного значения из диапазона.
* **с двумя ползунками** — для выбора диапазона значений.
* **с равномерной шкалой** — движение ползунка по шкале происходит равномерно с постоянным шагом.
* **с неравномерной шкалой** — движение ползунка по шкале происходит неравномерно с изменяющимся значением шага.

Поля ввода и ползунки связаны – значения полей `input` синхронно изменяются при перетягивании ползунков.
Блок предоставляет возможность настройки визуального отображения слайдера.

Примеры использования:

* В интернет-магазинах — выбор цен.
* При поиске автомобилей — выбор диапазона [пробег, год выпуска, объем двигателя].

В версиях браузера MSIE ниже 8 `input`-ы (элементы блока `slider`) деградируют до нативных полей ввода.

---
**NB** Реализация блока разнесена на отдельные компоненты в элементы:
`math` — функции для расчетов и `ui` — отрисовка внешнего вида.

---

---
**NB** В блоке не реализована возможность ленивой инициализации.

---

### Объявление блока на странице

BEMJSON для использования слайдера:

```javascript
{
    block: 'slider', // имя блока
    /* модификаторы. Модификаторы theme, size, orientation – обязательные*/
    mods: {theme: 'normal', size: 'm', orientation: 'horiz'},
    js: {
        /* [min, max] – область допустимых значений (не обязательные параметры)*/
        min: 10,  // минимальное значение диапазона
        max: 300, // максимальное  значение диапазона
        scale: [  // шкала слайдера (состоит из отрезков)
            {value: 0, step: 10, label: '0'},  // начальное значение, шаг, метка
            {value: 10, step: 5, label: '10', percent: 10},
            {value: 40, step: 10, percent: 40}, // промежуточное значение
            {value: 300, step: 20, label: '300', percent: 80},
            {value: 500, label: '500'} // конечное значение, метка
        ]
    },
    content: {
        elem: 'info', // информационные элементы слайдера: title, input, unit
        elemMods: {preset: 'inline'}, // расположение элементов в одну линию
        content: [
            {
                elem: 'title', // заголовок
                content: 'Цена'
            },
            {
                block: 'input', // поле ввода, связанное с ползунком
                mods: {size: 'm'},
                content: {elem: 'control'},
                value: 40 // значение в инпуте, задает начальное положение
            },
            {
                elem: 'unit', // единица измерения
                content: 'руб.'
            }
        ]
    }
}
```

Входные данные блока для настройки слайдера:

### Ползунки

* **количество ползунков** задается во входных данных количеством блоков [input](../input/input.ru.md).
* **положение ползунков**  задается значением `value` блока `input`.
* **слайдер с двумя ползунками** – для выбора диапазона значений. Во входных данных слайдера должен быть модификатор `type` со значением `range`.
* **ширину ползунка** можно установить во входном BEMJSON блока в JS-параметре [runnerWidth](https://github.yandex-team.ru/lego/islands/blob/dev/common.blocks/slider/__ui/slider__ui.js#L349).


```js
{
    block: 'slider',
    mods: {theme: 'normal',  size: 'm', orientation: 'horiz'},
    js: {
        scale: [
            {value: 0, step: 10, label: '0'},
            {value: 100, label: '100'}
        ],
        runnerWidth: 60
    },
    content: {
        elem: 'info',
        elemMods: {preset: 'inline'},
        content: [
            {
                elem: 'title',
                content: 'Цена'
            },
            {
                block: 'input',
                mods: {size: 'm'},
                content: {elem: 'control'},
                value: 50
            },
            {
                elem: 'unit',
                content: 'руб.'
            }
        ]
    }
}
```

В islands 4.2.0 добавлены методы блока [toDisplay](https://lego.yandex-team.ru/libs/islands/v4.3.0/desktop/slider/jsdoc/#toDisplay) и [fromDisplay](https://lego.yandex-team.ru/libs/islands/v4.3.0/desktop/slider/jsdoc/#fromDisplay), переопределив которые можно задать произвольный формат для отображения значений ползунка. [Пример формата для выбора часов работы](https://lego.yandex-team.ru/libs/islands/v4.3.0/desktop/slider/examples/#custom).

[Пример](https://github.yandex-team.ru/lego/islands/blob/v4.3.0/common.blocks/slider/slider.examples/custom.blocks/slider/slider.js) переопределения:

```javascript
BEM.DOM.decl('slider', {
    toDisplay: function(num) {
        return ('0' + num + ':00').slice(-5);
    },

    fromDisplay: function(str) {
        // В IE8 parseInt приведет '01' к 0.
        return parseFloat(str.split(':')[0]);
    }
});
```

### Область допустимых значений

* Элемент слайдера `allowed-range` — область допустимых значений (в HTML находится всегда).
* Необязательные JS-параметры слайдера [`min`, `max`] — динамические ограничения для области допустимых значений (диапазон):
  * `{Number} min` – минимальное значение диапазона.
  * `{Number} max` – максимальное значение диапазона.

Интервал, расположенный в области допустимых значений, визуально выделяется другим цветом (серый), нежели основная шкала (светло-серый).

---
**NB**: сейчас ползунки выходят за область допустимых значений. На данный момент договорились, что область допустимых значений просто подсказка для пользователя, а не ограничение. Планируется сделать параметр, который будет управлять этой функциональностью.

---

### Построение шкалы и ее параметры

Шкала слайдера (элемент `scale`) строится из отрезков (в HTML — элемент блока `range`).
Количество отрезков шкалы слайдера `range` = (количество ползунков + 1).

JS-параметры, отвечающие за построение и внешний вид шкалы:

* `{Number} value` — значение, обязательный параметр.

* `{Number} step` — шаг от текущего значения до следующего. Обязателен для всех значений, кроме последнего.

* `{Number} percent` — процент от общей ширины шкалы. Если на шкале есть промежуточные значения, то для них параметр `percent` обязателен.

  * `percent` = 0% (всегда для первого значения).
  * `percent` = 100% (всегда для последнего значения).

* `{String} label` — отвечает за визуальное отображение значений, необязательный параметр (BEMJSON). Границы отрезков слайдера можно обозначить «черточками», с использованием параметра `label: ' '`.

```js
{
    block: 'slider',
    mods: {theme: 'normal',  size: 'm', orientation: 'horiz'},
    js: {
        min: 10,
        max: 300,
        scale: [
            {value: 0, step: 10, label: ' '},
            {value: 10, step: 5, label: ' ', percent: 10},
            {value: 40, step: 10, label: ' ', percent: 40},
            {value: 300, step: 20, label: ' ', percent: 80},
            {value: 500, label: ' '}
        ]
    },
    content: {
        elem: 'info',
        elemMods: {preset: 'inline'},
        content: [
            {
                elem: 'title',
                content: 'Цена'
            },
            {
                block: 'input',
                mods: {size: 'm'},
                content: {elem: 'control'},
                value: 40
            },
            {
                elem: 'unit',
                content: 'руб.'
            }
        ]
    }
}
```

Шкала со [значениями по умолчанию](#defscale)

```javascript
{ // слайдер со значениями по умолчанию для шкалы
    block: 'slider',
    mods: {theme: 'normal',  size: 'm', orientation: 'horiz'},
    js: true,
    content: {...}
}
```

### Информационные элементы

Элемент `info` — содержит информационные элементы слайдера:

  * `title` – заголовок.
  * `input` – поля ввода.
  * `unit` – единицы измерения.

Для удобного изменения расположения элементов внутри элемента `info` стили по умолчанию были вынесены в модификатор — `preset`.
Модификатор элемента `preset` со значением `inline` выведет элементы `title`, `input` и `unit` в одну строку. Можно задать и свое расположение элементов.

```javascript
{
    block: 'slider',
    mods: {theme: 'normal',  size: 'm', orientation: 'horiz'},
    content: {
        elem: 'info', // информационные элементы слайдера: title, input, unit
        elemMods: {preset: 'inline'}, // расположение элементов в одну линию
        content: [/* массив информационных элементов */]
    }
}
```

### Модификаторы

#### Типы слайдеров
Для выбора диапазона значений используется **слайдер с двумя ползунками**. Для этого во входных данных должен быть обязательно выставлен модификатор `type` со значением `range`.
Интервал между бегунками визуально выделяется желтой подсветкой.

```js
{
    block: 'slider',
    mods: {type: 'range', theme: 'normal', size: 'm', orientation: 'horiz'},
    js: {
        min: 10,
        max: 90,
        scale: [
            {value: 0, step: 10},
            {value: 100}
        ]
    },
    content: {
        elem: 'info',
        elemMods: {preset: 'inline'},
        content: [
            {
                elem: 'title',
                content: 'Цена'
            },
            {
                block: 'input',
                mods: {size: 'm'},
                value: 30,
                content: {elem: 'control'}
            },
            {
                block: 'input',
                mods: {size: 'm'},
                value: 70,
                content: {elem: 'control'}
            },
            {
                elem: 'unit',
                content: 'руб.'
            }
        ] 
    }
}
```

#### Ориентация шкалы

Модификатор `orientation` – определяет ориентацию шкалы слайдера для движения ползунка. Может принимать значения `horiz` (горизонтальный слайдер).
Модификатор `orientation` – обязательный при объявлении блока (по умолчанию не определен).

```javascript
{
    block: 'slider',
    mods: {type: 'range', theme: 'normal', size: 'm', orientation: 'horiz'},
    ...
}
```

#### Темы оформления

Для блока `slider` реализована одна тема оформления – обычная (модификатор `theme` со значением `normal`) для горизонтального слайдера.
Модификатор темы `theme` – обязательный (по умолчанию не определен).

#### Размеры

Для горизонтального слайдера реализован модификатор размера `size`. Может принимать значения `s` и `m`, которые определяют размер шрифта информационных элементов, размеры бегунка, и поля ввода (элемент `input`). Высота поля ввода зависит о размера шрифта и `line-height`.  Модификатор размера – обязательный (по умолчанию не определен).
Если в инпуте явно не задан модификатор размера, то ему будет выставлено значение модификатора `size` из слайдера.

Высота блока `slider` соответствует высоте [кнопки](../button/button.ru.md).

Размер s:

```js
{
    block: 'slider',
    mods: {theme: 'normal', size: 's', orientation: 'horiz', input: 'hidden'},
    js: {
        min: 10,
        max: 90,
        scale: [
            {value: 0, step: 40},
            {value: 100}
        ]
    },
    content: {
        elem: 'info',
        elemMods: {preset: 'inline'},
        content: [
            {
                elem: 'title',
                content: 'Цена'
            },
            {
                block: 'input',
                mods: {size: 's'},
                value: 70,
                content: {elem: 'control'}
            },
            {
                elem: 'unit',
                content: 'руб.'
            }
        ]
    }
}
```

Размер m:

```js
{
    block: 'slider',
    mods: {theme: 'normal', size: 'm', orientation: 'horiz', input: 'hidden'},
    js: {
        min: 10,
        max: 90,
        scale: [
            {value: 0, step: 50},
            {value: 300}
        ]
    },
    content: {
        elem: 'info',
        elemMods: {preset: 'inline'},
        content: [
            {
                elem: 'title',
                content: 'Цена'
            },
            {
                block: 'input',
                mods: {size: 's'},
                value: 40,
                content: {elem: 'control'}
            },
            {
                elem: 'unit',
                content: 'руб.'
            }
        ]
    }
}
```

#### Отображение значения на ползунке
Модификатор слайдера `interactive` со значением `no` – не отображает значения на ползунке. Текст внутри бегунка содержится в элементе блока `text`.

#### Скрытие инпута
Модификатор `input` со значением `hidden` – инпуты и информационные элементы слайдера будут скрыты.

```js
{
    block: 'slider',
    mods: {theme: 'normal', size: 'm', orientation: 'horiz', input: 'hidden'},
    js: {
        min: 10,
        max: 90,
        scale: [
            {value: 0, step: 10},
            {value: 100}
        ]
    },
    content: {
        elem: 'info',
        elemMods: {preset: 'inline'},
        content: [
            {
                elem: 'title',
                content: 'Слайдер'
            },
            {
                block: 'input',
                mods: {size: 'm'},
                value: 30,
                content: {elem: 'control'}
            },
            {
                elem: 'unit',
                content: 'руб.'
            }
        ]
    }
}
```

#### Анимация
Модификатор `animation` со значением `yes` переместит ползунок по щелчку мыши на шкале плавно с анимацией в указанное место. Если модификатор не выставлен – перемещение ползунка выполнится моментально.

#### Состояния слайдера

Слайдер может находиться в состоянии:

* **Не активен**, модификатор `disabled` со значением `yes`. Все вложенные блоки и элементы слайдера будут недоступны.

Состояния ползунка (элемент `runner`):

* **В фокусе**, модификатор элемента `focused` со значением `yes`. Ползунок находится в фокусе. Перемещается ползунок в фокусе клавишами **[ ←, ↑, →, ↓ ]**.

```js
{
    block: 'slider',
    mods: {theme: 'normal', size: 'm', orientation: 'horiz', disabled: 'yes'},
    js: {
        scale: [
            {value: 0, step: 10},
            {value: 100}
        ]
    },
    content: {
        elem: 'info',
        elemMods: {preset: 'inline'},
        content: [
            {
                elem: 'title',
                content: 'Цена'
            },
            {
                block: 'input',
                mods: {size: 'm'},
                content: {elem: 'control'},
                value: 50
            },
            {
                elem: 'unit',
                content: 'руб.'
            }
        ]
    }
}
```


<a name="defscale"> </a>
### Значения по умолчанию
Параметры шкалы:

```javascript
scale: [
    {percent: 0, value: 0, step: 1, label: ''},
    {percent: 100, value: 100, step: 1, label: ''}
]
```

* минимальное значение шкалы – 0;
* максимальное значение шкалы – 100;
* шаг – 1.
