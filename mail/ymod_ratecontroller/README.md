## ymod_ratecontroller

### Что это?
Модуль для ограничения параллельности выполнения задач. Позволяет иметь множество независимых очередей на
выполнение.

Включает в себя два класса: *rate_controller* и *rate_controller_module*.


### rate_controller
Ограничивает количество одновременно выполняемых задач. Позволяет отменять задачи как вручную, так и по таймауту.


### rate_controller_module
Хранилище, оперирующее множеством rate_controller-ов, каждый из которых содержит независимую очередь задач.

Например, можно завести отдельный рейтконтроллер для походов в каждый внешний сервис.

Кроме того, рейтконтроллеры могут образовывать иерархию и наследовать настройки друг друга.


### Настройки
```yaml
reactor: global # однотредовый реактор, на котором будет работать модуль
settings: # базовые настройки
    max_concurrency: 100 # максимальное число одновременно выполняемых задач
    max_queue_size: 1000 # максимальный размер очереди на выполнение
children: # настройки для конкретных рейтконтроллеров
-   name: sharpei
    settings:
        max_concurrency: 500
        max_queue_size: 10000
-   name: xdb
    max_concurrency: 20
    max_queue_size: 1000
    children:
    -   name: xdb301
        settings:
            max_concurrency: 50
            max_queue_size: 1000
    -   name: xdb302
        settings:
            max_concurrency: 75
            max_queue_size: 1000
```


### Примеры
#### Использование модуля и выполнение задач
```c++
auto module = yplatform::find<ymod_ratecontroller::rate_controller_module>("rate_controller");
auto rate_controller = module->get_controller("xdb.xdb301");
rate_controller->post([](error_code err, const completion_handler& on_complete) {
    if (!err) {
        YLOG_G(info) << "do request";
    }
    on_complete();
});
```

#### Использование контекста задачи
При вызове метода post в качестве параметра можно передать контекст задачи.
```c++
auto context = boost::make_shared<yplatform::task_context>();
rate_controller->post(context, [](error_code err, const completion_handler& on_complete) {
    if (!err) {
        YLOG_G(info) << "do request";
    }
    on_complete();
});
```

Далее по этому контексту можно отменить задачу, если она еще не успела начать выполнение.
```c++
rate_controller->cancel(context);
```
Если в контексте задачи назначен дедлайн, то задача будет отменена при его наступлении.
#### Использование RAII для завершения задач
yplatform::execution_holder оборачивает completion_handler и вызывает его в деструкторе.
```c++
auto module = yplatform::find<ymod_ratecontroller::rate_controller_module>("rate_controller");
auto rate_controller = module->get_controller("xdb.xdb301");
rate_controller->post([](error_code err, const completion_handler& on_complete) {
    auto rc_holder = std::make_shared<yplatform::execution_holder>(on_complete);
    if (!err) {
        YLOG_G(info) << "do request";
    }
});
```
