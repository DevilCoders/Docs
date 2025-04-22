# CDP-SEGMENTS-EVALUATOR
Сервис, расчитывающий идентификаторы пользователей попавшие в сегмент CDP.
Описание CDP можно прочитать тут - https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/README.md.

## Описание
`cdp-segments-evaluator` - процессинговый сервис, расчитывающий идентификаторы пользователей (`UserID`) попавшие в сегмент CDP.
Для понимания работы `cdp-segments-evaluator` важно понимать как работает очередь обработки сегментов. Её описание
можно прочитать [на WIKI тут](https://wiki.yandex-team.ru/users/lavrinovich/cdp-remarketing-in-pictures/). Также можно
ознакомится с реализацией этой очереди [в коде класса SegmentsProcessingQueueYdb](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-processing-common/src/java/ru/yandex/metrika/cdp/processing/ydb/SegmentsProcessingQueueYdb.java).

### Deployment
production - https://deploy.yandex-team.ru/stages/cdp-segments-evaluator-production

testing - https://deploy.yandex-team.ru/stages/cdp-segments-evaluator-test

### Что делает?
Сам по себе сервис - `BusyWorker`([интерфейс тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-processing-common/src/java/ru/yandex/metrika/cdp/processing/worker/BusyWorker.java)).
По сути в бесконечном цикле выполняет некоторую работу. Если быть более точным, то тут используется `ParallelBusyWorker` -
реализация интерфейса `BusyWorker`, позволяющая выполнять некоторый заранее определённый `Runnable` в бесконечном цикле
параллельно в несколько потоков ([код тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-processing-common/src/java/ru/yandex/metrika/cdp/processing/worker/ParallelBusyWorker.java)).
Назовём одно исполнение заданного `Runnable` "тактом" работы сервиса.

Один "такт" работы `cdp-segments-evaluator` выглядит следующим образом:
1. Достаём из очереди сегментов в YDB (`segments_queue/segments_queue`) очередной идентификатор сегмента (`segmnent_id`) для расчёта идентификаторов.
У этого сегмента в очереди будет `stage = AWAITING_EVALUATION`. Детальная схема доставания элемента из очереди для расчёта идентификаторов описана
[вот тут на WIKI](https://wiki.yandex-team.ru/users/lavrinovich/cdp-remarketing-in-pictures/# raschjotsegmenta)
2. Достаём из таблички сегментов в YDB (`segments_data/segments`) описание сегмента по его идентификатору.
3. Сохраняем метаинформацию о текущем вычисление snapshot-а в таблицу `segments_data/evaluation_meta` в YDB.
4. Вычисляем в ClickHouse (через `mtgiga`) идентификаторы (`UserID`) попавшие в сегмент.
5. Записываем в ClickHouse (в `mtcdp`) snapshot набора идентификаторов попавших в сегмент.

#### Поточность
По факту пункты 4 и 5, а именно чтение и запись происходят не последовательно, а одновременно. То есть берётся итератор
прочитанных идентификаторов(`UserID`), вычитывается очередная пачка идентификаторов из одного кластера (`mtgiga`) и она
сразу записывается в другой кластер (`mtcdp`). Это позволяет потреблять O(1) памяти вне зависимости от размера сегмента.

## Графики
Графиков пока нет, будут добавлены после [CDP-582](https://st.yandex-team.ru/CDP-582)
