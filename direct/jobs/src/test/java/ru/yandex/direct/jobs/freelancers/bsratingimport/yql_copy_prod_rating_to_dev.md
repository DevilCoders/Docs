### YQL запрос для заполнения таблицы с рейтингом для отладки
Полезен для случая, когда хочется задать рейтинг специалистам на devtest.

Итоговую таблицу удобно использовать в [`FreelancerBsRatingImportJobManualTest`](FreelancerBsRatingImportJobManualTest.java).

### Запрос
```
use hahn;

$source_table = [home/bs/freelancers/direct/export/2018-11-16];
$result_table_date = "2018-11-17";
$result_table_name = "//home/direct/tmp/maxlog/freelancers/bs_rating/" || $result_table_date;

/* 
Запрос для получения SELECT'ов:
dbs-sql -B dt:ppc:all "select concat('SELECT ', ClientID, ' as ClientID UNION ALL') from freelancers" | tail -n +2
*/
$dt_fls = (
SELECT 100 as ClientID UNION ALL
SELECT 940045 as ClientID UNION ALL
SELECT 1590606 as ClientID UNION ALL
SELECT 2034502 as ClientID UNION ALL
SELECT 2186671 as ClientID UNION ALL
SELECT 2277397 as ClientID UNION ALL
SELECT 2283785 as ClientID UNION ALL
SELECT 2885774 as ClientID UNION ALL
SELECT 3265519 as ClientID UNION ALL
SELECT 4378289 as ClientID UNION ALL
SELECT 2213706 as ClientID UNION ALL
SELECT 4510129 as ClientID UNION ALL
SELECT 4877175 as ClientID UNION ALL
SELECT 4917135 as ClientID UNION ALL
SELECT 5878743 as ClientID UNION ALL
SELECT 7296373 as ClientID UNION ALL
SELECT 30473586 as ClientID UNION ALL
SELECT 6589323 as ClientID UNION ALL
SELECT 7834420 as ClientID UNION ALL
SELECT 8002175 as ClientID UNION ALL
SELECT 5936090 as ClientID UNION ALL
SELECT 8927380 as ClientID UNION ALL
SELECT 104268974 as ClientID UNION ALL
SELECT 15066524 as ClientID UNION ALL
SELECT 31459774 as ClientID UNION ALL
SELECT 32275500 as ClientID UNION ALL
SELECT 34996461 as ClientID UNION ALL
SELECT 33964774 as ClientID UNION ALL
SELECT 104407655 as ClientID UNION ALL
SELECT 104195938 as ClientID UNION ALL
SELECT 104202565 as ClientID UNION ALL
SELECT 38662868 as ClientID UNION ALL
SELECT 47062890 as ClientID UNION ALL
SELECT 47063590 as ClientID UNION ALL
SELECT 47064665 as ClientID UNION ALL
SELECT 47097064 as ClientID UNION ALL
SELECT 48178983 as ClientID UNION ALL
SELECT 39165414 as ClientID UNION ALL
SELECT 40447487 as ClientID UNION ALL
SELECT 43250741 as ClientID UNION ALL
SELECT 43913659 as ClientID UNION ALL
SELECT 47063810 as ClientID UNION ALL
SELECT 47063844 as ClientID UNION ALL
SELECT 47069696 as ClientID UNION ALL
SELECT 47206945 as ClientID UNION ALL
SELECT 47230202 as ClientID UNION ALL
SELECT 47544071 as ClientID UNION ALL
SELECT 48174488 as ClientID UNION ALL
SELECT 48185664 as ClientID UNION ALL
SELECT 48188527 as ClientID UNION ALL
SELECT 49195191 as ClientID UNION ALL
SELECT 39521276 as ClientID UNION ALL
SELECT 46776966 as ClientID UNION ALL
SELECT 47063107 as ClientID UNION ALL
SELECT 47063563 as ClientID UNION ALL
SELECT 47063695 as ClientID UNION ALL
SELECT 47064292 as ClientID UNION ALL
SELECT 47064682 as ClientID UNION ALL
SELECT 47076090 as ClientID UNION ALL
SELECT 47249142 as ClientID UNION ALL

/* Новый специалист, или потерянный в рейтинге ОКР */
-- SELECT 47630127 as ClientID UNION ALL

/* Несуществующий ClientID */
SELECT 90000000 as ClientID
);

$total_freelancers = (SELECT count(*) FROM $dt_fls);

INSERT INTO $result_table_name
WITH TRUNCATE 
SELECT 
    CAST(A.ClientID as Uint64) as client_id,
    ratings,
    production_freelancer_rating,
    A.freelancer_rank as freelancer_rank,
    $result_table_date as date,
    A.total_freelancers as total_freelancers
FROM (
SELECT
    ClientID,
    row_number() OVER w as freelancer_rank,
    $total_freelancers as total_freelancers /*оконная функция count(*) тут не работает*/
FROM $dt_fls
WINDOW w AS ()) as A
JOIN $source_table as B
ON (B.freelancer_rank = A.freelancer_rank);
```
