# Запуск mbi-tariffs локально

## Инструкция
1. Открыть тарифницу и прочитать [Readme.md](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/tariffs/mbi-tariffs-server/README.md)
1. Собрать проект [как написано в readme](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/tariffs/mbi-tariffs-server/README.md#gde-vzyat-15-jdk)
1. Установить локально PostgreSQL 10.15 [как написано в readme](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/tariffs/mbi-tariffs-server/README.md#pro-bazu)
1. Создать конфигурацию [как написано в readme](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/tariffs/mbi-tariffs-server/README.md#lokalnyj-zapusk)
1. Создать локальный properties-файл по пути [src/main/properties.d/development](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/tariffs/mbi-tariffs-server/src/main/properties.d/development), в который добавить следующее:
    * `tariffs.robot.yt.token=enter_your_token_here`

        Токен можно взять найти на **[yt](https://yt.yandex-team.ru) > setting > auth > show my token**
    * Порт поднятой базы прописать сюда:

        `mbi-tariffs.postgresql.hosts=localhost:postgre_port`
    * Если при запуске ругается на ssl:

        `mbi-tariffs.postgresql.properties=sslmode=disable&targetServerType=master&prepareThreshold=0`

1. Запустить и подсоединиться к tms командой `telnet localhost 8083`

{% note info %}

В конфигурации необходимо указывать только полные пути

{% endnote %}
