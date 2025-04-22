# Работа с контурами

## Как добавить новый системный контур

В папку [maps/garden/conf/cluster][environment_settings] поместить файл с настройками окружения вида `environment_settings.<contour_name>.json`.
Эти настройки будут передаваться в метод `load_environment_settings` в задачи огородных модулей, которые будут запускаться в этом контуре.

В файл с [секретами][secrets] вписать необходимые секреты, которые будут подставлены в плейсхолдеры в файле `environment_settings.<contour_name>.json`.

Выбрать имя окружения для запуска задач огородных модулей. Это имя будет передаваться в модули через переменную окружения `ENVIRONMENT_NAME`. Имя указать [здесь][task_environment].

Выбрать, какие версии модулей будут запускаться в этом контуре. В настоящий момент есть выбор из 2х вариантов: тестовые и стабильные версии модулей. Вариант указать [здесь][module_environment].

Создать контур в Монге командой:

```
db.contours.insertOne({
	"_id" : "<contour_name>",
	"status" : "active",
	"owner" : null,
	"creation_time" : null,
	"is_system" : true
})
```

Включить сканирование ресурсов в этом контуре. Для этого нужно вписать имя контура в [конфиг сервера][scan_resources].

Выкатить сервер и подождать, пока сканирование отработает. Это потребует ~15 минут.

Не все source-билды создаются через механизм сканирования ресурсов. При необходимости нужно создать source-билды через POST-запрос вручную.

Включить автостарты в этом контуре. Для этого нужно вписать имя контура в [конфиг сервера][autostart].

Автостартер для reduce-модулей требует наличия предыдущего билда. Первые билды для reduce-модулей нужно стартовать вручную через UI.


## Как удалить системный контур

TODO

## В каком окружении запускаются модули

Все модули запускаются с выставленной переменной окружения `ENVIRONMENT_NAME`. Она указывается при вызове функций `fill_graph`/`predict_consumption`/`propagate_properties`/`scan_resources` и при запуске операций в YT.

Имя окружения вычисляется для каждого контура в функции [get_task_environment_name][task_environment]:

Чтобы узнать имя окружения, в котором была запущена конкретная задача, нужно открыть страницу с YT-операцией этой задачи. Там на главной странице слева внизу будут перечислены переменные окружения, и в том числе `ENVIRONMENT_NAME`.

[environment_settings]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/conf/cluster
[secrets]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/server/sedem_config/secrets.yaml
[task_environment]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/sdk/utils/contour.py?rev=r8635881#L8
[module_environment]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/server/lib/contour_manager.py?rev=7477304#L43
[scan_resources]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/conf/cluster/server.stable.json?rev=7477304#L249
[autostart]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/conf/cluster/server.stable.json?rev=7477304#L252
