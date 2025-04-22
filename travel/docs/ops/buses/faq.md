---
title: FAQ
---

### Who is on duty today?

Можете узнать в двух местах:

1. Спросите у чат-бота [@YaIncBot](https://t.me/YaIncBot): `/onduty portal / travel-bus`
2. Посмотрите календарь в abc: https://abc.yandex-team.ru/services/sputnik/duty/

### Важные ссылки (дашборды и прочее)

https://wiki.yandex-team.ru/travel/buses/


### Что делает дежурный?

Общие требования те же, что и у Расписаний: [Как действовать во время дежурства](https://wiki.yandex-team.ru/travel/rasp/dev/duty/howto/#kakdejjstvovatvovremjadezhurstva) (за исключением «Окончания дежурства»)

### Как помочь поддержке выполнить возврат денег?

Инструкция: [Ручные возвраты](https://wiki.yandex-team.ru/sputnik/product/handmaid-refunds/)

### Как получить доступ в [страшную админку](https://tickets-admin.bus.yandex.ru/admin/) (aka «админка заказов»)?

Инструкция: [Страшная админка](https://wiki.yandex-team.ru/raspisanija/dev/dostupy-k-adminke/#strashnajaadminka)

### Клиент написал в саппорт, что у нас баг. Воспроизвести не удаётся, в логах нет полезной информации. Что делать?

Тут может помочь запись пользовательской сессии в Вебвизоре. Для её просмотра нужно [получить через idm доступ](https://wiki.yandex-team.ru/jandexmetrika/managerdostup/#kakzaprositpravadostupacherezidm) к счётчику [41853594](https://metrika.yandex.ru/dashboard?id=41853594).
Сессию легко найти по номеру заказа в url: [Видео](https://jing.yandex-team.ru/files/ypetrov/92CC2BB2-F98D-474C-86D7-650F40280161.2b169b8.mov)

### Более подробные логи партнера по заказу
запускаем python:
```python
>>> import binascii
>>> binascii.a2b_base64(b'eyJvcmRlcl9zaWQiOiAxNDQ1MDkwMiwgInRpY2tldF9zaWQiOiAxODc0MTI1Nn0=')
b'{"order_sid": 14450902, "ticket_sid": 18741256}'
```
ищем логи в [деплое](https://deploy.yandex-team.ru/stages/buses-connectors-production/logs?deployUnitId=connectors) по order_sid

### Обращение в саппорт о неправильных точках отправления-прибытия

https://st.yandex-team.ru/BUSES-1493#61796cfe368ee82cc22b0166

### Что делать, если у партнёра перестали работать продажи?

- если выходные/ночь и т.п.:
    1. [отключаем партнёра](#supplier-disable) и инвалидируем кэш, чтобы пользователи не страдали
    2. заводим тикет на разбор/починку
    3. [создаем напоминание](#lsr-reminder) про включение партнёра

- в остальных случаях:
    1. заводим тикет на разбор/починку
    2. разбираемся и чиним (в том числе и делегируя)

### Как отключить партнёра? {#supplier-disable}

1. В переменных деплой юнита `api` в [buses-backend-production](https://deploy.yandex-team.ru/stages/buses-backend-production/config/du-api/box-box)
   убираем из списка `APP_SUPPLIERS=3,5,6,8,9,10,11` id партнёра из [справочника](https://production.rasp.bus.admin.yandex-team.ru/admin/supplier/).
2. Отключаем алерты по продажам:
   - Если по одному партнёру, то меняем список `suppliers` в параметрах [шедулера BUS_SALESMON](https://sandbox.yandex-team.ru/scheduler/25473/view).
   - Если для всех партнёров сразу, то либо останавливаем этот шедулер, либо деактивируем [Buses Sale Alarm](https://solomon.yandex-team.ru/admin/projects/bus/alerts/7b3ce225-8604-46d3-a86f-2a9ce69848f7).

### Как не забыть откатить временные изменения, внесённые во время инцидента? {#lsr-reminder}

1. Опишите в тикете LSR, что сделали в процессе починки.
2. Создайте в этом тикете напоминание для себя: [Настроить напоминание о задаче](https://doc.yandex-team.ru/tracker/external/user/reminder.html)
