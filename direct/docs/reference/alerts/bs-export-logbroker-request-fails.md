# logbroker_request_fails
[juggler](https://juggler.yandex-team.ru/check_details/?host=direct.perl_bsexport&service=logbroker_request_fails&query=&last=1DAY)

## Описание { #description }
Включает в себя две проверки.

На этот алерт есть антифлап (20 минут), потом звонок и автоматический старт протокола (SPI).

### logbroker_write_fails_count

Проверяем количество ошибок при отправке данных экспортом в БК через logbroker за последние 3 минуты.
Ошибкой считается таймаут при взаимодействии с push-client (записи данных, закрытия подпроцесса) или получение ненулевого exit-code.

Зажигается warn если ошибок больше 3, crit'ом — если ошибок более 5% от числа успешных отправок
(чтобы алерт сработал даже от одной ошибки, если почему-то запросы упадут в ноль).

### logbroker_message_size_problems
Проверяем количество "сообщение превысило допустимый размер" при отправке данных экспортом в БК через logbroker за последние 10 минуты.
Зажигается при ненулевом количестве ошибок.

Означает, что мы формируем слишком большое сообщение (>12 Мб) по кампании или группе, и падаем даже не попытавшись отправить.

## Диагностика { #diagnostics }
Линия server_error (logbroker_write_fails_count) и client_error (logbroker_message_size_problems) на графике числа запросов:
<iframe height='400' width='100%' markdown="1"
src='https://solomon.yandex-team.ru/?graph=bsexport_requests_logbroker&legend=1&project=direct&b=3h&graphOnly=y&downsamplingAggr=default'></iframe>

## Решение { #solution }
Смотри [общую инструкцию по диагностике экспорта](../bs-export-diag.md#how-to) и соответствующие части:
- [{#T}](../bs-export-diag.md#logbroker-write-failed)
- [{#T}](../bs-export-diag.md#long-message)




