## Библиотека для создания junit тестов yql запросов.

Для работы библиотеки ваши запросы должны быть подготовлены к мокабельности.

Тут описано, как сделать свои запросы мокабельными: 
https://a.yandex-team.ru/arc/trunk/arcadia/market/pers/lib/yql-testable

Описание в вики https://wiki.yandex-team.ru/market/development/pers/market-pers-yt-tests/

### Как это работает
Для запуска теста нужно три параметра:
1) запрос (в файле или строкой) + название переменной для вычисления (по умолчанию yql)
2) json файл с ожидаемым результатом
3) мока (возможно несколько файлов)

```
runTest(
    loadScript("/yql/verified_grade.sql"),
    "/basic/verify_expected.json",
    "/basic/verify.mock"
);
```

При запуске теста
- парсится файл с моками, в //tmp по указанному пути создаются указанные таблицы
- вместо заголовка приклеивается заголовок-мока, перенаправляющая вызовы на таблицы-моки
- запускается yql запрос, результат сохраняется во временную таблицу
- результат из таблицы читается в json и проверяется с ожидаемым json-ом (без учёта порядка строк)

### Мокирование
Файл с моками описывает замены таблиц, каталогов, переменных и тд, позволяющих сделать выполнение yql скрипта детерминированным и достаточно быстрым.

Можно оставлять комментарии в начале строк # и пропускать любое количество строк. 
Парсер очень простенький и топорный, может не простить лишние пробелы в некоторых местах. Это не должно сильно мешать, но случиться может.

Примеры мок:
- https://a.yandex-team.ru/arc_vcs/market/pers/grade/pers-tms/src/test-yql/resources/agitation/lib_pay.mock
- https://a.yandex-team.ru/arc_vcs/market/pers/grade/pers-tms/src/test-yql/resources/agitation/paid_agitation_mail.mock
- https://a.yandex-team.ru/arc_vcs/market/pers/grade/pers-tms/src/test-yql/resources/agitation/paid_agitation_mail_flat.mock 

#### Мокирование таблицы
Все обращения к указанной таблице через `$_table(name)` будут превращены в обращения к соответствующей моке.
Мока таблицы генерируется в `//tmp/{basePath}/{uuid}`. 

Для использования вам нужно преобразовать запросы ```select * from `//my_lucky_table` ``` в `select * from $_table('//my_lucky_table')`

В схеме указываем стоблцы, которые будут в таблице, и их тип (тип берём из [TiType](https://a.yandex-team.ru/arc_vcs/yt/java/type_info/src/main/java/ru.yandex.type_info/TiType.java)).

Формат схемы: `имя_столбца:название_типа`. Схема может быть разбита на несколько строк. При повторе столбца используется последнее описание.
В схеме все поля optional для удобства написания тестов.

Далее описываем данные в json. Строка должна начинаться c {, чтобы парсер понял, что начинается объект. Объект 1 в 1 заливается в yt через java-клиент.

К примеру, есть запрос:
```
$pub_model_grades = (
    select * 
    from $_table('//home/cdc/market/production/pers-grade/tables/grade_grade')
    where state = 0 and type = 1 
);
```

Мока для него будет выглядеть вот так:
```
MOCK TABLE //home/cdc/market/production/pers-grade/tables/grade_grade
SCHEMA id:int64, state:int16, type:int16
SCHEMA resource_id:int64, author_id:int64, yandexuid:utf8, cr_time:string
{"id":1, "state":0, "type":1, "resource_id":1, "author_id":123, "yandexuid":"none", "cr_time":"2021-08-31T13:17:08+00:00"}
```

#### Мокирование каталога
Обращения к каталогам через `$_dir(path)` будут перенаправлены в каталог-моку.
Мока каталога таблицы создаётся в `//tmp/{basePath}/{uuid}`.

Внутри каталога-моки создаются таблицы с именнем, описанным в поле NAME.

К примеру, есть запрос:
```
$fresh_votes = (
    select * 
    from range($_dir('//home/cdc/market/production/pers-grade/tables/votes_daily'), $startDate, $endDate) --_INLINE_
);
```

Мока для него (может быть несколько: одна с таблицей, попадающей под фильтр, другая нет)
```
MOCK DIR_TABLE //home/cdc/market/production/pers-grade/tables/votes_daily
NAME 2020.01.05
SCHEMA grade_id:int64, author_id:int64, vote:int16, cr_time:string
{"grade_id":1, "vote":0, "author_id":123, "cr_time":"2021-08-31T13:17:08+00:00"}
```

#### Мокирование переменной-подзапроса
Заменяет указанную переменную на селект из `$_table('//..../{var_name}')`, ведущий в сгенерированную моку.
Исходное значение переменной остаётся рядом, под другим именем.

Для применения моки к запросу, переменная должна выглядеть как `$var_name = (`. Так было проще всего делать замену строки.

К примеру, есть запрос:
```
$model_rating = (
    select * 
    from $_table('//home/cdc/market/production/pers-grade/tables/model_rating') 
);
```

Мока для этой переменной:
```
MOCK VAR_TABLE $model_rating
SCHEMA model_id:int64, rating:double
{"model_id":123, "rating": 4.37}
```

Пример применения моки к скрипту:
```
$model_rating = ( select * from $_table('//tmp/yqltest/mocked_var/model_rating'));
$model_rating___mocked = ( select... [original content]
```

#### Мокирование простой переменной
Заменяет вызов `$var_name = .....` на значение, указанное в параметре SET.
Значение однострочное (пока что). Сделать многострочным в целом несложно, но пока не было нужно.

К примеру, есть незафиксированная переменная
```
$now = CurrentUtcDateTime();
```

Зафикисировать её для тестов можно так
```
MOCK VAR $now
SET DateTime::FromMilliseconds(1609459200000)
```

В результате в скрипте изменения будут такие
```
$now = DateTime::FromMilliseconds(1609459200000);
$now___mocked = CurrentUtcDateTime();
```


### Ограничения
- обращение к разным кластерам внутри одного запроса невозможно. Считается, что запрос выполняется в одном кластере. В локальном запуске это нестрашно, а вот в рецепте запрос упадёт. Решение можно придумать, но пока нет кейсов, где это было бы правда нужно.
- модификаторы вокруг таблиц (with schema и другое). Предполагается, что их нет. Можно обернуть такую таблицу в переменную, и мокировать саму переменную.
- подстановка `with inline` вокруг вызова range - крайне костыльная. Требует вставки якоря `--_INLINE_`, который выглядит ну очень грустно. Если он потеряется, тестовый запрос будет работать гораздо медленнее
- TableName не работает вместе с with_inline внутри range. Так что либо долго-долго ждать, либо смириться, что оно останется непротестированным
- замокировать можно только простой тип данных. К примеру, число, строку и тд. Структуру замокировать не выйдет (непонятно, как компактно и просто описывать её формат).


### Подключение
- junit5 модуль
- `PEERDIR (market/pers/lib/yql-test)`
  - также зависимость на вашу либу с yql запросами в classpath
  - либо просто ссылка на скрипты через `JAVA_SRCS`
- `INCLUDE(${ARCADIA_ROOT}/market/pers/lib/yql-test/yql_test_common.inc)`
- добавляем файл с пропертями теста (пример ниже)
- пишем тесты, наследуясь от `AbstractYqlTest`

Проперти помещаются в `resources/yql-test-application-custom.properties`
```
yqltest.jdbc.username=my_custom_robot - робот, под которым будут идти запросы
yqltest.yt.token=${YT_DEV_TOKEN:none} - токен для локального запуска, удобно использовать переменную окружения
yqltest.base.path=//tmp/my_custom_base_path/test - путь, внутри которого будут генерироваться таблицы-моки
yqltest.cleanAfterRun=true -- по умолчанию true, но бывает удобно иметь выключатель для отладки.
```

Настройки подклчюения к кластеру и рецепту прописаны [тут](https://a.yandex-team.ru/arc_vcs/market/pers/lib/yql-test/src/main/resources/yql-test-application.properties).
Если арнольд лежит, можно переключиться на хан. Но лучше не коммитить, запросы на хане выполняются всё же медленнее арнольда.

### Примеры
https://a.yandex-team.ru/arc_vcs/market/pers/grade/pers-tms/src/test-yql

Если у вас линукс, то можно просто зайти и запустить через ya make -ttt
У остальных запустить не получится, т.к. не прописан токен в YT_DEV_TOKEN.

Но можете подставить своего робота в проперти и прописать свой токен в переменной окружения YT_DEV_TOKEN, и тесты отработают.

### Как использовать при разработке и релизах
Текущая практика такая:
- при доработке скрипта дописываем тесты под него или проверяем, что существующие скрипты не падают, запустив вручную.
- если pr не горит - запускаем large тесты в нём. Рецепт поднимается медленно, но рано или поздно запустится
- при релизе есть кубик, прогоняющий тесты этого модуля. Он неблокирующий, но перед выкаткой в прод смотрим на него, если трогали скрипты.

Пример запуска тестов в пайплайне релиза (просто ya make -ttt над каталогом в sandbox джобе YA_MAKE)
https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/market-pers-grade-arc/release/61362f53e27ab92e2c82f6e2

