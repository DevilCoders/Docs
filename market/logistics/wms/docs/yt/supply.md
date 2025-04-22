**Увоз таблиц в YT репликатором такси**

### С чего начать
Прочитать [руководство](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/guides/market/replikacija-na-palcax/#dljarabotysadminkojjtaksi), подготовить [окружение](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/guides/market/marketstat-over-taxi/?from=%2Fmarket%2Fprojects%2Fmarketstat%2Fmarketstat-over-taxi%2F#poshagam).

Все последующие пункты описаны для [архивов](https://wiki.yandex-team.ru/delivery/fulfilment/wms/inforwms/?from=%2Fusers%2Fmoisandrew%2Finforwms%2F).

### 1. Подготовить данные для VIEW
1.1. По [примеру](https://st.yandex-team.ru/WINADMINREQ-14876) завести тикет на увозимую таблицу. Дождаться выполнения.
1.2 В увозимой таблице заполнить updated_at, если оно пустое
```
update SCPRD.wmwhse1.SERIALINVENTORY set UPDATED_AT=GETUTCDATE() where UPDATED_AT IS NULL;
```
Примеры для больших таблиц см. в комментах к [MARKETWMS-16122](https://st.yandex-team.ru/MARKETWMS-16122).
#### 1.3 Создать VIEW
VIEW должен отдавать все колонки таблицы, добавляя whs и whs_id()

[Пример](https://a.yandex-team.ru/arc_vcs/market/logistics/wms/app/db-migrations/liquibase/migrations/views/vYtSerialInventory.sql).

Раскатать на все архивные базы в [пайплайне миграции] (https://tsum.yandex-team.ru/pipe/projects/wms/delivery-dashboard/wms-db-migration).
#### 1.4 Создать индекс на поле UPDATED_AT в увозимой таблице
Действие не требуется, если индекс уже существует.
[Пример](https://a.yandex-team.ru/arc_vcs/market/logistics/wms/app/db-migrations/liquibase/migrations/views/vYtSerialInventory.sql).

### 2. Написать правило репликации c учетом требований по партицированию
Партиции в [raw](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/guides/market/replikacija-na-palcax/#raw) необходимо назначать по неизменяемому полю типа Datetime, обычно это adddate.

#### 2.1. Определить размер таблицы на архиве Софьино:
````
EXEC sp_spaceused  'schema_name.TABLE_NAME'
GO
````
Пример выполнения для `PICKDETAIL`:

|name          |rows                |reserved  |data      |index_size|unused   |
|--------------|--------------------|----------|----------|----------|---------|
|PICKDETAIL    |108449582           |566391384 KB|136289536 KB|410742088 KB|19359760 KB|

Далее число из колонки `data` умножить на два и перевести в гигабайты. 

#### 2.2 Выбрать размер партиции по алгоритму:
Число, полученное в предыдущем пункте, перевести в гигабайты, назначить партицирование:
- **tiny**: таблица до 1Gb, raw - не партиционируем, raw_history - по годам
- **middle**: таблица до 100Gb, raw - по годам, raw_history - по месяцам
- **large**: таблица более 100Gb, raw/raw_history - по месяцам
  
[Пример](https://github.yandex-team.ru/taxi-dwh/dwh/blob/develop/replication_rules/replication_rules/market_wms/yt_pick_detail.yaml) готового правила для таблицы ~100 GB.

### 3. table.py для raw, table.py для ods и loader.py
[Пример table.py для raw](https://github.yandex-team.ru/taxi-dwh/dwh/blob/develop/market_ba_etl/market_ba_etl/layer/yt/raw/wms/pickdetail/table.py),

[Пример table.py для ods](https://github.yandex-team.ru/taxi-dwh/dwh/blob/develop/market_ba_etl/market_ba_etl/layer/yt/ods/wms/pickdetail/table.py),

[Пример loader.py](https://github.yandex-team.ru/taxi-dwh/dwh/blob/develop/market_ba_etl/market_ba_etl/layer/yt/ods/wms/pickdetail/loader.py).

Разложить пустые файлики  \__init\__.py как в примерах.
Не забыть про [config.yml](https://github.yandex-team.ru/taxi-dwh/dwh/blob/develop/replication_rules/replication_rules/market_wms/plugins/config.yaml)

### Про нейминг. Очень важно
Без соблюдения [этих](https://wiki.yandex-team.ru/dmp/architecture/object-naming/#pravilanaimenovanijaatributov) требований ревью не пройти. 
Для этого:
1. Привести все поля к lower_camel_case. Пример из [loader.py](https://github.yandex-team.ru/taxi-dwh/dwh/blob/develop/market_ba_etl/market_ba_etl/layer/yt/ods/wms/pickdetail/table.py):
```
warehouse_id='whsid',
```
2. Снабдить все описываемые поля русскоязычными комментариями. См. пример из [table.py](https://github.yandex-team.ru/taxi-dwh/dwh/blob/develop/market_ba_etl/market_ba_etl/layer/yt/ods/wms/pickdetail/table.py):

```
warehouse_id = String(comment='Идентификатор склада', sort_key=True)
```
Избегать суффиксов _key в полях, заменяя их на _id.

Запушить все созданные файлы в свой бранч.

### 4. Запустить заливку в raw
Запросить [доступы](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/guides/market/replikacija-na-palcax/#dljarabotysadminkojjtaksi) и запустить согласно [шагу 3](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/guides/market/replikacija-na-palcax/#shag3protestirovat) руководства.

### 5. Потестировать ods-таску на Юпитерной виртуалке
Заходим на юпитернуя виртуалку пр ssh. (Описано [здесь](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/guides/market/marketstat-over-taxi/?from=%2Fmarket%2Fprojects%2Fmarketstat%2Fmarketstat-over-taxi%2F#poshagam) 
Склонировать репу dwh:
```
$git clone git@github.yandex-team.ru:taxi-dwh/dwh.git
```
Перейти на свой бранч:
```
$git checkout mybranch
```
Отредактировать config/default/greenplum.yaml
Добавить в конце
```
dev_prefix:
default: 'staff-login'
```
Отредактировать config/default/yt.yaml
заменить строку
```
_market_prefix: &market_prefix '//home/market/production/mstat/dwh'
```
на
```
_market_prefix: &market_prefix '//home/market/prestable/mstat/dwh'
```
Подготовить ENV. Выполнить последовательно:
```
1. $python3.7 -m tox -e dev
2. $source .env3/bin/activate
3. $source bin/activate
```
Запустить таску:
```
./bin/dmp-cli run backfill ods_wms_pickdetail_streaming --no-lock > dmp-cli.log 2>&1
```
Название таски указывается в файле [loader.py](https://github.yandex-team.ru/taxi-dwh/dwh/blob/develop/market_ba_etl/market_ba_etl/layer/yt/ods/wms/pickdetail/loader.py).

Успехом можно считать нижеприведенную строку в конце логе:
```
2021-11-24 12:34:28.628 pid=12956 MainThread run_id=bc8c9afc-ee1f-4452-a6e4-3930cda215ab    INFO dmp_suite.py_env.exit_hook: py process {python ./bin/dmp-cli run backfill ods_wms_pickdetail_streaming --no-lock} ended by success
```
И появление данных в ods. [Пример](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/market/prestable/mstat/dwh/ods/wms/pickdetail/2021).
### 6. Дождаться аппрувов от ревьюверов и выкатить
Назначить [Катерину Лебедеву](https://staff.yandex-team.ru/kateleb) или [Анну Малофееву](https://staff.yandex-team.ru/lyutanica) ревьюверами, поправить замечания (если есть),
затем схлопнуть коммиты с правильным коммит-мессаджем как указано в [п.4](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/guides/market/replikacija-na-palcax/#shag4vykatit).
Далее можно ничего не делать и ожидать пока кто-нибудь выкатит (обычно 1-2 дня). Если горит, то выкатывать как указано в [п.5](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/guides/market/replikacija-na-palcax/#vykatkavstejjbl). 

Примечание: ODS и RAW катятся разными релизами и разными командами.

### Про мониторинг ###
В конфиге [DEV_TEAMS](https://juggler.yandex-team.ru/check_details/?host=market-wms-yt-replication&service=wms-yt-replication&project=market.wms&last=1DAY) заведена группа **wms**.
После выкатки правил, автоматом заводятся джаглерные машинки. Примеры [здесь](https://juggler.yandex-team.ru/check_details/?host=taxi-dwh.task&service=ods_wms_serial_movement_streaming&project=taxidwh&last=7DAYS) и [здесь](https://juggler.yandex-team.ru/check_details/?host=taxi-dwh.task&service=ods_wms_itrn_streaming&project=taxidwh&last=7DAYS).  
На [дашборде](https://juggler.yandex-team.ru/dashboards/wms-prod-dash) заведена агрегированная [плашка](https://juggler.yandex-team.ru/check_details/?host=market-wms-yt-replication&service=wms-yt-replication&project=market.wms&last=1DAY), где логикой OR объединяются и выводятся все состояния всех поставок - см. [конфиг](https://a.yandex-team.ru/arc_vcs/market/sre/conf/market-alerts-configs/configs/market-wms-yt-replication.yaml) Малька. 

Также, может быть полезно [почитать](https://wiki.yandex-team.ru/delivery/development/monitorings-manual/) о мониторингах и [HOWTO Малек](https://wiki.yandex-team.ru/market/sre/fordev/howto-market-alerts-configurator/).

### Если ошибка ModuleNotFoundError: No module named 'lazy_object_proxy'
Лечение.
- активировать окружение, перейти в dwh.
- проверить bin/dmp-cli conf yt.nile_package_path
- скорее всего оно выдаст /usr/lib/yandex/taxi-dmp-deps-wheel-py3
- удалить все из этой папки
- python tools/update_wheel.py dmp_deps/py3/requirements-nile.txt .taxidwh-deps-wheel-py3
- он нагенерит колес в эту папку .taxidwh-deps-wheel-py3
- из нее скопировать все в /usr/lib/yandex/taxi-dmp-deps-wheel-py3

### Полезные ссылки
- [FAQ группы автоматизации](https://wiki.yandex-team.ru/taxi/backend/automatization/faq/)
- [YT: зачем Яндексу своя MapReduce-система и как она устроена](https://habr.com/ru/company/yandex/blog/311104/)
- [Сервис Yandex.Taxi Replication](https://docs.yandex-team.ru/taxi-replication/docs/arcadia/how_to_start)
- [Хранение данных](https://wiki.yandex-team.ru/taxi/backend/datastorage/#chatpodderzhki)
- [Чатик поддержки](https://nda.ya.ru/t/w3Jx0QGF4TN9mH)
