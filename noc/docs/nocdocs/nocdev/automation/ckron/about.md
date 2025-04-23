# Ckron - автоматическая выкатка конфигурации на сеть

В сетях Яндекса применяется система автоматического применения (автоматических выкаток) конфигурации на оборудовании сети. Рабочее название - Ckron.

**Ckron** - надстройка над стеком Annushka - CK - ChK, которая позволяет управлять параметрами автоматической выкатки конфигурации оборудования.

Охват Ckron на текущий момент следующий:
- Сети ДЦ
  - Cisco
  - Huawei
  - Juniper
  - Nokia
  - Mellanox
  - Cumulus
-  Сеть Офиса
 - IPMI-коммутаторы

{% note info %}

На текущий момент Ckron не охватывает сети Yandex Cloud, а также офисные точки доступа, freebsd устройства.

{% endnote %}

## Расписание применения конфигурации

**Для Датацентровой Сети**
| ДЦ | День Недели | Начало | Rackcode |
|:---:|:---:|:---:|:---:|
| Office | ПН | 9:10 | `{офисная инфраструктура} and {свитч} and not {в оффлайне} and not ({ свитч ABB} or {CloudNetbox}) and {Москва}` |
| Office | ВТ | 9:10 | `{офисная инфраструктура} and {свитч} and not {в оффлайне} and not ({ свитч ABB} or {CloudNetbox}) and not {Москва}` |
| Office | СР | 9:10 | `{свитч для IPMI} and {свитч} and not {в оффлайне} and not ({ свитч ABB} or {CloudNetbox}) and {Сасово}` |
| Office | ЧТ | 9:10 | `{свитч для IPMI} and {свитч} and not {в оффлайне} and not ({ свитч ABB} or {CloudNetbox}) and not {Сасово}` |
| MYT && VLX | ПН | 11:05 | `({Мытищи} or {Владимир AZ}) and ({Huawei CE} or {Nexus}) and {L3 ToR}` |
| MYT && VLX | ПН | 11:35 | `({Мытищи} or {Владимир AZ}) and {Mellanox} and {L3 ToR}` |
| MYT && VLX | ПН | 12:05 | `({Мытищи} or {Владимир AZ}) and {Huawei CE} and ({spine1} or {spine2})` |
| MYT && VLX | ПН | 13:05 | `({Мытищи} or {Владимир AZ}) and {Huawei CE} and {свитч агрегации}` |
| MYT | ПН | 13:35 | `{Мытищи} and {Juniper} and {многодэшка}` |
| IVA | ВТ | 11:05 | `{Ивантеевка} and {Huawei CE} and {серверный свитч}` |
| IVA | ВТ | 12:05 | `{Ивантеевка} and {Huawei 12800} and {distrubution с FastBone}` |
| IVA | ПН | 13:05 | `{Ивантеевка} and {Huawei CE} and {свитч агрегации}` |
| IVA | ВТ | 13:35 | `{Ивантеевка} and {Huawei} and {datacenter edge}` |
| SAS | СР | 11:05 | `{Сасово} and ({Huawei} or {Nexus}) and {серверный свитч}` |
| SAS | СР | 11:35 | `{Сасово} and {Mellanox} and {серверный свитч}` |
| SAS | СР | 12:05 | `{Сасово} and ({spine1} or {spine2})` |
| SAS | СР | 13:05 | `{Сасово} and {Huawei CE} and {свитч агрегации}` |
| SAS | СР | 13:35 | `{Сасово} and {Juniper} and {многодэшка}` |
| MAN | ЧТ | 11:05 | `{Мянтсяля} and ({Huawei} or {Nexus}) and {L3 ToR}` |
| MAN | ЧТ | 11:35 | `{Мянтсяля} and {Mellanox} and {L3 ToR}` |
| MAN | ЧТ | 12:05 | `{Мянтсяля} and ({spine1} or {spine2})` |
| MAN | ЧТ | 13:05 | `{Мянтсяля} and {Huawei CE} and {свитч агрегации}` |
| MAN | ЧТ | 13:35 | `{Мянтсяля} and ({Juniper} or {Huawei}) and {многодэшка}` |
| VLA | ПТ | 11:05 | `{Владимир} and {Huawei} and {L3 ToR}` |
| VLA | ПТ | 11:35 | `{Владимир} and {Mellanox} and {L3 ToR}` |
| VLA | ПТ | 11:05 | `{Владимир} and ({spine1} or {spine2})` |
| VLA | ПТ | 13:05 | `{Владимир} and {Huawei CE} and {свитч агрегации}` |
| VLA | ПТ | 13:35 | `{Владимир} and ({Juniper} or {Huawei}) and {многодэшка}` |
| M9 | ПН | 14:00 | `{border router} and {ММТС9}` |
| ASH | ПН | 15:00 | `({border router} or {свитч}) and {ТП Эшбёрн}` |
| MAR | ВТ | 14:00 | `{border router} and {Марьина Роща 40}` |
| STD | СР | 14:00 | `{border router} and {StoreData}` |
| SPB | ЧТ | 14:00 | `{border router} and {ТП Санкт-Петербург}` |
| EU | ПТ | 14:00 | `{border router} and {Европа}` |
| VLA | ПН | 11:00 | `{border router} and {Владимир}` |
| SAS | ВТ | 11:00 | `{border router} and {Сасово}` |
| MYT | СР | 11:00 | `{border router} and {Мытищи}` |

## Как это работает

В общем виде процесс автокаток происходит так:
- Эксплуатация сети заполняет конфигурационный файл с правилами автокаток
- Правила применяются в **noc-ck**
- В назначенное время запускается ckron, приводя в действие `checkist` для нужных `rackcode`. Для каждого правила создается своя очередь.
- Создается тикет через nocrfcd в очереди NOCRFCS.
- Формируется очередь job, которую можно увидеть в [noc-ck:ui](https://noc.yandex-team.ru/jobs?state=planned%2Cscheduled%2Crunning&page=1), привязанная к тикету NOCRFCS
- Производится выполнения job
- В случае возникновения ошибок больше чем параметр **report_threshold**, то в тикет призывается сотрудник из поля **summons**
- Призываемый сотрудник или сотрудник с админ-правами noc-ck может остановить выполнения ckron

{% note info %}

На текущий момент ckron работет только с acl_safe генераторами.

{% endnote %}

Инструментом управления запусками выкаток конфигурации является проект в Arc - [noc-ck](https://a.yandex-team.ru/arc_vcs/admins/salt-media/noc/roots/units/nocdev-ck/files/etc/noc-ck/).


Конфигурация лежит в специальном файле с конфигурациями: [noc-ck/config.yml](https://a.yandex-team.ru/arcadia/admins/salt-media/noc/roots/units/nocdev-ck/files/etc/noc-ck/config.yml-production). В файл можно добавить конфигурацию в раздел `ckron` список правил в подраздел `rules`.

Поля `ckron.rules`
| Поле                 | Тип     | Описание                                  | Пример                                  |
|:--------------------:|:-------:|:-----------------------------------------:|:---------------------------------------:|
| name                 | sting   | Название правила                          | Office: Автоматическая выкатка safe_acl |
| devices_rackcode     | rackcode| теги в стиле Racktables                   | "{офисная инфраструктура} and {свитч}"  |
| cronline             | cron    | строка cron в UTC, описывает когда надо запускать катку | "10 6 14 * *"             |
| comment              | string  | коментарий                                | автовыкатка офисного IPMI               |
| report_threshold     | int     | Количество подряд идущих фейлов для одного устройства, после которого мы начинаем призывать в тикет отвественных | 3               |
| summons              | dict    | словарь с ответственными за выкатку       | -                                       |
| summons.type         | string  | тип ответственного: user|abc_duty|            | `user`                                  |
| summons.logins       | list    | список с логинами                         | `["xh4l3"]`                             |
| params               | dict    | список с параметрами                      | -                                       |
| params.gens          | list    | лист с генераторами                       | ["Aaa", "MgmtAcl", "Ntp"]               |
| params.nocrfcs_service| string | список с параметрами                     | -                                       |
| params.nocrfcs_datacenters| dict | список с датацентрами                   | -                                       |
| params.max_fail_conditions| list | список условий для отмены джобов при превышении порога| -                         |

**Пример**

```yaml
- name: "Office: Автоматическая выкатка safe_acl на весь офисный парк и IPMI"
  type: checkist
  devices_rackcode: "{офисная инфраструктура} and {свитч} and not {в оффлайне} and not ({ свитч ABB} or {CloudNetbox}) and {Москва}"
  cronline: "10 6 14 * *"  # 09:10 MSK (min hours day)
  comment: ""
  report_threshold: 3
  summons:
    - type: user
      logins: ["xh4l3"]
  params:
      gens: ["Aaa", "MgmtAcl", "Ntp", "Snmp", "SnmpAcl", "SnmpTrap", "Syslog"]
      nocrfcs_service:  "NOC Office - Network"
      nocrfcs_datacenters: ["other"]

  # Условия (пороги и ошибки), при выполнении которых все джобы в запуске отменятся
  max_fail_conditions:
    # Отменяем все джобы при достижении абсолютного порога ошибочно завершённых джобов
    # с ошибкой, соответствующей регулярке /BadCommand/
    - title: Fail the launch if there are too many bad commands
      match:  # матчим по регулярке /BadCommand/
          type: regex
          regex: BadCommand  # пытаемся заматчить строку "comocutor.exceptions.BadCommand"
      threshold:  # абсолютное значение 1
          value: 1
          unit: absolute

    # Отменяем все джобы при достижении 5%-го порога ошибочно завершённых джобов
    # с любой ошибкой
    # Процент порога считается от всего количества джобов в запуске. Например, если в запуске 300
    # джобов, то достаточно сфейлиться хотя бы 15 джобам
    - title: Fail the launch if there are too many other errors
      match_error:  # матчим любые ошибки
          type: any
      threshold:  # относительное значение 5 в процентах от всех джобов
          value: 5
          unit: percentage
```
