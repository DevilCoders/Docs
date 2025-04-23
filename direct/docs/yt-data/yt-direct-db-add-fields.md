{% include [links](_includes/links.md) %}

# Выгрузка данных в YT //home/direct/db

## Как это устроено

Каждую ночь джоба [`HomeDirectDbOperationsJob`](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/java/ru/yandex/direct/jobs/directdb/HomeDirectDbOperationsJob.java)
запускает пачку YQL запросов, которые попали в сборку jobs из каталога <https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/export/home-direct-db>.

Обычно эти запросы собирают данные со всех шардов из динамических таблиц mysql-synс, делают джойны и прочие преобразования,
и складывают результат в статические таблицы в `//home/direct/db` в удобном для пользователей формате.

Выгрузка производится на кластерах:

 - Hahn <https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db>
 - Arnold <https://yt.yandex-team.ru/arnold/navigation?path=//home/direct/db>


## Когда надо добавлять что-то в выгрузку

TODO какие-нибудь рекомендации: когда делать новую таблицу,
когда расширять существующую, когда предложить потребителям обойтись имеющимися данными.


## Как добавить новую таблицу или поле в выгрузку

Надо добавить новый YQL запрос в директорию с ресурсами: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/export/home-direct-db>,
или отредактировать существующий.

При добавлении/удалении запросов стоит иметь в виду, что выгрузка может [поломаться](#reliz-s-dobavleniem-yql-vo-vremia-vygruzki-lomaet-vygruzku)
в зависимости от времени выкладки.  
TODO: как именно выполнять рекомендацию "иметь в виду".

### Требования к YQL-запросам

- файл в репозитории должен находиться в корне директории <https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/export/home-direct-db>,
- имя файла должно заканчиваться на `.yql`.
- в каждом запросе должна быть запись в результирующую таблицу таким образом:
```yql
INSERT INTO $output_table_name WITH TRUNCATE
SELECT ...
```
- имя результирующей таблицы берется из названия файла с запросом.

(TODO: А что будет, если вместо `$output_table_name` написать явное название?)

#### Пример 

Вот пример выгрузки, которая собирает данные со всех шардов и выдаёт в отсортированном виде:
```yql
INSERT INTO $output_table_name WITH TRUNCATE
SELECT pid, mw_id FROM EACH($shardedTable('adgroups_minus_words'))
ORDER BY pid, mw_id;
```

### Рекомендации к YQL-запросам

- Полезно добавить сортировку по столбцам, которые формируют уникальный ключ (в примере выше — `pid` и `mw_id`).
- Будьте осторожны с джойнами по ключам, которые могут повторяться в разных шардах. Например автоинкрементных.  
Если джойнить такие ключи, строки будут дублироваться, т.к. строка из одного шарда будет джойниться со строками
в других шардах с тем же ключом. Чтобы этого избежать, можно использовать синтетический столбец `__source__`, который
добавляется к каждой таблице в mysql-sync.
- Избегайте использования питоновских UDF в запросах. Говорят, что это существенно замедляет их выполнение
- При выгрузке большой таблицы с большим количеством джойнов, вам может помочь [стратегия YQL Star JOIN](https://clubs.at.yandex-team.ru/yql/2786).  
Пример, как это сделано для таблицы `banners`: <https://st.yandex-team.ru/DIRECT-117815#5ea2cba8d6b0cd1652c64060>

### Полезные ништяки для писателей запросов
Перед запуском каждого запроса к нему приписывается заголовочный файл [`include/common.yql`](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/export/home-direct-db/include/common.yql),
где описываются полезные прагмы, переменные и функции.

#### $shardedTable { #sharded-table }
Функция `$shardedTable($table)` возвращает список путей к таблице `$table` со всех шардов базы `PPC`.
Его удобно использовать в сочетании с YQL функцией [`EACH`](https://yql.yandex-team.ru/docs/yt/syntax/select/#each).

Например запрос
```yql
SELECT bid FROM $shardedTable('banners')
```
выберет все айдишники баннеров со всех шардов.

#### $dictTable { #dict-table }
Функция `$dictTable($table)` возвращает путь к таблице `$table` из базы `PPCDICT`.

#### $convertToRubUDF { #convert-to-rub-udf }
Функция `$convertToRubUDF($sum, $currency)` переводит сумму `$sum` из валюты `$currency` в рубли
и возвращает результат в виде строки с шестью знаками после запятой.

Курсы валют собираются из таблицы `ppcdict.currency_rates` и хардкодятся в текст запроса на этапе запуска.
Если валюты `$currency` не было в этой таблице, функция вернёт `NULL`.

## Известные проблемы
### Релиз с добавлением YQL во время выгрузки ломает выгрузку
Джоба запускает YQL один раз, после появления нового снепшота mysql-sync. Но готовой выгрузка считается только тогда,
когда кол-во выполненных YQL равно кол-ву YQL в приложении java-jobs _на момент проверки_.
Из-за этого выгрузка не будет считаться готовой, если до её завершения выложится релиз java-jobs с добавлением
или удалением YQL

Чинится здесь: [https://st.yandex-team.ru/DIRECT-117659](https://st.yandex-team.ru/DIRECT-117659)
