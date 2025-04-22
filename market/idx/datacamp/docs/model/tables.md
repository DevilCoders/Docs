
В таблицах хранится сериализованный протобаф. Во все таблицы добавлены User attributes со схемой протобафа для получения данных через YQL.

## Таблицы стейта продакшн

- [Базовая](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/united/basic_offers)
- [Сервисная](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/united/service_offers)
- [Складская](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/united/actual_service_offers)
- [Партнерские категории](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/united/categories)
- [msku](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/msku/msku)
- [Акции](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/promo/promo_description)
- [Блог](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/white/blog)
- [Синие бакеты](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/blue/delivery-calc/buckets)
- [Партнеры](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/united/partners)
- [Поисковые](https://yt.yandex-team.ru/markov/navigation?path=//home/market/production/indexer/datacamp/united/search_tables)

## Таблицы стейта тестинг

- [Базовая](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/testing/indexer/datacamp/united/basic_offers)
- [Сервисная](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/testing/indexer/datacamp/united/service_offers)
- [Складская](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/testing/indexer/datacamp/united/actual_service_offers)
- [Партнерские категории](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/testing/indexer/datacamp/united/categories)
- [msku](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/testing/indexer/datacamp/msku/msku)
- [Акции](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/testing/indexer/datacamp/promo/promo_description)
- [Блог](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/testing/indexer/datacamp/white/blog)
- [Синие бакеты](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/testing/indexer/datacamp/blue/delivery-calc/buckets)
- [Партнеры](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/testing/indexer/datacamp/united/partners)
- [Поисковые](https://yt.yandex-team.ru/markov/navigation?path=//home/market/testing/indexer/datacamp/united/search_tables)

## Выгрузки для индексатора { #datacamp-out }

- [Синие Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/united/blue_out)
- [Синие Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/blue_out)
- [Белые Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/united/white_out)
- [Белые Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/white_out)
- [ТГО Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/united/direct_out)
- [ТГО Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/direct_out)
- [Товарные вертикали (синие) Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/united/blue_turbo_out)
- [Товарные вертикали (остальные) Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/united/turbo_out)
- [Товарные вертикали (синие) Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/blue_turbo_out)
- [Товарные вертикали (остальные) Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/turbo_out)

## Бекапы

- [Бекапы Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/united/backups)
- [Бекапы Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/backups)

## Поисковые таблицы
Поисковые таблицы - динамические таблицы, которые можно считать некоторым представлением основных офферных таблиц. Так же, как и основных таблиц, поисковых таблиц три: базовая, сервисная и складская. Ключи в соответствующих таблицах совпадают, за исключением их порядка, так как поисковые таблицы в первую очередь предназначены для операций в пределах одного бизнеса/магазина/склада и являются optimize for scan (также из сервисной поисковой таблицы убраны лишние ключи warehouse_id и outlet_id). Реплики поисковых таблиц представлены на двух кластерах - seneca-sas и seneca-vla.

В основном, колонки поисковых таблиц имеют простейшие типы и хранят значения полей оффера. Такой способ хранения позволяет выполнять запросы с фильтрами по этим полям на стороне YT. В таблицах для упрощения не предусмотрено хранение значения null: если в протобафе оффера значение не заполнено, в таблицу сохраняется дефолтное значение соответствующего типа.

Запись в поисковые таблицы происходит в той же транзакции, что и запись в основные таблицы, таким образом гарантируется консистентность данных и отсутствие гонок. В поисковых таблицах не хранится meta данных. Чтения поисковых таблиц в транзакции не происходит. Реализовано три режима записи в поисковые таблицы: DISABLED, WRITE_ON_CHANGE, WRITE_FORCE. 
В режиме DISABLED запись в таблицы не происходит (не включать, ломает консистентность). WRITE_ON_CHANGE - основной режим, записываем в таблицу, если приходит апдейт для поля оффера, присутствующего в таблице (таблицы "подписаны" на поля оффера через разметку протобафа).
WRITE_FORCE - режим форсированной записи, используется для наливки данных в таблицы (например, если вы добавляете новую колонку в таблицу и запускаете полный перемайнинг, чтобы наполнить колонку значениями).

Удаление офферов из поисковых таблиц происходит одновременно с удалением из основных в клинере рутин.

Поисковые таблицы легковесны (по сравнению с основными таблицами) и хорошо подходят для сканирующих или mr-операций, в которых не требуется много знаний об оффере.

Полезные ссылки:
- [Корневой тикет](https://st.yandex-team.ru/MARKETINDEXER-41660)
- [Основной код](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/utils/yt_storage/yt_search_offers_storage.cpp)
- [Разметка протобафа](https://a.yandex-team.ru/search?search=search_tables,%5Emarket%2Fidx%2Fdatacamp%2Fproto%2Foffer%2F.*,jhC,arcadia,,200&repo=arc)
- [Обновление схемы](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/recreate_replicated_tables)
- [Пример наливки данных](https://st.yandex-team.ru/MARKETINDEXER-43496)

## Поставка в аналитику Маркета

- [Фильтрованная Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/export/filtered)
- [Фильтрованная Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/export/filtered)

## ECOM выгрузка

- [Офферы Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/ecom/export/offers/merged)
- [Офферы Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/ecom/export/offers/merged)
- [Партнеры Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/ecom/export/clients)
- [Партнеры Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/ecom/export/clients)
- [Фиды Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mbi/dictionaries/datacamp_feed/latest)
- [Фиды Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/mbi/dictionaries/datacamp_feed/latest)

- Колонка Data - [обертка](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/ExportMessage.proto?rev=r8592849#L9) над [внешним форматом оффера](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/external/Offer.proto?rev=r8592849#L21)
- Колонка Service - [описание класса оффера](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/external/Offer.proto#L329) для быстрой фильтрации
- Содержат все классы офферов: маркет, директ, еда, лавка, вертикали и т.д.
- Содержат офферы, скрытые по качеству и другим причинам. Потребитель может отфильтровать по [флагам скрытий](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/external/Offer.proto?rev=r8797567#L106)

