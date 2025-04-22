### Deploy 
- api       -> https://admin.vertis.yandex-team.ru/services/complaints-api/deployments
- scheduler -> https://admin.vertis.yandex-team.ru/services/complaints-scheduler

or start chat with https://t.me/vertis_shiva_bot and subscribe to
- sub -l [test/prod] complaints-scheduler
- sub -l [test/prod] complaints-api

### Monitoring

- graphana -> https://grafana.vertis.yandex-team.ru/d/NVmcntq7z/complaints-v2?orgId=1&from=now-2d&to=now
- juggler  -> search by tag 'vertis_ops_complaints-v2' or 'vertis_ops_test_complaints-v2'
- sentry scheduler -> https://sentry.vertis.yandex.net/verticals/complaints-scheduler/ 
- sentry api  ->  https://sentry.vertis.yandex.net/verticals/complaints-api/ 

## Keep in mind 

Возможны проблемы с id жалобщика в недвиге, нам присылают в СТАРЫХ ЖАЛОБАХ такие префиксы:
// "device" <- сookie - в новых убрали
// "cuid" <- yandex_uid - в новых убрали
// "uid" <- yandex_uid  - в новых убрали
// "NoUser" <- не должно быть мне сказали
// "phone"  <- временный id, не убирали

Также недвига в 2018 отправляла нам временные оффер id, поэтому могут возникнуть проблемы с простановкой сигнала.
Хотя этот механизм с временными id вроде давно не используется 