# Workflow фидбэка
Workflow определяет то, как мы работаем c фидбэком.
От него зависят допустимые операции над фидбэком и SLA на разбор.

Есть два workflow для фидбэка:
* От пользователей (в коде: `Workflow::Feedback`)
* Предположения (в коде: `Workflow::Task`)

Workflow является [вычисляемым значением](https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/libs/social/feedback/workflow_logic.cpp?rev=6263bb1db3#L21).

## Как обновить логику вычисления workflow
Весь код про workflow инкапсулирован [тут](https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/libs/social/feedback/workflow_logic.cpp?rev=r9559028).

Если закрыт [техдолг](https://st.yandex-team.ru/NMAPS-15594), нужно обновить [код создания матвьюшек](https://a.yandex-team.ru/arcadia/maps/wikimap/mapspro/migrations/migrations/V456__new_feedback_types.sql?rev=r7450975#L116).

## Связанные статьи
* [Срочность фидбэка](feedback_age_types.md).

## Техдолг
[NMAPS-15595](https://st.yandex-team.ru/NMAPS-15595) Выпилить колонки workflow из таблиц про фидбэк
