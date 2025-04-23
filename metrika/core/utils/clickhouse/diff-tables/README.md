# clickhouse-diff-tables

Тулза для сравнения количества записанных событий на mtmoblog и mtmobgiga по дням. На оба кластера пуляется запрос, в ответе которого первым параметром должно быть целочисленное значение. Если не заданы `-h2/-d2/-t2/-q2`, то используются из первого кластера. Вывод в формате
`[ok|failed]: from date_from till date_till,count1,count2,count2-count1`.

```
usage: clickhouse-diff-tables [-h] -h1 HOST1 [-h2 HOST2] -d1 DATABASE1
                              [-d2 DATABASE2] -t1 TABLE1 [-t2 TABLE2] -q1
                              QUERY1 [-q2 QUERY2] --date-from DATE_FROM
                              --date-till DATE_TILL
                              [--date-days-step DATE_DAYS_STEP]
                              [--output-skip-empty] [--output-skip-ok]
                              [-p CLICKHOUSE_SETTINGS CLICKHOUSE_SETTINGS]
                              [-v [{info,information,warn,warning,critical,error,debug,fatal}]]

optional arguments:
  -h, --help            show this help message and exit
  -h1 HOST1, --host1 HOST1
  -h2 HOST2, --host2 HOST2
  -d1 DATABASE1, --database1 DATABASE1
  -d2 DATABASE2, --database2 DATABASE2
  -t1 TABLE1, --table1 TABLE1
  -t2 TABLE2, --table2 TABLE2
  -q1 QUERY1, --query1 QUERY1
  -q2 QUERY2, --query2 QUERY2
  --date-from DATE_FROM
  --date-till DATE_TILL
  --date-days-step DATE_DAYS_STEP
  --output-skip-empty
  --output-skip-ok
  -p CLICKHOUSE_SETTINGS CLICKHOUSE_SETTINGS, --clickhouse-parameter CLICKHOUSE_SETTINGS CLICKHOUSE_SETTINGS
                        Any of ClickHouse key-value session settings
  -v [{info,information,warn,warning,critical,error,debug,fatal}], --verbose [{info,information,warn,warning,critical,error,debug,fatal}]
                        verbose level

For example
./clickhouse-diff-tables -d1=mobile -t1=installations_all -h1=mtmoblog01-01-1.yandex.ru -h2=mtmobgiga001-1.metrika.yandex.net -q1="SELECT uniqExactIf((APIKey, TrackingID, InstallationDate, intHash32(DeviceIDHash), InstallationID), APIKey != 1111) FROM {database}.{table} WHERE InstallationDate >= '{date_from}' and InstallationDate < '{date_till}'" --date-from='2020-04-01' --date-till='2020-07-01'
```

```
drobus@drobus:~/arc/metrika/core/utils/clickhouse/diff-tables$ ./clickhouse-diff-tables -d1=mobile -t1=installations_v2_all -t2=installations -h1=localhost -q1="select sum(sipHash64(APIKey)) from {database}.{table} WHERE InstallationDate >= '{date_from}' and InstallationDate < '{date_till}' and APIKey != 1111" -q2="select sum(sipHash64(APIKey)) from {database}.{table} WHERE EventDate >= '{date_from}' and EventDate < '{date_till}' and APIKey != 1111" --date-from='2009-12-31' --date-till='2018-06-19' --date-days-step=30 --output-skip-empty
[ok]: from 2009-12-31 till 2010-01-30: 88527642012334692, 88527642012334692, 0
[ok]: from 2015-01-04 till 2015-02-03: 86455921423282714, 86455921423282714, 0
[ok]: from 2016-10-25 till 2016-11-24: 4706252226636645567, 4706252226636645567, 0
[ok]: from 2016-12-24 till 2017-01-23: 11286324407645736141, 11286324407645736141, 0
[ok]: from 2017-01-23 till 2017-02-22: 13403231173070853221, 13403231173070853221, 0
[ok]: from 2017-02-22 till 2017-03-24: 9790769286110321786, 9790769286110321786, 0
[ok]: from 2017-03-24 till 2017-04-23: 1774732829974015387, 1774732829974015387, 0
[ok]: from 2017-04-23 till 2017-05-23: 5066354830871928671, 5066354830871928671, 0
[ok]: from 2017-05-23 till 2017-06-22: 4587278859092685167, 4587278859092685167, 0
[ok]: from 2017-06-22 till 2017-07-22: 7767079812390721220, 7767079812390721220, 0
[ok]: from 2017-07-22 till 2017-08-21: 5097163747061013621, 5097163747061013621, 0
[ok]: from 2017-08-21 till 2017-09-20: 2003107478538270871, 2003107478538270871, 0
[ok]: from 2017-09-20 till 2017-10-20: 8889138957126388900, 8889138957126388900, 0
[ok]: from 2017-11-19 till 2017-12-19: 8889138957126388900, 8889138957126388900, 0
```
