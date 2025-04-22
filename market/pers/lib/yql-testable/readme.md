## Небольшая библиотека для обеспечения мокабельности yql запросов.

Сами yql-тесты будут пишутся и запускаются в java, а эта библиотека нужна только для адаптации вашего кода и превращения запросов в мокабельные.

На текущий момент эта либа доступна только для java-кода. 
Расширение на другие языки также возможно, если вы готовы в этом поучаствовать. 
Приходите к ilyakis, если хотите поучаствовать в разработке и расширить либу на свой язык (кода тут строк 50).

Либа для запуска тестов описана тут: https://a.yandex-team.ru/arc/trunk/arcadia/market/pers/lib/yql-test

### Поключение в ya.make
Подключаем либу в ya.make для того, чтобы класс YqlTestable стал доступен в вашем коде.
```
PEERDIR(
    market/pers/lib/yql-testable
)
```

### Мокабельность
Для обеспечения мокабельности нужно обернуть обращения к таблицам и каталогам в специальные функции
- `$_table(path)` - транслирует 1 в 1 запрс к таблице. В тестах подменятся на запрос к моке. 
- `$_dir(path)` - возвращает 1 в 1 указанный путь. В тестах меняется на замокированный путь.

Также можно подставить специальные метки, чтобы упростить тестирование
- `--_INLINE_` - превратится в пустоту в обычном запуске. В тестах подставит `with inline`, что значительно ускоряет вычисление при условии, что все обращения к таблицам заинлайнены.

Запросы к `$_table(path)` из коробки заинлайнены. Если не забыть расставить `--_INLINE_` около range и тд мест, то запрос будет выполнен очень быстро (около минуты, как правило).
Если забыть его поставить, запрос в тесте отработает, но медленнее, чем мог бы. Прошёл инлайн или нет - хорошо виден в yql-консоли на вкладке прогресса запроса.

Инлайн не всегда возможен и допустим. В этих случаях можно замокировать весь подзапрос, вынеся его в переменную.
- `TableName()` не работает с инлайном (на момент написания либы)
- могут быть другие ограничения

### Использование

```
# файл /path/to/script.sql
$yql = (
    select a.*, b.field
    from $_table("//my_path/dir1/table") as a
    left join range($_dir("//my_path/dir2"), "2020.01.01") --_INLINE_
);

# прочитать запрос из файла
String orig = YqlTestable.readFile("/path/to/script.sql");

# загрузка файла в переменную с подстановкой заголовка-моки и селекта.
String yql = YqlTestable.withAll(orig, "yql");

# подставить только заголовок, без селекта. Нужно, если селект вы подставляете отдельно.
String yqlOnlyHeader = YqlTestable.withHeader(orig);

# подставить только селект из указанной переменной, без заголовка. Вдруг пригодится
String yqlOnlySelect = YqlTestable.withSelect("/path/to/script.sql", "yql");

```

### Пример, как превратить запрос в мокабельный
```
-- смотрим на отзывы за последние 90 дней
$gradeThresholdDate = DateTime::MakeTimestamp(CurrentUtcTimestamp()) - Interval("P90D");

$grades = (
    select g.*,
        $parseTmDate(g.cr_time) as cr_time_yt
    from `//home/cdc/market/production/pers-grade/tables/grade_grade` as g
    where g.state = 0
    and g.type in (1, 2)
    and $parseTmDate(g.cr_time) > $gradeThresholdDate
    and g.verified is null
);

$orders = (
    select model_id, yandexuid, cast(passportuid as Int64) as passportuid,
        DateTime::MakeTimestamp(DateTime::FromMilliseconds(cast(`timestamp` as UInt64))) as cr_time_yt
    from range(`//home/market/production/ugc/order_delivery`)
);


select distinct g.id
from $grades as g
         join $orders as p on g.author_id = p.passportuid and g.resource_id = p.model_id
where g.cr_time_yt >= p.cr_time_yt
  and g.author_id is not null

union all

select distinct g.id
from $grades as g
         join $orders as p on g.yandexuid = p.yandexuid and g.resource_id = p.model_id
where g.cr_time_yt >= p.cr_time_yt
  and g.author_id is null and g.yandexuid is not null
```

#### Что нужно поправить в запрсое
1) обращение к `//home/cdc/market/production/pers-grade/tables/grade_grade`
2) обращение к `range('//home/market/production/ugc/order_delivery')`
3) текущая дата `$gradeThresholdDate` (для детерменированности теста)
4) добавить `--_INLINE_` после range (для скорости, заинлайнит таблицы и посчитает быстрее)
5) обернуть селект в переменную (например, $yql)

Изменения
```
-    from `//home/cdc/market/production/pers-grade/tables/grade_grade` as g
+    from $_table('//home/cdc/market/production/pers-grade/tables/grade_grade') as g

-    from range(`//home/market/production/ugc/order_delivery`)
+    from range($_dir('//home/market/production/ugc/order_delivery')) --_INLINE_

-  select distinct g.id
+  $yql = (select distinct g.id

-  and g.author_id is null and g.yandexuid is not null
+  and g.author_id is null and g.yandexuid is not null);
```

Моки, которые нужны в этом запросе:
- мока таблицы отзывов
- мока каталога с заказами
- мока переменной $gradeThresholdDate для подмены даты
