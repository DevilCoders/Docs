Система сравнения данных
========================

[Вики](https://wiki.yandex-team.ru/check/)

Сборка пакетов
--------------

Deb/rpm пакеты собираем тут:

- https://teamcity.yandex-team.ru/project.html?projectId=Billing_Reports_DCS

где:

  - `yandex-balance-dcs` - это deb пакет для выкладки python кода
  - `Liquibase` - это rpm пакет для выкладки миграция БД

Выкладка пакетов
----------------

Выполняется тут:

- https://c.yandex-team.ru/packages/yandex-balance-dcs/tickets

Ветки имеют следующий смысл:

  - `testing` - выкладывать указанную версию в тестовое окружение
  - `hotfix / stable` - выкладывать в прод
