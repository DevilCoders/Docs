UrlChecker
==========
Ходим через [Зору](https://wiki.yandex-team.ru/market/development/abo/zora/) по урлам оферов.

Мониторинги
-------
https://juggler.yandex-team.ru/check_details/?service=pricechart-info-http&host=market_corba
https://solomon.yandex-team.ru/?project=market-abo&dashboard=urlchecker

Сборка
------
```
ya make
```

Запуск
------
Локально:
`DebugMain.java` в /test/java - запуск с embedded базой

Релиз: https://tsum.yandex-team.ru/pipe/projects/abo/release/new/urlchecker

Checkstyle
----------

[@SuppressWarnings](https://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-suppress_warnings.htm)
