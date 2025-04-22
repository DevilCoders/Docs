# Доступ к API

Доступ к API осуществляется по *логину лаборатории* и *API-ключу*. Их необходимо передавать во всех запросах к API в заголовках:

* `X-External-Service: <логин лаборатории>`
* `X-External-Api-Key: <API-ключ>`

Логин и API-ключ выдаются лаборатории после подписания договора с Яндексом. Способ их получения
обсуждается индивидуально с каждой лабораторией. По умолчанию данные высылаются по электронной почте.

## CORS

Согласно политике [CORS](https://ru.wikipedia.org/wiki/Cross-origin_resource_sharing), при обращении к API необходимо также передавать заголовок **Origin**. В нем необходимо
 указывать домен 'https://labs-api.yandex.ru':

* `Origin: https://labs-api.yandex.ru`

## Пример

```curl
curl 'https://labs-api.yandex.ru/lab/v1/buckets?lab_id=my_lab&date=2020-08-09' \
 -H 'X-External-Service: msk_lab' \
 -H 'X-External-API-Key: Njrgku45vmklf34gffgft44saafvvvqqnrfmgl9h'
 -H 'Origin: https://labs-api.yandex.ru'
```
