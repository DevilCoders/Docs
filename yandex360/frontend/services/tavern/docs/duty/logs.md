1. Логи балансеров никуда не отгружаются, можно почитать только прямо на машинках – https://wiki.yandex-team.ru/awacs/logs/ . До самих балансеров можно добраться кликнув "Service ID" в списке L7 балансеров – https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tavern.production.mail.yandex.net/show
2. Логи nginx и duffman
    2.1 При помощи logfeller (https://logbroker.yandex-team.ru/logbroker/accounts/tavern/prod/?page=browser&type=directory) отгружаются в:
        - YT c (задержка до часа) – https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tavern.production.mail.yandex.net/show
        - почтовую инсталяцию clickhouse (задержка 15с) – https://wiki.yandex-team.ru/pochta/sre/mail-logs/#tavern
