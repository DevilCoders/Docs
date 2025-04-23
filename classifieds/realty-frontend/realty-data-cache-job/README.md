# realty-data-cache-job

Сервис для кеширования ссылок для блоков на Яндекс.Недвижимости.

Тип сервиса - batch.

Периодическая таска, запускается раз в неделю. 

Пока собирает и кеширует ссылки для футера на Яндекс.Недвижимости для страниц типа: search, search-categories, index.

Генерируются наборы ссылок и помещаются в редис.

Testing: https://yc.yandex-team.ru/folders/foo4nrk07dl14udeb4js/managed-redis/cluster/mdb9sdq0uulda3h6ss6p?section=overview

Prod: https://yc.yandex-team.ru/folders/foo4nrk07dl14udeb4js/managed-redis/cluster/mdb0o5q03h0q2236itkm?section=overview

Ключ ```"rgid:${rgid};type:${type};category:${category}"```

## Основная информация
| Service | URL |
|---|---|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-data-cache-job |
| Deploy | https://admin.vertis.yandex-team.ru/services/realty-data-cache-job |
| Grafana | https://grafana.vertis.yandex-team.ru/d/zTp8d_Lnk/realty-data-cache-job?orgId=1&var-ENV=Prometheus-testing&var-dc=All |
