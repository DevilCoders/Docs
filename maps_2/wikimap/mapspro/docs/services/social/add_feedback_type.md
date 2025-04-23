### Как добавить новый тип фидбека в НК:
1. Добавить значение в [enum](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/libs/social/include/yandex/maps/wiki/social/feedback/enums.h?rev=r8580245#L120) с типами
2. Добавить [название](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/libs/social/feedback/enums.cpp?rev=r8580245#L91) нового типа
2.1 [Определить](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/libs/social/feedback/enums.cpp?rev=e338387372d257f12f7d6f763044f9cd5994a4aa#L236) категорию для нового типа.
3. Добавить миграцию с этим типом, [пример](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/migrations/migrations/V518__NONTRANSACTIONAL_scooter_feedback_type.sql?from_pr=1980533&rev=r8580245)
4. Добавить этот же тип в [схему](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/schemas/social/social.feedback.schema.json?rev=r8580245#L139). Схема описывает API сервиса social.
5. И ещё в [одну](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/schemas/tasks/feedback.xsd?rev=r8580245#L6): эта схема описывает http-интерфейс [grinder](https://abc.yandex-team.ru/services/maps-core-nmaps-grinder/)-а и значение в ней нужно, чтобы при импорте фидбека можно было выбрать новый тип фидбека.
6. Обновить [тестовые данные](https://a.yandex-team.ru/svn/trunk/arcadia/maps/wikimap/mapspro/services/social/src/libs/feedback-actions/tests/medium/data/meta-response.json?rev=r9779643#L2) для ручки с метаинформацией про фидбек.
7. Добавить ключ в танкере для имени нового типа в keyset [feedback](https://tanker.yandex-team.ru/project/nmaps/keyset/feedback?branch=master), id ключа имеет вид `task-type-<new_feedback_type_name>`, `<new_feedback_type_name>` совпадает с добавленным [названием](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/libs/social/feedback/enums.cpp?rev=r8580245#L91)

Пример [ревью](https://a.yandex-team.ru/review/1980533/details) с добавлением нового типа фидбека.


### Выкатка нового типа:
1. Ключи в танкере забирают для перевода в четврег, [детали](https://wiki.yandex-team.ru/jandekskarty/testing/wikimaps/autoticketstranslate/). Переводы обычно готовы к ближайшему релизу НК в среду. Без переводов нельзя выкатывать в прод
2. Из сервисов нужно выкатить:
  * [maintenance](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/maintenance/), [abc](https://abc.yandex-team.ru/services/maps-core-nmaps-maintenance/)
    - чтобы применилась миграция
  * [social](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/social/), [abc](https://abc.yandex-team.ru/services/maps-core-nmaps-social/)
  * [social_backoffice](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/social_backoffice), [abc](https://abc.yandex-team.ru/services/maps-core-nmaps-social-backoffice)
  * [editor_reader](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/editor/reader), [abc](https://abc.yandex-team.ru/services/maps-core-nmaps-editor)
    - editor_reader читает объекты с фидбеком из бд, чтобы отображать комментарии к фидбеку
  * [editor_writer](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/editor/writer), [abc](https://abc.yandex-team.ru/services/maps-core-nmaps-editor-writer/)
    - editor_writer записывает комментарии к фидбеку, для этого читает объекты с фидбеком из бд
  * [tasks_feedback](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_feedback), [abc](https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-feedback)
    - воркеры этого сервиса оперируют с фидбеком: добавляют новый, обновляют статусы и т.п. Им тоже надо читать объекты с фидбеком из бд. В частности, сломается [schedule_feedback_worker](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_feedback/src/schedule_feedback_worker).
  * [tasks_social](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_social), [abc](https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-social/)
    - нужно для оценки качества фидбека: сломается при попытке прочитать фидбек нового типа, если не выкатить
  * [tasks_sprav](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_sprav), [abc](https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-sprav) - выкатывать небязательно
    - использует уже известные типы фидбэка для poi/indoor, при добавлении нового типа не должен сломаться

[Инструкция](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/nmaps/HOW_TO_RELEASE.md) по выкатке сервисов народной карты.
