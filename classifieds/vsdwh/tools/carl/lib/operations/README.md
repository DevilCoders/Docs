# Библиотека операций `carl`

В этой директории содержится реализованная библиотека операций для `carl`.

Структура:
```
operations/                                            # общая библиотека операций
|- basic/                                              # базовые операции
|  |- projects/                                        # самописные операции команд, выполняющие какие-то узкоспециализированные задачи, не предназначенные для широкого использования
|  |  |- vertis_dwh/
|  |  |  |- __init__.py
|  |  |  |- some_vertis_dwh_operations_structure
|  |  |- some_other_project_1/
|  |  |- some_other_project_2/
|  |
|  |- services/                                        # операции, работающие с конкретными внутренними/внешними сервисами, например, операции для работы с ClickHouse, PostgreSQL, YT, YQL и т.п.
|  |  |- __init__.py
|  |  |- ch.py
|  |  |- yt.py
|  |  |- yql.py
|  |  |- some_service_ops.py
|  |
|  |- util/                                             # утилитные операции, операции, не работающие ни с какими конкретными сервисами, и прочие многофункциональные кубики
|  |  |- __init__.py
|  |  |- py_ops.py
|  |  |- shell.py
|  |  |- some_util_ops.py
|
|- composite/                                           # композитные операции
|  |- projects/                                         # предполагается хранение только внутри проектных директорий команд, так как композитные операции обычно очень специфичные и узкоориентированные
|  |  |- ...
|
|- subgraph/                                            # подграфы
|  |- projects/                                         # хранение аналогично композитным операциям
|  |  |- ...
```

## Правила доработки библиотеки операций

**Важно:** любые доработки библиотеки операций/пресетов/ресурсов и проч. требуют пересборки `carl` в [bin](../../bin) (и пересоздания симлинка, если он использовался) для того, чтобы можно было пользоваться изменениями при деплое графов.


**Важно:** все ресурсы и источники для операций добавляются только в локальный [ya.make](./ya.make).

### Общая информация
В библиотеку можно добавлять любые Nirvana-операции, однако, помимо распределения операций по соответствующим пакетам следует обратить внимание на следующие моменты:
1. При объявлении функции операции в декораторе `@vh3.decorator.external_operation` лучше указывать ссылку на операцию, а не её id.
2. Не стоит добавлять операции, дублирующие уже реализованные.
3. Если есть несколько операций, выполняющих примерно одно и то же, стоит предпочесть для реализации ту, которая находится в [библиотеке Nirvana](https://nirvana.yandex-team.ru/browse?selected=879274).
4. Не стоит добавлять deprecated-операции.
5. Не обязательно прописывать все опции кубиков в аргументы vh3-операций, можно внести только самые ходовые.
6. Недостающие опции кубиков можно внести в аргументы существующих vh3-операций, но при этом важно не сломать обратную совместимость. Всегда добавляйте дефолтное значение аргумента при добавлении новых опций.

Первые три пункта носят скорее рекомендательный характер, исключения допускаются. Например, [MR Read TSV
](https://nirvana.yandex-team.ru/operation/d23ec268-5a94-42f9-bd6b-5062dccbd3f5) и [MR read TSV parallel tmpfs unordered](https://nirvana.yandex-team.ru/operation/7f57bd48-d6bf-4074-b049-fb29f954c91e) делают одно и то же, но для выгрузки больших файлов вторая лучше подходит. Случаи, когда небиблиотечная операция функциональнее той, что в [библиотеке Nirvana](https://nirvana.yandex-team.ru/browse?selected=879274), также остаются на усмотрение реализующего.

При реализации операций также не стоит забывать, что `carl` во время работы хранит в объекте [GLOBAL_OPTIONS](https://a.yandex-team.ru/arc_vcs/classifieds/vsdwh/tools/carl/lib/config/__init__.py#L9) добавленные на граф глобальные операции и умеет подставлять их в операцию в качестве дефолтных значений опций. Посмотреть, как объявить операцию, которая будет так работать, можно на примере реализации [YQL 4](https://a.yandex-team.ru/arc_vcs/classifieds/vsdwh/tools/carl/lib/operations/basic/services/yql.py#L26), где большинство опций по умолчанию "примагнитится" к соответствующей глобальной опции графа. На данный момент такая функция реализована во многих операциях, поэтому далее при добавлении новых vh3-операций стоит поддерживать единообразие в именовании глобальных опций и использовании их в качестве дефолтных значений для операций.

Используемые названия глобальных опций:
```
# опции для кубиков ClickHouse
ch_host
ch_port
ch_user
ch_password

# опции для кубиков PostgreSQL
pg_host
pg_port
pg_user
pg_password

# опции для YT/YQL/MR кубиков
mr_account
yt_pool
yt_token
yql_token

# опции прочих кубиков
abc_token
arcanum_token
juggler_token
mdb_token
nirvana_token
sandbox_task_owner
sandbox_token
solomon_token
startrek_token
statface_token
wiki_token
```
При заведении новых vh3-операций в качестве дефолтных значений таких основных опций следует использовать перечисленные названия и добавлять их в глобальные опции графа при описании графа carl-кодом или через ресурсы своего проекта. Другие варианты названий для перечисленных сущностей будут отсеиваться на ревью PR. Для новых сущностей лучше выбирать более лаконичные названия в таком же ключе.

В [examples](examples) есть примеры добавления глобальных опций в граф явно или через [ресурсы](resources). Если vh3-операция создана правильно, то при наличии в графе соответствующих опций, их проставление произойдёт автоматически, что сделает описание графа лаконичнее. Например, при наличии нужных токенов в глобальных опциях, добавление на граф кубика [YQL 4](https://a.yandex-team.ru/arc_vcs/classifieds/vsdwh/tools/carl/lib/operations/basic/services/yql.py#L26) будет выглядеть максимально просто:

```python
yql_4_select = yql_4(request="SELECT * FROM hahn.`some/table/path`;")
```



### [basic](basic)

Директория для хранения базовых операций.
Внутренняя иерархия:
* projects/ — директория для базовых операций, специфичных для каких-то команд. Если существует сделанная для себя операция, которая полезна только вашей команде и не предполагает широкого использования, то следует поместить её внутрь projects в структуру операций внутри поддиректории вашего проекта.
* services/ — директория для базовых операций, взаиможействующих с конкретными внешними или внутренними сервисами. Каждый `.py` файл содержит в себе операции, предназначенными для работы с одним сервисом. Это должны быть общие операции, допустимые для переиспользования всеми пользователями `carl` аналогично [services библиотеки операций Nirvana](https://nirvana.yandex-team.ru/browse?selected=889784) (но не обязательно с именно такой же структурой). Здесь особенно важно по возможности указывать в дефолтных значениях vh3-операций глобальные опции графа, как описано выше, потому как предполагается массовое использование этих операций.
* util/ — директория для базовых операций, которые не взаимодействуют ни с какими конкретными сервисами. Сюда, например, попадают операции, имитирующие bash-команды, операции для взаимодействия с Git и Аркадией, операции для исполнения Python-кода и т.п. Если операций какого-то типа становится достаточно много, нужно выделять их в отдельный модуль, для единичных операций сделан общий модуль [util.py](basic/util/util.py).

**Важно!** [services](basic/services), [util](basic/util) и все проектные поддиректории в [projects](basic/projects) должны содержать в себе `__init__.py`, в котором должны быть сделаны импорты всех операций, определённых в этом пакете.  Это сделано, чтобы чуть-чуть упростить импорты в коде описания графов, а также сохранить обратную совместимость при каких-то возможных передвижениях операций внутри пакетов. Это налагает требования к уникальности имён определяемых внутри одного пакета vh3-операций, а также к тому, что все новые определённые операции должны явно импортироваться из соответствующего модуля в `__init__.py` пакета и быть записанными в свою группу в `__all__`.


### [composite](composite)
Директория для хранения композитных операций Nirvana.

На данный момент предполагается только внутреннее деление на проекты с требованиями по описанию новых операций аналогичными basic, потому что зачастую композитные операции выполняют какие-то специфические задачи отдельных команд. Если в будущем в библиотеке понядобится добавить общедоступные и переиспользуемые разными командами композитные операции, существующая структура может быть пересмотрена, и могут появиться новые поддиректории (например, util, ml и т.п.). Требования к описанию операций, привязке глобальных опций и `__init__.py` на уровне проектов здесь такие же, как в basic.


### [subgraph](subgraph)
Директории для хранения vh3-операций подграфов.

vh3 позволяет добавлять подграфы в граф через декоратор `@vh3.decorator.external_graph`. Такие операции должны храниться в этой директории. Обоснование иерархии внутри директории subgraph и правила для добавления новых подграфов аналогичны используемым для [composite](composite).

Неочевидные моменты:
1. В декоратор `@vh3.decorator.external_graph` нужно передавать InstanceID конкретного инстанса существующего графа, а не WorkflowID. При вызове полученной функции на граф будет добавляться подграф именно с этим конкретным инстансом.
2. Имя функции в библиотеке операций-подграфов должно совпадать с именем (приведённым к snake-case) того графа, инстанс которого служит основой для vh3-операции. Если это не так, vh3 будет добавлять в граф свежесозданный пустой подграф.



## Полезное

vh3 позволяет импортировать граф из Nirvana в Python-код. Для этого нужно в окружении с Python и установленной vh3 выполнить:
```shell
python -m vh3 import -f https://nirvana.yandex-team.ru/flow/WorkflowID/InstanceID/graph
```
vh3-код будет выведен в консоль.

Эта возможность может быть полезной при внесении новых операций в библиотеку, особенно, если у них много входов/выходов/опций. Нужно в Nirvana на пустой граф положить нужную операцию, сохранить драфт, а затем выполнить импорт.
Определение функции, выведенное в консоль можно копипастить в нужное место библиотеки операций, провязывать глобальные опции, делать прочие правки и в дальнейшем использовать. В большинстве своём полученный код будет работать, но надо отдельно смотреть, совпадает ли сигнатура функции с самим кубиком в Nirvana, потому что иногда vh3 что-то дописывает к названиям аргументов, а потом сама не может спарсить (например, если у операции в Nirvana вход и опция называются по-разному, но после приведения к snake-case становятся одинаковыми).
