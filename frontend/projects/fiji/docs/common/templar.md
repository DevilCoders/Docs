# Templar

> Внимание! Информация в разделе устарела и в ближайшее время будет актуализирована.

* [Быстрый старт ](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/templar#Быстрый-старт-на-примере-fiji)
* [FAQ](https://wiki.yandex-team.ru/search-interfaces/infra/templar/faq/)

### Автотесты

После создания PR, автоматически создаются беты для `perl-report`, `templar` и `report-renderer`. Однако, эти беты не предназначены и не используются для прогона автотестов. Во время запуска hermione тестов в TeamCity, на каждом агенте поднимается свой инстанс templar, на котором и прогоняются тесты.

Упрощённо и в TeamCity, и локально, тесты нужно запускать с помощью команды `fiji hermione`, которые поднимают внутри себя `templar` с включённым режимом чтения кэша, стаба тумбнейлов.

Автособранные беты на templar работают без кэша и стаба картинок.

Чтобы корректно работали `hermione` тесты необходимо предварительно собрать проект с `YENV=testing`.

Чтобы запустить `templar` без кэша, но с застабленными картинками (кому такое может быть интересно?) — `NODE_ENV=testing templar start`.

### Cache-mode
Чтобы запустить `templar` отдельно в том же режиме, в каком запускаются тесты (использование кэша и стаб картинок) — `templar start --cache-mode=read`.

[Про создание кэша для тестов](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/report-cache/README.md).

### Pre-search

> Отключить `presearch` можно, подставив user-agent: `Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)`. На данный момент templar работает в режиме без `preasearch`.

Локальные беты по-умолчанию работают в режиме full-search.
Для того чтобы протестировать функциональность с включенным pre-search необходимо:
1. Добавить в нужную платформу `presearch:true` в файле [.templar/config.js](https://github.yandex-team.ru/mm-interfaces/fiji/blob/c63f30f6bfc2b57737f5016b72f0e2033fce1c9a/.templar/config.js)
![](https://jing.yandex-team.ru/files/andysh/2018-09-27_15-11-37.png)
2. Перезапустить темплар
3. Проверить: в терминале на каждое обновление страницы должно уходить 2 запроса: первый запрос с параметром ``export=json_pre``, второй с параметром ``export=json``

<a name="selenium-set"></a>
