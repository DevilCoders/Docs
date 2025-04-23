# YT STAT && YT DIFF
Утилиты подсчитывают статистику по cgi параметрам в логах YT

Работают на кластере (быстро + ничего не скачивают)

Нужен [токен](https://yt.yandex-team.ru/docs/gettingstarted#auth) в `~/.yt/token`

Чтобы распечатать таблицу, добавьте `-p`

## YT STAT
Считает количество и процент cgi параметров

## YT DIFF
Получает на вход две статистики (лежат в YT) и выдает разность в доле cgi параметров

### За подробностями в `--help` к утилитам

## Пример
Хотим посчитать дифф между `[9:00-9:30)` и `[9:30-10:00)`

```shell
./yt_stat --cluster arnold -i "//logs/market-main-report-log/30min/2021-08-02T09:00:00" -o "//tmp/stats/A"

./yt_stat --cluster arnold -i "//logs/market-main-report-log/30min/2021-08-02T09:30:00" -o "//tmp/stats/B"

./yt_diff --cluster arnold --first "//tmp/stats/A" --second "//tmp/stats/B" -o "//tpm/diff/DONE" -p
```

# Solomon

На регулярной основе подсчетом статистики и отправкой её в Solomon занимается `MARKET_REPORT_AUTOMATIC_STAT`

# Sandbox
Для удобства создал `MARKET_REPORT_CALC_DIFF`

Скрывает промежуточные этапы, просто подаете логи и временные промежутки, а получаете файл в знакомом формате

```text
   diff%     count1(  prc1%)    count2(  prc2%) value

param
  -1.54%   20001718( 66.53%)  19197956( 64.98%) show_explicit_content
   1.48%   16668885( 55.44%)  16816282( 56.92%) rgb
  -1.45%   26024975( 86.56%)  25143348( 85.11%) rearr-factors
   1.35%   16611774( 55.25%)  16723095( 56.61%) test-buckets
  -1.34%   11989958( 39.88%)  11386927( 38.54%) showdiscounts
```
