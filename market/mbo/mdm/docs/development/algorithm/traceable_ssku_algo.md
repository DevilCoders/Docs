# Алгоритм расчета золотой прослеживаемости SSKU

За расчет золотой [прослеживаемости](../../contour/parameter/traceable.md) SSKU отвечает [TraceableSskuGoldenItemService](https://a.yandex-team.ru/arc_vcs/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/masterdata/services/ssku/TraceableSskuGoldenItemService.java), являющийся типичным представителем [MdmGoldenItemService](https://a.yandex-team.ru/arc_vcs/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/masterdata/services/iris/MdmGoldenItemServiceImpl.java) (вычисление золота по блокам). Результатом его работы является CommonSsku с единственным параметром - [прослеживаемостью](../../contour/parameter/traceable.md).


## Сплиттер серебра на блоки

[TraceableSskuSilverSplitter](https://a.yandex-team.ru/arc_vcs/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/masterdata/services/ssku/TraceableSskuSilverSplitter.java)

Принимаемые silver item:
- MasterDataSilverItem
- SilverServiceSsku
- CommonMsku

Особенности:
- создаются только Traceable блоки (тип MDM_PARAM, подтип 403)
- значения параметров CommonMsku должны иметь тип источника MSKU_INHERIT, иначе IllegalArgumentException

## Сплиттер золота на блоки

Отсутствует, поэтому этот сервис пока нельзя использовать для обогащения существующей золотой CommonSsku

## Препроцессор серебряных блоков

Отсутствует.

## Выбор лучшего блока (handle)

Используется стандартная логика по приоритетам источников. Плюс есть дополнительная фильтрация на Traceable блоки (тип MDM_PARAM, подтип 403).

{% cut "Подробнее про логику по приоритетам" %}

Выбираются блоки с наивысшим приоритетом, а среди них с самым поздним updated_ts. Приоритеты источников определены в [MasterDataSourceType](https://a.yandex-team.ru/arc_vcs/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/masterdata/model/golden/MasterDataSourceType.java) (чем меньше defaultPriority, тем больше приоритет).
Именно они используются в этом алгоритме, с учетом апгрейда источника SUPPLIER до WAREHOUSE для всех данных, полученных после [23.10.2020](https://st.yandex-team.ru/MBO-27725).

{% endcut %}

## Постпроцессор блоков

Отсутствует.

## Постпроцессор CommonSsku

Отсутствует.
