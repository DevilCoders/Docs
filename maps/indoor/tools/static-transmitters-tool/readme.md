## Утилита для загрузки/выгрузки/управления статическими трансмиттерами

### Actions

#### Help

conn - строка подключения к индор-базе - обязательный параметр, остальное в зависимости от action

Usage: static-transmitters-tool --conn <value> <options...>

  --conn <value>      Connection string to indoor db
  --action <value>    Action: (help,import,export,export-patch,apply-patch,activate)
  --file <filename>   Path to input/output file or stdin/stdout
  --plan-id <value>   Data indoor plan id (nmaps id)
  --version <value>   Data version
  --level <value>     Data indoor universal level id
  --status <value>    Data status (draft,active,archive)


#### import
Загрузка данных в базу из tsv-файла.
Необходимые колонки:
* longitude
* latitude
* indoor_plan_id
* indoor_level_universal_id
* transmitter_id
* transmitter_type
* signal_parameter_a
* signal_parameter_b
* version
* transmitter_description

```
longitude       latitude        indoor_plan_id  indoor_level_universal_id       transmitter_id  transmitter_type        signal_parameter_a      signal_parameter_b      version         transmitter_description
37.4157037125875        55.9815069465472        3686231333      1       F7826DA6-4FA2-4E98-8024-BC5B71E0893E,16542,12270        beacon  -70     5       svo_b_2022_01_19        aIKb 58
```

Пример запуска:<br/>
`./static-transmitters-tool --conn <postgresql://...> --action import --file <file-tsv>`

#### export
Экспорт данных в tsv-формате, в дополнении к "импортным" колонкам добавятся:
* id
* status
* created_at
* modified_at
* original_id

Пример запуска:<br/>
`./static-transmitters-tool --conn <postgresql://...> --action export --file <file-tsv> --plan-id 3686231333 --version svo_b_2022_01_19 --level 1 --status active`

#### export-patch
Экспорт данных в сокращенном tsv-формате, колонки:
* id
* longitude
* latitude

Необходимо для внешнего изменения координат маяков и дальнейшей загрузки данных с помощью `--action apply-path`

Пример запуска:<br/>
`./static-transmitters-tool --conn <postgresql://...> --action export-path --file <file-tsv> --plan-id 3686231333 --version svo_b_2022_01_19 --level 1 --status active`

#### apply-patch
Загрузка и модификация текущих данных согласно внутренним id-кам из tsv-файла, обязательные колонки:
* id
* longitude
* latitude

Если текущая версия маяка draft, то применяются новые координаты.<br/>
Если active, то делается копия с записью original_id = id (алгоритм расчета радиокарты возмет предыдущую копию данных в status=active), далее текущая версия становится draft и применяются новые координаты.<br/>
Для archive-версии никаких изменений не предусмотрено, будет ошибка.

Пример запуска:<br/>
`./static-transmitters-tool --conn <postgresql://...> --action apply-path --file <file-tsv>`

#### activate
Активация записей согласно внутренним id-кам из tsv-файла, обязательные колонки:
* id

Текущая версия маяка должна быть draft, иначе ошибка.<br/>
Если есть активная версия с original_id=id, то у нее меняется статус archive.<br/>
Текущая draft-версия меняет статус на active.

Пример запуска:<br/>
`./static-transmitters-tool --conn <postgresql://...> --action activate --file <file-tsv>`

