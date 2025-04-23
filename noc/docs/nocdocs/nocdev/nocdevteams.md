# Команды NOCDEV

В этом разделе узнаете про команды NOCDEV, их состав и ответственных менеджеров.

## Ops

**Руководитель команды**: Кирилл Глушенков (kglushen@)

**Технический менеджер**: Дмитрий Якубеня (demian@)

**Разработчики**:
- Борис Литвиненко,
- Сергей Черноморец
- Сергеей Качеев
- Андрей Росляков

## Мониторинг сети

**Технический менеджер**: Дмитрий Якубеня (demian@)

**Разработчики**:
- Александр Балезин (gescheit@)

## Автоматизация сети

**Технический менеджер**: Михаил Арефьев (m-arefiev@)

**Разработчики**:
- Влад Старостин
- Федор Жуков
- Азат Курбанов

## Firewall

**Технический менеджер**: Евгений Сафронов (esafronov@)

**Разработчики**:
- ???

## Racktables

**Технический менеджер**: Прохоров Александр (alexprokhorov@)

**Разработчики**:
- Константин Сазонов
- Кротов Алексей
- Мищенко Сергей
- Вадим Бурмакин

## Распределение систем по командам

| Система\Параметр | Ответственный PM      | Ответственный Разработчик| Где лежит код                                                             | Где дашбоард                                                                  | Где документация                                                 |
|:----------------:|:---------------------:|:------------------------:|:-------------------------------------------------------------------------:|:-----------------------------------------------------------------------------:|:----------------------------------------------------------------:|
| RackTables       | Прохоров Александр    | Константин Сазонов       | [GitLab:RT](https://noc-gitlab.yandex-team.ru/nocdev/racktables)          |  ?                                                                            | [Wiki](https://wiki.yandex-team.ru/noc/racktables/)              |
| InvAPI           | Прохоров Александр    | Константин Сазонов       | [GitLab:InvAPI](https://noc-gitlab.yandex-team.ru/nocdev/invapi)          |  ???                                                                          | ???                                                              |
| RT API           | Прохоров Александр    | Константин Сазонов       | [GitLab:RTAPI](https://noc-gitlab.yandex-team.ru/nocdev/rtapi2rr)         |  ???                                                                          | ???                                                              |
| Александрия      | Прохоров Александр    | Алексей Кротов           | [A:Alexandria](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria) |  [Mon:RT API](https://nda.ya.ru/t/ZO9CSFDN4QDEFv)                             | [Docs:Alexandria](https://docs.yandex-team.ru/alexandria/)       |
| Checkist\Чекист  | Михаил Арефьев        | Федор Жуков              | [Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/checkist)        |  [https://noc.yandex-team.ru](https://noc.yandex-team.ru)                     | [Wiki](https://wiki.yandex-team.ru/noc/racktables/)              |
| Аннушка          | Михаил Арефьев        | Федор Жуков              | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| ЦК               | Михаил Арефьев        | Федор Жуков              | [GitLab:CK](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck)              |  [https://noc.yandex-team.ru](https://noc.yandex-team.ru)                     | [docs:ck](https://docs.yandex-team.ru/ck/)                       |
| NOCRFCS-D        | Михаил Арефьев        | Азат Курбанов            | [A:NOCRFCS-D](https://a.yandex-team.ru/arc/trunk/arcadia/noc/nocrfcsd)    |  ???                                                                          | ???                                                              |
| HBF-server       | Евгений Сафронов      | Евгений Сафронов         | [Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/noc/checkist)        |  [https://noc.yandex-team.ru](https://noc.yandex-team.ru)                     | [Wiki](https://wiki.yandex-team.ru/noc/racktables/)              |
| Grad             | Якубеня Дмитрий       | - Не определен -         | [GitLab:Grad](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| Heatmap          | - Отсутствует -       | Влад Старостин           | [GitLab:Heatmap](https://noc-gitlab.yandex-team.ru/nocdev/noc-heatmap)    |  ???                                                                          | ???                                                              |
| Puncher          | @m-arefiev            | Влад Старостин           | [Arcadia:Puncher](https://a.yandex-team.ru/arc/trunk/arcadia/noc/puncher) |[https://puncher.yandex-team.ru/](https://puncher.yandex-team.ru/)             | ???                                                              |
| Linkeye          | - Отсутствует -       | - Не определен -         | [GitLab:Linkeye](https://noc-gitlab.yandex-team.ru/nocdev/linkeye)        |  ???                                                                          | ???                                                              |
| Graphene         | - Отсутствует -       | Сергей Качеев            | [A:Graphene](https://a.yandex-team.ru/arc/trunk/arcadia/noc/graphene)     |  [https://graphene.yandex-team.ru](https://graphene.yandex-team.ru)           | [Wiki](https://wiki.yandex-team.ru/nocdev/graphene/)             |
| Yanet            | Евгений Сафронов      | Тимур Аитов              | [A:Yanet](https://a.yandex-team.ru/arc/trunk/arcadia/noc/yanet)           |  ???                                                                          | ???                                                              |
| Nocauth          | - Отсутствует -       | - Не определен -         | [A:Nocauth](https://a.yandex-team.ru/arc/trunk/arcadia/noc/nocauth)       |  ???                                                                          | ???                                                              |
| Overseer         | @m-arefiev            | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| Topka            | Евгений Сафронов      | Евгений Сафронов         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| Valve            | - Отсутствует -       | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  [https://manage.valve.yandex-team.ru/](https://manage.valve.yandex-team.ru/) | ???                                                              |
| Netmap           | - Отсутствует -       | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| Pahom            | - Отсутствует -       | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| Susanin          | - Отсутствует -       | Георгий Кириченко        | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| Dr.Egress        | - Отсутствует -       | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |
| Megaping         | - Отсутствует -       | - Не определен -         | [???????????](https://noc-gitlab.yandex-team.ru/nocdev/grad)              |  ???                                                                          | ???                                                              |


## Чеклист по системам

|                                                | RackTables           |Checkist       |HBF-server|Grad |Heatmap |Puncher|Linkeye|Graphene|Yanet|Nocauth|Overseer|ЦК |Topka|Valve  |Netmap|InvAPI  |
|------------------------------------------------|----------------------|---------------|----------|-----|--------|-------|-------|--------|-----|-------|--------|---|-----|-------|------|--------|
| Код в аркадии                                  | ❌                   |✔️              |✔️         |✔️    |❌      |✔️      |❌     |✔️       |❌   |❌     |❌      |❌ |✔️    |✔️      |❌    |❌      |
| Автотесты                                      | ✔️                    |✔️              |✔️         |✔️    |❌      |✔️      |✔️      |❌      |✔️    |✔️      |?       |✔️  |❌   |✔️      |❌    |?       |
| Пользовательская (или какая-то) документация   | ✔️                    |✔️              |✔️         |⅔    |❌      |✔️      |❌     |✔️       |?    |✔️      |?       |❌ |✔️    |✔️      |❌    |?       |
| Легко тестировать (локально или есть стенды)   | ✔️                    |✔️              |✔️         |?    |✔️       |✔️      |✔️      |✔️       |?    |❌     |?       |✔️  |✔️    |✔️      |❌    |?       |
| Деплой без даунтаума                           | ✔️                    |❌ (рег. тесты)|✔️         |✔️    |❌      |✔️      |✔️      |✔️       |✔️    |❌     |?       |✔️  |✔️    |✔️      |✔️     |?       |
| Дашборд с графичками                           | ✔️                    |✔️              |[✔️\*][l1] |?    |❌      |✔️      |✔️      |❌      |✔️    |❌     |❌      |❌ |✔️    |[✔️\*][l2]|❌    |?       |
| Алерты                                         | ✔️                    |❌             |❌        |✔️    |❌      |❌     |❌     |✔️       |?    |❌     |❌      |✔️  |✔️    |❌     |❌    |✔️ (авто)|
| Деплой по кнопке                               |                      |✔️              |✔️         |✔️    |✔️       |✔️      |✔️      |✔️       |✔️    |✔️      |❌      |✔️  |✔️    |✔️      |✔️     |?       |
| Есть логи и понятно, где они                   | ✔️                    |✔️              |✔️         |✔️    |✔️       |✔️      |✔️      |✔️       |✔️    |✔️      |?       |✔️  |✔️    |✔️      |✔️     |?       |
| Понятный ответственный                         | ✔️                    |✔️              |✔️         |✔️    |✔️       |✔️      |✔️      |✔️       |✔️    |✔️      |❌      |✔️  |✔️    |✔️      |✔️     |✔️       |
| Живёт -1 ДЦ                                    | ❌ (в ручном режиме) |✔️              |✔️         |✔️    |✔️       |✔️      |❌     |✔️       |✔️    |✔️      |?       |✔️  |✔️    |✔️      |❌    |?       |


[l1]: <https://nda.ya.ru/t/CmTdVrHU4KnHLv>
[l2]: <https://yasm.yandex-team.ru/template/panel/valve/>
