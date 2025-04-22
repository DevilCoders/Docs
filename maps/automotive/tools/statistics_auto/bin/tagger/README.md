# Применение

Утилита предназначена для поиска и тэгирования проблемных ГУ.

# Запуск

    $ ./automotive-tools-tagger TAGGER_RUNNER[ --date DATE][ --dry-run]

`TAGGER_RUNNER` -- одно из следующих значений:
* `HeadKeyConflictRunner` -- повесить тег possible_head_key_conflict
* `HeadNoAttachRunner` -- повесить тег possible_head_no_attach
* `HeadOfflineRunner` -- повесить тег possible_head_offline
* `HeadOfflineUntagRunner` -- снять тег possible_head_offline
* `HeadTouchBrokenRunner` -- повесить тег possible_head_touch_broken
* `HeadSimIssuesRunner` -- повесить тег possible_head_sim_issues
* `HeadSimIssuesUntagRunner` -- снять тег possible_head_sim_issues
* `OldAppBuildRunner` -- повесить тег yaauto_update_firmware
* `OldAppBuildUntagRunner` -- снять тег yaauto_update_firmware
* `HeadGpsIssuesRunner` -- повесить тег possible_head_gps_issues
* `WrongHeadFwRunner` -- повесить тег possible_wrong_head_fw
* `WrongHeadFwUntagRunner` -- снять тег possible_wrong_head_fw
* `WrongRelatedCarsRunner` -- повесить тег possible_wrong_head_id

Список актуален на момент составления. Полный список можно посмотреть в хэлпе: `$ ./automotive-tools-tagger -h`

`--dry-run` -- опция отключает навешивание и снятие тега; в этом режиме будет произведён расчёт проблемных голов и вывод их в stdout.
`--date DATE` -- задаёт дату для произведения расчёта в формате YYYY-MM-DD.

# Добавление нового тега

Для добавления нового тега:
1. Составить SQL запрос на выборку машин, попадающих под критерий нового тега. Выборка должна содержать поля:
    * `city` ("MSK", "SPB", "KZN" и т.д.)
    * `car_id`
    * `head_id`
    * `plate` (госномер в формате "О660ХЕ750")
    * `model` (модель автомобиля)
    * `imei`
    * `firmware` (версия прошивки)
    * `app_ver` (версия лончера)

Сохранить файл с запросом сюда: `maps/automotive/tools/statistics_auto/sql/SQL_FILENAME.sql`

2. Создать python-класс, унаследованный от [`TaggerWithYqlQuery`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tools/statistics_auto/pylib/tagger/common/tagger.py?rev=6370219#L64) в случае **навешивателя** тегов, и унаследованный от [`UntaggerWithYqlQuery`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tools/statistics_auto/pylib/tagger/common/tagger.py?rev=6370219#L120) в случае **снимателя** тегов. Этот класс и будет выполнять всю работу.
Метод `__init__()` создаваемого класса должен вызвать соответствующий метод базового класса: `super().__init__(date, tag, dry_run, query_resource)`. Здесь:
    * `date` -- дата, за которую будет производиться расчёт
    * `tag` -- навешиваемый тег
    * `dry_run` -- если True, то фактического навешивания/снятия тега не произойдёт, только вывод машин на экран
    * `query_resource` -- имя ресурса, указанного в ya.make, соответствующего ранее созданному `SQL_FILENAME.sql`
При необходимости кастомные параметры, необходимые SQL-запросу, задаются в `__init__()` после вызова `super().__init__()`. Их необходимо добавить в словарь `self.parameters` ([пример](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tools/statistics_auto/pylib/tagger/wrong_relations_tagger.py?rev=6370219#L17)).
Если для выполнения SQL-запроса необходимо дождаться обновления или создания определённых таблиц, то необходимо переопределить метод `_prepare` ([пример](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tools/statistics_auto/pylib/tagger/wrong_relations_tagger.py?rev=6370219#L19))
.py-файл с эти классом положить сюда: `maps/automotive/tools/statistics_auto/pylib/tagger/TAG_TITLE_tagger.py`

3. В соответстввующие секции `maps/automotive/tools/statistics_auto/pylib/tagger/ya.make` добавить ранее созданные `TAG_TITLE_tagger.py` и `SQL_FILENAME.sql`

4. Создать python-класс runner, который будет инстанцировать добавляемый тегер (из позапрошлого шага) и, при необходимости, передавать ему кастомные параметры. Пример с описанием методов, которые необходимо переопределить при добавлении кастомных параметров можно посмотреть [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tools/statistics_auto/bin/tagger/runner/example.py). В случае, если кастомные параметры не требуются, в создаваемом классе достаточно задать поле класса `tagger = TAGGER_CLASS_NAME`; никаких дополнительных действий не требуется ([пример](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tools/statistics_auto/bin/tagger/runner/head_offline.py))
Файл с runner'ом положить сюда `maps/automotive/tools/statistics_auto/bin/tagger/runner/TAG_TITLE.py`.

5. В `maps/automotive/tools/statistics_auto/bin/tagger/runner/ya.make` добавить созданый файл.

6. Отправить на ревью, добавив в ревьюверы ruckus@ и/или dtyo@.

# Дополнительная информация

Скрипт складывает данные о помеченных машинах в таблицу [//home/maps/automotive/broken_head_units/tagged_cars](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/automotive/broken_head_units/tagged_cars)
