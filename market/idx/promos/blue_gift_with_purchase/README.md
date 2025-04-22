Робот-парсер описания синих акций в виде XLS файлов
https://st.yandex-team.ru/BMP-841


Запускается каждые 10 минут как задача sandbox - https://a.yandex-team.ru/arc_vcs/sandbox/projects/market/idx/BluePromoGwpXlsParser

Собирает задачи из STARTREK-а по заданному фильтру (для акций есть отдельная очередь), из запущенных или готовых к запуску задач загружает самый свежий XLS файл по маске robot_ специального формата (https://st.yandex-team.ru/MARKETINDEXER-29070).
Также загружает информацию SHOPSDAT из YT-таблицы, для работы с feed/склад/магазин (https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/stratocaster/in/shopsdat).

По содержимому файла формирует описание акции в виде протобуфа (https://a.yandex-team.ru/arc/trunk/arcadia/market/proto/feedparser/Promo.proto?rev=r9247935#L53), заполняется как описание ("шапка") акции, так и её товарный состав (в виде списка пар feed_id+offer_id, для некоторых промо-механик в виде набора правил OffersMatchingRules). Собранные протобуфки сохраняет в статические таблицы YT (на 2 кластер arnold и hahn).

Ввиду невозможности отслеживания фактов удаления акции или изменения параметров акции, реализована концепция полного обновления с "вращением" таблиц, при этом сслыка recent всегда указывает на актуальную таблицу.
