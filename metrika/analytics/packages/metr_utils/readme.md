# Table of Contents

* [metr\_utils](#metr_utils)
* [metr\_utils.configs](#metr_utils.configs)
* [metr\_utils.configs.get\_vault\_data](#metr_utils.configs.get_vault_data)
  * [get\_bishop\_config](#metr_utils.configs.get_vault_data.get_bishop_config)
  * [get\_yav](#metr_utils.configs.get_vault_data.get_yav)
  * [get\_yav\_one\_version](#metr_utils.configs.get_vault_data.get_yav_one_version)
  * [get\_all\_robot\_and\_personal\_secrets](#metr_utils.configs.get_vault_data.get_all_robot_and_personal_secrets)
  * [get\_db\_config](#metr_utils.configs.get_vault_data.get_db_config)
* [metr\_utils.configs.options](#metr_utils.configs.options)
  * [date\_type](#metr_utils.configs.options.date_type)
  * [datetime\_type](#metr_utils.configs.options.datetime_type)
  * [args](#metr_utils.configs.options.args)
* [metr\_utils.databases](#metr_utils.databases)
* [metr\_utils.databases.mongo\_db](#metr_utils.databases.mongo_db)
  * [get\_df](#metr_utils.databases.mongo_db.get_df)
* [metr\_utils.databases.psql\_db](#metr_utils.databases.psql_db)
  * [get\_df](#metr_utils.databases.psql_db.get_df)
* [metr\_utils.databases.solomon](#metr_utils.databases.solomon)
  * [push\_recs\_to\_solomon](#metr_utils.databases.solomon.push_recs_to_solomon)
  * [push\_raw\_df\_to\_solomon](#metr_utils.databases.solomon.push_raw_df_to_solomon)
  * [push\_df\_to\_solomon](#metr_utils.databases.solomon.push_df_to_solomon)
* [metr\_utils.databases.ydb\_db](#metr_utils.databases.ydb_db)
  * [get\_full\_table\_by\_index](#metr_utils.databases.ydb_db.get_full_table_by_index)
* [metr\_utils.databases.yt\_db](#metr_utils.databases.yt_db)
  * [create\_folder](#metr_utils.databases.yt_db.create_folder)
  * [write\_to\_yt](#metr_utils.databases.yt_db.write_to_yt)
* [metr\_utils.databases.chyt](#metr_utils.databases.chyt)
  * [get\_df](#metr_utils.databases.chyt.get_df)
  * [start\_clique](#metr_utils.databases.chyt.start_clique)
* [metr\_utils.databases.mysql\_db](#metr_utils.databases.mysql_db)
  * [get\_df](#metr_utils.databases.mysql_db.get_df)
* [metr\_utils.databases.wrappers](#metr_utils.databases.wrappers)
  * [DBDecorator](#metr_utils.databases.wrappers.DBDecorator)
* [metr\_utils.databases.clickhouse](#metr_utils.databases.clickhouse)
  * [http.client.\_MAXHEADERS](#metr_utils.databases.clickhouse.http.client._MAXHEADERS)
  * [get\_df](#metr_utils.databases.clickhouse.get_df)
  * [insert](#metr_utils.databases.clickhouse.insert)
  * [put\_data](#metr_utils.databases.clickhouse.put_data)
  * [create](#metr_utils.databases.clickhouse.create)
  * [drop](#metr_utils.databases.clickhouse.drop)
  * [multi\_requests](#metr_utils.databases.clickhouse.multi_requests)
  * [create\_and\_put\_df](#metr_utils.databases.clickhouse.create_and_put_df)
* [metr\_utils.databases.yql\_db](#metr_utils.databases.yql_db)
  * [get\_df](#metr_utils.databases.yql_db.get_df)
* [metr\_utils.test](#metr_utils.test)
* [metr\_utils.reports](#metr_utils.reports)
* [metr\_utils.reports.logs\_consistency\_utils](#metr_utils.reports.logs_consistency_utils)
* [metr\_utils.generate\_query](#metr_utils.generate_query)
  * [minute](#metr_utils.generate_query.minute)
  * [day](#metr_utils.generate_query.day)
  * [week](#metr_utils.generate_query.week)
  * [month](#metr_utils.generate_query.month)
  * [quarter](#metr_utils.generate_query.quarter)
  * [QueryFormatDecorator](#metr_utils.generate_query.QueryFormatDecorator)
  * [get\_query](#metr_utils.generate_query.get_query)
* [metr\_utils.pandas\_helpers](#metr_utils.pandas_helpers)
  * [full\_tsv](#metr_utils.pandas_helpers.full_tsv)
  * [add\_total\_rows](#metr_utils.pandas_helpers.add_total_rows)
  * [column\_division](#metr_utils.pandas_helpers.column_division)
  * [arr\_to\_tree](#metr_utils.pandas_helpers.arr_to_tree)
  * [share\_by\_key](#metr_utils.pandas_helpers.share_by_key)
  * [share\_by\_total\_row](#metr_utils.pandas_helpers.share_by_total_row)
  * [changing\_types](#metr_utils.pandas_helpers.changing_types)
  * [dataframe\_to\_wiki\_format](#metr_utils.pandas_helpers.dataframe_to_wiki_format)
  * [save\_to\_excel](#metr_utils.pandas_helpers.save_to_excel)
* [metr\_utils.plotly\_graphs](#metr_utils.plotly_graphs)
  * [clean\_filename](#metr_utils.plotly_graphs.clean_filename)
  * [put\_plot\_to\_jing](#metr_utils.plotly_graphs.put_plot_to_jing)
  * [base\_obj\_plot](#metr_utils.plotly_graphs.base_obj_plot)
  * [one\_df](#metr_utils.plotly_graphs.one_df)
  * [slices](#metr_utils.plotly_graphs.slices)
* [metr\_utils.blackbox](#metr_utils.blackbox)
  * [get\_tvm\_client](#metr_utils.blackbox.get_tvm_client)
  * [get\_bb\_info](#metr_utils.blackbox.get_bb_info)

<a id="metr_utils"></a>

# metr\_utils

<a id="metr_utils.configs"></a>

# metr\_utils.configs

<a id="metr_utils.configs.get_vault_data"></a>

# metr\_utils.configs.get\_vault\_data

<a id="metr_utils.configs.get_vault_data.get_bishop_config"></a>

#### get\_bishop\_config

```python
def get_bishop_config(config: str) -> str
```

Функция принимает на вход путь до конфига в бишопе и возвращает его содержимое

**Arguments**:

- `config` - адрес конфига в бишопе


**Returns**:

  содержиоме конфиго в строке (обычно там внутри json)

<a id="metr_utils.configs.get_vault_data.get_yav"></a>

#### get\_yav

```python
def get_yav(token: str = YAV_OAUTH) -> VaultClient
```

Функция получает инстаннс VaultClient по токену. Если токена нет, то попробует по ssh

**Arguments**:

- `token` - Токен oauth для yav


**Returns**:

  Инстанс VaultClient

<a id="metr_utils.configs.get_vault_data.get_yav_one_version"></a>

#### get\_yav\_one\_version

```python
def get_yav_one_version(version: str, token: str = YAV_OAUTH) -> dict
```

Функция полчает информацию из vault-а по id секрета или версии

**Arguments**:

- `version` - id секрета или версии
- `token` - токен oauth для vault


**Returns**:

  Содержимое секрета

<a id="metr_utils.configs.get_vault_data.get_all_robot_and_personal_secrets"></a>

#### get\_all\_robot\_and\_personal\_secrets

```python
def get_all_robot_and_personal_secrets(user: str = "robot-conv-main",
                                       token: str = YAV_OAUTH) -> dict
```

Получаем все пароли робота и личные секреты текущего юзера

**Arguments**:

- `user` - Юзер для которого нужно получить секреты
- `token` - токен oauth для vault


**Returns**:

  Все секреты робота, которые обогатили секретами текущего юзера. Для робота просто всего секреты

<a id="metr_utils.configs.get_vault_data.get_db_config"></a>

#### get\_db\_config

```python
def get_db_config(server_name: str,
                  db_type: str,
                  token: str = YAV_OAUTH) -> dict
```

Достаем конфиг из бишопа и для известного имени сервера достаем секрет с паролем, физический адрес, бд и порт
Тип бд указывает в каком конфиге искать

**Arguments**:

- `server_name` - ключ в конфиге, для которого достать информацию. короткое название сервера
- `db_type` - тип БД, он же тип конфига (ex. mysql, psql)
- `token` - токен oauth для vault


**Returns**:

  Словарь из конфига с информацией по серверу: секрет с паролем, бд, сервер, порт

<a id="metr_utils.configs.options"></a>

# metr\_utils.configs.options

<a id="metr_utils.configs.options.date_type"></a>

#### date\_type

```python
def date_type(s: str) -> str
```

Проверяем что дата в iso

**Arguments**:

- `s` - строка с датой


**Returns**:

  Та же самая строка, либо падает с ошибкой

<a id="metr_utils.configs.options.datetime_type"></a>

#### datetime\_type

```python
def datetime_type(s: str) -> str
```

Проверяем что дата-и-время в iso

**Arguments**:

- `s` - строка с датой


**Returns**:

  Та же самая строка, либо падает с ошибкой

<a id="metr_utils.configs.options.args"></a>

#### args

```python
def args(custom_args: Union[str, dict] = "",
         get_all_passes: bool = True,
         get_robot_passes: bool = False) -> argparse.Namespace
```

Функция разюираем параметры запуска

**Arguments**:

- `get_all_passes` - Получить вообще все пароли или только основные настройки
- `get_robot_passes` - получить пароли робота или личные. при ключенной настройке получаем доступ до тех секретов, до которых есть доступ у робота
- `custom_args` - параметры запуска строкой, будут распаршены как настоящие параметры запуска


**Returns**:

  Неймспейс с основными настройками и паролями

<a id="metr_utils.databases"></a>

# metr\_utils.databases

<a id="metr_utils.databases.mongo_db"></a>

# metr\_utils.databases.mongo\_db

<a id="metr_utils.databases.mongo_db.get_df"></a>

#### get\_df

```python
@DBDecorator
def get_df(query: dict,
           user: str = "",
           password: str = "",
           host: str = "",
           database: str = "",
           collection: str = "",
           port: int = 27018,
           raw: bool = False) -> Union[pd.DataFrame, list]
```

Коннектор к MongoDB

**Arguments**:

- `query` - Запрос
- `user` - Юзер в mongodb
- `password` - Пароль для юзера
- `host` - Хост
- `database` - База данных
- `collection` - Коллеция
- `port` - Порт для хоста
- `header` - Добавить заголовок, имеет смысл только для сырых данных
- `raw` - Вернуть сырую таблицу в json (list of dicts) вместо DF


**Returns**:

  Результат в DF

<a id="metr_utils.databases.psql_db"></a>

# metr\_utils.databases.psql\_db

<a id="metr_utils.databases.psql_db.get_df"></a>

#### get\_df

```python
@DBDecorator
def get_df(query: str,
           user: str = "",
           password: str = "",
           host: str = "",
           database: str = "",
           port: Union[str, int] = 6432,
           header: bool = True,
           raw: bool = False) -> Union[pd.DataFrame, str]
```

Простенькая функция для postgresql

**Arguments**:

- `query` - Запрос
- `user` - Юзер в postgresql
- `password` - Пароль для юзера
- `host` - Хост
- `database` - База данных
- `port` - Порт для хоста
- `header` - Добавить заголовок, имеет смысл только для сырых данных
- `raw` - Вернуть сырую таблицу в строке (по дефолту TSV) вместо DF


**Returns**:

  Результат в DF

<a id="metr_utils.databases.solomon"></a>

# metr\_utils.databases.solomon

<a id="metr_utils.databases.solomon.push_recs_to_solomon"></a>

#### push\_recs\_to\_solomon

```python
def push_recs_to_solomon(solomon_recs: list,
                         token: str,
                         cluster: str,
                         service: str = "metrika",
                         project: str = "metrika_analytics") -> None
```

Простая функция, которая пушит данные в заданный срез Solomon

**Arguments**:

- `solomon_recs` - массив записей вида {'labels': <cловарь c dimensions>, 'ts': <timestamp>, 'value': <значение сенсора>}
- `token` - oauth токен Solomon
- `cluster` - cluster в Solomon
- `service` - service в Solomon
- `project` - project в Solomon


**Returns**:

  Загруженные данные в Solomon

<a id="metr_utils.databases.solomon.push_raw_df_to_solomon"></a>

#### push\_raw\_df\_to\_solomon

```python
def push_raw_df_to_solomon(df: pd.DataFrame,
                           sensor: str,
                           token: str,
                           cluster: str,
                           service: str = "metrika",
                           project: str = "metrika_analytics") -> None
```

Функция, которые отправляет данные в виде dataframe в заданный срез Solomon

**Arguments**:

- `df` - DF с данными, ожидается, что у него будут колонки: value - значение показателя, fielddate - время, все остальные колонки попадут в dimensions
- `sensor` - sensor в Solomon
- `token` - oauth токен Solomon
- `cluster` - cluster в Solomon
- `service` - service в Solomon
- `project` - project в Solomon


**Returns**:

  Загруженные данные в Solomon

<a id="metr_utils.databases.solomon.push_df_to_solomon"></a>

#### push\_df\_to\_solomon

```python
def push_df_to_solomon(df: pd.DataFrame,
                       sensors: list,
                       token: str,
                       cluster: str,
                       service: str = "metrika",
                       project: str = "metrika_analytics",
                       lim_dimensions: int = 100) -> None
```

Функция, которые отправляет данные в виде dataframe в заданный срез Solomon

**Arguments**:

- `df` - DF с данными, ожидается, что у него будет колонка fielddate - время и передается список метрик sensors, все остальные колонки попадут в dimensions
- `sensor` - список sensor которые должны быть отчете в Solomon
- `token` - oauth токен Solomon
- `cluster` - cluster в Solomon
- `service` - service в Solomon
- `project` - project в Solomon
- `lim_dimensions` - Лимит для проверки того, что слишком много дименшенов


**Returns**:

  Загруженные данные в Solomon

<a id="metr_utils.databases.ydb_db"></a>

# metr\_utils.databases.ydb\_db

<a id="metr_utils.databases.ydb_db.get_full_table_by_index"></a>

#### get\_full\_table\_by\_index

```python
def get_full_table_by_index(host: str,
                            database: str,
                            table_name: str,
                            token: str,
                            index_fields_name: list,
                            index_fields_types: list,
                            limit: int = 500,
                            debug: bool = False) -> pd.DataFrame
```

Например, запускать так:
df_1 = ydb_db.get_full_table_by_index(host='ydb-ru.yandex.net:2135',
                           database='/ru/metrika/production/cdp',
                           table_name='segments_data/segments',
                           token=YQL_TOKEN,
                           index_fields_name=['counter_id','segment_id','version'],
                           index_fields_types=['Uint32', 'Uint64', 'Uint64'],
                           limit=500,
                           debug=True)

<a id="metr_utils.databases.yt_db"></a>

# metr\_utils.databases.yt\_db

<a id="metr_utils.databases.yt_db.create_folder"></a>

#### create\_folder

```python
def create_folder(path: str, cluster: str = DEFAULT_CLASTER) -> None
```

Фуункция создает папку на YT

**Arguments**:

- `path` - Путь для новой папки
- `cluster` - Кластер YT


**Returns**:

  Созданная папка на YT

<a id="metr_utils.databases.yt_db.write_to_yt"></a>

#### write\_to\_yt

```python
def write_to_yt(path: str,
                df: pd.DataFrame,
                schema: dict = None,
                append: bool = False,
                cluster: str = DEFAULT_CLASTER,
                portion_size: int = DEFAULT_PORTION_SIZE,
                portion_offset: int = 0) -> None
```

Запрос для вставки данных в YT через python-клиент

**Arguments**:

- `path` - Путь для вставки. формат //my/path/to/table
- `df` - DF для вставки
- `schema` - Схема данных в формате {'field': 'type'}. Далее все поля будут преведени к типам из схемы и null заменяться на пустые значения.
  Ожидаются типы YT. Если схемы нет, то будем считать что загружаем весь df по типам, которые там опредлены
- `append` - Дополнить таблицу или создать новую
- `cluster` - Кластер, где находится таблица
- `portion_size` - Размер одной пачки для вставки
- `portion_offset` - Сколько пачек пропустить (если поставка сорвалась)


**Returns**:

  Таблица на YT

<a id="metr_utils.databases.chyt"></a>

# metr\_utils.databases.chyt

<a id="metr_utils.databases.chyt.get_df"></a>

#### get\_df

```python
def get_df(query: str,
           cluster: str = "hahn",
           clique: str = "*metrica_analytics") -> pd.DataFrame
```

Функция делает запрос в CHYT

**Arguments**:

- `query` - Запрос
- `cluster` - Кластер YT
- `clique` - Клика CHYT


**Returns**:

  DF с результатом

<a id="metr_utils.databases.chyt.start_clique"></a>

#### start\_clique

```python
def start_clique(cluster: str = 'hahn') -> None
```

Функция стартует клику

**Arguments**:

  cluster - кластер YT


**Returns**:

  Запущенная клика

<a id="metr_utils.databases.mysql_db"></a>

# metr\_utils.databases.mysql\_db

<a id="metr_utils.databases.mysql_db.get_df"></a>

#### get\_df

```python
@DBDecorator
def get_df(query: str,
           user: str = "",
           password: str = "",
           host: str = MYSQL_DEFAULT_HOST,
           database: str = MYSQL_DEFAULT_DB,
           port: Union[str, int] = 3309,
           header: bool = True,
           raw: bool = False) -> Union[pd.DataFrame, str]
```

Простенькая функция для mysql

**Arguments**:

- `query` - Запрос
- `user` - Юзер в mysql
- `password` - Пароль для юзера
- `host` - Хост
- `database` - База данных
- `port` - Порт для хоста
- `header` - Добавить заголовок, имеет смысл только для сырых данных
- `raw` - Вернуть сырую таблицу в строке (по дефолту TSV) вместо DF


**Returns**:

  Результат в DF

<a id="metr_utils.databases.wrappers"></a>

# metr\_utils.databases.wrappers

<a id="metr_utils.databases.wrappers.DBDecorator"></a>

## DBDecorator Objects

```python
class DBDecorator()
```

Обертка подставляет дефолтные пароли и дополнительно не дает выполнять запросы из-под default

<a id="metr_utils.databases.clickhouse"></a>

# metr\_utils.databases.clickhouse

<a id="metr_utils.databases.clickhouse.http.client._MAXHEADERS"></a>

#### http.client.\_MAXHEADERS

Спрашиваем кликхаус и получаем ответ. А еще можно спрашивать много хостов одновремнно

<a id="metr_utils.databases.clickhouse.get_df"></a>

#### get\_df

```python
@DBDecorator
def get_df(query: str,
           host: str = DEFAULT_HOST,
           override_default: bool = False,
           user: str = "default",
           password: str = "",
           stream: bool = False,
           out_queue: queue.Queue = None,
           raw: bool = False,
           data: Union[str, bytes] = "",
           files: dict = None,
           **kwargs) -> Union[pd.DataFrame, str, iter, None]
```

Запрос в CH через http-клиент

**Arguments**:

- `query` - Запрос
- `host` - Хост в формате http://hostname:8123/
- `override_default` - Принудительно выполнить из-под default
- `user` - Юзер в CH
- `password` - Пароль для юзера
- `stream` - Вернуть вместо DF поток байтов. Нужно для запросов, которые возвращают много данных
- `out_queue` - Очередь для multi_process
- `raw` - Вернуть сырую таблицу в строке (по дефолту TSV) вместо DF
- `data` - данные, которые будут загружены
- `files` - dict с внешними файлами

  Формат файла: {'filename':
  {
- `'structure'` - structure of file,
- `'buffer'` - buffer-like object file
  }
  }
- `**kwargs` - предполагается, что здесь будут опции CH для запороса


**Returns**:

  Результат в DF. Если запрос возвращает пустоту, то будет None

<a id="metr_utils.databases.clickhouse.insert"></a>

#### insert

```python
@DBDecorator
def insert(table: str,
           data: Union[str, bytes, pd.DataFrame],
           format: str = "TSVWithNames",
           host: str = DEFAULT_HOST,
           override_default: bool = False,
           user: str = "default",
           password: str = "",
           **kwargs) -> Union[str, None]
```

Запрос для вставки данных в CH через http-клиент

**Arguments**:

- `table` - Таблица для вставки
- `data` - данные, которые будут загружены
- `format` - В каком формате данные. По дефолту TSVWithNames
- `host` - Хост в формате http://hostname:8123/
- `override_default` - Принудительно выполнить из-под default
- `user` - Юзер в CH
- `password` - Пароль для юзера
- `**kwargs` - предполагается, что здесь будут опции CH для запороса


**Returns**:

  В случае успеха будет None

<a id="metr_utils.databases.clickhouse.put_data"></a>

#### put\_data

```python
@DBDecorator
def put_data(query: str,
             host: str = DEFAULT_HOST,
             override_default: bool = False,
             user: str = "default",
             password: str = "",
             data: Union[str, bytes] = "",
             **kwargs) -> Union[str, None]
```

Запрос для вставки данных в CH через http-клиент

**Arguments**:

- `query` - Запрос
- `host` - Хост в формате http://hostname:8123/
- `override_default` - Принудительно выполнить из-под default
- `user` - Юзер в CH
- `password` - Пароль для юзера
- `data` - данные, которые будут загружены
- `**kwargs` - предполагается, что здесь будут опции CH для запороса


**Returns**:

  В случае успеха будет None

<a id="metr_utils.databases.clickhouse.create"></a>

#### create

```python
@DBDecorator
def create(create_type: str,
           name: str,
           schema: str = "",
           engine: str = "Log",
           host: str = DEFAULT_HOST,
           override_default: bool = False,
           user: str = "default",
           password: str = "",
           **kwargs) -> Union[str, None]
```

Запрос для соаздания таблицы или БД в CH через http-клиент

**Arguments**:

- `create_type` - Что создать: table или database
- `name` - Название создаваемой таблицы или бд
- `schema` - Схема для таблицы
- `engine` - Движок для таблицы
- `host` - Хост в формате http://hostname:8123/
- `override_default` - Принудительно выполнить из-под default
- `user` - Юзер в CH
- `password` - Пароль для юзера
- `data` - данные, которые будут загружены
- `**kwargs` - предполагается, что здесь будут опции CH для запороса


**Returns**:

  В случае успеха будет None

<a id="metr_utils.databases.clickhouse.drop"></a>

#### drop

```python
@DBDecorator
def drop(drop_type: str,
         name: str,
         host: str = DEFAULT_HOST,
         override_default: bool = False,
         user: str = "default",
         password: str = "",
         **kwargs) -> Union[str, None]
```

Запрос для удаления таблицы или БД в CH через http-клиент

**Arguments**:

- `drop_type` - Что удалить: table или database
- `name` - Название удаляемой таблицы или бд
- `host` - Хост в формате http://hostname:8123/
- `override_default` - Принудительно выполнить из-под default
- `user` - Юзер в CH
- `password` - Пароль для юзера
- `data` - данные, которые будут загружены
- `**kwargs` - предполагается, что здесь будут опции CH для запороса


**Returns**:

  В случае успеха будет None

<a id="metr_utils.databases.clickhouse.multi_requests"></a>

#### multi\_requests

```python
@DBDecorator
def multi_requests(query: str,
                   cluster: str = "mtgiga_all",
                   replica: int = 3,
                   user: str = "default",
                   password: str = "",
                   files: dict = None,
                   join_key: str = None,
                   **kwargs) -> pd.DataFrame
```

Спришивает все хосты CH одновременно

**Arguments**:

- `query` - Запрос
- `cluster` - В какой кластер будет запрос, как задан в таблице system.clusters
- `replica` - Номер реплики для кластера
- `user` - Юзер в CH
- `password` - Пароль для юзера
- `files` - dict с внешними фалйами
- `join_key` - По каком ключу смержить таблицы в финальный результат
- `**kwargs` - предполагается, что здесь будут опции CH для запороса


**Returns**:

  Результат в DF. Если запрос возвращает пустоту, то будет None

<a id="metr_utils.databases.clickhouse.create_and_put_df"></a>

#### create\_and\_put\_df

```python
@DBDecorator
def create_and_put_df(table: str,
                      df: pd.DataFrame,
                      schema: str,
                      engine: str = "Log",
                      host: str = DEFAULT_HOST,
                      override_default: bool = False,
                      user: str = "default",
                      password: str = "",
                      **kwargs) -> None
```

Функция создает таблицу и пишет в нее DF

**Arguments**:

- `table` - Имя таблица
- `df` - DF c данными
- `schema` - Поля с типами для create table
- `engine` - Движок для таблицы
- `host` - Хост в формате http://hostname:8123/
- `override_default` - Принудительно выполнить из-под default
- `user` - Юзер в CH
- `password` - Пароль для юзера
- `**kwargs` - предполагается, что здесь будут опции CH для запороса


**Returns**:

  Результат в DF. Если запрос возвращает пустоту, то будет None

<a id="metr_utils.databases.yql_db"></a>

# metr\_utils.databases.yql\_db

<a id="metr_utils.databases.yql_db.get_df"></a>

#### get\_df

```python
@DBDecorator
def get_df(query: str,
           token: str = "",
           cluster: str = DEFAULT_CLUSTER,
           add_default_header: bool = True,
           attach_urls: dict = None) -> pd.DataFrame
```

Функция ходит в YQL и получает на выходе DF

**Arguments**:

- `query` - запрос в YQL
- `token` - auth токен в YQL
- `cluster` - кластеер выполнения; use <cluster>
- `add_default_header` - добавить дефолтный хэдер к запросу
- `attach_urls` - добавить ссылки на sql файлы


**Returns**:

  DF с результатом запроса

<a id="metr_utils.test"></a>

# metr\_utils.test

<a id="metr_utils.reports"></a>

# metr\_utils.reports

<a id="metr_utils.reports.logs_consistency_utils"></a>

# metr\_utils.reports.logs\_consistency\_utils

<a id="metr_utils.generate_query"></a>

# metr\_utils.generate\_query

<a id="metr_utils.generate_query.minute"></a>

#### minute

```python
def minute(query_time: str, shift: int = -1, minute_count: int = 1) -> tuple
```

Функция получает начало и конец периода, с окгрлением до минут

**Arguments**:

- `query_time` - Какая дата была задана в запросе
- `shift` - На сколько периодов сместиться
- `minute_count` - Длина периода в минутах


**Returns**:

  Даты начала и конца периода, даты-и-время начала и конца периода

<a id="metr_utils.generate_query.day"></a>

#### day

```python
def day(query_date: str, shift: int = -1) -> tuple
```

Функция получает начало и конец периода, для дневных отчетов. Это одна и та же дата

**Arguments**:

- `query_date` - Какая дата была задана в запросе
- `shift` - На сколько периодов сместиться


**Returns**:

  Даты начала и конца периода. Для дневных отчетов это одна и та же дата

<a id="metr_utils.generate_query.week"></a>

#### week

```python
def week(query_date: str, shift: int = -1) -> tuple
```

Функция получает начало и конец недели, для еженедельных отчетов.
Считается для той недели, в которую папала query_date

**Arguments**:

- `query_date` - Какая дата была задана в запросе
- `shift` - На сколько периодов сместиться


**Returns**:

  Даты начала и конца недели

<a id="metr_utils.generate_query.month"></a>

#### month

```python
def month(query_date: str, shift: int = -1) -> tuple
```

Функция получает начало и конец месяца, для ежемесячных отчетов.
Считается для того месяца, в которую папала query_date

**Arguments**:

- `query_date` - Какая дата была задана в запросе
- `shift` - На сколько периодов сместиться


**Returns**:

  Даты начала и конца месяца

<a id="metr_utils.generate_query.quarter"></a>

#### quarter

```python
def quarter(query_date: str, shift: int = -1) -> tuple
```

Функция получает начало и конец квартала, для ежеквартальных отчетов.
Считается для того квартала, в которую папала query_date

**Arguments**:

- `query_date` - Какая дата была задана в запросе
- `shift` - На сколько периодов сместиться


**Returns**:

  Даты начала и конца квартала

<a id="metr_utils.generate_query.QueryFormatDecorator"></a>

## QueryFormatDecorator Objects

```python
class QueryFormatDecorator()
```

Обертка для форматирования запроса дефолтными параметрами

<a id="metr_utils.generate_query.get_query"></a>

#### get\_query

```python
@QueryFormatDecorator
def get_query(query: str,
              scale: str = "",
              query_date: str = "",
              shift: int = 0,
              query_time: str = None,
              sample: int = 0,
              parent_yt_tables: Union[list, str] = "",
              format_dict: dict = None) -> str
```

Функция, которая форматирует запрос

**Arguments**:

- `query` - Запрос
- `scale` - Временной интервал для расчета
- `query_date` - Дата за которую будет считаться запрос
- `shift` - На сколько периодов сместиться
- `query_time` - Дата-и-время за которую будет считаться запрос
- `sample` - Семпл
- `parent_yt_tables` - Таблицы на YT от родительского скрипта. Также можно передать произваольный набор таблиц
- `format_dict` - dict для форматирования других секций запроса


**Returns**:

  Отформатированный запрос

<a id="metr_utils.pandas_helpers"></a>

# metr\_utils.pandas\_helpers

<a id="metr_utils.pandas_helpers.full_tsv"></a>

#### full\_tsv

```python
def full_tsv(data: pd.DataFrame,
             key: Union[str, list],
             agg_type: str = "sum") -> pd.DataFrame
```

Группируем DF по ключам и считаем аггрегацию для остальных
Используется для финального DF после запрос по слоям

**Arguments**:

- `data` - DF
- `key` - Ключи по которым, будем группировать
- `agg_type` - тип аггрегации, пока поддержанны sum и max


**Returns**:

  Сгруппированный DF

<a id="metr_utils.pandas_helpers.add_total_rows"></a>

#### add\_total\_rows

```python
def add_total_rows(data: pd.DataFrame,
                   key: Union[str, list],
                   field_for_total: str,
                   total_name: str = "Total",
                   only_total_rows: bool = False) -> pd.DataFrame
```

Добавляет в качестве строк сгруппированные значения по key. Все значения field_for_total заменяются на Total

**Arguments**:

- `data` - DF
- `key` - По каким ключам сгруппировать DF. При группировке все остальные столбцы будут просуммированы
- `field_for_total` - Для какого поля посчитать Total
- `total_name` - Какое назваие будет для Total значений
- `only_total_rows` - Если включен этот флаг, то вернутся только новые поля, иначе полный DF с новыми строками Total


**Returns**:

  DF с новыми строками Total

<a id="metr_utils.pandas_helpers.column_division"></a>

#### column\_division

```python
def column_division(data: pd.DataFrame,
                    dividend: str,
                    divider: str,
                    result_name: str,
                    delta: bool = False,
                    full_division: bool = False) -> pd.DataFrame
```

Очень кастомная функция для деления колонок

**Arguments**:

- `data` - DF
- `dividend` - Колонка с делимым
- `divider` - Колонка с делителем
- `result_name` - Как назвать колонку с результатом
- `delta` - Считаем (dividend-divider)/divider
- `full_division` - Считаем dividend/(divider-dividend)


**Returns**:

  Исходный DF, дополненный новой колонкой - результатом деления

<a id="metr_utils.pandas_helpers.arr_to_tree"></a>

#### arr\_to\_tree

```python
def arr_to_tree(data: pd.DataFrame, column: str = "region") -> pd.DataFrame
```

Переводит массив CH в дерево stat

**Arguments**:

- `data` - DF
- `column` - В какой колонке находится массив, который будет переведен в дерево


**Returns**:

  Исходный DF в котором заменили массив на дерево стата

<a id="metr_utils.pandas_helpers.share_by_key"></a>

#### share\_by\_key

```python
def share_by_key(data: pd.DataFrame, key: Union[str, list], share_columnm: str,
                 result_name: str) -> pd.DataFrame
```

Вычисляет проценты для заданной колонки

**Arguments**:

- `data` - DF
- `key` - По каким колонкам сгруппровать
- `share_columnm` - Для какой колонки посчитать долю
- `result_name` - Название для колонки с результатом


**Returns**:

  Исходный DF в который добавлена колонка с долей для заданой метрики

<a id="metr_utils.pandas_helpers.share_by_total_row"></a>

#### share\_by\_total\_row

```python
def share_by_total_row(data: pd.DataFrame,
                       total_key: str,
                       share_columns: Union[str, list],
                       drop_total: bool = False,
                       total_name: str = "Total") -> pd.DataFrame
```

Вычисляет проценты для заданной колонки. При этом сумма уже там есть

**Arguments**:

- `data` - DF
- `total_key` - В какой колонке есть Total
- `share_columns` - Для каких колонок посчитать долю
- `drop_total` - Оставить строку с Total
- `total_name` - Как назвать новую колонку с долей


**Returns**:

  Исходный DF в который добавлена колонка с долей для заданой метрики

<a id="metr_utils.pandas_helpers.changing_types"></a>

#### changing\_types

```python
def changing_types(data: pd.DataFrame, int_keys: Union[str, list],
                   float_keys: Union[str, list],
                   string_keys: Union[str, list]) -> pd.DataFrame
```

Приводит числовые и строговые типы после map (для python 3)

**Arguments**:

- `data` - DF
- `int_keys` - список колонок с int
- `float_keys` - список колонок с float
- `string_keys` - список колонок с str


**Returns**:

  DF с привиденными типами

<a id="metr_utils.pandas_helpers.dataframe_to_wiki_format"></a>

#### dataframe\_to\_wiki\_format

```python
def dataframe_to_wiki_format(
        data: pd.DataFrame,
        show_index: bool = False,
        return_template: bool = False) -> Union[None, str]
```

Распечатывает dataframe в формате для вставки на wiki

**Arguments**:

- `data` - DF
- `show_index` - Показывать индекс в финальной таблице
- `return_template` - Вернуть таблицу в переменную или просто распечатать


<a id="metr_utils.pandas_helpers.save_to_excel"></a>

#### save\_to\_excel

```python
def save_to_excel(data: pd.DataFrame,
                  filename: str,
                  index: bool = False,
                  header: bool = True) -> None
```

Сохраняет датафрейм в excel

**Arguments**:

- `df` - Датафрейм
- `filename` - Название файла, куда созранить (ожидается расширегие .xlsx)
- `index` - Писать индекс в файл
- `header` - Писать заголовок в файл


**Returns**:

  Сохраненный файл на диске

<a id="metr_utils.plotly_graphs"></a>

# metr\_utils.plotly\_graphs

<a id="metr_utils.plotly_graphs.clean_filename"></a>

#### clean\_filename

```python
def clean_filename(filename: str,
                   whitelist: str = VALID_FILENAME_CHARS,
                   replace: str = " ")
```

Let any string or unicode string be an filename.

**Arguments**:

- `filename` - Название файла
- `whitelist` - Список разрешенных символов
- `replace` - Какие символы заменить на underscore


**Returns**:

  Корректное имя для загрузки файла

<a id="metr_utils.plotly_graphs.put_plot_to_jing"></a>

#### put\_plot\_to\_jing

```python
def put_plot_to_jing(html_plot: bytes,
                     login: str = "",
                     title: str = "") -> str
```

Put string from html_plot to jing servers as .html file and return link on it

**Arguments**:

- `html_plot` - html с графиком
- `login` - аккаунт в jing
- `title` - название файла


**Returns**:

  Загружает график на jing и возвращает ссылку на файл

<a id="metr_utils.plotly_graphs.base_obj_plot"></a>

#### base\_obj\_plot

```python
def base_obj_plot(plot_obj: dict,
                  title: str = "",
                  get_html: bool = False,
                  upload_to_jing: bool = False)
```

Функция для обрвывода графика. Либо as is, либо html, либо загрузка в jing, в зависимости от флагов

**Arguments**:

- `plot_obj` - dict с data и layout в формате plotly
- `title` - Тайтл графика
- `get_html` - Вернуть html код
- `upload_to_jing` - Загрузить график на jing


**Returns**:

  Выводит график, либо html с графиком, либо загружает на jing и отдает ссылку на него

<a id="metr_utils.plotly_graphs.one_df"></a>

#### one\_df

```python
def one_df(df: pd.DataFrame,
           title: str = "",
           yaxis_hoverformat: str = ".4s",
           xaxis_hoverformat: str = "",
           xaxis_add_time: bool = False,
           get_html: bool = False,
           upload_to_jing: bool = False) -> callable
```

Simple plotly lines. Expected DF with x as index (ex. time) and all lines as colums

**Arguments**:

- `df` - DF с данными. Ожидается что в индексе будут значения x, а в колонках значения для y
- `title` - Тайтл графика
- `yaxis_hoverformat` - Формат чисел оси Y для ховера
- `xaxis_hoverformat` - Формат оси Х для ховера
- `xaxis_add_time` - Добавить к дате время для оси X
- `get_html` - Вернуть html код
- `upload_to_jing` - Загрузить график на jing


**Returns**:

  Выводит график, либо html с графиком, либо загружает на jing и отдает ссылку на него

<a id="metr_utils.plotly_graphs.slices"></a>

#### slices

```python
def slices(slices: list,
           title: str = "",
           yaxis_hoverformat: str = ".4s",
           xaxis_hoverformat: str = "",
           xaxis_add_time: bool = False,
           get_html: bool = False,
           upload_to_jing: bool = False) -> callable
```

Plotly graphs with select. Expected dict with DFs. Each key - value in select.
Each DF with x as index (ex. time) and all lines as colums

**Arguments**:

- `slices` - list с DF, которые будут нарисованы на отдельных вкладках
- `title` - Тайтл графика
- `yaxis_hoverformat` - Формат чисел оси Y для ховера
- `xaxis_hoverformat` - Формат оси Х для ховера
- `xaxis_add_time` - Добавить к дате время для оси X
- `get_html` - Вернуть html код
- `upload_to_jing` - Загрузить график на jing


**Returns**:

  Выводит график, либо html с графиком, либо загружает на jing и отдает ссылку на него

<a id="metr_utils.blackbox"></a>

# metr\_utils.blackbox

<a id="metr_utils.blackbox.get_tvm_client"></a>

#### get\_tvm\_client

```python
def get_tvm_client(secret: str = "",
                   client_id: int = CLIENT_ID,
                   destinations: dict = None) -> tvmauth.TvmClient
```

Функция генерит TVM клиент с заданными настройками

**Arguments**:

- `secret` - TVM секрет приложения
- `client_id` - ID своего приложения, которое будет ходить с TVM в удаленный сервис
- `destinations` - Словарь {alias_name: service_id}, куда приложение будет ходить.


**Returns**:

  Инстанс клиента TVM

<a id="metr_utils.blackbox.get_bb_info"></a>

#### get\_bb\_info

```python
def get_bb_info(uid_list: Union[list, str],
                tvm: tvmauth.TvmClient = None) -> list
```

Принимает на вход список uid и tmv клиент. Возвращает в массиве информацию по этому списку

**Arguments**:

- `uid_list` - список или лист с uid
- `tvm` - инстанс клиента TVM


**Returns**:

  Ответ blackbox по каждому uid из списка 
