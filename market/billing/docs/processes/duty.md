# Дежурства по мониторингам

TODO описание: что дежурный делает, что не делает, куда смотрит, в чем успех

## Что такое дежурство
Дежурство - поддержание работоспособности сервиса отдельным человеком - дежурным.

Расписание дежурств: <https://abc.yandex-team.ru/services/market_billing/duty/>

## Что может сломаться и как об этом узнать
Есть два основных источника информации о проблемах в сервисе.
1. Мониторинги в juggler.
Корректность работы сервиса проверяется тестами и сводится к набору событий в juggler.
Основной дашборд, на который сведены проверки сервиса: <https://juggler.yandex-team.ru/dashboards/market-billing/>.
Статусы проверок дублируются в телеграм каналы MB.Monitoring.Calls, market-mbi-monitoring (TODO: вставить инвайт ссылки).
2. Кроме мониторингов к дежурному с описанием проблемы могут придти коллеги, смежники, менеджеры и т.д.

## Что дежурный делает
Сразу завести тикет на дежурство, [пример тикетов](https://st.yandex-team.ru/issues/?_f=type+priority+key+summary+description+status+resolution+created+updated+assignee+tags+components+parent+sprint+boards+order+automatizationTools&_q=Queue%3A+MARKETBILLING+Components%3A+duty+Status%3A+%21Closed+%22Sort+by%22%3A+Updated+ASC)

Прикрепить к нему предыдущий тикет. Ожидается, что за каждый день дежурства в тикете на дежурство будет запись, см. ["Как вести тикет на дежурство"](#kak-vesti-tiket-na-dezhurstvo-best-practices);

В первый день принять дежурство у предыдущего деружного, см. раздел ["Передача дежурства"](#peredacha-dezhurstva)

Основное: смотреть на мониторинги и чинить критичное <https://juggler.yandex-team.ru/dashboards/market-billing/>

Как определить очерёдность задач, требующих реакции.
* Есть набор проверок, требующих особого внимания. По ним звонит робот, их состояние публикуется в чатике MB.Monitoring.Calls, они отображаются на дашборде проверок в отдельной группе Phone. Их чиним в первую очередь.
* Следующие по очерёдности проверки, сведённые в группы "Критично ...".
* Отдельно про проверку mbi-tms-18. В неё собираются статусы выполнения большого количества джоб и CRIT на ней почти всегда не несёт информации о реальной поломке, которую нужно чинить. Планируется разделить эту проверку на насколько, чтобы сберечь нервные клетки дежурного.

Если появляется проблема, влияющая на закрытие месяца: записать в тикет на закрытие месяца.
Актуальный тикет есть на дашборде <https://st.yandex-team.ru/dashboard/52727>
Порядок работы с тикетом на закрытие месяца &mdash; в регламенте [{#T}](end-of-month.md)

### Как вести тикет на дежурство (best practices)
* если что-то делаешь, пиши про это в тикет на дежурство или создавай отдельный тикет;
* все тикеты, которыми занимаемся линкуем в тикет на дежурство;
* если ничего нет, то хотя бы вечером напиши в свободной форме, чем занимался;
* тикет на дежурство одновременно и журнал работа для самого дежурного и набор инструкций для следующих — пищи что сделано, что осталось, ЛОГИРУЙ команды!

### Передача дежурства
Для передачи дежурство необходимо организовать встречу с новым дежурным, не переписку в чате, а именно на полчасика посидеть в Zoom-е или в переговорке.
На встречео обсудить:
* какие моники флапают и почему?
* какие остались гореть и почему?
* по предудыщим пунктам успел посмотреть, успел что-то починить, не успел посмотреть.
* какие образовались договоренности со смежниками?
* есть ли что-то, что надо сделать в следующее дежурство (остались ли какие-то задания);
Результат обсуждения записать в тикет на дежурство предыдущего дежурного последним комментарием, после чего дежурство можно считать завершенным и тикет можно закрыть;

### Как чинить:
Накопленные знания по починке можно найти здесь <https://wiki.yandex-team.ru/mbi/development/monitoringssubs/#faq-derevopovsemmonitoringam>.
В этой табличке можно найти информацию по починке простом поиском по номеру мониторинга.

{% note warning %}

Некоторые починки предполагают переобилливание услуг. Нужно очень внимательно проверять необходимость таких действий в период закрытия месяца: последняя неделя предыдущего месяца и первый день следующего. Без крайней необходимости этого лучше не делать.

{% endnote %}

TODO: Написать про время реакции (SLA) на поломанные мониторинги

# Новому дежурному
## Как подготовиться к дежурству
* Подключиться во все чаты с сообщениями мониторинга
* Посмотреть на список критичных проверок (по которым звонит мониторинг), прочитать их описание и как чинить, уточнить непонятные моменты у коллег.
* Если ты дежуришь в первый раз, тебе будет помогать более опытный коллега. Обговори с ним порядок взаимодействия, время общения. Если ты взял тикет на починку, напиши ему об этом.

## Полезное
### Посмотреть запуски и статусы джобы
`select * from MBI_CORE.QRTZ2_LOG where JOB_NAME = 'completeDailyExecutor' order by TRIGGER_FIRE_TIME desc fetch first 10 rows only;`

## Посмотреть данные из таблички oracle в определённый момент в прошлом в пределах кеша истории (полезно для анализа флапов)
`select * from table as of timestamp TO_TIMESTAMP('2018-01-27 12:00:00', 'YYYY-MM-DD HH24:MI:SS');`

## Посмотреть последнее состояние мониторингов
Последние состояния мониторингов, которые выполняются в виде sql можно посмотреть так

`select * from monitor.v_monitorings;`

Если результат обрезан, можно выполнить руками запрос из колонки sql и получить полный результат, например:

`select result, description from mbi_core.v_tms_mbi_tasks where team='BILLING'`

## Ссылки на продовые машины в Няне
### Биллинг в монолите
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbi_billing_sas/>
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbi_billing_vla/>

### market-billing-tms (новое приложение)
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_market_billing_tms_sas>
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_market_billing_tms_vla>

### Бэкенд тарифницы
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbi_tariffs_sas>
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbi_tariffs_vla>

### Биллинг логистики (ПВЗ и Курьерка)
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_tpl_billing_sas>
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_tpl_billing_vla>
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_tpl_billing_iva>

### Чекер
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_market_checker_sas>
<https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_market_checker_vla>


## Самое главное
Keep calm.

Сначала пробуй разобраться самостоятельно.
Если не получается в разумное время, спрашивай в общем чате биллинга или в личке у коллег.
Дежурному помогают все, так как правильная работа сервиса - наша общая задача.

## Ссылки { #links }

* Самые важные события (по которым звонит мониторинг) <https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dmarket_dev%26tag%3Dmarket_mbi_billing%26tag%3Da_mark_market_mbi_billing%26tag%3Dmarket-billing-phone%26tag%3Dmarket%26tag%3Dmarket_mbi%26tag%3Dmarket_production>
* Общий дашборд событий в Juggler: <https://juggler.yandex-team.ru/dashboards/market-billing/>
* Описание проверок и как их чинить <https://wiki.yandex-team.ru/mbi/development/monitoringssubs/>
* Расписание дежурств: <https://abc.yandex-team.ru/services/market_billing/duty/>
* Тикеты на дежурства: <https://st.yandex-team.ru/MARKETBILLING/order:created:false/filter?components=91079>
* Дашборд дежурного: <https://st.yandex-team.ru/dashboard/7553>
* Wiki по дежурству (старая) <https://wiki.yandex-team.ru/market/money/mbi/Biznes-processy-billinga/Dezhurstva-mbi-money/>
* Показатели здоровья сервиса <https://wiki.yandex-team.ru/market/billing/observability/blue/>

