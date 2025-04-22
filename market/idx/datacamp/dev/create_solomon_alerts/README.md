# CREATE_SOLOMON_ALERTS

Инструмент предназначенный для создания алертов и мониторинга для топиков в LogBroker

Использование:
```
ya make
./make_solomon_alerts --solomon-token-path ~/.solomon_token --project-id market-indexer  --service piper --topic  /market-indexer/prod/united/datacamp-categories
```

У вас должны быть права на изменение метрик в соломоне для выбранного проекта.
Для принудительного обновления существующих нужно использовать опцию ```--force```.

В настоящий момент используются следующие метрики:
- ReadTimeLagMs
- WriteTimeLagMsByCommitted
- MessageLagByCommitted

Новые метрики и алерты добавляются в таблицу ALERT_SENSOR_TABLE

TODO:
- Удаление и зачистка созданных алертов
- Обновление всех существующих алертов
- Фильтр с выбором необходимых метрик
- Настройка Juggler
