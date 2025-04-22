# Фреймворки/общие решения в Директе

## Разработка { #dev } 

- баннеры на интерфейсах: [концепции](../dev/banner/concept.md), так же есть инструкции по разработке в разделе "Руководство"
- кампании на интерфейсах
- группы
- условия ретаргетинга
- корректировки: <https://wiki.yandex-team.ru/direct/development/java/documentation/express-bid-modifier/>
- бэкенд гридов
- jooq mapper
- ESS
- транспорт в модерацию: <https://wiki.yandex-team.ru/direct/development/java/documentation/ess-moderation/>
- ваншоты: [инструкция по разработке](../oneshot/howto-code.md)

## Тестирование { #qa }

- тесты скриншотами (?)

## Релизы { #releases }

- [релизные зависимости](../concepts/releases/release-dependencies.md)

## Эксплуатация { #ops }

- directadmin-juggler (заведение агрегатов в juggler), [документация](../jeri/howto-directadmin-juggler.md)
- access-check ( запускает какие скажешь команды и успех/неуспех отправляет сырыми событиями в juggler ): <https://wiki.yandex-team.ru/direct/development/howto/direct-access-check/>
- [schemata](https://a.yandex-team.ru/arc/trunk/arcadia/direct/schemata/), [db_schema](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/db_schema): текстовые описания различных запчастей Директа (таблицы, топики, консьюмеры, спеки, релизные правила и т.д.)
- копилка фидбеков к общеяндексовым инструментам (Мессенджер, arc, YDeploy, infra и т.п.):  
<https://wiki.yandex-team.ru/direct/development/infrastructure/feedback-box/>
- [работа с мессенджерами](chat-tools.md)
