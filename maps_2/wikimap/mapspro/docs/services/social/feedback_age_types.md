# Срочность фидбэка
Срочный фидбэк - это фидбэк от пользователей созданный ранее, чем сутки назад.

В интерфейсе в фильтрах именуется _Срочные_/_Несрочные_.

В коде - это [enum AgeType](https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/libs/social/include/yandex/maps/wiki/social/feedback/enums.h?rev=r9375546#L82).

Срочность фидбэка - [вычисляемое значение](https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/libs/social/feedback/task_brief.cpp?rev=r9325309#L280).

## Связанные статьи
* [Workflow фидбэка](feedback_workflow.md).

## Техдолг
[NMAPS-15593](https://st.yandex-team.ru/NMAPS-15593): Для определения срочности фидбэка использовать state_modified_at вместо created_at.

[NMAPS-15594](https://st.yandex-team.ru/NMAPS-15594): В общей статистике по регионам для фидбэка неверно вычисляется срочность.
