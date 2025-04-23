# Блок suggest2

_Саджест — это поисковая подсказка._

![suggest](https://jing.yandex-team.ru/files/tenorok/screen01_2014-03-27_20-30-25.png)

**Статус блока**: [unstable](https://github.yandex-team.ru/lego/islands-guidelines/blob/master/blocks-stabilization.md) (API блока в разработке).

Блок `suggest2` («саджест») используется для создания поисковых подсказок, которые всплывают в окне под поисковой строкой при вводе запроса. Список подсказок обновляется по мере набора новых букв или слов.

Блок предоставляет следующие возможности:

* изменять [стилевое оформление](#mods-theme) и [размер](#mods-size) саджеста;
* [группировать поисковые подсказки](#mods-group);
* [адаптировать ширину](#mods-adaptive) саджеста при изменении размеров страницы браузера;
* отображать подсказки только определенных [типов](#mods-type) в результате запроса;
* включать режим [пословного автодополнения](#mods-complete) для мобильных устройств;
* подключать к саджесту блоки [input](../suggest2-input/suggest2-input.ru.md) и [popup](../suggest2-popup/suggest2-popup.ru.md) из различных библиотек (как собственных – `islands-*`, так и сервисов);
* подключать [счетчик](../suggest2-counter/suggest2-counter.ru.md) отправки запроса;
* настраивать [параметры запроса](#js-params) к серверу саджеста.

## Обзор блока
<!-- [Быстрый старт](#qstart) -->
- [Счетчик саджеста](suggest2-counter/suggest2-counter.ru.md)
- [Особенности реализации](#features)
- [Примеры со всеми видами подсказок](#examples)
- [Известные проблемы](#issue)

### Вспомогательные блоки

Блок                                                          | Описание
------------------------------------------------------------- | -------------------------
[suggest2-form](../suggest2-form/suggest2-form.ru.md)            | Форма поиска, содержащая все контролы блока `suggest2`. Также используется для первоначальной инициализации блока `suggest2` в DOM-дереве.
[suggest2-item](../suggest2-item/suggest2-item.ru.md)            | Элемент поисковой подсказки.
[suggest2-input](../suggest2-input/suggest2-input.ru.md)         | Универсальный API для подключения к `suggest2` блоков `input` из разных библиотек.
[suggest2-popup](../suggest2-popup/suggest2-popup.ru.md)         | Универсальный API для подключения к `suggest2` блоков `popup` из разных библиотек.
[suggest2-detect](../suggest2-detect/suggest2-detect.ru.md)      | Блок для сбора данных о браузере пользователя.<br> **NB** _Необходимо [явно декларировать](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/suggest2/suggest2.examples/20-large.bemjson.js#L74) в BEMJSON блока._
[suggest2-provider](../suggest2-provider/suggest2-provider.ru.md)| Провайдер данных. Поставляет блоку `suggest2` данные о подсказках из набора источников (suggest-сервера).
[suggest2-model](../suggest2-model/suggest2-model.ru.md)          | Модель данных. Содержит методы работы с данными о подсказках, которые запрашиваются с сервера через [suggest2-provider](../suggest2-provider/suggest2-provider.ru.md).
[suggest2-view](../suggest2-view/suggest2-view.ru.md)            | Представление данных. Преобразует данные о подсказках, полученных от [suggest2-model](../suggest2-model/suggest2-model.ru.md), из формата JSON в BEMJSON. Обеспечивает различные способы представления данных.
[suggest2-counter](../suggest2-counter/suggest2-counter.ru.md)   | **Необязательный**. Счетчик саджеста. Подсчитывает [различные характеристики](https://beta.wiki.yandex-team.ru/tenorok/suggest/counter/) взаимодействия пользователя с саджестом.

### Модификаторы блока

| Модификатор                  | Допустимые значения |Способы установки | Описание |
| ---------------------------- | ------------------- | --------------------- | -------- |
| [theme](#mods-theme)         | `normal`, `largе`, `flow` | BEMJSON | **Обязательный**. Стилевое оформление блока. |
| [size](#mods-size)           | `s`, `m`         | BEMJSON | **Обязательный**. Размер блока. Используется совместно с [модификатором theme в значении normal](#mods-theme). |
| [type](#mods-type)| `simple`, `advanced`, `all` | BEMJSON | Файлы зависимостей для подключения подсказок только определенных [типов](../suggest2-item/suggest2-item.ru.md#%D0%9C%D0%BE%D0%B4%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%82%D0%BE%D1%80-type) (простого и/или расширенного формата).  |
| [adaptive](#mods-adaptive)   | `yes` | BEMJSON | Адаптация ширины саджеста при изменении размеров окна браузера. Используется совместно с [модификатором theme в значении normal](#mods-theme).|
| [disabled](#mods-disabled)   | `yes`           | BEMJSON, JS | Неактивное состояние саджеста.|
| [complete](#mods-complete)   | `auto`          | BEMJSON, JS | Автодополнение в поисковом поле ввода. |
| [nameplate](#mods-nameplate) | `yes`           | BEMJSON | Дополнительное смещение вправо контейнера с подсказками относительно блока `input`. Используется совместно с [модификатором theme в значении large](#mods-theme).  |
| [group](#mods-group)         | `label`, `type` | BEMJSON | Группировка подсказок. Используется совместно с [модификатором theme в значении normal и large](#mods-theme). Значение по умолчанию: `type`. Доступен на deskpad-уровне.|
| [tpah](#mods-tpah)           | `plus`, `yes`   | BEMJSON | [Автодополнение](https://beta.wiki.yandex-team.ru/SERP/suggest/TapAhead/). Доступен на touch-уровне.|
| [footer](#mods-footer)       | `yes`           | BEMJSON | Стилевое оформление блока с подвалом. Доступен на deskpad-уровне.|
| [login](#mods-login)         | `yes`           | BEMJSON | Кнопка авторизации в подвале. Доступен на deskpad-уровне.|
| [insert-arrow](#mods-insert-arrow)   | `yes`   | BEMJSON | Стрелки в подсказках для подстановки |


<a name="js-params"></a>
### JS-параметры блока
|  Поле                                                       | Тип    | Значение по умолчанию | Описание |
| ----------------------------------------------------------- | ------ | --------------------- | -------- |
| [url](#fields-url)                                          | String |  –  | **Обязательный**. Адрес suggest-сервера, например: `http://suggest.yandex.ru/suggest-ya.cgi`. |
| [data](#fields-data)                                        | Object | `{}` | [GET-параметры для отправки серверу](http://wiki/IvanJanikov/SuggestFormat).
| [cache](#fields-cache)                                      | Boolean | `false` | Кэшировать результаты запросов. |
| [type](#fields-type)                                        | String | `GET` | Тип запроса. |
| [dataType](#fields-dataType)                                | String | `jsonp` | Тип данных ответа от сервера. |
| [timeout](#fields-timeout)                                  | Number | `2000` | Таймаут для запроса, по истечении которого саджест скроется. |
| [submitBySelect](#fields-submitBySelect)                    | Boolean | `false` | Отправить данные формы при выборе подсказки в саджесте. |
| [updateOnEnterByKeyboard](#fields-submitBySelect)           | Boolean | `true` | Обновить содержимое поля ввода при перемещении по элементам клавишами **↑**, **↓**. |
| [onFocus](#fields-onFocus)                                  | Boolean, String | `request` | Действие при установке фокуса в поле ввода. Возможные значения: <br>1) `request` — отправить запрос со значением поля ввода и показать саджест с результатами; <br>2) `show` — показать ранее полученные подсказки без отправки запроса; <br>3) `false` — ничего не делать. |
| [requestOnEmptyInput](#fields-requestOnEmptyInput)           | Boolean | `false` | Отправить запрос при пустом поле ввода. |
| [abortQueries](#fields-abortQueries)                         | Boolean | `false` | Прервать отправку неактуальных запросов (работает при dataType=json). |
| [sequentialQueriesTimeout](#fields-sequentialQueriesTimeout) | Boolean, Number | `false` |Последовательная отправка запросов. При включении нужно указать максимальный интервал (мс) ожидания ответа от сервера для отправки следующего запроса. |
| [showPopupOnEnabled](#fields-showPopupOnEnabled)             | Boolean | `false`| Видимость саджеста в момент снятия модификатора `disabled` при условии, что фокус находится в поле ввода. |


## Подробнее

### Модификаторы блока

<a name="mods-theme"></a>
#### Модификатор `theme`

Отвечает за стилевое оформление блока.

Используется совместно с модификатором [size](#mods-size) (только для `themе` в значении `normal`).

Способ установки: BEMJSON.

Допустимые значения          | Описание
---------------------------- | ---------------------------------------------------
[normal](#mods-theme-normal) | Типовой саджест. Совпадает по ширине с поисковым полем ввода. Является аналогом блока [input с модификатором suggest в значении yes](https://lego.yandex-team.ru/libs/islands/v4.x/desktop/input/#Модификатор-suggest) из `islands-*`.
[large](#mods-theme-large)   | Саджест главного поискового поля ввода сервиса. Растягивается на всю ширину страницы. Применяется в сочетании с главным поисковым полем ввода сервиса, расположенным под шапкой. <br> **NB** _Данный саджест крупнее типового, так как шрифт главного поискового поля ввода крупнее, чем у типовых полей ввода_.
[flow](#mods-theme-flow)     | Стилевое оформление для пословного саджеста. Доступен на уровне `touch-phone`.

<a name="mods-theme-normal"></a>
Типовой саджест:

```js
{
    block: 'form',
    tag: 'form',
    js: true,
    mix: {block: 'suggest2-form', js: true}, // Микс необходим для взаимодействия suggest2 с формой на странице
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input', // Поле ввода для suggest2
                mods: {size: 'm', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                content: {elem: 'control'}
            },
            {
                block: 'popup', // Выпадающее окно для подсказок suggest2 (примиксовывается к любому popup)
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                mix: [{
                    block: 'suggest2',
                    mods: {theme: 'normal', size: 'm'}, // Модификаторы саджеста
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true //  Микс с suggest2
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

<a name="mods-theme-large"></a>
Саджест главного поискового инпута:

```js
{
    block: 'form',
    tag: 'form',
    mix: {block: 'suggest2-form', js: true}, // Микс необходим для взаимодействия suggest2 с формой на странице
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input', // Поле ввода для  саджеста
                mods: {size: 'm', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                content: {elem: 'control'}
            },
            {
                block: 'popup', // suggest2 примиксовывается к любому popup
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                mix: [{
                    block: 'suggest2',
                    mods: {theme: 'large'}, // Стилевое оформление
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true // Микс с suggest2
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```
<a name="mods-theme-flow"></a>
Пословный саджест:

```js
{
    block: 'form',
    tag: 'form',
    mix: [{block: 'suggest2-form', js: {
        popupName: 'popup2'
    }}],
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                 mods: {size: 'm', theme: 'normal'},
                 mix: {block: 'suggest2-form', elem: 'input'},
                 content: {elem: 'control'}
            },
            {
                block: 'popup2',
                mods: {target: 'anchor', theme: 'clear', autoclosable: 'yes'},
                directions: ['bottom-left'],
                mix: [{
                    block: 'suggest2',
                    mods: {theme: 'flow'}, // Стилевое оформление
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

<a name="mods-size"></a>
#### Модификатор `size`

Определяет размер блока, который зависит от размера шрифта (соответствуют значениям модификатора `size` блока [input](https://lego.yandex-team.ru/libs/islands/v4.x/desktop/input/) из `islands-*`). Используется только совместно с модификатором [theme в значении normal](#mods-theme).

Подробнее о размерах саджеста в примечании к [значению large модификатора theme](#mods-theme).

Способ установки: BEMJSON.<br>
Допустимые значения: `s`, `m`. <br>

Саджест размером `s`:

```js
{
    block: 'form',
    tag: 'form',
    mix: {block: 'suggest2-form', js: true},
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 'm', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                content: {elem: 'control'}
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                mix: [{
                    block: 'suggest2',
                    mods: {theme: 'normal', size: 's'}, // Размер саджеста
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

Саджест размером `m`:

```js
{
    block: 'form',
    tag: 'form',
    mix: {block: 'suggest2-form', js: true},
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 'm', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                content: {elem: 'control'}
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                mix: [{
                    block: 'suggest2',
                    mods: {theme: 'normal', size: 'm'}, // Размер саджеста
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

<a name="mods-type"></a>
#### Модификатор `type`

Определяет файлы c зависимостями, каждый из которых подключает подсказки определенных [типов](../suggest2-item/suggest2-item.ru.md). Используется для вывода в результатах запросов саджеста подсказок только нужных типов.

<!-- Определяет готовый набор зависимостей с типами [подсказок](suggest2-item/suggest2-item.ru.md), которые будут отображаться в результатах запроса саджеста. -->

Способ установки: BEMJSON.

Допустимые значения| Описание
------------------ | -----------------------------------------------------------
–                  | По умолчанию отображаются только простые текстовые подсказки.
`simple`           | Набор зависимостей для подключения подсказок типа `fact`, `nav`, `traffic`, `weather`, `icon` (типы подсказок с сокращенным форматом ответа от сервера).
`advanced`         | Набор зависимостей для подключения подсказок типа `bemjson` и `html` (типы подсказок с расширенным форматом ответа от сервера).
`all`              | Набор зависимостей для подключения всех вышеперечисленных типов подсказок.


> **NB** Чтобы использовать опциональный модификатор `type`, укажите его в зависимостях блока с нужными значениями на проектном уровне.

Саджест с простыми типами подсказок:
```js
{
    block: 'form',
    tag: 'form',
    mix: {block: 'suggest2-form', js: true},
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 's', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                attrs: {style: 'width: 50%'},
                content: {elem: 'control'}
            },
            {
                block: 'button',
                mods: {size: 's'},
                type: 'submit',
                mix: {block: 'suggest2-form', elem: 'button'},
                text: 'Найти'
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                js: {directions: 'bottom-left'},
                mix: [{
                    block: 'suggest2',
                    mods: {
                        type: 'simple', // Тип подсказок с простым форматом вывода
                        theme: 'normal',
                        size: 's'
                    },
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

Саджест с расширенными типами подсказок:

```js
 {
    block: 'form',
    tag: 'form',
    mix: {block: 'suggest2-form', js: true},
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 's', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                attrs: {style: 'width: 50%'},
                content: {elem: 'control'}
            },
            {
                block: 'button',
                mods: {size: 's'},
                type: 'submit',
                mix: {block: 'suggest2-form', elem: 'button'},
                text: 'Найти'
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                js: {directions: 'bottom-left'},
                mix: [{
                    block: 'suggest2',
                    mods: {
                        type: 'advanced', // Типы подсказок с расширенным форматом вывода
                        theme: 'normal',
                        size: 's'
                    },
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

Саджест со всеми типами подсказок:

```js
{
    block: 'form',
    tag: 'form',
    mix: {block: 'suggest2-form', js: true},
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 's', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                attrs: {style: 'width: 50%'},
                content: {elem: 'control'}
            },
            {
                block: 'button',
                mods: {size: 's'},
                type: 'submit',
                mix: {block: 'suggest2-form', elem: 'button'},
                text: 'Найти'
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                js: {directions: 'bottom-left'},
                mix: [{
                    block: 'suggest2',
                    mods: {
                        type: 'all', // Типы подсказок всех форматов
                        theme: 'normal',
                        size: 's'
                    },
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```


<a name="mods-adaptive"></a>
#### Модификатор `adaptive`

Автоматически синхронизирует ширину саджеста с шириной поискового поля ввода при изменении размеров окна браузера. Используется совместно с модификатором [theme в значении normal](#mods-theme).

>**NB** Применяйте модификатор только в случае крайней необходимости, поскольку операция ресурсоемкая. Не используется для фиксированной верстки.

Способ установки: BEMJSON.<br>
Допустимое значение: `yes`.

> **NB** Чтобы использовать опциональный модификатор `adaptive`, укажите его в зависимостях блока на проектном уровне.

```js
{
    block: 'form',
    tag: 'form',
    mix: {block: 'suggest2-form', js: true},
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 's', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                attrs: {style: 'width: 50%'},
                content: {elem: 'control'}
            },
            {
                block: 'button',
                mods: {size: 's'},
                type: 'submit',
                mix: {block: 'suggest2-form', elem: 'button'},
                text: 'Найти'
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                js: {directions: 'bottom-left'},
                mix: [{
                    block: 'suggest2',
                    mods: {
                        theme: 'normal',
                        size: 's',
                        adaptive: 'yes' // Адаптивный саджест
                    },
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

<a name="mods-disabled"></a>
#### Модификатор `disabled`

Отвечает за неактивное состояние блока («режим ожидания»), в котором все подписки на события сохраняются, но их обработка не выполняется. Позволяет временно отключить блок `suggest2`, для манипуляций с ним из JS. Используется в HOME (Морда, yandex.ru).

Поведение блока:

* при выставлении модификатора — блок `popup` закрывается и очищается содержимое списка подсказок;
* при снятии модификатора — после загрузки данных с подсказками блок `popup` раскрывается, при условии, что фокус находится в блоке `input`, связанном с данным блоком `suggest2`.

Способ установки: BEMJSON. JS <br>
Допустимое значение: `yes`.

```js
{
    block: 'form',
    tag: 'form',
    js: true,
    mix: {block: 'suggest2-form', js: true},
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 'm', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                content: {elem: 'control'}
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                mix: [{
                    block: 'suggest2',
                    mods: {theme: 'normal', size: 'm', disabled: 'yes'},
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true //  Микс с suggest2
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

<a name="mods-complete"></a>
#### Модификатор `complete`

Добавляет логику для отображения автодополнения в поле ввода саджеста. При этом подключатся файлы, необходимые для автодополнения.

Способ установки: BEMJSON. JS <br>
Допустимое значение: `auto`.

> **NB** Чтобы использовать опциональный модификатор `complete`, укажите в его зависимостях блока со значением `auto` на проектном уровне.

```js
{
    block: 'form',
    tag: 'form',
    js: true,
    mix: {block: 'suggest2-form', js: true},
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 'm', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                content: {elem: 'control'}
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                mix: [{
                    block: 'suggest2',
                    mods: {
                        theme: 'normal',
                        size: 'm',
                        complete: 'auto' // Автодополнение
                    },
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                 }, {
                    block: 'suggest2-detect', js: true //  Микс с suggest2
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

<a name="mods-nameplate"></a>
#### Модификатор `nameplate`

Сдвигает вправо контейнер с подсказками относительно блока `input`, чтобы он выравнивался по правому краю метки сервиса. Применяется в [header2 c элементом nameplate](https://lego.yandex-team.ru/libs/islands/v4.x/desktop/header2/#Элемент-nameplate) (визуально совмещен с блоком `input` саджеста). Используется совместно только с модификатором [theme в значении large](#mods-theme). В этом случае саджесту устанавливается стандартный размер шрифта.

Способ установки: BEMJSON.<br>
Допустимое значение: `yes`.

```js
[{
    block: 'header2',
    mods: {'show-websearch': 'yes', fixed: 'yes', border: 'transparent'},
    logo: {elem: 'logo', url: 'http://yandex.ru'},
    elem: 'nameplate', // Метка с названием сервиса
    service: 'mail',
    websearch: {
        block: 'search2', mods: {template: 'websearch'},
        mix: [
            {block: 'suggest2-form', js: true},
            {block: 'suggest2-form', elem: 'node'}
        ],
        input: [{
            block: 'input',
            mods: {size: 'm', theme: 'websearch'},
            mix: [{block: 'suggest2-form', elem: 'input'}],
            content: {
                elem: 'control',
                attrs: {name: 'text', autocomplete: 'off', maxlength: 400}
            }
        }, {
            block: 'popup',
            mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
            js: {directions: 'bottom-left'},
            mix: [{
                block: 'suggest2',
                mods: {
                    type: 'simple',
                    theme: 'large',
                    nameplate: 'yes' // Добавляет смещение вправо саджесту
                },
                js: {
                    url: '//suggest-server.lego-dev.dev.yandex-team.ru/portal/',
                    data: {
                        v: 4,
                        lr: 213,
                        wiz: 'TrWth',
                        fact: 1,
                        icon: 1,
                        hl: 1
                    }
                }
            }, {
                block: 'suggest2-detect', js: true
            }],
            content: {elem: 'content'}
        }]
    }
}, {
    block: 'x-deps',
    content: {block: 'i-services'}
}]
```

<a name="mods-group"></a>
#### Модификатор `group`

Определяет способ группировки подсказок саджеста.

Допустимые значения | Описание
------------------- | --------------------------------------------------
`label`             | Группировка подсказок по сервисам. В этом случае пользователь переходит  на сервис выбранной подсказки. Используется с [модификатором theme](#mods-theme) в любом значении.|
`type`              | Группировка подсказок по [типу](https://beta.wiki.yandex-team.ru/serp/suggest/html-items/#avtodopolneniedljatachejjtapaxed). По умолчанию применяется только для саджеста с [модификатором theme в значении large](#mods-theme). Не используется совместно с [модификатором theme в значении normal](#mods-theme).|

Способ установки: `BEMJSON`.<br>
Уровень переопределения: `deskpad` (общий для `desktop` и `touch-pad`).

Типовой саджест с группировкой подсказок по сервисам:

```js
{
    block: 'form',
    tag: 'form',
    mix: {block: 'suggest2-form', js: true},
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 'm', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                attrs: {style: 'width: 50%'},
                content: {elem: 'control'}
            },
            {
                block: 'button',
                mods: {size: 'm'},
                type: 'submit',
                mix: {block: 'suggest2-form', elem: 'button'},
                text: 'Найти'
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                js: {directions: 'bottom-left'},
                mix: [{
                    block: 'suggest2',
                    mods: {
                        type: 'simple',
                        theme: 'normal',
                        size: 'm',
                        group: 'label' // Группировка подсказок по сервису
                    },
                    js: {
                        url: '//suggest-server.lego-dev.dev.yandex-team.ru/portal/',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

Большой саджест с группировкой подсказок по типу (по умолчанию):

```js
{
    block: 'header2',
    mods: {'show-websearch': 'yes', fixed: 'yes', border: 'transparent'},
    logo: {elem: 'logo', url: 'http://yandex.ru'},
    websearch: {
        block: 'search2', mods: {template: 'websearch'},
        mix: [
            {block: 'suggest2-form', js: true},
            {block: 'suggest2-form', elem: 'node'}
        ],
        input: [{
            block: 'input',
            mods: {size: 'm', theme: 'websearch'},
            mix: [{block: 'suggest2-form', elem: 'input'}],
            content: {
                elem: 'control',
                attrs: {name: 'text', autocomplete: 'off', maxlength: 400}
            }
        }, {
            block: 'popup',
            mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
            js: {directions: 'bottom-left'},
            mix: [{
                block: 'suggest2',
                mods: {
                    type: 'simple',
                    theme: 'large'
                },
                js: {
                    url: '//suggest-server.lego-dev.dev.yandex-team.ru/portal/',
                    data: {
                        v: 4,
                        lr: 213,
                        wiz: 'TrWth',
                        fact: 1,
                        icon: 1,
                        hl: 1
                    }
                }
            }, {
                block: 'suggest2-detect', js: true
            }],
            content: {elem: 'content'}
        }]
    }
}
```


Большой саджест с группировкой подсказок по сервисам:

```js
{
    block: 'header2',
    mods: {'show-websearch': 'yes', fixed: 'yes', border: 'transparent'},
    logo: {elem: 'logo', url: 'http://yandex.ru'},
    websearch: {
        block: 'search2', mods: {template: 'websearch'},
        mix: [
            {block: 'suggest2-form', js: true},
            {block: 'suggest2-form', elem: 'node'}
        ],
        input: [{
            block: 'input',
            mods: {size: 'm', theme: 'websearch'},
            mix: {block: 'suggest2-form', elem: 'input'},
            content: {
                elem: 'control',
                attrs: {name: 'text', autocomplete: 'off', maxlength: 400}
            }
        }, {
            block: 'popup',
            mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
            js: {directions: 'bottom-left'},
            mix: [{
                block: 'suggest2',
                mods: {
                    type: 'simple',
                    theme: 'large',
                    group: 'label' // Группировка подсказок по сервису
                },
                js: {
                    url: '//suggest-server.lego-dev.dev.yandex-team.ru/portal/',
                    data: {
                        v: 4,
                        lr: 213,
                        wiz: 'TrWth',
                        fact: 1,
                        icon: 1,
                        hl: 1
                    }
                }
            }, {
                block: 'suggest2-detect', js: true
            }],
            content: {elem: 'content'}
        }]
    }
}
```

<a href="#mods-tpah"></a>
#### Модификатор `tpah`

Задает визуальное представление для текста запроса вида «+текст запроса». В списке подсказок наглядно отделяет текст запроса от предлагаемого варианта, которым по касанию (`tap`) можно дополнить вводимое слово в поле ввода.

Допустимые значения | Описание
------------------- | --------------------------------------------------------
`plus`              | Расширенная форма представления текста запроса. Выделяется стилевым оформлением и увеличенной областью для касания.
`yes`               | Упрощенная форма представления текста запроса. Графически не выделяется.

Способ использования: BEMJSON.<br>
Уровень переопределения: `touch`.

```js
{
    block: 'form',
    tag: 'form',
    mix: {block: 'suggest2-form', js: true},
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 's', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                content: {elem: 'control'}
            },
            {
                block: 'button',
                mods: {size: 's'},
                type: 'submit',
                mix: {block: 'suggest2-form', elem: 'button'},
                text: 'Найти'
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                mix: [{
                    block: 'suggest2',
                    mods: {
                        type: 'simple',
                        theme: 'normal',
                        size: 's',
                        tpah: 'plus' // Выделение автодополнения
                    },
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1,
                            tpah: 1
                        }
                    }
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

<a href="#mods-footer"></a>
#### Модификатор `footer`

Задает стилизацию блока для случая, когда добавляется подвал

Способ установки: BEMJSON.<br>
Допустимое значение: `yes`.
Уровень переопределения: `deskpad`.

<a href="#mods-login"></a>
#### Модификатор `login`

Добавляет подвал со ссылкой на авторизацию

Способ установки: BEMJSON.<br>
Допустимое значение: `yes`.
Уровень переопределения: `deskpad`.

<a href="#mods-insert-arrow"></a>
#### Модификатор `insert-arrow`

Добавляет в подсказки стрелку. По клику срабатывает событие `arrowInsert` c параметрами `val`, `domEvent`

* `val` - текстовое значение подсказки для подстановки в поле ввода
* `domEvent` - DOM событие

Способ использования: `BEMJSON`.<br>
Допустимое значение: `yes`.<br>
Уровень переопределения: `desktop`, `touch-pad`.

<a name=features></a>
### Особенности реализации

* Состоит из нескольких блоков: `suggest2` и вспомогательных `suggest2-*`.
* Зависит от библиотеки [bem-bl](https://lego.yandex-team.ru/libs/bem-bl/dev/).
* Подключается с помощью описания в BEMJSON-декларации (в отличие от первой версии саджеста, блок [suggest](../suggest/suggest.ru.md), который [подключается в JavaScript](https://lego.yandex-team.ru/libs/islands/v3.x/desktop/suggest/#Объявление-блока-на-странице-22)).
* Реализация и возможности существенно отличаются от блока [suggest](../suggest/suggest.ru.md).

### Клавиатурное управление

* **↑**, **↓** — переход по элементам поисковой подсказки.
* **Enter** — выбор подходящего запроса из списка подсказок.
* **Esc** — скрытие саджеста.
* **Tab** и **→** — активация дополнения (работают при выставленном модификаторе `complete_auto`).

<a name="examples"></a>
### Примеры со всеми видами подсказок

Примеры `90-simple-all` и `90-large-all` обращаются к тестовой ручке, которая отвечает только на пробел в качестве запроса. Они нужны для удобного тестирования корректного отображения всех типов подсказок.

![all-items](https://jing.yandex-team.ru/files/tenorok/screen01_2014-03-27_20-34-32.png)

<a name="issue"></a>
### Известные проблемы
