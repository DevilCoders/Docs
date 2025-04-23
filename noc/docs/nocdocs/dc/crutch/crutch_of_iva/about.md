# Особенности дизайна IVA

# Topology

![file:/users/kitaro/iva-design-notes/ivatopologyv4.png](file:/users/kitaro/iva-design-notes/ivatopologyv4.png)Схема в .drawio формате ![file:/users/kitaro/iva-design-notes/ivatopologyv4.drawio](file:/users/kitaro/iva-design-notes/ivatopologyv4.drawio)Текущая схема отражает текущий дизайн сети ДЦ ИВА.
# L2

В текущем дизайне ToR коммутаторы имеют Eth-trunk с номером 100 в который входят минимум 2 интерфейса, по одному в каждый спайн iva-d1, iva-d2, между которыми собран MC-LAGG. Eth-Trunk 100 работает в L2 режиме и может пропускать VLAN L2 сервисов и vlan3002, который является IX-VLAN и используется для пиринга ToR коммутаторов, сервисных коммутаторов (iva-.a.) с внутренним RR ДЦ. L3 MTN VLAN на ToR коммутаторах живут только в пределах одного коммутатора.   У схемы с MC-LAGG между iva-d1 и iva-d2 есть несколько важных особенностей:
1. Между спайнами iva-d1 и iva-b-d2 собран 1 Tb линк, который работает как MC-LAGG peer link.
   > interface Eth-Trunk50   description iva-b-d2 Eth-Trunk50   mode lacp-static   peer-link 1
2. MC-LAGG heartbeat пакеты ходят через менеджмент сеть с соурс адресами менеджмент интерфейсов me0/0/0 спайнов. me0/0/0 интерфейсы между собой соединены через OOB менеджмент коммутатор iva-b-inoc1. Настройки на iva-d1:
   > dfs-group 1  source ip 178.154.140.2interface MEth0/0/0  description iva-b-inoc1 gi0/20  ip address 178.154.140.2 255.255.254.0
Все эти настройки и особенности отражены в коде аннушки, аннушка генерит все необходимые команды.   В спайны iva-d1, iva-d2 помимо ToR включаются сервисные коммутаторы iva-a1a, iva-a1b, iva-a3a, iva-a3b и FB PE устройства iva-32z1, iva-32z2 на них также собраны Eth-Trunk c линками в iva-d1 и iva-d2.   Терминация проектных L2 сетей растянутых по всему ДУ может осуществляться несколькими способами:
1. L2 FB проектные сети (да, да, они все еще существуют) происходит на саб-интерфейсах FB PE iva-32z1, iva-32z2. На сегодняшний день у нас осталось 3 FB VLAN 761, 762, 763 в которых все еще теплится жизнь. На iva-32z1, iva-32z2 настроен VRRP для этих VLAN, таким образом first-hop резервируется.
2. Часть L2 BB проектных сетей терминируются на паре коммутаторов iva-a3a, iva-a3b на Vlanif интерфейсах и между которыми также настроен VRRP.
3. Еще есть какое-то количество L2 BB проектных сетей которые терминируются на FreeBSD FW, работающих в роле Core router. В связи с планами по полному отказу от использования FreeBSD, эти сети будут переносится на коммутаторы iva-a3a, iva-a3b.
# L3

ToR свитчи будут иметь IBGP сессии с RR iva-b-rr11 и iva-b-rr12 через каждый спайн в vlan 3002. Далее FB, BB ToR маршруты будут доходить до PE и агргироваться по ::/56 и ::/48 и анонсироваться VPN рефлекторам сети.
# Edge

На границе ДЦ сети Backbone и Fastbone будут терминироваться на разных девайсах, для Backbone - iva-e1, iva-e2 (Huawei NE40); для Fastbone sr
1,2
-iva. Все эти устройства будут работать в роле PE.
# Tests

Коллеги из Huawei провели тестирование с нашими исходными данными, вот их отчет ![file:/users/kitaro/IVA-design-notes/yandexm-lagtestingreport.docx](file:/users/kitaro/IVA-design-notes/yandexm-lagtestingreport.docx)Во время работ 11.09.2019 проводили следующие виды тестов с конструкцией MC-LAGG, скриншот ниже показывает таймлайн и влияние на сервис в мониторинге Netmon на срезе all:![file:/users/kitaro/IVA-design-notes/ivatimeline1.jpg](file:/users/kitaro/IVA-design-notes/ivatimeline1.jpg)
1. Выведение ряда портов в сторону ToR коммутатором из MC-LAGG со стороны спайна, вывели 5 ToR свитчей и линки в сторону STOR iva-a1a из Eth-Trunk на iva-d2. Влияние на сервис замечено не было, прироста BUM траффика на портах замечено не было. Этим тестом проводилась проверка поведения системы при неконсистентной конфигурации и кейс с которым столкнулись при первой попытке включения конструкции MC-LAGG. При наличии портов в L2 режиме и не включенных в MC-LAGG свитч лернил bpdu с этих портов и пересчитывал stp, это вызывало шторм BUM траффика, из-за которого забивались очереди mac-learning на картах. Это поведение было починено в hot-patch /CE12800-V200R005SPH009.pat. Из проведенного теста делаем вывод что патч проблему полечил.
2. Выключение MC-LAGG peer-link. В мониторинге Netmon было заметно кратковременное (
   
    минута) незначительное проседание связности внутри и кросс-ДЦ связности.
3. Возвращение в работу второго спайна, включение MC-LAGG peer-link. В мониторинге Netmon было заметно более длительное (
   
    минут) проседание связности внутри и кросс-ДЦ связности.
4. Смена мастера MC-LAGG по средствам изменения dfs priority. В мониторинге Netmon было заметно кратковременное (
   
    минута) незначительное проседание связности.
5. Выключение management интерфейса на спайне, через который MC-LAGG обменивается hertbeat. Влияния на сервис не замечено.
# Fastbone

Текущая схема работы FB представлена ниже.![file:/users/kitaro/IVA-design-notes/ivafbnew.jpg](file:/users/kitaro/IVA-design-notes/ivafbnew.jpg)Схема в .drawio формате ![file:/users/kitaro/IVA-design-notes/ivafbnew.drawio](file:/users/kitaro/IVA-design-notes/ivafbnew.drawio)
1. Layer 2 FB сети терминируются на FB PE sr1-iva на сабинтерфейсах Eth-trunk1 (Eth-Trunk1.7
   , Eth-Trunk1.8
   ). Далее, маршруты к этим сетям анонсируются FB VPN рефлекторам сети.
2. FB PE sr1-iva имеет пиринг с RR iva-b-rr
   11,12
    и принимает от них маршруты c ToR FB community 13238:3098. Далее эти маршруты агрегируются по ::/56 и ::/48 и аннонсируются FB VPN рефлекторам сети.
3. Traffic flow для L2 и L3 выглядит одинаково:

- Входящий траффик в ДЦ **sr1-iva -> iva-b-d2 -> ToR iva-s***
- Исходящий траффик из ДЦ **ToR iva-s* -> iva-b-d2 -> sr1-iva**
- Внутренний траффик ДЦ **ToR iva-s* -> iva-b-d2 -> ToR iva-s***
ToDo:
1. Замена sr
   1,2
   -iva с Huawei CE8850-32CQ-EI на Huawei CE8850-64, CE8850-64 лучше подходит для использования в качестве PE, вендор рекомендует использовать этот девайс. Для начала их нужно купить - ![https://st.yandex-team.ru/BUY-12249](https://st.yandex-team.ru/BUY-12249)
2. После замены CE8850-32CQ-EI на Huawei CE8850-64 нужно будет сделать внешние линки sr2-iva, сделать пиринг с RR ДЦ и заагрегировать на нем L3 FB маршруты, у L3 FB появится резерв на границе ДЦ.
# Backbone

Планируемая реализация BB сети представлена ниже.![file:/users/kitaro/iva-design-notes/ivabbv3.png](file:/users/kitaro/iva-design-notes/ivabbv3.png)Схема в .drawio формате ![file:/users/kitaro/iva-design-notes/ivabbv3.drawio](file:/users/kitaro/iva-design-notes/ivabbv3.drawio)
1. L2 сети заехавшие в vrf Hbf будут терминироваться на а3* коммутаторах, с VRRP на Vlanif интерфейсах между каждой парой a3* свитчей, часть старых L2 сетей продолжит жить на FreeBSD FW core router.
2. iva-a1
   a,b
    коммутаторы имеют BGP peering с RR и принимать от RR сети с ToR BB_ToR community 13238:3099 и дале анонсируют эти сети с теми же community iva-e
   1,2,3,4
   . На iva-e* сети агрегируются до ::/56 и ::/48 и далее анонсируются VPN BB RR сети.
3. К iva-a1
   a,b
    подключена вся "a-шечные" устройства сети - FW ферма, FW core router, декапсуляторы, туннеляторы, L3 балансеры, NAT64-транслятор. Коммутаторы iva-a3
   a,b
    получают дефолт от FW-фермы подключенной к iva-a1* коммутаторам через iva-e
   . Также к iva-a3
    подключено несколько балансеров с 10G портами.