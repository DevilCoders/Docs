**Complete Commands Routine**
--

Новый механизм скрытия офферов не найденных в комплит фиде.

**Краткий тезаурус**
- *комплит фид* - документ содержащий полный список товарных позиций для магазина.
- *комплит команда* - специальные сообщения посылаемые qparser-ом после парсинга комплит фида. Суть - задание на поиск и скрытие скрытие офферов не найденных в комплит фиде. Команда описывается прото структурой **Market.DataCamp.CompleteFeedCommandParams**. После парсинга одного фида обычно посылается несколько пакетов (~1k для больших фидов). Это нужно чтобы размер сообщений не был слишком большим (комплит команды содержат полный список оффер id фида).
- *очередь комплит команд* - упорядоченная реплицированная таблица YT используемая как очередь (аналог Logbroker)


-----

Bird view
--

![Bird view](CompleteCommands.png "Architecture")


- qparser парсит фид и если фид помечен как complete то записывает комплит команды в *очередь комплит команд*
- Рутины обрабатывают комплит команды
    - Выгружают из очереди новые комплит команды
    - С помощью map-reduce обрабатывают операции, формируя таблицу со скрытиями для офферов
    - Выходные таблицы перемещаются в специальную папку из которой читает сканнер
- Сканнер читает новые таблицы из специальной директории с таблицами комплит команд. Прочитанные таблицы сканнер помечает специальными атрибутами.
- При следующем запуске рутины смотрят на список таблиц в директории сканнера, удаляют старые таблицы, отправляют статистику времени чтении таблиц сканнером.


------

Очередь комплит комманд
--
Представляет собой упорядоченную реплицированную таблицу. [Прод](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/united/routines/CompleteCommands/commands_queue), [Тетсинг](https://yt.yandex-team.ru/pythia/navigation?offsetMode=key&path=//home/market/testing/indexer/datacamp/united/routines/CompleteCommands/commands_queue)

Что важно:
* Запись идет через meta cluster Markov (тестинг Pythia)
* Таблица имеет две асинхронные реплики в arnold и hahn
* Выставлен [dynamic_store_auto_flush_period](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&navmode=user_attributes&path=//home/market/production/indexer/datacamp/united/routines/CompleteCommands/commands_queue) в минуту, чтобы данные быстрее доезжали до асинхронных реплик
* MapReduce у таблиц сейчас выключен enable_dynamic_read
* Данные в таблице автоматически ротируются  ["max_data_ttl": 604800000](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&navmode=user_attributes&path=//home/market/production/indexer/datacamp/united/routines/CompleteCommands/commands_queue)
* Таблицы реплики кушают довольно много чанков, сейчас в проде 10 таблетов, максимальное кол-во чанков на таблет 10k, если ротация не будет успевать за новыми данными то таблеты достигнут лимита по чанкам и репликация остановится.
* Offset очереди
    * накатанный сканнером -- хранится на meta cluster [scannedPosition](https://yt.yandex-team.ru/markov/navigation?navmode=user_attributes&path=//home/market/production/indexer/datacamp/united/routines/CompleteCommands/lock)
    * позиция **queue_position** обработанная map reduce-ом -- выставляется на [выходных](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/routines/CompleteCommands/mr/outputs) таблицах поставляемых сканнеру
    * при последующем запуске внутри одного ДЦ используется позиция на выходных таблицах, при переключении между кластерами используется некоторая окрестность  **scannedPosition**
* Offset очереди читает и меняет только рутина CompleteComands

**TODO monitoring alerts:*
- replication lag
- chunks count

------------------

Рутина CompleteCommands
--
Написана на C++. Исходники [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/tasks/complete_commands)


Расширенное описание последовательности действий:
- Рутина запускается каждые 2 минут на каждом инстансе DataCamp Routines
- Рутина захватывает [глобальный лок](https://yt.yandex-team.ru/markov/navigation?navmode=locks&path=//home/market/production/indexer/datacamp/united/routines/CompleteCommands/lock) через meta cluster, т.е. нет паралельно работающих инстансов
- Выбирает доступный вычислительный кластер Arnold (по умолчанию) или Hahn
- Вычисляет **offset** очереди как максимум **scannedPosition**  и атрибута **queue_position** непрочитанных сканнером таблиц.
- Выгружает данные из очереди комплит команд используя **offset** описанный выше.
    - Выгрузка делается через операцию merge чтобы данные не покидали вычислительный кластер
    - В результате формируется [статическая таблица](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/routines/CompleteCommands/mr/input)


 - Таблица с необработанными командами join-интся с сервисной таблицей datacamp с помощью [MapReduce операции](https://yt.yandex-team.ru/arnold/operations?filter=TDisableOffersAbsentFromCompleteFeed)
    - В результате получается таблица с сервисными офферами со скрытиями
    - На выходную таблицу запускается дополнительная [операция](https://yt.yandex-team.ru/arnold/operations?filter=TGroupRegionalCloneOffers) для групировки региональных клонов
- Выходная таблица помечается специальными аттрибутами и перемещается в [папку](https://yt.yandex-team.ru/arnold/navigation?sort=asc-false,field-name&path=//home/market/production/indexer/datacamp/united/routines/CompleteCommands/mr/outputs) для чтения сканнером.
    - Атрибуты которые ставит рутина: queue_position, max_offer_ts,  min_offer_ts
- Рутина чистит старые выходные таблицы (старше 7 дней)
- Рутина отправляет разнообразную статистику по MR операциям, latency обработки команд, и чтении сканера

**Дедупликация очереди сканера**
- Если кол-во непрочитанных таблиц сканнера растет, то рутина мержит все выходные непрочитанные таблицы в одну, дедуплицируя офферы для скрытий. Это делается через отдельную MapReduce операцию.
- Это позволяет схлопнуть очередь если сканнер не работал продолжительное время, при этом данные не теряются.

-----
Сканнер
--
- Используется новый режим чтения - папка с таблицами
- Таблицы читаются последовательно, в FIFO
- После чтения таблица помечается атрибутами
    - scanner_processed_ts, market_reader_processed_content_revision.
- Умеет читать шардированно
- Папки в разных ДЦ независимы и читаются параллельно, но они обычно не пересекаются по данным
    - MapReduce джоба запускается только на одном ДЦ, следовательно выходная таблица появляется только на одном ДЦ.

--------

Графики
--
Графики [тут](https://nda.ya.ru/t/3EO11xe24KnkWs)

Панели
* Max Processing latency from last hour
    * *last_1h_total_max_lag_seconds* - время от начала парсинга комплит фида до завершения чтения выходной таблицы сканнером (максимум за последний час) <-- **основная метрика**
        - меньше часа условно ок
        - больше часа - что-то не так.
        - несколько часов -- что-то сломалось
    * *last_1h_scanner_max_lag_seconds* - время от начала обработки комплит команды (запуск MR) до накатки выходной таблицы сканнером (максимум за последний час)
* Command Processing latencies - много сенсоров с задержками
    * total_unprocessed_max_lag_seconds - возраст ненакатанных сканнером данных. Если растет, сканнер тормозит или не работает. <-- **важная метрика**
    * scanner_unscanned_max_lag_seconds - на эту метрику лучше не смотреть.
    * Остальные лучше смотреть по коду, редко будут нужны если не разбираться в тонких проблемах.
* Pipeline Running Time
    * pipeline_running_time_seconds время работы рутины
    * reducer_running_time_seconds время работы MR операций
    * Рутины запускают синхронно MR опеарции, поэтому время работы рутины чуть больше чем операции.
* Pipeline time between run - время между удачными запусками рутины
* Scanner total tables count - кол-во выходных таблиц для сканнера, старые удаляются рутинами.
* Scanner unscanned tables count
    - scanner_unscanned_tables_count - кол-во непрочитанных таблиц сканнером
        - 1-2 - норм
    - **merged_output_table_count** - если больше 0, то сработал механизм дедупликации очереди сканнера. Сканнер тормозит или не работает.

-------------
Troubleshooting
--

- Нет новых данных на графиках
    - Если новых данных нет пол часа то причина может быть:
    - не работают рутины: падают или не запускаются
        - грепаем логи *todo: добавить команду sky portorun*
        - смотрим кто держит [лок](https://yt.yandex-team.ru/markov/navigation?navmode=locks&path=//home/market/production/indexer/datacamp/united/routines/CompleteCommands/lock), заходим на инстанс, смотрим логи там
    - не работает репликация
        - нет комплит команд -- нет работы
        - проверяем [метатаблицу](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/united/routines/CompleteCommands/commands_queue). Лаг на репликацию должен быть близок к 0.
    - qparser не пишет в очередь - падает или еще что.
- Растет last_1h_total_max_lag_seconds, смотрим на графиках latency куда уходит время, скорее всего сканнер медленно читает, или долго не работал.
- Растет total_unprocessed_max_lag_seconds - сейчас не работает или тормозит сканнер.

-------
Рецепты
--
- Выключить новый механизм (переключиться на старый)
    - В [ITS qparser](https://nanny.yandex-team.ru/ui/#/its/locations/market/datacamp/parser-white/) выставить `"mr_complete_commands_enable_for_all": false` в секции `values.feature`
    - qparser перестанет писать комплит команды в очередь YT, вместо этого будет посылать их на обработку в Piper
- Переключить обработку комплит команд на другой ДЦ
    - в ITS [routines](https://nanny.yandex-team.ru/ui/#/its/locations/market/datacamp/routines/) делаем находим секцию 'values.complete_commands' и меням primary_mr_proxy и reserve_mr_proxy
    - пример:
        ```
        "values": {
            "complete_commands": {
                "primary_mr_proxy": "hahn",
                "reserve_mr_proxy" : "arnold"
            }
        }
        ```
- Создание/шардирование динтаблиц таблиц
    - некоторые команды и важные аттрибуты описаны в [create_tables.txt](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/tasks/complete_commands/create_tables.txt)


------

**TODO monitoring alerts:**
----
На [дэшбоард комплит команд](https://nda.ya.ru/t/3EO11xe24KnkWs) вынесены следующие мониторинги
- Общий лаг обработки комплит комманд
- Лаг накатики выходних таблиц сканнером
- Максимальное кол-во выходных таблиц в папке для сканнера

----------
TODO:
--

- Учитвать лаг реплики при выборе активного ДЦ
- Использовать external reduce реплику сервисной таблицы сортированную по `business_id, shop_id` - уменьшит общий лаг обработки

- Починить залипание сканнера LBOPS-6642

