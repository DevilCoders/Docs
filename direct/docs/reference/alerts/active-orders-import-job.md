# jobs.ActiveOrdersImportJob.working.production

[Ссылка на проверку](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ActiveOrdersImportJob.working.production&query=&last=1DAY).

## Описание { #description }
Проверяется работа джобы, получающей информацию об открутках из БК и записывающей суммы истраченного на кампаниях.

{% note alert "Это важный алерт" %}

Когда процесс не работает → у нас неактуальные остатки → люди не узнают об окончании денег → не пополняют баланс → мы недозарабатываем.

{% endnote %}


## Диагностика { #diagnostics }
1. Проверяем логи в [logviewer](https://direct.yandex.ru/logviewer/short/PH4UCYFB3ZJP4x) или [YQL](https://yql.yandex-team.ru/Operations/X5AOcVPzVDGI0tQIi_joADj3oGP3KjD44llsPvB_CMA=).
Если в логах присутсвует строка "No suitable cluster", то это значит джоба не нашла доступного YT кластера.
1. Проверяем, что атрибуты YT таблицы OrderStat со стороны БК свежие.
   ```sh
   for dc in sas vla man; do echo $dc; YT_TOKEN_PATH=/etc/direct-tokens/yt_robot-direct-yt yt --proxy seneca-$dc get '//home/yabs/stat/OrderStat/@last_sync_time_bs-chevent-log'; done
   ```
   Выведет:
   ```text
   sas
   "2020-08-18T10:48:01Z"
   vla
   "2020-08-18T10:40:00Z"
   man
   "2020-08-18T10:40:00Z"
   ```
   Если атрибут не обновляется, то надо написать о проблеме в чатик [статистики БК](../chats.md#bs-stat)
1. Проверяем обновление статистики в MySQL.
   ```sh
   dbs-sql pr:ppcdict 'select * from ppc_properties where name like "active_orders_order_stat_bs_chevent_log_timestamp%"'
   ```
   Значения должны соответстовать аттрибутам из таблицы в YT.  
   После починки по ним удобно смотреть, что импорт работает — они должны увеличиваться во всех шардах.

## Примечания { #notes }
После восстановления работы после простоя возможна ситуация с наплывом запросов в Баланс. Тут может наложился резкий рост вообще платежей на какой-то естественный процент платежей без денег, что в перемножении может пробить мониторинг у [Траста](https://st.yandex-team.ru/DIRECTINCIDENTS-660).
Это можно подтвердить просмотром логов в logviewer(balance, method=Balance.CreateRequest2), [графиками в Solomon](https://solomon.yandex-team.ru/?project=trust&cluster=greed-prod&graph=direct_ppc_cumulative&b=2020-08-18T07%3A39%3A13.000Z&e=2020-08-19T01%3A58%3A28.000Z) и [запросами в YQL](https://yql.yandex-team.ru/Operations/XzwfRBpqv72eH-S90eYmxH7Kdoa9jxY4vMj8UYXVpfo=).

## Подробности { #details }
Джоба шардированная, каждый шард обрабатывается независимо:
1. Получает из ppc_property предыдущее обработанное значение "свежести" БКшной таблицы
1. Выбирает свежий кластер по алгоритму, описанному [тут](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/statistics/repository/OrderStatClusterChooseRepository.java#L36).
1. Сравнивает содержимое нашей таблицы [репликатора](../../glossary/glossary.md#b2yt) `//home/direct/mysql-sync/current/combined/campaigns` и БКшной `//home/yabs/stat/OrderStat`, выбирает кампании с отличающейся суммой истраченного
1. Делает адпейт в MySQL записывая суммы, полученные из БКшной таблички
1. Обновляет ppc_property соответствующего шарда, записывая туда значение аттрибута свежести использованной БКшной таблицы

## Ссылки { #links }
- логи в [logviewer](https://direct.yandex.ru/logviewer/short/PH4UCYFB3ZJP4x) (поменяйте дату!)
- логи в [YQL](https://yql.yandex-team.ru/Operations/X5AOcVPzVDGI0tQIi_joADj3oGP3KjD44llsPvB_CMA=) (если есть и настроен доступ к нашем кликхаусу)
- [наша таблица campaigns](https://yt.yandex-team.ru/seneca-sas/navigation?offsetMode=key&path=//home/direct/mysql-sync/current/combined/campaigns) на Seneca-SAS
- [БКшная таблица OrderStat](https://yt.yandex-team.ru/seneca-sas/navigation?offsetMode=key&path=//home/yabs/stat/OrderStat) на Seneca-SAS
- [исходный код джобы](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/java/ru/yandex/direct/jobs/statistics/activeorders/ActiveOrdersImportJob.java)

