mbi-cli
================

[Скачать](https://a.yandex-team.ru/api/tree/blob/trunk/arcadia/market/mbi/mbi-tools/mbi-cli/mbi-cli)


Установка
---------

[Инструкция по установке](https://wiki.yandex-team.ru/mbi/mbi-cli/install/)

Файл настроек
-------------

[Настройки](https://wiki.yandex-team.ru/mbi/mbi-cli/settings/)


Возможности
-----------

* [Бинарный поиск по логам](https://wiki.yandex-team.ru/mbi/mbi-cli/logs/),
  там где это возможно для того, чтобы мгновенно получать доступ к нужному фрагменту лога
* Простое выполнение любой  [команды на удалённой машине](https://github.yandex-team.ru/market-java/mbi-tools/wiki/mbi-cli-%D0%B2%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BD%D0%B0-%D1%83%D0%B4%D0%B0%D0%BB%D1%91%D0%BD%D0%BD%D0%BE%D0%B9-%D0%BC%D0%B0%D1%88%D0%B8%D0%BD%D0%B5)
* [Bash/zsh completion](https://wiki.yandex-team.ru/mbi/mbi-cli/remote/)
* Интеграция с RTC сервисами:
  [partner-api](https://wiki.yandex-team.ru/mbi/mbi-cli/partner-api/),
  [mbi-partner](https://wiki.yandex-team.ru/mbi/mbi-cli/mbi-partner/),
  [mbi-api](https://wiki.yandex-team.ru/mbi/mbi-cli/mbi-api/),
* Поддержка [подключения к консоли mbi-billing](https://wiki.yandex-team.ru/mbi/mbi-cli/mbi-billing/#m-console)
* Поиск по логам на logview:
  [mbi-billing](https://wiki.yandex-team.ru/mbi/mbi-cli/mbi-billing/),
  [report-generator](https://wiki.yandex-team.ru/mbi/mbi-cli/report-generator/)
* [Быстрый доступ к clickhouse](https://wiki.yandex-team.ru/mbi/mbi-cli/clickhouse/)
* [Доступ к актуальной shops.dat и suppliers.dat в MDS](https://wiki.yandex-team.ru/mbi/mbi-cli/mds/)
* [Интеграция с report'ом](https://wiki.yandex-team.ru/mbi/mbi-cli/report/)
* Поддержка [jconsole для mbi-partner](https://wiki.yandex-team.ru/mbi/mbi-cli/mbi-partner/#m-jconsole)
* [Интеграция с Nanny](https://wiki.yandex-team.ru/mbi/mbi-cli/nanny/)
* [Интеграция со Startrack](https://wiki.yandex-team.ru/mbi/mbi-cli/startrack/)

Примеры
-------

Актуальный список команд можно получить при помощи команды `mbi-cli help`.

------------------------------------------------------------------------------------------------------------------------

Получить фрагмент лога приложения mbi-partner в котором содержится обработка запроса с
Request-ID: 1533032434616/856cab20da964ef45acb63d34b230a7e и сохранить его в файл `~/mbi-partner.log`

````
mbi-cli mbi-partner trace 1533032434616/856cab20da964ef45acb63d34b230a7e >~/mbi-partner.log
````

------------------------------------------------------------------------------------------------------------------------

Получить треддамп работающего приложения
````
./mbi-cli mbi-partner thread-dump vla1-4714 | tee ~/threaddumps/`date '+%Y%m%d_%H%M%S'`_vla1-4714_thread_dump.log
````

------------------------------------------------------------------------------------------------------------------------

Подключится к консоле mbi-billing в тестинге

````
mbi-cli mbi-billing console -t
````

------------------------------------------------------------------------------------------------------------------------

Получить фрагмент лога report-generator с машины mbi01e.market.yandex.net начинающийся в 2018-07-30 15:44:33
и сохранить его в файл `~/rg.log`

````
mbi-cli report-generator logs mbi01e.market.yandex.net '2018-07-30 15:44:33' >~/rg.log
````

------------------------------------------------------------------------------------------------------------------------

Получить статус тикетов MBI-30011 и MBI-29307

````
mbi-cli startrack issue-status MBI-30011 MBI-29307
````

------------------------------------------------------------------------------------------------------------------------

Получить информацию о офере (в продакшене на синем маркете) с `feed_id` равным 500554 и `shop_sku` равным 2240206

````
mbi-cli report offerinfo --marketplace beru 500554 2240206
````

------------------------------------------------------------------------------------------------------------------------

Прокинуть порт 1235 с машинки vla1-4714.search.yandex.net в RTC под сервисом mbi-partner в локальный порт 8080

````
mbi-cli mbi-partner ssh-port-forward --local-port 5015 --remote-port 1235 vla1-4714
````
