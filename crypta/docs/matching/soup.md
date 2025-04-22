# Описание
**СУП** (**С**истема **У**нифицированных **П**ар) - это хранилище сведений о связях идентификаторов.

Каждая запись супа - это факт связки двух идентификаторов: наличие записи означает, что в логах эти два иденификатора были замечены вместе (например, yandexuid и логин пользователя в одной записи в watch-log).
Основной объем связок собирается [с середины 2017 года](https://yql.yandex-team.ru/Operations/XR3MBJ3udptIK7LxdauzNPK9FevRbbegJGTRjek91r8=).

**Важно**: это только прямые связки. Например, наличие логина в приложении (связка puid-uuid) не означает автоматически наличие логина на устройстве (puid-mm\_device\_id). Для получения в этом случае логинов на устройстве нужно приджойнить факты логинов в приложениях (puid-uuid) к фактам наличия установок приложений на устройствах (uuid-mm\_device\_id).

Формат записи:

1. id1Type - тип первого идентификатора связки
2. id2Type - тип второго идентификатора связки
3. sourceType - "процесс", который приводит к появлению связок (полный список [тут](soup_sources.md))
4. logSource - лог, откуда берутся данные связки
5. id1 - значение первого идентификатора
6. id2 - значение второго идентификатора
7. dates - даты активности связки (== даты, за которые эта связка была замечена в логах)

Четвёрка (id1Type, id2Type, sourceType, logSource) называется **типом ребра**.
Каждому типу ребра соответствует таблица, хранящая все записи для этого типа ребра (//home/crypta/public/matching/by\_id/__[id1Type]__/soup/__[id2Type]__/__[sourceType]__\___[logSource]__)

Для доступа к таблицам нужно [запросить правильную роль в IDM](https://wiki.yandex-team.ru/users/lida-l/matchingroles).

# API 

Описание всех доступных типов рёбер лежит [в Аркадии в виде сериализованного протобуфа](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/soup/config/edge_types.pb.txt). Для доступа рекомендуется использовать одну из библиотек ([C++](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/soup/config/cpp), [Python](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/soup/config/python), [Java](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/soup/config/java)).

# Примеры

1. [Поиск способов связи yandexuid с mm\_device\_id с использованием API супа](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/soup/config/examples/yuid_mmdevid)

2. [Вычисление списка установленных мобильных приложений по yandexuid'ам, с распространением установок по логину](https://yql.yandex-team.ru/Operations/XK4neJ3udmsEl-mNHwTu9M3C5qK8v15dlflRoNXgi-A=)

