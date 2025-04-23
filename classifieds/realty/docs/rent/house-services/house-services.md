## ЖКХ в Аренде

Сервис ЖКХ в Аренде позволяет автоматизировать работу с услугами ЖКХ для жильцов и пользователей, упрощая передачу
показаний и квитанций и делая прозрачней выставление счетов за услуги. Модуль ЖКХ позволяет жильцу до подписания
договора ознакомиться с условиями, которые выставляет собственник по услугам в квартире. Сервис своевременно напоминает
обеим сторонам о необходимых действиях, не позволяя тем самым забыть отправить показания или же оплатить выставленный
счёт.

Основной функционал ЖКХ состоит из следующих модулей:

- [**Настройки ЖКХ**](https://docs.yandex-team.ru/realty/rent/house-services/settings) - требования собственника по ЖКХ,
  с которыми он сдает квартиру
- [**Квитанции**](https://docs.yandex-team.ru/realty/rent/house-services/receipts) - квитанции за электричество, воду и
  т.п.
- [**Платежи**](https://docs.yandex-team.ru/realty/rent/house-services/payments) - выставление счета и его оплата.
  Подтверждение оплаты
- [**Счётчики**](https://docs.yandex-team.ru/realty/rent/house-services/meter-readings) - передача показаний по
  счетчикам.
- [**Нотификации**](https://docs.yandex-team.ru/realty/rent/house-services/notifications) - нотификации ЖКХ

Структура БД:

![db](img/db.png)

1. `owner_request` - Заявление собственника. Содержит настройки ЖКХ и статус этих настроек.

- `responsible_for_payment` - Кто будет оплачивать коммуналку?
- `should_send_receipt_photos` - Должен ли жилец слать фотографии квитанции?
- `should_send_readings` - Должен ли жилец слать показания счетчиков?
- `should_tenant_refund` - Должен ли жилец возвращать деньги за коммуналку?
- `payment_confirmation` - Должен ли жилец присылать фото с подтверждениями оплаты?
- `has_services_paid_by_tenant` - Есть услуги, которые жилец оплачивает сам?
- `settings_status` - статус настроек (заполнено ли жильцом, подтверждено ли жильцом)

2. `house_service` - Счетчик или услуга.
3. `period` - Период (месяц), во время которых оказываются коммунальные услуги.

- `period` - первое число месяца периода текущий группы
- `meter_readings_status` - общий статус показаний
- `bill_status` - статус счёта
- `receipt_status` - статус квитанций
- `payment_confirmation_status` - статус подтверждения платежей

4. `meter_readings` - Показания по одному конкретному счётчику за данный месяц.

- `status` - Статус показаний.

Обработка периодов (`period`) и показаний счётчиков (`meter_readings`) осуществляется в вотчере
`realty/realty-rent/realty-rent-scheduler/src/main/scala/ru/yandex/realty/rent/watcher/RentContractWatcher.scala`

1. `ru.yandex.realty.rent.stage.contract.CreatePeriodStage` - стейдж создания периодов и показаний запускается, когда
   договор вступает в силу и когда необходимо создать период и соответствующие показания на текущий месяц. Старые
   периоды и показания игнорируются
2. `ru.yandex.realty.rent.stage.contract.ProcessPeriodStatusesStage` - стейдж обновления статусов при каждом прогоне
   обновляет статусы периода в соответствии со статусами показаний

Обработка показаний счетчиков осуществляется в вотчере
`ru.yandex.realty.rent.watcher.MeterReadingsWatcher`

1. `ru.yandex.realty.rent.stage.meter.readings.SendMeterReadingsStage` - стейдж отправления показаний через 15 минут
2. `ru.yandex.realty.rent.stage.meter.readings.ShouldBeSentMeterReadingsStage` - стейдж изменения статуса показаний
   сообразно настройкам счётчика
3. `ru.yandex.realty.rent.stage.meter.readings.ExpiredMeterReadingsStage` - стейдж просрочки показаний после истечения
   срока отправления из настроек счётчика

Валидация запросов ручек осуществляется в

1. `ru.yandex.realty.rent.backend.validator.HouseServiceValidator` - валидация изменений счётчика в настроках
2. `ru.yandex.realty.rent.backend.validator.PeriodValidator` - валидация действий в периоде (отправление показаний,
   квитанций, подтверждений платежей, выставления счёта)
