# Как написать контур выгрузки в БК на базе ESS

Упрощенно новый транспорт со стороны Директа работает следующим образом:
1. через ESS-контур получаем событие о том, что объект изменился и его надо синхронизировать с БК;
2. выгружаем объект в таблицу в YT на `markov` в [/home/adv](https://yt.yandex-team.ru/markov/navigation?path=//home/adv) а также записываем событие об изменении (создании, удалении) в CeaSar (TODO: ссылку на описание) откуда его подхватывает БК.

## ESS-контур
О написании ESS-контура есть соответствующая [документация](../ess/howto-code.md)

## Классы реализующие выгрузку в БК

### Сервис
Основное место с логикой транспорта, именно этот класс будет вызываться ESS Processor'ом из jobs.

* получает информацию об изменившихся объектах;
* обогащает ее дополнительными данными из БД Директа;
* вызывает YT-репозиторий для обновления данных в YT.

Данные в репозиторий передаются в виде специальных моделей, сгенерированных по protobuf-схеме (нужно для выгрузки в CeaSar).

Мапинг в из сообщений ESS (LogicObject) в модели CeaSar также происходит в этом классе.

Пример [BsExportCampaignService](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/bsexport/campaign/BsExportCampaignService.kt)

### YT-репозиторий
Класс-наследник [BaseBsExportYtRepository](https://a.yandex-team.ru/arc_vcs/direct/libs-internal/bstransport-yt/src/main/java/ru/yandex/direct/bstransport/yt/repository/BaseBsExportYtRepository.java).

Мэпит протобафные модели в записи YT.

Обновляет таблицу в YT, и, с некоторых пор, посылает сообщение в CeaSar.

Одновременная запись в YT и CaeSar происходит в методе [doRequest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/bstransport-yt/src/main/java/ru/yandex/direct/bstransport/yt/repository/BaseBsExportYtRepository.java?rev=r8160788#L104)

Пример [BaseBannerResourcesYtRepository](https://a.yandex-team.ru/arc_vcs/direct/libs-internal/bstransport-yt/src/main/java/ru/yandex/direct/bstransport/yt/repository/resources/BaseBannerResourcesYtRepository.kt)

### protobuf схема моделей
Описание моделей для общения с CeaSar

Пример таких файлов [proto/banner_resources](https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources)

По ним генерятся модели в виде java-классов в момент сборки проекта (`ya-ide-idea`)

### Внутренний отчёт для переотправки объектов по номеру кампании { #resync-tool }

Инструмент, переотправляющий объекты, связанные с заданными кампаниями, в БК.

Это работает так:
1. по номеру кампании ищутся её группы, ресурсы баннеров, корректировки, условия показа и т.д.
2. для этих сущностей генерируются логические объекты и отправляются соответствующим ESS-процессорам

Код находится [тут](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/internaltools/src/main/java/ru/yandex/direct/internaltools/tools/ess/sendcampaign),
а воспользоваться инструментом можно [здесь](https://direct.yandex.ru/internal_tools/#ess_send_campaigns_content).

{% note warning %}

При разработке нового контура отчёт надо дополнить. Для этого нужно реализовать интерфейс [CampaignContentRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/internaltools/src/main/java/ru/yandex/direct/internaltools/tools/ess/sendcampaign/repository/CampaignContentRepository.kt), пример: [CampaignMultipliersRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/internaltools/src/main/java/ru/yandex/direct/internaltools/tools/ess/sendcampaign/repository/CampaignMultipliersRepository.kt).

{% endnote %}

## Конфиги
Для работы выгрузки в YT-таблицу, путь к этой таблице надо указать в [конфиге](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf?rev=7263479#L579)
Также надо обновить конфиги для других сред.

Пример [коммита](https://a.yandex-team.ru/arc/commit/7263579#file-/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf:R583)
