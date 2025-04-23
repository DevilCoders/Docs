# Окружение модуля

Функции модуля (`fill_graph`, `scan_resources`, `handle_build_status`), а также задачи модуля (`Task`) запускаются с выставленной переменной окружения `ENVIRONMENT_NAME`. Она может принимать значения: `stable`, `datatesting`, `unstable`.

Окружение зависит от контура, в котором запускается модуль:

* в контуре `stable` значение `ENVIRONMENT_NAME=stable`;
* в контуре `datatesting` значение `ENVIRONMENT_NAME=datatesting`;
* во всех остальных контурах  значение `ENVIRONMENT_NAME=unstable`.

Узнать имя окружения изнутри модуля можно так:

* в коде на Питоне с помощью функции [maps.pylibs.yandex_environment.environment.get_yandex_environment()](https://a.yandex-team.ru/arc/trunk/arcadia/maps/pylibs/yandex_environment/environment.pyx?rev=r6603787#L25);
* в коде на C++ с помощью функции [maps::common::getYandexEnvironment()](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/common/include/yandex/maps/common/environment.h?rev=r6603787#L48).

## Настройки окружения

В задачи модуля дополнительно передаётся словарь с настройками окружения `environment_settings` через вызов метода `Task.load_environment_settings`. Словарь содержит секреты для доступа к разным внешним сервисам, а также пути в Кипарисе и S3 для хранения ресурсов.

У каждого контура свой словарь с настройками. Для системных контуров словарь формируется вручную и хранится в Аркадии. Для пользовательских контуров словарь генерируется на лету по шаблону:

* в контуре `stable` файл [environment_settings.stable.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/scheduler/config/environment_settings.stable.json);
* в контуре `datatesting` файл [environment_settings.datatesting.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/scheduler/config/environment_settings.datatesting.json);
* в пользовательских контурах шаблон [environment_settings_user_template.stable.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/scheduler/config/environment_settings_user_template.stable.json).

Остальные файлы в папке [maps/garden/scheduler/config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/scheduler/config) относятся к другим инстансам Огорода, и разработчикам модулей они не нужны.

### Расширение настроек окружения

Если вашему модулю нужны какие-то настройки, которые зависят от имени окружения, то рекомендуется хранить их прямо в модуле.

Настройки можно выбирать вручную в зависимости от значения `ENVIRONMENT_NAME`, либо использовать вкомпилированные в бинарный модуль ресурсы и библиотеку [maps/libs/config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/config) для чтения:

```
RESOURCE(
    config.stable.json      /config.stable.json
    config.datatesting.json /config.datatesting.json
    config.unstable.json    /config.unstable.json
    config.unittest.json    /config.unittest.json
)
```

Но если вам в модуле нужен доступ к новому секрету, то придётся расширять словарь `environment_settings`. Для этого нужно добавить секрет в 3 выше описанных файла (`environment_settings.stable.json`, `environment_settings.datatesting.json`, `environment_settings_user_template.stable.json`) по [инструкции](secrets.md). Далее нужно попросить разработчиков Огорода выкатить шедьюлер Огорода в стейбл.
