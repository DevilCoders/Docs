Утилита апдейтит ресурс с семплами логов (с дев-контура) в сендбоксе для caesar/b2b-теста.

Обратите внимание, что после добавления лога в sources.py семплер необходимо пересобрать

**На выходе утилиты будет айди ресурса. Его необходимо прописать [тут](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/caesar/tests/lib/b2b/ya.make.inc?rev=r8860623#L17) и [ниже в том же файле](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/caesar/tests/lib/b2b/ya.make.inc?rev=r8860623#L22), заменив старые айдишники с пометкой LOG SAMPLES**

Утилита требует ssh-ключи, если используете разраб-машины, используйте ssh -A

Берётся последний ресурс из сендбокса и создаётся новый

Типовой вызов утилиты

```./sampler  update_source direct-yt/direct-banners-log```


Вызов с опциями
```./sampler  update_source direct-yt/direct-banners-log```

По умолчанию чтение выполняется от имени вызывающего (проверка прав всегда). Для логброкеровских логов поддерживаются `--use-tvm`, `--tvm-id`, `--tvm-secret`. Первое для команды bigrt и требует доступа в секретницу за секретами тестового цезаря. Последние позволяют явно сделать вызов с данными айди и секретом. Поэтому если вы не в bigb убедитесь, что у вас есть ReadTopic (в логброкере) или аналогичные права на таблички в yt

Пример вызова для логброкера при наличии прав до секретов цезаря

```sampler --use-tvm update_source bar_navig/bar-navig-log```

По умолчанию данные семплируются с 7го контура, кастомизируется через `--dev-key 8`

При добавлении нового логброкер-топика, следует создать read-rules на /bigb/test/sampler-consumer

```logbroker -s {cluster} schema create read-rule -t {topic} -c /bigb/test/sampler-consumer --all-original```


grpc._channel._MultiThreadedRendezvous: <_MultiThreadedRendezvous of RPC that terminated with:
	status = StatusCode.UNAVAILABLE
	details = "failed to connect to all addresses"

Если видишь такую ошибку, у тебя нет доступа к аркадийному апи (увы), возьми ресурс отсюда https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/caesar/tests/lib/b2b/ya.make.inc и подтсавь аргумент `--base-resource ddddddddd`
