## Откат графа на предыдущую версию

Инструкцию по откату графа на предыдущую весию можно найти [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/road_graph_deployment/README.md)


## Откат сервиса роутера на предыдущую версию

Для отката сервиса с подозрительной на стабильную версию нужно использовать [команды](https://docs.yandex-team.ru/sedem/releases) утилиты SEDEM.
Предположим, что подозрительная версия, с которой надо делать откат, это v125.1, а стабильная проверенная - это v123.1.
Приведенные ниже команды надо выполнять из корня Аркадии:

1. Чтобы узнать, на какую версию можно откатиться, используем команду [rollback](https://docs.yandex-team.ru/sedem/releases#release-rollback): <br/> `ya tool sedem release rollback maps/routing/router <staging>`
2. Выбрать версию, на которую откатиться, и выполнить команду отката: <br/> `ya tool sedem release rollback maps/routing/router <staging> <version>` <br/> например, <br/> `ya tool sedem release rollback maps/routing/router prestable v123.1`
3. Если требуется, выполните откат на всех продакшен-окружениях (prestable, stable), где развернута подозрительная версия, и на тестовых окружениях
4. Если есть уверенность, что эту подозрительную версию (с которой откатывались) в дальнейшем ни в коем случае нельзя выкатывать в продакшен (в следующие стейджинги или снова в тот, откуда откатывали), то надо пометить версию как бракованную, воспользовавшись командой [reject](https://docs.yandex-team.ru/sedem/releases#release-reject): <br/> `ya tool sedem release reject maps/routing/router v125.1 -m "reject message" `


## Включение деградации роутера через ITS

Если сервис роутера перестаёт справляться с нагрузкой (то есть заметно ухудшаются тайминги, уровень потребления CPU приближается к 90-100%, часто возникают 503, 499 ответы), то можно включить деградацию роутера при помощи механизма ITS в Няне. На текущий момент поддержаны две деградации:
1. Ручка `/v2/nearby_alternatives` перестаёт искать альтернативы по маршруту и отдаёт пустой ответ. Поле `nearby-alternatives-degradation` в ITS.
2. Ручка `/v2/route` на запросы в режиме `mode=best` от клиентов, чьи TVM прописаны в [config.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/yacare/bin/config.json?rev=r9440688#L73) в секции `degradation_config -> restricted_tvm_ids`, отвечает в режиме `mode=approx`. Изначально там прописаны TVM для мобильной прокси. Поле `mode-best-to-fast-degradation` в ITS.

[Ссылка на вкладку ITS](https://nanny.yandex-team.ru/ui/#/its/locations/maps/custom/core-driving-router)
Указанные выше поля включают деградации в `dataprestable`-, `prestable`- и `stable`- окружениях роутера. Суффикс `-testing` у поля указывает на то, что деградация применяется к тестовому окружению роутера.

