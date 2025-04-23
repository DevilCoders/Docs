## Утилита для создания РРов

### Использование

* прописать в `rrs_data.py` нужные РРы;
* собрать через `ya make` и перенести на mtcalclog или куда-нибудь, откуда есть доступ к `zk`;
* на mtcalclog проверить, какие порты у envoy'a для доступа к zk с помощью `netstat -plntao | grep envoy`;
* прописать `export ZK_STRING="localhost:XXXXX"`, где `XXXXX` - порт с предыдущего шага;
* запустить программу.

### Пример массива РРов с минимальным набором полей
```json
rrs = [
    {
        "requests": {
            "unique_events": [
                {
                    "store": [
                        {
                            "path": "revenue_events_sharder/IntermediateEvent_1658486564_00000000000012060730_1_591332984136611485_0",
                            "host": "mtcalclog04ft.metrika.yandex.net"
                        },
                        {
                            "path": "revenue_events_sharder/IntermediateEvent_1658486564_00000000000012060730_1_591332984136611485_0",
                            "host": "mtcalclog01it.metrika.yandex.net"
                        }
                    ],
                    "chunk_id": "00000000000012060730_1_591332984136611485_0",
                }
            ]
        }
    },
    {
        "requests": {
            "unique_events": [
                {
                    "store": [
                        {
                            "path": "revenue_events_sharder/IntermediateEvent_1658486564_00000000000012060730_1_591332984136611485_0",
                            "host": "mtcalclog04ft.metrika.yandex.net"
                        },
                        {
                            "path": "revenue_events_sharder/IntermediateEvent_1658486564_00000000000012060730_1_591332984136611485_0",
                            "host": "mtcalclog01it.metrika.yandex.net"
                        }
                    ],
                    "chunk_id": "00000000000012060730_1_591332984136611485_0",
                }
            ]
        }
    }
]
```
