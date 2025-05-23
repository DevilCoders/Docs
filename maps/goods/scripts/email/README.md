# Скрипты для создания выборки email рассылки

## Использование
Соберите и запустите проект.

```
user$ ya make
user$ ./email
```
Это создаст табличку на YT по адресу:

[//home/maps/geoapp/goods/experimental_trash/email/selection](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/geoapp/goods/experimental_trash/email/selection)


Для записи в другую таблицу, укажите путь к ней через аргумент --output-table

```
user$ ./email --output-table '//home/maps/geoapp/goods/experimental_trash/email/selection_test'
```

Для выбора гипотез указываются доп флаги (./email --help для списка всех флагов).
Например, если мы хотим выборку в которой и организации которые давно не обновляли прайсы и организации без прайсов, но с прайсами в фичах, нужно
использовать:

```
user$ ./email -of
```

По умолчанию флаги -av, то есть организации без прайсов с рекламой и без прайсов с галочкой (verified_owner)


## Данные и гипотезы
Мы проверяем все **несетевые, неонлайн** организации из таблички
[company](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/geosearch_snapshot/company)
у которых в табличке
[company_to_owner](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/geosearch_snapshot/company_to_owner)
есть 'owner'.
Для каждой организации мы проверяем 5 гипотез:

|Гипотеза      |Описание|Флаг|
|--------------|--------------------------------------|----|
|WITH_OWNER_VER|организация без прайсов, но с галочкой|-v|
|HAS_ADS|организация без прайсов, но с активной рекламой|-a|
|HAS_GOODS_AS_FEATURES|организация без прайсов, но с товарами или услугами в фичах|-f|
|OUTDATED_PRICES|организация у которых прайслист не обновлялся более года|-o|
|NO_PRICES|организация без прайсов (без доп. ограничений)|-n|

В результирующей таблице для каждого **user_id** владельца (owner) перечисляются до 5 его организаций, которые попали под хотя бы одну из выбранных
гипотез, названия этих организаций и их permalink'и.

Если у пользователя более 5 организаций попавших под хотя бы одну из выбранных гипотез - он не попадает в выборку.

Так же в результирующей таблице есть колонки **comps_num** - количество компаний попавших в выборку для данного user_id, **all_rubrics** со всеми
рубриками выбранных компаний и **all_hypotheses** co всеми гипотезами которые подходят для хотя бы одной компании из списка.