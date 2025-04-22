# Примеры задач (не забывать про тесты!)
## Новые подписки

Подписки живут в таблице `EMAIL_SUBSCRIPTION`. В таблице `EMAIL_SUBSCRIPTION_DATA` живут параметры подписок, которые у разных типов разные, а в таблице `EMAIL_SUBSCRIPTION_PARAM` описания параметров.

    select es.* from EMAIL_SUBSCRIPTION es, EMAIL_SUBSCRIPTION_DATA esd, EMAIL_SUBSCRIPTION_PARAM esp
    where es.EMAIL in ('vasckinamary@yandex.ru', 'nadenka.vaskina@yandex.ru')
    and es.SUBSCRIPTION_TYPE=11
    and es.ID = esd.EMAIL_SUBSCRIPTION_ID
    and es.SUBSCRIPTION_TYPE = esp.SUBSCRIPTION_TYPE
    and esp.NAME='modelId'
    and esd.EMAIL_SUBSCRIPTION_PARAM_ID = esp.ID
    and esd.VALUE='111260188'
    order by es.ID desc;

Этот запрос ищет подписки на снижение цены на емэйлы 'vasckinamary@yandex.ru', 'nadenka.vaskina@yandex.ru', сделанные на модель с идентификатором 111260188.

### Алгоритм

1. Надо добавить новое значение enum-типа `ru.yandex.market.pers.notify.model.NotificationType`
(Например, для красного маркета при этом надо указать в конструкторе `ru.yandex.market.pers.notify.model.Market#TRANSBOUNDARY_TRADING`)
2. Если подписка является непараметризованной (т.е. не связана с конкретной моделью, типа подписки на снижение цены, или с конкретным отзывом, типа `QA_NEW_ANSWERS`), то надо добавить её по соответствующему ключу в `ru.yandex.market.pers.notify.model.NotificationType#nonParametricTypes`.
3. Также надо подумать, должна ли быть подписка подпиской по-умолчанию или нет `ru.yandex.market.pers.notify.model.NotificationType#defaultTypes`.
Т.е. считается ли емэйл подписанным даже без явно существующей подписки в базе или надо, чтобы в базе была реальная подтвержденная подписка.
Если емэйл может быть подписанным без явно существующей подписки в базе, то новый тип нужно включить в `ru.yandex.market.pers.notify.model.NotificationType#defaultTypes`.
Если же нужно, чтобы подписка не была подпиской по-умолчанию, то надо проверить, не попадает ли она в `defaultTypes` случайно, т.к., например, для белого маркета дефолтными считаются все непараметризованные подписки, которые явно не исключены.
(Например, для красного такого нет)
4. Добавить в mCRM в `types.yson` (при необходимости), сделать миграцию
5. Зазеплоить `market-util`, `market-mailer`, запустить выгрузку клиента нового в артефактори

### Примеры

1. [Новая красная подписка](https://st.yandex-team.ru/MARKETMAIL-1165)
2. [Новые журнальные подписки](https://st.yandex-team.ru/MARKETMAIL-1208)


## Удаление данных пользователя
### Алгоритм

На вход даны какие-то идентификаторы пользователя. Надо всех удалить(отписать).

**1**. Если это email, то всё просто - идём в [карту коммуникаций](https://lilucrm.market.yandex-team.ru/communications), находим все связи.
Если дан puid, то ищем пользователя и его айдиники через yt при помощи [таких запросов](https://paste.yandex-team.ru/746997) 

**2**. Если это просто отписать пользователя от подписки на рекламу (например), то

* заходим на продовую машину `market-utils`, делаем `curl` (контроллер `SubscriptionController`);
* ищем порт приложения (`netstat -nlp`);
* выполняем команду (подставлем все параметры, какие известны)

```bash
http://localhost:20617/api/subscription/type?uid=855075741&email=855075741@lotalot.ru&uuid=c4b7adc0c0e04465bca2ef096b05a0ae&subscriptionType=TRANSBOUNDARY_TRADING_TRIGGER_PUSH
```

После отписки проверить в базе (таблица EMAIL_SUBSCRIPTION) и в yt в таблицу [Subscription](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/crm/platform/facts/Subscription&offsetMode=key)

**3**. Возможно придется отписать от пуш уведомлений.
См контроллер `MobileController` (ручка `unregister`).
Подобное сработает для синего и белого.
Красные подписываются при помощи фейкового email (`uid@lotalot.ru` или `uuid@lotalot.ru`) на email подписку `TRANSBOUNDARY_TRADING_TRIGGER_PUSH`, `TRANSBOUNDARY_TRADING_ADVERTISING_PUSH`.
В этом случае нужно будет дополнительно вызвать ручку из пункта 2.
Все результаты проверяем в таблицах платформы [Subscription](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/crm/platform/facts/Subscription&offsetMode=key)
и [MobileAppInfo](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/crm/platform/facts/MobileAppInfo&offsetMode=key).

### Примеры
* [1](https://st.yandex-team.ru/MARKETMAIL-1206)
* [2](https://st.yandex-team.ru/MARKETMAIL-1177)
* [3](https://st.yandex-team.ru/MARKETMAIL-1193)
* [4](https://st.yandex-team.ru/MARKETMAIL-1199)

## Розыгрыш
пример [тут](https://st.yandex-team.ru/MARKETMAIL-1180)

## Транзакционные письма

### Как это организовано в коде
Есть источники уведомлений, есть потребители (см классы с постфиксом `Consumer`).
Каждый консьюмер можно настроить "читать" определенный вид уведомления (1 консьюмер может обрабатывать несколько видов уведомлений).
Все эти уведомления настраиваются в классе `NotificationSubtype` (cм помеченные `TRANSACTIONAL`).
Например, там есть `BLUE_ORDER_DELIVERY`. Смотрим настройку в классе `FastMailConfig` (все может быть и в отдельном классе конфигов, нужно его только подключить).

```java
 put(NotificationSubtype.BLUE_ORDER_DELIVERY, BLUE_ORDER_LETTER_CONFIG.apply(
    SimpleTemplateResolver.sender(SenderTemplate.BLUE_ORDER_DELIVERY)
   ));
```

Для каждого транзакционного события заводим соответствие в `SenderTemplate`.
Для того, чтобы настроить идентификаторы шаблонов писем в рассыляторе.
Они настраиваеются в файле пропертей `campaigns-production.properties` (для прода) и в `campaign-testing.properties` (для тестинга).

```text
#https://sender.yandex-team.ru/beru/campaign/30293/overview
BLUE_ORDER_DELIVERY=SDY058Z2-NET1
```

Далее, основаная логика отправки письма организована в консьюмере.

##### check

Проверяем контекст события, достаем нужные переменные.
Ходим в различные сервисы.
Если письмо не надно (или не можем) отправить, то валимся с соотвествующей ошибкой, возвращаем ошибочный статус (в этот момент обработка события самого перкратится).

##### getModel

Если все хорошо было в check, то этот метод возвращает контекст письма, то, что мы передаем в рассылятор для рендеринга шаблона.
Заполняем все нужные параметры в мапу. Согласуем их все с [Таней Хамловой](https://staff.yandex-team.ru/khamlova?from=suggest).

##### getPostSendAction

Обработка действий после отправки письма делается двумя способами:

* либо той же джобой, которая дёргает консьюмер
* либо, если что-то не срослось и было исключение, то в отдельной джобе, которая пытается для писем периодически вызываеть postSendAction, для которых он не отработал.

Например, когда шедулится письмо-напоминание с просьбой подтвердить подписку:
`ru.yandex.market.pers.notify.mail.consumer.ConfirmationSenderConsumer#getPostSendAction`

* `true` возвращается, если хочется сказать, что хватит уже этот `postSendAction` обрабатывать, с ним всё ок (или не ок, но бесполезно пытаться дальше:)
* `false`, если надо ещё ретраить (в случае исключения).
Кажется, есть какой-то предельный срок, когда `postSendAction` ретраятся и после него ретраиться уже не будут.
Проверяется текущий статус письма, `postSendAction` которого обрабатывается.

### Как это отлаживать
Все события записываются в бд в таблицу `EVENT_SOURCE`.
По истечение 30 дней переносятся логфеллером в `//logs/market-mailer-notification-event-source-log/1d/`.
У события есть статусы - `NotificationEventStatus`.
* `TYPE_ID` - айдишник события из `NotificationSubtype`.
* `EMAIL`
* `SOURCE_ID` (например для заказов это id заказов)

На текущий момент айдишник сообщения не пишется (имеется ввиду message-id из рассылятора).
Например, чтобы разобрать полеты по письму (или посмотреть, с каким контекстом было отправлено) можно:

1. В логах поискать по id из записи в `EVENT_SOURCE`
2. Зайти в рассылятор в нужный шаблон, выгрузить статистику, найти по email
3. Можно обратиться к рассыляторщикам (например к [Сергею](https://staff.yandex-team.ru/arp106?from=suggest)) и попросить выгрузить контекст из yt.
У нас нет туда доступа. [Пример зарпоса в yt](https://paste.yandex-team.ru/726971)

### Примеры
* [чеки, пример нового события](https://st.yandex-team.ru/MARKETMAIL-1174)
* [мноого новых параметров](https://st.yandex-team.ru/MARKETMAIL-1143)
* [еще один пример](https://st.yandex-team.ru/MARKETMAIL-1066)
* [кредиты](https://st.yandex-team.ru/MARKETMAIL-1170)

## Джобы по расписанию

Чтобы создать одноразовую джобу в мэйлере, надо объявить класс-наследник `ru.yandex.market.tms.quartz2.model.ComplexVerboseExecutor`, как, например, `ru.yandex.market.pers.notify.executor.EuroUsersUnsubscriberExecutor`, и в методе `doRealJob` написать тот код, который будет выполняться.
Джоба должна быть бином, и этот бин надо заиспользовать в файле `tms2-config.xml`.
Сделать примерно то же самое, что сделано для `euroUsersUnsubscriberTrigger` или `yandexStationPaOnSaleSchedulerTrigger` - указано время запуска в далеком будущем.
Сама она в ближайшее время из-за этого не запустится, но можно запустить руками. Для этого есть 2 способа - через http-интерфейс (непроверенный способ, знаю, что есть контроллер `ru.yandex.market.util.tms.TmsJobController`, который приезжает из библиотеки common-husk - можно как-то его использовать) и через telnet.

#### Запуск через telnet

**1**. Надо зайти на public по ssh

**2**. Подключиться по telnet к любому экземпляру мэйлера, на котором хочется запустить джобу, например, к notify01h

```bash
telnet notify01h.market.yandex.net 38609
```

**3**. В сеансе telnet выполнить команду

```bash
tms-run <название executor-а джобы> production
```

Например, для запуска джобы EuroUsersUnsubscriberExecutor в сеансе telnet надо выполнить команду

``` bash
tms-run euroUsersUnsubscriberExecutor production
```

**4**. Потом можно подключиться по ssh к нужному экземпляру мэйлера и грепать логи в поисках результат работы джобы.
Можно также грепать логи на logview.market, но поскольку при ручном запуске джобы известно, где она запустилась, то проще и быстрее читать логи прям на самом экземпляре мэйлера

**5**. Если джоба работает долго, то можно периодически мониторить её состояние также по базе `notify_tms`.
Параметры подключения см. также в датасорцах, ключи `notify.tms.jdbc.url`, `notify.tms.password`, `notify.tms.username`.

Подключившись к базе можно выполнять запрос

    SELECT * FROM notify_tms.QRTZ2_LOG
    where JOB_NAME like '<название executor-а джобы>'
    order by ID desc;

Как только проставится `JOB_STATUS` - значит, джоба завершила работу.
