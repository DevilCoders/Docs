## Счёт

Если в настройках ЖКХ собственник указал, что жилец должен возвращать деньги за коммуналку, то собственник должен
ежемесячно выставлять счёт за услуги ЖКХ, а жилец должен его оплачивать. В случае отклонения счёта собственник может
пересмотреть/дополнить счёт (указав, например, новые фотографии, подтверждающие сумму счёта) и выставить его вновь. Счёт
привязан к периоду (`Period`) и может находиться в следующих статусах:

- **Не выставлен** - счёт не выставлен и еще рано это делать. На текущий момент период находится в этом статусе с 1
  числа месяца периода по последнее число этого месяца.
- **Можно выставлять** - счёт не выставлен, но выставить его уже возможно. На текущий момент период находится в этом
  статусе с последнего числа месяца периода по 15 число следующего месяца.
- **Необходимо выставлять** - счёт не выставлен, но должен быть выставлен. На текущий момент период переходит в этот
  статус с 15 числа месяца, следующего за месяцем периода, или в день расторжения договора.
- **Необходимо оплатить** - счёт выставлен, но еще не оплачен. Выставить счёт можно при статусах "Можно выставлять", "
  Необходимо выставлять" и "Отклонено".
- **Отклонён** - счёт был выставлен собственником и отклонен жильцом. Отклонить счёт можно в статусе "Необходимо
  оплатить", обязательно указав причину отклонения.
- **Оплачен** - счёт был оплачен жильцом. Переход в этот статус осуществляется после оплаты.

Жизненный цикл счёта:

![bill lifecycle](img/bill.png)

После того как собственник вновь выставляет счёт после отклонения, старый счёт становится недоступным в интерфейсе, но
хранится у нас в бд (мягкое удаление). Счёт также содержит в себе время выставления. Успешно выставить можно только один
счёт за месяц. Однако, отклонять и выставлять новые счета, удаляя старые, можно сколько угодно. Таким образом, за период
может быть успешно выставлен и оплачен только один счёт.

Платёж к счёту создается после выставления счёта. Происходит это в стейдже:
`ru.yandex.realty.rent.stage.contract.CreateHouseServicePaymentStage`

Генерация платежа происходит посредством:
`ru.yandex.realty.rent.backend.payment.HouseServicePaymentsGenerator`

После отклонения и повторного выставления счёта этот платеж обновляется в том же стейдже на основе платежа, который
генерируется заново.

## Подтверждение оплаты

Логика работы с подтверждением оплаты аналогична логике работы с квитанциями. Если собственник в настройках ЖКХ указал
необходимость присылать подтверждение оплаты (флаг "Подтверждение оплаты"), то жилец ежемесячно должен присылать фото
этих подтверждений. Для этого жилец должен добавить все необходимые фотографии платежей и отправить их собственнику на
рассмотрение. Собственник может отклонить фотографии и тогда жильцу вновь необходимо будет добавить фотографии и
отправить их на рассмотрение собственником. Подтверждения платежей могут находиться в следующих статусах:

- **Не отправлено** - подтверждения не отправлены и еще рано это делать. На текущий момент является техническим и не
  используется.
- **Можно отправлять** - подтверждения не отправлены, но их отправление доступно. На текущий момент период находится в
  этом статусе с 1 числа месяца периода по 15 число следующего месяца.
- **Необходимо отправлять** - подтверждения не отправлены, но уже должны быть отправлены. На текущий момент период
  переходит в этот статус с 15 числа месяца, следующего за месяцем периода. То есть подтверждение за октябрь необходимо
  отправить 15 ноября.
- **Отправлено** - подтверждения были отправлены. Отправление подтверждений доступно при статусах "Отправлено" (
  позволяет поменять фотографии), "Можно отправлять", "Необходимо отправлять" и "Отклонено".
- **Отклонено** - подтверждения были отправлены жильцом и отклонены собственником. Отклонить можно подтверждения в
  статусе "Отправлено", обязательно указав причину отклонения.

Жизненный цикл подтверждений платежей:

![bill lifecycle](img/payment-confirmations.png)

После того как жилец вновь отправляет подтверждения после отклонения, старые фотографии становятся недоступны в
интерфейсе, но хранятся у нас бд (мягкое удаление). Все отправленные подтверждения содержат в себе время отправления.
Подтверждения успешно можно отправить только один раз в месяц как некоторое множество фотографий. Однако, отклонять и
отправлять новые вновь, удаляя старые, можно сколько угодно. Таким образом, за период может быть только одно множество
успешно отправленных фото подтверждений платежей. После выставления счета отправление фотографий блокируется.