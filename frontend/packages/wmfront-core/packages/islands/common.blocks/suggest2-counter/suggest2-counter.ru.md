# suggest2-counter

Блок `suggest2-counter` используется для подключения [счетчика](https://beta.wiki.yandex-team.ru/SERP/suggest/metrics2#schetchiki) [саджеста](../suggest2/suggest2.ru.md). Предназначен для единообразного логирования на разных сервисах информации о способах выбора подсказок. По умолчанию счетчик отключен.

[Подробное описание формата ручки счетчика](https://wiki.yandex-team.ru/tenorok/suggest/counter/)

## Обзор
[Подключение счетчика](#counter-on)

<a name="mods"></a>
### Модификаторы блока

| Модификатор                | Допустимые значения | Способы установки | Описание                    |
| -------------------------- | ------------------- | ----------------- | --------------------------- |
| [disabled](#mods-disabled) |	`yes`              |	JS               | Неактивное состояние блока. |


<a name="js-params"></a>
### JS-параметры блока

|  Поле           | Тип     | Значение по умолчанию | Описание               |
| --------------- | ------- | --------------------- | ---------------------- |
| `service`       | String  | –                     | Идентификатор сервиса. |
| `submitBySelect`| Boolean | `false`               | Флаг отправки запроса при выборе подсказки в саджесте.
| `suggestReqID`  | Boolean | `false`               | Флаг привязки уникального номера для подклейки логов к сессии пользователя, включает формирование параметра `suggest_reqid`.
| `host`          | String  | `//yandex.ru`         | Хост адреса счетчика.
| `path`          | String  | `/clck/`              |  Путь адреса счетчика.
| `params`        | Object  | `{}`                  | Постоянные параметры запроса.
| `dataUrl`       | String  | `http://ya.ru`        | Адрес страницы, отправляющей запрос.
| `preventSubmit` | Boolean | `true`                | Флаг для предотвращения отправки формы запроса, пока не будет отправлен счетчик.
| `timeout`       | Number  | `300`                 | Время ожидания ответа от сервера счетчика, мс.

## Подробнее

<a name="counter-on"></a>
### Подключение счетчика

Чтобы подключить счетчик к саджесту, необходимо:

* Явно примиксовать к блоку [suggest2-form](../suggest2-form/suggest2-form.ru.md) блок `suggest2-counter`, с указанием [JS-параметров](#js-params).
* К блоку `button2` (кнопка «Найти») примиксовать одноименный элемент блока `suggest2-form` (счетчику нужно знать о существовании кнопки).

```js
{
    block: 'form',
    tag: 'form',
    mix: [
        {block: 'suggest2-form', js: true},
        // Подключение сечтичка
        {block: 'suggest2-counter', js: {
            service: 'morda_ru',
            submitBySelect: true,
            host: '//yandex.ru',
            path: '/clck/jclck/',
            params: {
                dtype: 'stred',
                pid: 0,
                cid: 2873
            }
        }}
    ],
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
                block: 'button2',
                mods: {size: 'm', theme: 'normal', pin: 'clear-round'},
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
                    mods: {theme: 'normal', size: 'm'},
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
### Модификатор `disabled`

Отвечает за неактивное состояние, при котором счетчик подключен, но не выполняет логирование. Используется для временного отключения.

Выставляется автоматически при выставлении неактивного состояния блоку [suggest2-form](../suggest2-form/suggest2-form.ru.md#%D0%9C%D0%BE%D0%B4%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%82%D0%BE%D1%80-disabled).

Способы установки: JS <br>
Допустимое значение: `yes`.
