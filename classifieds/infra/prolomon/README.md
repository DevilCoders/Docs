# Prolomon

Сервис по перекладыванию метрик из Solomon в Prometheus, представляет собой примитивный exporter.

В настоящее время реализует экспорт метрик:

- **kafka_log_logendoffset** [VERTISADMIN-27065](https://st.yandex-team.ru/VERTISADMIN-27065)
- **kafka_group_topic_partition_lag** [VERTISADMIN-27236](https://st.yandex-team.ru/VERTISADMIN-27236)
- **kafka_group_topic_partition_offset** [VERTISADMIN-28450](https://st.yandex-team.ru/VERTISADMIN-28450)

Могут быть получены из ptomethtus запросами вида:

```promql
kafka_mdb_selective{sensor="kafka_group_topic_partition_lag"}
kafka_mdb_selective{sensor="kafka_log_log_logendoffset"}
kafka_mdb_selective{sensor="kafka_group_topic_partition_offset"}
```

## Значения по умолчанию и конфиг передаваемый через env

```go
type config struct {
 DeployMetricsPort     string `env:"_DEPLOY_METRICS_PORT"`
 KafkaClusters         string `env:"KAFKA_CLUSTERS" envDefault:"mdb_mdb9adu18n492urt7kuk,mdb_mdb4u82hc7bsaq7cq1tc"` // cid to watch
 MetricsUpdateInterval int    `env:"UPDATE_INTERVAL" envDefault:"15"` // in sec
 SolomonToken          string `env:"SOLOMON_TOKEN"` // https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1c0c37b3488143ff8ce570adb66b9dfa, https://yav.yandex-team.ru/secret/sec-01fjm24673twte7x8x8ht80p5q
}
```
