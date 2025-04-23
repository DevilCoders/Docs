## Подключение библиотеки в проект

Библиотека подключается в проект благодаря spring-boot-autoconfigure. Для того чтобы конфигурация начала
инициализироваться, необходимо указать пять обязательных настроек: ```yt.static.proxy```, ```yt.static.username```,
```yt.static.token```, ```yt.static.module.source``` и ```uw.moderation.yt.root```. Весь перечень настроек проекта:

1. ```yt.static.proxy``` - имя кластера YT, к которому отправляются запросы.
2. ```yt.static.username``` - имя пользователя.
3. ```yt.static.token``` - токен пользователя для доступа к данным.
4. ```yt.static.module.source```- модуль, из которого идут
   запросы. [Все модули](https://a.yandex-team.ru/arc_vcs/market/jlibrary/request/request-utils/src/main/java/ru/yandex/market/request/trace/Module.java)
   для трассировки.
5. ```uw.moderation.yt.root``` - путь в YT, по которому будут сохраняться таблицы с задачами на модерацию и
   результатами.
6. ```uw.moderation.yt.prefix``` - базовый префикс для названия таблицы. По умолчанию ```uw-moderation-request```.
7. ```uw.moderation.yt.suffix``` - суффикс для таблицы с результатами модерации. По умолчанию ```moderated```.

## Тестирование приложения с использованием библиотеки

Чтобы написать функциональные тесты, необходимо сделать следующее:

1. Прописать в ```ya.make``` ```INCLUDE(${ARCADIA_ROOT}/market/adv/inc/yt_test.inc)```.
2. Использовать библиотеку [adv-shop/yt-test](https://a.yandex-team.ru/arc_vcs/market/adv/adv-shop/yt-test/README.md).
