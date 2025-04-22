# Сервис для бронирования объявлений

## Назначение

Бронирование Авто.ру - система, предназначенная для брониварония автомобилей, размещенных дилеров на Авто.ру.

Бизнес-задача: https://nda.ya.ru/t/P_2vk5h53VyFyL

## Модули
- api –– API сервиса
- scheduler –– модуль, отвечающий за реагирование на изменение статусов бронирования

## Логи
- [Vertis админка](https://nda.ya.ru/t/Wu_4MvXN3W2owg)

## Метрики
- [gRPC сервер](https://nda.ya.ru/t/QSx1tw_i3W2owC)
- [gRPC клиент api-server](https://nda.ya.ru/t/qlMhJ-483W2owN)
- [Kafka consumers](https://nda.ya.ru/t/qZgGIW693W2owS)

## Sentry
- [api] [booking-api](https://sentry.vertis.yandex.net/verticals/booking-api/)
- [scheduler] [booking-scheduler](https://sentry.vertis.yandex.net/verticals/booking-scheduler/)

## Jaeger
- [api] [booking-api](https://nda.ya.ru/t/5ePdTs733W2jZU)

## Интеграции и процесс
todo

## базы данных

[Тестинг](https://yc.yandex-team.ru/folders/fooqm2o1sunm8jknjhkc/managed-postgresql/cluster/mdb4htf3po9k5lei8a3v),
[Секрет](https://yav.yandex-team.ru/secret/sec-01e8ca2xab94nv0b6yabegq0ak/explore/versions)

[Production](https://yc.yandex-team.ru/folders/fooqm2o1sunm8jknjhkc/managed-postgresql/cluster/mdbs23ieg80cq668srf4),
[Секрет](https://yav.yandex-team.ru/secret/sec-01e8caa0y76216cjppntxzyq78/explore/versions)

[Выгрузка в YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/auto/booking_change_event/1y/2020-01-01)
