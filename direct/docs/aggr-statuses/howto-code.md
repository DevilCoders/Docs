[Концепция агр. статусов](concept.md)<br />
[Диагностика статуса объекта](howto-diagnose-status.md)<br />
[Эксплуатация системы статусов](jeri.md)<br />


# Структура кода агрегированных статусов


## Классы


### GdSelfStatusEnum
Статусы содержатся в классе [GdSelfStatusEnum](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/java/ru/yandex/direct/core/entity/aggregatedstatuses/GdSelfStatusEnum.java)

Если вам нужно добавить новый статус, то подумайте еще раз :) Скорее всего вам это не нужно. Иначе не забудьте обсудить новый статус с фронтом (не забыть про мобильную версию, dna, uc), разработать дизайн иконки нового статуса, учесть новый статус в фильтрах, помигрировать табличку ```aggr_statuses_keywords```, учесть новый статус в конвертере UAC бекенда [RmpCampaignConverter](https://a.yandex-team.ru/arc_vcs/direct/core/src/main/java/ru/yandex/direct/core/entity/uac/service/RmpCampaignConverter.kt)

Глядя на этот класс и причины в классе `GdSelfStatusReason` можно понять какие в принципе бывают статусы у объектов.


### GdSelfStatusReason

Текстовые токены подписей к статусам (они же reason-ы) содержатся в классе [GdSelfStatusReason](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/java/ru/yandex/direct/core/entity/aggregatedstatuses/GdSelfStatusReason.java)

Добавления нового значение в этот enum создает релизную зависимость: сначала изменение должно выехать в java-web (где происходит чтение из БД), потом в java-jobs (запись).

Перед удалением значения необходимо убедится, что таковых не осталось в БД. Для этого сначала убираем весь код генерирующий подобный статус, потом пересчитываем все статусы (TBD)


### AdStates, KeywordStates, RetargetingStates, AdGroupStates, CampaignStates

[/direct/core/src/main/java/ru/yandex/direct/core/aggregatedstatuses/logic/*States.java](https://a.yandex-team.ru/search?search=,%5Edirect.*%2Flogic%2F.*States.java%24,,arcadia,,5000&repo=arc)

Эти классы реализуют метод calc, который на входе получает модель объекта Директа (объявление, фразу, группу, кампанию) и возвращает набор "стейтов" (состояний) объекта.


### SelfStatusCalculators

[SelfStatusCalculators](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/aggregatedstatuses/logic/SelfStatusCalculators.java)

Реализует методы `calc*SelfStatus` которые по набору стейтов (в идеале) из предыдущего класса и счетчиков подобъектов, если применимо, вычисляет статус объекта, который мы потом и пишем в базу.

Походов в БД, и медленных операцих в этих метода быть не должно. Все объекты должны быть получены пачками снаружи этих методов.


### EffectiveStatusCalculators

[EffectiveStatusCalculators](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/aggregatedstatuses/logic/EffectiveStatusCalculators.java)

Реализует методы `*EffectiveStatus` которые вызываются в момент показа объектов в интерфейсе. Каждый из этих методов по данным самого объекта, его собственному статусу, сохраненному в БД и собственным статусам его объектов верхнего уровня вычисляет тот статус и набор причин, которые будут отображены клиенту.

Походов в БД, и медленных операцих в этих метода быть не должно.


### StatusUtils

[StatusUtils](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/aggregatedstatuses/logic/StatusUtils.java)

Логика мерджа статусов между объектами разных уровней (как статусы сверху с кампании схлопываются вниз, например до объявления), реализована в этом классе.


### AggregatedStatusesService

[AggregatedStatusesService](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/aggregatedstatuses/AggregatedStatusesService.java)

Сервис. Методы этого класса вызываются из ESS-контура для подсчета собственных статусов. Этот же класс используется в job-е для полного пересчета статусов всех объектов.


### AggregatedStatusesViewService

[AggregatedStatusesViewService](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/aggregatedstatuses/AggregatedStatusesViewService.java)

Сервис, методы которого вызываются при отображения грида для получения эффективных (отображаемых на фронт синхронно) статусов объектов. Именно использования этого класса надо искать по коду, чтобы найти *Data классы собирающие информацию для отображения в гридах.


### ESS контур

* [AggregatedStatusesConfig](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/config/src/main/java/ru/yandex/direct/ess/config/aggregatedstatuses/AggregatedStatusesConfig.java)
* [AggregatedStatusesRule](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/router/src/main/java/ru/yandex/direct/ess/router/rules/aggregatedstatuses/AggregatedStatusesRule.java)
* [AggregatedStatusesProcessor](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/aggregatedstatuses/AggregatedStatusesProcessor.java)

