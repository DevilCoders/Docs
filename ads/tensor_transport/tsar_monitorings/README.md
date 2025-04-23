### Мониторинг моделей царя

## Что мониторится:
* Отставание ресурса TSAR_DUMP
* Отставание ресурса TSAR_DUMPS_LIST
* ~~Отставание таблиц на yt~~ Сейчас не мониторится. Для включения можно поправить секцию в конфиге `tsar_yt_tables`

Понять смыслы отставаний можно по коду мониторинга.

## Как устроен конфиг мониторинга?
Конфиг состоит из секций на каждый объект мониторинга. Секции обладают общими параметрами:
```yaml
tsar_dump:  # имя конфига
    warn:   # время до warn 
        hours: 10
        minutes: 0
        seconds: 0
    crit:  # время до crit
        hours: 12  # любую секцию hours, minutes, seconds можно опустить
    juggler_service: tsar_dump  # название сервиса в джагглере куда отправлять события
```

## Как обновить мониторинг?
* Собрать ресурс ARCADIA_PROJECT с помощью таска [YA_MAKE](https://sandbox.yandex-team.ru/task/537756271/view).
Важные параметры:
```yaml
    Svn url for arcaida: arcadia:/arc/trunk/arcadia@<REVISION>
    Build artifacts:     ads/tensor_transport/tsar_monitorings/tsar_monitorings
    Targets:             ads/tensor_transport/tsar_monitorings
```
* Подставить id ресурса `ARCADIA_PROJECT` в [шедулер](https://sandbox.yandex-team.ru/scheduler/17351/view)
* Если по каким-то причинам шедулер потерялся или не работает, правильные параметры нового шедулера:
```yaml
TASK_TYPE:    RUN_YABS_PYTHON_SCRIPT_2
config_path:  ads/tensor_transport/tsar_monitorings/conf
cmd_template: {binary} --conf {conf} --token $YT_TOKEN
```
