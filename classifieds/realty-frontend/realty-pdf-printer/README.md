# realty-front-pdf-printer

## Описание
Единственная ручка в сервисе /get-document - умеет как по GET (dev + test), для этого параметры нужно положить в GET-параметр `data`, так и в POST (все окружения).
Параметры для шаблонов лежат в [schema-registry](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/realty/pdfprinter/templates.proto).
Для разработки шаблонов используются автосгенерированные типы для Typescript по `.proto` схемам. 
Валидация входных параметров для шаблонов также идет на основе `.proto` схем.

## Версионирование документов
При разработке, если явно не указывать версию в запросе, то проставится версия `development` и сервис будет производить рендеринг шаблона документа из актуальных исходников.
После того, как шаблон документаа готов к релизу, его версию можно собрать/пересобрать через команду:
```bash
make release version=${INT} document=${documentName}`
```

Команда выше запускает продовую `webpack` сборку и складывает версию шаблона в build папку, все когда-либо зарелизенные версии шаблонов документов комитаются и лежат вместе с сервисом.
Сгенерированные шаблоны документов можно найти по пути `build/documents/${document}/versions/${version}`.


## Регламент выпуска новой версии документа
Обсуждается с продуктами. Примерный план такой - версточные баги правим в текущей версии, формулировки/тексты/данные - выпускаем новую.

## Примеры запросов
```bash
curl -X POST https://realty-frontend.pdf-printer.local.dev.vertis.yandex.ru/get-document \
-H 'Content-Type: application/json' \
-d '{"rentKeysHandoverFromManagerToOwner":{}, "version":1}' \
-o test.pdf
```

Пример запроса локально через GET (удобно смотреть в браузере)

```bash
https://realty-frontend.pdf-printer.local.dev.vertis.yandex.ru/get-document?data={"rentKeysHandoverFromManagerToOwner":{},"version":1}
```

Для удобной разработки шаблонов есть параметр `_html=1`.
Если он будет присутствовать в урле запроса, то сервис отдаст не PDF,
а HTML, использованную для генерации PDF, а в косноль бразуера выведется отладочная информация.

```bash
https://realty-frontend.pdf-printer.local.dev.vertis.yandex.ru/get-document?_html=1&data={"rentKeysHandoverFromManagerToOwner":{},"version":1}
```

## Основная информация

| Service | URL                                                                                                                   |
|---|-----------------------------------------------------------------------------------------------------------------------|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-pdf-printer |
| Deploy | https://admin.vertis.yandex-team.ru/services/realty-front-pdf-printer                                                 |
| Grafana | https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?var-job=realty-front-pdf-printer            |

## Хосты

| Environment | URL |
|---|---|
| Testing | http://realty-front-pdf-printer-http.vrts-slb.test.vertis.yandex.net/get-document <br> http://realty-front-pdf-printer-${branch}-http.vrts-slb.test.vertis.yandex.net/get-document |
| Production | http://realty-front-pdf-printer-http.vrts-slb.prod.vertis.yandex.net/get-document |
