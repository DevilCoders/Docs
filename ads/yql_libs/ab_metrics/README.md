Что использовать
----------------
* ab_metrics_bschevent_ex.sql - ничего лишнего, пример запроса расчета метрик на bs-chevent;
* ab_metrics_ex.sql - много лишнего, подразумевает редактирование;

Как использовать
----------------
1. Скопировать содержимое ab_metrics_ЧТО-ТО_ex.sql, например, в окно запроса.

2. Присоединять либу ab_metrics.sql  
 Можно напрямую из аркадии. Нужно в Attachments -> Add URL указать:
 ```
 "ab_metrics.sql" "arc://ads/yql_libs/ab_metrics/ab_metrics.sql?rev=6135039"
 ```

 Подключить либу через основной запрос вот так нельзя.
 ```(yql)
 --PRAGMA File("ab_metrics.sql", "arc://ads/yql_libs/ab_metrics/ab_metrics.sql?rev=6135039");
 --ERROR File not found 
 --это ограничение для всех либ. Они могут быть только в аттаче,
 --потому что компилируются раньше, чем запрос
 ```

3. Настроить запрос.  
 Отредактировать ключи, условия грепа, сам финальный запрос (выбрать из закомментированных вариантов)

Замечания по секциям
--------------------
### $etalon_cnds
Подразумевается, что оставляет только один key. В противном случае для каждого эталона
будет отдельная строка, но понять какой это эталон нет возможности.


Нужен разрез не только по экспериментам, но и, например, по пейджам
-------------------------------------------------------------------
На примере [ab_metrics_yabar_ex.sql](https://a.yandex-team.ru/arc/trunk/arcadia/ads/yql_libs/ab_metrics/ab_metrics_yabar_ex.sql)
1. Нужно сварить поле *subkey* во входном логе
 В сабквери которое идет, например, в $raw_yabar_result, или любой другой $raw..result, добавить:
 ```(yql)
 $subkey_expr = ($t) -> {
     RETURN $t.page_id
 };

 DEFINE SUBQUERY $yabar_efh() AS
     FROM
         $yabar_efhwv_log($yabar_efh_log_infix, $start_date, $finish_date) AS t
     SELECT
         $key_expr(TableRow()) AS key,
         $subkey_expr(TableRow()) AS subkey, -- <====
         t.* WITHOUT subkey                  -- <==== удалить дефолтный ноль
     WHERE
         $event_cnds(TableRow());
 END DEFINE;
 ```
 Чтобы все это работало, внутри ab_metrics.sql во все логи уже добавленое дефолтное
 поле subkey: ```0 as subkey```, поэтому чтобы не было ругани про дубли, надо удалить дефолт

2. Сам запрос оформить, чтобы было видно subkey.
 ```yql
 -- Метрики по efh-логам
 FROM 
     $norm_result($result_yabar_efh, $etalon_cnds, $ratio, $metrics_to_norm) AS t
 SELECT 
     key AS KEY,
     subkey AS SUBKEY,  -- <=== куку
     metrics AS METRICS_D,
     $struct_for_columns($map_to_double(TableRow()), $metrics_to_show) AS METRICS,
     t.*
 into result t1_and_t2_and_orders_with_no_extended_geo;
 ```
