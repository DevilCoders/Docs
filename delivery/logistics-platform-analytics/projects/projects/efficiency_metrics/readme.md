- определять тип сапплая (термокороб, термосумка, медкниижка, сммс-подтвереждениие etc)
к 1) типу сапплая на линии можно смотреть по тегам из кубика Димы Фролова 
https://yql.yandex-team.ru/Operations/YBAZSyyLNR8WsxKHrRkLqQBwFIZjyYtdThkc4wJrZp8=

Он забирает множество тегов водителя из логов приоритетов. Вообще с тегами есть некоторая боль, сейчас dwh готовят нам объект по тегам

про авто курьеров - для РФ считаем их по водителям, которым были доступны больше 80% времени только 2 тарифа - express и courier. для остального мира по тегу auto_courier

удобнее всего теги смотреть или по кубику Димы, или по моей витрине, собранной на основе его кубика:
- home/taxi-analytics/d-captain/driver_cube_v3
- home/taxi-analytics/alena-lukina/express/supply/export_gp

Вот код сборки моей витрины на основе кубика Димы
https://github.yandex-team.ru/taxi-dwh/business_analytics_cron/blob/master/logistics/supply/vitrina_mazo/yt_supply_data_v2.sql


по моей витринке
- тег автокурьера
для РФ - autocourier_sh_share >= 0.8, для мира - auto_courier_tag >= 0.8
- тег пешика walking_courier_tag >= 0.8
- термокороб - thermobox_option_on_tag = True
- термобэг - thermobag_confirmed_tag = True

- опредеелять тип заказа ()

к 2) supply_plan - это требования к заказу
https://github.yandex-team.ru/taxi-dwh/business_analytics_cron/blob/master/nbobukh/20200712_orders_datamart/yt_orders_query.sql - вот тут поиском supply_plan найдешь
но также есть еще спецтребования типо большого кузова и другого, которые не как supply plan, а как order_requirments.cargo_type реализованы
вот пример: https://yql.yandex-team.ru/Operations/X7-nmmim9VhRBF4KIyYtRyvNdX_3hjPsFRCNEEYF7LE=

из витринок, где это собрано:
home/taxi-dwh/summary/dm_order/
home/taxi-analytics/nbobukh/express/demand/orders/
home/taxi-analytics/alena-lukina/express/demand/orders
моя витрина - уменьшенная версия Никитиной, просто она реплицируется на гринплам

- начать писать в квоту логистики
- запросить квоту на операции

- 


# TODO
Важно:
- сейчас не считаю paid waiting

