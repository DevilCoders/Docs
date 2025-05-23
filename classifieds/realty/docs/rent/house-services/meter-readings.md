## Счётчики

Если в настройках ЖКХ собственник указал необходимость высылать показания счетчиков, то ежемесячно жилец должен
отправлять эти показания собственнику. Собственник в свою очередь может отклонить эти показания и потребовать, чтобы
жилец вновь отправил показания. Показания необходимо посылать по всем добавленным в настройках счетчикам. После
отправления показаний жилец может изменить эти показания в течение 15 минут после отправления. После изменений таймер на
15 минут начинает свой отсчет заново. После истечения 15 минут показания изменить уже нельзя.

Показания счётчиков представляются в виде сущностей `MeterReadings` (таблица `meter_readings`), которые создаются вместе
с периодами в стейдже `ru.yandex.realty.rent.stage.contract.CreatePeriodStage`. На каждый счётчик `house_service` для
каждого периода создаются свои показания.

Счётчики могут находиться в следующих статусах:

- **Не отправлено** - показания не отправлены и еще рано это делать. На текущий момент счетчики находятся в этом статусе
  с 1 числа месяца периода по день их отправления, указанный в настройках ЖКХ.
- **На отправление** - показания будут отправлены через определенный промежуток времени и пока их возможно изменить.
  Отправить показания можно только в статусах "Не отправлено", "На отправление", "Необходимо отправлять", "Отклонено"
  и "Просрочено"
- **Необходимо отправлять** - показания не отправлены, но должны быть отправлены. На текущий момент счетчики переходят в
  этот статус в день, с которого можно передавать показания (указанный в настройках).
- **Отправлено** - показания счетчиков были отправлены собственнику и изменение их жильцом уже недоступно.
- **Отклонено** - показания были отклонены собственником. Отклонить показания можно только в статусе "Отправлено",
  обязательно указав причину отклонения.
- **Просрочено** - показания счетчиков не были отправлены вовремя. На текущий момент счетчики переходят в этот статус на
  следующий день после дня, до которого необходимо передавать показания. Этот день указан в настройках счетчика.

Существуют также агрегированные статусы по счётчикам, хранящиеся в периоде (поле `meterReadingsStatus` в `Period`).

- **Не отправлено** - если в периоде есть хотя бы один счетчик в статусе "Не отправлено" и нет ни одного счетчика в
  статусах "Необходимо отправлять", "Отклонено" или "Просрочено".
- **Необходимо отправлять** - если в периоде есть хотя бы один счетчик в статусе "Необходимо отправлять" и нет ни одного
  счетчика в статусах "Отклонено" или "Просрочено".
- **Отправлено** - если в периоде все счетчики находятся в статусе "Отправлено" или "На отправление".
- **Отклонено** - если в периоде есть хотя бы один счетчик в статусе "Отклонено".
- **Просрочено** - если в периоде есть хотя бы один счетчик в статусе "Просрочено" и нет ни одного счетчика в статусах "
  Отклонено".

Для отправки показаний счётчика необходимо указать:

- **Показания** - в количестве, соответствующем тарифу счётчика. Показания за текущий период не могут быть меньше
  показаний за предыдущий период или начальных показаний, указанных собственником в настройках.
- **Фотографии** - фото, подтверждающие показания. Фото первоначально загружаются в аватарницу и после информация о фото
  сохраняется в аренде

На все эти поля есть валидация в момент отправления. Если жилец попытается изменить показания через 15 минут после их
отправления, то ему также будет отправлено сообщение о невозможности это сделать. После отправления собственник может
отклонить показания (попросив, например, прислать более качественные фотографии). Жилец в таком случае должен вновь
повторить процесс отправления фотографий. Все отклоненные показания вместе причинами их отклонения и датой отправления
хранятся в базе данных.

Жизненный цикл показаний:

![meter_readings lifecycle](img/meter-readings.png)