# Тут лежат дашборды [Хита](https://heat.yandex-team.ru/)
Каждый файл с расширением yaml - один даборд.

Схема:
```yaml
# Имя дашборда, используется в качестве слага. Единственный обязательный параметр.
name: Mydashboard

# Описание дашборда (показывается в саджест). По умолчанию ничего.
description: мой крутой дашборд

# Сортировка событий. Варианты: mostCritical / last. По умолчанию last.
sortBy: mostCritical

# Минимальный приоритет. Варианты: null (Любой) / info / warning / average / high. По умолчанию null.
priorityLimit: high

# Период. Варианты: null (Любые) / h / d / w / m. По умолчанию null.
timeLimit: d

# Juggler фильтр для агрегатов. По умолчанию ничего.
jugglerAggregateQuery: 'namespace=traffic-duty | namespace=dns-duty'

# RT фильтр. По умолчанию ничего.
rtQuery: '{decapsulator} or {балансировщик} and not {метабалансер} and not {балансировщик CDN}'

# Группировка. Варианты: zabbix / zabbix+. По умолчанию zabbix+.
groupBy: zabbix+

# RegExp. По умолчанию ничего.
regexp: '(utilization|diff|forced by stable_time|rdr-|test)'

# Значение RegExp. Варианты: include / exclude. По умолчанию exclude.
regexpMode: exclude

# Показывать ли скрытые события. Варианты: true / false. По умолчанию false.
showHidden: false
showMuted: false

# Гибкий фильтр по атрибутам событий. См. описание ниже. По умолчанию ничего.
filter: '(tag = "linkeye" and not (rt_tag = "Бенуа" or rt_tag = "БЦ Аврора")) or help_key = "unispace"'
```

## Гибкий фильтр
В поле `filter` можно дополнительно пофильтровать события, которые попали на дашборд через `rtQuery` и `jugglerAggregateQuery`.

Язык фильтра состоит из _селекторов_, которые можно объединять через операторы `and`, `or` и скобки. Также можно использовать отрицание через `not`.

Селектор - это тип селектора, оператор сравнения и значение. Например, `rt_tag = "Бенуа"` или `help_key != "unispace"`.

Оператор сравнения - это `=` (равно) или `!=` (не равно). Значение - это всегда строка в двойных кавычках.

Доступные типы селекторов:
  - `tag` - тег события (из Джагглера или Заббикса (applications)). Например, `tag = "linkeye"`.
  - `rt_tag` - тег хоста из RT. Например, `rt_tag != "в оффлайне"`.
  - `prio` - приоритет события, варианты:
    - `diagnostic`
    - `warning`
    - `average`
    - `critical`
    - `disaster`

    Например, `prio = "critical"`
  - `help_key` - вики-ключ из проверки. Например, `help_key != "unispace"`.
  - `juggler_service` - поле `service` из Джагглера. Например, `juggler_service = "fw-fhop-unreach"`.
  - `juggler_instance` - поле `instance` из Джагглера. Например, `juggler_instance = "some_instance"`.
