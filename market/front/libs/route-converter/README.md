# @yandex-market/route-converter
Позволяет из тачевого URL'а получить URL соответствующей десктопной страницы (и наоборот). Применяем для генерации ссылки в футере, alternate и canonical ссылок и редиректов между Десктопом и Тачём в Белом и Синем Маркете.

## API

### Функции

#### blueDesktop.toBlueTouch(route, options)
Генерирует URL на Синий Тач из ссылки на Синий Десктоп. Всегда возвращает `string` (готовый URL). Если не удаётся сгенерировать подходящую ссылку, возвращает URL морды.

#### blueDesktop.toBlueTouchOrNull(route, options)
Генерирует URL на Синий Тач из ссылки на Синий Десктоп. Возвращает или `string` (готовый URL), или `null` (если не удаётся сгенерировать подходящую ссылку).

#### blueTouch.toBlueDesktop(route, options)
Генерирует URL на Синий Десктоп из ссылки на Синий Тач. Всегда возвращает `string` (готовый URL). Если не удаётся сгенерировать подходящую ссылку, возвращает URL морды.

#### blueTouch.toBlueDesktopOrNull(route, options)
Генерирует URL на Синий Десктоп из ссылки на Синий Тач. Возвращает или `string` (готовый URL), или `null` (если не удаётся сгенерировать подходящую ссылку).

#### desktop.toTouch(route, options)
Генерирует URL на Белый Тач из ссылки на Белый Десктоп. Всегда возвращает `string` (готовый URL). Если не удаётся сгенерировать подходящую ссылку, возвращает URL морды.

#### desktop.toTouchOrNull(route, options)
Генерирует URL на Белый Тач из ссылки на Белый Десктоп. Возвращает или `string` (готовый URL), или `null` (если не удаётся сгенерировать подходящую ссылку).

#### touch.toDesktop(route, options)
Генерирует URL на Белый Десктоп из ссылки на Белый Тач. Всегда возвращает `string` (готовый URL). Если не удаётся сгенерировать подходящую ссылку, возвращает URL морды.

#### touch.toDesktopOrNull(route, options)
Генерирует URL на Белый Десктоп из ссылки на Белый Тач. Возвращает или `string` (готовый URL), или `null` (если не удаётся сгенерировать подходящую ссылку).

### Аргументы функций
Все функции принимают одни и те же аргументы.

#### route
Объект, описывающий исходную ссылку. С помощью Flow тип аргумента описывается следующим образом:

```js
type Route = {
    pageId: PageId, // Название роута исходной ссылки.
    params: QueryParams, // Таблица query-параметров исходной ссылки.
};
type PageId = string;
type QueryParams = {[string]: string | string[]};
```

#### options
Объект с опциями конвертирования ссылки.

- `[addParams = {}]`

  Таблица параметров, которые следует добавить к получившемуся URL. С помощью Flow тип аргумента описывается следующим образом:

  ```js
  type QueryParams = {[string]: ?string | string[]};
  ```

  Например, если вы хотите отключить добавление параметра `no-pda-redir`, вам нужно передать следующий аргумент:

  ```js
  addParams: {
      'no-pda-redir': null,
  },
  ```

- `tld`

  Домен верхнего уровня для конечной ссылки. Тип `string`. Например: `ru`, `kz`.

### Примеры
Если вы программируете Белый Тач и хотите получить ссылку на Белый десктопный Маркет в Казахстане, используйте функцию `touch.toDesktop`.

```js
import {touch as routeConverter} from '@yandex-market/route-converter';

routeConverter.toDesktop({
    pageId: 'touch:search-filters',
    params: {
        hid: '91491',
        nid: '54726',
        onstock: '1',
    },
}, {
    tld: 'kz',
}); //=> '//market.yandex.kz/catalog/54726/filters?hid=91491&onstock=1'
```

Если вы программируете Белый Десктоп и хотите получить ссылку на Белый Тач в России и особым образом обрабатывать случаи, когда route-converter не может сконвертировать ссылку — получать в этом случае `null`, используйте функцию `desktop.toTouchOrNull`.

```js
import {desktop as routeConverter} from '@yandex-market/route-converter';

const result = routeConverter.toTouchOrNull({
    pageId: 'market:all-filters',
    params: {
        nid: '54726',
        hid: '91491',
        onstock: '1',
    },
}, {
    tld: 'ru',
}); //=> '//m.market.yandex.ru/search/filters?nid=54726&hid=91491&onstock=1'

if (result === null) {
    // Не забудьте обработать возможное значение null.
}
```

Если вы программируете Синий Тач и хотите получить ссылку на Синий десктопный Маркет в России, используйте функцию `blueTouch.toBlueDesktop`.

```js
import {blueTouch as routeConverter} from '@yandex-market/route-converter';

routeConverter.toBlueDesktop({
    pageId: 'blue-market:product',
    params: {
        slug: 'xiaomi-redmi-note-3-pro-32gb',
        skuId: '91491',
    },
}, {
    tld: 'ru',
}); //=> '//beru.ru/product/xiaomi-redmi-note-3-pro-32gb/91491?&onstock=1&no-pda-redir=1'
```

## Как сделать пулл-реквест в route-converter?
1. Откройте `lib/analogous-pages.js` и поищите интересующее вас имя роута — возможно, кто-то уже добавил поддержку интересующих вас страниц в более свежую версию route-converter'а, чем используется в вашем проекте. В последнем случае можете сразу перейти к шагу 7.
2. Добавьте конфиги нужных роутов в соответствующие файлы в директории `lib/routes`.
3. Создайте отношение между вашими роутами в массиве `analogousPagesList` в `lib/analogous-pages.js`. JSDoc комментарии в файле содержат исчерпывающие сведения, как это сделать.
4. Напишите тесты для добавленных вами отношений (см. директорию `spec`). Проверьте, что вы ничего не сломали:

   ```sh
   veendor install
   npm test
   ```

5. Закомитьте ваш код и убедитесь, что покрытие кода в предыдущей ревизии route-converter'а было не больше, чем в вашей.
6. Увеличьте номер версии в `package.json`, допишите ченджлог в файле CHANGELOG.md и присылайте пулл-реквест в [нашу репу](https://github.yandex-team.ru/market/route-converter).
7. Когда ваш пулл-реквест вмёржили и сделали `npm publish`, апните `@yandex-market/route-converter` в `package.json` вашего проекта.
