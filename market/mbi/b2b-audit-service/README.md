## О компоненте
Сервис обработки сообщений аудита MBI. Схема работы:
- клиент пушит сообщение EntityHistory в топик аудита;
- сервис аудита слуашет топики (на текущий момент он один, но можно добавить) и сохраняет сообщения в дин таблицы

Сообщения передаются в формате Protobuf [market/mbi/b2b-audit-proto/entity_history.proto]
На стороне клиента сообщения пушаться в топик в рамках транзакции.
При коммите или откате транзакции необходимо отправить соответсвующее сообщение в том же формате.


## Локальный запуск из IDEA
##### Main class
`ru.yandex.market.mbi.audit.service.B2BAuditService`

##### VM-options
`
-Djava.library.path=/Users/lozovskii/IdeaProjects/arcadia-market_mbi_b2b-audit-servcie/dlls
-Djna.library.path=/Users/lozovskii/IdeaProjects/arcadia-market_mbi_b2b-audit-servcie/dlls
-Dspring.profiles.active=development
-Dconfigs.pat=/Users/lozovskii/arcadia/market/mbi/b2b-audit-serviec/src/main/properties.d/development
`
##### Working-directory
`/Users/lozovskii/IdeaProjects/arcadia-market_mbi_b2b-audit-servcie`

##### Before launch
Для локального запуска используется тестовая таблица на Pythia
`//tmp/mbi/b2b_audit_tst/log_entity_history`

Для аутентификации на YT необходимо подставить свой YT-токен https://oauth.yt.yandex.net

`mbi_billing.hive.username=user`

`market.b2b-audit-service.target.yt.token=token`

Для аутентификации в Логброкере необходимо подставить свой доменный токен
https://logbroker.yandex-team.ru/docs/concepts/security#oauth

`market.b2b-audit-service.ouathtoken=user-domain-token`

для dev можно использовать топик и консьюмер

`market.logbroker.b2b-audit-service.default.topic-path=/mbi/dev/b2b-audit`

`market.logbroker.b2b-audit-service.default.consumer-path=/mbi/dev/b2b-audit-consumer`

