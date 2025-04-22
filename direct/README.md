# Директ
Яндекс.Директ – сервис для заведения рекламных материалов, которые в последствии откручиваются Баннерной Крутилкой на Поиске, РСЯ и других площадках.

Очередь в Стартреке https://st.yandex-team.ru/DIRECT

Стафф https://staff.yandex-team.ru/departments/yandex_monetize_search_direct_interface/

Сервис в ABC https://abc.yandex-team.ru/services/direct/

## Дежурства
- https://duty.mtrs.yandex-team.ru/project/direct/ - дежурные по продакшену тут
- https://abc.yandex-team.ru/services/direct/duty/
- https://radar.qart.yandex-team.ru/release/directOnDuty.html - общая страничка с дежурствами из разных источников (для просмотра нужны дырки) 

## Документация
Новая документация https://docs.yandex-team.ru/direct-dev/ (с иходники в [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/direct/docs/)). 

### Разработка
- Кластер разработки https://wiki.yandex-team.ru/direct/development/
- Коммуникации https://wiki.yandex-team.ru/direct/Development/howto/communications/

### Эксплуатация
Кластер на вики https://wiki.yandex-team.ru/jeri/

## Репозиторий в Аркадии
https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl
В 2007 году Директ был написан на Perl, часть этого кода в виде legacy лежит тут

https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa
Код на автотестов на Java для запуска в Aqua, собираются в jenkins, тоже своего рода legacy из времен когда автотестирование делалось в отдельной команде

https://a.yandex-team.ru/arc/trunk/arcadia/direct/autotests
Интеграционные тесты, но уже в Аркадии. Не зависят от внешних сервисов, гоняются покоммитно в аркадийном CI

### Приложения (не-микро-сервисы) из которых состоит Директ
- https://a.yandex-team.ru/arc/trunk/arcadia/direct/api5 - Внешнее API к Директу
- https://a.yandex-team.ru/arc/trunk/arcadia/direct/canvas - Бэкэнд конструктора креативов (Графических объявлений, HTML5, Видео)
- https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs - Повторяющиеся задачи на собственном шедулере
- https://a.yandex-team.ru/arc/trunk/arcadia/direct/logviewer - Сервис для просмотра логов Директа из clickhouse
- https://a.yandex-team.ru/arc/trunk/arcadia/direct/web - Бэкэнд обеспечивающий Swagger и GraphQl API для интефрейса
- https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/binlogbroker - Демон для заливки бинлогов mysql в Логброкер
- https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/chassis - Внутренний сайт/сервис для обслуживания разработки и эксплуатации
- https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system - Событийная система поверх бинлогов в Логброкере
- https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/mysql-direct-yt-sync - Зеркалирование (иногда с конвертаций) БД Директа в YT
- https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/user-action-log - Система обеспечивающая сбор и просмотр логов пользовательских действий в Директе
