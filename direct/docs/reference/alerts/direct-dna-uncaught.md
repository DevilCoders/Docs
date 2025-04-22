# direct_DNA_uncaught

## Описание { #description }
Порог на ошибки на фронте (в DNA).
Когда на фронте случается необработанное исключение мы пишем его в error-booster и click-daemon, по количеству ислючений есть график на пороговое значение которого есть алерт.
Проверка [juggler:direct_DNA_uncaught](https://juggler.yandex-team.ru/check_details/?service=direct_DNA_uncaught&host=yasm_direct_DNA_uncaught) см. также ссылки в правом верхнем углу на Голован, там исходные графики.

## Решение { #solution }
Разбирательствами с причинами загорания этой проверки занимается дежурный фронта. Пример диагностики есть можно посмотреть в тикете в разделе ссылок.

Ошибки фронта можно посмотреть в [Error-booster:direct front](https://error.yandex-team.ru/projects/direct/projectDashboard?filter=environment%20==%20production%20AND%20service%20empty) — в ссылке выборка сразу только по ошибкам фронта (без бэка)

## Подробности { #details }
Важно!! Несмотря на то, что при в error-booster пишутся также и ошибки бэкэнда, текущая проверка загорается только на превышение порогового значения ошибок фронта, т.к. только они попадают в click-daemon.
Записи в error-booster-е дублирующие и служат для диагностики, но при диагностике надо отфильтровать ошибки фронта.

## Ссылки { #links }
* Тикет с обсуждением проверки [DIRECT-111646](https://st.yandex-team.ru/DIRECT-111646)
* [Error-booster](https://error.yandex-team.ru)
* [github:RUM](https://github.yandex-team.ru/RUM/error-counter/) — ошибки с фронта пишем этой библиотекой, с помощью click-daemon
* [wiki:clickdaemon](https://wiki.yandex-team.ru/logs/clickdaemon/)
* [wiki:redirlog](https://wiki.yandex-team.ru/statbox/availabledata/redirlog/) — полезное, релевантное
