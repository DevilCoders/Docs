1.3.7
-----
 * PYPI-285 fetch_package with quarantine  [ https://a.yandex-team.ru/arc/commit/9744116 ]

[terrmit](http://staff/terrmit) 2022-07-20 03:03:56+03:00

1.3.6
-----

* [terrmit](http://staff/terrmit)

 * PYPI-216 release file upload_time field  [ https://a.yandex-team.ru/arc/commit/9373746 ]

* [dsamuylov](http://staff/dsamuylov)

 * ARCANUM-5510 prepare migration from .devexp.json to a.yaml (intranet)  [ https://a.yandex-team.ru/arc/commit/9231012 ]

* [maratik](http://staff/maratik)

 * feat: startrek integration for PYPI ARCANUM-5357

feat: startrek integration  [ https://a.yandex-team.ru/arc/commit/9140539 ]

* [shadchin](http://staff/shadchin)

 * IGNIETFERRO-1154 Rename contrib/python/requests_toolbelt to contrib/python/requests-toolbelt  [ https://a.yandex-team.ru/arc/commit/9123261 ]

[terrmit](http://staff/terrmit) 2022-04-20 12:50:54+03:00

1.3.5
-----

* [maratik](http://staff/maratik)

 * Revert commit r9099909                                                        [ https://a.yandex-team.ru/arc/commit/9100108 ]
 * feat: startrek integration for PYPI ARCANUM-5357

feat: startrek integration  [ https://a.yandex-team.ru/arc/commit/9099909 ]

* [shadchin](http://staff/shadchin)

 * CONTRIB-2153 Update amqp from 2.6.1 to 5.0.9, kombu from 4.6.3 to 5.2.3, celery from 4.3.0 to 5.2.3                                                                                                  [ https://a.yandex-team.ru/arc/commit/9091829 ]
 * DEVTOOLSSUPPORT-12493 Drop ResourceFinder

Текущая реализация `library.python.django.contrib.staticfiles.finders.ResourceFinder` эквивалентна `django.contrib.staticfiles.finders.FileSystemFinder`  [ https://a.yandex-team.ru/arc/commit/8711107 ]

* [tikhonov-ka](http://staff/tikhonov-ka)

 * PYPI-164: Не скачивать пакеты через приложение PYPI

PYPI-164: Не скачивать пакеты через приложение PYPI  [ https://a.yandex-team.ru/arc/commit/8797785 ]

[terrmit](http://staff/terrmit) 2022-02-04 13:01:35+03:00

1.3.4
-----

[tikhonov-ka](http://staff/tikhonov-ka) 2021-10-06 18:34:36+03:00
PYPI-172 (localshop)

1.3.3
-----
 * PYPI-170 simple-detail optimization  [ https://a.yandex-team.ru/arc/commit/8662285 ]

[terrmit](http://staff/terrmit) 2021-09-23 16:33:02+03:00

1.3.2
-----

* [tikhonov-ka](http://staff/tikhonov-ka)

 * PYPI-153: HTTP error 403, SSL is required

PYPI-153: HTTP error 403, SSL is required  [ https://a.yandex-team.ru/arc/commit/8482929 ]

* [shadchin](http://staff/shadchin)

 * IGNIETFERRO-1154 Rename contrib/python/requests_mock to contrib/python/requests-mock  [ https://a.yandex-team.ru/arc/commit/8345553 ]

[tikhonov-ka](http://staff/tikhonov-ka) 2021-08-04 16:24:02+03:00

1.3.1
-----

* [terrmit](http://staff/terrmit)

 * PYPI-143 not to fetch local packages ever  [ https://a.yandex-team.ru/arc/commit/7846360 ]

[denis-p](http://staff/denis-p) 2021-02-10 19:01:55+03:00

1.3.0
-----
 * PYPI-133: [Deploy] Перевезти PyPI в YD  [ https://a.yandex-team.ru/arc/commit/7469769 ]

[aksenovma](http://staff/aksenovma) 2020-10-15 19:09:37+03:00

1.2.4
-----
 * PYPI-133: Убрал ds из uwsgi  [ https://a.yandex-team.ru/arc/commit/7324248 ]

[aksenovma](http://staff/aksenovma) 2020-09-11 19:43:25+03:00

1.2.3
-----
 * PYPI-133: [Подготовка] Уходим от использования datasources  [ https://a.yandex-team.ru/arc/commit/7323823 ]

[aksenovma](http://staff/aksenovma) 2020-09-11 17:59:21+03:00

1.2.2
-----
 * Меньше uwsgi-воркеров  [ https://a.yandex-team.ru/arc/commit/7260688 ]

[aksenovma](http://staff/aksenovma) 2020-08-27 17:09:44+03:00

1.2.1
-----
 * Добавил pypi в ya.make, поправил название переменной конфига celery  [ https://a.yandex-team.ru/arc/commit/7242557 ]

[aksenovma](http://staff/aksenovma) 2020-08-21 17:23:58+03:00

1.2.0
-----

* [aksenovma](http://staff/aksenovma)

 * Добавлены версии и сборка из docker-package.json  [ https://a.yandex-team.ru/arc/commit/7127133 ]
 * Используется стандартный Dockerfile               [ https://a.yandex-team.ru/arc/commit/7127114 ]
 * PYPI-118: Поправил импорты                        [ https://a.yandex-team.ru/arc/commit/7124531 ]
 * PYPI-118: Поправил devexp.json                    [ https://a.yandex-team.ru/arc/commit/7124529 ]
 * PYPI-118: Убрал docker-compose.yml                [ https://a.yandex-team.ru/arc/commit/7124528 ]
 * PYPI-118: Доработки по ревью                      [ https://a.yandex-team.ru/arc/commit/7124527 ]
 * Merge branch 'master' into arcadia                [ https://a.yandex-team.ru/arc/commit/7124526 ]

* [nslus](http://staff/nslus)

 * ARCADIA-2297 [migration] github/tools/pypi  [ https://a.yandex-team.ru/arc/commit/7126720 ]

[aksenovma](http://staff/aksenovma) 2020-07-20 11:30:05+03:00

1.1.1
-----
 * Settings fix  [ https://github.yandex-team.ru/tools/pypi/commit/1bb3382 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-07-16 11:04:59+03:00

1.1.0
-----
 * Revert "PYPI-118: Аркадийные переменные окружения БД"  [ https://github.yandex-team.ru/tools/pypi/commit/3a0115f ]
 * Revert "PYPI-118: Аркадийные переменные окружения БД"  [ https://github.yandex-team.ru/tools/pypi/commit/0c33a68 ]
 * PYPI-118: Аркадийные переменные окружения БД           [ https://github.yandex-team.ru/tools/pypi/commit/1f5389e ]
 * PYPI-118: Перенёс тесты из localshop                   [ https://github.yandex-team.ru/tools/pypi/commit/414f2cf ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-07-15 13:44:08+03:00

1.0.6
-----
 * Rollback slaves separation                 [ https://github.yandex-team.ru/tools/pypi/commit/7198364 ]
 * Don't pop from empty state_stack           [ https://github.yandex-team.ru/tools/pypi/commit/8ce2465 ]
 * Add second slave and decrease db downtime  [ https://github.yandex-team.ru/tools/pypi/commit/8479055 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-07-14 11:12:45+03:00

1.0.5
-----
 * Increase timeout  [ https://github.yandex-team.ru/tools/pypi/commit/f39ec60 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-07-02 18:47:49+03:00

1.0.4
-----
 * Fix uploading files >100 MB and fix updating files with filename >200 symbols  [ https://github.yandex-team.ru/tools/pypi/commit/45e0e27 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-06-30 13:39:23+03:00

1.0.3
-----
 * Fix 5xx for safe methods + credentials  [ https://github.yandex-team.ru/tools/pypi/commit/2296f96 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-06-25 22:09:35+03:00

1.0.2
-----
 * Fix update_packages task failure  [ https://github.yandex-team.ru/tools/pypi/commit/16deed0 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-06-25 19:02:45+03:00

1.0.1
-----
 * Fix django_yauth settings  [ https://github.yandex-team.ru/tools/pypi/commit/c5292cf ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-06-25 11:23:33+03:00

1.0.0
------
 * PYPI-121: Last terrmit/localshop commit in deps  [ https://github.yandex-team.ru/tools/pypi/commit/201f718 ]
 * PYPI-121: Settings fixes                         [ https://github.yandex-team.ru/tools/pypi/commit/bd5900f ]
 * PYPI-121: Write celery task `started` state      [ https://github.yandex-team.ru/tools/pypi/commit/0a5542d ]
 * PYPI-121: Drop Py2/Py3.5 support                 [ https://github.yandex-team.ru/tools/pypi/commit/132a228 ]
 * PYPI-121: Ubuntu 20.04 with Py3.8                [ https://github.yandex-team.ru/tools/pypi/commit/ee5e1fc ]
 * PYPI-121: Some more refactoring                  [ https://github.yandex-team.ru/tools/pypi/commit/893f94d ]
 * PYPI-121: Finally granular settings              [ https://github.yandex-team.ru/tools/pypi/commit/fa038e5 ]
 * PYPI-121: Settings improvements                  [ https://github.yandex-team.ru/tools/pypi/commit/b9fb967 ]
 * PYPI-121: Iter-1                                 [ https://github.yandex-team.ru/tools/pypi/commit/b9782b9 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-06-24 16:45:23+03:00

0.14.7
------
 * PYPI-122: settings fix  [ https://github.yandex-team.ru/tools/pypi/commit/1e58616 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-06-15 20:33:18+03:00

0.14.6
------
 * PYPI-40: Add cleaner-task for deleting old packages           [ https://github.yandex-team.ru/tools/pypi/commit/77174f4 ]
 * PYPI-122: Settings refactoring                                [ https://github.yandex-team.ru/tools/pypi/commit/a5f1361 ]
 * PYPI-122: Drop redundant requirements and sort the remaining  [ https://github.yandex-team.ru/tools/pypi/commit/ac80ea8 ]
 * PYPI-122: Temporary requirements replacement                  [ https://github.yandex-team.ru/tools/pypi/commit/1414e40 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-06-15 19:43:01+03:00

0.14.5
------
 * PYPI-125: Убрал из логов user_agent  [ https://github.yandex-team.ru/tools/pypi/commit/6c0f994 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-06-04 15:37:55+03:00

0.14.4
------
 * TOOLS-2628: Улучшенные логи              [ https://github.yandex-team.ru/tools/pypi/commit/f3ddbf1 ]
 * TOOLS-2628: Многопоточность в uwsgi      [ https://github.yandex-team.ru/tools/pypi/commit/55efd67 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-06-02 21:30:57+03:00

0.14.3
------
 * Up ylock version  [ https://github.yandex-team.ru/tools/pypi/commit/7a016ae ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2020-03-25 12:36:31+03:00

0.14.2
------
 * PYPI-68 requires-python stable version  [ https://github.yandex-team.ru/tools/pypi/commit/1e43ea8 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2020-01-15 14:42:46+03:00

0.14.1
------
 * PYPI-68 localshop version  [ https://github.yandex-team.ru/tools/pypi/commit/0ea2ffc ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2020-01-15 13:16:31+03:00

0.14.0
------
 * PYPI-68 requires-python  [ https://github.yandex-team.ru/tools/pypi/commit/18ad205 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2020-01-15 12:39:18+03:00

0.13.1
------
 * PYPI-104 Чистка кода и зависимостей от mysql  [ https://github.yandex-team.ru/tools/pypi/commit/844a680 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2019-09-12 15:13:53+03:00

0.13.0
-------
 * PYPI-92 Переезд в PGaaS  [ https://github.yandex-team.ru/tools/pypi/commit/d157f9b ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2019-09-05 20:22:24+03:00

0.12.16
-------
 * Увеличил harakiri в uwsgi  [ https://github.yandex-team.ru/tools/pypi/commit/e427e73 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-09-04 18:13:16+03:00

0.12.15
-------
 * USE_ACCEL_REDIRECT в environ  [ https://github.yandex-team.ru/tools/pypi/commit/0089251 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2019-04-30 14:42:59+03:00

0.12.14
-------
 * Revert "Do not try to build from pypi.y-t.ru"  [ https://github.yandex-team.ru/tools/pypi/commit/d8b0262 ]
 * Do not try to build from pypi.y-t.ru           [ https://github.yandex-team.ru/tools/pypi/commit/3b4395e ]
 * up ylock version                               [ https://github.yandex-team.ru/tools/pypi/commit/9e04ab4 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2019-04-30 13:16:21+03:00

0.12.13
-------
 * Добавил ipython в зависимости                                     [ https://github.yandex-team.ru/tools/pypi/commit/395460b ]
 * PYPI-94 Не запускаем апдейт пакетов в изолированных репозиториях  [ https://github.yandex-team.ru/tools/pypi/commit/ca41391 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2019-03-12 18:16:50+03:00

0.12.12
-------
 * PYPI-87 Не создаем пакетов с одним normalized_name  [ https://github.yandex-team.ru/tools/pypi/commit/44b53b7 ]
 * clean up                                            [ https://github.yandex-team.ru/tools/pypi/commit/bc0303f ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2019-02-27 18:14:55+03:00

0.12.11
-------
 * Revert "Поменял формат uwsgi-логов"  [ https://github.yandex-team.ru/tools/pypi/commit/be9fcc6 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2019-02-07 17:21:32+03:00

0.12.10
-------
 * Поменял формат uwsgi-логов  [ https://github.yandex-team.ru/tools/pypi/commit/2c19c83 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2019-02-05 19:21:24+03:00

0.12.9
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * PYPI-85: Добавил зависимость на yt в ylock  [ https://github.yandex-team.ru/tools/pypi/commit/d864426 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2019-01-22 16:45:38+03:00

0.12.8
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * PYPI-85: Locke  [ https://github.yandex-team.ru/tools/pypi/commit/f6687f5 ]

 * [Mikhail Agranovskiy](http://staff/agrml@yandex-team.ru)

 * Rename .devexp.jsons to .devexp.json  [ https://github.yandex-team.ru/tools/pypi/commit/e5ae23a ]
 * Create .devexp.jsons                  [ https://github.yandex-team.ru/tools/pypi/commit/2c02aaa ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2019-01-22 16:33:45+03:00

0.12.7
------
 * STAFF-10275: Celery в MaaS

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2018-11-30 16:53:00+03:00

0.12.6
------
 * Обновил версию django-mds, где есть ретраи  [ https://github.yandex-team.ru/tools/pypi/commit/52d4d22 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2018-05-21 15:42:13+03:00

0.12.5
------
 * UWSGI buffer-size is set to default https://st.yandex-team.ru/PYPI-74

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2017-10-30 14:27:34+03:00

0.12.4
------
 * UWSGI buffer-size increased https://st.yandex-team.ru/PYPI-74

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2017-10-27 14:12:57+03:00

0.12.3
------
 * Removed homepage from package-detail template  [ https://github.yandex-team.ru/tools/pypi/commit/5e7f5f7 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2017-10-05 13:32:26+03:00

0.12.2
------
 * Поднял таймаут в MDS до 15 секунд          [ https://github.yandex-team.ru/tools/pypi/commit/c203cda ]
 * Поправил ip dns-резолвера в nginx-конфиге  [ https://github.yandex-team.ru/tools/pypi/commit/3b40ff6 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2017-08-17 21:56:52+03:00

0.12.1
------
 * small fix  [ https://github.yandex-team.ru/tools/pypi/commit/5b94c7b ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2017-08-17 19:04:16+03:00

0.12.0
------

* [Dmitry Terrov](http://staff/terrmit@yandex-team.ru)

 * Сконвертировал changelog.md                        [ https://github.yandex-team.ru/tools/pypi/commit/2ea2b28 ]
 * Добавил .release.hjson                             [ https://github.yandex-team.ru/tools/pypi/commit/bc3fe0e ]
 * Выпилил debian и etc директории                    [ https://github.yandex-team.ru/tools/pypi/commit/e9ebe90 ]
 * Настроил логгирование                              [ https://github.yandex-team.ru/tools/pypi/commit/3296267 ]
 * Поднял версию pytz                                 [ https://github.yandex-team.ru/tools/pypi/commit/737bba5 ]

* [root](http://staff/zivot@yandex-team.ru)

 * ipv6 resolver added                     [ https://github.yandex-team.ru/tools/pypi/commit/df806a9 ]
 * uwsgi workers is set to 8               [ https://github.yandex-team.ru/tools/pypi/commit/be1cc58 ]
 * Добавил Dockerfile для запуска в qloud  [ https://github.yandex-team.ru/tools/pypi/commit/fbb92c6 ]

[Dmitry Terrov](http://staff/terrmit@yandex-team.ru) 2017-08-17 18:53:38+03:00

0.11.7
---

  * localshop version up

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-07-11 13:17:23

0.11.6
---

  * PYPI-59 localshop version up (fix)

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-06-09 14:57:55

0.11.5
---

  * Revert "Сделал PyPI полностью изолированным"
  * PYPI-59 localshop version up (PEP-503)

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-06-09 14:18:22

0.11.4
---

  * Сделал PyPI полностью изолированным

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-04-19 14:26:09

0.11.3
---

  * chunk\_size и pool\_size сделал опциональными

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-04-12 21:45:28

0.11.2
---

  * Распараллелил миграцию переливки из Elliptics в MDS

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-04-12 21:08:26

0.11.1
---

  * Фикс тупой баги в принте

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-04-12 18:40:30

0.11.0
---

  * Elliptics to MDS

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-04-12 18:17:26

0.10.10
---

  * Вернул версию localshop без правок про md5

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-04-05 18:44:22

0.10.9
---

  * localshop version up

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-03-03 16:39:53

0.10.8
---

  * localshop version up

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-03-03 15:39:38

0.10.7
---

  * localshop version up

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-03-03 11:49:40

0.10.6
---

  * localshop version up

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-03-03 03:32:54

0.10.5
---

  * localshop version up

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-03-03 03:09:30

0.10.4
---

  * Переопределил index\_view с редиректом на страницу репозитория
  * Добавляем нового пользователя в дефолтную команду
  * Обновил версию localshop

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-03-02 13:19:17

0.10.3
---

  * localshop version up

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-02-26 19:21:11

0.10.2
---

  * Починил статику админки

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-02-26 15:03:08

0.10.1
---

  * Добавил в зависимости libfreetype6-dev для Pillow

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-02-26 13:54:43

0.10.0
---

  * Новый localshop
  * Запрещаем заливать пакет с той же версией

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-02-26 12:26:48

0.9.2
---

  * Поменял версию django-guardian на ту, которая была в продакшене
  * Лог celery пишется в projectname pypi

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-02-19 15:12:15

0.9.1
---

  * Добавил wsgi.py

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-02-17 14:10:54

0.9.0
---

  * Настроил robe
  * Заменил localshop скрипт запуска на pypi
  * PYPI-48 - Конфиг uwsgi
  * PYPI-44 - Переезд на MongoDB 3
  * Обновил debian-сборку

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2016-02-17 13:15:16

0.8-16
---

  * .gitignore
  * Добавил DEBUG-режим в девелопмент
  * Поменял версию localshop

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2015-11-09 20:42:18

0.8-15
---

  * Новая версия localshop
  * Теперь берем код localshop из ветки stable
  * PYPI-33 - В продакшене два слейва
  * PYPI-33 - Добавил порты в настройки MySQL
  * PYPI-31 - Свежая версия pytz
  * Указываю коммит вместо имени ветки в requirements.txt для localshop

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2015-07-09 16:34:08

0.8-14
---

  * Новая версия localshop

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2015-07-09 15:52:24

0.8-13
---

  * Обновил localshop

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-09-08 19:11:23

0.8-12
---

  * Поправил celeryd-конфиг

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-08-27 11:06:57

0.8-11
---

  * PYPI-19 - Ротирование логов gunicorn

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-08-25 14:11:20

0.8-10
---

  * Добавил ReadOnlyMiddleware

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-31 15:13:42

0.8-9
---

  * Добавил тайминги для MySQL

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-31 14:00:30

0.8-8
---

  * Обновил версию localshop
  * Подключил python-django-alive

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-28 17:17:44

0.8-7
---

  * Поправил requirements.txt

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-24 15:53:16

0.8-6
---

  * Поправил requirements.txt
  * fab build

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-24 14:55:23

0.8-5
---

  * Опечатка

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-23 19:19:08

0.8-4
---

  * Настроил логи для gunicorn

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-23 19:04:53

0.8-3
---

  * Исправил линки

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-23 18:08:35

0.8-2
---

  * Правки дебианизации

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-23 17:52:28

0.8-1
---

  * Переезд к новым админам
  * postistn и postrm скрипты для yandex-tools-pypi-www

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-23 13:08:55

0.8
---

  * Переезд к новым админам

 [Dmitry Terrov](https://staff.yandex-team.ru/terrmit@yandex-team.ru) 2014-07-22 15:35:45

0.7-3
---

  * Фикс requirements
  * pymongo 2.6.2

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-23 18:16:24

0.7-2
---

  * Джанга 1.5.4

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-23 17:44:09

0.7-1
---

  * Убивем *.egg-info в clean
  * Используем . вместо source

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-23 17:12:16

0.7
---

  * Ставим localshop из форка
  * Апдейт сборки окружения
  * Фикс работы с syslog

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-19 01:50:54

0.6
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Поменял ssh на git ro протокол
  * Фикс конфига nginx
  * Использование pip-accel
  * Ставим localshop прям с github

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-18 22:39:38

0.5ubuntu1
---

    [ Andrey Larionov ]
    * Enlarge max content body size in nginx config

 [Andrey Larionov](https://staff.yandex-team.ru/mou@yandex-team.ru) 2013-02-19 19:11:01

0.5
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Дополнил бекэнд методами

 [alexkoshelev](https://staff.yandex-team.ru/alexkoshelev@pypi.dev.yandex.net) 2013-02-15 16:47:29

0.4
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Московская таймзона
  * Временные логи в файл

 [alexkoshelev](https://staff.yandex-team.ru/alexkoshelev@pypi.dev.yandex.net) 2013-02-15 16:33:20

0.3
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Использование самого pypi.y-t.ru для сборки
  * Установка дополнительных зависимостей с форсированным update

 * [alexkoshelev](https://staff.yandex-team.ru/alexkoshelev)


 [alexkoshelev](https://staff.yandex-team.ru/alexkoshelev@pypi.dev.yandex.net) 2013-02-15 07:48:54

0.2
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Репозиторий yandex-lucid
  * Репозиторий yandex-precise
  * yenv в зависимостях сборки
  * Зависимость от devscripts
  * Фикс раскладки uwsgi конфига
  * Фикс хоста в конфиге nginx
  * Использование gunicorn
  * Совсем выпилил uwsgi
  * Убил лишние auth бакэнды
  * Фикс замены auth мидлвари
  * auth backend, который разрешает всё

 * [alexkoshelev](https://staff.yandex-team.ru/alexkoshelev)


 [alexkoshelev](https://staff.yandex-team.ru/alexkoshelev@pypi.dev.yandex.net) 2013-02-14 16:52:07

0.1.2
---

  * Убил зависимость от кастомного nginx конфига
  * pypi-user для mysql в продакшене

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-04 11:56:06

0.1.1
---

  * Не используем nginx магию Влада
  * production настройки
  * dh\_environment пока не нужен

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-04 11:45:55

0.1
---

  * Первый релиз

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-04 03:01:39

