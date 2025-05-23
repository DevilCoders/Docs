# Отладка перехода алерта в No data

Алерты могут переходить в статус <span style="color: blue;">**No data</span>** по двум причинам:
1. Хотя бы по одному селектору из алерта не найдено метрик (например, их не существует или они были удалены по TTL).
2. Хотя бы для одной из метрик во временном окне алерта нет точек.

Более подробно об этом можно прочитать в разделе [{#T}](../../concepts/alerting/index.md#no-data-policies).

Ниже — наиболее частые ситуации, в которых алерт может переходить в статус <span style="color: blue;">**No data</span>**.

## В селекторе мульти-алерта присутствуют устаревшие метрики {#outdated-metrics}

Под-алерты в мульти-алерте генерируются для всех существующих метрик по заданному селектору, в том числе для метрик, в которые не поступают новые значения. При вычислении алерта такие под-алерты переходят в статус <span style="color: blue;">**No data</span>**, так как для них отсутствуют значения в окне вычисления алерта.

Пример такой ситуации: хосты, которые передавали метрики, были удалены, но метрики в мониторинге остались. 

Для того, чтобы перестать получать алерты по неактуальным метрикам, можно воспользоваться одним из следующих способов:

1. Настроить [политики](../../concepts/alerting/index.md#no-data-policies) для обработки отсутствия данных в алерте;
2. Настроить [TTL](../../concepts/deletion/ttl.md) для автоматического удаления неактуальных метрик;
3. Создать [запрос на удаление метрик по селектору](../../problems/howtoreport.md#deletion).


## Метрики, по которым формируется под-алерт, были удалены {#deleted-metrics}

Под-алерты для каждого мульти-алерта генерируются каждые 10 минут, а вычисление алертов происходит каждую минуту.

Если метрика, по которой сгенерирован под-алерт, была удалена (например, сработал [TTL](../../concepts/deletion/ttl.md)), то при очередном вычислении алерта метрика будет отсутствовать, и, согласно политике *No metrics policy*, алерт перейдет в <span style="color: blue;">**No data</span>**.

Под-алерты для удаленных метрик будут удалены из мульти-алерта в следующем цикле генерации под-алертов.

Обработка отсутствия данных в метриках, по которым вычисляется алерт, осуществляется с помощью [политик](../../concepts/alerting/index.md#no-data-policies).





