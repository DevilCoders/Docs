blackbox
================

Сервис аутентифицирует пользователей и отдаёт про них информацию.

Документация
------------
1) [Публичная документация](http://doc.yandex-team.ru/blackbox/concepts/about.xml) - может отставать от реальности.
2) [Про обновление NEED_RESET куки](https://doc.yandex-team.ru/Passport/AuthDevGuide/concepts/authorization-policy-resign.html).
3) [Описание атрибутов](https://wiki.yandex-team.ru/passport/dbmoving/).
4) [Yet another документация](https://wiki.yandex-team.ru/passport/blackbox/).

Сборка релиза
-------------
Через `ci changelog -on` + `ci release --no-issue`

Сборка устаревшая
------------
1) Собрать changelog через `ci changelog -on`
2) Сделать релизный таск в PASSP с changelog'ом
3) Руками запустить [сборку](https://sandbox.yandex-team.ru/scheduler/11454/view) debian-пакета
4) Сделать таск в Кондукторе для выкладки debian-пакета
5) Сделать таск на админов для выкатки этого debian-пакета

Количественные мониторинги
-------------
Основные панельки:
1) [большой прод](https://yasm.yandex-team.ru/menu/passport/sezam/stable/blackbox/default/)
2) [yandex-team](https://yasm.yandex-team.ru/menu/passport/sezam/yateam_stable/blackbox/default/)

В соседних вкладках можно найти больше графиков.
Все исходники панелек лежат [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/passport/infra/tools/scripts/yasm).

Качественные мониторинги
-------------
Т.е. алерты. Основные алерты - у админов.

Есть ещё [доморощенные алерты](https://yasm.yandex-team.ru/template/panel/passport_simple_alerts/)

Куда задавать вопросы
-------------
passport-dev@yandex-team.ru
