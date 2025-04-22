#Монетизация пользовательских событий

За основу взята схема https://github.com/YandexClassifieds/billing/pull/304/files

Прием пользовательских событий, факторов и запросов цен к howmuch осуществляем через топики в Broker+Kafka

Фактор - любое уточнение по событию

Сервис сам решает когда можно послать price-request для howmuch для обиливания event+factors

Генерация факторов полностью на стороне внешнего сервиса:
* Задачи для хобо теперь генерит внешний сервис (например по жалобе на звонок или чат), в event-monetization отправляет резолюцию по задаче в связке с id события
* Матчинг звонков телепони на коллцентр тоже осуществляет внешний сервис, в event-monetization отправляет только заматченные на коллцентр id события

Для модели события рассчитываем на наличие поля ((https://github.com/YandexClassifieds/billing/pull/304/files BillingHeader)) + определяем для события уникальный event_type(calls, developer_chats...), id события уникален в рамках domain + event_type

Из кафки сохраняем события, факторы, price-requests в БД:
* Таблица событий: ключ(domain, event_type, id) -> event
* Таблица для факторов: Hobo, коллцентр,... : ключ(domain, event_type, id, snapshot_id) -> Factor_payload


Производные задачи выполняем асинхронно через добавление в очередь и обработкой через watcher
Схема очереди: ключ(shard_id, task_type, process_time, task_id) -> payload
В той же транзакции добавляем задачу на отправку через Broker обновленного снэпшота события в очередь
Если по событию приходит price-request, добавляем в очередь таску на получение цены от howmuch по слепку события

##Scheduler
Cодержит в себе watcher-ы для каждого task_type, совершают постоянный переобход очереди:
* получение цены от howmuch: достаем по payload eventId + snapshotId, получаем цену из howmuch. Записываем цену по snapshotId. В той же транзакции добавляем в очередь таск на отправку события(EventState) через Broker+Kafka
* таск на отправку обновлений по событию(EventState) через брокер. Этот топик будет читать старый биллинг, обиливать по нему события с ценой. Для чатов с застройщиками по нему будем строить статистику по чатам для партнерки

##Consumer
* потребляет пользовательские события, факторы монетизации, price-requests

[Схема emon](https://wiki.yandex-team.ru/users/rmuzhikov/user-event-monetization/.files/event-monetization11.jpeg)

##Схема таблиц
В качестве базы пробуем ydb.
Модель событий, с которыми будем работать https://github.com/YandexClassifieds/schema-registry/pull/4704

```
shard_id = hash(project, event_type, event_id)
CREATE TABLE event
(
shard_id Uint32,
project Utf8,
event_type Utf8,
event_id Utf8,
payer string,
payload string,
create_time Timestamp,
PRIMARY KEY (shard_id, project, event_type, event_id)
);

CREATE TABLE factors_snapshot
(
shard_id Uint32,
project Utf8,
event_type Utf8,
event_id Utf8,
snapshot_id Uint64,
factors string,
factors_snapshot string,
price_kopecks Uint64,
price_rule_id Utf8,
create_time Timestamp,
PRIMARY KEY (shard_id, project, event_type, event_id, snapshot_id)
);

shard_id = hash(task_type, process_time, task_id)
CREATE TABLE task_queue
(
shard_id Uint32,
task_type Uint32,
process_time Timestamp,
task_id Utf8,
payload string,
PRIMARY KEY (shard_id, task_type, process_time, task_id)
);

```

###Приходит новый event:
```
TRANSACTION {
   UPSERT INTO event(,,,) VALUES (,,,) // сохраняем событие
   UPSERT INTO task_queue(shard_id, task_type, process_time, task_id, payload) VALUES (shard_id, send_event_state_id, now, event_id, payload{project + event_type + event_id}) // добавляем таску на отправку события(EventState) через брокер в очередь
}
```

###Приходит новый factor:
```
TRANSACTION {
   SELECT * FROM factors_snapshot WHERE shard_id = ... AND project = ... AND event_type = ... AND event_id = ... order by snapshot_id desc limit 1
   //склеиваем прошлый снэпшот факторов с новым фактором
   UPSERT INTO factors_snapshot(shard_id, project, event_type, event_id, snapshot_id, factors_snapshot) VALUES (shard_id, project, event_type, event_id, snapshot_id + 1, factors, factors_snapshot) //записываем новую версию снэпшота
   UPSERT INTO task_queue(shard_id, task_type, process_time, task_id, payload) VALUES (shard_id, send_event_state_id, now, event_id, payload{project + event_type + event_id + snapshot_id}) //добавляем таску на отправку изменения состояния события
}
```


###Приходит price request:
Запрашиваем цену в howmuch -> price(TODO: обсудить читаем кафку и сразу делаем запрос в howmuch или записывать в очередь таск в базе, и через таск ходить в howmuch(позволит разгребать очередь в кафке даже при частично сломанных запросах))
```
TRANSACTION {
   UPSERT INTO factors_snapshot(shard_id, project, event_type, event_id, snapshot_id, price) VALUES (shard_id, project, event_type, event_id, snapshot_id, price) //добавляем информацию о цене снэпшота
   UPSERT INTO task_queue(shard_id, task_type, process_time, task_id, payload) VALUES (shard_id, send_event_state_id, now, event_id, payload{project + event_type + event_id + snapshot_id}) //таска на отправку события(EventState) потребителям
   
}
```

###Таска на отправку обновлений по событию :
Вычитываем таски из очереди
Вынимаем из payload: project + event_type + event_id + snapshot_id
Джойним по ним factors_snapshot и event
Формируем событие
Посылаем в брокер


[Cхема обиливания чатов](https://wiki.yandex-team.ru/users/rmuzhikov/user-event-monetization/.files/event-monetization8.jpeg)
Для чатов с застройщиками из факторов нужны только результаты проверок в Hobo.

