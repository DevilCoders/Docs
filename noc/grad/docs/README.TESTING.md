# Разработка и тестирование
## Запуск сервера
Для разработки и тестинга подойдет любой Linux. Если нужны дырки как у прода, то есть dev-сервер **sas-test-grad1.net.yandex.net**.
Можно сделать свой, но нужно катить новые acl и иметь 4ку, так как есть много устройств v4-only.

Запуск сервера:
```bash
ya make noc/grad/cmd/grad_server
noc/grad/cmd/grad_server/grad_server -c grad_server_test.yml -l
```
Внимательно изучите конфиг grad_server_test.yml перед запуском!

В текущей grad_server_test.yml конфиге не указаны поллеры, поэтому надо их либо
добавить в этот файл, либо подключить директорию со своими конфигами:
```bash
noc/grad/cmd/grad_server/grad_server -c grad_server_test.yml -l --config-directory conf_test.d
```
Можно сделать симлинк из conf_test.d на конфиг в conf.d для включения части поллеров.

Для ускорения запуска можно включить редис в конфиге.

## Подключение к потоку данных сервера:
Если в конфиге включен http upstream, то данные можно увидеть так:
```bash
curl "http://127.0.0.1:12346/local_grad/#"
```

## Разработка
Единица конфигурации это поллер. В нем указывается набор хостов,
тип опроса, аргументы опроса, интервал и серию данных.

Конфигурация:
```yaml
series: # Настройки связанные с импортом данных в rmq.
  # snmp_poller.power - параметр series из секции poller, он же routing key в rmq
  snmp_poller.power:
    # Частота данных в БД. Влияет на интервал опроса и настройки интерполяторов.
    min_interval: 60
    # Данные не указанные в keys и values не будут обработаны в grad-client.
    # Можно не указывать, тогда не будет фильтрации
    keys: ["host", "index"]
    values: ["power"]
    client: # куда будет пушить grad-client
      solomon network: {common_labels: {"project": "noc", "cluster": "all", "service": "network"}}

pollers:
  test poller: # Имя поллера
    ....
    series: snmp_poller.power
```

## Comocutor-поллер
1. Идем в comocutor_helper.py и добавляем функция выполняющую команду. Например:
```python
async def get_some_counters(conn: BasicDevice, job: Job) -> Kvts_set:
    data = await conn.cmd("show ololo | display json")
    ts = int(time.time())
    res = parse_data(data.out, timestamp=ts)
    return mapdata_to_kvts(res)

def parse(data, timestamp):
    mapdata = []
    for item in range(data):
        mapdata.append(
            (
                timestamp,  # Mapdata_ts
                {           # Mapdata_key
                    "ifname": item["ifname"]
                },
                {           # Mapdata_value
                    "bytes": float(item["bytes"]),
                }
            )
        )
    return mapdata
```
В проекте comocutor-contrib есть много парсеров. Стоит сначала поискать там. Если новый парсер может пригодится другим, то стоит его занести в comocutor-contrib.

2. Добавляем новую функцию в список GETTERS переменную в comocutor_poller.py.

3. Создаем в папке conf.d yaml-файл по [этой](conf.d/README.md "Документация").

### Пример конфигурации comocutor-поллера
```yaml
credentials: !include credentials.yml
# Настройки связанные с импортом данных смотри выше

pollers:
  comocutor cumulus_ololo:
    poller: comocutor
    poller params:
      getter: get_ololo_data
      device: PCDevice
      login: "login"
      password: "password"
      # fn применение функций над определенным ключом данных
      fn: {bytes: [ "multiplier_8", "resampler_linear_{sample_period}"],
           oper_status: ["resampler_repeat_{sample_period}"],
      }
    filter: "{test}"
    series: test_series
    interval: 600
    logging: WARNING
    instance_group: main comocutor instance
```
```device: PCDevice``` Лучше указать, чтоб комокутор не пытался определять тип при подключении.

Подробности про [netconf](https://noc-gitlab.yandex-team.ru/nocdev/grad/-/blob/master/NETCONF_POLLER.md "readme")
