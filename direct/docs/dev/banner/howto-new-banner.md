[Архитектура баннеров (концепции)](concept.md) <br/>

# Создание нового типа баннера

TODO: страница появится по запросу.

Почитайте [страницу об архитектуре баннеров](concept.md).

С вопросами обращайтесь к @mexicano, @ovazhnev, @aleran, @yarashid.

## Переопределение логики модерации баннера

Вам пригодится эта инструкция, если дефолтная логика управления статусом модерации баннера не подходит как есть для целевого типа баннера (подробнее о [статусе модерации баннера в операции обновления](concept.md#op-update-banner-moderation)).

Реализуйте [UpdateOperationModerationProcessor](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/moderation/update/UpdateOperationModerationProcessor.java) в той же директории.

Возможно, вам пригодится один из абстрактных классов: [AbstractDefaultUpdateOperationModerationProcessor](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/moderation/update/AbstractDefaultUpdateOperationModerationProcessor.java) или [AbstractUpdateOperationModerationProcessor](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/moderation/update/AbstractUpdateOperationModerationProcessor.java).
