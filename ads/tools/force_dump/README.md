
Предельно простая тулза

`./force_dump --task_id shoutpva_test_dump --last_log_date 20191103 --token <тут токен> --new_last_log_date 20191105`

Возьмет дамп с `task_id=shoutpva_test_dump` и `last_log_date=20191103` и проставит ему `last_log_date=20191105`

Если какая-то линейка сломана:
 * ищем первый **не** сломаный дамп забираем из него `last_log_date`
 * прикидываем eta починки вычитаем 1 день - это `new_last_log_date`
 * запускаем тулзу

Тулза спросит, готовы ли вы ломать продашн, надо проверить, что все ок и напечатать `y`
 
 