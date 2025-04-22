# Структура сервиса

![Общая схема работы](diagrams/Service_Structure.png)

Компоненты:

1. [signal_acceptor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/signal_acceptor)
	- веб-сервис на Flask, который реализует [Backoffice API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bizdir/sps/docs/BackofficeApi.md) СПП
	- принимает сигналы, складывает их в БД
	- умеет выдавать наружу статус сигнала
2. [sprav_loader](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/sprav_loader)
	- регулярно ищет в БД сигналы без информации об организации
	- загружает информацию из экспорта Справочника и обновляет сигнал
3. [signal_processor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/signal_processor)
	- регулярно ищет в БД сигналы без созданных гипотез, создаёт гипотезы для сигналов
	- умеет размечать атрибуты как совпадающие с текущим значением в карточке
	- на этапе прототипа умел автоматически создавать задания на валидацию и искать дубликаты для новых организаций, до production это не добралось.
4. [validator](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/validator)
	- регулярно ищет в БД задания на валидацию, которые не отправлены в колл-центр, и посылает их туда
	- регулярно ищет в БД задания для колл-центра, по которым ещё не получен результат, и опрашивает колл-центр
	- при получении результата обновляет гипотезу
5. [yang](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/yang) – адаптер, который преобразует API yang в [API колл-центра](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bizdir/callcenter)
6. [workstation/api](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/workstation/api)
	- веб-сервис на Flask, который реализует [Workstation API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bizdir/sps/docs/WorkstationApi.md)
	- отдаёт контент-менеджерам информацию про гипотезы
	- принимает от них вердикты
	- при соответствующем вердикте создаёт задания на валидацию
	- при соответствующем вердикте создаёт диффы для отправки в Справочник
7. [workstation/frontend](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/workstation/frontend)
	- UI АРМ контент-менеджера
	- React + TypeScript
8. [exporter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/exporter)
	- регулярно ищет в БД диффы, которые не отправлены в Справочник, и посылает их туда
	- регулярно ищет в БД отправленные диффы, по которым ещё не получен результат, и опрашивает Справочник
	- при получении результата от Справочника обновляет сигнал, на этом обработка гипотезы завершается.

Все компоненты собираются в один общий [бинарник](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/bin)
