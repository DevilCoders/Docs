# Инструмент определения наиболее широко сработавших правил

Данная тулза предназначена для поиска тех колдунщиков, которые матчатся наибольшее число раз.
Так данный инструмент позволяет быстро определить wizard_id правила, срабатывающего, например, на всем потоке.

Входные параметры:
- `--period` - отвечает за то, [какие агрегированные данные нужно собрать](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yasm/yasmapi#periody). По умолчанию пятисекундные
- `--end_ts` - до какого момента нужно собирать данные в виде таймстемпа. По умолчанию end_ts = current timestamp
- `--period_count` - число периодов. По умолчанию = 12 => сбор данных по умолчанию происходит за минуту
- `--output` - название файла с выходными данными

Выходной файл имеет вид:
```
Link to golovan - https://yasm.yandex-team.ru/chart/hosts=ASEARCH;itype=proxywizard;ctype=prod;prj=fastres2;signals=...
Number of wizard matches within 60 seconds:
    605274		unistat-wizard_warning_about_trash_information_ukraine_version_6_num_matches_dmmm
    605273		unistat-wizard_testing_full_potok_num_matches_dmmm
    139228		unistat-wizard_nav_query_exp_command_num_matches_dmmm
     65157		unistat-wizard_q_ask_offer_num_matches_dmmm
     65157		unistat-wizard_test666_num_matches_dmmm
...
```
- ссылка на голован с собранными сигналами
- список собранных wizard_id, отсортированных в порядке убывания показов
