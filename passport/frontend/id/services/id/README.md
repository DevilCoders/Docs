# Фронтенд нового личного кабинета ID

https://id.yandex.ru

## Архитектура

[NestJS](https://nestjs.com) + [Next.js](https://nextjs.org).
Для связки используется [nest-next](https://www.npmjs.com/package/nest-next).

В качестве API — [GraphQL](https://graphql.org/).

### Яндексовые библиотеки

* [@yandex-int/nest-common](https://a.yandex-team.ru/arc_vcs/frontend/packages/nest-common) - набор NestJS-модулей общего назначения (cookie, tld, async storage, etc)
* [@yandex-int/nest-infra](https://a.yandex-team.ru/arc_vcs/frontend/packages/nest-infra) — набор NestJS-модулей для работы с инфраструктурой Яндекса (blackbox, tvm, uatraits, csp, etc)

## Запуск

При первом запуске приложения, в файл `/etc/hosts` необходимо добавить следующие строки (это необходимо сделать только один раз):

```
127.0.0.1   localhost.msup.yandex.ru
127.0.0.1   passport-test-internal.yandex.ru
```

### Настройка работы с geobase

Для корректной работы приложения в режиме разработки, необходимо выбрать способ работы с `geobase`.

Предусмотрено 2 способа для работы с `geobase` локально:

1. Загрузка бинарного файла `geodata6.bin`
2. Статичный мок данных в виде json файла

Подробнее про geobase можно почитать [здесь](https://wiki.yandex-team.ru/geotargeting/libgeobase) и [здесь](https://doc.yandex-team.ru/lib/libgeobase5/concepts/interfaces-nodejs.html).

#### 1. Загрузка бинарного файла

> Преимущества данного способа в том, что мы получаем данные, как в проде.

Необходимо скачать один из следующих файлов:

- `geodata6.bin` (1.6GB) - дерево регионов + лингвистики. [скачать](https://proxy.sandbox.yandex-team.ru/last/GEODATA6BIN_STABLE?owner=GEOBASE&attrs=%7B%22released%22:%22stable%22%7D)
- `geodata6-xurma.bin` (130MB) - дерево регионов с сильно уменьшенным числом полей, без лингвистик. [скачать](https://proxy.sandbox.yandex-team.ru/last/GEODATA6BIN_XURMA_STABLE?owner=GEOBASE&attrs=%7B%22released%22:%22stable%22%7D)

По умолчанию скаченный файл должен быть доступен по пути `/var/cache/geobase/geodata6.bin`.

Также при запуске приложения можно указать переменную окружения `GEOBASE_DATA_PATH`:

```bash
GEOBASE_DATA_PATH=/path/to/geodata6-xurma.bin npm start
```

Некоторым методам гео-базы, так же нужна информация о часовых поясах (`tzdata`). Скачать `tzdata` можно по [ссылке](https://proxy.sandbox.yandex-team.ru/last/GEODATATZDATA_STABLE?owner=GEOBASE&attrs=%7B%22released%22:%22stable%22%7D). Скаченный архив можно распаковать в директорию: `/usr/local/share/geobase/`. На выходе должна получиться такая структура:

```bash
/usr/local/share/geobase
├── zones2
└── zones_bin
```

По-умолчанию, поиск файлов происходит в директории `/usr/share/geobase/zones_bin`. Поменять путь можно с помощью переменной окружения: `GEOBASE_TZ_PATH`:

```bash
export GEOBASE_TZ_PATH=/usr/local/share/geobase/zones_bin
```

#### 2. Статичный мок данных

Для того чтобы использовать этот способ локально достаточно установить переменную окружения `GEOBASE_MOCKDATA_PATH` с путём к файлу, где находится мок данных:

```bash
GEOBASE_MOCKDATA_PATH=.geodata/moscow.json npm start
```

В репозитории подготовлен файл с моком данных [.geodata/moscow.json](.geodata/moscow.json)

### Запуск приложения

Далее запускаем скрипты:

```bash
# скачать сертификаты для локального запуска
npm run dev:dotenv

# в отдельном терминале пробросить порт через дев-машину, на которую есть доступы к API Паспорта
$ ssh -L 127.0.0.1:8080:passport-test-internal.yandex.ru:80 python-dev2.passport.yandex.net

# development (запускает TVM-демона, NestJS)
$ npm start

# production mode
$ npm run build
$ npm run start:prod
```

Сервис будет доступен по адресу: https://localhost.msup.yandex.ru/

## Тесты

```bash
# server tests
$ npm run server:unit

# client tests
$ npm run client:unit
```

## Анатомия

```
src/
    client - клиентский код
    server - серверный код
    pages - изоморфный код (выполняется на клиенте и на сервере)
```

## Метрика

* Номер [продового счетчика в Метрике](https://metrika.yandex.ru/dashboard?id=784657) – `784657`
* Номер [тестового счетчика в Метрике](https://metrika.yandex.ru/dashboard?id=88077604) – `88077604`

Запросить доступ к счетчику – https://nda.ya.ru/t/N7SBrd3q4w56GU

События просмотра страниц `pageView` отправляются автоматически при открытии страницы, а также при SPA-переходах между ними.

Чтобы отправить событие, например при клике на кнопку нужно сделать так:

```ts
import { reachGoal } from '@client/shared/libs/metrika';
```

```tsx
<button onPress={() => reachGoal('SOME_NAME_OF_GOAL')}></button>
```

Для дебага отправки событий (все будет логироваться в консоль) можно в открыть страницу с параметром `_ym_debug=1`, например `https://localhost.msup.yandex.ru/finance?_ym_debug=1`. Этот флаг запишется в куку. Чтобы отключить дебаг – нужно просто удалить куку `_ym_debug`

## Статика

* Бакет – https://yc.yandex-team.ru/folders/aku635gj1oc7j1nnb9k2/storage/buckets/yandex-id
* Статика беток выгружается по пути `/yandex-id/pr-<PR_ID>/_next/static/`
* Статика релиза – `/yandex-id/_/_next/static`
* Конфиг для выгрузки статики создаётся в deb-сборке: [build-deb.sh](./tools/build-deb.sh#L127)

Чтобы использовать в Deploy или на железе локальную статику, то необходимо прокинуть ENV-переменную: `USE_LOCAL_ASSET='1'`

## Public

[Дока](./docs/public.md)
