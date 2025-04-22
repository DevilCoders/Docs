# Моки для автотестов

О том, как это работает и для чего нужно, можно прочитать [здесь](./HOW_IT_WORKS.md).

## Содержание

- [Тайлы](#Тайлы)
- [Поиск](#Поиск)
- [Метапоиск](#Метапоиск)
- [Саджест](#Саджест)
- [Маршрутизатор](#Маршрутизатор)
    - [Автомобильный маршрутизатор](#Автомобильный-маршрутизатор)
    - [ОТ маршрутизатор](#ОТ-маршрутизатор)
    - [Пешеходный маршрутизатор](#Пешеходный-маршрутизатор)
- [Панорамы](#Панорамы)
- [Погода](#Погода)
- [Sendmail](#sendmail)
- [Общественный транспорт](#Общественный-транспорт)
    - [Все нитки маршрута](#Все-нитки-маршрута)
    - [Сервис остановок](#Сервис-остановок)
    - [Нитка маршрута](#Нитка-маршрута)
- [Фото организации](#Фото-организации)
    - [Список фото](#Список-фото)
- [Саджест логина неавторизованным пользователям](#Саджест-логина-неавторизованным-пользователям)
- [Дорожные события](#Дорожные-события)
- [Афиша](#Афиша)
- [Рассылятор](#Рассылятор)

## Готовые моки

### Тайлы

Будет отдан одноцветный файл в формате PNG.

__Адрес__: `/mocks/layers/:color`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[hosts][mapTiles]=http://podrick.c.maps.yandex-team.ru/mocks/layers/red/

https://l7test.yandex.ru/maps/?host_config[hosts][mapTiles]=http://podrick.c.maps.yandex-team.ru/mocks/layers/red/?l=map&%c&%l
```

__Параметры__:

Параметры задаются в запросе, как часть пути.

__`color`__: Цвет тайла

- `white` (по умолчанию)
- `black`
- `blue`
- `gray`
- `green`
- `orange`
- `red`
- `yellow`

Остальные параметры отображаются на тайле в виде текста, если в `query` параметрах присутствуют [тайловые координаты](https://wiki.yandex-team.ru/maps/dev/core/layers/current.layers/#servisy). Если параметр не указан в запросе, то используется его имя.

__`l`__: Тип слоя

__`x`__, __`y`__, __`z`__: Тайловые координаты

__`scale`__: Масштаб тайла

__`lang`__: Локаль

[&#8593; Содержание](#Содержание)

### Поиск

В зависимости от переданных _query_ параметров будет отдан JSON файл. Если параметр не указан в запросе, то используется его имя.

Пример имени файла: `1_text_1357972692_mode_uri_ll_z.json`

__Важные замечания__:

- При добавлении моков будет заменен `urlTemplate` для превьюшек фотографий организаций на `http://podrick.c.maps.yandex-team.ru/mocks/layers/yellow/`.

__Адрес__: `/mocks/search/1.x`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][searchApi]=http://podrick.c.maps.yandex-team.ru/mocks/search/
```

__Параметры__:

Поддерживается часть параметров геопоиска:

__`results`__: Количество результатов

__`text`__: Поисковой запрос

__`business_oid`__: Идентификатор организации

По умолчанию используется `oid`.

__`mode`__: Режим поиска

__`uri`__: URI объекта

__`ll`__: Координаты для поиска

__`z`__: Зум для поиска

__`lang`__: Язык запроса

__`mock_version`__: Используется для инвалидации моков в БЯК

[&#8593; Содержание](#Содержание)

### Метапоиск

В зависимости от переданных _query_ параметров будет отдан JSON файл. Если параметр не указан в запросе, то используется его имя.

Пример имени файла: `1_text_1357972692_mode_uri_ll_z.json`

__Адрес__: `/mocks/metasearch/yandsearch`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][search]=http://podrick.c.maps.yandex-team.ru/mocks/metasearch/
```

__Параметры__:

Параметры те же, что и в [поисковом моке](#Поиск).

[&#8593; Содержание](#Содержание)

### Саджест

В зависимости от переданных _query_ параметров будет отдан JSONP. Если параметр не указан в запросе, то используется его имя.

__Важные замечания__:

- Моки забираются только из русского саджеста: [`suggestApi_RU`](https://github.yandex-team.ru/maps/hosts/blob/master/hosts/1.3/hosts-production.json#L114).
- Параметр `callback` будет учитан только для возврата, в моках будет сохранено без колбэка.

__Адрес__: `/mocks/suggest/suggest-geo`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[hosts][suggestApi]=https://podrick.c.maps.yandex-team.ru/mocks/suggest/
```

__Параметры__:

Поддерживается часть параметров [геосаджеста](https://wiki.yandex-team.ru/suggest/geo/):

__`v`__: Актуальный формат ответа (default: `5`)

__`bases`__: Дополнительные типы

__`part`__: Пользовательский ввод

__`pos`__: Позиция курсора

__`spn`__: Размер окна поиска

__`ll`__: Координаты центра окна

__`bbox`__: Окно поиска, параметр заменяет ll/spn

__`lang`__: Язык запроса (default: `ru`)

__`n`__: Максимальное количество подсказок (default: `7`)

__`search_type`__: Тип подсказок (default: `all`)

__`local_only`__: Искать только объекты, входящие в области, захватываемые spn пользователя (default: `1`)


[&#8593; Содержание](#Содержание)

### Маршрутизатор

В зависимости от переданных _query_ параметров будет отдан XML файл. Если параметр не указан в запросе, то используется его имя.

#### Автомобильный маршрутизатор

__Адрес__: `/mocks/routes/auto/route/` или `/mocks/routes/auto/route_jams/`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][router]=http://podrick.c.maps.yandex-team.ru/mocks/routes/auto/
```

__Параметры__:

__`lang`__: Язык запроса

__`rll`__: Набор точек маршрута

__`via`__: Индексы промежуточных точек

__`rtm`__: Режим построения маршрута

__`mode`__: Режим маршрутизации

__`results`__: Количество результатов

__`dir`__: Направление начала маршрута

__`snap`__: Уровень детальности маршрута

__`output`__: Подробность ответа

[&#8593; Содержание](#Содержание)

#### ОТ маршрутизатор

__Адрес__: `/mocks/masstransit/route`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][masstransit]=http://podrick.c.maps.yandex-team.ru/mocks/routes/masstransit/
```

__Параметры__:

__`lang`__: Язык запроса

__`rll`__: Набор точек маршрута

__`rtm`__: Режим маршрутизации

[&#8593; Содержание](#Содержание)

#### Пешеходный маршрутизатор

__Адрес__: `/mocks/pedestrian/route`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][pedestrian]=http://podrick.c.maps.yandex-team.ru/mocks/routes/pedestrian/
```

__Параметры__:

__`lang`__: Язык запроса

__`rll`__: Набор точек маршрута

[&#8593; Содержание](#Содержание)

### Панорамы

Будет отдан один JSON файл. Никакие параметры не учитываются.

__Адрес__: `/mocks/panorama/panorama/1.x`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[hosts][panoramasApi]=http://podrick.c.maps.yandex-team.ru/mocks/panorama/
```

[&#8593; Содержание](#Содержание)

### Погода

Моки над [API погоды](https://wiki.yandex-team.ru/weather/api/). Будет отдан JSON файл в зависимости от `geoid`.

__Адрес__: `/mocks/weather/v1/forecast`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][weatherApi]=http://podrick.c.maps.yandex-team.ru/mocks/weather/
```

__Параметры__:

Поддерживается часть параметров:

__`geoid`__: id региона из геобазы Яндекса

По умолчанию используется регион Москвы: `213`.

- `213` - Москва
- `10309` - Бишкек

[&#8593; Содержание](#Содержание)

### Sendmail

Моки для [отправки писем](https://wiki.yandex-team.ru/AndrejjLarionov/Dev/SendMailServant/). Будет отдан XML файл.

__Адрес__: `/mocks/sendmail/send-mail`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][sendmailv6]=http://podrick.c.maps.yandex-team.ru/mocks/sendmail/
```

[&#8593; Содержание](#Содержание)

### Общественный транспорт

В зависимости от переданных _query_ параметров будет отдан JSON файл. Если параметр не указан в запросе, то используется его имя.

Пример имени файла: `station__lh_96035181_ru_RU_uri_mode.json`

Если мок не найдет, то данные будут загружены с настоящего бекенда, и в последствии для данного запроса будет отдаваться мок. Готовые моки хранятся на гитхабе: [maps/mocks](https://github.yandex-team.ru/maps/mocks/tree/master/masstransit).

__Важные замечания__:

- Параметр `format` должен быть равен `json`, иначе мок не будет сохранен.

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][masstransitApi]=http://podrick.c.maps.yandex-team.ru/mocks/masstransit/
```

[&#8593; Содержание](#Содержание)

#### Все нитки маршрута

Моки для получения информации обо [всех нитках маршрута ОТ](https://wiki.yandex-team.ru/maps/api/internal/masstransit/route/).

__Адрес__: `/mocks/masstransit/1.x/route.xml`

__Параметры__:

__`id`__: Идентификаторы остановок (обязательно)

__`lang`__: Язык запроса

[&#8593; Содержание](#Содержание)

#### Сервис остановок

Моки для получения информации об [остановках ОТ](https://wiki.yandex-team.ru/maps/api/internal/masstransit/stops/).

__Адрес__: `/mocks/masstransit/1.x/stops.xml`

__Параметры__:

__`id`__: Идентификаторы остановок (обязательно)

__`lang`__: Язык запроса

__`uri`__: Идентификатор геообъекта

__`mode`__: Режим (например, `prognosis`)

[&#8593; Содержание](#Содержание)

#### Нитка маршрута

Моки для получения информации об [нитке маршрута ОТ](https://wiki.yandex-team.ru/maps/api/internal/masstransit/threads/).

__Адрес__: `/mocks/masstransit/1.x/threads.xml`

__Параметры__:

__`id`__: Идентификаторы остановок (обязательно)

__`lang`__: Язык запроса

[&#8593; Содержание](#Содержание)

### Фото организации

В зависимости от переданных _query_ параметров будет отдан Protobuf файл. Если параметр не указан в запросе, то используется его имя.

Если мок не найдет, то данные будут загружены с настоящего бекенда, и в последствии для данного запроса будет отдаваться мок. Готовые моки хранятся на гитхабе: [maps/mocks](https://github.yandex-team.ru/maps/mocks/tree/master/sprav-photo).

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][spravPhotoApi]=http://podrick.c.maps.yandex-team.ru/mocks/sprav-photo/
```

[&#8593; Содержание](#Содержание)

#### Список фото

__Адрес__: `/mocks/sprav-photo/v2/business/list/`

__Параметры__:

Поддерживаются все параметры [соответствующей ручки](https://wiki.yandex-team.ru/hevil/maps/photos/#get/v2/business/list).

[&#8593; Содержание](#Содержание)

### Саджест логина неавторизованным пользователям

В зависимости от переданных _query_ параметров будет отдан JSON c данными о предполагаемом аккаунте пользователя. Если параметр не указан в запросе, то вернется пустой массив.

__Важные замечания__:

- Моки забираются только из русского саджеста: [`passportApi_RU`]

__Адрес__: `/mocks/passport-api`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[hosts][passportApi]=https://podrick.c.maps.yandex-team.ru/mocks/passport-api/
```

__Параметры__:

__`yu`__: yandexuid пользователя.


[&#8593; Содержание](#Содержание)

### Дорожные события

Моки для получения данных экспорта дорожных событий.

__Адрес__: `/mocks/jams-arm`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][jamsArm]=http://podrick.c.maps.yandex-team.ru/mocks/jams-arm/
```

[&#8593; Содержание](#Содержание)


### Афиша

Моки для получения данных АПИ Афиши.

__Адрес__: `/mocks/afisha`

Пример ссылки с использованием `host_config`:

```
https://l7test.yandex.ru/maps/?host_config[inthosts][afisha]=http://podrick.c.maps.yandex-team.ru/mocks/afisha/
```

__GET-параметры__:

__`query_name`__: Идентификатор потребителя Афиши. Произвольная строка, по которой АПИ Афиши распознаёт запросы в
своих логах. Например, БЯК обращается к ним с параметрами `?query_name=maps-afisha-events` и `?query_name=maps-afisha-event-info`


__POST-параметры__:

__`query`__: Строка запроса в GraphQl-формате. Из неё извлекаются два уникальных параметра запроса: `id` кинотеатра и
дата запроса `date` вида `2018-10-26`.

### Рассылятор

Проверяет, подписан ли пользователь

__Адрес__: `/mocks/sender/api/0/*/maillist/*/email/<user_email>`

Параметр задаётся в запросе, как часть пути.

__`user_email`__: Адрес пользователя.

[&#8593; Содержание](#Содержание)
