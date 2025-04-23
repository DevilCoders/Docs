# Сброник вендорных особенностей

Здесь собраны вендорные особенности, с которыми мы столкнулись во время разработки и интеграции Susanin.

## Cisco
Где | Что | Объяснение
:--- | :--- | :---
PCEP | В OPEN приходит неизвестный Association type: **20** | Соответствует [P2MP SR Policy Association Type](https://datatracker.ietf.org/doc/html/draft-hsd-pce-sr-p2mp-policy-03#section-4.1.2). Стандарт находит в состоянии **draft**, поэтому пока присвоено такое значение
 PCEP | В PCRpt приходит Vendor-Information Object [[RFC7470]](https://datatracker.ietf.org/doc/html/rfc7470#page-7) | The Vendor Information TLV can be used to carry vendor-specific information that applies to a specific PCEP object by including the TLV in the object. The PCE determines how to interpret the Vendor Information TLV by examining the Enterprise Number it contains.  If the Enterprise Number is unknown to the PCE, it MUST treat the Vendor Information TLV as an unknown TLV and handle it as described in [[RFC5440]](https://datatracker.ietf.org/doc/html/rfc5440). В общем, если контроллер знает что делать с этой информацией - пусть делает, если не знает - пусть игнорирует.
SR-Policy via BGP | `RouteTarget` обязателен | `RouteTarget` для Cisco должен быть всегда представлен и должен указывать на `headend`, даже если `BGP Update` отправляется напрямую в `headend`. Формат `RouteTarget`: `<headend>:color`
SR-Policy via BGP | SRLB по умолчанию для IOS-XR: 15000 – 15999 (возможна переконфигурация) | Для РСЕ Cisco рекомендовано использовать BGP-LS для сбора информации о SRLB с устройств

## Juniper
Где | Что | Объяснение
:--- | :--- | :---
PCEP | В OPEN приходит неизвестный Association type: **65505** | Соответствует [SR Policy Association Type](https://datatracker.ietf.org/doc/html/draft-ietf-pce-segment-routing-policy-cp-05#section-7.1). Значение взято до стандартизации и должно быть заменено в будущем.
SR-Policy via BGP | SRLB = 1000000-1048575 | SRLB выделяется из диапазона статических меток. TODO: проверить корректность интепретации `BSID` из этого диапазона на JUNOS
PCEP | Используются кастомные значения для `SRPOLICY-POL-ID`, `SRPOLICY-CPATH-ID` и `SRPOLICY-CPATH-PREFERENCE` | Эти TLV были введены в [PCEP extension to support Segment Routing Policy Candidate Paths](https://datatracker.ietf.org/doc/html/draft-barth-pce-segment-routing-policy-cp-06), который находится в стадии draft'а, а соответствующие значения описаны как TBD. Juniper использует следующие значения: `SRPOLICY-POL-ID`=`65507`, `SRPOLICY-CPATH-ID`=`65508` и `SRPOLICY-CPATH-PREFERENCE`=`65509`.

## Nokia
Где | Что | Объяснение
:--- | :--- | :---
PCEP | В OPEN приходят неизвестные TLV (101,113,114) | Как выяснилось, они значат следующее: `101` - `PATH-PROFILE-CAPABILITY TLV` – **Internal / Proprietary**. These two are carried in the Open Object but they will likely change when Association Objects and Multipath get fully implemented in SROS :`103` - `ASSOC-Type-List TLV` - **Internal / Proprietary**, `114` - `Multipath Capability TLV` - **Internal / Proprietary**
SR-Policy via BGP | SRLB назначается динамически путем определения т.н. reserved block из диапазона динамических меток: 18432-524287 | TODO: проверить корректность интепретации BSID из этого диапазона на SR-OS

## Huawei
Где | Что | Объяснение
:--- | :--- | :---

## Arista
Где | Что | Объяснение
:--- | :--- | :---
PCEP | Не поддерживается |
SR-Policy via BGP | SRLB = 965536-1031071 (65536) | TODO: проверить корректность интепретации BSID из этого диапазона на vEOS
