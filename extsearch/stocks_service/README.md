# Содержимое
1. [Запуск сервиса](#launch)
1. [Про фабрику](#factory)
    1. [Регистрация интерфейсов](#factory_interfaces)
    1. [Регистрация имплементаций](#factory_impls)
    1. [Создание объектов](#factory_cretion)
1. [Про таски](#tasks)
    1. [Локальные таски](#tasks_local)
    1. [Распределенные таски](#tasks_remote)
1. [Про парсеры свечек](#candles)
1. [Mongo DB](#mongodb)



---
# Запуск сервиса <a name="launch"></a>
Использование:
```bash
./stocks-master -c ./config.json
```


---
# Про фабрику <a name="factory"></a>
`NStocksService::TFactoryBase` - шаблонный класс, используемый в качестве фабрики для всех интерфейсов.
Фабрика - синглтон с глобальными регистраторами.

## Регистрация интерфейсов <a name="factory_interfaces"></a>
 - Фабрика использует `TIntrusivePtr`, так что все интерфейсы должны иметь счетчики.

 - Интерфейсы регистрируются с помощью `NSTOCKS_REGISTER_INTERFACE(interface, ... )`

- При добавлении нового интерфейса нужно задать список типов аргументов, которые будут у конструкторов в имплементациях интерфейса. Все наследники будут обязына иметь конструктор с таким набором аргументов:
   - `NSTOCKS_REGISTER_INTERFACE(IBlabla, const NConfig::TConfig&, TLogger&, THolder<ICringe>&&);`
   - `NSTOCKS_REGISTER_INTERFACE(IThing, const NConfig::TConfig&);`

- `NSTOCKS_REGISTER_INTERFACE` под капотом дефайнит частичную специализацию `NStocksService::TFactoryTraits<>` для указанного интерфейса со списком типов для конструкторов;

Пример:
```cpp
class IBlabla : public TAtomicRefCount<IBlablaA> {
public:
    virtual ~IBlabla() = default;

    virtual void Run() = 0;
};
NSTOCKS_REGISTER_INTERFACE(IBlabla, const NConfig::TConfig&, TLogger&, THolder<ICringe>&&);



class IThing : public TAtomicRefCount<IThing> {
public:
    virtual ~IThing() = default;

    virtual void Break() = 0;
};
NSTOCKS_REGISTER_INTERFACE(IThing, const NConfig::TConfig&);
```

## Регистрация имплементаций <a name="factory_impls"></a>
- каждая имплементация интерфейса должна иметь констуртор с сигнатурой, описаной при регистрации интерфейса;
- имплементации регистрируются с помощью `NSTOCKS_REGISTER_INTERFACE`
- `NSTOCKS_REGISTER_IN_FACTORY` под капотом создает глобальный объект регистратор, который в конструкторе добавляет имплементацию в фабрику;
- Имя класса ф фабрку берется через `##`

Пример:
```cpp

class TSomeBlablaA : public IBlablaA {
public:
    TSomeBlablaA(const NConfig::TConfig& conf, TLogger& logger, THolder<ICringe>&& cringe);

    void Run() override;
};
NSTOCKS_REGISTER_IN_FACTORY(IBlablaA, TSomeBlablaA);



class TSomeThing : public IThing {
public:
    TSomeThing(const NConfig::TConfig& conf);

    void Break() override;
};
NSTOCKS_REGISTER_IN_FACTORY(IThing, TSomeThing);
```

## Создание объектов <a name="factory_cretion"></a>
```cpp
NConfig::TConfig conf;
TLogger logger;

auto blabla = TFactory<IBlablaA>::Create("TSomeBlablaA", conf, logger, MakeHolder<TCringe>());
auto thing = TFactory<IThing>::Create("TSomeThing", conf);
```


---
# Про таски <a name="tasks"></a>
 - Сервис содержит шедуллер `NStocksService::TScheduller`, который выполяет таски;
 - Таски - экземляры классов, имплементирующих интерфейс `NStocksService::IScheduledTask`;
 - Сервис создает таски через фабрику.
 - Таски по источнику,в котором описаны конфиги тасок, делятся на `локальные` и `распределенные`


## Локальные таски <a name="tasks_local"></a>
 - конфиги тасок лежат в объекте `tasks` в `config.json`
 - сервис при старте по этому конфигу создает таски и добавляет в шедуллер


## Распределенные таски <a name="tasks_remote"></a>
 - конфиги тасок лежат в `mongodb`
 - у сервиса должна быть локальная таска `TRemouteTasksUpdateTasks`, которая будет переодически:
   - ходить в mongodb и забирать таски у которых старый `heartbeat`;
   - добавлять такие таски в шедулер сервиса;
   - обновлять hearbeat у тасков в `mongodb`, чтобы другие инстансы из не взяли себе;

Распределенные таски **не** распределеюся **равномерно** по инстансам сервиса. Таски получает тот инстанс, кто первый заметил устаревшие `heartbeat` у тасок в mongodb.
Как только инстанс сервиса упал, обновляет ресурсы в няне, или по другой причине стал offline, то у его распределенных тасок устареет значение `hearbeat` и они будут
созданы в других online инстансах.



---
# Про парсеры свечек <a name="candles"></a>

Данные свечек извилаются тасками `NStockService::TRequestDataTask`.
В таске задаются:
 - урл куда сходить
 - парсер, которым надо вытащить данные свечек из ответа

Парсеры реализуют интерфейс `NStocksService::ICandleDataExtractor` и создаются через фабрику.
У `ICandleDataExtractor` eсть так же наследники
 - `IJsonCandleDataExtractor`,
 - `IXmlCandleDataExtractor`,

от которых можно унаследоваться в своих парсерах, чтобы извлекать данные свечек из `json`, `xml`



---
# Mongo DB <a name="mongodb"></a>

Живет в Yandex Cloud [stocks_mongodb](https://yc.yandex-team.ru/folders/foou2c8mmhjoebn2thmc/managed-mongodb/cluster/mdbataj07iah8jcobog2?section=overview)

```bash
mongo --norc \
        --host 'rs01/sas-k6wkzl4fdr1vb4de.db.yandex.net:27018,vla-l788fmds2jjxkyxr.db.yandex.net:27018' \
        --ipv6 \
        -u <user> \
        -p <psswd> \
        stocks

```


### Cхема коллекции `tasks`
```js
db.createCollection( "tasks" , {
   validator: { $jsonSchema: {
      bsonType: "object",
      required: [ "type", "period", "config", "last_runner_heartbeat", "current_runner" ],
      properties: {
         type: {
            bsonType: "string",
            description: "Task class name in factory. Required and must be a string" },
         period: {
            bsonType: "string",
            description: "Time period. Examples: '2s', '2m', '2h'. Required and must be a string" },
         config: {
            bsonType: "object",
            description: "Task config object. Required and must be an object" },
         last_runner_heartbeat: {
            bsonType: "date",
            description: "Last runner heartbeat date time. Required and must be an Date" },
         current_runner: {
            bsonType: "string",
            description: "Current runner name. Must be a string" }
      }
   }
}})
```
 - `type`  : _string_ - Имя класса таски, зарегистрированне в фабрике тасок;
 - `period` : _string_ - Период `TDuration` запуска таски, передоваемый в конструктор таски;
 - `config` : _object_ - Конфиг таски в json, передоваемый в конструктор таски;
 - `last_runner_heartbeat` : _date_ - DateTime последнего hearthbeat от инстанса сервсиа в котором запускается таска; В конфиге инстанса должна быть таска `TRemoteTasksUpdateTask`, котоая отвечает за heartbeat и запускает таски из mongodb;
 - `current_runner` : _string_ - Идентификатор инстанса, в шедуллере которого запускается сейчас таска. (или запускалась таска);

Добавление новой таски в `mongodb`:
```js
db.tasks.insert({
    type: 'TEchoTask',
    period: '5s',
    config: {
        message: 'Hello from mongo'
    },
    last_runner_heartbeat: new Date(0),          // or ISODate('1970-01-01T00:00:00Z')
    current_runner:''
})
```
