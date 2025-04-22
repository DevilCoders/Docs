## Логи
Логи с машинок отгружаются при помощи push-client, детали можно поизучать в `tools/specs/base.yaml`

Существует разные логи:
 - логи балансера (покачто выключены, задача на подключение https://st.yandex-team.ru/PSTAVERN-44)
 - логи nginx отгружаются в YT и "почтовую" инсталяцию clickhouse
 - логи duffman :
    - access отгружаются в YT и "почтовую" инсталяцию clickhouse
    - http отгружаются в YT и "почтовую" инсталяцию clickhouse
    - master (пока не отгружается, нужно написать парсер для logfeller)

Директория в логброкере – https://logbroker.yandex-team.ru/logbroker/accounts/tavern/prod/?page=browser&type=directory

Топики отгружаются:
 - в почтовую инсталяцию КХ https://wiki.yandex-team.ru/pochta/sre/mail-logs/#tavern
 - YT https://yt.yandex-team.ru/hahn/navigation?filter=tavern&path=//home/logfeller/logs
