# JS API с Webpack

В современном JS-мире использовать глобальную библиотеку в своем коде неудобно.
Однако JS API 3.0 Яндекс.Карт распространяется только как JS-скрипт и подключается как глобальная переменная `ymaps3`:

```html
<head>
  <script src="https://api-maps.yandex.ru/3.0-beta/?apikey=<ваш API-ключ>&lang=ru_RU" type="text/javascript"></script>
</head>
<script>
  ymaps3.ready.then(() => {
    const {YMaps} = ymaps3;
    new YMaps({});
  });
</script>
```

{% note alert "Внимание." %}

Скрипт подключает лишь легковесный загрузчик. Полностью API будет доступно только после резолва `ymaps3.ready`

{% endnote %}

Разработчики привыкли работать с npm-пакетами. И в коде удобно работать с API так:

```js
import {YMaps} from 'ymaps3';

new YMaps({});
```

В этом может помочь [webpack](https://webpack.js.org/).
Верно его сконфигурировав, можно работать с API, как с обычным JS npm пакетом.

Ниже приведены способы, как настроить webpack с помощью опции [externals](https://webpack.js.org/configuration/externals/)
для работы с API.

## Способ 1 {#method1}

У вас уже где-то на странице [подключен](load.md) JS API Яндекс Карт, т.е. доступна глобальная переменная `ymaps3`.

Где-то уже подключен JS API.

```html
<head>
  <script src="https://api-maps.yandex.ru/3.0-beta/?apikey=<ваш API-ключ>&lang=ru_RU" type="text/javascript"></script>
</head>
```

Тогда настройка может иметь такой вид:

```json
{
  "externals": {
    "ymaps3": "ymaps3"
  }
}
```

После чего, в вашем коде можно будет использовать такой импорт:

```js
import ymaps3 from 'ymaps3';

ymaps3.ready.then(() => {
  const {YMaps} = ymaps3;
  new YMaps({});
});
```

## Способ 2 {#method2}

Вариант почти такой же в использовании, как `способ 1`

```json
{
  "externalsType": "script",
  "externals": {
    "ymaps3": ["https://api-maps.yandex.ru/3.0-beta/?apikey=<ваш API-ключ>&lang=ru-RU", "ymaps3"]
  }
}
```

В коде также необходимо использовать `ymaps3.ready`:

```js
import ymaps3 from 'ymaps3';

ymaps3.ready.then(() => {
  const {YMaps} = ymaps3;
  new YMaps({});
});
```

{% note alert "Внимание." %}

> В обоих вариантах импортируется еще не готовое API. Необходимо дождаться резолва промиса `ymaps3.ready`

{% endnote %}

## Способ 3 {#method3}

Чтобы писать код, похожий на работу с обычным пакетом, какой был в начале статьи:

```js
import {YMaps} from 'ymaps3';

new YMaps({});
```

Нам необходимо обработать промис еще до импорта.

Сделать это можно используя такую запись:

```js
const config = {
  //...
  externalsType: 'script',
  externals: {
    ymaps3: [
      `promise new Promise((resolve) => {
          if (typeof ymaps3 !== 'undefined') {
            return ymaps3.ready.then(() => resolve(ymaps3));
          }

          const script = document.createElement('script');
          script.src = "https://api-maps.yandex.ru/3.0-beta/?apikey=<ваш API-ключ>&lang=ru-RU";
          script.onload = () => {
            ymaps3.ready.then(() => resolve(ymaps3));
          };
          document.body.appendChild(script);
        })`
    ]
  }
};
```

Мы подключаем загрузчик API, ждем, пока он полностью загрузится, и отдаем в конечный `import` уже полностью загруженные модули.

Тогда в вашем коде можно будет использовать уже готовые к работе модули API:

```js
import {YMaps} from 'ymaps3';
new YMaps({});
```

## Сравнение способов {#comparison-of-methods}

У `способа 3` есть очевидный недостаток: в вашем модуле не будет выполнен никакой код,
пока JS API 3.0 Яндекс.Карт не загрузится полностью.

Например, вы не сможете показать анимацию загрузки или другие компоненты:

```js
import ymaps3 from 'ymaps3';
const {YMap} = ymaps3.reactify(React, ReactDOM);

// ...

function App() {
  return (
    <div>
      <button>Кнопка</button>
      <YMap />
    </div>
  );
}
```

При использовании `способа 1` или `способа 2` этого можно избежать:

```js
import ymaps3 from 'ymaps3';
import React, {useState, useEffect} from 'react';

// ...

function Map() {
  const [loaded, setLoaded] = useState(true);

  useEffect(() => {
    ymaps3.ready.then(() => setLoaded(false));
  }, []);

  if (loaded) {
    return <div>Loading...</div>;
  }

  const {YMap} = ymaps3.reactify(React, ReactDOM);

  return <YMap />;
}

function App() {
  return (
    <div>
      <button>Кнопка</button>
      <Map />
    </div>
  );
}
```

Помните, что при подключении API указывается [язык](load.md#parms). Если вы создаете интернациональные сайты,
при любом способе подключения следите за его переключением.

Например, для способа 3 это можно сделать так:

```js
const config = {
  //...
  externals: {
    ymaps3: [
      `promise new Promise((resolve) => {
          ...
          const lang = ['ru', 'ru-ru'].includes(navigator.language) ? 'ru-Ru' : 'en-US';
          script.src = "https://api-maps.yandex.ru/3.0-beta/?apikey=<ваш API-ключ>&lang=" + lang;
          ...
        })`
    ]
  }
};
```

[Пример готовой сборки](https://codesandbox.io/s/yimzzd)
