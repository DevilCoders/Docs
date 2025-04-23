# Микросервис офферного хранилища, отвечающий за парсинг фидов (Push-Parser)

Работает в двух режимах:
- основном, при котором результат парсинга отправляется в piper для внесения соответствующих изменений в хранилище.
- валидации (чек-фид), при котором никакие изменения не применяются, а только проверяется корректность фида.

Взаимодействует с другими сервисами через топики logbroker-а.

Задания приходят от MBI в формате [FeedParsingTask](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/UpdateTask.proto?rev=r9344218#L20) из [GeneralizedMessage](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/GeneralizedMessage.proto?rev=r6861451#L18)

Формат ответа: [FeedParsingTaskReport](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/UpdateTask.proto?rev=r9344218#L160)

Исходный код разбит на две части:
- [qparser](https://a.yandex-team.ru/arc_vcs/market/idx/feeds/qparser) - C++ модуль, в котором непосредственно реализована логика парсера
- [пуш-робот](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/parser) - Python обвязка, которая вычитывает топики, формирует настройки и запускает сам qparser

## Основной режим

Маркетные фиды:
- market-indexer/prod/united/datacamp-market-update-tasks ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-market-update-tasks?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Flogs%2Fmarket-datacamp-update-task-log-market), [yql](https://yql.yandex-team.ru/Operations/Yl7n9q5OD3WOjGFIRcxoKVfe-AFxRFagPjyW8EgIL8c=))
- market-indexer/testing/united/datacamp-market-update-tasks ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-market-update-tasks?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Flogs%2Fmarket-datacamp-update-task-log-testing-market), [yql](https://yql.yandex-team.ru/Operations/Yl7n9q5OD3WOjGFIRcxoKVfe-AFxRFagPjyW8EgIL8c=))

> Фиды директа:
> - market-indexer/prod/white/datacamp-update-tasks
> - market-indexer/testing/white/datacamp-update-tasks

В случае неуспешного парсинга не по вине партнера (отвалился YT, etc), кладет задание на перепарсинг в технический топик.

Для маркетных фидов:
- market-indexer/prod/united/datacamp-market-push-feeds-technical ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-market-push-feeds-technical?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-push-feeds-technical-market), [yql](https://yql.yandex-team.ru/Operations/Yl8SV9JwbLI3EgGFns7lW6f6I0vvtAzqgcCSA8WWWD0=))
- market-indexer/testing/united/datacamp-market-push-feeds-technical ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-market-push-feeds-technical?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-push-feeds-technical-testing-market), [yql](https://yql.yandex-team.ru/Operations/Yl8SV9JwbLI3EgGFns7lW6f6I0vvtAzqgcCSA8WWWD0=))

> Для фидов директа:
> - market-indexer/prod/white/datacamp-push-feeds-technical
> - market-indexer/testing/white/datacamp-push-feeds-technical

Ответ в MBI отправляет через топики:
- market-indexer/prod/white/datacamp-reports-for-mbi ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/white/datacamp-reports-for-mbi?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-reports-for-mbi-white), [yql](https://yql.yandex-team.ru/Operations/Yl8ozbq3k_zTB7HCNkQ5fkZRwMTRPybvY3nEy4uCna0=))
- market-indexer/testing/white/datacamp-reports-for-mbi ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/white/datacamp-reports-for-mbi?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-reports-for-mbi-testing-white), [yql](https://yql.yandex-team.ru/Operations/Yl8ozbq3k_zTB7HCNkQ5fkZRwMTRPybvY3nEy4uCna0=))

Результатом парсинга является набор офферов в формате [DatacampOffer](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto)
которые записываются в топики:
- market-indexer/prod/united/datacamp-qoffers ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-qoffers?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-united-datacamp-qoffers-log), [yql](https://yql.yandex-team.ru/Operations/Ykq6R1Z1O-uTG-2m4Wby1HZvLsN3fbAu0hWMqvaRzsI=))
- market-indexer/prod/blue/datacamp-qoffers ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-qoffers?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-qoffers-log), [yql](https://yql.yandex-team.ru/Operations/Ykq6R1Z1O-uTG-2m4Wby1HZvLsN3fbAu0hWMqvaRzsI=))

Каждый запуск фиксируется пуш-роботом в таблице ClickHouse **market.robot_sessions** ([пример yql запроса](https://yql.yandex-team.ru/Operations/Yl70AJfFt_90kAiByKZmp-jC3tXO9DZbFkudWRPrZUo=))

> Можно быстро поменять период обхода фидов в MBI: [MBI-64507](https://st.yandex-team.ru/MBI-64507)

## Валидация фидов (чек-фид)

В задании чек-фид промаркирован флагом is_check_task=*true*.

Задания на валидацию фида приходят от MBI в топики:
- market-indexer/prod/blue/datacamp-check-tasks ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-check-tasks?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Flogs%2Fmarket-datacamp-check-tasks-log-blue), [yql](https://yql.yandex-team.ru/Operations/Yl8rhbq3k_zTB7ZyKHmtzz3uMC8mbWemG7pPUQn7Y9c=))
- market-indexer/testing/blue/datacamp-check-tasks ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/blue/datacamp-check-tasks?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Flogs%2Fmarket-datacamp-check-tasks-log-testing-blue), [yql](https://yql.yandex-team.ru/Operations/Yl8rhbq3k_zTB7ZyKHmtzz3uMC8mbWemG7pPUQn7Y9c=))

Ответ в MBI отправляет через топики:
- market-indexer/prod/blue/datacamp-check-tasks-result ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-check-tasks-result?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Flogs%2Fmarket-datacamp-check-tasks-result-log-blue), [yql](https://yql.yandex-team.ru/Operations/Yl8rnrq3k_zTB7aTTL6vQTvWMFAttcAADgvFMr02oKQ=))
- market-indexer/testing/blue/datacamp-check-tasks-result ([lb](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/blue/datacamp-check-tasks-result?page=statistics&type=topic), [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Flogs%2Fmarket-datacamp-check-tasks-result-log-testing-blue), [yql](https://yql.yandex-team.ru/Operations/Yl8rnrq3k_zTB7aTTL6vQTvWMFAttcAADgvFMr02oKQ=))

Каждый запуск чек-фида фиксируется пуш-роботом в таблице ClickHouse **market.parser_checkfeed_sessions** ([пример поиска по shop_id](https://yql.yandex-team.ru/Operations/YKVKbb94hkmJz_4PfmrPaxo9KFQ5XX963L7iXE0KIt8=))

Мониторинг по кодам возврата чек-фида: [Прод](https://monitoring.yandex-team.ru/projects/market-indexer/explorer/queries?range=1w&q.0.s=%7Bproject%3D%22market-indexer%22%2C%20cluster%3D%22production%22%2C%20service%3D%22sessions%22%2C%20sensor%3D%22checkfeed_retcode_%2A%22%2C%20period%3D%22one_hour%22%7D&normz=off&colors=auto&type=auto&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default), [Тестинг](https://monitoring.yandex-team.ru/projects/market-indexer/explorer/queries?range=1w&q.0.s=%7Bproject%3D%22market-indexer%22%2C%20cluster%3D%22testing%22%2C%20service%3D%22sessions%22%2C%20sensor%3D%22checkfeed_retcode_*%22%2C%20period%3D%22one_hour%22%7D&normz=off&colors=auto&type=auto&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default). Наиболее распространенные коды возврата: 0 - фид валидный, 114 - ошибка парсинга.

Технические подробности можно почитать тут:
- [Чек-фид через Логброкер](https://wiki.yandex-team.ru/users/a-anikina/check-feed-cherez-logbroker/),
- [Supplier feed от MBI](https://wiki.yandex-team.ru/users/emgusev/supplier-feed-lb/)

## Фид архив { #feed_archives }

Сессии парсера сохраняются в архиве:
- [production](http://idxapi.vs.market.yandex.net:29334/v1/feed_archives/get?feed_id=1491615)
- [testing](http://idxapi.tst.vs.market.yandex.net:29334/v1/feed_archives/get?business_id=10441467&checkfeed=true)

CGI параметры:
- для поиска по основным сессиям: ```?feed_id=``` или ```session_id=``` или ```business_id=``` или ```shop_id=```
- для поиска по сессиям чек-фидов: ```?checkfeed=true&``` + ```business_id=``` или ```shop_id=```
- дополнительные cgi параметры: ```days, count```

Про идентификатор сессии подробнее в [документации саппорта](https://wiki.yandex-team.ru/users/thesonsa/market/markethow/partner-supp-tips/#kaknajjtisessijuparsingachtobyposmotretlog)

Содержимое фида в ```fetched.xml.gz``` или ```cached.gz``` или ```downloaded.gz```


## Метрики воркеров

Графики и дашборды парсера на [странице](https://docs.yandex-team.ru/market-datacamp/support/metrics#parser).

Основные [метрики](https://yql.yandex-team.ru/Operations/YehX5C3DcI9JLK0uamZ6nyMF0n2OUfAE3_d39hKff10=) производительности воркеров парсера:
- time_of_response_send - время, затраченное на отправку ответов в MBI (в ms)
- time_in_wait - время простоя (в ms)
- time_in_parsing - время, затраченное на парсинг time_in_parsing (в ms)
- memory_utilization - утилизация памяти воркером
- cpu_utilization - утилизация CPU

## Deploy { #deploy }
Основной режим:
- [production](https://deploy.yandex-team.ru/stages/production_market_datacamp-parser)
- [prestable](https://deploy.yandex-team.ru/stages/prestable_market_datacamp-parser)
- [testing](https://deploy.yandex-team.ru/stages/testing_market_datacamp-parser)

Чек-фид:
- [production](https://deploy.yandex-team.ru/stages/production_market_datacamp-checkfeed)
- [prestable](https://deploy.yandex-team.ru/stages/prestable_market_datacamp-checkfeed)
- [testing](https://deploy.yandex-team.ru/stages/testing_market_datacamp-checkfeed)

## ЦУМ
- [release pipeline](https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/datacamp-parser)

## ITS
- [основной режим](https://nanny.yandex-team.ru/ui/#/its/locations/market/datacamp/parser-blue)
- [чек-фид](https://nanny.yandex-team.ru/ui/#/its/locations/market/datacamp/parser-white)
