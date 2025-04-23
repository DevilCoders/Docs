# Проверка логов

## promo-triggers

promo-trigger - это топик в [логброкере](https://lb.yandex-team.ru/logbroker/accounts/market-dj/mars/testing/promo-triggers?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1635415208243&metricsTo=1635501608243&sortOrder=%22default%22)

### Чтение

Прочитать данные топика можно, например, так:
```bash
logbroker -s vla.logbroker.yandex.net:2135 data read --topic /market-dj/mars/testing/promo-triggers --consumer /market-dj/mars/testing/demo-consumer
```

За подробностями обращаться [сюда](https://logbroker.yandex-team.ru/docs/quickstart#reading-data)
