### Общая структура конфига
```yaml
config:
    system:
        <общие для всего приложения настройки>
    log:
        <настройки логирования>
    modules:
        <настройки модулей>
```

### Секция system
```yaml
system:
    dir: .
    uid: user
    gid: group
    reactor:
    -   { pool_count: 1, threads: 4, _name: global }
    -   { pool_count: 1, threads: 2, _name: http }
```

dir - рабочая директория процесса 
uid - запуск с привилегиями указанного юзера 
gid - запуск с привилегиями указанной группы 
reactor - именованные глобальные реакторы  

#### reactor
![](reactor.png)

I/O reactor - это именованный набор N пулов по M потоков. Пул - это обертка над boost::asio::io_context.

Рекомендуемая конфигурация - ```pool_count=N threads=1```. Такая конфигурация является в общем случае более производительной и простой для построения приложений.

### Секция log
```yaml
log:
    logger_name:
        level: info
        async: true
        queue_size: 100000
        format: ...
        sinks:
        -   type: reopenable_file
            path: var/log/myservice/myservice.log
        -   type: stdout
```

- level - debug, info, notice, warning, error, critical, alert, emerg или off   
- async - асинхронная запись в лог (из фонового треда), true|false  
- queue_size - размер очереди для асинхронной записи (только для async: true)  
- format - опциональный, дефолт ```[%Y-%b-%d %H:%M:%S.%f] %v```  
- sinks - куда писать логи, массив  
  -  type - file | reference | stdout  
  -  name - требуется для синков с type=reference  
  -  path - путь к файлу для синков с type=reference  
  -  force_flush - сбрасывать каждую запись на диск, по умолчанию false

Про формат подробнее можно почитать в [документации](https://github.com/gabime/spdlog/wiki/3.-Custom-formatting) на spdlog. 

Также см. раздел [log](log.md).

### Секция modules
```yaml
modules:
    module:
    -   system:
            name: statserver
            factory: ymod_statserver::impl
        configuration:
            # module specific items
    -   system:
            name: pq
            factory: ymod_pq::call_impl
        configuration:
            # module specific items
```

Конфиг модуля содержит две секции: system и configuration.

#### system
Предопределенные настройки для конструирования модулей:
name - имя модуля, используется для поиска через yplatform::find<>()
factory - имя конструктора, заранее определенного с помощью макроса REGISTER_MODULE

#### configuration
Специфические для модуля настройки. Помимо этого в configuration также можно задавать настройку ```reactor``` - загрузчик yplatform найдет этот реактор и передаст модулю для инициализации.

Подробнее об инициализации и регистрации модулей см. раздел [модули](modules.md).