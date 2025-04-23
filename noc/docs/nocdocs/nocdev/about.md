# Список систем NOC

В данном разделе вы сможете найти список систем NOCDEV с основной информацией по ним:
- краткое описание
- список контактов
- список полезных основных ссылок
- check-list системы

С обратной связью по этой странице обращайтесь к [Воловику Вадиму](https://staff.yandex-team.ru/vdvolovik)

--------------------

## 1. Системы Inventory


### 1.1 Racktables

Racktables - основная система инвентари, IPAM, VLAN и учета других ресурсов сетей DC, Backbone, Fastbone и Office.


#### Контакты

- **Технический менеджер**: [Прохоров Александр](https://staff.yandex-team.ru/alexprokhorov)
- **Ведущий разработчик**: [Константин Сазонов](https://staff.yandex-team.ru/moonug)


#### Check-list системы

|                                                | Status     | Links                                                                                       |
|------------------------------------------------|:----------:|:-------------------------------------------------------------------------------------------:|
| Есть UI                                        | ★          | [Interface](https://racktables.yandex-team.ru/)                                             |
| Код в аркадии                                  | ☆          | [Gitlab](https://noc-gitlab.yandex-team.ru/nocdev/racktables)                               |
| Автотесты                                      | ★          | [Gitlab Tests](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/tree/master/tests)     |
| Пользовательская (или какая-то) документация   | ★          | [RT Docs](https://docs.yandex-team.ru/racktables/)                                          |
| Легко тестировать (локально или есть стенды)   | ★          | -                                                                                           |
| Deploy без Downtime                            | ★          | -                                                                                           |
| Dashboard                                      | ★          | [Monitoring](https://monitoring.yandex-team.ru/projects/racktables/dashboards)              |
| Алерты                                         | ★          | [nocdev-rt-*](https://noc-gitlab.yandex-team.ru/nocdev/mondata/-/tree/master/kulebyaks)     |
| Деплой по кнопке                               | ☆          | [NOCDEV-6032](https://st.yandex-team.ru/NOCDEV-6032)                                        |
| Есть логи и понятно, где они                   | ★          | -                                                                                           |
| Понятный ответственный                         | ★          | [ABC](https://abc.yandex-team.ru/services/racktables/)                                      |
| Живёт -1 ДЦ                                    | ☆  (в ручном режиме) | -                                                                                 |


### 1.2 Alexandria

Сервис Alexandria создан для учёта и контроля версий программного обеспечения(далее ПО), устанавливаемого на сетеобразующее оборудование в Яндекс.

Основанием для разработки послужило желание решать следующие типы задач:

Определение типа и версии ПО для нового сетевого устройства при введении его в эксплуатацию (в т.ч. при "наливке").
Контроль версий ПО на эксплуатируемых сетевых устройствах.
Если коротко: "какой софт ставить на новую коробку, и надо ли менять софт на действующей коробке".


#### Контакты

- **Технический менеджер**: [Прохоров Александр](https://staff.yandex-team.ru/alexprokhorov)
- **Разработчик**: [Кротов Алексей](https://staff.yandex-team.ru/aykrotov)
- **Разработчик**: [Мищенко Сергей](https://staff.yandex-team.ru/smishche)

#### Check-list системы

|                                                | Status     | Links                                                                                                                 |
|------------------------------------------------|:----------:|:---------------------------------------------------------------------------------------------------------------------:|
| Есть UI                                        | ☆          | [Swagger](https://alexandria.yandex-team.ru/swaggerui/)                                                               |
| Код в аркадии                                  | ★          | [Repo](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria)                                                     |
| Автотесты                                      | ★          | -                                                                                                                     |
| Пользовательская (или какая-то) документация   | ★          | [Docs](https://docs.yandex-team.ru/alexandria/)                                                                       |
| Легко тестировать (локально или есть стенды)   | ★          | [Diff CI](https://docs.yandex-team.ru/alexandria/repository/ci) [cmd](https://docs.yandex-team.ru/alexandria/hld/cli) |
| Deploy без Downtime                            | ★          | [Release](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Falexandria&id=alexandria-release)   |
| Dashboard                                      | ☆          | -                                                                                                                     |
| Алерты                                         | ☆          | [Только из Deploy](https://deploy.yandex-team.ru/stages/Alexandria-prod/monitoring)                                   |
| Деплой по кнопке                               | ★          | [Release](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Falexandria&id=alexandria-release)   |
| Есть логи и понятно, где они                   | ★          | [Deploy](https://deploy.yandex-team.ru/stages/Alexandria-prod/logs?deploy-unit=Alexandria-prod-du)                    |
| Понятный ответственный                         | ★          | -                                                                                                                     |
| Живёт -1 ДЦ                                    | ★          | -                                                                                                                     |


### 1.3. CMDB

Сервис CMDB предназначен для хранения информации о физических и логических стыках с операторами связи.


#### Контакты

- **Технический менеджер**: [Андрей Василенков](https://staff.yandex-team.ru/indigo)
- **Ведущий разработчик**: [Григорий Бородин](https://staff.yandex-team.ru/grihabor)


#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | [CMDB:Docs](https://wiki.yandex-team.ru/users/grihabor/cmdb/)         |
| Месторасположение кода        | [CMDB:Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/cmdb)   |
| Форма в ST                    | [STRMTODO](https://st.yandex-team.ru/STRMTODO/)                       |


#### Check-list системы

|                                                | CMDB       |
|------------------------------------------------|:----------:|
| Код в аркадии                                  | ★          |
| Автотесты                                      | ☆          |
| Пользовательская (или какая-то) документация   | ★          |
| Легко тестировать (локально или есть стенды)   | ☆          |
| Deploy без Downtime                            | ☆          |
| Dashboard                                      | ☆          |
| Алерты                                         | ☆          |
| Деплой по кнопке                               | ★          |
| Есть логи и понятно, где они                   | ☆          |
| Понятный ответственный                         | ★          |
| Живёт -1 ДЦ                                    | ☆          |


### 1.4 Netbox

Сервис Netbox - это инвентарная система и система учёта IP-пространства в Netinfra Yandex.Cloud.


#### Контакты

- **Технический менеджер**: Марат Сибгатулин [eucariot@](https://staff.yandex-team.ru/eucariot)
- **Ведущий разработчик**: Марат Сибгатулин [eucariot@](https://staff.yandex-team.ru/eucariot)


#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | [Netbox:UI](http://netbox.cloud.yandex.net/)                          |
| Дашбоард                      | - Не планируется -                                                    |
| Пользовательская документация | [Netbox:Docs](https://wiki.yandex-team.ru/cloud/devel/netinfra/netbox/) |
| Месторасположение кода        | [Netbox:Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/cmdb) |
| Форма в ST                    | - Не определена -                                                     |


#### Check-list системы

|                                                | Alexandria |
|------------------------------------------------|:----------:|
| Код в аркадии                                  | ☆          |
| Автотесты                                      | ☆          |
| Пользовательская (или какая-то) документация   | ★          |
| Легко тестировать (локально или есть стенды)   | ☆          |
| Deploy без Downtime                            | ☆          |
| Dashboard                                      | ☆          |
| Алерты                                         | ☆          |
| Деплой по кнопке                               | ☆          |
| Есть логи и понятно, где они                   | ☆          |
| Понятный ответственный                         | ★          |
| Живёт -1 ДЦ                                    | ☆          |

### 1.5. Gfglister

Сервис **gfglister** предназначен для хранения конфигурации сетевого оборудования в текстовом виде.

#### Контакты

- **Технический менеджер**: [Александр Балезин](https://staff.yandex-team.ru/gescheit)
- **Ведущий разработчик**: [Александр Балезин](https://staff.yandex-team.ru/gescheit)

#### Ссылки на систему

| Тип ссылки                    |                                   gfglister                                   |
|:-----------------------------:|:-----------------------------------------------------------------------------:|
| Пользовательский интерфейс    |                                    - CLI -                                    |
| Дашбоард                      | [dashboards](https://monitoring.yandex-team.ru/projects/gfglister/dashboards) |
| Пользовательская документация |        [docs:gfglister](https://docs.yandex-team.ru/gfglister)                |
| Месторасположение кода        |   [ARC:gfglister](https://a.yandex-team.ru/arc/trunk/arcadia/noc/gfglister)   |

#### Check-list системы

|                                                | gfglister |
|------------------------------------------------|:---------:|
| Код в аркадии                                  |     ★     |
| Автотесты                                      |     ★     |
| Пользовательская (или какая-то) документация   |     ★     |
| Легко тестировать (локально или есть стенды)   |     ☆     |
| Deploy без Downtime                            |     ☆     |
| Dashboard                                      |     ★     |
| Алерты                                         |     ☆     |
| Деплой по кнопке                               |     ★     |
| Есть логи и понятно, где они                   |     ☆     |
| Понятный ответственный                         |     ☆     |
| Живёт -1 ДЦ                                    |     ★     |

## 2. Automation


### 2.1. CK/ChK

Сервис CK/ChK - системы управления деплоя конфигурации на сетевом оборудовании и контроль конфигурации сетевого оборудования.

#### Контакты

- **Технический менеджер**: [Михаил Арефьев](https://staff.yandex-team.ru/m-arefiev)
- **Ведущий разработчик**: [Федор Жуков](https://staff.yandex-team.ru/azryve)

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | [CK/ChK:UI](https://noc.yandex-team.ru/)                              |
| Дашбоард                      | - Не планируется -                                                    |
| Пользовательская документация | [CK/ChK:Docs](https://docs.yandex-team.ru/ck/)                        |
| Месторасположение кода        | [CK/ChK:Gitlab](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck)      |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |

#### Check-list системы

|                                                | CK/ChK     |
|------------------------------------------------|:----------:|
| Код в аркадии                                  | ☆          |
| Автотесты                                      | ☆          |
| Пользовательская (или какая-то) документация   | ★          |
| Легко тестировать (локально или есть стенды)   | ☆          |
| Deploy без Downtime                            | ☆          |
| Dashboard                                      | ☆          |
| Алерты                                         | ☆          |
| Деплой по кнопке                               | ☆          |
| Есть логи и понятно, где они                   | ☆          |
| Понятный ответственный                         | ★          |
| Живёт -1 ДЦ                                    | ☆          |

### 2.2. Аннушка

Сервис Аннушка (Ann) - это система хранения и управления конфигурацией на оборудовании сети.

#### Контакты

- **Технический менеджер**: [Михаил Арефьев](https://staff.yandex-team.ru/m-arefiev)
- **Ведущий разработчик**: [Федор Жуков](https://staff.yandex-team.ru/azryve)

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - CLI -                                                               |
| Дашбоард                      | - Не планируется -                                                    |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | [Annushka:Gitlab](https://noc-gitlab.yandex-team.ru/nocdev/annushka)  |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |

#### Check-list системы

|                                                | Annushka   |
|------------------------------------------------|:----------:|
| Код в аркадии                                  | ☆          |
| Автотесты                                      | ★          |
| Пользовательская (или какая-то) документация   | ☆          |
| Легко тестировать (локально или есть стенды)   | ☆          |
| Deploy без Downtime                            | ★          |
| Dashboard                                      | ☆          |
| Алерты                                         | ☆          |
| Деплой по кнопке                               | ★          |
| Есть логи и понятно, где они                   | ★          |
| Понятный ответственный                         | ★          |
| Живёт -1 ДЦ                                    | ☆          |

### 2.3. PNS

Сервис PNS - часть Racktables отвечающая за первоначальную конфигурацию сетевых устройств

#### Контакты

- **Технический менеджер**: [Михаил Арефьев](https://staff.yandex-team.ru/m-arefiev)
- **Ведущий разработчик**: [Федор Жуков](https://staff.yandex-team.ru/azryve)

#### Ссылки на систему

| Тип ссылки                    |  PNS                                                                  |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - CLI -                                                               |
| Дашбоард                      | - Не планируется -                                                    |
| Пользовательская документация | [Wiki](https://wiki.yandex-team.ru/azryve/nalivka-debug/)             |
| Месторасположение кода        | [PNS:Gitlab](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/tree/master/switchconf)  |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |

#### Check-list системы

|                                                | PNS        |
|------------------------------------------------|:----------:|
| Код в аркадии                                  | ☆          |
| Автотесты                                      | ★          |
| Пользовательская (или какая-то) документация   | ☆          |
| Легко тестировать (локально или есть стенды)   | ☆          |
| Deploy без Downtime                            | ★          |
| Dashboard                                      | ☆          |
| Алерты                                         | ☆          |
| Деплой по кнопке                               | ★          |
| Есть логи и понятно, где они                   | ★          |
| Понятный ответственный                         | ★          |
| Живёт -1 ДЦ                                    | ☆          |

### 2.4. SDN

Сервис Susanin (SDN) - это SDN-контроллер, обеспечивающий балансировку сетевого MPLS-трафика в BackBone сети.

#### Контакты

- **Технический менеджер**: [Борис Хасанов](https://staff.yandex-team.ru/bhassanov)
- **Ведущий разработчик**: [Георгий Кириченко](https://staff.yandex-team.ru/g-e-o-r-g-y)

#### Ссылки на систему

| Тип ссылки                    |   SDN                                                                 |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - CLI -                                                               |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | [SDN:Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/susanin) |
| Форма в ST                    | - Не определена - |

#### Check-list системы

|                                                | SDN        |
|------------------------------------------------|:----------:|
| Код в аркадии                                  | ☆          |
| Автотесты                                      | ★          |
| Пользовательская (или какая-то) документация   | ★          |
| Легко тестировать (локально или есть стенды)   | ☆          |
| Deploy без Downtime                            | ★          |
| Dashboard                                      | ☆          |
| Алерты                                         | ☆          |
| Деплой по кнопке                               | ★          |
| Есть логи и понятно, где они                   | ★          |
| Понятный ответственный                         | ★          |
| Живёт -1 ДЦ                                    | ☆          |

### 2.5. Comocutor

Модуль Comocutor предназначен для унификации доступа оборудование через CLI.

#### Контакты

- **Технический менеджер**: [- Отсутствует - ](https://docs.yandex-team.ru/nocdoc/utils/404)
- **Ведущий разработчик**: [Александр Балезин](https://staff.yandex-team.ru/gescheit)

#### Ссылки на систему

| Тип ссылки                    |   Comocutor                                                           |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - CLI -                                                               |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | [Arc:Comocutor](https://a.yandex-team.ru/arc/trunk/arcadia/noc/comocutor/README.md) |
| Месторасположение кода        | [Arc:Comocutor](https://a.yandex-team.ru/arc/trunk/arcadia/noc/comocutor) |

#### Check-list системы

|                                                | Comocutor  |
|------------------------------------------------|:----------:|
| Код в аркадии                                  | ★          |
| Автотесты                                      | ★          |
| Пользовательская (или какая-то) документация   | ★          |
| Легко тестировать (локально или есть стенды)   | ☆          |
| Deploy без Downtime                            | ☆          |
| Dashboard                                      | ☆          |
| Алерты                                         | ☆          |
| Деплой по кнопке                               | ☆          |
| Есть логи и понятно, где они                   | ☆          |
| Понятный ответственный                         | ★          |
| Живёт -1 ДЦ                                    | ☆          |

### 2.6. Nalivkin

Nalivkin - новый интерфейс наливки на замену PNS. Доступен [тут](https://nalivkin.yandex-team.ru).

#### Контакты

- **Технический менеджер**: m-arefiev@
- **Ведущие разработчики**: azryve@, vladstar@

#### Check-list системы

|                                                                                                         | Nalivkin   |
|---------------------------------------------------------------------------------------------------------|:----------:|
| [Код в аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/noc/nalivkin)                                | ★          |
| Автотесты                                                                                               | ★          |
| Пользовательская (или какая-то) документация                                                            | ☆          |
| Легко тестировать (локально или есть стенды)                                                            | ★          |
| Deploy без Downtime                                                                                     | ★          |
| [Dashboard](https://monitoring.yandex-team.ru/projects/noc/dashboards/monsekf40j9a69k7gf9g)             | ★          |
| [Алерты](https://a.yandex-team.ru/arc/trunk/arcadia/noc/mondata/kulebyaks/nocdev/nocdev-nalivkin.yaml)  | ★          |
| [Деплой по кнопке](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Fnalivkin&id=nalivkin), [UI](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Fnalivkin%2Fui&id=nalivkin)                                                                                              | ★          |
| Есть логи и понятно, [где они](https://deploy.yandex-team.ru/stages/nalivkin-prod/logs)                 | ★          |
| Понятный ответственный                                                                                  | ★          |
| Живёт -1 ДЦ                                                                                             | ★          |

## 3. Security

### 3.1. Puncher - удобный дырокол для FW

#### Назначение системы

Разработанный в Яндексе инструмент для работы с доступами, включающий в себя:
- интерфейс для создания заявок на доступы
- интерфейс для подтверждения заявок и создания правил
- поиск по правилам

#### Контакты

- **Технический менеджер**: [Михаил Арефьев](https://staff.yandex-team.ru/m-arefiev)
- **Ведущий разработчик**: [Влад Старостин](https://staff.yandex-team.ru//vladstar)

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | [Puncher:UI](https://puncher.yandex-team.ru/)                         |
| Дашбоард                      | [Puncher:Dashboard](https://puncher.yandex-team.ru/)                  |
| Пользовательская документация | [Puncher:UserDocs](https://docs.yandex-team.ru/nocdoc/utils/404)      |
| Месторасположение кода        | [Puncher:Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/puncher) |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |

#### Check-list системы

|                                                                                                                        | Status  | Comment                                    |
|------------------------------------------------------------------------------------------------------------------------|:-------:|:------------------------------------------:|
| [Код в аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/noc/puncher/)                                               | ★       |                                            |
| Автотесты                                                                                                              | ★       |                                            |
| Пользовательская (или какая-то) документация                                                                           | ☆       | [Duty](https://docs.yandex-team.ru/noc-duty-docs/firewall/puncher), [cli](https://docs.yandex-team.ru/puncher/cli), [FAQ](https://wiki.yandex-team.ru/noc/nocdev/puncher/FAQ/)                             |
| Легко тестировать (локально или есть [стенды](https://puncher2-test.yandex-team.ru/))                                  | ★       | Бэкенд - `puncher-vladstar.yandex-team.ru` |
| Deploy без Downtime                                                                                                    | ★       |                                            |
| [Dashboard](https://graf.yandex-team.ru/d/eN2pjtLmz/puncher)                                                           | ★       |                                            |
| [Алерты](https://noc-gitlab.yandex-team.ru/nocdev/mondata/-/blob/master/kulebyaks/nocdev/nocdev-puncher.yaml)          | ★       |                                            |
| [Деплой по кнопке](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Fpuncher&id=puncher-release) | ★       |                                            |
| Есть логи и понятно, где они                                                                                           | ★       | `journald` на `%nocdev-puncher`            |
| [Понятный ответственный](https://abc.yandex-team.ru/services/puncher)                                                  | ★       |                                            |
| Живёт -1 ДЦ                                                                                                            | ★       |                                            |


|                                                | Status     | Links                                                                                       |
|------------------------------------------------|:----------:|:-------------------------------------------------------------------------------------------:|
| Есть UI                                        | ★          | [Interface](https://racktables.yandex-team.ru/)                                             |
| Код в аркадии                                  | ☆          | [Gitlab](https://noc-gitlab.yandex-team.ru/nocdev/racktables)                               |
| Автотесты                                      | ★          | [Gitlab Tests](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/tree/master/tests)     |
| Пользовательская (или какая-то) документация   | ★          | [RT Docs](https://docs.yandex-team.ru/racktables/)                                          |
| Легко тестировать (локально или есть стенды)   | ★          | -                                                                                           |
| Deploy без Downtime                            | ★          | -                                                                                           |
| Dashboard                                      | ★          | [Monitoring](https://monitoring.yandex-team.ru/projects/racktables/dashboards)              |
| Алерты                                         | ★          | [nocdev-rt-*](https://noc-gitlab.yandex-team.ru/nocdev/mondata/-/tree/master/kulebyaks)     |
| Деплой по кнопке                               | ☆          | [NOCDEV-6032](https://st.yandex-team.ru/NOCDEV-6032)                                        |
| Есть логи и понятно, где они                   | ★          | -                                                                                           |
| Понятный ответственный                         | ★          | [ABC](https://abc.yandex-team.ru/services/racktables/)                                      |
| Живёт -1 ДЦ                                    | ☆  (в ручном режиме) | -                                                                                 |

### 3.2. NOCAuth

#### Назначение системы

Nocauth - это инструмент, который позволяет заходить на сетевые устройства по SSH, при этом доступы настраиваются через IDM, а не на каждом устройстве по отдельности.

#### Команда

- **Технический менеджер**: - Отсутствует -
- **Ведущий разработчик**: Влад Старостин (vladstar@)

#### Ссылки на систему

| Тип ссылки                    |                                                                           |
|:-----------------------------:|:-------------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                           |
| Дашбоард                      | - Отсутствует -                                                           |
| Пользовательская документация | [NOCAuth:Docs](https://docs.yandex-team.ru/nocdoc/nocdev/nocauth/about)   |
| Месторасположение кода        | [NOCAuth:Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/nocauth) |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |

#### Check-list системы

|                                                | NOCAuth |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ★       |
| Автотесты                                      | ☆       |
| Пользовательская (или какая-то) документация   | ☆       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ☆       |
| Dashboard                                      | ☆       |
| Алерты                                         | ☆       |
| Деплой по кнопке                               | ☆       |
| Есть логи и понятно, где они                   | ☆       |
| Понятный ответственный                         | ★       |
| Живёт -1 ДЦ                                    | ★       |

### 3.3. HBF
#### Назначение системы
HBF - или Host Based Firewall - представляет собой сервер генерации фаервольных правил для раздачи конечным потребителям.

#### Команда
- **Технический менеджер**: [Евгений Сафронов](https://staff.yandex-team.ru/esafronov)
- **Ведущий разработчик**: [Евгений Сафронов](https://staff.yandex-team.ru/esafronov)

#### Ссылки на систему
| Тип ссылки                    |                                                                           |
|:-----------------------------:|:-------------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                           |
| Дашбоард                      | - Отсутствует -                                                           |
| Пользовательская документация | [HBF:Docs](https://wiki.yandex-team.ru/noc/newnetwork/hbf)                |
| Месторасположение кода        | [HBF:Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/hbf-server)  |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |

#### Check-list системы
|                                                | HBF     | Links                                                                   |
|------------------------------------------------|:-------:|:-----------------------------------------------------------------------:|
| Есть UI                                        | ☆       | -                                                                       |
| Код в аркадии                                  | ★       | [Repo](https://a.yandex-team.ru/arc/trunk/arcadia/noc/hbf-server)       |
| Автотесты                                      | ★       | [Repo](https://a.yandex-team.ru/arc/trunk/arcadia/noc/hbf-server/tests) |
| Пользовательская (или какая-то) документация   | ★       | [Wiki](https://wiki.yandex-team.ru/noc/newnetwork/hbf)                  |
| Легко тестировать (локально или есть стенды)   | ★       | [Conductor](https://c.yandex-team.ru/groups/nocdev-test-hbf)            |
| Deploy без Downtime                            | ★       | -                                                                       |
| Dashboard                                      | ★       | [Monitoring](https://monitoring.yandex-team.ru/projects/noc/dashboards/monu5n9d33if0fj78v6r?range=1d&refresh=60&p.group%5B0%5D=%2A&p.dc%5B0%5D=all&p.host%5B0%5D=all&p.Host%5B0%5D=all&p.method%5B0%5D=%2A) |
| Алерты                                         | ★       | -                                                                       |
| Деплой по кнопке                               | ★       | [CI](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Fhbf-server&id=hbf-release) |
| Есть логи и понятно, где они                   | ★       | -                                                                       |
| Понятный ответственный                         | ★       | -                                                                       |
| Живёт -1 ДЦ                                    | ★       | -                                                                       |

### 3.4. Firewall (Topka)

#### Назначение системы
Topka - представляет собой сервис выкатки фаервольных правил в датацентры для передачи в HBF.

#### Команда
- **Технический менеджер**: [Евгений Сафронов](https://staff.yandex-team.ru/esafronov)
- **Ведущий разработчик**: [Евгений Сафронов](https://staff.yandex-team.ru/esafronov)

#### Ссылки на систему
| Тип ссылки                    |                                                                           |
|:-----------------------------:|:-------------------------------------------------------------------------:|
| Пользовательский интерфейс    | [Topka:UI](https://firewall.yandex-team.ru)                               |
| Дашбоард                      | [Topka:Dashboard](https://firewall.yandex-team.ru)                        |
| Пользовательская документация | [Topka:Duty:Docs](https://docs.yandex-team.ru/noc-duty-docs/firewall/topka) и [Topka:Drills:Docs](https://docs.yandex-team.ru/topka-drills-doc) |
| Месторасположение кода        | [Topka:Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/topka)     |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |

#### Check-list системы
|                                                | HBF     | Links                                                           |
|------------------------------------------------|:-------:|:---------------------------------------------------------------:|
| Есть UI                                        | ★       | [UI](https://firewall.yandex-team.ru)                           |
| Код в аркадии                                  | ★       | [Repo](https://a.yandex-team.ru/arc/trunk/arcadia/noc/topka)    |
| Автотесты                                      | ☆       | -                                                               |
| Пользовательская (или какая-то) документация   | ★       | [Topka:Duty:Docs](https://docs.yandex-team.ru/noc-duty-docs/firewall/topka) и [Topka:Drills:Docs](https://docs.yandex-team.ru/topka-drills-doc) |
| Легко тестировать (локально или есть стенды)   | ★       | [Conductor](https://c.yandex-team.ru/groups/nocdev-test-packfw) |
| Deploy без Downtime                            | ★       | -                                                               |
| Dashboard                                      | ★       | [Monitoring](https://monitoring.yandex-team.ru/projects/topka/explorer/queries?from=now-1d&to=now&refresh=60000&q.0.s=%7Bproject%3D%22topka%22%7D&normz=off&colors=auto&type=auto&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg) |
| Алерты                                         | ★       | -                                                               |
| Деплой по кнопке                               | ★       | [CI:Backend](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Ftopka&id=topka-release) и [CI:UI](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Ftopka&id=topka-ui-release) |
| Есть логи и понятно, где они                   | ★       | -                                                               |
| Понятный ответственный                         | ★       | -                                                               |
| Живёт -1 ДЦ                                    | ★       | -                                                               |


## 4. Monitoring

### 4.1. Mondata

Mondata и кулебяки - генератор проверок в solomon и juggler.
| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Дашбоард                      | [Mondata:Dashboard](https://juggler.yandex-team.ru/dashboards/kulebyaks) |
| Пользовательская документация | [Mondata:Docs](https://a.yandex-team.ru/svn/trunk/arcadia/noc/mondata/README.md)               |
| Месторасположение кода        | [Mondata:Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/mondata) |


### 4.2. Heatmap

Heatmap - это сервис алертов по событиям на сети.

#### Контакты

- **Технический менеджер**: Прохоров Александр [alexprokhorov@](https://staff.yandex-team.ru/alexprokhorov)
- **Ведущий разработчик**: Александр Балезин [gescheit@](https://staff.yandex-team.ru/gescheit)

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | [Heatmap:UI](https://heat.yandex-team.ru)                             |
| Дашбоард                      | [Heatmap:Dashboard](https://monitoring.yandex-team.ru/projects/racktables/dashboards) |
| Пользовательская документация | [Heatmap:Docs](https://docs.yandex-team.ru/racktables/)               |
| Месторасположение кода        | [Heatmap:GitLab](https://noc-gitlab.yandex-team.ru/nocdev/racktables) |
| Форма в ST                    | [Heatmap](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |

#### Check-list системы

|                                                | Heatmap |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ☆       |
| Автотесты                                      | ★       |
| Пользовательская (или какая-то) документация   | ★       |
| Легко тестировать (локально или есть стенды)   | ★       |
| Deploy без Downtime                            | ★       |
| Dashboard                                      | ★       |
| Алерты                                         | ★       |
| Деплой по кнопке                               | ★       |
| Есть логи и понятно, где они                   | ★       |
| Понятный ответственный                         | ★       |
| Живёт -1 ДЦ                                    | ☆  (в ручном режиме) |


### 4.3 Netmon

Netmon - это агент мониторинга качества сети. Разрабатывается командой Netmon не связанной с NOCDEV.

#### Команда

- **Менеджер со стороны NOC** - [Александр Азимов](https://staff.yandex-team.ru/mitradir)
- **Команда ABC** - [https://abc.yandex-team.ru/services/netmon/](https://abc.yandex-team.ru/services/netmon/)

### 4.4 Dr.Egress

Dr.Egress - это система мониторинга внешних сетевых стыков.

#### Команда

- **Технический менеджер**: Александр Азимов [mitradir@](https://staff.yandex-team.ru/mitradir)
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | Dr.Egress |
|------------------------------------------------|:---------:|
| Код в аркадии                                  | ☆         |
| Автотесты                                      | ☆         |
| Пользовательская (или какая-то) документация   | ☆         |
| Легко тестировать (локально или есть стенды)   | ☆         |
| Deploy без Downtime                            | ☆         |
| Dashboard                                      | ☆         |
| Алерты                                         | ☆         |
| Деплой по кнопке                               | ☆         |
| Есть логи и понятно, где они                   | ☆         |
| Понятный ответственный                         | ☆         |
| Живёт -1 ДЦ                                    | ☆         |

### 4.5 Grad

Grad - это система сбора метрик с сетевого оборудования средствами SNMP, CLI, Telemetry и др.

#### Команда

- **Технический менеджер**: - [Кирилл Глушенков](https://staff.yandex-team.ru/kglushen)
- **Ведущий разработчик**: [Александр Балезин](https://staff.yandex-team.ru/gescheit)


#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | [Grad:Wiki](https://wiki.yandex-team.ru/noc/product/grad/)            |
| Месторасположение кода        | [Grad:Gitlab](https://noc-gitlab.yandex-team.ru/nocdev/grad)          |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |


#### Check-list системы

|                                                | Grad    |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ☆       |
| Автотесты                                      | ★       |
| Пользовательская (или какая-то) документация   | ☆       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ★       |
| Dashboard                                      | ☆       |
| Алерты                                         | ★       |
| Деплой по кнопке                               | ★       |
| Есть логи и понятно, где они                   | ★       |
| Понятный ответственный                         | ★       |
| Живёт -1 ДЦ                                    | ★       |


### 4.6 Linkeye

Linkeye - это сервис мониторинга состояния портов и интерфейсов на сетевом оборудовании.

#### Команда

- **Технический менеджер**: - Кирилл Глушенков [kglushen@](https://staff.yandex-team.ru/kglushen)
- **Ведущий разработчик**: Влад Старостин [vladstar@](https://staff.yandex-team.ru/vladstar)

#### Ссылки на систему

| Тип ссылки                    |                                                                           |
|:-----------------------------:|:-------------------------------------------------------------------------:|
| Пользовательский интерфейс    | [Linkeye:UI](https://linkeye.yandex-team.ru/)                             |
| Дашбоард                      | [Linkeye:Moninor](https://graf.yandex-team.ru/d/000013049/linkeye?orgId=1)|
| Пользовательская документация | [Linkeye:UserDocs](https://wiki.yandex-team.ru/noc/product/linkeye/)      |
| Месторасположение кода        | [Linkeye:Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/nocauth) |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |

#### Check-list системы

|                                                | Linkeye |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ★       |
| Автотесты                                      | ☆       |
| Пользовательская (или какая-то) документация   | ☆       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ☆       |
| Dashboard                                      | ☆       |
| Алерты                                         | ☆       |
| Деплой по кнопке                               | ☆       |
| Есть логи и понятно, где они                   | ☆       |
| Понятный ответственный                         | ★       |
| Живёт -1 ДЦ                                    | ★       |

### 4.7 Natasha

Natasha - это blackbox мониторинг L3 балансировщиков.

#### Команда

- **Технический менеджер**: - Борис Литвиненко [borislitv@](https://staff.yandex-team.ru/borislitv)
- **Ведущий разработчик**: - Борис Литвиненко [borislitv@](https://staff.yandex-team.ru/borislitv)

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - [wiki](https://wiki.yandex-team.ru/traffic/l3-monitoring/#natasha)  |
| Месторасположение кода        | - [arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/mds/natasha)   |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | Natasha |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ★       |
| Автотесты                                      | ★       |
| Пользовательская (или какая-то) документация   | ★       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ★       |
| Dashboard                                      | ☆       |
| Алерты                                         | ★       |
| Деплой по кнопке                               | ☆       |
| Есть логи и понятно, где они                   | ★       |
| Понятный ответственный                         | ★       |
| Живёт -1 ДЦ                                    | ★       |

### 4.8 Pahom

Pahom - это анализатор реалтайм состояний BGP сессий с быстрым HTTP API

api:
 - yttl_network_blacklist: список сетей TOR-ов у которых неполная связность
 - x_d_status: список линков X<=>D где есть проблемы (где не все BGP сессии живы)

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: Вадим Бурмакин [mocksoul@](https://staff.yandex-team.ru/mocksoul)

#### Ссылки на систему

| Тип ссылки                    |                                                                               |
|:-----------------------------:|:-----------------------------------------------------------------------------:|
| Пользовательский интерфейс    | [Swagger:Pahom API]({{service.pahom.url.api-doc}})                          |
| Дашбоард                      | [Grafana:Pahom]({{service.pahom.url.grafana}})                              |
| Пользовательская документация | - Отсутствует -                                                               |
| Месторасположение кода        | [Arcadia:noc/pahom]({{service.pahom.url.arcadia}})                          |
| Форма в ST                    | - Отсутствует -                                                               |

#### Check-list системы

| Проверка                                       | Cтатус | Примечания                                                                                |
|:-----------------------------------------------|:------:|:------------------------------------------------------------------------------------------|
| Код в аркадии                                  |   ★    | [Arcadia:noc/pahom]({{service.pahom.url.arcadia}})                                      |
| Автотесты                                      |   ☆    |                                                                                           |
| Пользовательская (или какая-то) документация   |   ☆    |                                                                                           |
| Легко тестировать (локально или есть стенды)   |   ☆    |                                                                                           |
| Deploy без Downtime                            |   ★    | [SLB]({{service.pahom.url.api}})                                                        |
| Dashboard                                      |   ★    | [Grafana:Pahom]({{service.pahom.url.grafana}})                                          |
| Алерты                                         |   ★    | [Juggler]({{service.pahom.url.juggler}})                                                |
| Деплой по кнопке                               |   ★    | [CI]({{service.pahom.url.ci}}) + [Conductor]({{service.pahom.url.conductor-package}}) |
| Есть логи и понятно, где они                   |   ★    | [%nocdev-pahom]({{service.pahom.url.conductor-group}}):`/var/log/pahom/*`               |
| Понятный ответственный                         |   ★    | [mocksoul@](https://staff.yandex-team.ru/mocksoul)                                        |
| Живёт -1 ДЦ                                    |   ★    | автоматически                                                                             |

### 4.9 Zabbix

Zabbix - это ???.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | Zabbix  |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ☆       |
| Автотесты                                      | ☆       |
| Пользовательская (или какая-то) документация   | ☆       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ☆       |
| Dashboard                                      | ☆       |
| Алерты                                         | ☆       |
| Деплой по кнопке                               | ☆       |
| Есть логи и понятно, где они                   | ☆       |
| Понятный ответственный                         | ☆       |
| Живёт -1 ДЦ                                    | ☆       |

### 4.10 Graphene

Graphene - это расширяемая система для построения динамических дашбордов с графиками сетевых устройств, учитывающая связи между ними и конфигурацию сети.

#### Команда

- **Технический менеджер**: Дмитрий Якубеня
- **Ведущий разработчик**: Влад Старостин (vladstar@)

#### Ссылки на систему

| Тип ссылки                    |                                                                           |
|:-----------------------------:|:-------------------------------------------------------------------------:|
| Пользовательский интерфейс    | [Graphene:UI](https://graphene.yandex-team.ru)                            |
| Дашбоард                      | - Отсутствует -                                                           |
| Пользовательская документация | [Graphene:UserDocs](https://wiki.yandex-team.ru/noc/product/graphene/)    |
| Месторасположение кода        | [Graphene:Gitlab](https://noc-gitlab.yandex-team.ru/nocdev/graphene)      |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |

#### Check-list системы

|                                                | Graphene |
|------------------------------------------------|:--------:|
| Код в аркадии                                  | ☆        |
| Автотесты                                      | ☆        |
| Пользовательская (или какая-то) документация   | ☆        |
| Легко тестировать (локально или есть стенды)   | ☆        |
| Deploy без Downtime                            | ☆        |
| Dashboard                                      | ☆        |
| Алерты                                         | ☆        |
| Деплой по кнопке                               | ☆        |
| Есть логи и понятно, где они                   | ☆        |
| Понятный ответственный                         | ☆        |
| Живёт -1 ДЦ                                    | ☆        |

### 4.11 Telegraf

Telegraf - это ???.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | Telegraf |
|------------------------------------------------|:--------:|
| Код в аркадии                                  | ☆        |
| Автотесты                                      | ☆        |
| Пользовательская (или какая-то) документация   | ☆        |
| Легко тестировать (локально или есть стенды)   | ☆        |
| Deploy без Downtime                            | ☆        |
| Dashboard                                      | ☆        |
| Алерты                                         | ☆        |
| Деплой по кнопке                               | ☆        |
| Есть логи и понятно, где они                   | ☆        |
| Понятный ответственный                         | ☆        |
| Живёт -1 ДЦ                                    | ☆        |

### 4.12 Grafana

Grafana - это ???.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | Grafana |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ☆       |
| Автотесты                                      | ☆       |
| Пользовательская (или какая-то) документация   | ☆       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ☆       |
| Dashboard                                      | ☆       |
| Алерты                                         | ☆       |
| Деплой по кнопке                               | ☆       |
| Есть логи и понятно, где они                   | ☆       |
| Понятный ответственный                         | ☆       |
| Живёт -1 ДЦ                                    | ☆       |

### 4.13 Cacti

Cacti - это ???.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | Cacti   |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ☆       |
| Автотесты                                      | ☆       |
| Пользовательская (или какая-то) документация   | ☆       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ☆       |
| Dashboard                                      | ☆       |
| Алерты                                         | ☆       |
| Деплой по кнопке                               | ☆       |
| Есть логи и понятно, где они                   | ☆       |
| Понятный ответственный                         | ☆       |
| Живёт -1 ДЦ                                    | ☆       |

### 4.14 YaTTL

YaTTL - это ???.

#### Команда

- **Технический менеджер**: [Александр Азимов](https://staff.yandex-team.ru/mitradir)
- **Ведущий разработчик**: [Александр Азимов](https://staff.yandex-team.ru/mitradir)

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | YaTTL   |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ☆       |
| Автотесты                                      | ☆       |
| Пользовательская (или какая-то) документация   | ☆       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ☆       |
| Dashboard                                      | ☆       |
| Алерты                                         | ☆       |
| Деплой по кнопке                               | ☆       |
| Есть логи и понятно, где они                   | ☆       |
| Понятный ответственный                         | ☆       |
| Живёт -1 ДЦ                                    | ☆       |

### 4.15 Megaping

Megaping - это ???.

#### Команда

- **Технический менеджер**: [Александр Азимов](https://staff.yandex-team.ru/mitradir)
- **Ведущий разработчик**: [Александр Азимов](https://staff.yandex-team.ru/mitradir)

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | Megaping |
|------------------------------------------------|:--------:|
| Код в аркадии                                  | ☆        |
| Автотесты                                      | ☆        |
| Пользовательская (или какая-то) документация   | ☆        |
| Легко тестировать (локально или есть стенды)   | ☆        |
| Deploy без Downtime                            | ☆        |
| Dashboard                                      | ☆        |
| Алерты                                         | ☆        |
| Деплой по кнопке                               | ☆        |
| Есть логи и понятно, где они                   | ☆        |
| Понятный ответственный                         | ☆        |
| Живёт -1 ДЦ                                    | ☆        |

### 4.16 Decapinger, он же "Бомж"

Decapinger - это blackbox мониторинг декапсуляторов машинами rtc.

#### Команда

- **Технический менеджер**: - Борис Литвиненко [borislitv@](https://staff.yandex-team.ru/borislitv)
- **Ведущий разработчик**: - Антон Кортунов [toshik@](https://staff.yandex-team.ru/toshik)

#### Ссылки на систему

| Тип ссылки                    |                                                                          |
|:-----------------------------:|:------------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                          |
| Дашбоард                      | - Отсутствует -                                                          |
| Пользовательская документация | - [wiki](https://wiki.yandex-team.ru/noc/product/decapinger/)            |
| Месторасположение кода        | - [arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/soft_pingers) |
| Форма в ST                    | - Отсутствует -                                                          |

#### Check-list системы

|                                                | Decapinger |
|------------------------------------------------|:----------:|
| Код в аркадии                                  | ★          |
| Автотесты                                      | ☆          |
| Пользовательская (или какая-то) документация   | ★          |
| Легко тестировать (локально или есть стенды)   | ☆          |
| Deploy без Downtime                            | ★          |
| Dashboard                                      | ☆          |
| Алерты                                         | ★          |
| Деплой по кнопке                               | ☆          |
| Есть логи и понятно, где они                   | ☆          |
| Понятный ответственный                         | ★          |
| Живёт -1 ДЦ                                    | ★          |

### noc-syslog

noc-syslog - это ???.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | noc-syslog |
|------------------------------------------------|:----------:|
| Код в аркадии                                  | ☆          |
| Автотесты                                      | ☆          |
| Пользовательская (или какая-то) документация   | ☆          |
| Легко тестировать (локально или есть стенды)   | ☆          |
| Deploy без Downtime                            | ☆          |
| Dashboard                                      | ☆          |
| Алерты                                         | ☆          |
| Деплой по кнопке                               | ☆          |
| Есть логи и понятно, где они                   | ☆          |
| Понятный ответственный                         | ☆          |
| Живёт -1 ДЦ                                    | ☆          |

### ib-mon

Мониторинг Infiniband фабрики.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: [Черноморец Сергей](https://staff.yandex-team.ru/chernomorets)

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | [wiki](https://wiki.yandex-team.ru/noc/nocdev/infiniband/)            |
| Месторасположение кода        | [gitlab](https://noc-gitlab.yandex-team.ru/nocdev/ib-mon/)            |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | ib-mon     |
|------------------------------------------------|:----------:|
| Код в аркадии                                  | ☆          |
| Автотесты                                      | ☆          |
| Пользовательская (или какая-то) документация   | *          |
| Легко тестировать (локально или есть стенды)   | ☆          |
| Deploy без Downtime                            | ☆          |
| Dashboard                                      | ☆          |
| Алерты                                         | ☆          |
| Деплой по кнопке                               | ☆          |
| Есть логи и понятно, где они                   | ☆          |
| Понятный ответственный                         | *          |
| Живёт -1 ДЦ                                    | *          |

### 4.17 snmptrapper

snmptrapper - cервис для приема SNMP trap, форматирование их в удобный вид и запись в Unified Agent для последующего хранения в YT. Так-же поддерживается вызов web-hook.


#### Команда

- **Технический менеджер**: [Александр Балезин](https://staff.yandex-team.ru/gescheit)
- **Ведущий разработчик**: [Александр Балезин](https://staff.yandex-team.ru/gescheit)


#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | [monitoring](https://monitoring.yandex-team.ru/projects/snmptrapper/dashboards/monidfmin34sek8t094o?from=now-1d&to=now&refresh=60000), [juggler](https://juggler.yandex-team.ru/dashboards/snmptrap?project=nocdev)                                                       |
| Пользовательская документация | [wiki](https://a.yandex-team.ru/arc/trunk/arcadia/noc/snmptrapper/Readme.md)            |
| Месторасположение кода        | [Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/snmptrapper/)          |
| Форма в ST                    | [NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658) |


#### Check-list системы

|                                                | Grad    |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ★       |
| Автотесты                                      | ★       |
| Пользовательская (или какая-то) документация   | ★       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ★       |
| Dashboard                                      | ★       |
| Алерты                                         | ★       |
| Деплой по кнопке                               | ★       |
| Есть логи и понятно, где они                   | ★       |
| Понятный ответственный                         | ★       |
| Живёт -1 ДЦ                                    | ★       |


### 4.18 Dr.Egress - Checker

Dr.Egress - Checker - сервис по обработке метрик мониторинга dregress'а, выявления проблем на стыках/AS и составление обходных маршрутов.

#### Команда

- **Технический менеджер**: Александр Азимов [mitradir@](https://staff.yandex-team.ru/mitradir)
- **Ведущий разработчик**: Тимур Аитов [taitov@](https://staff.yandex-team.ru/taitov)

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Дашбоард                      | - |
| Пользовательская документация | - |
| Месторасположение кода        | [Arc](https://a.yandex-team.ru/arc/trunk/arcadia/noc/dregress-checker) |

#### Check-list системы

|                                                | Status | Links |
|------------------------------------------------|:------:|:-----:|
| Код в аркадии                                  | ★ | [Repo](https://a.yandex-team.ru/arc/trunk/arcadia/noc/dregress-checker) |
| Автотесты                                      | ☆ | - |
| Пользовательская (или какая-то) документация   | ☆ | - |
| Легко тестировать (локально или есть стенды)   | ☆ | - |
| Deploy без Downtime                            | ☆ | - |
| Dashboard                                      | ☆ | - |
| Алерты                                         | ☆ | - |
| Деплой по кнопке                               | ☆ | - |
| Есть логи и понятно, где они                   | ★ | journalctl -u dregress-checker |
| Понятный ответственный                         | ☆ | - |
| Живёт -1 ДЦ                                    | ★ | - |


## 5. Other

### 5.1 L3Manager

L3Manager - это ???.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | L3Manager |
|------------------------------------------------|:---------:|
| Код в аркадии                                  | ☆         |
| Автотесты                                      | ☆         |
| Пользовательская (или какая-то) документация   | ☆         |
| Легко тестировать (локально или есть стенды)   | ☆         |
| Deploy без Downtime                            | ☆         |
| Dashboard                                      | ☆         |
| Алерты                                         | ☆         |
| Деплой по кнопке                               | ☆         |
| Есть логи и понятно, где они                   | ☆         |
| Понятный ответственный                         | ☆         |
| Живёт -1 ДЦ                                    | ☆         |

### 5.2 DynDNS

DynDNS - это ???.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | DynDNS  |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ☆       |
| Автотесты                                      | ☆       |
| Пользовательская (или какая-то) документация   | ☆       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ☆       |
| Dashboard                                      | ☆       |
| Алерты                                         | ☆       |
| Деплой по кнопке                               | ☆       |
| Есть логи и понятно, где они                   | ☆       |
| Понятный ответственный                         | ☆       |
| Живёт -1 ДЦ                                    | ☆       |

### 5.3 CDN

CDN - это ???.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | CDN     |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ☆       |
| Автотесты                                      | ☆       |
| Пользовательская (или какая-то) документация   | ☆       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ☆       |
| Dashboard                                      | ☆       |
| Алерты                                         | ☆       |
| Деплой по кнопке                               | ☆       |
| Есть логи и понятно, где они                   | ☆       |
| Понятный ответственный                         | ☆       |
| Живёт -1 ДЦ                                    | ☆       |

### 5.4 Overseer

Overseer - это система поиска пользователей, заинтересованных в работоспособности некоторого сетевого оборудования. Например, от работоспособности стоечного свича зависят все хосты, находящиеся в стойке, а значит, о его поломке захотят узнать все владельцы этих хостов. Оверсер агрегирует все знания NOC`а об устройстве сети и позволяет найти все объекты и всех пользователей, которых затрагивает поломка на том или ином устройстве. Еще оверсер умеет определять ответственных за вланы и сети, выдача во всех случаях происходит в одном и том же формате.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | [Wiki:Overseer](https://wiki.yandex-team.ru/noc/overseer/)            |
| Месторасположение кода        | [GitLab:Overseer](https://noc-gitlab.yandex-team.ru/nocdev/overseer)  |
| Форма в ST                    | - Отсутствует -                                                       |
| API                           | [https://overseer.common-int.yandex-team.ru/](https://overseer.common-int.yandex-team.ru/) |

#### Check-list системы

|                                                | Overseer |
|------------------------------------------------|:--------:|
| Код в аркадии                                  | ☆        |
| Автотесты                                      | ☆        |
| Пользовательская (или какая-то) документация   | ☆        |
| Легко тестировать (локально или есть стенды)   | ☆        |
| Deploy без Downtime                            | ☆        |
| Dashboard                                      | ☆        |
| Алерты                                         | ☆        |
| Деплой по кнопке                               | ☆        |
| Есть логи и понятно, где они                   | ☆        |
| Понятный ответственный                         | ☆        |
| Живёт -1 ДЦ                                    | ☆        |

### 5.4 Matilda

Matilda - это система учета трафика.

#### Команда

- **Технический менеджер**: - Не определен -
- **Ведущий разработчик**: - Не определен -

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Пользовательский интерфейс    | - Отсутствует -                                                       |
| Дашбоард                      | - Отсутствует -                                                       |
| Пользовательская документация | - Отсутствует -                                                       |
| Месторасположение кода        | - Отсутствует -                                                       |
| Форма в ST                    | - Отсутствует -                                                       |

#### Check-list системы

|                                                | Matilda |
|------------------------------------------------|:-------:|
| Код в аркадии                                  | ☆       |
| Автотесты                                      | ☆       |
| Пользовательская (или какая-то) документация   | ☆       |
| Легко тестировать (локально или есть стенды)   | ☆       |
| Deploy без Downtime                            | ☆       |
| Dashboard                                      | ☆       |
| Алерты                                         | ☆       |
| Деплой по кнопке                               | ☆       |
| Есть логи и понятно, где они                   | ☆       |
| Понятный ответственный                         | ☆       |
| Живёт -1 ДЦ                                    | ☆       |

### 5.5 YANET

YANET - это программный роутер основанный на DPDK. Выполняет задачи: FIREWALL, DECAP, NAT64, TUN64, L3BALANCER, DR.EGRESS и др.

#### Команда

- **Технический менеджер**: Евгений Сафронов [esafronov@](https://staff.yandex-team.ru/esafronov)
- **Ведущий разработчик**: Тимур Аитов [taitov@](https://staff.yandex-team.ru/taitov)

#### Ссылки на систему

| Тип ссылки                    |                                                                       |
|:-----------------------------:|:---------------------------------------------------------------------:|
| Дашбоард                      | [YANET](https://grafana.yandex-team.ru/d/BJnsBXbWk/yanet-common), [Общий](https://grafana.yandex-team.ru/d/ar1ALXxZz/yanet), [Capacity](https://grafana.yandex-team.ru/d/kx29LP5nk/yanet-capacity), [Firewall](https://grafana.yandex-team.ru/d/tCBS8wlGz/yanet-fw), [Dr.Egress](https://grafana.yandex-team.ru/d/32EfriiMz/dr-egress) |
| Пользовательская документация | [Wiki](https://wiki.yandex-team.ru/users/taitov/yadecap) |
| Месторасположение кода        | [Arc](https://a.yandex-team.ru/arc/trunk/arcadia/noc/yanet) |

#### Check-list системы

|                                                | Status | Links |
|------------------------------------------------|:------:|:-----:|
| Код в аркадии                                  | ★ | [Repo](https://a.yandex-team.ru/arc/trunk/arcadia/noc/yanet) |
| Автотесты                                      | ★ | [Repo](https://a.yandex-team.ru/arc/trunk/arcadia/noc/yanet/yanet/autotests/units) |
| Пользовательская (или какая-то) документация   | ★ | [Wiki](https://wiki.yandex-team.ru/users/taitov/yadecap) |
| Легко тестировать (локально или есть стенды)   | ☆ | - |
| Deploy без Downtime                            | ★ | - |
| Dashboard                                      | ★ | [Grafana](https://grafana.yandex-team.ru/d/BJnsBXbWk/yanet-common) |
| Алерты                                         | ★ | [Juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dyanet_decapsulator%20%7C%20host%3Dyanet_firewall&project=) |
| Деплой по кнопке                               | ☆ | - |
| Есть логи и понятно, где они                   | ★ | [Wiki](https://wiki.yandex-team.ru/users/adess/newdecaps/?from=%2Fusers%2Ftaitov%2Fyadecap%2F#diagnostika) |
| Понятный ответственный                         | ★ | [ABC](https://abc.yandex-team.ru/services/yanet) |
| Живёт -1 ДЦ                                    | ★ | - |

## Сводная таблица по системам

|###| Система\Параметр | Ответственный PM      | Ответственный Разработчик| Где лежит код                                                             | Где дашбоард                                                                  | Где документация                                                 |
|---|:----------------:|:---------------------:|:------------------------:|:-------------------------------------------------------------------------:|:-----------------------------------------------------------------------------:|:----------------------------------------------------------------:|
| 01| RackTables       | Прохоров Александр    | Константин Сазонов       | [GitLab:RT](https://noc-gitlab.yandex-team.ru/nocdev/racktables)          |  ?                                                                            | [Wiki](https://wiki.yandex-team.ru/noc/racktables/)              |
| 02| InvAPI           | Прохоров Александр    | Константин Сазонов       | [GitLab:InvAPI](https://noc-gitlab.yandex-team.ru/nocdev/invapi)          |  ???                                                                          | ???                                                              |
| 03| RT API           | Прохоров Александр    | Константин Сазонов       | [GitLab:RTAPI](https://noc-gitlab.yandex-team.ru/nocdev/rtapi2rr)         |  ???                                                                          | ???                                                              |
| 04| Александрия      | Прохоров Александр    | Алексей Кротов           | [A:Alexandria](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria) |  [Mon:RT API](https://nda.ya.ru/t/ZO9CSFDN4QDEFv)                             | [Docs:Alexandria](https://docs.yandex-team.ru/alexandria/)       |
| 05| Checkist\Чекист  | Михаил Арефьев        | - Не определен -         | [Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/checkist)        |  [https://noc.yandex-team.ru](https://noc.yandex-team.ru)                     | [Wiki](https://wiki.yandex-team.ru/noc/racktables/)              |
| 06| Аннушка          | Михаил Арефьев        | Федор Жуков              | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| 07| ЦК               | Михаил Арефьев        | Федор Жуков              | [GitLab:CK](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck)              |  [https://noc.yandex-team.ru](https://noc.yandex-team.ru)                     | [docs:ck](https://docs.yandex-team.ru/ck/)                       |
| 08| NOCRFCS-D        | Михаил Арефьев        | Азат Курбанов            | [A:NOCRFCS-D](https://a.yandex-team.ru/arc/trunk/arcadia/noc/nocrfcsd)    |  ???                                                                          | ???                                                              |
| 09| HBF-server       | Евгений Сафронов      | Евгений Сафронов         | [Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/hbf-server)      |  ???                                                                          | [Wiki](https://wiki.yandex-team.ru/noc/newnetwork/hbf)           |
| 10| Grad             | Якубеня Дмитрий       | - Не определен -         | [GitLab:Grad](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| 11| Heatmap          | - Отсутствует -       | Влад Старостин           | [GitLab:Heatmap](https://noc-gitlab.yandex-team.ru/nocdev/noc-heatmap)    |  ???                                                                          | ???                                                              |
| 12| Puncher          | Михаил Арефьев        | Влад Старостин           | [Arcadia:Puncher](https://a.yandex-team.ru/arc/trunk/arcadia/noc/puncher) |[https://puncher.yandex-team.ru/](https://puncher.yandex-team.ru/)             | ???                                                              |
| 13| Linkeye          | - Отсутствует -       | - Не определен -         | [GitLab:Linkeye](https://noc-gitlab.yandex-team.ru/nocdev/linkeye)        |  ???                                                                          | ???                                                              |
| 14| Graphene         | - Отсутствует -       | Вадим Бурмакин           | [GitLab:Graphene](https://noc-gitlab.yandex-team.ru/nocdev/graphene)      |  ???                                                                          | ???                                                              |
| 15| Yanet            | Евгений Сафронов      | Тимур Аитов              | [A:Yanet](https://a.yandex-team.ru/arc/trunk/arcadia/noc/yanet)           |  ???                                                                          | ???                                                              |
| 16| Nocauth          | - Отсутствует -       | - Не определен -         | [A:Nocauth](https://a.yandex-team.ru/arc/trunk/arcadia/noc/nocauth)       |  ???                                                                          | ???                                                              |
| 17| Overseer         | Михаил Арефьев        | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| 18| Topka            | Евгений Сафронов      | Евгений Сафронов         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| 19| Valve            | - Отсутствует -       | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  [https://manage.valve.yandex-team.ru/](https://manage.valve.yandex-team.ru/) | ???                                                              |
| 20| Netmap           | - Отсутствует -       | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| 21| Pahom            | - Отсутствует -       | Вадим Бурмакин           | [Arcadia:noc/pahom]({{ service.pahom.url.arcadia }})                      |  [Grafana:Pahom]({{ service.pahom.url.grafana }})                             | ???                                                              |
| 22| Susanin          | - Отсутствует -       | Георгий Кириченко        | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| 23| Dr.Egress        | - Отсутствует -       | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| 24| Megaping         | - Отсутствует -       | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
