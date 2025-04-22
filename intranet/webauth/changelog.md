2.5.12
------
 * VIEWER-945 Докинул логов                         [ https://a.yandex-team.ru/arc/commit/9736288 ]
 * VIEWER-945 Фикс преобразования fields_data       [ https://a.yandex-team.ru/arc/commit/9722258 ]
 * VIEWER-945 Получаем роли в Webauth через S3-MDS  [ https://a.yandex-team.ru/arc/commit/9720473 ]

[smosker](http://staff/smosker) 2022-07-18 19:00:14+03:00

2.5.11
------

* [kir-choo](http://staff/kir-choo)

 * PR for branch fix/VIEWER-936-fields-data-serialization                                                                                                        [ https://a.yandex-team.ru/arc/commit/9637432 ]

2.5.10
------

 * VIEWER-924: Log features
\- Log response body from blackbox
 - Use log_context to provide request metadata in logs
 - Add debug option to log secrets in log  [ https://a.yandex-team.ru/arc/commit/8790745 ]

* [smosker](http://staff/smosker)

 * DEVEXPMIGRATION-169 Переезд на аркадийную ревьюшницу  [ https://a.yandex-team.ru/arc/commit/9461171 ]

* [shadchin](http://staff/shadchin)

 * DEVTOOLS-1066 Move ipaddress in contrib/deprecated/python

Пакет `ipaddress` - это бэкпорт из стандартной библиотеки Python 3, сейчас пакет не получает обновления из вежих версий Python 3, автор похоже забросил пакет и имеет незакрытые CVE  [ https://a.yandex-team.ru/arc/commit/9456025 ]

* [dsamuylov](http://staff/dsamuylov)

 * ARCANUM-5510 prepare migration from .devexp.json to a.yaml (intranet)  [ https://a.yandex-team.ru/arc/commit/9231012 ]

* [maratik](http://staff/maratik)

 * feat: startrek integration for VIEWER ARCANUM-5357

feat: startrek integration  [ https://a.yandex-team.ru/arc/commit/9141016 ]
 * Revert commit r9099919                                                          [ https://a.yandex-team.ru/arc/commit/9100081 ]
 * feat: startrek integration for VIEWER ARCANUM-5357

feat: startrek integration  [ https://a.yandex-team.ru/arc/commit/9099919 ]

[kir-choo](http://staff/kir-choo) 2022-06-27 17:08:54+05:00

2.5.9
-----
 * Правка работы unistat ручки на не cron компонентах  [ https://a.yandex-team.ru/arc/commit/8771985 ]

[smosker](http://staff/smosker) 2021-10-26 19:26:26+03:00

2.5.8
-----
 * VIEWER-921: Add CA certs config for httpclient  [ https://a.yandex-team.ru/arc/commit/8766031 ]
 * Add a.yaml file                                 [ https://a.yandex-team.ru/arc/commit/8756468 ]

[kir-choo](http://staff/kir-choo) 2021-10-25 17:34:05+03:00

2.5.7
-----
 * VIEWER-920: Write logs to stderr  [ https://a.yandex-team.ru/arc/commit/8749111 ]

[kir-choo](http://staff/kir-choo) 2021-10-19 19:37:38+03:00

2.5.6
-----

* [kir-choo](http://staff/kir-choo)

 * VIEWER-919: Export metrics through /unistat  [ https://a.yandex-team.ru/arc/commit/8707892 ]

* [rocco66](http://staff/rocco66)

 * feat: change some owners tools-access -> tools-python  [ https://a.yandex-team.ru/arc/commit/8584305 ]

[kir-choo](http://staff/kir-choo) 2021-10-06 20:32:23+05:00

2.5.5
-----
 * BALANCERSUPPORT-3176 фикс заголовка  [ https://a.yandex-team.ru/arc/commit/8582188 ]
 * Фикс тестов                          [ https://a.yandex-team.ru/arc/commit/8580265 ]

[smosker](http://staff/smosker) 2021-09-01 18:15:16+03:00

2.5.4
-----

* [smosker](http://staff/smosker)

 * VIEWER-916 Правка обновления кеша  [ https://a.yandex-team.ru/arc/commit/8578684 ]

* [rocco66](http://staff/rocco66)

 * feat: change some owners tools-access -> tools-python  [ https://a.yandex-team.ru/arc/commit/8564665 ]
 * Change "ya.make"                                       [ https://a.yandex-team.ru/arc/commit/8402868 ]

* [ezaitov](http://staff/ezaitov)

 * Берем адрес пользователя из заголовка AWACS X-Forwarded-For-Y  [ https://a.yandex-team.ru/arc/commit/8497563 ]

* [shadchin](http://staff/shadchin)

 * IGNIETFERRO-1870 Auto enable pytest-tornado plugin

Раньше автоматическое подключение плагинов pytest не работало, сейчас работает, достаточно плагин добавить в PEERDIR, поэтому удалил ненужное определение `pytest_plugins`, чтобы было попроще  [ https://a.yandex-team.ru/arc/commit/8434386 ]

* [exprmntr](http://staff/exprmntr)

 * DEVTOOLS-7781 - remove NO_LINT()

DEVTOOLS-7781  [ https://a.yandex-team.ru/arc/commit/8097952 ]

* [v-korovin](http://staff/v-korovin)

 * DEVTOOLS-8344 Migration for intranet

Migration  [ https://a.yandex-team.ru/arc/commit/8095225 ]

[smosker](http://staff/smosker) 2021-08-31 23:00:02+03:00

2.5.3
-----
 * VIEWER-902: Фикс доменной зоны куки  [ https://a.yandex-team.ru/arc/commit/8030167 ]

[qazaq](http://staff/qazaq) 2021-03-29 17:02:33+03:00

2.5.2
-----
 * VIEWER-892: Правильно получаем IP пользователя  [ https://a.yandex-team.ru/arc/commit/7674365 ]
 * Добавил компонент в конфиг releaser             [ https://a.yandex-team.ru/arc/commit/7615149 ]

[qazaq](http://staff/qazaq) 2020-12-16 11:42:25+03:00

2.5.1
---
 * VIEWER-893: Поддержка SameSite  [ https://a.yandex-team.ru/arc/commit/7614539 ]

[qazaq](http://staff/qazaq) 2020-11-24 00:30:16+03:00

2.5
---

* [qazaq](http://staff/qazaq)

 * VIEWER-893: Проставляем SameSite=None для куки с токеном  [ https://a.yandex-team.ru/arc/commit/7612002 ]

* [ezaitov](http://staff/ezaitov)

 * Яндекс.Деньги больше не Яндекс (IS-3372)  [ https://a.yandex-team.ru/arc/commit/7591513 ]

[qazaq](http://staff/qazaq) 2020-11-23 17:50:59+03:00

2.4
---
 * IDM-9961: Добавление новых систем в webauth без перевыкатки

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![chirkinvf](https://codereview.common-int.yandex-team.ru/badges/chirkinvf-...-yellow.svg)](https://staff.yandex-team.ru/chirkinvf) [![d1568](https://codereview.common-int.yandex-team.ru/badges/d1568-...-yellow.svg)](https://staff.yandex-team.ru/d1568) [![ndtretyak](https://codereview.common-int.yandex-team.ru/badges/ndtretyak-ok-green.svg)](https://staff.yandex-team.ru/ndtretyak)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/7153302 ]

[alexsaplin](http://staff/alexsaplin) 2020-07-28 19:14:11+03:00

2.3
---

* [ndtretyak](http://staff/ndtretyak)

 * Новая версия yql

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![chirkinvf](https://codereview.common-int.yandex-team.ru/badges/chirkinvf-...-yellow.svg)](https://staff.yandex-team.ru/chirkinvf) [![terrmit](https://codereview.common-int.yandex-team.ru/badges/terrmit-...-yellow.svg)](https://staff.yandex-team.ru/terrmit)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6854393 ]

* [alexsaplin](http://staff/alexsaplin)

 * Change balancer_request_time.yql

Note: mandatory check (NEED_CHECK) was skipped  [ https://a.yandex-team.ru/arc/commit/6845021 ]

* [shadchin](http://staff/shadchin)

 * Update pytest-mock from 1.11.0 to 2.0.0 for PY2 and 3.0.0 for PY3

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![feakuru](https://codereview.common-int.yandex-team.ru/badges/feakuru-ok-green.svg)](https://staff.yandex-team.ru/feakuru) [![chirkinvf](https://codereview.common-int.yandex-team.ru/badges/chirkinvf-...-yellow.svg)](https://staff.yandex-team.ru/chirkinvf)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6683965 ]

[ndtretyak](http://staff/ndtretyak) 2020-06-04 12:31:33+03:00

2.2
---

* [v-sopov](http://staff/v-sopov)

 * Ручка ping в Webauth  [ https://a.yandex-team.ru/arc/commit/6513129 ]

* [monory](http://staff/monory)

 * [CONTRIB-1727] Move Tornado to django-way differentiation of lib versions

[CONTRIB-1727] Add Tornado 6.0.3 for Py3  [ https://a.yandex-team.ru/arc/commit/6455462 ]

[v-sopov](http://staff/v-sopov) 2020-03-20 14:33:00+03:00

2.1
---
 * env pool size                             [ https://a.yandex-team.ru/arc/commit/6241981 ]
 * PR from branch users/ndtretyak/releaserr  [ https://a.yandex-team.ru/arc/commit/6240568 ]

[ndtretyak](http://staff/ndtretyak) 2020-01-23 10:40:41+03:00

2.0
------

* [ndtretyak](http://staff/ndtretyak)

 * Добавил параметр for_webauth при походе в idm  [ https://a.yandex-team.ru/arc/commit/6240464 ]


1.6.49
------
 * VIEWER-811: поправлен путь к supervisord  [ https://github.yandex-team.ru/idm/webauth/commit/38066d2 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-08-23 19:32:02+03:00

1.6.48
------
 * VIEWER-811: supervisor теперь ставится через apt, выпилен envtpl (#81)  [ https://github.yandex-team.ru/idm/webauth/commit/d9d32c3 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-08-23 18:56:11+03:00

1.6.47
------
 * Управление garbage collection (#80)  [ https://github.yandex-team.ru/idm/webauth/commit/f0557e5 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-08-09 16:18:08+03:00

1.6.46
------
 * Отключаем garbage collection в качестве эксперимента  [ https://github.yandex-team.ru/idm/webauth/commit/a2c1a75 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-08-05 18:47:19+03:00

1.6.45
------
 * Логирование общего времени запроса  [ https://github.yandex-team.ru/idm/webauth/commit/52b42bc ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-08-04 19:46:23+03:00

1.6.44
------
 * Логирование времени похода в redis (#79)  [ https://github.yandex-team.ru/idm/webauth/commit/21476b0 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-08-02 17:41:46+03:00

1.6.43
------
 * Уменьшен таймаут до blackbox, добавлен ретрай (#78)  [ https://github.yandex-team.ru/idm/webauth/commit/5d3a370 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-31 13:28:39+03:00

1.6.42
------
 * Теперь для хождения по http используется curl, логируется время запроса без нахождения в очереди (#77)  [ https://github.yandex-team.ru/idm/webauth/commit/4392024 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-30 13:00:43+03:00

1.6.41
------
 * Выпил логов ещё и в /auth_request  [ https://github.yandex-team.ru/idm/webauth/commit/e8293dc ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-26 19:55:17+03:00

1.6.40
------
 * Временно выключено логирование запросов, включено логирование времени ответа blackbox (#76)  [ https://github.yandex-team.ru/idm/webauth/commit/85f4fac ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-26 19:00:41+03:00

1.6.39
------
 * Revert "Временное отключение логирования запросов"  [ https://github.yandex-team.ru/idm/webauth/commit/badbfe9 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-24 12:28:33+03:00

1.6.38
------
 * Временное отключение логирования запросов  [ https://github.yandex-team.ru/idm/webauth/commit/14eea6f ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-19 13:25:17+03:00

1.6.37
------
 * VIEWER-820: уменьшаем нагрузку от обновления кеша, улучшаем логирование (#75)  [ https://github.yandex-team.ru/idm/webauth/commit/a0d9174 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-17 15:39:57+03:00

1.6.36
------
 * VIEWER-820: теперь пути узлов всегда обёрнуты в скобки (#74)  [ https://github.yandex-team.ru/idm/webauth/commit/b5f0b4c ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-16 16:57:51+03:00

1.6.35
------
 * VIEWER-820: правки по синку с redis  [ https://github.yandex-team.ru/idm/webauth/commit/c167e99 ]
 * \-check_role                         [ https://github.yandex-team.ru/idm/webauth/commit/1c12ecc ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-15 18:32:05+03:00

1.6.34
------
 * VIEWER-820: WebAuth: Писать кэш ролей в redis (#73)  [ https://github.yandex-team.ru/idm/webauth/commit/7070feb ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-15 13:07:11+03:00

1.6.33
------
 * VIEWER-816 Привести имя аккаунта в locke к lowercase (#72)  [ https://github.yandex-team.ru/idm/webauth/commit/fcd7e1e ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-06-24 19:22:35+03:00

1.6.32
------
 * VIEWER-815 Убрал qloud-test из синка (#71)  [ https://github.yandex-team.ru/idm/webauth/commit/5de004f ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-06-21 22:28:53+03:00

1.6.31
------
 * VIEWER-802: убрать флаг  [ https://github.yandex-team.ru/idm/webauth/commit/2bf10b8 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-13 20:53:45+03:00

1.6.30
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * VIEWER-802: шифровать токен в куках (#64)  [ https://github.yandex-team.ru/idm/webauth/commit/e50ccb0 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-13 14:03:43+03:00

1.6.29
------
* Поправил номер версии

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-06-11 16:43:51+03:00

0.6.28
------
 * VIEWER-800 Поправил dockerfile, добавил логов, учел часовой пояс  [ https://github.yandex-team.ru/idm/webauth/commit/dc504b3 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-06-11 12:33:56+03:00

1.6.27
------
 * VIEWER-800 Токен для YQL  [ https://github.yandex-team.ru/idm/webauth/commit/b28ec16 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-06-10 20:30:48+03:00

1.6.26
------
 * VIEWER-800 Отредактировал конфиг релизера  [ https://github.yandex-team.ru/idm/webauth/commit/1c3c50d ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-06-10 19:30:17+03:00

1.6.25
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * VIEWER-800 Мониторинг по логам балансера (#66)  [ https://github.yandex-team.ru/idm/webauth/commit/90b586d ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-06-10 18:42:57+03:00

1.6.24
------
 * VIEWER-808: подгрузка данных теперь выполняется в отдельном треде (#65)  [ https://github.yandex-team.ru/idm/webauth/commit/aa30179 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-06-06 12:32:54+03:00

1.6.23
------
 * crontab-команды завёрнуты в bash  [ https://github.yandex-team.ru/idm/webauth/commit/eb5d40e ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-05-31 16:10:35+03:00

1.6.22
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Новые компоненты, проверка на необходимость запуска синка с qloud в компоненте  [ https://github.yandex-team.ru/idm/webauth/commit/b5f8130 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-05-31 14:26:24+03:00

1.6.21
------
* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * VIEWER-792 add yandex-team.tld  [ https://github.yandex-team.ru/idm/webauth/commit/dae90e8 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * VIEWER-799: добавлена настройка про запуск синка с IDM (#62)  [ https://github.yandex-team.ru/idm/webauth/commit/95d0925 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-05-31 14:17:54+03:00

0.6.19
------
 * VIEWER-792 Правки после ревью                                       [ https://github.yandex-team.ru/idm/webauth/commit/8085662 ]
 * VIEWER-792 Правки после ревью                                       [ https://github.yandex-team.ru/idm/webauth/commit/59bea05 ]
 * VIEWER-792 В некоторых случаях ставить куку на зону, а не на домен  [ https://github.yandex-team.ru/idm/webauth/commit/f2699db ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-05-30 14:50:28+03:00

1.6.18
------
 * VIEWER-744: поправлен базовый класс мониторинга  [ https://github.yandex-team.ru/idm/webauth/commit/c9c6e9f ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-04-10 12:43:03+03:00

1.6.17
------
 * VIEWER-744: Добавить защиту от удаления всех узлов (#60)  [ https://github.yandex-team.ru/idm/webauth/commit/038015a ]
 * ndtretyak добавлен в основные ревьюверы (#59)             [ https://github.yandex-team.ru/idm/webauth/commit/50aeef0 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-04-10 12:31:37+03:00

1.6.16
------
 * Выводим текст ошибки от oauth.yandex-team.ru  [ https://github.yandex-team.ru/idm/webauth/commit/90d55ad ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-29 13:35:05+03:00

1.6.15
------
 * Добавлено логирование ошибок от OAuth в OAuthCallbackHandler (#58)  [ https://github.yandex-team.ru/idm/webauth/commit/1c5f186 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-28 16:19:01+03:00

1.6.14
------
 * COMPUTERPROBLEM-146 cron files chmod (#57)  [ https://github.yandex-team.ru/idm/webauth/commit/02486a8 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-03-14 21:33:36+03:00

1.6.13
------

* [vladimir](http://staff/chirkinvf@yandex-team.ru)

 * VIEWER-749 Обновил версию ylock  [ https://github.yandex-team.ru/idm/webauth/commit/14d1214 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-03-13 11:34:43+03:00

1.6.12
------
 * VIEWER-749: Съехать Webauth-ом с zookeper  [ https://github.yandex-team.ru/idm/webauth/commit/0001f5f ]

[vladimir](http://staff/chirkinvf@yandex-team.ru) 2019-03-12 10:29:50+03:00

1.6.11
------
 * VIEWER-767 Отдаем данные о времени генерации кеша в минутах (#53)  [ https://github.yandex-team.ru/idm/webauth/commit/38046c5 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-18 14:51:08+03:00

1.6.10
------
 * VIEWER-767 Изменение агрегации (#52)  [ https://github.yandex-team.ru/idm/webauth/commit/4bd526a ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-15 19:23:13+03:00

1.6.9
-----
 * VIEWER-767 Добавил новые типы агрегации (#51)  [ https://github.yandex-team.ru/idm/webauth/commit/31d2e53 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-15 18:39:33+03:00

1.6.8
-----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * trendbox container_resource changed  [ https://github.yandex-team.ru/idm/webauth/commit/6b5b563 ]
 * Добавил ревьюеров, tmux              [ https://github.yandex-team.ru/idm/webauth/commit/7bfc30a ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * VIEWER-767 Ручка unistat для голована (#50)                                        [ https://github.yandex-team.ru/idm/webauth/commit/0401739 ]
 * VIEWER-766 Сохранять время начала и окончания двух последних генераций кеша (#49)  [ https://github.yandex-team.ru/idm/webauth/commit/53c6caa ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-15 17:00:24+03:00

1.6.7
-----
 * VIEWER-735 Использовать параметр no_meta при походах за кешом (#42)  [ https://github.yandex-team.ru/idm/webauth/commit/1233a0b ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-12-29 18:09:50+03:00

1.6.6
-----
 * VIEWER-714-2 Поправил пути  [ https://github.yandex-team.ru/idm/webauth/commit/0e8d0b3 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-12-17 10:33:53+03:00

1.6.5
-----
 * VIEWER-726 Проблема с запуском cron (#39)  [ https://github.yandex-team.ru/idm/webauth/commit/38afcd5 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-12-14 16:48:26+03:00

1.6.4
-----

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * VIEWER-714 Добавить мониторинг полноты и свежести кеша (#37)  [ https://github.yandex-team.ru/idm/webauth/commit/e0fe6a3 ]
 * Поправлен конфиг ревьюшницы                                   [ https://github.yandex-team.ru/idm/webauth/commit/cddfe34 ]
 * VIEWER-726 Проблема с запуском cron (#36)                     [ https://github.yandex-team.ru/idm/webauth/commit/e7a8352 ]

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * VIEWER-720: Конфиг ревьюшницы - сквозное ревью  [ https://github.yandex-team.ru/idm/webauth/commit/df6bd68 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-12-14 16:15:44+03:00

1.6.3
-----
 * Апнули версию ubuntu                             [ https://github.yandex-team.ru/idm/webauth/commit/24cb368 ]
 * Теперь новенький redis собирается из исходников  [ https://github.yandex-team.ru/idm/webauth/commit/646b97f ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-27 14:28:34+03:00

1.6.2
-----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * VIEWER-707: Увеличен пул bb, уменьшен пул redis  [ https://github.yandex-team.ru/idm/webauth/commit/140b6de ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-26 16:59:15+03:00

1.6.1
-----
 * VIEWER-713: все параметры пула вынесены в настройки          [ https://github.yandex-team.ru/idm/webauth/commit/3a4ae5a ]
 * VIEWER-713: теперь redis-пул создаётся при первом обращении  [ https://github.yandex-team.ru/idm/webauth/commit/170ac3d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-23 18:55:42+03:00

1.6.0
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * VIEWER-687: добавить сети в байпас  [ https://github.yandex-team.ru/idm/webauth/commit/a542a74 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * VIEWER-713: memcached заменён на redis, в очередной раз переделаны тесты                                                                    [ https://github.yandex-team.ru/idm/webauth/commit/e37bca2 ]
 * VIEWER-713: поправлен адрес memcached, изменена генерация ключа для кеша                                                                    [ https://github.yandex-team.ru/idm/webauth/commit/0a87914 ]
 * VIEWER-713: теперь из кеша тоже достаётся tuple, а не список; добавлены тесты для наполненного кеша                                         [ https://github.yandex-team.ru/idm/webauth/commit/d8bbb9b ]
 * VIEWER-713: в тестах теперь проверяется запись в кеш и прокидывается проверяемый хост                                                       [ https://github.yandex-team.ru/idm/webauth/commit/539509e ]
 * VIEWER-713: добавлено разграничение кешей для внешнего и внутреннего ЧЯ                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/6974a85 ]
 * VIEWER-713: добавлены тесты на случай, когда кеш не заполнен, поправлен хешер, учтён случай отсутствия второй куки, поправлены мелкие баги  [ https://github.yandex-team.ru/idm/webauth/commit/0dc78d7 ]
 * VIEWER-713: memcached теперь принимает только локальные соединения                                                                          [ https://github.yandex-team.ru/idm/webauth/commit/adbb410 ]
 * VIEWER-713: данные при работе с кешом теперь нормально (де)сериализуются                                                                    [ https://github.yandex-team.ru/idm/webauth/commit/aa2e01d ]
 * VIEWER-713: добавлено хождение в кеш                                                                                                        [ https://github.yandex-team.ru/idm/webauth/commit/95771e9 ]
 * VIRERT-713: добавлен запуск memcached                                                                                                       [ https://github.yandex-team.ru/idm/webauth/commit/42dcdcc ]
 * Поправлены Dockerfile и docker-compose.yaml, добавлен конфиг для trendbox                                                                   [ https://github.yandex-team.ru/idm/webauth/commit/2f8c580 ]
 * Конфиг Ревьюшницы                                                                                                                           [ https://github.yandex-team.ru/idm/webauth/commit/bd24cfb ]
 * VIEWER-712: убрать из error-log'a данные пользователей                                                                                      [ https://github.yandex-team.ru/idm/webauth/commit/a6bce7c ]
 * VIEWER-709: вернул старый таймаут                                                                                                           [ https://github.yandex-team.ru/idm/webauth/commit/7fcda05 ]
 * VIEWER-709: чуть увеличен таймаут до ЧЯ, увеличено количество обрабатываемых запросов к ЧЯ                                                  [ https://github.yandex-team.ru/idm/webauth/commit/ba324f6 ]
 * Увеличить таймаут до ЧЯ                                                                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/d1d68f4 ]
 * Поправлено логирование                                                                                                                      [ https://github.yandex-team.ru/idm/webauth/commit/a6c9888 ]
 * VIEWER-688: выпилено логирование в файл (#26)                                                                                               [ https://github.yandex-team.ru/idm/webauth/commit/781ea22 ]
 * VIEWER-682: Добавить новые домены для байпаса в Webauth (#24)                                                                               [ https://github.yandex-team.ru/idm/webauth/commit/9040e92 ]
 * VIEWER-661: возврат X-Forwarded-For, но с более корректной его обработкой (#23)                                                             [ https://github.yandex-team.ru/idm/webauth/commit/fd1ebec ]
 * VIEWER-661: Возможность байпаса webauth для заданных сетей/макросов (#22)                                                                   [ https://github.yandex-team.ru/idm/webauth/commit/1d520fc ]
 * DeniedReasons переименован в Webauth-Denial-Reasons и отсылается ещё и в extcookie-схеме (#21)                                              [ https://github.yandex-team.ru/idm/webauth/commit/3e7ec13 ]
 * VIEWER-665: /auth_request для кулаудной схемы логируется некорректно (#20)                                                                  [ https://github.yandex-team.ru/idm/webauth/commit/f379a7f ]
 * VIEWER-663: добавлена проверка fields_data                                                                                                  [ https://github.yandex-team.ru/idm/webauth/commit/c5ca014 ]
 * VIEWER-663: добавлено логирование ручки                                                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/16b2447 ]
 * VIEWER-663: Добавлена ручка для проверки наличия роли на пользователя                                                                       [ https://github.yandex-team.ru/idm/webauth/commit/5f8cf0e ]
 * VIEWER-655: подключённые системы теперь подцепляются из переменных окружения                                                                [ https://github.yandex-team.ru/idm/webauth/commit/270ce10 ]
 * VIEWER-650: добавлена проверка скоупов для внешней схемы аутентификации                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/e106dc1 ]
 * VIEWER-648: теперь токен в сложной схеме можно пробрасывать в заголовке Webauth-Authorization (формат каноничный)                           [ https://github.yandex-team.ru/idm/webauth/commit/2396e86 ]
 * VIEWER-645: поддержан новый формат кулаудных ssl-заголовков                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/dd9d897 ]
 * SECAUDIT-2223: правки по эскейпингу токена, небольшая правка с юникодом в модуле шифрования                                                 [ https://github.yandex-team.ru/idm/webauth/commit/783f56b ]
 * SECAUDIT-2223: теперь токен, получаемый через OAuth callback, пробрасывается в зашифрованном виде                                           [ https://github.yandex-team.ru/idm/webauth/commit/7ce5de1 ]
 * Убран проброс старого заголовка с логином                                                                                                   [ https://github.yandex-team.ru/idm/webauth/commit/318a978 ]
 * Добавлен проброс старого заголовка с логином                                                                                                [ https://github.yandex-team.ru/idm/webauth/commit/f9a53d5 ]
 * Подключение urllib3-адаптера теперь выполняется индивидуально для каждого запроса                                                           [ https://github.yandex-team.ru/idm/webauth/commit/5322d12 ]
 * VIEWER-616: блокировка теперь делается через with-statement, скрипт запускается раз в десять минут, а не в пять                             [ https://github.yandex-team.ru/idm/webauth/commit/d764fe7 ]
 * VIEWER-616: retry-policy взята из urllib3, добавлены англоязычные названия узлов                                                            [ https://github.yandex-team.ru/idm/webauth/commit/774e180 ]
 * VIEWER-616: при хождении в IDM и Qloud теперь используется exponential backoff                                                              [ https://github.yandex-team.ru/idm/webauth/commit/6a5b78e ]
 * VIEWER-616: уменьшен размер страницы при хождении в IDM                                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/c8c3614 ]
 * VIEWER-616: добавлены префиксы логам команд                                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/1225e96 ]
 * VIEWER-616: размер страницы IDM вынесен в настройки                                                                                         [ https://github.yandex-team.ru/idm/webauth/commit/bd67d9c ]
 * VIEWER-616: поправлены пути до узлов                                                                                                        [ https://github.yandex-team.ru/idm/webauth/commit/46e59b0 ]
 * VIEWER-616: доработки по логированию                                                                                                        [ https://github.yandex-team.ru/idm/webauth/commit/d66fede ]
 * VIEWER-616: изменена структура дерева ролей                                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/63c06fe ]
 * VIEWER-616: теперь синхронизация не выдаёт роли                                                                                             [ https://github.yandex-team.ru/idm/webauth/commit/6eab7df ]
 * VIEWER-616: правки по скрипту синхронизации                                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/d7ee9f5 ]
 * VIEWER-616: в скрипт добавлен распределённый лок, скрипт теперь запускается вместе с инстансом Webauth                                      [ https://github.yandex-team.ru/idm/webauth/commit/c00a6d5 ]
 * VIEWER-616: правки багов, правки деплоя                                                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/4da6729 ]
 * VIEWER-616: обновлён скрипт (изменена структура узлов и логика их создания/удаления)                                                        [ https://github.yandex-team.ru/idm/webauth/commit/de4137e ]
 * VIEWER-616: реализовано обновление IDM согласно окружениям; мелкие правки                                                                   [ https://github.yandex-team.ru/idm/webauth/commit/f37c026 ]
 * VIEWER-616: добавлен сервис, регулярно загружающий информацию обо всех окружениях Qloud                                                     [ https://github.yandex-team.ru/idm/webauth/commit/13f6404 ]
 * VIEWER-617: небольшой фикс неправильного ответа от oauth.y-t.ru                                                                             [ https://github.yandex-team.ru/idm/webauth/commit/872f58d ]
 * Расширен вывод логов                                                                                                                        [ https://github.yandex-team.ru/idm/webauth/commit/02653b0 ]
 * VIEWER-635: теперь для неаутентифицированных пользователей check_oauth_token возвращает id OAuth-приложения                                 [ https://github.yandex-team.ru/idm/webauth/commit/5ad7e02 ]
 * VIEWER-617: добавлено кеширование системы webauth-qloud                                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/09efd0d ]
 * Правки по логированию                                                                                                                       [ https://github.yandex-team.ru/idm/webauth/commit/5097f76 ]
 * Ограничена выдача содержимого запроса при логировании                                                                                       [ https://github.yandex-team.ru/idm/webauth/commit/3f4793a ]
 * VIEWER-617: поправлены тесты после ребейза                                                                                                  [ https://github.yandex-team.ru/idm/webauth/commit/4957269 ]
 * VIEWER-617: схема с ассессорским токеном переделана под прямой вызов Authorizer                                                             [ https://github.yandex-team.ru/idm/webauth/commit/f95415c ]
 * VIEWER-617: Authorizator вынесен в отдельный файл                                                                                           [ https://github.yandex-team.ru/idm/webauth/commit/d9563ef ]
 * VIEWER-617: логика авторизации отвязана от Tornado                                                                                          [ https://github.yandex-team.ru/idm/webauth/commit/d0de90b ]
 * VIEWER-617: добавлена параметризация тестов blackbox по внутренним/внешним хостам                                                           [ https://github.yandex-team.ru/idm/webauth/commit/0f8bbd7 ]
 * VIEWER-617: замоканные http-запросы теперь хранят хост, http-client вытаскивает из HTTPRequest url запроса                                  [ https://github.yandex-team.ru/idm/webauth/commit/409f8ca ]
 * VIEWER-617: добавлеы таймауты и более точные описания ошибок при хождении в blackbox                                                        [ https://github.yandex-team.ru/idm/webauth/commit/19809f8 ]
 * VIEWER-617: добавлено хождение во внешний ЧЯ для доменов не из yandex-team.ru                                                               [ https://github.yandex-team.ru/idm/webauth/commit/b8107ef ]
 * VIEWER-612: добавлено получение uid, его прокидывание в заголовки. Поправлены тесты                                                         [ https://github.yandex-team.ru/idm/webauth/commit/06d9e2c ]
 * VIEWER-596: запись кук теперь выполняется с атрибутами secure и httponly                                                                    [ https://github.yandex-team.ru/idm/webauth/commit/05092ae ]
 * VIEWER-596: перенос криптографического ключа в настройки. Правки по переименованию настроек                                                 [ https://github.yandex-team.ru/idm/webauth/commit/58d7c88 ]
 * VIEWER-596: поправлен баг с не-выходом из хендлера, добавлена проверка формата параметра state                                              [ https://github.yandex-team.ru/idm/webauth/commit/d1841ca ]
 * VIEWER-596: вывод url запроса при ошибке создания/удаления узлов IDM                                                                        [ https://github.yandex-team.ru/idm/webauth/commit/21ed01b ]
 * VIEWER-596: поправлен баг с не-выходом из DeleteQloudRolesHandler.get(), написаны тесты для этой ручки                                      [ https://github.yandex-team.ru/idm/webauth/commit/a22986f ]
 * VIEWER-596: поправлен баг с не-выходом из AddQloudRolesHandler.get(), написаны тесты для этой ручки                                         [ https://github.yandex-team.ru/idm/webauth/commit/ffb9fef ]
 * VIEWER-596: упрощена обработка запросов в IDM из ручек add/delete_qloud_roles                                                               [ https://github.yandex-team.ru/idm/webauth/commit/5140e1d ]
 * VIEWER-596: поправлен баг с порчей HMAC, написаны тесты для crypto_utils                                                                    [ https://github.yandex-team.ru/idm/webauth/commit/ccccf25 ]
 * VIEWER-596: обработка неправильного формата роли в IdmManager, покрытие тестами check_idm_role                                              [ https://github.yandex-team.ru/idm/webauth/commit/a34f8e9 ]
 * VIEWER-596: небольшие правки по flake8                                                                                                      [ https://github.yandex-team.ru/idm/webauth/commit/cd533f8 ]
 * VIEWER-596: добавлены ручки для создания/удаления ролей окружений Qloud                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/d6c0c9e ]
 * VIEWER-596: реализована схема внешней авторизации через OAuth-токен приложения Webauth                                                      [ https://github.yandex-team.ru/idm/webauth/commit/6aa0fc0 ]
 * VIEWER-596: auth_request теперь возвращает 200/401/403                                                                                      [ https://github.yandex-team.ru/idm/webauth/commit/fbcbdf8 ]
 * VIEWER-596: IDM_HOST вынесен в настройки, переименованы файлы                                                                               [ https://github.yandex-team.ru/idm/webauth/commit/096cbf9 ]
 * VIEWER-596: небольшой рефакторинг хэндлера авторизации                                                                                      [ https://github.yandex-team.ru/idm/webauth/commit/f6c3eda ]
 * VIEWER-622: поправлено форматирование при логировании                                                                                       [ https://github.yandex-team.ru/idm/webauth/commit/e678834 ]
 * VIEWER-622: более активное логирование полученных и обработанных запросов                                                                   [ https://github.yandex-team.ru/idm/webauth/commit/bd720fc ]
 * VIEWER-622: конфигурация логгера через словарь                                                                                              [ https://github.yandex-team.ru/idm/webauth/commit/b1ce94b ]
 * VIEWER-622: скорректированы уровни логирования                                                                                              [ https://github.yandex-team.ru/idm/webauth/commit/10ce35e ]
 * VIEWER-622: удалена информация о потоке исполнения в логах                                                                                  [ https://github.yandex-team.ru/idm/webauth/commit/a15c1d4 ]
 * VIEWER-622: ylog и rsyslog более не используются                                                                                            [ https://github.yandex-team.ru/idm/webauth/commit/9d662f9 ]
 * VIEWER-620: интервал запуска кеширования уменьшен до 5 минут                                                                                [ https://github.yandex-team.ru/idm/webauth/commit/319b32a ]
 * VIEWER-620: удалено использование ACL                                                                                                       [ https://github.yandex-team.ru/idm/webauth/commit/0ae06c3 ]
 * VIEWER-620: файлы сборки добавлены в .gitignore                                                                                             [ https://github.yandex-team.ru/idm/webauth/commit/7271322 ]
 * VIEWER-620: реализована настройка размера запроса к IDM                                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/a910860 ]
 * VIEWER-620: захват лока при генерации кеша сделан блокирующим                                                                               [ https://github.yandex-team.ru/idm/webauth/commit/c221fd7 ]
 * VIEWER-620: реализована backoff-политика при обращении к IDM                                                                                [ https://github.yandex-team.ru/idm/webauth/commit/89e71ee ]
 * VIEWER-620: правки по логированию                                                                                                           [ https://github.yandex-team.ru/idm/webauth/commit/1a5ae8d ]
 * VIEWER-620: удалён скрипт для генерации ACL                                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/876908a ]
 * VIEWER-619: отмена обновления системы в случае ошибки при получении ролей                                                                   [ https://github.yandex-team.ru/idm/webauth/commit/a8007b2 ]
 * VIEWER-602: перечислениие параметров сообщений логгера через запятую                                                                        [ https://github.yandex-team.ru/idm/webauth/commit/c4058c0 ]
 * VIEWER-602: лок файлов вынесен в контекст-менеджер                                                                                          [ https://github.yandex-team.ru/idm/webauth/commit/0affb1e ]
 * VIEWER-602: неблокирующий лок на файле с ролями в скрипте генерации                                                                         [ https://github.yandex-team.ru/idm/webauth/commit/7eeb9c3 ]
 * VIEWER-602: исправлен баг с не-выходом из функции get() после вызова decline() в AuthRequestHandler                                         [ https://github.yandex-team.ru/idm/webauth/commit/cb2ef47 ]
 * VIEWER-602: requests, пул процессов                                                                                                         [ https://github.yandex-team.ru/idm/webauth/commit/34a1b41 ]
 * VIEWER-602: поддержка параметров idm_role и fields_data                                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/a335da1 ]
 * VIEWER-602: добавлен скрипт для кеширования ролей из IDM                                                                                    [ https://github.yandex-team.ru/idm/webauth/commit/dd03f10 ]
 * VIEWER-595: Вывод причин при отсутствии credentials. Переименование настроек, рефакторинг функций                                           [ https://github.yandex-team.ru/idm/webauth/commit/ead7f0e ]
 * VIEWER-595: изменена обработка X-Qloud-Ssl-Verified                                                                                         [ https://github.yandex-team.ru/idm/webauth/commit/fb53512 ]
 * VIEWER-595: правки по стилю кода                                                                                                            [ https://github.yandex-team.ru/idm/webauth/commit/9896e02 ]
 * VIEWER-595: способы аутентификации вынесены в отдельные классы, поправлены тесты                                                            [ https://github.yandex-team.ru/idm/webauth/commit/5f939a2 ]
 * VIEWER-595: проверка issuer dn для клиентского сертификата                                                                                  [ https://github.yandex-team.ru/idm/webauth/commit/7ee647c ]
 * VIEWER-595: разделение AuthRequestHandler.get на несколько более мелких функций                                                             [ https://github.yandex-team.ru/idm/webauth/commit/c7205d2 ]
 * VIEWER-595: по-другому реализованная обработка способов проверки                                                                            [ https://github.yandex-team.ru/idm/webauth/commit/7f26db1 ]
 * VIEWER-595: допустимые ssl-домены вынесены в настройки                                                                                      [ https://github.yandex-team.ru/idm/webauth/commit/725d386 ]
 * VIEWER-595: unicode_literals                                                                                                                [ https://github.yandex-team.ru/idm/webauth/commit/be2634e ]
 * VIEWER-595: добавлены тесты для AuthRequestHandler.get                                                                                      [ https://github.yandex-team.ru/idm/webauth/commit/b1d5510 ]
 * VIEWER-595: добавлены тесты для AuthRequestHandler.check_cert                                                                               [ https://github.yandex-team.ru/idm/webauth/commit/ad9bd16 ]
 * VIEWER-595: тесты подстроены под новое поведение check_blackbox и check_acl                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/57339d1 ]
 * VIEWER-595: отсутствующий и невалидный сертификат теперь обрабатываются по-разному                                                          [ https://github.yandex-team.ru/idm/webauth/commit/07edb4f ]
 * VIEWER-595: переход на вторую версию API                                                                                                    [ https://github.yandex-team.ru/idm/webauth/commit/d2548a1 ]
 * VIEWER-595: обработка pipeline согласно Webauth API на вики                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/1f554c2 ]
 * VIEWER-592: добавлен метод проверки клиентского сертификата                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/7d52f02 ]
 * VIEWER-590 (#7)                                                                                                                             [ https://github.yandex-team.ru/idm/webauth/commit/eb0d189 ]
 * VIEWER-583: тестирование (#5)                                                                                                               [ https://github.yandex-team.ru/idm/webauth/commit/ca6c17e ]
 * VIEWER-580: тесты разбиты на несколько файлов                                                                                               [ https://github.yandex-team.ru/idm/webauth/commit/dd21755 ]
 * VIEWER-580: Убрано строгое требование sessionid2 в соответствие с изменениями Blackbox. Аналогично поправлены функциональные тесты          [ https://github.yandex-team.ru/idm/webauth/commit/cc048f8 ]
 * VIEWER-580: добавлены функциональные тесты для auth.check_acl                                                                               [ https://github.yandex-team.ru/idm/webauth/commit/4e386d7 ]
 * VIEWER-580: добавлены функциональные тесты для функции auth.check_blackbox                                                                  [ https://github.yandex-team.ru/idm/webauth/commit/f9d7174 ]
 * VIEWER-580: запуск в виде модуля, замена импортов на относительные                                                                          [ https://github.yandex-team.ru/idm/webauth/commit/d9ecd55 ]
 * VIEWER-580: проверки сессии через blackbox и доступа по ACL вынесены в отдельные функции                                                    [ https://github.yandex-team.ru/idm/webauth/commit/8defb27 ]
 * VIEWER-580: Запрос в blackbox и чтение ACL сделаны асинхронными                                                                             [ https://github.yandex-team.ru/idm/webauth/commit/9f83aa2 ]
 * VIEWER-580: Поправлены заголовки ответа и отключено кеширование по etag                                                                     [ https://github.yandex-team.ru/idm/webauth/commit/3a68195 ]
 * VIEWER-580: Каркас приложения изменён на совместимый с tornado                                                                              [ https://github.yandex-team.ru/idm/webauth/commit/bb27844 ]
 * VIEWER-580: убраны упоминания nginx и uwsgi                                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/0101cba ]
 * VIEWER-581: поправлен путь к скрипту генерации ACL                                                                                          [ https://github.yandex-team.ru/idm/webauth/commit/f7a0d5b ]
 * VIEWER-581: поправлены пути к файлу с переменными окружения                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/420f438 ]
 * Обновлён docker-compose.yaml                                                                                                                [ https://github.yandex-team.ru/idm/webauth/commit/f664564 ]
 * Поправлен параметр parent в запросе к IDM                                                                                                   [ https://github.yandex-team.ru/idm/webauth/commit/b082137 ]
 * Удалены все конфиги вьюверов                                                                                                                [ https://github.yandex-team.ru/idm/webauth/commit/2a41d73 ]
 * VIEWER-578: Удалена фильтрация по имени сервера в конфиге nginx                                                                             [ https://github.yandex-team.ru/idm/webauth/commit/bf399c6 ]
 * VIEWER-578: Почищены ненужные cron-задачи                                                                                                   [ https://github.yandex-team.ru/idm/webauth/commit/28a024d ]
 * VIEWER-578: Исправлен баг с неправильным именем системы idm и комментариями                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/b233c50 ]
 * VIEWER-578: Запрос в idm для получения списка вьюверов теперь использует параметр parent                                                    [ https://github.yandex-team.ru/idm/webauth/commit/096251d ]
 * VIEWER-578: Получение списка хостов через idm                                                                                               [ https://github.yandex-team.ru/idm/webauth/commit/6cbdf30 ]
 * VIEWER-578: Удалены вспомогательные скрипты вьювера                                                                                         [ https://github.yandex-team.ru/idm/webauth/commit/96ab1d9 ]
 * VIEWER-578: Использование ручки /info у вьювера вместо локального хранения конфигураций                                                     [ https://github.yandex-team.ru/idm/webauth/commit/d22caa5 ]
 * VIEWER-577: Поправлены пути к python-модулю                                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/5277f7c ]
 * VIEWER-577: Переименован python-модуль, связанные с ним директории и скрипты; Вырезан скрипт для генерации index.html                       [ https://github.yandex-team.ru/idm/webauth/commit/3686403 ]
 * VIEWER-577: Удалены упоминания sites-enabled                                                                                                [ https://github.yandex-team.ru/idm/webauth/commit/b55f3b8 ]
 * VIEWER-577: Конфигурация nginx изменена для запуска webauth                                                                                 [ https://github.yandex-team.ru/idm/webauth/commit/63a362c ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-23 17:13:11+03:00

0.851
-----
 * VIEWER-572: Переключить бекенды webmaster-data.viewer.yandex-team.ru                         [ https://github.yandex-team.ru/idm/viewer/commit/63eeed0 ]
 * TOOLSUP-19948: Странное с вьюером saas-dm.viewer.yandex-team.ru     Убрал устаревший бекэнд  [ https://github.yandex-team.ru/idm/viewer/commit/c99c2ac ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-07-13 13:32:30+00:00

0.850
-----
 * проверяем конфиги вьюверов раз в 15 минут  [ https://github.yandex-team.ru/idm/viewer/commit/28620a4 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-07-13 13:18:49+00:00

0.849
-----
 * VIEWER-571: Удалить вьюер idash.v.yandex-team.ru                                                                                                           [ https://github.yandex-team.ru/idm/viewer/commit/abcac17 ]
 * Host morda-madm-delta.viewer.yandex-team.ru with backends v44.wdevx.yandex.net:1443 and resps cheetah,dkhlynin,torubarov,wwax added to viewers-available/  [ https://github.yandex-team.ru/idm/viewer/commit/ba4bcf4 ]
 * Host morda-madm-beta.viewer.yandex-team.ru with backends v44.wdevx.yandex.net:1443 and resps cheetah,dkhlynin,torubarov,wwax added to viewers-available/   [ https://github.yandex-team.ru/idm/viewer/commit/605a0c2 ]
 * Host morda-madm-alpha.viewer.yandex-team.ru with backends v44.wdevx.yandex.net:1443 and resps cheetah,wwax,torubarov,dkhlynin added to viewers-available/  [ https://github.yandex-team.ru/idm/viewer/commit/09b461e ]
 * Host morda-madm-omega.viewer.yandex-team.ru with backends v44.wdevx.yandex.net:1443 and resps cheetah,wwax,torubarov,dkhlynin added to viewers-available/  [ https://github.yandex-team.ru/idm/viewer/commit/dd05a5e ]
 * Host morda-madm-gamma.viewer.yandex-team.ru with backends v44.wdevx.yandex.net:1443 and resps cheetah,dkhlynin,torubarov,wwax added to viewers-available/  [ https://github.yandex-team.ru/idm/viewer/commit/3268e85 ]
 * Host morda-madm-test.viewer.yandex-team.ru with backends v44.wdevx.yandex.net:1443 and resps cheetah,dkhlynin,torubarov,wwax added to viewers-available/   [ https://github.yandex-team.ru/idm/viewer/commit/fdff7a6 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-07-11 14:38:40+00:00

0.848
-----
 * VIEWER-568: Сделать новый вьювер antifraud.v.yandex-team.ru  [ https://github.yandex-team.ru/idm/viewer/commit/920f1d5 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-07-10 20:32:49+00:00

0.847
-----
 * Host orgvisits.viewer.yandex-team.ru with backends frau.search.yandex.net:9825 and resps anelyubin,goltsman added to viewers-available/  [ https://github.yandex-team.ru/idm/viewer/commit/884c760 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-07-10 13:35:57+00:00

0.846
-----
 * Host callisto-test.viewer.yandex-team.ru with backends jupiter-beta.haze.yandex.net:9121 and resps zhenyok,grmammaev,zagevalo added to viewers-available/  [ https://github.yandex-team.ru/idm/viewer/commit/24518c3 ]
 * VIEWER-565: Нужно перенастроить вьюер jupiter-nightly.viewer.yandex-team.ru на новый бэкэнд                                                                [ https://github.yandex-team.ru/idm/viewer/commit/973e300 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-06-27 15:43:21+00:00

0.845
-----
 * Host nevasca-cm.viewer.yandex-team.ru with backends wspm3.search.yandex.net:3670 and resps renadeen,ashagarov,zudina,cepera added to viewers-available/  [ https://github.yandex-team.ru/idm/viewer/commit/1541a67 ]
 * VIEWER-555: Перевезти ontodbfixes.v.yandex-team.ru на новые бекенды                                                                                      [ https://github.yandex-team.ru/idm/viewer/commit/ed40074 ]
 * VIEWER-553: Вьюверы для кластермастера taas-big                                                                                                          [ https://github.yandex-team.ru/idm/viewer/commit/502b770 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-06-08 07:25:58+00:00

0.844
-----
 * Host posmonitor.viewer.yandex-team.ru with backends frauda.search.yandex.net:80 and resps foton,akazz,noxandry added to viewers-available/  [ https://github.yandex-team.ru/idm/viewer/commit/73f8473 ]
 * Фикс скриптов создания вьюверов                                                                                                             [ https://github.yandex-team.ru/idm/viewer/commit/279b5d5 ]
 * Фикс конфига ppl                                                                                                                            [ https://github.yandex-team.ru/idm/viewer/commit/6514fd5 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-06-05 16:03:51+00:00

0.843
-----
 * Host ppl.v.yandex-team.ru with backends ppl-viewer.haze.yandex.net:8080 and resps nkmakarov,panoff,iv-ivan added to viewers-available/  [ https://github.yandex-team.ru/idm/viewer/commit/0e74cd5 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-06-05 14:28:54+00:00

0.842
-----
 * Ещё закомментировал пропавшие из dns хосты  [ https://github.yandex-team.ru/idm/viewer/commit/070b0ba ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-05-19 14:51:38+00:00

0.841
-----
 * Закомментировал пропавшие из dns хосты  [ https://github.yandex-team.ru/idm/viewer/commit/7534a36 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-05-19 14:35:55+00:00

0.840
-----
 * VIEWER-547: Сконфигурировать бэкенды codesearch.viewer  [ https://github.yandex-team.ru/idm/viewer/commit/a7534d8 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-05-02 09:14:04+00:00

0.839
-----
 * VIEWER-546: Добавить бэк к вьюеру codesearch  [ https://github.yandex-team.ru/idm/viewer/commit/8271c4b ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-04-18 12:54:39+00:00

0.838
-----
 * Правильный резолвер  [ https://github.yandex-team.ru/idm/viewer/commit/abc3ca0 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-04-14 12:48:17+00:00

0.837
-----
 * VIEWER-503: Удалить вьюеры                                                   [ https://github.yandex-team.ru/idm/viewer/commit/e06303a ]
 * VIEWER-537: [tallis.haze.yandex.net] Cлушать порты на IPv6 интерфейсе        [ https://github.yandex-team.ru/idm/viewer/commit/6ebebb4 ]
 * VIEWER-532: [arachnid09.search.yandex.net] Cлушать порты на IPv6 интерфейсе  [ https://github.yandex-team.ru/idm/viewer/commit/cc7acaa ]
 * VIEWER-533: [vdbdb-dev.search.yandex.net] Cлушать порты на IPv6 интерфейсе   [ https://github.yandex-team.ru/idm/viewer/commit/bcfa853 ]
 * VIEWER-527: [vdb-dev.search.yandex.net] Cлушать порты на IPv6 интерфейсе     [ https://github.yandex-team.ru/idm/viewer/commit/3daf07e ]
 * VIEWER-524: [vdb.yandex.ru] Cлушать порты на IPv6 интерфейсе                 [ https://github.yandex-team.ru/idm/viewer/commit/b52a999 ]
 * VIEWER-493: Переезд в Qloud                                                  [ https://github.yandex-team.ru/idm/viewer/commit/699a570 ]
 * VIEWER-543: Переключить бэкнеды board-st.v.yandex-team.ru                    [ https://github.yandex-team.ru/idm/viewer/commit/dfc0002 ]
 * VIEWER-542: Переключить бэкенды addurl.viewer.yandex-team.ru                 [ https://github.yandex-team.ru/idm/viewer/commit/b53b324 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-04-10 10:49:44+00:00

0.836
---

  * VIEWER-518: Host orgheatmap.v.yandex-team.ru with backends man1-6589.search.yandex.net:8081 and resps lamo,marvelstas added to viewers-available/
  * VIEWER-520: Host jupiter-delivery-ro.viewer.yandex-team.ru with backends jupiter-cm.search.yandex.net:8204 and resps chelentano,grmammaev added to viewers-available/
  * VIEWER-519: Подключить kikimr.viewer.yandex-team.ru для процессов rtmr-server
  * VIEWER-514: Добавить хосты к rotor.viewer.yandex-team.ru

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2017-03-24 17:56:23

0.835
---

  * VIEWER-511: [newspikes.viewer] Перевести бекэнды на IPv6
  * VIEWER-510: [kiwi-admin.viewer] Перевести бекэнды на IPv6
  * VIEWER-513: Заявка на вьювер puma
  * Host bm.v.yandex-team.ru with backends augur-social-web-man01prod.haze.yandex.net:80,augur-social-web-sas01prod.haze.yandex.net:80 and resps vegayours added to viewers-available/
  * Host bm-testing.v.yandex-team.ru with backends augur-social-web-sas01dev.haze.yandex.net:80 and resps vegayours added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2017-03-13 19:29:02

0.834
---

  * bm-testing.v.yandex-team.ru with backends augur-social-web-
    sas01dev.haze.yandex.net:80 and resps vegayours added to viewers-
    available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2017-03-13 19:25:11

0.833
---

  * bm..v.yandex-team.ru with backends augur-social-web-
    man01prod.haze.yandex.net:80,augur-social-web-
    sas01prod.haze.yandex.net:80 and resps vegayours added to viewers-
    available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2017-03-13 19:24:52

0.832
---

  * seo-coverage.viewer.yandex-team.ru with backends
    mfas008.search.yandex.net:80,viewspam.search.yandex.net:80,frauda.se
    arch.yandex.net:80 and resps akindyakov,moskupols added to viewers-
    available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2017-02-28 14:34:55

0.831
---

  * VIEWER-500: Подключить бэкэнды к rotor.viewer.yandex-team.ru
  * выключил cs.viewer.yandex-team.ru

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2017-02-21 14:00:09

0.830
---

  * VIEWER-498: Проблема с zen-zap.v.yandex-team.ru

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2017-02-13 14:27:57

0.829
---

  * VIEWER-492: Поправить ссылку на форму IDM в заглушке
  * VIEWER-495: Поднять таймаут на ответ бэкенда до 3 минут
  * VIEWER-497: вьювер документов картиночного индекса переезжает на tarski
  * Host userfeat.viewer.yandex-team.ru with backends perun.search.yandex.net:15733 and resps diver added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2017-02-06 10:06:26

0.828
---

  * userfeat.viewer.yandex-team.ru with backends
    perun.search.yandex.net:15733 and resps diver added to viewers-
    available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2017-02-06 09:57:20

0.827
---

  * VIEWER-494: Изменить список бекендов для вьюера idash.v.yandex-team.ru

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2017-01-25 20:45:10

0.826
---

  * Убрал копипасту из конфигов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-12-27 17:10:17

0.825
---

  * выключил myts бекэнды

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-12-21 20:44:24

0.824
---

  * VIEWER-490: Сменить адрес бекенда

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-12-21 20:31:50

0.823
---

  * video-findurl.viewer.yandex-team.ru with backends mago-nn-
    dev.haze.yandex.net:5005 and resps mago-nn,matveieff added to
    viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-12-14 03:00:53

0.822
---

  * geogen-cm.v.yandex-team.ru with backends geogen.yandex.ru:3130 and
    resps iofik added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-12-12 20:56:15

0.821
---

  * cv.viewer.yandex-team.ru with backends jones.yandex.ru:80 and resps
    skyhawk,krainov,ladaev added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-12-02 20:16:47

0.820
---

  * video-misc-factors.viewer.yandex-team.ru with backends
    slovo2.search.yandex.net:9472 and resps avdergunov,tolich added to
    viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-12-02 20:13:04

0.819
---

  * smoo.viewer.yandex-team.ru with backends s1.clop.yandex.net:81 and
    resps wwax added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-12-02 20:07:45

0.818
---

  * VIEWER-473: Доступ к вьюверам через OAuth

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-12-01 19:19:00

0.817
---

  * Version 0.817

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-11-25 12:52:30

0.816
---

  * callisto.viewer.yandex-team.ru with backends jupiter-
    cm.search.yandex.net:8603 and resps
    steela,isafarov,grmammaev,alexeyche added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-11-24 10:15:53

0.815
---

  * saas-dm.viewer.yandex-team.ru with backends ws36-
    206.search.yandex.net:1031,sas1-4617.search.yandex.net:1036,man1-
    5213.search.yandex.net:1025 and resps saku,osidorkin added to
    viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-11-24 10:10:21

0.814
---

  * Version 0.814

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-11-22 10:13:42

0.813
---

  * Version 0.813

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-11-15 10:06:14

0.812
---

  * Version 0.812

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-11-14 17:00:01

0.811
---

  * Version 0.811

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-11-09 16:59:43

0.810
---

  * Version 0.810

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-11-07 20:26:14

0.809
---

  * matrixnet-perfstand.v.yandex-team.ru with backends kirillovs-
    mx.haze.yandex.net:5000 and resps kirillovs,annaveronika added to
    viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-11-07 14:49:56

0.808
---

  * jupiter-backup.viewer.yandex-team.ru with backends jupiter-cm-
    vm.haze.yandex.net:8103 and resps
    steela,isafarov,shuster,zhenyok,grmammaev,niknik added to viewers-
    available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-19 14:57:24

0.807
---

  * yt-vivisector.viewer.yandex-team.ru with backends
    perun.search.yandex.net:15732 and resps akhropov,diver added to
    viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-19 14:56:49

0.806
---

  * VIEWER-454

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-17 22:45:05

0.805
---

  * VIEWER-445

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-17 16:54:33

0.804
---

  * VIEWER-454

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-17 10:40:31

0.803
---

  * revert 24725

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-11 12:44:38

0.802
---

  * video-docbase-ultra.viewer.yandex-team.ru with backends
    slovo2.search.yandex.net:9452 and resps vkap,tolich added to
    viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-10 19:53:38

0.801
---

  * video-docbase-fresh.viewer.yandex-team.ru with backends
    slovo2.search.yandex.net:9462 and resps vkap,tolich added to
    viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-10 19:53:19

0.800
---

  * news-rkn.viewer.yandex-team.ru with backends news-
    rkn1.haze.yandex.net:80,news-rkn2.haze.yandex.net:80 and resps
    gennadiy added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-10 19:52:41

0.799
---

  * rem-perun.viewer.yandex-team.ru with backends
    perun.search.yandex.net:25001 and resps diver,geolog added to
    viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-10 19:51:01

0.798
---

  * rtp.viewer.yandex-team.ru with backends perun.search.yandex.net:8081
    and resps agniash,akhropov,diver added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-09-22 18:43:40

0.797
---

  * VIEWER-449: change backend for lemur-cm

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-09-16 18:48:52

0.796
---

  * VIEWER-448

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-09-15 21:38:15

0.795
---

  * video-docbase.viewer.yandex-team.ru with backends
    slovo2.search.yandex.net:9442 and resps vkap,matveieff,tolich added
    to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-09-06 17:21:35

0.794
---

  * dbview-testing.viewer.yandex-team.ru with backends
    xya.search.yandex.net:80 and resps bazil added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-09-06 17:21:18

0.793
---

  * webmaster-data.viewer.yandex-team.ru with backends wmcon-backend-
    1.search.yandex.net:8150,wmcon-backend-2.search.yandex.net:8150 and
    resps lester added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-09-06 17:20:55

0.792
---

  * lemur-stg.v.yandex-team.ru with backends ukrop-
    master.search.yandex.net:8090 and resps abogutskiy added to viewers-
    available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-08-26 21:34:20

0.791
---

  * VIEWER-433

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-08-23 20:40:06

0.790
---

  * yahrefs.viewer.yandex-team.ru with backends
    mfas008.search.yandex.net:80,viewspam.search.yandex.net:80,frauda.se
    arch.yandex.net:80 and resps dude added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-08-23 15:34:17

0.789
---

  * yandex-merge-test.viewer.yandex-team.ru with backends
    lya.search.yandex.net:5160 and resps saku,aavdonkin added to
    viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-08-23 14:57:56

0.788
---

  * alphapth

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-08-17 14:58:56

0.787
---

  * saas-graph

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-08-08 17:20:17

0.786
---

  * VIEWER-430: Перенацелить https://gemini-cm.viewer.yandex-team.ru/
  * VIEWER-432: Поменять backend'ы для 'http://av-client-log.viewer.yandex-team.ru/' на 'vdblog-bro-{1,2,3}.search.yandex.net'

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-08-02 17:32:24

0.785
---

  * Пофиксил конфиг upstream'а для gemini

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-29 15:41:52

0.784
---

  * VIEWER-429: Перенацелить https://gemini.viewer.yandex-team.ru/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-29 14:44:41

0.783.3
---

  * selection-rank.v.yandex-team.ru with backends gemini-
    dev2.search.yandex.net:5009 and resps yurap added to viewers-
    available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-26 16:06:32

0.783.2
---

  * virustotal.viewer.yandex-team.ru with backends
    mfas008.search.yandex.net:8022,frauda.search.yandex.net:8022 and
    resps reddog,cepera added to viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-18 12:58:49

0.783.1
---

  * Version 0.783.1

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-12 20:47:45

0.783
---

  * Version 0.783

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-12 20:27:02

0.782
---

  * Some backend fixes

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-08 17:58:52

0.781
---

  * VIEWER-423

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-07 20:19:16

0.780
---

  * juno.viewer.yandex-team.ru with backends jupiter-
    cm.search.yandex.net:7892 and resps shuster,niknik added to viewers-
    available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-07 20:07:09

0.779
---

  * Delete viewer report-data-updaterd
  * Delete viewer ontodbfixes

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-06 17:05:49

0.778
---

  * av-client-log.viewer.yandex-team.ru with backends vdblog-bro-
    3.haze.yandex.net:80,vdblog-bro-2.haze.yandex.net:80,vdblog-bro-
    1.haze.yandex.net:80 and resps cepera,avkov,anechiporuk added to
    viewers-available/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-04 18:07:28

0.777
---

  * VIEWER-419: Create new viewer queue.v.yandex-team.ru

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-04 17:53:11

0.776.1
---

  * some fixes

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-06-30 11:28:33

0.776
---

  * VIEWER-416: add jupiter-nightly.viewer.yandex-team.ru viewer

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-06-30 11:06:39

0.775
---

  * setup-test fix

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-29 11:41:10

0.774
---

  * setup and setup-test fixes

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-29 11:35:19

0.773
---

  * fix crawlview backend

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-24 15:22:16

0.772
---

  * fixes to watto

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-24 12:22:52

0.771
---

  * watto-cluster.viewer.yandex-team.ru

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-24 12:08:22

0.770
---

  * peoplebase-cm.v.yandex-team.ru with backends
    bigbrother.yandex.ru:8001 and resps nkmakarov,panoff added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-23 17:25:26

0.769
---

  * vdblog-bro.v.yandex-team.ru with backends vdblog-bro-
    3.haze.yandex.net:80,vdblog-bro-2.haze.yandex.net:80,vdblog-bro-
    1.haze.yandex.net:80 and resps cepera,avkov,anechiporuk added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-21 14:02:10

0.768
---

  * add pdfetch to zora

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-17 16:40:06

0.767
---

  * limbo.v.yandex-team.ru with backends ukrop-
    master.search.yandex.net:4150 and resps lazy,olegsenin added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-17 11:24:07

0.766
---

  * zen-zap.v.yandex-team.ru with backends zstorage-
    test.yandex.net:12015 and resps khamukhin added to viewers-
    available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-15 18:38:34

0.765
---

  * lemur-quality-cm.v.yandex-team.ru with backends ukrop-
    master.search.yandex.net:4140 and resps lazy,egoregor,olegsenin
    added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-10 17:26:42

0.764
---

  * https://st.yandex-team.ru/INFRASEARCH-1235: replaced /api/frontend with /api/v1

 [Zhivotnev Vladislav](https://staff.yandex-team.ru/inkvizitor68sl@yandex-team.ru) 2016-06-02 15:54:21

0.763
---

  * usf-beta-build.viewer.yandex-team.ru with backends
    ultralisk01e.search.yandex.net:18106 and resps geolog added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-06-01 15:43:12

0.762
---

  * again

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-27 13:20:40

0.761
---

  * delete some old viewers

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-27 13:18:49

0.760
---

  * voicecode.v.yandex-team.ru with backends
    codesearch.search.yandex.net:18181 and resps mvel,kartynnik added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-27 12:19:21

0.759
---

  * adult-cm.viewer.yandex-team.ru with backends
    mfas006.search.yandex.net:19002 and resps akolosov,g-
    kostin,lkozhinov,achigin,vdf added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-21 18:04:51

0.758
---

  * antimalware-cm.viewer.yandex-team.ru with backends vdblog-
    5.search.yandex.net:3590 and resps anechiporuk,cepera added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-21 17:59:45

0.757
---

  * galileo.viewer.yandex-team.ru with backends jupiter-
    cm.search.yandex.net:7890 and resps shuster,niknik added to viewers-
    available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-19 11:47:41

0.756
---

  * port for crawlview.v was fixed

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-19 11:28:02

0.755
---

  * crawlview.v.yandex-team.ru

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-18 17:03:12

0.754
---

  * new main backend for webspam-spm

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-12 16:21:25

0.753
---

  * new main backend for webspam-spm-support

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-12 16:11:12

0.752
---

  * fleur-cm.viewer.yandex-team.ru with backends
    simcity00.search.yandex.net:3580 and resps cepera added to viewers-
    available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-12 11:33:16

0.751
---

  * direct-checker-batch-cm.viewer.yandex-team.ru with backends
    mfas007.search.yandex.net:8042 and resps galtsev,diseaz,bnagaev
    added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-05-12 11:32:38

0.750
---

  * ukrop-jupiter.v.yandex-team.ru with backends
    ukropmon00.search.yandex.net:8888 and resps lazy,olegsenin added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-28 12:23:20

0.749
---

  * morchella removed
  * mirrors-merge-ro backend fix

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-22 15:39:16

0.748
---

  * video-duplicates.viewer.yandex-team.ru with backends
    sable02.search.yandex.net:8253 and resps vilenkin added to viewers-
    available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-21 14:19:58

0.747
---

  * direct-checker-rt-cm.viewer.yandex-team.ru with backends
    mfas007.search.yandex.net:26284 and resps galtsev,diseaz,bnagaev
    added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-21 14:19:15

0.746
---

  * without-acl for url2smth

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-14 15:46:20

0.745
---

  * url2smth.viewer.yandex-team.ru with backends
    mfas008.search.yandex.net:29474,frauda.search.yandex.net:29474 and
    resps bnagaev added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-14 15:22:26

0.744
---

  * fixed port for ontodbfixes-test

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-11 15:26:28

0.743
---

  * directpth-cm.viewer.yandex-team.ru with backends
    plus002.search.yandex.net:3476 and resps akindyakov added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-10 17:50:58

0.742
---

  * new backends for watto

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-10 17:49:39

0.741
---

  * gemini moved to s.y.n

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-07 19:34:43

0.740
---

  * geo-metrics-cm.v.yandex-team.ru with backends geo-abt-
    2.haze.yandex.net:19000 and resps d-sun-d added to viewers-
    available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-06 16:39:24

0.739
---

  * ontodbfixes-test.viewer.yandex-team.ru with backends sas1-
    4895.search.yandex.net:10240 and resps nataxane,belalex,qqq added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-06 16:38:37

0.738
---

  * fix mirrors-dev

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-06 16:26:38

0.737
---

  * mirrors-dev.viewer.yandex-team.ru with backends mirrors-
    dev00.search.yandex.net:443 and resps almaslov added to viewers-
    available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-06 15:54:51

0.736
---

  * ya.yandex.ru -> lya.search.yandex.net

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-05 14:46:56

0.735
---

  * antispam-metrics root redirect

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-04-04 13:33:43

0.734
---

  * new backend for switch.v

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-31 11:08:48

0.733
---

  * changing backend for vdbview.viewer

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-30 20:17:47

0.732
---

  * jupiter-delivery.viewer.yandex-team.ru with backends jupiter-
    cm.search.yandex.net:8203 and resps grmammaev,shuster added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-26 02:06:42

0.731
---

  * video-html5.viewer.yandex-team.ru with backends
    slovo2.search.yandex.net:9432 and resps rushans,iemelyanov,tolich
    added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-25 14:50:15

0.730
---

  * jupiter2-ro.viewer.yandex-team.ru with backends jupiter-
    cm.search.yandex.net:8304 and resps mkulemin,osol added to viewers-
    available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-25 14:24:48

0.729
---

  * new backed for misspell.viewer

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-24 12:20:30

0.728
---

  * video-yt-urlbase-ultra.viewer.yandex-team.ru with backends
    slovo2.search.yandex.net:9412 and resps rushans,matveieff,tolich
    added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-24 12:16:20

0.727
---

  * video-recommender.viewer.yandex-team.ru with backends
    slovo2.search.yandex.net:9422 and resps rushans,tolich,vvp added to
    viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-24 12:15:14

0.726
---

  * ud-states.viewer.yandex-team.ru with backends
    perun.search.yandex.net:8080 and resps panoff,kaa added to viewers-
    available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-23 16:20:16

0.725
---

  * watch-snippets.viewer.yandex-team.ru with backends
    lya.search.yandex.net:8143 and resps saku,mkulemin added to viewers-
    available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-21 18:53:35

0.724
---

  * backends for grimhold was returned

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-21 14:30:04

0.723
---

  * robot-metrics-services.i-folb.fog.yandex.net -> robot-metrics-services.haze.yandex.net

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-15 13:40:36

0.722
---

  * xya.yandex.ru -> xya.search.yandex.net

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-15 13:29:27

0.721
---

  * another crutch-fix

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-15 13:26:47

0.720
---

  * directpth.viewer.yandex-team.ru with backends
    mfas008.search.yandex.net:80,frauda.search.yandex.net:80 and resps
    cepera,vlegeza added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-14 17:36:58

0.719
---

  * fix for unavailable blackbox

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-14 14:32:11

0.718
---

  * ontodb-clarinet new backends

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-10 15:52:33

0.717
---

  * change backend for switch.v

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-07 19:01:12

0.716
---

  * db-info.viewer.yandex-team.ru with backends gemini-
    dev2.search.yandex.net:80 and resps marvelstas added to viewers-
    available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-07 18:59:24

0.715
---

  * video-freon.viewer.yandex-team.ru with backends
    slovo2.search.yandex.net:9402 and resps rushans,tolich,akaluzhin
    added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-03-07 18:57:09

0.714
---

  * tcyan.viewer.yandex-team.ru with backends
    mfas008.search.yandex.net:80,frauda.search.yandex.net:80 and resps
    ulyanov,anelyubin added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-02-26 14:36:28

0.713
---

  * delete some viewers

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-02-16 18:24:41

0.712
---

  * add idm timeout for gen-waf-acl script

 [Kirill Komlev](https://staff.yandex-team.ru/komnac@yandex-team.ru) 2016-02-15 19:20:35

0.711
---

  * delurl.viewer.yandex-team.ru with backends
    cold1.search.yandex.net:80,cold3.search.yandex.net:80,cold2.search.y
    andex.net:80 and resps cepera,vlegeza added to viewers-available/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-02-12 15:22:36

0.710
---

  * fix typo in gen-waf-acl

 [Kirill Komlev](https://staff.yandex-team.ru/komnac@yandex-team.ru) 2016-02-11 17:59:59

0.709
---

  * https://st.yandex-team.ru/INFRASEARCH-1034

 [Kirill Komlev](https://staff.yandex-team.ru/komnac@yandex-team.ru) 2016-02-11 17:47:29

0.708
---

  * https://st.yandex-team.ru/INFRASEARCH-1019

 [Zhivotnev Vladislav](https://staff.yandex-team.ru/inkvizitor68sl@yandex-team.ru) 2016-02-11 16:25:15

0.707
---

  * viewers -> viewers-available
  * smart check nginx  in postinstall script (#INFRASEARCH-970)

 [Kirill Komlev](https://staff.yandex-team.ru/komnac@yandex-team.ru) 2016-02-10 19:18:34

0.706
---

  * old acl dirs removed

 [Zhivotnev Vladislav](https://staff.yandex-team.ru/inkvizitor68sl@yandex-team.ru) 2016-02-10 16:13:23

0.705
---

  * change backup for oak.viewer

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-02-08 14:20:27

0.704
---

  * fix backends for abies

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-02-02 18:29:40

0.703
---

  * replace gen-viewer-acl.sh and gen-all-viewers.sh to single python script (close: #INFRASEARCH-951)

 [Kirill Komlev](https://staff.yandex-team.ru/komnac@yandex-team.ru) 2016-02-02 16:15:08

0.702
---

  * jupiter2.viewer.yandex-team.ru with backends jupiter-
    cm.search.yandex.net:8303 and resps mkulemin added to viewers/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-02-02 16:11:19

0.701
---

  * jupiter3.viewer.yandex-team.ru with backends jupiter-
    cm.search.yandex.net:8403 and resps mkulemin added to viewers/

 [Andrey Primorskiy](https://staff.yandex-team.ru/rizn@yandex-team.ru) 2016-02-02 16:10:14
 16:10:14

