[Концепция агр. статусов](concept.md)<br />
[Код агр. статусов](howto-code.md)<br />
[Эксплуатация системы статусов](jeri.md)<br />


# Диагностика значения Агр. Статуса
Понять о том, почему на объекте тот или иной статус поможет эта страница.

В первую очередь необходимо проверить, что контур работает, об этом можно прочитать на [странице эксплуатации Агрегированных Статусов](jeri.md)


## Отображение на фронте в Grid-ах (и GraphQL)
Стоит проверить какие данные о статусе попадают на фронт и убедится, что нет проблемы с отображением статуса на стороне фронтэнда, а также выяснить, какой именно эффективный статус отдается с бэка. Сделать это можно открыв испектор браузера в гриде и в ответе с бэкенда на запрос соответствующего грида поискать поле `aggregatedStatusInfo`

Пример
```json
"aggregatedStatusInfo": {
                            "status": "STOP_OK",
                            "isObsolete": false,
                            "reasons": [
                                "CAMPAIGN_SUSPENDED_BY_USER"
                            ],
                            "counters": null
                        },
```

За значения полей status и reasons отвечают Java-классы [GdSelfStatusEnum](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/java/ru/yandex/direct/core/entity/aggregatedstatuses/GdSelfStatusEnum.java) и [GdSelfStatusReason](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/java/ru/yandex/direct/core/entity/aggregatedstatuses/GdSelfStatusReason.java) соответственно.

**Для просмотра json'а агрегированных статусов прямо в интерфейсе у нас есть фича** (выдается на оператора): `show_aggregated_status_debug`

## Таблицы в которых хранятся статусы

Предагрегированные значения статусов хранятся в таблицах:
```
aggr_statuses_adgroups
aggr_statuses_banners
aggr_statuses_campaigns
aggr_statuses_keywords
aggr_statuses_retargetings
```

За исключением `aggr_statuses_keywords`, JSON описывающий статус хранится в поле aggr_data соответствующий таблицы

Полезно проверить время пересчета статуса по полю `updated` соответствующей таблицы

Пример запроса в БД
```bash
$ direct-sql pr:ppc:21 'select c.aggr_data as camp, c.updated, g.aggr_data as adgroup, g.updated, kw.status, kw.reason, kw.updated from bids join phrases using(pid) join campaigns on phrases.cid = campaigns.cid join aggr_statuses_campaigns c on c.cid = campaigns.cid join aggr_statuses_adgroups g on g.pid = phrases.pid join aggr_statuses_keywords kw on kw.id = bids.id where bids.id = 15794798902\G'
pr:ppc:21
*************************** 1. row ***************************
   camp: {"s": "ARCHIVED", "sts": ["SUSPENDED"], "cnts": {"s": {"ARCHIVED": 1}, "grps": 1}}
updated: 2020-09-09 15:42:38
adgroup: {"s": "ARCHIVED", "cnts": {"ads": 1, "b_s": {"ARCHIVED": 1}, "kws": 12, "kw_s": {"RUN_OK": 12}, "rets": 0, "b_sts": {"ARCHIVED": 1, "REJECTED": 1, "SUSPENDED": 1}}}
updated: 2020-09-02 07:29:56
 status: RUN_OK
 reason: ACTIVE
updated: 2020-08-27 11:15:24
```

Тут видно, что несмотря на то, что статус фразы `RUN_OK` она будет отображаться как архивная, т.к. архивна ее группа.

Эти же данные доступы в гридах в YT, таблицах соответствующих объектов, но на время написания документации (2020-12-28) для отображения статусов используется MySQL


## От базы до отображения на фронте

При отображении статуса объекта учитываются статусы его объектов верхнего уровня. Так, чтобы понять почему отображается определенный статус фразы необходимо проверить статус самой фразы, статус ее группы и статус кампании этой группы. В общем случае из этих трех статусов будет выбран наиболее приоритетный.

Приоритет определяется порядком значений enum-а [GdSelfStatusEnum](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/java/ru/yandex/direct/core/entity/aggregatedstatuses/GdSelfStatusEnum.java)

Помимо приоритета для каждого случая может существовать какая-то особенная логика. Ее реализацию можноо посмотреть в классе [EffectiveStatusCalculators](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/aggregatedstatuses/logic/EffectiveStatusCalculators.java). Именно этот класс определяет как "схопываются" статусы объектов разного уровня (как статусы группы и кампании влияют на отображаемый, эффективный, статус объявления или фразы).

Также важно понимать, что на фронте может быть какая-то логика отображения определенных пар status+reason.
