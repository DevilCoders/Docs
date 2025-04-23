# Архив моделек

В маркете модельки катаются где-то рядом с индексом непонятными процессами (которые мы не особо контролируем). В наших репортах их вынесли в отдельный ресурс который мы релизим сами. Сами формулы лежат всё [там же](https://a.yandex-team.ru/arc/trunk/arcadia/market/report/data/formulas/formulas), где и у маркета -- мы переделали только релизную часть.

[Хитман процесс](https://hitman.yandex-team.ru/projects/goods-runtime/release_models_archive/) запускает [сандбокс таску](https://a.yandex-team.ru/arc_vcs/sandbox/projects/goods/GoodsReleaseDynamicResource/__init__.py), которая выкачивает папку из аркадии и, если находит дифф с продом, релизит её. Чтобы релизнуть самому, достаточно прожать триггер в процессе. На репортах настроена тикет-интеграция с автокоммитом. Дёргается релиз ресурса и он катится через [дашборд](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/goods-report). Сейчас там немного медленная выкатка из-за проблем репорта маркета, это решается.

Сами формулы лежат в контейнере в папке formulas/formulas/formulas (не спрашивайте). Также можно скачать из няни ресурс [GOODS_REPORT_MODELS_ARCHIVE](https://sandbox.yandex-team.ru/resources/?type=GOODS_REPORT_MODELS_ARCHIVE)
