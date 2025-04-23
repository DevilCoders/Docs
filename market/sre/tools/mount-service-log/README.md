mount-service-log
====================

Утилита для подключения логов няня-сервисов к logview через rfs-протокол

Общее описание и принцип работы
-------------------------------

mount-service-log должна вызываться либо через sudo, либо от пользователя root. Параметрами является список нян-сервисов, которые нужно смонтировать.
Монтируются в подкаталоги /mnt/nanny по-сервисно, пример: `/mnt/nanny/test_report_market_vla/17050@vla1-4543.search.yandex.net`

Ссылки
------

[sandbox job to build debian package](https://sandbox.yandex-team.ru/task/215290176/view)
