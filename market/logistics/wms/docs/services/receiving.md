# Приёмка

## Приоритизация поставок

### Вычисление приоритета

Приоритет поставок отображается на странице "Поставки с приоритетом" (7, 1, 2
/ui/admin/receivingPriorityReceipts/priorityReceipts).

Приоритет рассчитывается для поставок 1, 3 типов с учётом критериев:

- FIFO (прошедшее время после приёмки по тарным местам)
- OOS (out of stock, необходимое количество товара на стоке с учетом GMV)
- Объём поставки (количество товара в поставке с учетом производительности склада)
- Временной интервал для попадания в SLA (0..9, 9..18 и 18..*)
- Специальное повышение приоритета поставки (ручная приоритизация).

Пересчет приоритета выполняется фоновым процессом.

Приоритеты поставок хранятся в таблице `RECEIPTS_TO_PRIORITIES`.

### Запрос паллет к столу приемки

Исходя из приоритета паллеты запрашиваются к столу приемки.
В любой момент приёмки можно нажать кнопку "Запросить паллету".
При запросе происходит бронирование паллет и создание заданий на перемещение.

Возможные ошибки при запросе паллет:

| Код                     |                                    Описание                                     |                                                                                                                                                                                                                          Действия для исправления |
|:------------------------|:-------------------------------------------------------------------------------:|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| NO_AVAILABLE_CONTAINERS |                        Нет доступных паллет/контейнеров.                        |                                                                                                                                                                                       Разместить паллеты в буфере приемки (зона с типом INB_BUF). |
| ACTIVE_BOOKINGS_LIMIT   | Достигнут лимит ({limit}) на запросы паллет. Активные запросы: {activeBookings} | Надо переместить тару к столу приемки по заданию. Если задания нет, то можно переместить без задания и начать приёмку паллеты на столе. Если ничего не помогает, то можно поменять статус бронирования на 2 в таблице INBOUND_CONTAINER_BOOKINGS. |
| WRONG_TARGET_LOCATION   |    Недоступное место назначения: {location}. Обратитесь к поддержке системы.    |                                                          Маршрут между ячейкой отправки и ячейкой назначения не найден. Проверить доступные маршруты можно запросом [1](#find-route). Надо скорректировать настройки топологии или транспортеров. |
| WRONG_SOURCE_LOCATION   |     Недоступное место отправки: {location}. Обратитесь к поддержке системы.     |                                                          Маршрут между ячейкой отправки и ячейкой назначения не найден. Проверить доступные маршруты можно запросом [1](#find-route). Надо скорректировать настройки топологии или транспортеров. |

### Фоновые процессы

#### CalculateReceiptPriorityJob

Периодичность запуска: 5 минут.

Производит расчет приоритета, вызывает inbound-management API.

#### ReceivingPalletBufferJob

Периодичность запуска: 2 минуты.

Следит за актуальными запросами паллет и состоянием задач на транспортировку.
Если задание в статусе CANCELED, отменяет бронирование паллеты и запрашивает к столу еще паллету.
Если задание в статусе FAILED, снимает со стола бронирование паллеты, чтобы другой стол смог запросить ее.

### Мониторинг

История расчетов приоритета: [ReceiptPriorityCalculation](https://datalens.yandex-team.ru/c2g5xwd2a09g4-receiptprioritycalculation).

Приоритет поставок, из которых принимают паллеты: [Приоритет поставок](https://datalens.yandex-team.ru/l979n04bbnsad-prioritet-postavok).

### Конфигурация

| Ключ                            | Значение по-умолчанию |                                                                                                                                                    Описание |
|:--------------------------------|:---------------------:|------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| INBOUND_WAREHOUSE_PERFORMANCE   |          200          |                                                                                                      Производительность склада для расчета объёма поставок. |
| INBOUND_PRIORITY_LAST_DAYS      |          100          |                                                                                 Приоритет рассчитывается для поставок, созданных за последние {value} дней. |
| INBOUND_MAX_CONTAINER_BOOKINGS  |           1           |                                                                                                               Число активных запросов паллет у одного стола |
| INBOUND_MIN_TIME_INTERVAL_HOURS |           9           |                                                               Поставкам с sla меньше указанного значения присваивается мин коэффициент временного интервала |
| INBOUND_MAX_TIME_INTERVAL_HOURS |          18           | Поставкам с sla больше значения INBOUND_MIN_TIME_INTERVAL_HOURS и меньше или равным указанного значения присваивается макс коэффициент временного интервала |

# Примечания

## [1] Поиск маршрута между зонами {#find-route}
```
select
  loc_source.LOC               srcLoc
, loc_source.LOCATIONTYPE      srcLocType
, loc_source.PUTAWAYZONE       srcZone
, loc_source.ADDWHO            srcAddwho
, loc_source.EDITWHO           srcEditwho
, loc_source.LOSEID            srcLoseId
, loc_source.LOGICALLOCATION   srcLogicalLocation
, l_dest.LOC                   destLoc
, l_dest.LOCATIONTYPE          destLocType
, l_dest.PUTAWAYZONE           destZone
, l_dest.ADDWHO                destAddwho
, l_dest.EDITWHO               destEditwho
, l_dest.LOSEID                destLoseId
, l_dest.LOGICALLOCATION       destLogicalLocation
, tr.TRANSPORTERID             transporterId
, tr.PUTAWAYZONE               trZone
, tr.ENABLED                   trEnabled
, tr.ADDWHO                    trAddwho
, tr.EDITWHO                   trEditwho
, tr.automation                trAutomation
from wmwhse1.LOC loc_source
join wmwhse1.LOC l_tin on loc_source.TRANSPORTERLOC = l_tin.LOC and l_tin.LOCATIONTYPE = 'T_IN_BUF'
join wmwhse1.TRANSPORTER tr on l_tin.PUTAWAYZONE = tr.PUTAWAYZONE
join wmwhse1.LOC l_tout on l_tout.PUTAWAYZONE = tr.PUTAWAYZONE and l_tout.LOCATIONTYPE = 'T_OUT_BUF'
join wmwhse1.LOC l_dest on l_dest.TRANSPORTERLOC = l_tout.LOC
where tr.ENABLED = 1
and loc_source.PUTAWAYZONE = 'IN_BUF_B'
and l_dest.PUTAWAYZONE in ('IN_CONV_A', 'IN_CONV_B', 'IN_CONV_C', 'IN_CONV_D')
```
