# Стрелялка

Пример запроса для исходных данных в YQL (https://yql.yandex-team.ru)

```
use hahn;

SELECT count(1) as count, vhost as host, request as path
FROM `home/logfeller/logs/qloud-router-log/1d/2020-03-05`
WHERE qloud_project = 'rasp'
AND qloud_application = 'morda-front'
AND qloud_environment = 'production'
AND nginx_request_method = 'GET'
AND status = '200'
AND request LIKE '/station/%'
GROUP BY vhost, request
ORDER BY count DESC
LIMIT 300
```

## Примеры команд из консоли

### Запустить интеграционный тест

```
node transpilerOnFly --path=./tools/integrationTest/integrationTest.ts -- --etalon=rasp.yandex --testing=experiments2.morda-front.rasp.common.yandex --maxConcurrent=3
```
