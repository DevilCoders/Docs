# Внешняя капча [WIP]

Компонент внешней капчи

## 🔗 Содержимое

* [Подключение](#подключение)
* [Использование](#использование)
* [API](#api)
* [Разработка](./contribute.md)

## Подключение

Внешняя капча подключает на сайт при помощи загрузочного скрипта `(captcha.js)`.

```html
<script src="path/captcha.js?param1=value1"></script>
```

## Использование

Капча работает в 2 режимах: автоматический и программный.

При автоматическом режиме, после загрузки загрузочного скрипта происходит поиск DOM элементов с классом `yacaptcha`, после чего в каждом из них происходит рендер компонента капчи.

```html
<!-- Внешняя капча в автоматическом режиме -->
<script src="path/capthca.js?sitekey=key" async defer></script>

<div class="yacaptcha"></div>
<div class="yacaptcha" data-sitekey="another-key"></div>
```

При программном режиме, после загрузки загрузочного скрипта происходит вызов callback, переданного в качестве query параметра, который выполняет дольнейшую работу.


```html
<!-- Внешняя капча в программном режиме -->
<script src="path/capthca.js?render=onload&onload=fn" async defer></script>

<script>
  function fn() {
    if (!window.yacaptcha) {
      return;
    }

    const container = document.getElementById("captcha-container");

    window.yacaptcha.render(container, {
      sitekey: 'key',
    })
  }
</script>

<div id="captcha-container"></div>
```

## API

API отличается в зависимости от режима подключения капчи.

### Автоматический режим

При автоматическом режиме, параметры для рендера можно установить как в query параметрах ссылки загрузочного скрипта, так и в data аттрибутах контейнера для капчи. При чем, если один и тот же параметр установлен и в query параметре и в data аттрибуте, то будет использован data аттрибут.

```html
<!-- Внешняя капча в автоматическом режиме -->
<script src="path/capthca.js?sitekey=key&callback=successFn" async defer></script>

<script>
  function successFn(token) {
    console.log(token);
  }

  function anotherSuccessFn(token) {
    console.log('Another', token);
  }
</script>

<div class="yacaptcha"></div>
<div class="yacaptcha" data-sitekey="another-key" data-callback="anotherSuccessFn"></div>
```

### Программный режим

При программном режиме, инициализация капчи происходит при помощи функции `window.yacaptcha.render`, которая получает на вход контейнер и объект с параметрами для капчи и возвращает идентификатор виджета. Также yacaptcha предоставляет функции `window.yacaptcha.reset`, которая сбрасывает капчу и `window.yacaptcha.getResponse`, которая позволяет получить результат капчи.

```html
<!-- Внешняя капча в программном режиме -->
<script src="path/capthca.js?render=onload&onload=fn" async defer></script>

<script>
  let widgetId;

  function fn() {
    if (!window.yacaptcha) {
      return;
    }

    const container = document.getElementById("captcha-container");

    function callback(token) {
      console.log(token);
    }

    widgetId = window.yacaptcha.render(container, {
      sitekey: 'key',
      callback: callback
    });
  }

  function reset() {
    if (!window.yacaptcha) {
      return;
    }

    window.yacaptcha.reset(widgetId);
  }

  function getResponse() {
    if (!window.yacaptcha) {
      return;
    }

    console.log(window.yacaptcha.getResponse(widgetId));
  }
</script>

<div id="captcha-container"></div>
<button onclick="reset()">Reset</button>
<button onclick="getResponse()">Get response</button>
```

Если функции `reset` и `getResponse` не получают на вход widgetId, то они применяются к первому отрендереному компоненту капчи.

### Список параметров для загрузочного скрипта

| Аттрибут | Data-аттрибут | Описание |
| -------- | ------------- |:-------------|
| sitekey?  | string      | Опционально. Ключ капчи |
| render? | "auto" \| "onload"      | Опционально. Флаг об установке капчи в программном или автоматическом режиме. По умолчанию, используется "аuto"  |
| onload?  | string      | Опционально. Функция, которая будет вызвана после загрузки капчи. Если render=auto, то onload вызывется после отрисовки капчи. Если render=onload, то onload вызывается после загрузки загрузочного скрпита  |
| hl? | string      | Опционально. Язык капчи. По умолчанию, капча автоматически определяет язык   |

### Список аттрибутов

| Аттрибут | Data-аттрибут | Описание |
| -------- | ------------- |:-------------|
| sitekey  | data-sitekey      | Ключ для капчи |
| callback? | data-callback      | Опционально. Функция, которая будет вызвана при успешном вызове капчи   |

### Список JS функций

| Функция | Параметры | Описание |
| -------- | ------------- |:-------------|
| render  | (container: stringId \| Element, params: object): WidgetId     | Функция отрисовки компонента внешней капчи |
| reset | (widgetId?: WidgetId): void      | Функция, сбрасывающая капчу. Без передачи widgetId, вызывается для первой созданной капчи.   |
| getResponse | (widgetId?: WidgetId): string | Функция, которая возвращает результат капчи. Без передачи widgetId, вызывается для первой созданной капчи.     |
