# Как перелить табличку из PG в Yt

## Разовая переливка

1. В настройках [источника](https://yc.yandex-team.ru/folders/foohmq8ndf4kcdd7k28k/data-transfer/endpoint/dte99e0i9flqccj6g35p/edit) указываем "Список включённых таблиц" в формате `schema.table_name`. Можно несколько - каждая скопируется в свою yt-табличку.
2. [Здесь](https://yc.yandex-team.ru/folders/foohmq8ndf4kcdd7k28k/data-transfer/transfer/dttmqujb1baf3umq7ah7/view) жмём "Активировать"
3. Ждём статуса "Завершён"
4. Ваша табличка будет [тут](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mdm/transfer)

## Регулярная переливка

## Выгрузки MSTAT

{% note info "" %}

MSTAT поставка используется для небольших табличек, выгружающихся раз в день. Формирует прямой слепок таблички готовый для употребления.

{% endnote %}

Таблицы, создающиеся с помощью MSTAT: [тык!](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mdm)

#### Как создать новую поставку?
Как заводить выгрузку MSTAT подробно описано [в документации](https://a.yandex-team.ru/arc/trunk/arcadia/market/mstat/components/dictionaries-yt/README.md).
Если что-то пошло не так, хотлайн MSTAT [здесь](https://nda.ya.ru/t/ylKqELd_579M59).

---

## Инкрементальные выгрузки через репликатор

В двух словах принцип следующий:

1. Имеется наша таблица-источник в PostgreSQL с данными, которые мы хотим выгружать в Yt.
2. На эту таблицу-источник вешается индекс по `updated_ts` (если его ещё нет) - по времени фактического обновления строчки в БД.
3. В специальном яндексовом инструменте, который мы называем "Таксишный репликатор", настраивается правило репликации этой таблицы.
4. По этим правилам с помощью магии и волшебного дыма Репликатор перенесёт данные в партицированную по месяцам таблицу в Yt. Такая первично-реплицированная таблица называется `raw_history`.
5. С помощью другого инструмента Яндекса, который называется "Реактор", мы запускаем по крону специальные YQL. В этих YQL берутся сырые выгруженные данные из той самой `raw_history`, обогащаются и трансформируются произвольным нужным нам образом и insert-ятся в результирующую суточную таблицу уже в нашем каталоге в Yt.

{% note info "Инкрементальная!" %}

Инкрементальная поставка используется для больших таблиц, в которых **не происходят удаления**, так как репликатор накатывает в дифф только обновившиеся по таймштампу или создавшиеся записи. Поставка оказывается в YT посредством очереди MongoDB в виде json с полями. Для своих нужд мы используем raw history поставки.

{% endnote %}


{% cut "Схема доставки, позаимствованная из документации репликатора" %}

![Схема](../../_images/postgresql_transfer_1.png "Схема" =750x350)

{% endcut %}



#### [Да кто такой этот ваш raw history?](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/guides/market/replikacija-na-palcax/?from=%2Fmarket%2Fdwh-bi%2Fprocesses%2Fgreenplum%2Freplikacija-na-palcax%2F#prokakietakiepostavkidannyx)
Если вкратце, *raw* поставка - выгрузка диффами в единственную табличку, соответственно *raw history* это поставка партиционированная по дате обновления.

Таблицы, создающиеся с помощью репликатора такси: [тык!](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mdm/dictionaries)

{% cut "Внешние потребители таблиц с инкрементальной поставкой (критичное SLA)" %}

Таблица | Где используется | Дата начала использования | Ответственный | Комментарий
------ | ------ | ------ | ------ | ------
[reference_item](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mdm/dictionaries/reference_item/1d)  | iris   | 2019   | ts-slava@   | основной потребитель
[reference_item](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mdm/dictionaries/reference_item/1d) | lb_dumper (индексатор) | 2019 | evlyubimov@ | -
[reference_item](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mdm/dictionaries/reference_item/1d) | MBI (billing)  | - | @skiftcha @mexicano | -   
[reference_item](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mdm/dictionaries/reference_item/1d) | DWH   Системная аналитика данных маркета | 2021 | teleginaxenia@ | -   
[master_data](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mdm/dictionaries/master_data/1d) | Алгоритмы Репленишмента | - | teleginaxenia@ | влияет на процесс закупки; для получения useInMercury, периодически использовать для исключения из списка к перемещению в регионы товаров ЖП.   
[silver_items](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mdm/dictionaries/silver_items/1d) | DQ | - | evgeniyashes@ | -    

{% endcut %}


#### Как создается снапшот таблички, поставляемой репликатором?
Возьмем для примера [reference_item](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mdm/dictionaries/reference_item/1d).
- В реалтайм накатывается инкрементальная [поставка](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dwh/etl/raw_history/mdm/reference_item)  репликатора в последнюю табличку. Если актуальные данные в этой поставке отсутствуют, то стоит сходить в [админку репликации](https://tariff-editor.taxi.yandex-team.ru/replications/show/market_mdm) посмотреть логи. Для доступа в админку необходимы права которые можно запросить в IDM [подробнее](https://docs.yandex-team.ru/taxi-replication/docs/arcadia/access#dostup-k-adminke).
В случае непонятных обстоятельств хотлайн репликации [здесь](https://nda.ya.ru/t/w3Jx0QGF4TN9mH).
- По крону в [Реакторе](https://reactor.yandex-team.ru/browse?selected=10319384) запускается YQL (ссылка под `Parameters -> Query`). Чтобы отредактировать запрос, залогиньтесь во внутренней сети под роботом `robot-mdm-stable` ([секрет](https://yav.yandex-team.ru/secret/sec-01dwzc7zyhkayrw0zgte9w99w7/explore/versions)).
- [YQL](https://yql.yandex-team.ru/Operations/Yoz8xQVK8Fa3LpOnnrE2YqstJpOfm93xF_lSj4vYc6E=) парсит положенные в doc поля таблички, мержит дифф, кладет результат в dictionaries и удаляет старые таблички.

#### Как создать новую поставку?

Если уже есть настроенная виртуалка для работы с таксишным репликатором, то достаточно сгенерировать правило и далее следовать очень классной инструкции начиная с [шага 3](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/guides/market/replikacija-na-palcax/?from=%2Fmarket%2Fdwh-bi%2Fprocesses%2Fgreenplum%2Freplikacija-na-palcax%2F#shag3protestirovat
).

Пример команды для генерации master_data:
```
python3 rules_generator --source postgres --tables mdm.v_master_data_internalized --replicate-by modified_timestamp --scope market_mdm --options msk_timezone prepared_statement_disabled --scale large --responsible market --with-ext --primary-keys shop_sku supplier_id  --secret-source POSTGRES_MARKET_MBO_MDM
```
Подробное описание ключей можно найти [в документации утилиты](https://a.yandex-team.ru/arcadia/taxi/dmp/dwh/replication_rules#generaciya-pravil).

#### Что делать если я хочу свою таксишную среду для генерации?
 Для начала получить юпитерную [виртуалку](https://jupyter.yandex-team.ru/hub/spawn). Документация утилиты генерации правил отвечает на вопрос относительно развертки среды и та стала проще после переезда такси в аркадию.

 Если что-то пошло не так, можно попробовать обратиться к допотопным [решениям](https://st.yandex-team.ru/MBO-38041).
