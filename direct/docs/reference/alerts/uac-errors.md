# uac-*

- [yasm_uac_page_errors:uac_page_errors](https://juggler.yandex-team.ru/project/yasm.ambry.simple/aggregate?host=yasm_uac_page_errors&service=uac_page_errors&project=yasm.ambry.simple) - количество клиентских ошибок (desktop + mobile)
- [yasm_uac_server_errors:uac_server_errors](https://juggler.yandex-team.ru/project/yasm.ambry.simple/aggregate?host=yasm_uac_server_errors&service=uac_server_errors&project=yasm.ambry.simple) - количество серверных ошибок
- [yasm_uac_server_response_time_ms:uac_server_response_time_ms](https://juggler.yandex-team.ru/project/yasm.ambry.simple/aggregate?host=yasm_uac_server_response_time_ms&service=uac_server_response_time_ms&project=yasm.ambry.simple) - время ответа node-js-сервера

## Решение { #solution }
Разбирательствами с причинами загорания этой проверки занимается [дежурный фронта UAC](https://abc.yandex-team.ru/services/direct/duty/?role=4844&lang=ru).