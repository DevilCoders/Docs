# Локальные серверы whois

@startuml
cloud "External whois servers" as ext_whois {
}

component whois.yandex.net {
}

package dc1-whois01 {
[PgSQL_Master]
[RabbitMQ]
[irrd]
}

package dc2-whois01 {
[PgSQL_Slave]
[RabbitMQ.]
[irrd.]
}

PgSQL_Slave --> PgSQL_Master
irrd -> PgSQL_Master
irrd --> RabbitMQ

irrd. -> PgSQL_Slave
irrd. --> RabbitMQ.

irrd --> ext_whois

whois.yandex.net --> irrd
whois.yandex.net --> irrd.

@enduml

Дабы при построении префикс-листов не заваливать тяжелыми запросами внешние серверы whois, была поднята локальная инсталляция. На текущий момент(май 2022) происходит переезд со старой инсталляции(живущей на noc-sas и noc-myt) на новую(живущую на %nocdev-whois). Основным потребителем данных является RackTables. Точкой входа является балансер whois.yandex.net .

Данные отдаются из [irrd][1], для нормальной работы ему требуется локальный PostgreSQL и RabbitMQ. Так же требуется IPv4-адрес для синка с внешними зеркалами.

Инстансы PostgreSQL реплицируются(дабы обе машины отдавали одинаковые данные). Для управления репликацией используется [repmgr][2]. В Salt есть логика, которая отключает для irrd хождение во внешние зеркала в случае, если irrd запущен на реплике, поэтому после переключения репликации нужно будет дополнительно прогнать Salt.


[1]: <https://irrd.readthedocs.io/en/stable/>
[2]: <https://repmgr.org/docs/current/index.html>
