# Kafka в Вертикалях

Для Вертикальных сервисов существуют общие коммунальные кластеры Kafka в MDB, по одному для тестинга и прода.
Параллельно работают исторически сложившиеся "железные" кластеры Kafka, поддерживаемые группой эксплуатации Вертикалей.
Актуальными считаем кластера Kafka в MDB, все новые топики селим в них.
"Железная" Kafka более не развивается, считается legacy и deprecated. Новые топики в ней не заводим без крайней необходимости. Ожидаем, что когда-нибудь существующие топики переедут из "железной" кафки в MDB.

## Kafka в MDB
В настоящий момент управление топиками и пользователями в кластерах производится вручную [руками админов через тикет в очереди VASUP](https://st.yandex-team.ru/createTicket?queue=VASUP&_form=62920), однако [ведётся работа](https://st.yandex-team.ru/VERTISADMIN-27333) по интеграции MDB-Кафки с [shiva](../../deploy/quick-start.md) для автоматизации этих процессов.
Kafka в MDB использует ACL для аутентификации пользователей. Создаются отдельные пользователи для записи (от сервисов-продюсеров) и для чтения (от сервисов-консьюмеров).
Подключение производится по SSL, приложение должно использовать сертификат, получить который можно согласно [инструкции](https://docs.yandex-team.ru/cloud/managed-kafka/operations/connect#get-ssl-cert).

#### Кластеры
[Тестинг](https://cloud.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-kafka/cluster/mdb9adu18n492urt7kuk/view)
[Прод](https://cloud.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-kafka/cluster/mdb4u82hc7bsaq7cq1tc/view)

### Политика очистки
Данные в кафке могут удаляться по времени или по месте. По умолчанию настроено удаление только по времени жизни сегмента. Политику можно переопределить на уровне отдельного топика.

{% note warning %}

Ограничение по месту действует в рамках партиции, а не топика целиком.

{% endnote %}

Тестинг – 1 день
Прод – 7 дней

### Connection string
Стоит обратить внимание, что списки хостов теоретически могут изменяться со временем, и это изменение в моменте может не быть синхронизировано с данной докой. Поэтому перед использованием лучше сверить эти списки с фактическими списками хостов в кластерах MDB.
В будущем планируем формировать conn string динамически: [тикет](https://st.yandex-team.ru/VERTISADMIN-27333).

#### Тестинг
```
sas-7pa44rjg1t1t7smt.db.yandex.net:9091,sas-ekaclmp7msddjrme.db.yandex.net:9091,sas-lnqm3t9cbke9u64p.db.yandex.net:9091,vla-6a4msuafgn2f8b68.db.yandex.net:9091,vla-m5rmfk02bccg4tnq.db.yandex.net:9091,vla-pjm6572sv9lncof7.db.yandex.net:9091,vlx-5dhc8qes11vuhi83.db.yandex.net:9091,vlx-oq0913pdrte0hc1f.db.yandex.net:9091,vlx-qtp75pv57cscjb47.db.yandex.net:9091
```

#### Прод
```
sas-2q7gflm28ftbfm6g.db.yandex.net:9091,sas-5cvbfk4mf6bmb1s3.db.yandex.net:9091,sas-5df2emjv32u2stat.db.yandex.net:9091,sas-a6q9aa7noo4u7ibh.db.yandex.net:9091,sas-b0jfur73ub9n5013.db.yandex.net:9091,sas-d4hslqb4ebqca5in.db.yandex.net:9091,sas-dvhg4qe7odvv6cej.db.yandex.net:9091,sas-e67me1ler6av5eau.db.yandex.net:9091,sas-fbos5nj1c6qc8cp2.db.yandex.net:9091,sas-sttur2ninkeghkom.db.yandex.net:9091,vla-261ikb4ab5uk3nuc.db.yandex.net:9091,vla-47aajmado8uvbsr1.db.yandex.net:9091,vla-54ctm6n3bso5vhu3.db.yandex.net:9091,vla-71m8dv6ovn5blgdu.db.yandex.net:9091,vla-7gkc78g1891jm3hb.db.yandex.net:9091,vla-7ks6jp5jb08got6t.db.yandex.net:9091,vla-cijlv7hqqhlfq76i.db.yandex.net:9091,vla-e9tojjmg4sq9luf7.db.yandex.net:9091,vla-h6fba2mibjnlp2c8.db.yandex.net:9091,vla-tgaa5f7adihgiqgg.db.yandex.net:9091,vlx-1nqlhhhe9r4go1vb.db.yandex.net:9091,vlx-3f9ipnvulnqb5hsm.db.yandex.net:9091,vlx-5rivb6pqelug6gre.db.yandex.net:9091,vlx-7vvgqh70f1v5nj68.db.yandex.net:9091,vlx-864712stauf83ja9.db.yandex.net:9091,vlx-9qke5errapnrhll4.db.yandex.net:9091,vlx-bm8f6ii4874u4a8k.db.yandex.net:9091,vlx-bop2dpl64pk8e81q.db.yandex.net:9091,vlx-e73trc829vqvk6q3.db.yandex.net:9091,vlx-hva15vvb1rbs3kcq.db.yandex.net:9091
```

### Графики
[Метрики чтения](https://grafana.vertis.yandex-team.ru/d/mdb-kafka/mdb-kafka-consumer?orgId=1&refresh=30s)

Различные системные метрики
[Тестинг](https://cloud.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-kafka/cluster/mdb9adu18n492urt7kuk/monitoring)
[Прод](https://cloud.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-kafka/cluster/mdb4u82hc7bsaq7cq1tc/monitoring)
[Grafana](https://grafana.vertis.yandex-team.ru/goto/Eet0T6rnz?orgId=1)

## Kafka "на железе"
В "железной" кафке не используется ACL и SSL, подключение происходит посредством PLAIN-протокола.
В случае крайней необходимости новые топики заводятся через [тикет в VASUP](https://st.yandex-team.ru/createTicket?queue=VASUP&_form=62920), с обоснованием такой необходимости.

### Политика очистки
Тестинг – 2 дня
Прод – 7 дней

### Connection string

#### Тестинг

SLB-балансер
```
kafka-legacy-int.noc-slb.test.vertis.yandex.net:9092
```

Список брокеров
```
kafka-01-myt.test.vertis.yandex.net:9092,kafka-01-vla.test.vertis.yandex.net:9092,kafka-01-sas.test.vertis.yandex.net:9092
```
#### Прод
SLB-балансер
```
kafka-legacy-int.noc-slb.prod.vertis.yandex.net:9092
```

Список брокеров
```
kafka-01-myt.prod.vertis.yandex.net:9092,kafka-02-myt.prod.vertis.yandex.net:9092,kafka-03-myt.prod.vertis.yandex.net:9092,kafka-04-myt.prod.vertis.yandex.net:9092,kafka-01-vla.prod.vertis.yandex.net:9092,kafka-02-vla.prod.vertis.yandex.net:9092,kafka-03-vla.prod.vertis.yandex.net:9092,kafka-04-vla.prod.vertis.yandex.net:9092,kafka-01-sas.prod.vertis.yandex.net:9092,kafka-02-sas.prod.vertis.yandex.net:9092,kafka-03-sas.prod.vertis.yandex.net:9092,kafka-04-sas.prod.vertis.yandex.net:9092
```

### Графики
[Метрики чтения](https://grafana.vertis.yandex-team.ru/d/kpdUo1ank/burrow-kafka-consumer?orgId=1&refresh=1m)

[Системные метрики](https://nda.ya.ru/t/ssEKepY455zSpQ)

## Best practices

1) Используйте [сжатие](https://kafka.apache.org/documentation/#producerconfigs_compression.type) при записи.
2) Рекомендуемый коэффициент репликации – 3. Это позволяет переживать выпадение любой машины или целого датацентра.
3) Пишите данные с [acks=all](https://kafka.apache.org/documentation/#producerconfigs_acks) по умолчанию. Так вы не потеряете данные.
4) При чтении лучше выставлять оффсет по умолчанию в [earliest](https://kafka.apache.org/documentation/#consumerconfigs_auto.offset.reset). Иногда kafka не находит запрашиваемый оффсет и использует эту политику для сброса. Так вы можете обработать данные за день повторно, но зато ничего не потеряете.
5) Указывайте [client.id](https://kafka.apache.org/documentation/#consumerconfigs_client.id) для продюсеров и консьюмеров (например, пишите туда имя приложения) – это повышает наблюдаемость.
6) Дубли могут появиться как при записи, так и при обработке – учитывайте это в логике консьюмера. 
7) Следите за лагом обработки для консьюмера.