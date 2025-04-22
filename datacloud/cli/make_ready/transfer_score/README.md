# Transfer Score

Утилита для выставления задачи на заливку таблицы со скором на YDB

## Параметры бинарника
- `-h, --help` Вызвать хэлп
- `-p <PARTNER_ID>, --partner-id <PARTNER_ID>` <Required> (например bank_mega_capital, sberkoff)
- `-s <SCORE_NAME>, --score-name <SCORE_NAME>` <Required> Score name (например bmc_aml_xprod_1103, sberkoff_xprod_889_20180508)
- `-d <DATE_STR>, --date-str <DATE_STR>` <Required> Date Str (например 2019-01-01)

## Важно помнить:
- После выполнения таски будет запущенка цепочка всех последующих операция в графе
