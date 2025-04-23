## Фингерпринт iOS между ssp и аппметрикой

Вид связок: ssp_user_id - mm_device_id
Таблица в супе: [ssp_user_id_mm_device_id_app-metrica-ios_fingerprint](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/state/graph/v2/soup/ssp_user_id_mm_device_id_ssp-app-metrica-ios_fingerprint)

### Основная таска - UpdateSoupEdges
* ежедневно запускается sandbox [шедулером](https://sandbox.yandex-team.ru/scheduler/24301/view)
* собирает фп связки по дневному rtb-логу
* складывает их в общий пул [all_pairs](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/state/fingerprint/ssp/all_pairs), считает статистику
* собирает из пула "хорошие" связки
* складывает хорошие в суп табличку [ssp_user_id_mm_device_id_app-metrica-ios_fingerprint](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/state/graph/v2/soup/ssp_user_id_mm_device_id_ssp-app-metrica-ios_fingerprint)



### Метрики
- Все метрики считаются [тут](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/metrics/fingerprint).
- Основной [дашборд](https://datalens.yandex-team.ru/uj0m556sqfoir-unifiedcryptastats?tab=QyZ).
