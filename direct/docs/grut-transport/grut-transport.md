# Транспорт в Цезарь через GrUT

### Описание
Транспорт в Цезарь через GrUT представляет собой переходный шаг к хранению данных Директа в GrUT вместо mysql.
Состоит из двух частей: репликацию данных Директа из mysql в GrUT (см [Mysql2GrutReplicationProcessor](../reference/jobs/list/Mysql2GrutReplicationProcessor.md)) и транспорт из GrUT в Цезарь.<br>
**Первая часть** представляет собой перекладывание данных "как есть" по возможности, то есть не делает сложных преобразований данных, как в перловом транспорте, а сохраняет данные как они лежат в mysql.<br>
**Вторая часть** написана на C++ и на основании данных полученный из части 1 вычисляет дополнительные поля(ComputedFields). Здесь уже реализованны все основные преобразования из перлового транспорта.<br>
Таблицы в груте описываются в виде proto, посмотреть ее можно [тут](https://a.yandex-team.ru/arcadia/grut/libs/proto/objects).

### Репликация из mysql в GrUT
Ess-процессор [Mysql2GrutReplicationProcessor](../reference/jobs/list/Mysql2GrutReplicationProcessor.md).
Чтобы посмотреть, что сохранилось в результате репликации в грут, можно воспользоваться клиентом к orm - [grut-orm](https://a.yandex-team.ru/arcadia/grut/tools/cli/orm).
В скором времени можно будет воспользоваться [YT ORM в YQL](https://wiki.yandex-team.ru/yt/orm/yql/).
Так же можно смотреть данные в посуточных [бекапах](https://yt.yandex-team.ru/hahn/navigation?path=//home/grut/backups/stable)

### Транспорт из GrUT в Цезарь
Кодовая база транспорта лежит в директории [arcadia/ads/bsyeti/caesar/libs/grut](https://a.yandex-team.ru/arcadia/ads/bsyeti/caesar/libs/grut?rev=r9657368). За подробностями реализации обращаться к [osidorkin](https://staff.yandex-team.ru/osidorkin), [bulatman](https://staff.yandex-team.ru/bulatman)
Верхнеуровнево: следит за изменениями в объектах грута, изменившиеся перекладывает в профили цезаря. Так же рассчитывает Computed поля - функции от существующих полей, джойны и т.п.

### Процесс переключение на транспорт через GrUT
Переключение происходит на стороне БК. Переключаются отдельные Loader'ы. Первым шагом происходит переключение кампаний Uac ТГО.
Статус переключения можно узнать у  [danilgrig](https://staff.yandex-team.ru/danilgrig), [bulatman](https://staff.yandex-team.ru/bulatman)

### Вопросы
#### Как переотправлять объекты?
- На данный момент переотправить объекты можно с помощью ваншота [Mysql2GrutReplicationOneshot](https://a.yandex-team.ru/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/mysql2grut/Mysql2GrutReplicationOneshot.kt?rev=r9679085#L177), а так же с помощью инструмента переотправки объектов в ESS - [Отправка объектов в ESS](https://direct.yandex.ru/internal_tools/#sending_objects_to_ess). В скором времени появится отдельный отчет для переотправки в репликацию. Computed поля для активных кампаний пересчитываются раз в три часа, вызвать их расчет раньше можно только изменив поля в базе грута.

#### В какой транспорт добавлять новые поля?
- Разработчик со стороны БК может сказать, переключен ли Loader, в который будет добавлено новое поле, на новый транспорт. Стоит так же призвать в тикет [danilgrig](https://staff.yandex-team.ru/danilgrig), чтобы он подтвердил решение. При исправлении транспорта существующего поля, если оно уже отправляется через грут, нужно делать исправление во всех местах, а также не забыть переотправить все затронутые объекты через репликацию. По вопросам разработки в Директе обращаться к [mspirit](https://staff.yandex-team.ru/mspirit), [ppalex](https://staff.yandex-team.ru/ppalex), [elwood](https://staff.yandex-team.ru/elwood)

### Особенности
- Нейминг таблиц в GrUT. Таблицы репликации кампаний, групп и баннеров в груте называются campaign_v2, ad_group_v2 и banner_v2. Это связано с тем, что таблицы без суффикса v2 были занятыми таблицами заявок uac. Переименовать их нетривиально, поэтому пока называются так.
