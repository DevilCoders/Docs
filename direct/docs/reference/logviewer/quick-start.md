# Быстрый старт

LogViewer — интерфейс просмотра логов Директа. Например:
- действий над объектом в интерфейсе,
- действий над объектом в API,
- модерации,
- отправленных писем
  и т.д.

Живёт по адресу [https://direct.yandex.ru/logviewer/](https://direct.yandex.ru/logviewer/)


## Описание полей

**Log** — список логов, по которому необходимо получить данные. Обязательное поле.  
**Range** — временной промежуток, за который необходимо получить данные. По умолчанию берется текущий день.  
**Filter condition** — условие поиска для выбранных значений. Необязательные поля, можно выбрать несколько.  
**Columns** — список колонок, которые будут отображены.  
**Show stats** — группировка по выбранным колонкам.  


## Примеры использования

#### В интерфейсе что-то пошло не так, знаем reqid
В `Log` выбираем `messages`, в `Range` устанавливаем нужный период, в `Filter condition` выбираем `trace_id` и вставляем значение заданного reqid. После этого нажимаем кнопку `Show`. В колонке `message` будет текст ошибки

Например, при открытии главной страницы нового интерфейса видна ошибка
> Что-то пошло не так. Внутренняя ошибка сервера. При обращении в службу поддержки укажите следующие данные: reqId = 52704129967899017

В логах находим [текст ошибки](https://direct.yandex.ru/logviewer/short/0np0dwUW3xZtan)

#### Расход баллов клиента в API
В `Log` выбираем `ppclog_api`, в `Range` устанавливаем нужный период, в `Filter condition` выбираем `uid` и вставляем логин клиента. В выпадающем списке отмечаем колонку `units`. После этого нажимаем кнопку `Show`. В колонках `cmd` и `units` находим сколько стоила каждая команда клиенту

Например, хотим узнать расход баллов для клиента `ra-elama` в заданном временном промежутке.
В логах находим [расход](https://direct.yandex.ru/logviewer/short/H0kVGxfW3vaLXL)


#### Посмотреть изменения объекта в БД
В `Log` выбираем `binlog_rows_fields_v2`, в `Range` устанавливаем нужный период, в `Filter condition` выбираем `table` и вставляем значение нужной нам таблицы, в которой лежит объект, и задаем ограничения в `primary_key`. В колонке `row` будет json-объект с изменениями

Например, нужно посмотреть изменения статуса модерации кампании с идентификатором `61780828`.  
В логах находим [изменения](https://direct.yandex.ru/logviewer/short/dVvtg-u13vaCVi)
