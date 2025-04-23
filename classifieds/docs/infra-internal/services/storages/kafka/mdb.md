# kafka в MDB

## [Testing](https://cloud.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-kafka/cluster/mdb9adu18n492urt7kuk/view)

Name: **kafka-shared-01-test**

CID: **mdb9adu18n492urt7kuk**

## [Prod](https://cloud.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-kafka/cluster/mdb4u82hc7bsaq7cq1tc/view)

Name: **kafka-shared-01-prod**

CID: **mdb4u82hc7bsaq7cq1tc**

## Настройки топика по умолчанию

* Имя - указываем осмысленное название топика. В test/prod названия должны совпадать;
* Количество разделов (partitions) - необходимое количество партиций. Выбирается заказчиком топика, по умолчанию не указывается и соответсвует числу брокеров в кластере;
* Фактор репликации (replication factor) - указываем значение `2`;
* Минимальное число синхронных реплик (aka min.insync.replicas) - указываем значение `2`;
* ~~Установить опцию `min.insync.replicas = 1`. ***ВНИМАНИЕ*** эта опция носит временный характер. Необходима до восстановления работоспособности DC в MAN.~~

## YAV и создание пользователей

1. В настройках кластера создать нового пользователя: `<serviceName>` с правами на чтение и запись, те: `ACCESS_ROLE_CONSUMER` + `ACCESS_ROLE_PRODUCER`. (`<serviceName>` - имя сервиса из тикета VASUP, является названием существующего сервиса в карте сервисов);
2. Все секреты хранятся в [секретнице](https://yav.yandex-team.ru/);
3. Все названия секретов имеют вид `kafka-<env>-<serviceName>`, например: `kafka-prod-rent-appointments`;
4. Секрет содержит ключи:
   * PASSWORD: `добыть из pwgen -1 20 1`
   * USER: `<serviceName>`
5. Секрет содержит тэг `kafka`;
6. Описание секрета содержит id тикета в st.yandex-team.ru.

### Готовые примеры секретов

* [test_1](https://yav.yandex-team.ru/secret/sec-01g4yy1ehc11n8819z1edsq981/explore/versions)
* [test_2](https://yav.yandex-team.ru/secret/sec-01g4yy4507swzt5xemrghymhse/explore/versions)

## Наколенная автоматика

```sh
# создать топик topicName в кластере clusterID
$ yc managed-kafka topic create <topicName> --cluster-id <clusterID> --min-insync-replicas 1 --partitions 2 --replication-factor 2
# создать пользователя serviceName в кластере clusterID с паролем ZZZZ выдать права producer+consumer на topicName
$ yc managed-kafka user create <serviceName> --cluster-id <clusterID> --permission role=producer,role=consumer,topic=<topicName> --password ZZZZZZZ

# создать секрет в prod
$ yav create secret kafka-prod-<serviceName> -c 'VASUP-XXXX' \
  -v '{"PASSWORD": "ZZZ", "USER": "<serviceName>"}' \
  -r +owner:staff:yandex_personal_vertserv_infra_mnt -r +reader:robot-vertis-yav-prd \
  -t 'kafka'

# создать секрет в test
$ yav create secret kafka-test-<serviceName> -c 'VASUP-XXXX' \
  -v '{"PASSWORD": "XXX", "USER": "<serviceName>"}' \
  -r +owner:staff:yandex_personal_vertserv_infra_mnt -r +reader:robot-vertis-yav-tst \
  -t 'kafka'
```

## Про tuning

После нескольких случаев остановки кластеров из-за исчерпания ресусров были приняты меры:

- Для тестинга:
  - Более агрессивная политика `cleanup-policy = compact_and_delete` вместо `delete`;
  - Обновление `cleanup.policy` влияет на старые сегменты лога, для ее активации на старых топиках нужно потрогать `delete.retention.ms`;
  - Уменьшено c 7d до 1d хренение основного лога `retention.ms`;
  - Финальная комманда: `yc managed-kafka topic update vos2-auto-offers-calls-updates --cluster-id mdb9adu18n492urt7kuk --delete-retention-ms 86400000 --cleanup-policy compact_and_delete --retention-ms 86400000`
- Для прода:
  - Не определено, зависит от <https://st.yandex-team.ru/VERTISADMIN-28212>
