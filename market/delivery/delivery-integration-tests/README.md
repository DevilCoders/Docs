# delivery-integration-tests
Интеграционные тесты Доставки и Фулфилмента

Основная страничка: https://wiki.yandex-team.ru/vvod/operationaltesting/avtotesty-java/kak-nachat-rabotat-v-arkadii/

## Запуск локально с генерацией отчета

Обычно делается из консоли примерно так:

`YA_DIR_OUTPUTS='0' ya make -ttt  -F *ondemand.lavka.LavkaTest* --allure=allure-results/report`


Но нужно помнить о том, что фильтр должен трактоваться однозначно, потому как к примеру фильтр `*delivery*` запустит все тесты в проекте т.к. это слово содержится в пути самого проекта.

## Что проверяют

Интеграционные тесты доставки - покрывают регресс флоу заказов для контура checkouter-mdb-lgw(dsm)
ru.yandex.market.delivery.deliveryintegrationtests.delivery
Запускаются по расписанию в шедульной сендбокс таске: https://sandbox.yandex-team.ru/scheduler/25043/tasks?hidden=true&all_tags=false&all_hints=false&limit=20

# Что здесь происходит?

## Структура проекта
Основные пакеты которые нам понадобятся
#### api
доступные API для тестов
#### client
http клиенты для тестов,работают с пакетом api
#### factory/OfferItems
для получения нужных офферов для заказа
#### step
для написания любого теста оперируем шагами для тестов

# Пример создания заказа

```java
    CreateOrderParameters params = CreateOrderParameters
                  .newBuilder(regionId, OfferItems.DROPSHIP_DR.getItem())
                  .paymentType(PaymentType.POSTPAID)
                  .paymentMethod(PaymentMethod.CASH_ON_DELIVERY)
                  .experiment(EnumSet.of(RearrFactor.DEFFERED_COURIER))
                  .build();
    Order order = ORDER_STEPS.createOrder(params);`
```
На какой то конкретный адрес
```java
    CreateOrderParameters params = CreateOrderParameters
                .newBuilder(regionId, item)
                .address(Address.LAVKA_HOUR_SLOT)
                .paymentType(PaymentType.PREPAID)
                .paymentMethod(PaymentMethod.YANDEX)
                .experiment(EnumSet.of(RearrFactor.DEFFERED_COURIER))
                .forceDeliveryId(hourSlot)
                .build();
        Order order = CHECKOUTER_STEPS.createOrder(params);
```

Все pojo используем из клиентов соответствующих модулей

Степы есть практически для всего,например если нам нужна работа с tracker то используем TrackerSteps

```java
        WaybillSegmentDto middleSDWaybillSegment = LOM_ORDER_STEPS.getWaybillSegmentForDS(lomOrder, partnerPVZKirova);
        DELIVERY_TRACKER_STEPS.addCheckpointToTracker(middleSDWaybillSegment.getTrackerId(), DELIVERY_ARRIVED_PICKUP_POINT);
```

Посмотреть доступные stepы можно в пакете steps
