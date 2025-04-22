Тарификация
===========

Описание тарифов
----------------
Описание формата и процесс их изменения можно найти [здесь][tariff].


Обработка отсутствующих тарифов
-------------------------------
Непосредственно перед расчётом отчёта, но после вычисления всех логов работ и
словарей [проверяется наличие тарифов][find absent tariffs] необходимых для
расчёта заработной платы. Если каких либо тарифов не хватает, то отчёт не
рассчитывается, а создаётся задача в очереди [CPM][] на заведение этих
тарифов. При закрытии задачи срабатывает [триггер][tracker trigger] который
создаёт новую версию артефакта [_Issue Id_][issue id artifact]. Этот артефакт
содержит номер закрытой задачи. Появление новой версии этого артефакта вызывает
запуск реакции [_Issue Id -> Date_][issue id -> date] которая извлекает из
закрытой задачи дату для которой не удалось рассчитать отчёт. Для этой даты
создаётся новая версия артефакта [_Date_][date artifact], что в свою очередь
запускает расчёт отчёта Tasks Payment.

Схематически данный процесс выглядит следующим образом:

![Overview](_images/absent-tariffs.svg)


[cpm]:                 https://st.yandex-team.ru/CPM
[date artifact]:       https://beta.nirvana.yandex-team.ru/browse?selected=9725504
[find absent tariffs]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/find_absent_tariffs
[issue id -> date]:    https://beta.nirvana.yandex-team.ru/browse?selected=9725635
[issue id artifact]:   https://beta.nirvana.yandex-team.ru/browse?selected=9725511
[tariff]:              https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/dictionaries/tariff
[tracker trigger]:     https://st.yandex-team.ru/admin/queue/CPM/triggers/30335
