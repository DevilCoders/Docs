## Фингерпринт iOS по аппметричному логу

Вид связок: *mm_device_id - mm_device_id*

Таблица в супе: [mm_device_id_mm_device_id_app-metrica-ios_fingerprint](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/state/graph/v2/soup/mm_device_id_mm_device_id_app-metrica-ios_fingerprint)

### Основная таска - UpdateSoupEdges
* ежедневно запускается sandbox [шедулером](https://sandbox.yandex-team.ru/scheduler/24301/view)
* собирает фп связки по дневному аппметричному логу
* складывает их в общий пул [all_pairs](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/state/fingerprint/appmetrica/all_pairs), считает статистику
* собирает из пула "хорошие" связки
* складывает хорошие в суп табличку [mm_device_id_mm_device_id_app-metrica-ios_fingerprint](//home/crypta/production/state/graph/v2/soup/mm_device_id_mm_device_id_app-metrica-ios_fingerprint)

### Типы фингерпринтов
* [identity](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/fingerprint/match/appmetrica/lib/query/identity_fp.sql)
* [location](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/fingerprint/match/appmetrica/lib/query/location_fp.sql)
* [mobile](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/fingerprint/match/appmetrica/lib/query/mobile_fp.sql)
* [mobile_ip](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/fingerprint/match/appmetrica/lib/query/mobile_ip_fp.sql)

### Метрики
- Все метрики считаются [тут](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/metrics/fingerprint).
- Основной [дашборд](https://datalens.yandex-team.ru/uj0m556sqfoir-unifiedcryptastats?tab=QyZ).
