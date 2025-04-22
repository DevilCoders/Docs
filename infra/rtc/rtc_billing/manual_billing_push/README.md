Граф для запуска ручного пуша:

https://nirvana.yandex-team.ru/flow/28ee2e6f-b5e6-4ee2-ba54-782fb3e2555c/8f9821b2-854e-4b58-a992-de8fb3ad719a/graph

Для того чтоб его запустить, необходимо:
1. Склонировать инстанс графа
2. (опционально) В кубике ManualRTCBillingPush заменить переменные YT_TOKEN и ABC_TOKEN на актуальные
3. В кубике ManualRTCBillingPush DATE_HOUR_STRING_START и DATE_HOUR_STRING_FINISH выставить время, за которое необходимо запустить пуш в 
формате "YYYY-mm-dd_HH". Если оставить DATE_HOUR_STRING_FINISH пустым, то процедура запустится только за один час. Часы
для запуска указаны включительно.
4. (опционально) Проверить, что запись данных прошла успешно: данные за нужный период можно посмотреть так:
https://yql.yandex-team.ru/Operations/YDy2BtK3DINFKlz2DdVfsuiQyTkIC34QPa3yoxqj_pI=
Подставив нужный source_wt (можно посмотреть в данных самого кубика). Данные попадают с задержкой в 3+ часа. 
Чтобы проверить факт записи в топик logbroker, можно посмотреть на графики:
https://lb.yandex-team.ru/lbkx/accounts/yc/yandex/billing-qloud
https://lb.yandex-team.ru/lbkx/accounts/yc/yandex/billing-yp
https://lb.yandex-team.ru/lbkx/accounts/yc/yandex/billing-gencfg


NB: При запуске за длительные интервалы (10 часов и более) единовременно, граф может ООМиться. Для решения этой проблемы
необходимо увеличить значение параметра Max. RAM, Mb в кубике ManualRTCBillingPush

