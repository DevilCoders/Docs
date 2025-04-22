## Нагрузочное тестирование

[Тикет](MAILPG-3135) на разработку.

[Load](https://nanny.yandex-team.ru/ui/#/services/catalog/mail_sharpei_load/)-окружение в YP.Lite.

[Jenkins](https://jenkins-load.yandex-team.ru/job/sharpei_pandora/)-джоба для запуска нагрузочных тестов.
Также есть [sandbox-таска](https://sandbox.yandex-team.ru/task/772159475/view) для запуска стрельб.
Сейчас не используется, но, возможно, пригодится, когда соберемся делать автоматику для релиза.

[Страничка регрессии](https://lunapark.yandex-team.ru/regress/MAILPG?service=sharpei) в lunapark

### Что тестируем
* ручка `/conninfo`
* три версии ручки `/stat`
* ленивую регистрацию посредствам `/conninfo`

За подробностями см. [код](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/load/pandora/handlers.go?rev=6775489#L18).

### Sharddb

**sharddb** живет отдельно от самого Шарпея в [yc](https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql/cluster/mdb89eo15641i2ooopcf).
Пароль для пользователя **sharpei** такой же, как и в нагрузочной **mdb** (см. [страничку](https://wiki.yandex-team.ru/mail/pg/xdb/)).

База заполнена пользователями из шарда **pgload03** нагрузочной почтовой метабазы.\
[Скрипт](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/load/populate_sharddb) для заполнения.

### Пушка

Пушка: [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/load/pandora)\
Скрипты для генерации патронов: [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/load/tools/)

По немодифицирующим операциям стреляем уидами из сандбокс-ресурса, ссылку на который можно передать в параметрах джобы.\
Для ленивой регистрации уиды генерируются [налету](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/load/pandora/handlers.go?rev=6775489#L34).

### Стрельбы
* Перезапускаем [джобу](https://jenkins-load.yandex-team.ru/job/sharpei_pandora/953/) a.k.a. стрельба на разладку; автостоп должен быть на рпс > 30К.
* Перезапускаем [джобу](https://jenkins-load.yandex-team.ru/job/sharpei_pandora/956/) a.k.a. стрельба с постоянной нагрузкой; должен не произойти автостоп. РПС достаточно большие, но при этом далекие от критических. Нагружаем в течении 30 минут - убеждаемся, что сервис не деградирует под нагрузкой.

Инстансы шарпея и базы должны находиться в IVA, потому что там самое слабое железо.
