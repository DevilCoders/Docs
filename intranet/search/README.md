# Поиск по интранету

**Миссия сервиса** – отвечать на вопросы сотрудников Яндекса.

**Цель** – единый поиск по всему интранету. У пользователя должна быть
возможность найти любую информацию в интранете с помощью поисковой строки
на странице любого из внутренних сервисов.

## Полезные ссылки
* [описание сервиса в abc](https://abc.yandex-team.ru/services/isearch/)
* [http://search.yandex-team.ru/](http://search.yandex-team.ru/)
* [wiki](http://wiki.yandex-team.ru/intranetpoisk)
* [трекер](https://st.yandex-team.ru/ISEARCH)
* [админка](http://search.yandex-team.ru/_admin/sources/)
* [тестинг](http://search.test.yandex-team.ru/)
* [qloud](https://qloud-ext.yandex-team.ru/projects/tools/intrasearch)
* [документация SaaS](https://doc.yandex-team.ru/Search/saas/saas-overview/concepts/about.html)
* [вики-страница SaaS](https://wiki.yandex-team.ru/jandekspoisk/SaaS/)
* [админка SaaS](https://saas-mon.n.yandex-team.ru/?my=1)
* [проект в Нирване](https://nirvana.yandex-team.ru/project/isearch)

## Точки входа во время разработки

[Про разработку](https://wiki.yandex-team.ru/IntranetPoisk/Development/howto/)

Запустить локально поиск: ```make run```

Запустить локально тесты: ```make test```

## Сборка релиза:
0. Установить и настроить [релизер](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/releaser#установка)
1. ```releaser release``` (находиться нужно в корне проекта arcadia/intranet/search)

## Документация
* [Факторы](docs/factors.md)
* [Источник](docs/source.md)


to be continued...
