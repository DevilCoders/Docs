Streaming telemetry - bleeding edge в мире сбора метрик. На столько bleeding, что даже
в википедии нет статьи про неё. За telemetry нет четкого технологического стека. Обычно, за
словами telemetry скрывается стандарт от [Openconfig](https://github.com/openconfig/reference/tree/master/rpc/gnmi), но кроме него есть и реализации от juniper, huawei, cisco.

Мотивация от openconfig:
```
SNMP-based network monitoring is long overdue for an upgrade. It was designed for legacy implementations,
with poor scaling for today’s high-density platforms, and very limited extensibility. Streaming telemetry is a
new approach for network monitoring in which data is streamed from devices continuously with efficient,
incremental updates. Operators can subscribe to the specific data items they need, using OpenConfig data
models as the common structure and interface.
```

### Openconfig
Группа визионеров пытающихся формализовать данные в YANG-модели(как MIB в мире SNMP). Стремятся к избавлению нас от вендорских особенностей и прийти в светлое будущее SDN.
Их модели описывают данные вроде сетевых счетчиков, сенсоров трансиверов, ((https://www.openconfig.net/projects/wifi/ Wi-Fi)) и многое другое. Создали язык описания моделей данных ((https://github.com/openconfig/public/blob/master/doc/openconfig_style_guide.md YANG)).
Стандартные модели и некоторые вендорские [тут](https://github.com/YangModels/yang).

#### GNMI - gRPC Network Management Interface
Стандарт описывает RPC, но не описывает сами данные. Данные прилетают в формате дерева key/value, где value почти всё что угодно.
От float до JSON-строка со структурой данных. Данные могут быть закодированы в text/JSON/JSON(RFC7951)/bytes/proto в зависимости от что поддерживает устройство.
Поддерживается get/set/delete/subscribe-запросы.

#### GNOI - gRPC Network Operations Interface
Стандарт описывающий RPC для выполнения команд. Описывает такие команды как:
- Перезагрузка.
- Скачать/залить файл.
- Проверка статуса системы - healthz.
- Операции с BGP типа рестарта сессии.

Смотри [openconfig/gnoi](https://github.com/openconfig/gnoi)

#### Nokia
Доки https://github.com/nokia/SROS-grpc-services

### Утилиты
https://github.com/karimra/gnmic
```(bash)
git clone https://github.com/karimra/gnmic.git
cd gnmic
go build -o gnmic main.go
./gnmic
```

Примеры:
```(bash)
gnmic -a 127.0.0.1:50051 --insecure sub --path "/interfaces/interface" --stream-mode stream --mode once
```



#### JTI - Junos Telemetry Interface
Используется UDP как транспорт и protobuf для кодирования данных. Все сенсоры честно зафиксированы в ((https://github.com/Juniper/TelemetryInterface proto файлах)).
https://www.juniper.net/documentation/us/en/software/junos/interfaces-telemetry/topics/concept/junos-telemetry-interface-oveview.html



#### Cisco MDT - Cisco model-driven telemetry
https://www.cisco.com/c/en/us/td/docs/iosxr/ncs5xx/telemetry/63x/b-telemetry-cg-63x-ncs540/model_driven_telemetry.html#:~:text=Model-driven%20Telemetry%20(MDT),set%20in%20a%20YANG%20model.
#### Huawei GRPC
https://support.huawei.com/enterprise/en/doc/EDOC1100125554/113266d1/key-telemetry-technologies

#### Особенности telemetry
- Из-за PUSH-модели очень сложно понять когда получен весь набор данных для агрегации. Сделать агрегат по всем интерфейсам очень сложно. В GNMI есть get запрос, что упрощает проблему.
- Интервал хоть и указывается в конфиге, но никто не гарантирует что он будет соблюден.


#### Особенности вендорские
juniper:
- Использует самодельный протокол JTI
- Не всегда есть счетчики по агрегатным интерфейсам типа ae. Чтобы собрать его значение, нужно получить счетчики с каждого интерфейса входящего в ae. То что разные карты могут слать с разным интервалом данные еще больше усложняет суммирование.

huawei:
- Для telemetry нужно покупать лицензию.

https://netdevops.me/2020/arista-veos-gnmi-tutorial/ \
https://www.cisco.com/c/en/us/td/docs/iosxr/ncs5000/programmability/70x/b-programmability-cg-ncs5000-70x/b-programmability-cg-ncs5000-70x_chapter_011.html \
https://blogs.cisco.com/developer/which-yang-model-to-use \
https://www.cisco.com/c/en/us/td/docs/optical/ncs1001/telemetry/guide/b-telemetry-cg-ncs1000.pdf \
https://infocenter.nokia.com/public/7750SR150R1A/index.jsp?topic=%2Fcom.sr.system.mgmt%2Fhtml%2Ftelemetry-intro.html
