### Продукт/подсистема
GrUT (единая база рекламы). Репликация из MySQL Директа в GrUT.


### Роль в работе продукта/подсистемы
Выполняет две задачи:
- дает примеры данных для разработки дальнейшей части системы (GrUT → CaSaR)
- создает/подновляет объекты в GrUT (поддерживая консистентность данных) до момента,
пока все пишущие места Директа не начали синхронно записывать данные в GrUT


### Датафлоу
ESS-router отслеживает изменения сразу по нескольким типам объектов, и пишет их все в один топик этого процессора.
Затем процессор:
1. вычитывает пачку данных
1. пробует обработать ее всеми типами `*ReplicationWriter`
([список тут](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/mysql2grut/replicationwriter/ReplicationWriterService.kt?rev=r9303069#L19)),
каждый из которых делает
([код](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/mysql2grut/replicationwriter/BaseReplicationWriter.kt?rev=r9234102#L26))
примерно следующее
1. отфильтровывает внутри из всей пачки только свои объекты
1. выкидывает те объекты, для которых внутри GrUT'а отсутствует родительский объект
1. пишет в GrUT объекты, которые нужно создать или обновить
1. удаляет из GrUT соответствующие объекты

Если любой из Writer'ов в процессе обработки чанка упадет — процессор ничего не закоммитит в логброкер и на следующей итерации будет повторять обработку (этот процесс может быть бесконечным без вмешательства дежурного).


### Способы наблюдения за текущим состоянием
- [график отставания процессора](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.ess_processor=mysql_to_grut_replication&l.host=CLUSTER&l.sensor=binlog_delay&graph=auto&stack=false&b=6h)
- [Juggler-проверка](https://juggler.yandex-team.ru/project/direct.prod/aggregate?host=checks_auto.direct.yandex.ru&service=jobs.Mysql2GrutReplicationProcessor.working.production&project=direct.prod)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'mysql2grut.Mysql2GrutReplicationProcessor)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы
Могут начаться ошибки (отсутствия родительского объекта) при сохранении объектов из Мастера кампаний (там данные пишутся в том числе в GrUT) для новых клиентов.

В ближайшей перпесктиве (или уже): GrUT будет первоисточником для показа объявлений из Мастера.

Если долго (\~сутки) не чинить процессор, могут прийти дежурные со стороны логброкера с тем что у нас important-consumer не вычитывает данные.


### Как пользователи (или команда) заметят проблему и через какое время
Клиенты — по ошибкам в мастере (если клиент новый и не успел/не смог приехать по репликации — сохранение заявок будет падать).

Разработчики — по отставанию ESS.


### Контакты разработчиков и менеджеров

Разработчики:
- [a-beliakov](https://staff.yandex-team.ru/a-beliakov)
- [elwood](https://staff.yandex-team.ru/elwood)
- [mspirit](https://staff.yandex-team.ru/mspirit)
- [ppalex](https://staff.yandex-team.ru/ppalex)

Если нужно помочь с приоритезацией/экспертами — [poldnev](https://staff.yandex-team.ru/poldnev).


### Желательное время исправления в случае поломки
Разблокировать репликацию клиентов желательно быстро (полчаса), чтобы не ломался мастер кампаний.  
Более детальная починка и восстановление репликцации остальных объектов — день-несколько.


### Способы регулирования работы джобы
_Проперти редактируются в [туле редактирования типизированных свойств](https://direct.yandex.ru/internal_tools/#set_typed_ppc_property)._

#### Отключение репликации
Для большинства объектов есть свои проперти, позволяющие пошардово отлючать (=пропускать) обработку объектов этого типа:
- `grut_skip_campaigns_replication_shards`
- `grut_skip_adgroups_replication_shards`
- `grut_skip_banners_replication_shards`
- `grut_skip_biddable_show_condition_replication_shards`
- `grut_skip_minus_phrases_replication_shards`
- `grut_skip_mobile_content_replication_shards`
- `grut_skip_vcards_replication_shards`
- возможно после написания документации появятся и другие (для новых объектов), с тем же префиксом

В качестве значения нужно указывать номера шардов через запятую, или `all` для отключения сразу во всех.  
Также для точечного пропуска плохого объекта можно использовать общий механизм [{#T}](../../../guide/jeri/howto-ess-blacklist.md).

#### Настройка репликации
Есть три проперти, отвечающие за чанкование запросов к GrUT'у:
- `grut_replication_create_or_update_batch_size`
- `grut_replication_delete_batch_size`
- `grut_replication_get_batch_size`


{% note warning %}

Несмотря на название, могут влиять не только на джобу репликации.

{% endnote %}

Кроме того, данные в очередь репликации может писать ваншот Mysql2GrutReplicationOneshot.
Скорость работы ваншота регулируется пропертями:
- `mysql2grut_oneshot_chunk_size`
- `mysql2grut_oneshot_relax_time_sec`

Проверить, запущен ли ваншот можно на cтранице запусков ваншотов: https://direct.yandex.ru/internal_tools/#oneshot_launches
 
### Известные причины поломок
#### таймауты запросов к GrUT'у
Может выглядеть в логах как сообщение
`ru.yandex.grut.object_api.client.GrutGrpcDeadlineExceededException: io.grpc.StatusRuntimeException: DEADLINE_EXCEEDED: deadline exceeded after 4.999949951s`

Можно попробовать покрутить размер чанка.  
Желательно сдампить текст исключения в тикет, чтобы иметь возможность по request_id / trace_id / span_id / address / host потом раздебажить на стороне ORM причину тормозов.


#### лежит грут
🤷‍♂️, напишите [дежурному GrUT'а](https://abc.yandex-team.ru/services/grut/duty/?interval=P1M)

### растет лаг репликации
🤷‍♂️, напишите [дежурному GrUT'а](https://abc.yandex-team.ru/services/grut/duty/?interval=P1M)


#### отличающийся parent объекта
Выглядит как ошибка _Provided parent key <NN> is different from existing <MM>_.
Пример:
```
ru.yandex.grut.object_api.client.YtGenericException:
'Error executing transactional request; transaction aborted'
<== 'Failed to check the parent key for minus phrase 15699309'
<== 'Provided parent key 31830584 is different from existing 53848217'
```

Возможно из-за битых данных в нашей базе (дубли по id) — нужно исправлять данные.  
В качестве "подорожника" — пропускать конкретный объект через ess или отключать всю репликацию типа в этом шарде.


#### исключения в коде
Могут быть ошибки на чтении и преобразовании данных из базы (что-то не предусмотрели или баг в коде).

Здесь скорее нужно чинить код, в качестве "подорожника" — пропускать объект (ESS-blacklist) или отключать репликацию этого типа объектов (во всех шардах или одном, смотри проперти выше).


### Дополнительно: тонкости и подводные камни
#### Как посмотреть trace запроса в GrUT'е
Для этого есть интерфейс [Jaeger UI](https://jaeger.yt.yandex-team.ru/grut/search) — там (в правом углу) есть поиск "Lookup by Trace ID".

Сам trace_id можно добыть двумя способами:
1. получить из текста ошибки,

   {% cut "например из сообщения" %}

   `Job Mysql2GrutReplicationProcessor shard_24 threw Exception:
   ru.yandex.grut.object_api.client.YtGenericException: 'Error executing transactional request; transaction aborted' <== 'Error fetching data' <== 'Internal RPC call failed' <== 'Chunk data is not preloaded yet'; full error:{"code"=1;"message"="Error executing transactional request; transaction aborted";"attributes"={"address"="end6xkibsird3i2g.sas.yp-c.yandex.net:8090";"method"="CreateObjects";"realm_id"="0-0-0-0";"request_id"="601343f8-650e8a71-ce38ffb2-a556d4d7";"service"="NGrut.NClient.NApi.NProto.ObjectService";"timeout"=4999;"host"="end6xkibsird3i2g.sas.yp-c.yandex.net";"pid"=8;"tid"=2688112837607664097u;"fid"=18446450125620019486u;"datetime"="2022-04-04T15:00:15.373785Z";"trace_id"="d12ec700-0-3a8b9e5e-c8a089c7";"span_id"=5796702458140037413u};"inner_errors"=[{"code"=1;"message"="Error fetching data";"attributes"={"host"="end6xkibsird3i2g.sas.yp-c.yandex.net";"pid"=8;"tid"=5194623260488245463u;"fid"=18446450125613934211u;"datetime"="2022-04-04T15:00:15.373448Z";"trace_id"="d12ec700-0-3a8b9e5e-c8a089c7";"span_id"=5796702458140037413u};"inner_errors"=[{"code"=1;"message"="Internal RPC call failed";"attributes"={"address"="myt0-2525-rpc-proxy-nash.myt.yp-c.yandex.net:9013";"connection_id"="9b62ba35-48705c3b-726f8576-12a729a6";"method"="VersionedLookupRows";"realm_id"="0-0-0-0";"request_id"="97cdfdb-b4f38b92-c1c354e5-f44eaed8";"service"="ApiService";"timeout"=5009u;"host"="myt0-2525-rpc-proxy-nash.myt.yp-c.yandex.net";"pid"=865609;"tid"=14133337292894385343u;"fid"=18435521298187025446u;"datetime"="2022-04-04T15:00:15.371669Z";"trace_id"="d12ec700-0-3a8b9e5e-c8a089c7";"span_id"=17968384373963170016u};"inner_errors"=[{"code"=1;"message"="Chunk data is not preloaded yet";"attributes"={"address"="sas1-2496-node-seneca-sas.sas.yp-c.yandex.net:9012";"chunk_id"="4c54e-5446a5-3ee0064-4f23ad03";"connection_id"="d1a0487e-730a2de4-ff54a0d-5e52aa48";"method"="Multiread";"realm_id"="0-0-0-0";"request_id"="9e271b7a-67fbab6-8787c1cd-bc99a390";"service"="QueryService";"store_id"="4c54e-5446a5-3ee0064-4f23ad03";"table_path"="//home/grut/stable/db/schemas";"tablet_id"="49762-10d351-3ee02be-fab0c6fe";"timeout"=5009;"host"="sas1-2496-node-seneca-sas.sas.yp-c.yandex.net";"pid"=282;"tid"=11366205603471980480u;"fid"=18446440720490208886u;"datetime"="2022-04-04T15:00:15.365673Z";"trace_id"="d12ec700-0-3a8b9e5e-c8a089c7";"span_id"=2048234220288699412u}}]}]}]}	at ru.yandex.grut.object_api.client.ErrorsKt.getException(Errors.kt:63) ~[java-client.jar:?]`

   {% endcut %}

   trace_id это — `d12ec700-0-3a8b9e5e-c8a089c7`
2. сконвертировать директовый trace_id (числовой) скриптом из корня аркадии. пример:
   ```sh
   arcadia % ./grut/deploy/script/trace_id_decode.py  4218639605892680135
   d12ec700-0-3a8b9e5e-c8a089c7
   ```
   компилировать скрипт или собирать не надо, работает так. наш trace_id передавать аргументом командной строки

Полученный id можно вбить в поиск или сразу открыть по ссылке [https://jaeger.yt.yandex-team.ru/grut/trace/<подставь_trace_id>](https://jaeger.yt.yandex-team.ru/grut/trace/d12ec700-0-3a8b9e5e-c8a089c7).

#### Как посмотреть данные в GrUT
Доступ в сами YT таблицы не дают (по вопросам производительности), вместо этого предлагают использовать консольную утилиту **grut-orm**
или смотреть в бекапы таблиц (лежат [на Хане в //home/grut/backups/stable/latest/db](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/grut/backups/stable/latest/db)).

Дырки есть с ppcdev.
Сначала утилиту нужно собрать (из корня аркадии): `ya make --checkout grut/tools/cli/orm/`.
Затем можно делать запросы (get или select).
Пример:
```sh
./grut/tools/cli/orm/grut-orm get campaign 72746886 --address=stable  --selector='/spec' --format=yson --no-tabular
```
Подробнее в [README на утилиту](https://a.yandex-team.ru/arc/trunk/arcadia/grut/tools/cli/orm/README.md), или спрашивать помощи в чатике GrUT'а.

