## SNMP-поллер
Используется модуль fastsnmp.

Конфигурация:
```yaml
# Настройки связанные с импортом данных в rmq.
series:
  # Тут power - параметр series из секции poller.
  snmp_poller.power:
    # Частота данных в БД. Влияет на интервал опроса и настройки интерполяторов.
    min_interval: 60
    # Данные не указанные в keys и values будут удалены.
    keys: ["host", "index"]
    values: ["power"]
    client: # параметры пуша данных
      solomon network: {common_labels: {"project": "noc", "cluster": "all", "service": "network"}}

pollers:
  SNMP cisco power: # Имя поллера
    poller: snmp
    poller version: 3  # 3 используется fn, вместо функций из snmp_mib.py
    poller params:
      counters: # oid'ы из дикта MIB в snmp_helper.py
        - oid: cefcFRUPowerSupplyGroupTable.cefcPowerUnits
         # В options поддерживается use_snmpget, use_snmpgetnext, use_snmpbulkget(по умолчанию) и use_snmpwalk. тип опроса
         # alias - аналог alias из snmp_helper.py, но более приоритетный. Например ("alias", "interface")
          options: ["use_snmpbulkget"]
        - oid: cefcFRUPowerSupplyGroupTable.cefcTotalDrawnCurrent
          options: ["use_snmpget"]
      log_counter_wrap: false  # Логгирование уменьшения счетчика
      post_fn: [rearrange_partial_data, recalc_cisco_power_usage, sum_all_values_with_host_key]
      skip_key_expr: {'ifname': '((?!ge|xe|et)|.+\.\d+)'} # Фильтр по ключам.
      oid_limit: 16 # максимальное количетсво oid'ов в запросе
      max_bytes: 1500 # ограничение на ожидаемый ответ. Работает не так как ожидается. Смотри исходники.
      bulk_max_repetitions: None # ограничение на количество запрашиваемых oid'ов в bulk-запросе. Зависит от max_bytes.
      max_interp: 720  # максимальная глубина интерполяции
      job_timeout: 600  # максимальное суммарное время опроса
      community: znoc
      ignore_error_5: true # подавление ошибок rfc3416 genErr
      dups_ok: false # отключить удаление дубликатов индексов
    filter: "{Cisco} and {Nexus} and {Cisco 6500} and [работает SNMP]"
    hosts: [] # Cтатический список хостов. Необходимо указать filter или hosts
    series: power
    interval: 60  # Интервал опроса
    # Опциональные опции:
    timeout: 20  # Первый таймаут ожидаения ответа, дальше back-off.
    afterburn: 4  # Количество итераций сбора с урезанным интервалом
    logging: DEBUG  # Установить указанный уровень логгирования.
    instances: 1  # Количество инстансов поллеров. Для распределения нагрузки по процессам.
```

Внимание: при использовании use_snmpbulkget и use_snmpget* для oid'ов c type=value могут быть спецэффекты из-за того
что данные будут получены в разное время что повлечет за собой неполные(в рамках единицы результата, в конечном итоге данные будут полными) данные в результате.
Для нивелирования этой проблемы надо использовать функцию rearrange_partial_data.

oid типа key всегда опрашиваются bulk'ом, а oid с данными могут bulk'ом, а могут get'ом.
Если использовать bulk, то данные с одним индексом могут иметь разное время.

Если несколько поллеров использует одинаковый series, то series может быть указан только в одном конфиге.

Интервал должен быть больше частоты обновления счетчика. Её можно выяснить с помощью скрипта utils/get_update_freq.py.

Oidы хранятся в snmp_mib.py
```python
...
    "JUNIPER-COS-MIB": {
        "1.3.6.1.4.1.2636.3.15.4.1.7": {
            "name": "jnxCosQstatTxedPkts",  # имя из MIB, удобно использовать для поиска
            "alias": "passed_packets",  #  используется в grad
            "type": "value",  # тип данных. value - сенсор например rx_packets, key - ключ данные например ifname
            "fn": "speed"  # функция обработки данных. Например speed вычисляет скорость из нарастающего счетчика
        },
        "1.3.6.1.4.1.2636.3.15.4.1.9": {"name": "jnxCosQstatTxedBytes", "alias": "passed_bytes",
                                        "type": "value", "fn": ("speed", {"factor": 8})},
        "1.3.6.1.4.1.2636.3.15.4.1.53": {"name": "jnxCosQstatTotalDropPkts", "alias": "discarded_packets",
                                         "type": "value", "fn": "speed"},
        "1.3.6.1.4.1.2636.3.15.4.1.55": {"name": "jnxCosQstatTotalDropBytes", "alias": "discarded_bytes",
                                         "type": "value", "fn": ("speed", {"factor": 8})},
        "1.3.6.1.4.1.2636.3.15.4.1.58": {"name": "jnxCosQstatDepthCurrent", "alias": "queued_depth_bytes",
                                         "type": "value"},
    },
...
```
