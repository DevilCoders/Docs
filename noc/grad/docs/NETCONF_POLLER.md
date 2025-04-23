В grad есть утилита для генерации запросов в netconf - grad/utils/netconfwalk.py.
Так как она комокуторе, ей можно передать учетные данные через переменные COMOCUTOR_IDENTITY, COMOCUTOR_LOGIN, COMOCUTOR_PASSWORD.
```shell
./venv/bin/python grad/utils/netconfwalk.py --jnx cloud-tehno-b1.cloud.yandex.net get-interface-information
# можно указать сырой xml 
./venv/bin/python grad/utils/netconfwalk.py --jnx cloud-tehno-b1.cloud.yandex.net "<get-interface-information><extensive/></get-interface-information>"
```
Есть опция --save PATH для сохранения запроса и ответа в python файл, который потом можно использовать в тестах. 

```shell
./venv/bin/python grad/utils/netconfwalk.py --jnx cloud-tehno-b1.cloud.yandex.net "<get-interface-information><extensive/></get-interface-information>" --save

```

Пример вывода:
```
/{jnx}interface-information /{jnx}physical-interface  {jnx}traffic-statistics =
/{jnx}interface-information /{jnx}physical-interface /{jnx}traffic-statistics  {jnx}input-bytes =0
/{jnx}interface-information /{jnx}physical-interface /{jnx}traffic-statistics  {jnx}output-bytes =0
/{jnx}interface-information /{jnx}physical-interface /{jnx}traffic-statistics  {jnx}input-packets =0
/{jnx}interface-information /{jnx}physical-interface /{jnx}traffic-statistics  {jnx}output-packets =0
/{jnx}interface-information /{jnx}physical-interface /{jnx}traffic-statistics  {jnx}ipv6-transit-statistics =
/{jnx}interface-information /{jnx}physical-interface /{jnx}traffic-statistics /{jnx}ipv6-transit-statistics  {jnx}input-bytes =0
/{jnx}interface-information /{jnx}physical-interface /{jnx}traffic-statistics /{jnx}ipv6-transit-statistics  {jnx}output-bytes =0
/{jnx}interface-information /{jnx}physical-interface /{jnx}traffic-statistics /{jnx}ipv6-transit-statistics  {jnx}input-packets =0
/{jnx}interface-information /{jnx}physical-interface /{jnx}traffic-statistics /{jnx}ipv6-transit-statistics  {jnx}output-packets =0
```

Пример конфига:
```yaml
pollers:
  comocutor transceiver linux:
    poller: comocutor
    poller params:
      getter: get_jnx_network
      device: NetconfDevice
      <<: *comocutor_credentials
      fn:
         temp: ["resampler_linear_{sample_period}"]
         rx_power: ["resampler_linear_{sample_period}"]
         tx_power: ["resampler_linear_{sample_period}"]
         rx_power_threshold_low: ["resampler_linear_{sample_period}"]
         rx_power_threshold_high: ["resampler_linear_{sample_period}"]
         oper_status: ["resampler_repeat_{sample_period}"]
         admin_status: ["resampler_repeat_{sample_period}"]
      
    filter: "([Cumulus] or [Switchdev]) and [опрос comocutor]"
    series: optical
    interval: 600
    logging: WARNING
    instance_group: main netconf instance
```

Из особенностей netconf тут можно выделить тот факт, что данные всегда в xml и не нужно парсить текст. 
В grad в основном используется привидение xml к объектам питонам, но никто не мешает извлекать данные через xpath или еще как из xml.
Тесты парсеров для данных netconf лежат в test_netconf.py. Сырые данные удобно собирать через netconfwalk.py.

Пример функций сбора:
```python
JNX_NETCONF_NETWORK = make_jnx_netconf_cmd("get-interface-information", ["extensive"])

def parse_jnx_network(data: str, ts: int) -> Mapdata_set:
    res = []
    rpc_reply = parse_juniper_netconf_xml_reply(data)
    for ifdata in rpc_reply["interface-information"]["physical-interface"]:
        values = {}
        ...
        res.append([ts, {"ifname": lifname}, values])
    return res

async def get_jnx_network(conn: BasicDevice, job: Job) -> Kvts_set:
    cmd_res = await conn.cmd(JNX_NETCONF_NETWORK)
    ts = int(time.time())
    res = parse_jnx_network(cmd_res.out, ts=ts)
    return mapdata_to_kvts(res)
```
Больше примеров есть в grad/user_functions/netconf_huawei.py.
