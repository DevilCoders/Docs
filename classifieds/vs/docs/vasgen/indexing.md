# Стейт индексирования

### Main state
State, получающийся в результате индексирования, можно найти здесь: 
- [testing](https://yt.yandex-team.ru/arnold/navigation?path=//home/saas/ferryman-prestable/vasgen_search_lb/workspace/state/main)
- [prod](https://yt.yandex-team.ru/arnold/navigation?path=//home/saas/ferryman-stable/vasgen_search_lb/workspace/state/main)

Достать данные отсюда можно с помощью вот такого запроса:

```sql
SELECT
    Url,
    ProtoMessage
FROM arnold.home/saas/ferryman-stable/vasgen_search_lb/workspace/state/main
where Url='vasgen/g/29526083524415488'
LIMIT 100;
```

### YT pull <a name="yt-pull"></a>
Файл _full.N_ в папке: 
- [testing](https://yt.yandex-team.ru/arnold/navigation?path=//home/saas/ferryman-prestable/vasgen_search_lb/ytpull)
- [prod](https://yt.yandex-team.ru/arnold/navigation?path=//home/saas/ferryman-stable/vasgen_search_lb/ytpull)

### Маппинг
- [testing](https://ydb.yandex-team.ru/db/ydb-ru-prestable/home/lesser-daemon/mydb/browser/general/mapping)
- [prod](https://ydb.yandex-team.ru/db/ydb-ru/verticals/production/vs_saas/browser/general/mapping)
