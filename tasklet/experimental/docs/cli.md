# Command line tool

## tasklet-tool

Для управления тасклетами используется `ya tool tasklet`.
При необходимости можно собрать бинарник `tasklet-tool` самому, он находится в `arcadia/tasklet/experimental/cli`.

В [tasklet/experimental/examples](https://a.yandex-team.ru/arc/trunk/arcadia/tasklet/experimental/examples)
можно найти примеры тасклетов и позапускать их.

## Распространенные аргументы запуска { #arguments }

#### Descriptor file

```
-f, --file <t.yaml>             Path to tasklet descriptor (t.yaml)
```

При запуске клиент тасклетов использует yaml-спецификацию тасклета
в текущей директории (`t.yaml` по умолчанию) и достаёт из него недостающие параметры запроса.

Например, любой тасклет создаётся и находится в некотором пространстве имен (_Namespace_).
Поэтому, если при запуске не указать этот параметр, то он будет взят из файла yaml-спецификации.

#### Output format

```
-o, --output [json|yaml|table]  Output format.
```

Для большинства команд можно управлять форматом результата, печатаемого в stdout.

#### Help { #help-arg }

```
-h, --help                      Show this message and exit.
```

## Основные команды { #commands }

### Работа с Namespace { #namespaces }

```
~/arc/.../secrets_extractor$ ya tool tasklet namespace create --owner abc:tasklets
 Namespace     test-tasklets
 Namespace ID  4517d9e6-4b3d-45df-bae3-5329f8c8186a
 Owner         abc:tasklets
 Created       2022-03-28T13:27:28


~/arc/.../secrets_extractor$ ya tool tasklet namespace list
+---------------+--------------------------------------+--------------+---------------------+
|   Namespace   |             Namespace ID             |    Owner     |       Created       |
+---------------+--------------------------------------+--------------+---------------------+
| test-tasklets | 4517d9e6-4b3d-45df-bae3-5329f8c8186a | abc:tasklets | 2022-03-28T13:27:28 |
+---------------+--------------------------------------+--------------+---------------------+
```

### Работа с Tasklet { #tasklets }

```
~/arc/.../secrets_extractor$ ya tool tasklet tasklet list
No tasklets in namespace 'test-tasklets'

~/arc/.../secrets_extractor$ ya tool tasklet tasklet create
 Tasklet     secrets_extractor
 Tasklet ID  7a80cc09-7dc5-42c0-a0ed-dc8a187ae3e7
 Owner       abc:tasklets
 Catalog     /library/examples
 Created     2022-03-28T13:29:15
 Revision    0

~/arc/.../secrets_extractor$ ya tool tasklet tasklet list
+-------------------+--------------------------------------+--------------+-------------------+---------------------+----------+
|      Tasklet      |              Tasklet ID              |    Owner     |      Catalog      |       Created       | Revision |
+-------------------+--------------------------------------+--------------+-------------------+---------------------+----------+
| secrets_extractor | 7a80cc09-7dc5-42c0-a0ed-dc8a187ae3e7 | abc:tasklets | /library/examples | 2022-03-28T13:29:15 |    0     |
+-------------------+--------------------------------------+--------------+-------------------+---------------------+----------+
```

### Создание новых билдов (Build) { #builds }

```
# Build tasklet binary
~/arc/.../secrets_extractor$ ya m
Ok

# Upload it with schema from t.yaml
~/arc/.../secrets_extractor$ ya tool tasklet build upload --owner TASKLETS --build-schema ./secrets_extractor
Building schema registry ...
Ok
Registered schema with ID: e4ab2f1891f88ae01e1d930eff29edc2
Annotations:
[...]
Calculating total files size ...
	1 file(s) found totally for 242.96MiB.
Done. [00s]
Preparing upload task ...
	Task #1258794245 created: https://sandbox.yandex-team.ru/task/1258794245
	Resource #2919461267 registered: https://sandbox.yandex-team.ru/resource/2919461267
Done. [02s]
Uploading |#####################################################################################################################################| 100% | 242.96MiB/242.96MiB | Elapsed Time: 0:00:36 | Time:  0:00:36 |  6.7 MiB/s
Sharing uploaded data ...
	Resource currently is in 'READY' state.
	Resource download link: http://s3.mds.yandex.net/sandbox-36768-default/2919461267/secrets_extractor
	Skybone ID is rbtorrent:677ac56318b55b9ab8e2bcbf33b184eb2d16ca3e, MD5 checksum is 04b31c1dee963b083a92cee963645625
Done. [00s]
 Build ID     f70af745-d441-45c1-9917-db464ace9563
 Resource ID  2919461267
 Type         binary
 CPU          1.000
 RAM          1.0Gb
 Storage      hdd:100.0Mb
 Created      2022-03-28T15:53:47

~/arc/.../secrets_extractor$ ya tool tasklet build list
+--------------------------------------+-------------+--------+-------+-------+-------------+---------------------+
|               Build ID               | Resource ID |  Type  |  CPU  |  RAM  |   Storage   |       Created       |
+--------------------------------------+-------------+--------+-------+-------+-------------+---------------------+
| f70af745-d441-45c1-9917-db464ace9563 |  2919461267 | binary | 1.000 | 1.0Gb | hdd:100.0Mb | 2022-03-28T15:53:47 |
+--------------------------------------+-------------+--------+-------+-------+-------------+---------------------+
```

### Управление метками (Label) { #labels }

```
~/arc/.../secrets_extractor$ ya tool tasklet label list
No labels in tasklet 'secrets_extractor'

# Take already created Build to initialize label
~/arc/.../secrets_extractor$ ya tool tasklet label create latest --build f70af745-d441-45c1-9917-db464ace9563
 Label     latest
 Label ID  781cffa7-a240-4635-9465-8df6cd5c92ba
 Build ID  f70af745-d441-45c1-9917-db464ace9563

~/arc/.../secrets_extractor$ ya tool tasklet label list
+--------+--------------------------------------+--------------------------------------+-------------+--------+-------+-------+-------------+---------------------+
| Label  |               Label ID               |               Build ID               | Resource ID |  Type  |  CPU  |  RAM  |   Storage   |       Created       |
+--------+--------------------------------------+--------------------------------------+-------------+--------+-------+-------+-------------+---------------------+
| latest | 781cffa7-a240-4635-9465-8df6cd5c92ba | f70af745-d441-45c1-9917-db464ace9563 |  2918987545 | binary | 1.000 | 1.0Gb | hdd:100.0Mb | 2022-03-28T13:49:19 |
+--------+--------------------------------------+--------------------------------------+-------------+--------+-------+-------+-------------+---------------------+
```

### Запуск исполнения (Execution) { #executions }

Запуск исполнения тасклета выполняется для заданного лейбла.
`input` для исполнения можно передать через `stdin` или через файл. Также при помощи

```
~/arc/.../secrets_extractor$ ya tool tasklet execution list
No executions in 'test-tasklets/secrets_extractor'

~/arc/.../secrets_extractor$ echo '{"secrets": [{"id": "sec-01fymqbk1d656srm8g18n3w1wg"}]}' | ya tool tasklet run --input-format json latest -
 Execution ID  77fe2104-da9c-4448-8314-2a9f966e99ad
[...]
 Status        executing
 Sandbox Task   (id: 0)
 Result        <no result>

~/arc/.../secrets_extractor$ ya tool tasklet execution get 77fe2104-da9c-4448-8314-2a9f966e99ad
[...]
 Status        executing
 Sandbox Task  Sandbox status: ASSIGNED (id: 1258798649)
[...]

~/arc/.../secrets_extractor$ ya tool tasklet execution get 77fe2104-da9c-4448-8314-2a9f966e99ad
[...]
 Status        finished
 Sandbox Task  Sandbox status: SUCCESS (id: 1258798649)
 Result        Finished with exit code: 0 (0.46578s)
 Output        b'<some serialized protobuf message>'

~/arc/.../secrets_extractor$ ya tool tasklet execution get-output 77fe2104-da9c-4448-8314-2a9f966e99ad
{
    "secrets": [
        {
            "id": "sec-01fymqbk1d656srm8g18n3w1wg",
            "values": [
                {
                    "key": "qwe",
                    "value": "sec-01fymqbk1d656srm8g18n3w1wg:ver-01fymqbk1vg135e4s1t0sb5xes:qwe"
                },
                [...]
            ],
            "version": "ver-01fymqbk1vg135e4s1t0sb5xes"
        }
    ]
}
```
