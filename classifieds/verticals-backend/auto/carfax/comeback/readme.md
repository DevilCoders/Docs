# Сервис "твоя бывшая"

## Назначение
В личном кабинете дилера появляется новый раздел "Снова в продаже".
В разделе находится листинг с объявлениями от пользователей (частных лиц) авто.ру, 
которые были опубликованы после того, как дилер продал этот автомобиль. 
Данный листинг строим на основе данных из истории размещений, идентифицируя авто по VIN.

https://wiki.yandex-team.ru/vertis/autoru-money-dev/comeback/

## Модули
  - api – http api сервиса
  - consumer – чтение из кафки и обновление данных в базе
  
## Хранилище

Все свои данные сервис хранит в postgresql

## Интеграции

  - Чтение топика кафки воса с изменениями офферов.
  - Получение отчетов по вину из карфакса (история размещений)
  - Получение контента старых объявлений из воса

## Sentry
- [api] [comeback-api](https://sentry.vertis.yandex.net/verticals/comeback-api/)
- [consumer] [comeback-consumer](https://sentry.vertis.yandex.net/verticals/comeback-consumer/)

## Jaeger
- [api] [comeback-api](https://nda.ya.ru/t/_GR35G5W3W36TA)

## Метрики
- [gRPC сервер](https://nda.ya.ru/t/kKShyEM43W36VJ)
- [gRPC клиент api-server](https://nda.ya.ru/t/t6j1rm343W36VQ)
