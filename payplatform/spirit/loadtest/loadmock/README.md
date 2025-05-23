# Мок для нагрузочного тестирования

Сервис осуществляет мок хранилища MDS-S3

## МОК MDS-S3

По сути является сервисом nginx с плагином для исполнения lua кода.
Предназначен для мока хранения чеков в хранилище. Сервис запоминает лишь наличие чека, но не запоминает
содержимое переданного чека. При запросе
отдает один и тот же шаблон чека, меняя параметры серийного номера фискального накопителя и номера документа
на указанные в запросе. Фискальный признак устанавливается равным номеру документа.
Шаблоны ответов лежат в `nginx_data_templates/`. Код логики ответа лежит в `nginx_sites/`

Сервис слушает на 7001 порту запросы:
 - `/spirit/receipts/(?P<FS_SN>[0-9]+)/(?P<DN>[0-9]+)`
   - `PUT` позволяет указать, что чек с указанными `SN_SN` и `DN` должен возвращаться сервисом в течение
`MDSS3_EXPIRE_DOCS_SECONDS` секунд
   - `GET` - возвращает чек с указанными `SN_SN` и `DN` при условии, что в течение последних
`MDSS3_EXPIRE_DOCS_SECONDS` секунд был запрос `PUT` с указанными `SN_SN` и `DN`
 - `/spirit/receipts/reset`
   - `GET` сбросить запомненные чеки

Через переменные окружения в сервисе можно задать следующие настройки:
 - `MDSS3_EXPIRE_DOCS_SECONDS` - Число секунд, на которое сервис запоминает наличие переданного чека
 - `MDSS3_REQUEST_DELAY_SECONDS` - задержка ответа сервиса
 - `FN_SN_ALWAYS_HAS_RECEIPT` - серийный номер фискального накопителя для которого сервис всегда будет
отвечать о наличии чека, независимо от наличия `PUT` запросов. (может быть полезно, для тестирования
получения чеков)
 - `FN_SN_ALWAYS_NO_RECEIPT` - серийный номер фискального накопителя для которого сервис всегда будет
     отвечать о отсутствии чека, независимо от наличия `PUT` запросов. (может быть полезно, для тестирования
     помещения чеков)

## Сборка

Собрать докер образ
