# data_processing

## Таблицы

* **labels** – сортированная динтаблица с ключом **label**. Хранит всю историю лэйблов
* **processed_snapshots** – сортированная динтаблица с ключом **partner_name**+**partner_order_id** и значениями
**hash**, **updated_at**. Хранит последний обработанный снэпшот для каждого заказа. Такая схема нужна для корректной
обработки "мигающих" заказов
* **snapshots** – сортированная динтаблица с ключом **partner_name**+**order_id**+**updated_at**. Хранит всю историю
заказов
* **order_queue** – упорядоченная динтаблица. Очередь заказов на обработку
* **order_queue_slow** – упорядоченная динтаблица. Фоновая очередь заказов на обработку. Обрабатывается после того, как
закончились заказы в **order_queue**
* **order_purgatory** – сортированная динтаблица с ключом **label**+**partner_name**+**partner_order_id** и значением
**updated_at**. Хранит заказы с "отстающими" лэйблами
* **orders_internal** – сортированная динтаблица с ключом **partner_name**+**order_id**. Хранит текущее состояние
заказов
* **orders** – статическая таблица. Экспорт из **orders_internal** для аналитики

[Формат таблиц](https://a.yandex-team.ru/arc_vcs/travel/cpa/tools3/tables_config.yaml)

## Обработка лэйблов:

* Читаем лэйблы из LB. Если лэйбл уже есть в таблице **labels**, ничего больше не делаем
* Конвертируем лэйблы для авиа из JSON в protobuf. Для *Отелей* и *ЖД* оставляем protobuf, который получили на входе
* Проверяем, есть ли полученные лэйблы в таблице **order_purgatory**. Если есть, обновляем данными лэйбла
соответствующие заказы (при условии, что они есть в таблице **orders_internal**). Удаляем лэйблы из **order_purgatory**
* Обработанные лэйблы записываем в таблицу **labels**
* Коммитим изменения в LB

Формат лэйблов:
* [Авиа](https://a.yandex-team.ru/arc_vcs/travel/proto/avia/cpa/label.proto)
* [Отели](https://a.yandex-team.ru/arc_vcs/travel/hotels/proto2/label.proto)
* [ЖД](https://a.yandex-team.ru/arc_vcs/travel/proto/trains/label_params.proto)

Обработка выполняется в [LabelProcessor.java](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_processing/flow/src/main/java/ru/yandex/travel/cpa/data_processing/flow/processors/LabelProcessor.java)

## Обработка снэпшотов:

* Читаем снэпшоты из LB. Сравниваем с содержимым таблицы **processed_snapshots**. Снэпшот нужно обработать (добавляем в
`snapshots_to_process`), если:
    * снэпшота нет в **processed_snapshots**
    * хэш не совпадает
    * `updated_at` снэпшота < `updated_at` в **processed_snapshots**
* Для всех `snapshots_to_process` получаем историю заказов `existing_snapshots` из таблицы **snapshots** по ключу заказа
(**partner_name**+**partner_order_id**)
* Получаем снэпшоты для дедупликации `snapshots_to_deduplicate = existing_snapshots + snapshots_to_process`
* Дедуплицируем локально, получаем `deduplicated_snapshots`: Упорядочиваем `snapshots_to_deduplicate` по `updated_at` и
удаляем идущие подряд дубли по хэшу
* Получаем новые снэпшоты `new_snapshots = deduplicated_snapshots - existing_snapshots`
* Новые снэпшоты `new_snapshots` добавляем в таблицу **snapshots**
* Ключи новых/изменённых заказов пишем в **order_queue**
* Добавляем `snapshots_to_process` в таблицу **processed_snapshots**
* Коммитим изменения в LB

Обработка выполняется в [SnapshotProcessor.java](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_processing/flow/src/main/java/ru/yandex/travel/cpa/data_processing/flow/processors/SnapshotProcessor.java)

## Обработка заказов:

Прцесс запускается периодически и обрабатывает заказы в течение ограниченного настройками времени. Сначала
обрабатывается **order_queue**, затем **order_queue_slow**. Таким образом, обработка заказов из **order_queue_slow**
выполняется с более низким приоритетом. Обарботка пачки закаов выполняется так:

* Читаем ключи новых/изменённых заказов из **order_queue**/**order_queue_slow**
* Получаем все снэпшоты заказов из таблицы **snapshots**
* Для всех полученных снэпшотов, выполняем формирование заказа
* Дополняем заказ данными лэйбла из таблицы **labels**. Если лэйбла ещё нет – добавляем запись в таблицу
**order_purgatory**
* Полученные заказы добавляем в таблицу **orders_internal**
* Делаем трим обработанных заказов в **order_queue**/**order_queue_slow**

По окончании обработки заказов переливаем данные из **orders_internal** в **orders**

Основные функции обработки заказов:
* объединение снэпшотов в заказ
* проверка заказа по его истории изменений
* конвертирование валют и расчёт комиссии
* добавление к заказу информации из лэйбла

Вся partner specific логика по возможности должна находиться здесь

Обработка выполняется в [update_orders_incremental](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_processing/update_orders_incremental)

Для того, чтобы `update_orders_incremental` обрабатывал заказы нового партнёра, нужно написать класс-обработчик для
этого партнёра в [data_processing/lib/order_processor.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/data_processing/lib/order_processor.py)
и добавить его в `PROCESSORS`. Если нет partner specific логики – достаточно только переопределить `PARTNER_NAME`

Тестовые данные для `update_orders` находятся в [tests/lib/data/update_orders](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/tests/lib/data/update_orders).
Сюда нужно добавить тестовые данные для нового партнёра

### Добавление полей в заказ

Основные поля заказа описываются в [order_data_model](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_processing/lib/order_data_model.py).
Они вычисляются при объединении снэпшотов. Удаление полей (включая поля лэйблов) не поддерживается. Удалённое из
описания поле сохраниится в таблице заказов

### Удаление заказов

!!! Удаление заказов – опасная операция. Нормальная работа CPA не требует удаления заказов. Единственная причина удалять
заказы – были загружены заказы с некорректными ключами. В тестинге можно удалить самостоятельно. Для удаления в проде
обратитесь в канал [#cpa-support](https://yndx-travel.slack.com/archives/CDWRFEE4S)

Информация о заказах содержится в таблице снэпшотов и таблице заказов. Удалять строки из каждой таблицы нужно отдельно.
Чтобы удалить снэпшоты/заказы, нужно записать в соответствующую таблицу ключи заказов, которые требуется удалить:
* снэпшоты `//home/travel/testing/cpa_flow/inbox/snapshots_to_delete`, ключ (**partner_name**+**partner_order_id**+**updated_at**)
* заказы `//home/travel/testing/cpa_flow/{avia, buses, hotels, train}/inbox/orders_to_delete`, ключ (**partner_name**+**partner_order_id**)

После удаления строк также будет удалена соответствующая таблица с ключами

Пример того, как подготовить таблицы с ключами с помощью YQL:

```SQL
INSERT INTO `home/travel/testing/cpa_flow/inbox/snapshots_to_delete` WITH TRUNCATE
SELECT
    partner_name,
    partner_order_id,
    updated_at,
FROM `home/travel/testing/cpa_flow/snapshots`
WHERE partner_name == "booking";

INSERT INTO `home/travel/testing/cpa_flow/hotels/inbox/orders_to_delete` WITH TRUNCATE
SELECT
    partner_name,
    partner_order_id,
FROM `home/travel/testing/cpa_flow/hotels/orders_internal`
WHERE partner_name == "booking";
```

## Повторная обработка заказов

Для некоторых партнёров (*booking*, *hotelscombined*) при обработке части заказов необходимо использовать актуальный
курс валюты. Для таких заказов не достаточно пересчитывать их только при обновлении данных от партнёра. Повторную
обработку инициализирует отдельный процесс, который раз в день получает заказы, которые нужно обновить, и записывает их
в **order_queue_slow**

Обработка выполняется в [rebuild_orders](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_processing/rebuild_orders)

## Общая информация

* На Hahn & Arnold работают независимые копии приложения
* На каждом этапе чтение данных для обработки из LB выполняется пачками. Обработка пачки фиксируется
подтверждением чтения. Ошибки недоступности инфраструктуры "лечатся" ретраями. Повторная обработка пачки данных при этом
допустима. Ошибки данных приводят к падению процесса

