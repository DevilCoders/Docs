# Алгоритм удаления серебра ССКУ

## Условие удаления оффера
**В ЕОХ:**

В ЕОХ удаленный оффер помечен [флагом](https://a.yandex-team.ru/svn/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto#L231)

**В МДМ:**

В МДМ удаленный оффер помечен флагами
- Бизнес часть - [флаг](https://mdm.market.yandex-team.ru/constructor/mdm-entity-type/884303947/884336948/37387/4356597148)
- Сервис - [флаг](https://mdm.market.yandex-team.ru/constructor/mdm-entity-type/884303947/884136951/38137/4356597150)

Оффер считается удаленным, если бизнес часть или все сервисы помечены флагами на удаление

## Процесс удаления оффера

Удаление серебряного оффера из МДМ происходит в 2 этапа.

### Этап 1. Импорт из ЕОХ и пометка оффера на удаление

При импорте оффера из ЕОХ МДМ смотрит на [флаг](https://a.yandex-team.ru/svn/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto#L231) и, если он выставлен в ```true```, помечает такой оффер на удаление и добавляет его в очередь на удаление.

Удаленный оффер перестает быть видимым для всех остальных процессов МДМ(например, расчет золота).

### Этап 2. Удаление оффера

За удаление оффера отвечает [SskuToDeleteExecutor](https://a.yandex-team.ru/arcadia/market/mbo/mbo-category/mbo-mdm-tms/src/main/java/ru/yandex/market/mbo/mdm/tms/executors/SskuToDeleteExecutor.java)

Логика работы:
- ```Executor``` выбирает все офферы, которые были добавлены в очередь ```ssku_to_delete``` более 30 дней назад
- МДМ подгружает всю группу из стораджа
- МДМ проверяет актуальное состояние оффера по логике из [SilverCommonSskuGroup](https://a.yandex-team.ru/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/masterdata/model/ssku/SilverCommonSskuGroup.java#L53), сейчас логика такая:
    * Если нет серебра от поставщика, удаляем всю группу
    * Если более чем одно серебро от поставщика проверяем самое актуальное
    * Если база серебра от поставщика помечена на удаление, то удаляем всю группу
    * Если сервиса нет в серебре поставщика или он помечен на удаление, удаляем такой сервис со всего серебра
    * Если после очистки серебра на нем не осталось сервисов, то удаляем всю группу
- Обновляем изменившиеся офферы и удаляем полностью удаленные офферы
- Если в результате проверки оффер помечен на удаление, то снимаем на него маркер из `mdm.ssku_existence`
- Отправляем все изменившиеся и удаленные офферы на пересчет

## Дополнительные процессы
При первоначальной работе процесса дополнительно используется [MarkupOfferForDeleteQueueExecutor](https://a.yandex-team.ru/arcadia/market/mbo/mbo-category/mbo-mdm-tms/src/main/java/ru/yandex/market/mbo/mdm/tms/executors/MarkupOfferForDeleteQueueExecutor.java), который помечает офферы из очереди `markup_offer_for_delete_queue` флагом на удаление.
Он используется для удаления офферов, которые все еще есть в МДМ, но уже удалены в ЕОХ.

## Рубильники
### Удаление офферов
- **shouldRunDeleteOffer** - Должен ли запускаться [SskuToDeleteExecutor](https://a.yandex-team.ru/arcadia/market/mbo/mbo-category/mbo-mdm-tms/src/main/java/ru/yandex/market/mbo/mdm/tms/executors/SskuToDeleteExecutor.java), дефолт - `false`
- **deleteOfferMarkExistence** - Снимать ли маркировку `mdm.ssku_existence` при удалении оффера, дефолт - `true`
- **deleteOfferEnqueueRecalc** - Отправлять ли удаленные офферы на пересчет золота, дефолт - `true`
- **deleteOfferBatchSize** - Размер батча на удаление, дефолт - `300`

### Импорт офферов
- **datacampUnmarkExistenceForRemoved** - Снимать ли маркировку `mdm.ssku_existence` при удалении получении флага на удаление из ЕОХ, дефолт - `false`


