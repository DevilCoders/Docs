# Архитектура магистральной сети

Идеология магистральной сети предполагает, что устройства, образующие IP/MPLS ядро (отдельно стоящие [P-маршрутизаторы](https://racktables.yandex-team.ru/index.php?andor=and&cft%5B%5D=516&cfe=&page=depot&tab=default) и [Edge-коммутаторы](https://racktables.yandex-team.ru/index.php?page=depot&tab=default&andor=and&cfe=%7B%24typeid_8%7D&cft[]=1379) внутри ДЦ), не участвуют в BGP и не обладают информацией о внешних IPv4/IPv6 маршрутах. Их роль сводится к форвардингу трафика от одного PE-устройства к другому по MPLS-метке.

В роли PE-устройств выступают [бордеры](https://racktables.yandex-team.ru/index.php?andor=and&cft%5B%5D=57&cfe=&page=depot&tab=default), z'ки (ищутся по тегу "многодэшка"), и e'шки (если говорим про IVA).

Эти маршрутизаторы связаны друг с другом оптическими линками, арендованными каналами или через DWDM и создают 2 отдельные друг от друга сущности, две сети: [Backbone](http://cacti-noc.yandex.net/plugins/weathermap/weathermap-cacti-plugin.php?action=viewmap&id=dc3dd752b90ed19d1485) и [Fastbone](http://cacti-noc.yandex.net/plugins/weathermap/weathermap-cacti-plugin.php?action=viewmap&id=1d7aa359cc8b314202bd).

**Backbone** - по ней передается пользовательский и прочий "интерактивный" трафик, для которого критичны задержки и потери.

**Fastbone** - предназначена для служебного трафика, не столь критично относящегося к увеличению задержки и потерям. По сети Fastbone стоит передавать bulk-трафик:
- вроде репликации баз данных
- передачи логов.

По сети Backbone передавать критический сервисный тафик с минимизацией потерь и задержек.

Для создания LSP и распространения транспортных меток используется SR для Fastbone и связка LDP/RSVP для Backbone.

Поддержка IPv6 в ядре отсутствует, поэтому информация о привязке MPLS-меток к различным маршрутам (IPv6/VPNv6) распространяется по BGP с помощью labeled IPv6-префиксов, с IPv4 BGP Next Hop и технологий 6PE [RFC4798](http://tools.ietf.org/html/rfc4798) и 6VPE [RFC4659](https://tools.ietf.org/html/rfc4659).

Между PE-маршрутизаторами эту информацию распространяют BGP Route Reflector-ы.

[Список BGP Route Reflector](https://wiki.yandex-team.ru/noc/reflectors/)

## IGP

### Общая информация

В качестве протокола IGP на FB магистральных устройствах сети Яндекса используется протокол `IS-IS`.

В качестве протокола IGP на BB магистральных устройствах сети Яндекса должен использоваться протокол `OSPFv2`. Планируется миграция на протокол `IS-IS`.

На сети BB применяются LDP и RSVP-TE

#### Основные параметры IS-IS

Используем тип метрики `wide-only` на всех маршрутизаторах сети.

Используем `level-2-only` на всех Uplink.

Используем `p2p` на всех Uplink.

Не используем `BFD`.

**Таймеры** подбираем так, чтобы быстро реагировать на события IGP и если этих событий много, то мы быстро тормозим их.

### Segment Routing

В настоящее время применяется на сети FB.

Используем следующий диапазон SRGB:
- `SRGB_START` равен 160000
- `SRGB_END` равен 225000

В качестве протокола распространения меток используется расширение SR в ISIS. Для реализации SR-TE применяются SR-Policy. Как и следует из имени, это просто политика, упрощающая "пуш" сервисного трафика в SR-туннели.
Псевдокодом любая политика может быть описана так:
```
if
  prefix.bgp_color_community == tunnel.color &&
  prefix.bgp_nexthop == tunnel.endpoint
then 
  prefix.fib_nh = tunnel
```

На данный момент мы используем `color:10`, чтобы пометить FB-префиксы, в качестве некст-хопа в политике экспорта `SET_VPN_NHOP` записывается `Loopback10`.

После переезда на IS-IS в BB некст-хопом станет `Loopback0`, а разделение BB/FB-префикс будет осуществляться исключительно с помощью color-коммьюнити. 

К примеру, получив такой префикс, ОС маршрутизатора парсит некст-хоп (10.255.0.10) и color-коммьюнити (10) и пытается "резолвить" такой маршрут через какой-нибудь туннель/протокол.
```
vvenglovskii-nocauth@sas-32z1> show route 2a02:6b8:fc03::/56 receive-protocol bgp 10.255.0.30 table bgp.l3vpn-inet6.0 detail

bgp.l3vpn-inet6.0: 2856 destinations, 8543 routes (2828 active, 0 holddown, 56 hidden)
* 95.108.237.10:1110:2a02:6b8:fc03::/56 (3 entries, 0 announced)
     Import Accepted
     Route Distinguisher: 95.108.237.10:1110
     VPN Label: 524282
     Nexthop: ::ffff:10.255.0.10
     Localpref: 100
     AS path: ?  (Atomic Originator)
     Cluster list:  87.250.234.18
     Originator ID: 95.108.237.10
     Communities: 13238:3090 target:13238:101 color:0:10
```

В зависимости от вендора/платформы выбор процесс выбора туннеля/протокола сильно отличается:
* Подобный дракону Huawei использует политику в vrf (или GRT), которая определяет порядок приоритетов у протоколов
```
tunnel-policy SR-POLICY
tunnel select-seq sr-te-policy cr-lsp lsp load-balance-number 64 unmix
ip vpn-instance Hbf
ipv6-family
tnl-policy SR-POLICY
```
* Солнцеликая Nokia "хардкодит" приоритет SR-Policy как наивысший, то есть если у маршрута есть возможность "зарезолвиться" через SR-политику, то все остальные протоколы идут лесом, а трафик идет по туннелю из политики. Если не вышло, то дальше в дело вмешивается общий приоритет протоколов.

* Богоподобный Juniper пошел дальше всех, в политике импорта в vrf указывается так называемая ```resolution-map```, то еть список вариантов для "резолва" маршрутов в vrf. К сожалению, на данный момент там есть только color, что означает "или резолвим через SR-Policy, или не резолвим вообще". Это приводит к таким бодрящим сценариям, когда из-за лежащего туннеля маршрут помечается как Hidden (Unusable next-hop).

На самом деле, в Junos зашит хардкод на фоллбек на LDP, но нам он ни к месту. 
```
vvenglovskii-nocauth@myt-32z1> ...icy-statement VRF_Hbf_IMPORT | display set | grep CHECK_RT_Hbf_FB
set policy-options policy-statement VRF_Hbf_IMPORT term CHECK_RT_Hbf_FB from community RT_VRF_Hbf_FB
set policy-options policy-statement VRF_Hbf_IMPORT term CHECK_RT_Hbf_FB then accept
set policy-options policy-statement VRF_Hbf_IMPORT term CHECK_RT_Hbf_FB then resolution-map Hbf_COLOR  

vvenglovskii-nocauth@myt-32z1> ...configuration policy-options resolution-map Hbf_COLOR
mode ip-color;
```

Предположим, что все ок и у нас есть вот такой туннель в состоянии Up.
```
vvenglovskii-nocauth@sas-32z1> show configuration protocols source-packet-routing source-routing-path to_myt32z4_color_10
to 10.255.0.10;
color 10;
primary {
    to_myt32z4_via_stdp1_sl {
```

Исходя из вышеупомянутой логики
```
if
  10 == 10 &&
  10.255.0.10 == 10.255.0.10
then 
  2a02:6b8:fc03::/56 NH = tunnel "to_myt32z4_via_stdp1_sl"
```

Сам туннель в арго SR-политик зовется сегмент-листом и выглядит как упорядоченный список MPLS-меток (сегментов):
```
segment-list 1 {
    admin-state enable
    segment 1 {
        mpls-label 160992
    }
    segment 2 {
        mpls-label 164322
    }
}
```

### Диагностические команды

{% list tabs %}

- Nokia

  #### Общая информация

  Саммари по всем SR-политикам можно посмотреть так, есть опция `detail`.
  Из интересного только последний столбец `ACT`, что как несложно дагадаться показывает активна SR-политика или нет.

  ```
  [/]
  A:vvenglovskii-nocauth@lab-vla-32z2# show router segment-routing sr-policies static-policy

  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ===
  SR Policy Static Policy Summary
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ===
  Policy Name              Color  EndPoint       RD        Local  Admin  ACT
  ------------------------------------------------------------------------------
  to_iva32z1_color_10      10     10.255.0.62    0         Yes    Up     Yes
  to_iva32z2_color_10      10     10.255.0.3     0         Yes    Up     Yes
  to_man32z1_color_10      10     10.255.0.15    0         Yes    Up     Yes
  to_man32z2_color_10      10     10.255.0.16    0         Yes    Up     Yes
  to_man32z3_color_10      10     10.255.0.17    0         Yes    Up     Yes
  to_man32z4_color_10      10     10.255.0.19    0         Yes    Up     Yes
  to_man32z5_color_10      10     10.255.0.20    0         Yes    Up     Yes
  to_man32z6_color_10      10     10.255.0.21    0         Yes    Up     Yes
  to_man32z7_color_10      10     10.255.0.23    0         Yes    Up     No
  to_man32z8_color_10      10     10.255.0.24    0         Yes    Up     Yes
  to_man32z9_color_10      10     10.255.0.25    0         Yes    Up     Yes
  to_myt32z1_color_10      10     10.255.0.8     0         Yes    Up     Yes
  to_myt32z2_color_10      10     10.255.0.18    0         Yes    Up     Yes
  to_myt32z3_color_10      10     10.255.0.6     0         Yes    Up     Yes
  to_myt32z4_color_10      10     10.255.0.10    0         Yes    Up     Yes
  to_sas32z1_color_10      10     10.255.0.41    0         Yes    Up     Yes
  to_sas32z2_color_10      10     10.255.0.42    0         Yes    Up     Yes
  to_sas32z3_color_10      10     10.255.0.43    0         Yes    Up     Yes
  to_sas32z4_color_10      10     10.255.0.44    0         Yes    Up     Yes
  to_sas32z5_color_10      10     10.255.0.45    0         Yes    Up     Yes
  to_sas32z6_color_10      10     10.255.0.46    0         Yes    Up     Yes
  to_sas32z7_color_10      10     10.255.0.47    0         Yes    Up     Yes
  to_sas32z8_color_10      10     10.255.0.52    0         Yes    Up     Yes
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ===
  ```

  В детальном выводе могут быть интересны:
  `TunnelId` если нужно смотреть в LFIB
  `S-BFD State` для проверки S-BFD
  `Seg n / State` если требуется проверить, что сегменты корректно "отрезолвились".

  ```
  [/]
  A:vvenglovskii-nocauth@lab-vla-32z2# show router segment-routing sr-policies static-policy "to_man32z4_color_10" detail

  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  SR-Policies Static Policy
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  Policy Name: to_man32z4_color_10
  Admin Status    : Up                    Color           : 10
  Head End Addr   : 0.0.0.0               Endpoint Addr   : 10.255.0.19
  Preference      : 100                   BSID            : 149514
  RD              : 0

  Path Entry:
  Active          : Yes                   Owner           : static
  TunnelId        : 917511                Age             : 2061659
  Origin ASN      : 0                     Origin          : 0.0.0.0
  NumReEval       : 0                     ReEvalReason    : none
  NumActPathChange: 0                     Last Change     : 01/10/2022 15:37:19
  Maintenance Policy: S-BFD

  Path Segment Lists:
  Segment-List    : 1                     Weight          : 1
  S-BFD State     : Up                    S-BFD Transitio*: 4
  Num Segments    : 2                     Last Change     : 01/10/2022 15:36:55
    Seg 1 Label   : 160992                State           : resolved-up
    Seg 2 Label   : 164324                State           : N/A

  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  * indicates that the corresponding row element may have been truncated.
  ```

  #### RIB/FIB/LRIB/LFIB

  ##### RIB

  Все понятно без слов, есть опция `detail` для особо любопытных.
  ```
  [/]
  A:vvenglovskii-nocauth@lab-vla-32z2# show router service-name "Hbf" route-table ipv6 2a02:6b8:fc03::/56

  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  IPv6 Route Table (Service: 56860)
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  Dest Prefix[Flags]                            Type    Proto     Age        Pref
        Next Hop[Interface Name]                                    Metric
  -------------------------------------------------------------------------------
  2a02:6b8:fc03::/56                            Remote  BGP VPN   04d02h15m  170
        10.255.0.6 (tunneled:SR-Policy:917519)                       0
  2a02:6b8:fc03::/56                            Remote  BGP VPN   04d02h15m  170
        10.255.0.8 (tunneled:SR-Policy:917517)                       0
  2a02:6b8:fc03::/56                            Remote  BGP VPN   04d02h15m  170
        10.255.0.10 (tunneled:SR-Policy:917520)                      0
  2a02:6b8:fc03::/56                            Remote  BGP VPN   04d02h15m  170
        10.255.0.18 (tunneled:SR-Policy:917518)                      0
  -------------------------------------------------------------------------------
  No. of Routes: 4
  Flags: n = Number of times nexthop is repeated
        B = BGP backup route available
        L = LFA nexthop available
        S = Sticky ECMP requested
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  ```

  ##### FIB

  Все понятно без слов, есть опция `extensive` для особо любопытных. Заодно показывает сервисную метку.
  ```
  [/]
  A:vvenglovskii-nocauth@lab-vla-32z2# show router service-name "Hbf" fib 1 ip-prefix-prefix-length 2a02:6b8:fc03::/56

  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  FIB Display
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  Prefix [Flags]                                              Protocol
    NextHop
  -------------------------------------------------------------------------------
  2a02:6b8:fc03::/56                                          BGP_VPN
    10.255.0.10 (VPRN Label:524282 Transport:SR-Policy:917520)
    10.255.0.6 (VPRN Label:17 Transport:SR-Policy:917519)
    10.255.0.8 (VPRN Label:17 Transport:SR-Policy:917517)
    10.255.0.18 (VPRN Label:524282 Transport:SR-Policy:917518)
  -------------------------------------------------------------------------------
  Total Entries : 1
  -------------------------------------------------------------------------------
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  ```

  ##### LRIB
  Здесь в деталях прячется финский дьявол, если проверить SR-политику в LRIB выяснится, что она `is-over-tunnel`, то есть SR-политика - это туннель, который содержит только промежуточные хопы, внутри SR-туннеля, который содержит только последний хоп ака лупбек. `¯\_(ツ)_/¯`
  ```
  [/]
  A:vvenglovskii-nocauth@lab-vla-32z2# show router tunnel-table 10.255.0.18/32 protocol sr-policy detail

  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  Tunnel Table (Router: Base)
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  Destination      : 10.255.0.18/32
  NextHop          : 10.255.0.68 (524337, isis (0))
  NextHop Weight   : 1
  Tunnel Flags     : is-over-tunnel has-color
  Age              : 01d19h33m            Color            : 10
  CBF Classes      : (Not Specified)
  Owner            : sr-policy            Encap            : MPLS
  Tunnel ID        : 917518               Preference       : 14
  Tunnel Label     : 162322               Tunnel Metric    : 0
  Tunnel MTU       : 9040                 Max Label Stack  : 2
  -------------------------------------------------------------------------------
  Number of tunnel-table entries          : 1
  Number of tunnel-table entries with LFA : 0
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 

  [/]
  A:vvenglovskii-nocauth@lab-vla-32z2# show router tunnel-table 10.255.0.18/32 protocol isis detail

  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  Tunnel Table (Router: Base)
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  Destination      : 10.255.0.18/32
  NextHop          : 10.255.3.61
  Tunnel Flags     : entropy-label-capable
  Age              : 01d19h35m
  CBF Classes      : (Not Specified)
  Owner            : isis (0)             Encap            : MPLS
  Tunnel ID        : 524418               Preference       : 8
  Tunnel Label     : 162322               Tunnel Metric    : 210800
  Tunnel MTU       : 9044                 Max Label Stack  : 1
  -------------------------------------------------------------------------------
  Destination      : 10.255.0.18/32
  NextHop          : 10.255.3.63
  Tunnel Flags     : entropy-label-capable
  Age              : 01d19h35m
  CBF Classes      : (Not Specified)
  Owner            : isis (0)             Encap            : MPLS
  Tunnel ID        : 524418               Preference       : 8
  Tunnel Label     : 162322               Tunnel Metric    : 210800
  Tunnel MTU       : 9044                 Max Label Stack  : 1
  -------------------------------------------------------------------------------
  Number of tunnel-table entries          : 2
  Number of tunnel-table entries with LFA : 0
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  ```

  ##### LFIB

  "Чиповая" версия вышеописанных комманд. Из интересного можно подсунуть как префикс, так и TunnelId, нету детальных выводов.
  ```
  [/]
  A:vvenglovskii-nocauth@lab-vla-32z2# show router fp-tunnel-table 1 tunnel-id 917518

  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  IPv4 Tunnel Table Display

  Legend:
  label stack is ordered from bottom-most to top-most
  B - FRR Backup
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  Destination                                  Protocol         Tunnel-ID
    Lbl/SID
      NextHop                                                   Intf/Tunnel
    Lbl/SID (backup)
      NextHop   (backup)
  -------------------------------------------------------------------------------
  10.255.0.18/32                               SR-Policy         917518
    162322
      10.255.0.68                                                SR
  -------------------------------------------------------------------------------
  Total Entries : 1
  -------------------------------------------------------------------------------
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  ```

  ##### S-BFD

  Саммари по всем S-BFD сессиям, есть опция ```detail```. Из интересного:
  ```Type``` Всегда будет cpm-np, то есть Control Processing Module - Network Processor ака обрабатывается на чипе в "мозгах" (не на CPU в "мозгах")
  ```Tx/Rx Intvl``` согласованные интервалы
  ```
  [/]
  A:vvenglovskii-nocauth@lab-vla-32z2# show router bfd seamless-bfd session sr-policy

  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  Legend:
    Session Id = Interface Name | LSP Name | Prefix | RSVP Sess Name | Service Id
    wp = Working path   pp = Protecting path
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  BFD Session
  ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### ##### #### 
  Session Id                                        State      Tx Pkts    Rx Pkts
    Rem Addr/Info/SdpId:VcId                      Multipl     Tx Intvl   Rx Intvl
    Protocols                                        Type     LAG Port     LAG ID
    Loc Addr
  -------------------------------------------------------------------------------
  10.255.0.6/32                                        Up          N/A        N/A
    10.255.0.6                                          3          300        300
    srPolicy                                       cpm-np          N/A        N/A
    87.250.228.146
  10.255.0.8/32                                        Up          N/A        N/A
    10.255.0.8                                          3          300        300
    srPolicy                                       cpm-np          N/A        N/A
    87.250.228.146
  10.255.0.10/32                                       Up          N/A        N/A
    10.255.0.10                                         3          300        300
    srPolicy                                       cpm-np          N/A        N/A
    87.250.228.146
  10.255.0.15/32                                       Up          N/A        N/A
    10.255.0.15                                         3          300        300
    srPolicy                                       cpm-np          N/A        N/A
  ```

- Huawei

  #### Общая информация

  Саммари нету, есть огромная портянка. На что обратить внимание:
  ```BFD State``` для S-BFD
  ```List State``` для проверки резолва сегментов
  ```Label``` покажет весь сегмент-лист
  ```Segment-List ID ``` нужен для, кхм, S-BFD
  ```
  <lab-vla-32z1>disp sr-te policy
  PolicyName : to_iva32z2_color_10
  Endpoint             : 10.255.0.3           Color                : 10
  TunnelId             : 1                    TunnelType           : SR-TE Policy
  Binding SID          : -                    MTU                  : 9000
  Policy State         : UP                   BFD                  : Disable
  Admin State          : UP                   DiffServ-Mode        : -
  Traffic Statistics   : Enable               Backup Hot-Standby   : Disable
  Candidate-path Count : 1

  Candidate-path Preference: 100
  Path State           : Valid                Path Type            : Primary
  Protocol-Origin      : Configuration(30)    Originator           : 0, 0.0.0.0
  Discriminator        : 100                  Binding SID          : -
  GroupId              : 1                    Policy Name          : to_iva32z2_color_10
  Template ID          : -
  Segment-List Count   : 1
  Segment-List        : to_iva32z2_via_stdp1_sl
    Segment-List ID    : 78                   XcIndex              : 2000078
    List State         : UP                   BFD State            : -
    EXP                : -                    TTL                  : -
    DeleteTimerRemain  : -
    Label : 160081, 161322

  PolicyName : to_myt32z3_color_10
  Endpoint             : 10.255.0.6           Color                : 10
  TunnelId             : 2                    TunnelType           : SR-TE Policy
  Binding SID          : -                    MTU                  : 9000
  Policy State         : UP                   BFD                  : SBFD Enable
  Admin State          : UP                   DiffServ-Mode        : -
  Traffic Statistics   : Enable               Backup Hot-Standby   : Disable
  Candidate-path Count : 1

  Candidate-path Preference: 100
  Path State           : Valid                Path Type            : Primary
  Protocol-Origin      : Configuration(30)    Originator           : 0, 0.0.0.0
  Discriminator        : 100                  Binding SID          : -
  GroupId              : 2                    Policy Name          : to_myt32z3_color_10
  Template ID          : -
  Segment-List Count   : 1
  Segment-List        : to_myt32z3_via_m9p2_sl
    Segment-List ID    : 68                   XcIndex              : 2000068
    List State         : UP                   BFD State            : UP
    EXP                : -                    TTL                  : -
    DeleteTimerRemain  : -
    Label : 160992, 162323
  ```

  #### RIB/FIB/LRIB/LFIB
  ##### RIB
  N.B. V2R21 вместо безликого SR-TE Policy указывает имя SR-политики, есть ```verbose```.
  Для проверки резолва нужен TunnelID
  ```
  <lab-vla-32z1>disp ipv6 routing-table vpn-instance Hbf 2a02:6b8:fc03:: 56
  Route Flags: R - relay, D - download to fib, T - to vpn-instance, B - black hole route
  ------------------------------------------------------------------------------
  Routing Table : Hbf
  Summary Count : 4

  Destination  : 2A02:6B8:FC03::                         PrefixLength : 56
  NextHop      : ::FFFF:10.255.0.10                      Preference   : 255
  Cost         : 0                                       Protocol     : IBGP
  RelayNextHop : 0.0.0.0                                 TunnelID     : 0x000000003200000004
  Interface    : SR-TE Policy                            Flags        : RD

  Destination  : 2A02:6B8:FC03::                         PrefixLength : 56
  NextHop      : ::FFFF:10.255.0.6                       Preference   : 255
  Cost         : 0                                       Protocol     : IBGP
  RelayNextHop : 0.0.0.0                                 TunnelID     : 0x000000003200000002
  Interface    : SR-TE Policy                            Flags        : RD

  Destination  : 2A02:6B8:FC03::                         PrefixLength : 56
  NextHop      : ::FFFF:10.255.0.8                       Preference   : 255
  Cost         : 0                                       Protocol     : IBGP
  RelayNextHop : 0.0.0.0                                 TunnelID     : 0x000000003200000003
  Interface    : SR-TE Policy                            Flags        : RD

  Destination  : 2A02:6B8:FC03::                         PrefixLength : 56
  NextHop      : ::FFFF:10.255.0.18                      Preference   : 255
  Cost         : 0                                       Protocol     : IBGP
  RelayNextHop : 0.0.0.0                                 TunnelID     : 0x000000003200000008
  Interface    : SR-TE Policy                            Flags        : RD
  ```

  ##### FIB
  То же самое только по версии Solar'а. Со слов R&D Huawei "VRP is a very complex system", поэтому если в FIB'е будет не всё, то это не баг, а missing feature.
  ```
  <lab-vla-32z1>disp ipv6 fib slot 1 vpn-instance Hbf 2a02:6b8:fc03:: 56
  Route Entry Count: 4

  Destination:  2A02:6B8:FC03::                         PrefixLength : 56
  Nexthop    :  ::10.255.0.8                            Flag         : DGU
  Interface  :  SR-TE Policy                            Tunnel ID    : 0x000000003200000003
  TimeStamp  :  2022/02/03 13:25:54
  Destination:  2A02:6B8:FC03::                         PrefixLength : 56
  Nexthop    :  ::10.255.0.6                            Flag         : DGU
  Interface  :  SR-TE Policy                            Tunnel ID    : 0x000000003200000002
  TimeStamp  :  2022/02/03 13:25:54
  Destination:  2A02:6B8:FC03::                         PrefixLength : 56
  Nexthop    :  ::10.255.0.18                           Flag         : DGU
  Interface  :  SR-TE Policy                            Tunnel ID    : 0x000000003200000008
  TimeStamp  :  2022/02/03 13:25:54
  Destination:  2A02:6B8:FC03::                         PrefixLength : 56
  Nexthop    :  ::10.255.0.10                           Flag         : DGU
  Interface  :  SR-TE Policy                            Tunnel ID    : 0x000000003200000004
  TimeStamp  :  2022/02/03 13:25:54
  ```

  ##### LRIB
  Минимальная информация, просто проверить корректный резолв
  ```
  <lab-vla-32z1>disp tunnel-info 0x000000003200000008
  Tunnel ID:       0x000000003200000008
  Type:            srtepolicy
  Name:            SR-TE Policy
  Destination:     10.255.0.18
  Instance ID:     0
  MTU:             9000
  Cost:            0
  Status:          UP
  Color:           10
  Group:           0
  ```

  ##### LFIB
  TBD

  #### S-BFD
  Небольшое саммари, по ID сегмент-листа можно посмотреть ```verbose``` вывод
  ```
  <lab-vla-32z1>display bfd session all | i SID
  Info: It will take a long time if the content you search is too much or the string you input is too long, you can press CTRL_C to break.
  (w): State in WTR
  (*): State is invalid
  --------------------------------------------------------------------------------
  Local      Remote     PeerIpAddr      State     Type        InterfaceName
  --------------------------------------------------------------------------------
  16385      18000023   10.255.0.6      Up        D_SID_LIST        -
  16386      18000021   10.255.0.8      Up        D_SID_LIST        -
  16387      525024     10.255.0.10     Up        D_SID_LIST        -
  16388      17000041   10.255.0.15     Up        D_SID_LIST        -
  16389      17000042   10.255.0.16     Up        D_SID_LIST        -
  16390      17000043   10.255.0.17     Up        D_SID_LIST        -
  16391      525022     10.255.0.18     Up        D_SID_LIST        -
  16392      17000044   10.255.0.19     Up        D_SID_LIST        -
  16393      17000045   10.255.0.20     Up        D_SID_LIST        -
  16394      17000046   10.255.0.21     Up        D_SID_LIST        -
  16395      18000047   10.255.0.23     Up        D_SID_LIST        -
  16396      18000048   10.255.0.24     Up        D_SID_LIST        -
  16397      18000049   10.255.0.25     Up        D_SID_LIST        -
  16398      18000031   10.255.0.41     Up        D_SID_LIST        -
  16399      525032     10.255.0.42     Up        D_SID_LIST        -
  16400      18000033   10.255.0.43     Up        D_SID_LIST        -
  16401      525034     10.255.0.44     Up        D_SID_LIST        -
  16402      18000035   10.255.0.45     Up        D_SID_LIST        -
  16403      525036     10.255.0.46     Up        D_SID_LIST        -
  16404      18000037   10.255.0.47     Up        D_SID_LIST        -
  16405      525038     10.255.0.52     Up        D_SID_LIST        -
  --------------------------------------------------------------------------------
      Total UP/DOWN Session Number : 33/0

  <lab-vla-32z1>display bfd session segment-list 68 verbose
  (w): State in WTR
  (*): State is invalid
  --------------------------------------------------------------------------------
    State : Up                    Name : dyn_16385
  --------------------------------------------------------------------------------
    Local Discriminator    : 16385            Remote Discriminator   : 18000023
    Session Detect Mode    : Seamless Mode Without Echo Function
    BFD Bind Type          : SID_LIST
    Bind Session Type      : Dynamic
    SID_LIST Id            : 68               Color                  : 10
    Bind Peer IP Address   : 10.255.0.6
    Bind Interface         : -
    FSM Board Id           : 1                TOS-EXP                : 7
    Min Tx Interval (ms)   : 300              Min Rx Interval (ms)   : 300
    Actual Tx Interval (ms): 300              Actual Rx Interval (ms): 300
    Local Detect Multi     : 3                Detect Interval (ms)   : 900
    Echo Passive           : Disable          Acl Number             : -
    Destination Port       : 7784             TTL                    : 1
    Proc Interface Status  : Disable          Process PST            : Enable
    WTR Interval (ms)      : 1000             Config PST             : Enable
    Active Multi           : 3
    Last Local Diagnostic  : Control Detection Time Expired
    Bind Application       : SRPOLICY
    Session TX TmrID       : -                Session Detect TmrID   : -
    Session Init TmrID     : -                Session WTR TmrID      : -
    Session Echo Tx TmrID  : -
    Session Description    : -
  --------------------------------------------------------------------------------
  ```

- Juniper

  #### Общая информация

  Саммари по все SR-политикам, есть опция ```detail```
  ```
  vvenglovskii-nocauth@lab-vla-32z3> show spring-traffic-engineering lsp
  To              State     LSPname
  10.255.0.62-10<c> Up      to_iva32z1_color_10
  10.255.0.3-10<c> Up       to_iva32z2_color_10
  10.255.0.15-10<c> Up      to_man32z1_color_10
  10.255.0.16-10<c> Up      to_man32z2_color_10
  10.255.0.17-10<c> Up      to_man32z3_color_10
  10.255.0.19-10<c> Up      to_man32z4_color_10
  10.255.0.20-10<c> Up      to_man32z5_color_10
  10.255.0.21-10<c> Up      to_man32z6_color_10
  10.255.0.23-10<c> Down    to_man32z7_color_10
  10.255.0.24-10<c> Up      to_man32z8_color_10
  10.255.0.25-10<c> Up      to_man32z9_color_10
  10.255.0.8-10<c> Up       to_myt32z1_color_10
  10.255.0.18-10<c> Up      to_myt32z2_color_10
  10.255.0.6-10<c> Up       to_myt32z3_color_10
  10.255.0.10-10<c> Up      to_myt32z4_color_10
  10.255.0.41-10<c> Up      to_sas32z1_color_10
  10.255.0.42-10<c> Up      to_sas32z2_color_10
  10.255.0.43-10<c> Up      to_sas32z3_color_10
  10.255.0.44-10<c> Up      to_sas32z4_color_10
  10.255.0.45-10<c> Up      to_sas32z5_color_10
  10.255.0.46-10<c> Up      to_sas32z6_color_10
  10.255.0.47-10<c> Up      to_sas32z7_color_10
  10.255.0.52-10<c> Up      to_sas32z8_color_10


  Total displayed LSPs: 23 (Up: 22, Down: 1)
  ```

  В детальном выводе из интересного:
  ```BFD status / BFD name```, чтобы глянуть глянуть внутренее имя BFD-сессии
  ```Hop``` для проверки сегментов
  ```
  Name: to_man32z1_color_10
    Tunnel-source: Static configuration
    To: 10.255.0.15-10<c>
    State: Up
    Telemetry statistics:
    Sensor-name: 10.255.0.15-a, Id: 3758096390
    Sensor-name: ::ffff:10.255.0.15-a, Id: 3758096391
      Path: to_man32z1_via_m9p2_sl
      Outgoing interface: NA
      Auto-translate status: Disabled Auto-translate result: N/A
      Compute Status:Disabled , Compute Result:N/A , Compute-Profile Name:N/A
      BFD status: Up BFD name: V4-srte_bfd_session-2
      ERO Valid: true
        SR-ERO hop count: 2
          Hop 1 (Loose):
            NAI: None
            SID type: 20-bit label, Value: 160992
          Hop 2 (Loose):
            NAI: None
            SID type: 20-bit label, Value: 164321
  ```

  #### RIB/FIB/LRIB/LFIB
  ##### RIB
  Куча полезной информации:
  ```Indr Composite``` чтобы узнать сервисную метку
  ```Krt_inh / PNH``` показывает через что зарезолвился префикс, где `<c>` - это color, а `<c6>` - color6 
  ```
  vvenglovskii-nocauth@lab-vla-32z3> show route table Hbf.inet6.0 2a02:6b8:fc03::/56 active-path detail expanded-nh

  Hbf.inet6.0: 503 destinations, 9385 routes (481 active, 0 holddown, 747 hidden)
  2a02:6b8:fc03::/56 (13 entries, 2 announced)
          State: <CalcForwarding>
  Installed-nexthop:
  List (0xd53d79c) Index:2097457 Push 17
    Indr Composite (0x11475adc) ::ffff:10.255.0.6-10<c6> Push 17
      Krt_cnh (0xe344d28) Index:736 Push 17
        Krt_inh (0x512bd08) Index:2097183 PNH: ::ffff:10.255.0.6-10<c6>
          Chain (0x11e65f1c) Index:1267 Push 162323
            Frr_inh (0x11e64e9c) Index:2097441 PNH: 160992
              List (0x623231c) Index:2097324 Swap 160992
                Chain (0x104ad3dc) Index:1900 Swap 160992
                  Router (0x11e26cdc) Index:665 10.255.3.113 Session-ID: 0x234 via ae102.10
                Chain (0x10e3d9dc) Index:1009 Swap 160992
                  Router (0xd467d1c) Index:702 10.255.3.89 Session-ID: 0x236 via ae101.10
    Indr Composite (0x11e473dc) ::ffff:10.255.0.8-10<c6> Push 17
      Krt_cnh (0x238548f0) Index:1286 Push 17
        Krt_inh (0x513be88) Index:2097566 PNH: ::ffff:10.255.0.8-10<c6>
          Chain (0x11e6501c) Index:1270 Push 162321
            Frr_inh (0x11e64e9c) Index:2097441 PNH: 160992
              List (0x623231c) Index:2097324 Swap 160992
                Chain (0x104ad3dc) Index:1900 Swap 160992
                  Router (0x11e26cdc) Index:665 10.255.3.113 Session-ID: 0x234 via ae102.10
                Chain (0x10e3d9dc) Index:1009 Swap 160992
                  Router (0xd467d1c) Index:702 10.255.3.89 Session-ID: 0x236 via ae101.10
    Indr Composite (0x1164609c) ::ffff:10.255.0.10-10<c6> Push 524282
      Krt_cnh (0x1470bca0) Index:2132 Push 524282
        Krt_inh (0x50cb908) Index:2097473 PNH: ::ffff:10.255.0.10-10<c6>
          Chain (0x11e6411c) Index:1219 Push 162324
            Frr_inh (0x11e3d7dc) Index:2097440 PNH: 160081
              List (0x622891c) Index:2097214 Swap 160081
                Chain (0x11e650dc) Index:1843 Swap 160081
                  Router (0x11e26cdc) Index:665 10.255.3.113 Session-ID: 0x234 via ae102.10
                Chain (0x104e15dc) Index:819 Swap 160081
                  Router (0xd467d1c) Index:702 10.255.3.89 Session-ID: 0x236 via ae101.10
    Indr Composite (0x1166ffdc) ::ffff:10.255.0.18-10<c6> Push 524282
      Krt_cnh (0xf048cd8) Index:1197 Push 524282
        Krt_inh (0x9165e08) Index:2097220 PNH: ::ffff:10.255.0.18-10<c6>
          Chain (0x11e6fd5c) Index:1156 Push 162322
            Frr_inh (0x11e3d7dc) Index:2097440 PNH: 160081
              List (0x622891c) Index:2097214 Swap 160081
                Chain (0x11e650dc) Index:1843 Swap 160081
                  Router (0x11e26cdc) Index:665 10.255.3.113 Session-ID: 0x234 via ae102.10
                Chain (0x104e15dc) Index:819 Swap 160081
                  Router (0xd467d1c) Index:702 10.255.3.89 Session-ID: 0x236 via ae101.10
  ```

  ##### LRIB
  Очередная таблица в Junos... Точнее, даже две. К слову, и SR-TE, и SR-Policy помечается как SPRING-TE, уот так уот.
  ```
  vvenglovskii-nocauth@lab-vla-32z3> show route table inet6color.0

  inet6color.0: 22 destinations, 22 routes (22 active, 0 holddown, 0 hidden)
  + = Active Route, - = Last Active, * = Both

  ::ffff:10.255.0.3-10<c6>/160
                    *[SPRING-TE/8] 1d 20:10:04, metric 1, metric2 210800
                        to 10.255.3.89 via ae101.10, Push 161322, Push 160081(top)
                      >  to 10.255.3.113 via ae102.10, Push 161322, Push 160081(top)
  ::ffff:10.255.0.6-10<c6>/160
                    *[SPRING-TE/8] 1d 20:10:04, metric 1, metric2 210800
                        to 10.255.3.89 via ae101.10, Push 162323, Push 160992(top)
                      >  to 10.255.3.113 via ae102.10, Push 162323, Push 160992(top)
  ::ffff:10.255.0.8-10<c6>/160
                    *[SPRING-TE/8] 1d 20:10:04, metric 1, metric2 210800
                      >  to 10.255.3.89 via ae101.10, Push 162321, Push 160992(top)
                        to 10.255.3.113 via ae102.10, Push 162321, Push 160992(top)
  ::ffff:10.255.0.10-10<c6>/160
                    *[SPRING-TE/8] 1d 20:10:04, metric 1, metric2 210800
                      >  to 10.255.3.89 via ae101.10, Push 162324, Push 160081(top)
                        to 10.255.3.113 via ae102.10, Push 162324, Push 160081(top)
  ::ffff:10.255.0.15-10<c6>/160
                    *[SPRING-TE/8] 1d 20:10:04, metric 1, metric2 212200
                      >  to 10.255.3.89 via ae101.10, Push 164321, Push 160992(top)
                        to 10.255.3.113 via ae102.10, Push 164321, Push 160992(top)
  ::ffff:10.255.0.16-10<c6>/160
                    *[SPRING-TE/8] 1d 20:10:04, metric 1, metric2 212200
                        to 10.255.3.89 via ae101.10, Push 164322, Push 160081(top)
                      >  to 10.255.3.113 via ae102.10, Push 164322, Push 160081(top)
  ```

  ##### FIB/LFIB
  Нечитаемая портянка, как обычно.
  ```
  vvenglovskii-nocauth@lab-vla-32z3> show route forwarding-table destination 2a02:6b8:fc03::/56 table Hbf extensive
  Routing table: Hbf.inet6 [Index 1799]
  Internet6:

  Destination:  2a02:6b8:fc03::/56
    Route type: user
    Route reference: 0                   Route interface-index: 0
    Multicast RPF nh index: 0
    P2mpidx: 0
    Flags: sent to PFE, rt nh decoupled
    Next-hop type: unilist               Index: 2097457  Reference: 12
    Nexthop:
    Next-hop type: composite             Index: 736      Reference: 2
    Load Balance Label: Push 17, None
    Next-hop type: indirect              Index: 2097183  Reference: 2
                                      Weight: 0x0
    Nexthop:
    Next-hop type: composite             Index: 1267     Reference: 2
    Load Balance Label: Push 162323, None
    Next-hop type: indirect              Index: 2097441  Reference: 8
                                      Weight: 0x0
    Next-hop type: unilist               Index: 2097324  Reference: 3
    Nexthop:
    Next-hop type: composite             Index: 1900     Reference: 2
    Load Balance Label: Swap 160992, None
    Nexthop: 10.255.3.113
    Next-hop type: unicast               Index: 665      Reference: 56
    Next-hop interface: ae102.10      Weight: 0x0
    Nexthop:
    Next-hop type: composite             Index: 1009     Reference: 2
    Load Balance Label: Swap 160992, None
    Nexthop: 10.255.3.89
    Next-hop type: unicast               Index: 702      Reference: 51
    Next-hop interface: ae101.10      Weight: 0x0
    Nexthop:
    Next-hop type: composite             Index: 1286     Reference: 2
    Load Balance Label: Push 17, None
    Next-hop type: indirect              Index: 2097566  Reference: 2
                                      Weight: 0x0
  ```

  ##### S-BFD
  Небольшое саммари, есть ```detail``` со всякими подробностями
  ```
  vvenglovskii-nocauth@lab-vla-32z3> show spring-traffic-engineering sbfd
  BFDname                  State
  V4-srte_bfd_session-22   Up
  V4-srte_bfd_session-2    Up
  V4-srte_bfd_session-11   Up
  V4-srte_bfd_session-3    Up
  V4-srte_bfd_session-12   Up
  V4-srte_bfd_session-4    Up
  V4-srte_bfd_session-13   Up
  V4-srte_bfd_session-5    Up
  V4-srte_bfd_session-14   Up
  V4-srte_bfd_session-6    Up
  V4-srte_bfd_session-7    Up
  V4-srte_bfd_session-8    Down
  V4-srte_bfd_session-9    Up
  V4-srte_bfd_session-10   Up
  V4-srte_bfd_session-15   Up
  V4-srte_bfd_session-16   Up
  V4-srte_bfd_session-17   Up
  V4-srte_bfd_session-18   Up
  V4-srte_bfd_session-19   Up
  V4-srte_bfd_session-20   Up
  V4-srte_bfd_session-21   Up
  ```

{% endlist %}

## Механизм выбора между BB и FB

На PE-маршрутизаторах границе ДЦ запущено два IGP процесса: OSPFv2 и IS-IS, в каждый из которых включены соответствующие логические интерфейсы - или BB, или FB. Может быть как физическое разделение, так и логическое. На стыке z и e линки общие, используем логическое разделение по dot1Q-тегу: 
- vlan-id 1 для BB
- vlan-id 10 для FB

В каждый процесс добавлен loopback-интерфейс, кроме Juniper. На оборудовании Juniper два адреса на lo0.0, так как на Juniper нельзя сделать несколько loopback.

Для того, чтобы удаленные PE, могли верно выбрать искомый интерфейс, PE анонсирует префиксы, добавляя уникальный атрибут Next Hop, равный [IPv6 IPv4-mapped](https://tools.ietf.org/html/rfc4291#section-2.5.5) адресу loopback-интерфейса в зависимости от BGP-community маршрута - `::FFFF:<BB IPv4 loopback>` или `::FFFF:<FB IPv4 loopback>`.

_Пример политики:_
```
<vla-32z2>dis cu int LoopBack
#
interface LoopBack0
 ip address 87.250.228.167 255.255.255.255
#
interface LoopBack10
 ip address 10.255.0.1 255.255.255.255
 isis enable 1
 isis prefix-sid index 5322
#
return
<vla-32z2>dis cu configuration route-policy SET_VPN_NHOP
#
route-policy SET_VPN_NHOP permit node 10
 if-match community-filter REANNOUNCE_COMMUNITY
 if-match extcommunity-filter MATCH_VPN_COMM_BB
 apply ipv6 next-hop ::FFFF:87.250.228.167
#
route-policy SET_VPN_NHOP permit node 20
 if-match community-filter REANNOUNCE_COMMUNITY
 if-match extcommunity-filter MATCH_VPN_COMM_FB
 apply ipv6 next-hop ::FFFF:10.255.0.1
 apply extcommunity color 0:10
#
route-policy SET_VPN_NHOP permit node 30
 if-match ipv6 address prefix-list PFXS_SPECIALv6
 if-match community-filter TOR_ANYCAST_COMMUNITY
 if-match extcommunity-filter MATCH_VPN_COMM_BB
 apply ipv6 next-hop ::FFFF:87.250.228.167
#
route-policy SET_VPN_NHOP permit node 40
 if-match ipv6 address prefix-list PFXS_YANDEX_TUN64_ANYCASTv6
 if-match community-filter TOR_ANYCAST_COMMUNITY
 if-match extcommunity-filter MATCH_VPN_COMM_BB
 apply as-path 65401 additive
 apply cost 9000
 apply ipv6 next-hop ::FFFF:87.250.228.167
#
return
```

## Дизайн Route Reflector

На текущий момент имеется несколько разных типов RR: IPv4, 6PE, VPN, LUARR подробнее будет описано тут:....
