# Store

## Подготовка

```bash
$ npm i
```

Для запуска нам так же необходим tvmtool и [api](../paskills-api).

## Запуск

```bash
$ export PASKILLS_NEWS_API_CSRF_TOKEN='salt'
$ npm run dev
```

### Запуск с API из приёмки

```bash
$ PASKILLS_API_URL=http://paskills-common-testing.alice.yandex.net/priemka/api
```

Сайт будет доступен по [https://localhost.msup.yandex.ru/store](https://localhost.msup.yandex.ru/store)

## Используемые библиотеки:

-   Для универсального рендеринга используется [next.js](https://github.com/zeit/next.js/)
-   Для роутинга [next-routes](https://github.com/fridays/next-routes)
-   typescript
-   sass
-   axios

## Для загрузки статики которая должна лежать под доменом (robots.txt, etc...)

Должны быть прописаны в переменных окружения:

```
PASKILLS_S3_ACCESS_KEY_ID=
PASKILLS_S3_SECRET_ACCESS_KEY=
```
