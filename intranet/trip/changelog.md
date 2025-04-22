0.10.158
--------

* [shigarus](http://staff/shigarus)

 * BTRIP-2848: provider city field

BTRIP-2848: provider city field  [ https://a.yandex-team.ru/arc/commit/9788768 ]

* [d1568](http://staff/d1568)

 * releasing version 0.13  [ https://a.yandex-team.ru/arc/commit/9788688 ]
 * fixed ext-api           [ https://a.yandex-team.ru/arc/commit/9788684 ]
 * releasing version 0.12  [ https://a.yandex-team.ru/arc/commit/9788617 ]

[shigarus](http://staff/shigarus) 2022-07-29 02:12:57+03:00

0.10.157
--------

* [d1568](http://staff/d1568)

 * BTRIP-3164: add check support  [ https://a.yandex-team.ru/arc/commit/9788592 ]

* [birhoff](http://staff/birhoff)

 * BTRIP-3158: Замокать ручку POST /registries/  [ https://a.yandex-team.ru/arc/commit/9785965 ]

[d1568](http://staff/d1568) 2022-07-29 00:09:53+03:00

0.10.156
--------
 * BTRIP-3137: new statuses for employees

\- migration:
  * fix merge downgrade (drop type if it is needed)
  * add field rejected_at
\- src:
  * add EmployeeStatus
  * implement statuses in filter
  * patch middleware + RejectedException
\- test:
  * test_employee_status
  * test_employee_filter
  * test_employee_filter_several_statuses  [ https://a.yandex-team.ru/arc/commit/9785864 ]

[firedebug](http://staff/firedebug) 2022-07-28 15:31:37+03:00

0.10.155
--------

[alexeyshesh](http://staff/alexeyshesh) 2022-07-27 19:11:22+03:00

0.10.154
--------

* [alexeyshesh](http://staff/alexeyshesh)

 * BTRIP-3163: рассчитывать сервисные сборы  [ https://a.yandex-team.ru/arc/commit/9781261 ]

* [d1568](http://staff/d1568)

 * BTRIP-3099: add new client for samsara  [ https://a.yandex-team.ru/arc/commit/9773958 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-27 18:48:42+03:00

0.10.153
--------
 * BTRIP-2984: endpoints for employees

\* endpoints skeleton for employee
\* gateway skeleton for db
\* schemas and models
\* actions skeleton
\* endpoints for employees (https://st.yandex-team.ru/BTRIP-3139)
\* tests 

[ https://a.yandex-team.ru/arc/commit/9772234 ]
[firedebug](http://staff/firedebug) 2022-07-26 13:47:55+03:00

0.10.152
--------
 * BTRIP-3165: log transaction id

BTRIP-3165: log transaction id  [ https://a.yandex-team.ru/arc/commit/9771728 ]

[shigarus](http://staff/shigarus) 2022-07-26 12:48:50+03:00

0.10.151
--------
 * BTRIP-3149 fix aeroclub documents sync  [ https://a.yandex-team.ru/arc/commit/9763467 ]

[terrmit](http://staff/terrmit) 2022-07-24 08:31:48+03:00

0.10.150
--------
 * BTRIP-3148 BTRIP-2603 BTRIP-3149 new documents sync  [ https://a.yandex-team.ru/arc/commit/9762841 ]

[terrmit](http://staff/terrmit) 2022-07-23 20:29:00+03:00

0.10.149
--------
 * BTRIP-3142: fix migration  [ https://a.yandex-team.ru/arc/commit/9761142 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-22 20:59:48+03:00

0.10.148
--------

[alexeyshesh](http://staff/alexeyshesh) 2022-07-22 19:11:46+03:00

0.10.147
--------
 * BTRIP-3142: ya.make fix  [ https://a.yandex-team.ru/arc/commit/9760743 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-22 19:07:23+03:00

0.10.146
--------

[alexeyshesh](http://staff/alexeyshesh) 2022-07-22 18:01:10+03:00

0.10.145
--------

* [hallucinite](http://staff/hallucinite)

 * BTRIP-2769: Научиться создавать групповую заявку  [ https://a.yandex-team.ru/arc/commit/9759987 ]

* [alexeyshesh](http://staff/alexeyshesh)

 * BTRIP-3142: add column is_penalty  [ https://a.yandex-team.ru/arc/commit/9759983 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-22 17:32:58+03:00

0.10.144
--------
 * BTRIP-3168 flag to disable executed pt sync  [ https://a.yandex-team.ru/arc/commit/9756189 ]

[terrmit](http://staff/terrmit) 2022-07-22 01:46:47+03:00

0.10.143
--------
 * BTRIP-3098: add support_id and chat_id to person  [ https://a.yandex-team.ru/arc/commit/9749797 ]

[d1568](http://staff/d1568) 2022-07-20 22:06:20+03:00

0.10.142
--------
 * BTRIP-2603 provider_document_id migration  [ https://a.yandex-team.ru/arc/commit/9749645 ]

[terrmit](http://staff/terrmit) 2022-07-20 21:05:21+03:00

0.10.141
--------
 * BTRIP-2830: ручка баланса клиента  [ https://a.yandex-team.ru/arc/commit/9744935 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-20 10:41:22+03:00

0.10.140
--------
 * BTRIP-2848: migration

BTRIP-2848: migration  [ https://a.yandex-team.ru/arc/commit/9743246 ]

[shigarus](http://staff/shigarus) 2022-07-19 20:22:15+03:00

0.10.139
--------
 * BTRIP-3133: fixed empty flags  [ https://a.yandex-team.ru/arc/commit/9742885 ]

[d1568](http://staff/d1568) 2022-07-19 19:14:52+03:00

0.10.138
--------
 * BTRIP-2787: remove old value in service  [ https://a.yandex-team.ru/arc/commit/9740893 ]

[d1568](http://staff/d1568) 2022-07-19 15:17:16+03:00

0.10.137
--------

* [hallucinite](http://staff/hallucinite)

 * BTRIP-2973: Настроить фильтр по отелям по способу оплаты  [ https://a.yandex-team.ru/arc/commit/9737541 ]

* [d1568](http://staff/d1568)

 * BTRIP-3133: fixed provider search  [ https://a.yandex-team.ru/arc/commit/9737539 ]

[d1568](http://staff/d1568) 2022-07-18 22:24:41+03:00

0.10.136
--------
 * BTRIP-2764: Ручка списка транзакций

BTRIP-2764: списковые ручки транзакций  [ https://a.yandex-team.ru/arc/commit/9737248 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-18 21:07:18+03:00

0.10.135
--------
 * BTRIP-2982: Добавить типы офлайн услуг + BTRIP-2833: таблица депозитов  [ https://a.yandex-team.ru/arc/commit/9735259 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-18 16:17:33+03:00

0.10.134
--------
 * BTRIP-3121  [ https://a.yandex-team.ru/arc/commit/9734769 ]

[d1568](http://staff/d1568) 2022-07-18 15:13:10+03:00

0.10.133
--------
 * BTRIP-3087 person trip approve action  [ https://a.yandex-team.ru/arc/commit/9727850 ]

[terrmit](http://staff/terrmit) 2022-07-15 16:48:26+03:00

0.10.132
--------

[alexeyshesh](http://staff/alexeyshesh) 2022-07-15 16:14:50+03:00

0.10.131
--------
 * BTRIP-2831: Ручка, которая отдает расходы клиента по времени

BTRIP-2831  [ https://a.yandex-team.ru/arc/commit/9727283 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-15 15:42:58+03:00

0.10.130
--------
 * BTRIP-2868: get_person, update_person in PassportPersonalData gateway

   \* fix Passport.Contact api (incorrect documentation): add update for contact (see: https://a.yandex-team.ru/arcadia/mail/search/passport/address/address_proxy/test/java/ru/yandex/passport/ContactsTest.java)
   \* implement get_person and update_person in PassportPersonalData gateway
   \* call pdg.get_person before fill_fio_in_passports  
   [ https://a.yandex-team.ru/arc/commit/9724983 ]

[firedebug](http://staff/firedebug) 2022-07-15 11:36:51+03:00

0.10.129
--------
 * fixed_transfer_filter  [ https://a.yandex-team.ru/arc/commit/9722798 ]

[d1568](http://staff/d1568) 2022-07-14 18:20:42+03:00

0.10.128
--------

* [d1568](http://staff/d1568)

 * BTRIP-2787: first  [ https://a.yandex-team.ru/arc/commit/9714767 ]

* [terrmit](http://staff/terrmit)

 * rebase fix  [ https://a.yandex-team.ru/arc/commit/9714650 ]

[terrmit](http://staff/terrmit) 2022-07-13 14:48:20+03:00

0.10.127
--------

* [terrmit](http://staff/terrmit)

 * BTRIP-3086 person_role approver added  [ https://a.yandex-team.ru/arc/commit/9714478 ]

* [birhoff](http://staff/birhoff)

 * BTRIP-2773: Таблица для хранения мета-данных реестров  [ https://a.yandex-team.ru/arc/commit/9714414 ]

[terrmit](http://staff/terrmit) 2022-07-13 14:19:31+03:00

0.10.126
--------
 * BTRIP-3077: Пофиксить типы в ручках баланса для фронта  [ https://a.yandex-team.ru/arc/commit/9711829 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-12 23:21:23+03:00

0.10.125
--------
 * BTRIP-2132 add_documents and delete_document in aeroclub client  [ https://a.yandex-team.ru/arc/commit/9709021 ]

[terrmit](http://staff/terrmit) 2022-07-12 15:21:00+03:00

0.10.124
--------
 * BTRIP-3031: fix access for manager - add has_manager_perm

\* fix access for manager to partial person data
\* fix unclosed connection in middleware test  [ https://a.yandex-team.ru/arc/commit/9705542 ]

[firedebug](http://staff/firedebug) 2022-07-11 21:43:09+03:00

0.10.123
--------
 * BTRIP-2904: create person endpoint + tests

BTRIP-2904  [ https://a.yandex-team.ru/arc/commit/9703002 ]

[firedebug](http://staff/firedebug) 2022-07-11 15:44:02+03:00

0.10.122
--------
 * BTRIP-2765: CRUD ручки для транзакций  [ https://a.yandex-team.ru/arc/commit/9696969 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-09 00:37:21+03:00

0.10.121
--------
 * BTRIP-3023: fix manager with limited access

BTRIP-3023: fix manager with limited access  [ https://a.yandex-team.ru/arc/commit/9696032 ]

[firedebug](http://staff/firedebug) 2022-07-08 19:20:59+03:00

0.10.120
--------
 * BTRIP-3013: add log_message for PermissionDenied

BTRIP-3013: add log_message for PermissionDenied  [ https://a.yandex-team.ru/arc/commit/9694432 ]

[firedebug](http://staff/firedebug) 2022-07-08 15:53:08+03:00

0.10.119
--------

* [d1568](http://staff/d1568)

 * BTRIP-2939: add order_by to provider search  [ https://a.yandex-team.ru/arc/commit/9690376 ]

* [birhoff](http://staff/birhoff)

 * Подключить S3  [ https://a.yandex-team.ru/arc/commit/9681347 ]

[d1568](http://staff/d1568) 2022-07-07 19:08:27+03:00

0.10.118
--------
 * BTRIP-2907: fix migration

fix migration  [ https://a.yandex-team.ru/arc/commit/9678700 ]

[firedebug](http://staff/firedebug) 2022-07-05 19:59:44+03:00

0.10.117
--------
 * BTRIP-2907: add company domains + migration

\* add domains for company
\* fix tests  [ https://a.yandex-team.ru/arc/commit/9678109 ]

[firedebug](http://staff/firedebug) 2022-07-05 18:31:09+03:00

0.10.116
--------
 * BTRIP-2895: provider make optional  [ https://a.yandex-team.ru/arc/commit/9677509 ]
 * BTRIP-2965: fixed_provider_api      [ https://a.yandex-team.ru/arc/commit/9677391 ]

[d1568](http://staff/d1568) 2022-07-05 17:20:08+03:00

0.10.115
--------
 * BTRIP-2903: change middleware

BTRIP-2903: change middleware  [ https://a.yandex-team.ru/arc/commit/9676552 ]

[firedebug](http://staff/firedebug) 2022-07-05 15:45:26+03:00

0.10.114
--------
 * BTRIP-2903: (migration) add email_confirmed_at to person

BTRIP-2903: (migration) add email_confirmed_at to person  [ https://a.yandex-team.ru/arc/commit/9674708 ]

[firedebug](http://staff/firedebug) 2022-07-05 14:29:10+03:00

0.10.113
--------
 * BTRIP-2763: создать таблицу billing_transaction

BTRIP-2763: создать таблицу billing_transaction  [ https://a.yandex-team.ru/arc/commit/9670964 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-07-04 16:58:49+03:00

0.10.112
--------
 * BTRIP-2675: Рефактор общих ручек поиска  [ https://a.yandex-team.ru/arc/commit/9663743 ]

[hallucinite](http://staff/hallucinite) 2022-07-01 18:50:14+03:00

0.10.111
--------
 * BTRIP-2699: aviacenter cancel, refund, issue

BTRIP-2699: cancel and refund aviacenter  [ https://a.yandex-team.ru/arc/commit/9662436 ]

[shigarus](http://staff/shigarus) 2022-07-01 16:24:55+03:00

0.10.110
--------
 * BTRIP-2354: Получение детализации результата поиска по Авиа  [ https://a.yandex-team.ru/arc/commit/9658109 ]

[hallucinite](http://staff/hallucinite) 2022-06-30 19:03:10+03:00

0.10.109
--------

[alexeyshesh](http://staff/alexeyshesh) 2022-06-28 13:47:10+03:00

0.10.108
--------
 * BTRIP-2844: починить Zora на worker (2)  [ https://a.yandex-team.ru/arc/commit/9643124 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-06-28 12:46:03+03:00

0.10.107
--------
 * BTRIP-2836-fix: fix empty first_name/last_name when creating a contact

BTRIP-2836: fix empty first_name/last_name when creating a contact  [ https://a.yandex-team.ru/arc/commit/9640828 ]

[firedebug](http://staff/firedebug) 2022-06-27 19:46:45+03:00

0.10.106
--------
 * BTRIP-2836: create PersonalDataGateway and refactoring code

BTRIP-2836: create PersonalDataGateway  [ https://a.yandex-team.ru/arc/commit/9638235 ]

[firedebug](http://staff/firedebug) 2022-06-27 14:08:37+03:00

0.10.105
--------

* [d1568](http://staff/d1568)

 * BTRIP-2786: add universal fields service  [ https://a.yandex-team.ru/arc/commit/9637666 ]
 * BTRIP-2546: fixed auth messenger for b2b  [ https://a.yandex-team.ru/arc/commit/9637663 ]

* [firedebug](http://staff/firedebug)

 * BTRIP-2873: add test for has_trip_read_perm

refactoring test permissions; add test for has_trip_read_perm  [ https://a.yandex-team.ru/arc/commit/9637582 ]

[d1568](http://staff/d1568) 2022-06-27 12:59:13+03:00

0.10.104
--------
 * BTRIP-2691: hotel details

BTRIP-2691: hotel details  [ https://a.yandex-team.ru/arc/commit/9636750 ]

[shigarus](http://staff/shigarus) 2022-06-27 10:00:19+03:00

0.10.103
--------
 * BTRIP-2821: Донаписать тесты на все конвертеры  [ https://a.yandex-team.ru/arc/commit/9632252 ]

[hallucinite](http://staff/hallucinite) 2022-06-24 16:39:09+03:00

0.10.102
--------
 * BTRIP-2851 mocked balance api endpoints  [ https://a.yandex-team.ru/arc/commit/9628387 ]

[terrmit](http://staff/terrmit) 2022-06-23 19:48:11+03:00

0.10.101
--------
 * BTRIP-2620: Дополнительная валидация документов  [ https://a.yandex-team.ru/arc/commit/9626446 ]

[birhoff](http://staff/birhoff) 2022-06-23 15:31:34+03:00

0.10.100
--------
 * BTRIP-2644: coordinator for holding

BTRIP-2644: coordinator for holding, refactoring permission check  [ https://a.yandex-team.ru/arc/commit/9622177 ]

[firedebug](http://staff/firedebug) 2022-06-22 18:12:40+03:00

0.10.99
-------

* [terrmit](http://staff/terrmit)

 * BTRIP-2847 fix services authorization  [ https://a.yandex-team.ru/arc/commit/9620330 ]

* [d1568](http://staff/d1568)

 * BTRIP-2805: исправить отправление поля "Действителен до" для загран паспорта  [ https://a.yandex-team.ru/arc/commit/9620271 ]

[d1568](http://staff/d1568) 2022-06-22 14:52:24+03:00

0.10.98
-------

* [alexeyshesh](http://staff/alexeyshesh)

 * BTRIP-2844: fix zora  [ https://a.yandex-team.ru/arc/commit/9619847 ]

* [firedebug](http://staff/firedebug)

 * BTRIP-2815: don't call PermissionDenied if don't need trip verification  [ https://a.yandex-team.ru/arc/commit/9612789 ]

* [terrmit](http://staff/terrmit)

 * releasing version 0.4              [ https://a.yandex-team.ru/arc/commit/9604209 ]
 * fix redis_sentinel_master in prod  [ https://a.yandex-team.ru/arc/commit/9604208 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-06-22 13:31:24+03:00

0.10.97
-------
 * fix rebase 2           [ https://a.yandex-team.ru/arc/commit/9604203 ]

[terrmit](http://staff/terrmit) 2022-06-17 22:42:23+03:00

0.10.96
-------
 * fix rebase  [ https://a.yandex-team.ru/arc/commit/9604161 ]

[terrmit](http://staff/terrmit) 2022-06-17 22:13:30+03:00

0.10.95
-------
 * BTRIP-2768 BTRIP-2781 trip lib and sftp service  [ https://a.yandex-team.ru/arc/commit/9604118 ]

[terrmit](http://staff/terrmit) 2022-06-17 21:49:54+03:00

0.10.94
-------
 * BTRIP-2784: Прийти к единообразной схеме локаций во всех типах услуг  [ https://a.yandex-team.ru/arc/commit/9601826 ]

[hallucinite](http://staff/hallucinite) 2022-06-17 15:26:49+03:00

0.10.93
-------
 * BTRIP-2726: add lib for Passport contact  [ https://a.yandex-team.ru/arc/commit/9599399 ]

[firedebug](http://staff/firedebug) 2022-06-17 09:53:25+03:00

0.10.92
-------
 * BTRIP-2706: подключение к Zora  [ https://a.yandex-team.ru/arc/commit/9597922 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-06-16 19:41:14+03:00

0.10.91
-------
 * BTRIP-2780: [HOTEL] Добавить город в ручку получения объекта поиска  [ https://a.yandex-team.ru/arc/commit/9584410 ]

[hallucinite](http://staff/hallucinite) 2022-06-14 13:49:58+03:00

0.10.90
-------

* [d1568](http://staff/d1568)

 * BTRIP-2418: fixed null in series passport  [ https://a.yandex-team.ru/arc/commit/9578040 ]

* [hallucinite](http://staff/hallucinite)

 * BTRIP-2748:  Добавить поле service_type (тип услуги) в ручки получения результатов поиска  [ https://a.yandex-team.ru/arc/commit/9578019 ]
 * BTRIP-2696: Разобраться с тестами в аркадии                                                [ https://a.yandex-team.ru/arc/commit/9578016 ]

[hallucinite](http://staff/hallucinite) 2022-06-10 18:41:22+03:00

0.10.89
-------
 * BTRIP-2643: [ЖД] Ручка детализации поезда  [ https://a.yandex-team.ru/arc/commit/9571422 ]

[hallucinite](http://staff/hallucinite) 2022-06-09 16:30:41+03:00

0.10.88
-------
 * fix test for BTRIP-2690
   [ https://a.yandex-team.ru/arc/commit/9554870 ]
 
 * BTRIP-2642
   mocked client for passport API  [ https://a.yandex-team.ru/arc/commit/9554102 ]

[firedebug](http://staff/firedebug) 2022-06-06 23:52:25+03:00

0.10.87
-------
 * BTRIP-2690
   set is_yqndex_employee if IS_YA_TEAM  [ https://a.yandex-team.ru/arc/commit/9551498 ]

[firedebug](http://staff/firedebug) 2022-06-06 14:11:06+03:00

0.10.86
-------

[alexeyshesh](http://staff/alexeyshesh) 2022-06-06 12:34:26+03:00

0.10.85
-------
 * BTRIP-2575: Убрать aeroclub_profile_id

tests

BTRIP-2575: Убрать aeroclub_profile_id  [ https://a.yandex-team.ru/arc/commit/9544170 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-06-03 15:12:53+03:00

0.10.84
-------
 * BTRIP-2643: переходим на единообразные ID поездов\самолётов\отелей

\+ тесты теперь `SIZE(MEDIUM)` с таймаутом 10 минут  [ https://a.yandex-team.ru/arc/commit/9534383 ]

[hallucinite](http://staff/hallucinite) 2022-06-01 20:42:22+03:00

0.10.83
-------
 * BTRIP-2559: hotel search support api

BTRIP-2559: hotel search support api  [ https://a.yandex-team.ru/arc/commit/9528279 ]

[shigarus](http://staff/shigarus) 2022-05-31 21:09:09+03:00

0.10.82
-------
 * BTRIP-2641 document refactoring, add external_document_id
   [ https://a.yandex-team.ru/arc/commit/9527303 ]

[firedebug](http://staff/firedebug) 2022-05-31 20:16:42+03:00

0.10.81
-------
 * BTRIP-2601 remove user uid from api  [ https://a.yandex-team.ru/arc/commit/9524701 ]

[terrmit](http://staff/terrmit) 2022-05-31 15:34:19+03:00

0.10.80
-------
 * BTRIP-2673: data field

BTRIP-2673: data field  [ https://a.yandex-team.ru/arc/commit/9521766 ]

[shigarus](http://staff/shigarus) 2022-05-30 19:54:32+03:00

0.10.79
-------
 * BTRIP-2562: hotel filters

BTRIP-2562: hotel filters  [ https://a.yandex-team.ru/arc/commit/9513466 ]

[shigarus](http://staff/shigarus) 2022-05-29 15:57:49+03:00

0.10.78
-------
 * fixed get assignment  [ https://a.yandex-team.ru/arc/commit/9513141 ]

[d1568](http://staff/d1568) 2022-05-27 18:17:16+03:00

0.10.77
-------

* [hallucinite](http://staff/hallucinite)

 * BTRIP-2561: [ЖД] Ручка получения возможных фильтров  [ https://a.yandex-team.ru/arc/commit/9507515 ]

* [firedebug](http://staff/firedebug)

 * fix tests

BTRIP-2586, BTRIP-2558: fix tests  [ https://a.yandex-team.ru/arc/commit/9506523 ]

[hallucinite](http://staff/hallucinite) 2022-05-26 18:53:13+03:00

0.10.76
-------

* [d1568](http://staff/d1568)

 * fixed allowed_documents  [ https://a.yandex-team.ru/arc/commit/9500114 ]

* [hallucinite](http://staff/hallucinite)

 * BTRIP-2560: [ЖД] Ручка получения объекта поиска + ручка статуса + каунтер

Реализация универсальных ручек: 
\**/rail/{search_id}/**
\**/rail/{search_id}/count/**

190 строк -- тесты  [ https://a.yandex-team.ru/arc/commit/9499406 ]

[hallucinite](http://staff/hallucinite) 2022-05-25 16:10:23+03:00

0.10.75
-------
 * BTRIP-2558: hotel search results  [ https://a.yandex-team.ru/arc/commit/9496140 ]

[shigarus](http://staff/shigarus) 2022-05-25 11:11:14+03:00

0.10.74
-------
 * BTRIP-2586: поправить логику отправки 403/404

BTRIP-2586

BTRIP-2586: поправить логику для 403/404  [ https://a.yandex-team.ru/arc/commit/9489243 ]

[alexeyshesh](http://staff/alexeyshesh) 2022-05-23 17:44:33+03:00

0.10.73
-------
 * BTRIP-2557: [ЖД] Ручка списка результатов  [ https://a.yandex-team.ru/arc/commit/9488496 ]

[hallucinite](http://staff/hallucinite) 2022-05-23 16:04:20+03:00

0.10.72
-------
 * BTRIP-2602: field's names to upper; add TYPE_EXPENSES 
   [ https://a.yandex-team.ru/arc/commit/9474924 ]

[firedebug](http://staff/firedebug) 2022-05-19 15:58:07+03:00

0.10.71
-------
 * BTRIP-2572: remove fields from person response; add flags
   [ https://a.yandex-team.ru/arc/commit/9450567 ]

[firedebug](http://staff/firedebug) 2022-05-13 12:55:20+03:00

0.10.70
-------
 * BTRIP-2606 dont reserve avia  [ https://a.yandex-team.ru/arc/commit/9448345 ]

[d1568](http://staff/d1568) 2022-05-12 19:33:05+03:00

0.10.69
-------
 * BTRIP-2595: search person with collate; check lower in test with collation
   add collation and run collate for person fields in search_persons  [ https://a.yandex-team.ru/arc/commit/9445327 ]

[firedebug](http://staff/firedebug) 2022-05-12 12:38:16+03:00

0.10.68
-------
 * suggest only for self
   [ https://a.yandex-team.ru/arc/commit/9427047 ]

[firedebug](http://staff/firedebug) 2022-05-05 10:08:11+03:00

0.10.67
-------
 * BTRIP-2573: move from profile_id to person_id
   [ https://a.yandex-team.ru/arc/commit/9423549 ]

[firedebug](http://staff/firedebug) 2022-05-04 13:57:20+03:00

0.10.66
-------

[terrmit](http://staff/terrmit) 2022-04-29 20:39:38+03:00

0.10.65
-------

* [terrmit](http://staff/terrmit)

 * BTRIP-2587 enable CSRF  [ https://a.yandex-team.ru/arc/commit/9410855 ]

* [d1568](http://staff/d1568)

 * fix_review_flow  [ https://a.yandex-team.ru/arc/commit/9398119 ]

[terrmit](http://staff/terrmit) 2022-04-28 17:18:01+03:00

0.10.64
-------
 * BTRIP-2569 extended scheme for person details and change permission
   - extended the scheme PersonDetails
   - change permissions for details  
 [ https://a.yandex-team.ru/arc/commit/9395971 ]

[firedebug](http://staff/firedebug) 2022-04-25 22:53:25+03:00

0.10.63
-------
 * BTRIP-2545: add is_yandexoid
   - add flag is_yandexoid to meta + test
   - fix get annotations error
   - don't add IPython environment files  
 [ https://a.yandex-team.ru/arc/commit/9395818 ]

[firedebug](http://staff/firedebug) 2022-04-25 21:48:48+03:00

0.10.62
-------

* [firedebug](http://staff/firedebug)
  BTRIP-2565 смена заголовка с X-Real-Ip на X-Forwarded-For-Y  [ https://a.yandex-team.ru/arc/commit/9387741 ]

* [shadchin](http://staff/shadchin)
  Update mock from 3.0.5 to 4.0.3  [ https://a.yandex-team.ru/arc/commit/9387280 ]

[firedebug](http://staff/firedebug) 2022-04-22 18:05:29+03:00

0.10.61
-------
 * BTRIP-2553 changed order of tables  [ https://a.yandex-team.ru/arc/commit/9371688 ]

[terrmit](http://staff/terrmit) 2022-04-19 22:05:47+03:00

0.10.60
-------
 * ipython startup script                [ https://a.yandex-team.ru/arc/commit/9371499 ]
 * BTRIP-2553 remove needless db tables  [ https://a.yandex-team.ru/arc/commit/9371496 ]

[terrmit](http://staff/terrmit) 2022-04-19 21:50:17+03:00

0.10.59
-------
 * BTRIP-2438: aeroclub registry from sftp to yt
   Async sftp upload + periodic job  [ https://a.yandex-team.ru/arc/commit/9369131 ]

[firedebug](http://staff/firedebug) 2022-04-19 17:32:29+03:00

0.10.58
-------
 * dont synk close pt  [ https://a.yandex-team.ru/arc/commit/9368089 ]

[d1568](http://staff/d1568) 2022-04-19 13:20:19+03:00

0.10.57
-------
 * BTRIP-2531: use cyrilic passport only for RU
   [ https://a.yandex-team.ru/arc/commit/9366342 ]

[firedebug](http://staff/firedebug) 2022-04-18 23:48:02+03:00

0.10.56
-------

[d1568](http://staff/d1568) 2022-04-13 16:13:48+03:00

0.10.55
-------
 * BTRIP-2536: fixed create new company  [ https://a.yandex-team.ru/arc/commit/9346079 ]
 * fixed Makefile b2b_prod               [ https://a.yandex-team.ru/arc/commit/9337656 ]

[d1568](http://staff/d1568) 2022-04-13 15:53:28+03:00

0.10.54
-------
 * BTRIP-2477: add fake person  [ https://a.yandex-team.ru/arc/commit/9337582 ]
 * remove devexp                [ https://a.yandex-team.ru/arc/commit/9337581 ]

[d1568](http://staff/d1568) 2022-04-11 22:50:17+03:00

0.10.53
-------
 * BTRIP-2490: xml parser for registry
   [ https://a.yandex-team.ru/arc/commit/9324818 ]

 * BTRIP-2489: add yt registry sample
   [ https://a.yandex-team.ru/arc/commit/9324816 ]

[firedebug](http://staff/firedebug) 2022-04-11 12:18:49+03:00

0.10.52
-------
 * BTRIP-2494: check permissions when get aeroclub profile; add holding check to has_read_perm
 [ https://a.yandex-team.ru/arc/commit/9311574 ]

 * BTRIP-2494 fix-company: add company to select data for person
 [ https://a.yandex-team.ru/arc/commit/9312382 ]

[firedebug](http://staff/firedebug) 2022-04-05 18:57:48+03:00

0.10.51
-------
 * BTRIP-2478: restrict the visibility of users within the same company

   [ https://a.yandex-team.ru/arc/commit/9311256 ]

[firedebug](http://staff/firedebug) 2022-04-05 10:38:33+03:00

0.10.50
-------
 * BTRIP-2501: hide openapi for trip.yandex.ru

   [ https://a.yandex-team.ru/arc/commit/9310349 ]

[firedebug](http://staff/firedebug) 2022-04-05 09:16:39+03:00

0.10.49
-------
 * fix migration

fix migration         [ https://a.yandex-team.ru/arc/commit/9293066 ]

 * BTRIP-2480: add holding

BTRIP-2480  [ https://a.yandex-team.ru/arc/commit/9291535 ]

[firedebug](http://staff/firedebug) 2022-03-30 22:54:09+03:00

0.10.48
-------

* [d1568](http://staff/d1568)

 * releasing version 0.11       [ https://a.yandex-team.ru/arc/commit/9274314 ]
 * BTRIP-2336: add b2b ext api  [ https://a.yandex-team.ru/arc/commit/9274279 ]

* [terrmit](http://staff/terrmit)

 * BTRIP-2453 arq stats endpoint  [ https://a.yandex-team.ru/arc/commit/9274284 ]

[d1568](http://staff/d1568) 2022-03-25 15:53:12+03:00

0.10.47
-------
 * BTRIP-2415 permissions for manager

BTRIP-2415: add check for manager in has_trip_read_perm, has_person_trip_read_perm, has_service_read_perm  [ https://a.yandex-team.ru/arc/commit/9270415 ]

[firedebug](http://staff/firedebug) 2022-03-24 18:01:21+03:00

0.10.46
-------
 * BTRIP-2433: add field is_coordinator to meta

[firedebug](http://staff/firedebug) 2022-03-23 22:47:59+03:00

0.10.45
-------

* [d1568](http://staff/d1568)

 * BTRIP-2335: add b2b auth  [ https://a.yandex-team.ru/arc/commit/9262013 ]

* [maratik](http://staff/maratik)

 * ARCANUM-5460: BTRIP migration  [ https://a.yandex-team.ru/arc/commit/9245109 ]

[d1568](http://staff/d1568) 2022-03-23 00:35:36+03:00

0.10.44
-------
 * BTRIP-2422: add services flags

[firedebug](http://staff/firedebug) 2022-03-17 16:15:59+03:00

0.10.43
-------

* [terrmit](http://staff/terrmit)

 * BTRIP-2407 interconf cancellation reason  [ https://a.yandex-team.ru/arc/commit/9239039 ]

* [dsamuylov](http://staff/dsamuylov)

 * ARCANUM-5510 prepare migration from .devexp.json to a.yaml (intranet)  [ https://a.yandex-team.ru/arc/commit/9231012 ]

[terrmit](http://staff/terrmit) 2022-03-17 11:43:00+03:00

0.10.42
-------
 * BTRIP-2340 Универсальная модель фильтрации

[firedebug](http://staff/firedebug) 2022-03-14 12:42:37+03:00

0.10.41
-------
 * BTRIP-2317: запрет пустой причины отмены заявки

[firedebug](http://staff/firedebug) 2022-03-07 17:38:22+03:00

0.10.40
-------
 * BTRIP-2367: скрываем ручки в зависимости от параметра IS_YA_TEAM

[firedebug](http://staff/firedebug) 2022-03-03 12:56:33+03:00

0.10.39
-------
 * BTRIP-2336 allow external unistat without auth  [ https://a.yandex-team.ru/arc/commit/9195673 ]

[dymov-k](http://staff/dymov-k) 2022-03-02 14:46:38+03:00

0.10.38
-------
 * BTRIP-2336 add external router for monitoring and notifications  [ https://a.yandex-team.ru/arc/commit/9190884 ]

[dymov-k](http://staff/dymov-k) 2022-03-01 12:04:18+03:00

0.10.37
-------
 * BTRIP-2355: add provider create search  [ https://a.yandex-team.ru/arc/commit/9184941 ]

[d1568](http://staff/d1568) 2022-02-26 20:40:10+03:00

0.10.36
-------
 * BTRIP-2334 person suggest from db data  [ https://a.yandex-team.ru/arc/commit/9183512 ]

[terrmit](http://staff/terrmit) 2022-02-25 20:16:02+03:00

0.10.35
-------
 * BTRIP-2314 обработка ответа в клиенте авиа

выделение parse_response в отдельный класс и наследование клиентов для авиа и жд от него

удаление локального скрипта для подключения к виртуалке

Изменение текста отбивки при создании заявки  [ https://a.yandex-team.ru/arc/commit/9179281 ]

 * BTRIP-2366 флаг is_b2b в ручку /api/meta

добавление флага is_b2b в ручку /api/meta  [ https://a.yandex-team.ru/arc/commit/9179279 ]

[firedebug](http://staff/firedebug) 2022-02-24 18:30:22+03:00

0.10.34
-------
 * BTRIP-2395 version and deploy unit to error booster  [ https://a.yandex-team.ru/arc/commit/9178332 ]

[dymov-k](http://staff/dymov-k) 2022-02-24 15:20:42+03:00

0.10.33
-------
 * BTRIP-2339 filter parameters universal endpoint  [ https://a.yandex-team.ru/arc/commit/9173586 ]

[dymov-k](http://staff/dymov-k) 2022-02-22 18:35:21+03:00

0.10.32
-------

* [dymov-k](http://staff/dymov-k)

 * BTRIP-2330 fix csrf vulnerability  [ https://a.yandex-team.ru/arc/commit/9159806 ]

* [firedebug](http://staff/firedebug)

 * удаление ошибочно добавленного скрипта/корректировка описания

удаление локального скрипта для подключения к виртуалке

Изменение текста отбивки при создании заявки  [ https://a.yandex-team.ru/arc/commit/9157432 ]

* [terrmit](http://staff/terrmit)

 * BTRIP-2344 fix  [ https://a.yandex-team.ru/arc/commit/9155113 ]

[dymov-k](http://staff/dymov-k) 2022-02-18 12:04:07+03:00

0.10.31
-------
 * BTRIP-2322: fixed empty fields in middle name  [ https://a.yandex-team.ru/arc/commit/9153668 ]

[d1568](http://staff/d1568) 2022-02-16 22:41:50+03:00

0.10.30
-------
 * BTRIP-2344 avia search filter model + refactoring  [ https://a.yandex-team.ru/arc/commit/9152869 ]

[terrmit](http://staff/terrmit) 2022-02-16 18:57:17+03:00

0.10.29
-------
 * BTRIP-2303: add provider search info and count  [ https://a.yandex-team.ru/arc/commit/9144251 ]

[d1568](http://staff/d1568) 2022-02-15 04:00:54+03:00

0.10.28
-------
 * BTRIP-2167 aviacenter train book  [ https://a.yandex-team.ru/arc/commit/9133969 ]

[terrmit](http://staff/terrmit) 2022-02-11 13:47:43+03:00

0.10.27
-------
 * BTRIP-2183 fix uow dependency call  [ https://a.yandex-team.ru/arc/commit/9130467 ]

[dymov-k](http://staff/dymov-k) 2022-02-10 17:33:59+03:00

0.10.26
-------
 * BTRIP-2183 pyscopg2 in trip  [ https://a.yandex-team.ru/arc/commit/9130114 ]

[dymov-k](http://staff/dymov-k) 2022-02-10 16:23:03+03:00

0.10.25
-------
 * BTRIP-2327 fix get_person_trip_ids call and organization sync  [ https://a.yandex-team.ru/arc/commit/9129262 ]

[dymov-k](http://staff/dymov-k) 2022-02-10 14:52:19+03:00

0.10.24
-------
 * BTRIP-2310: fixed AviaSearchResult  [ https://a.yandex-team.ru/arc/commit/9122599 ]

[d1568](http://staff/d1568) 2022-02-09 01:17:15+03:00

0.10.23
-------
 * BTRIP-2302 person trip update fix  [ https://a.yandex-team.ru/arc/commit/9108768 ]

[terrmit](http://staff/terrmit) 2022-02-04 16:34:44+03:00

0.10.22
-------

* [dymov-k](http://staff/dymov-k)

 * BTRIP-2308 operation_id uniquness test  [ https://a.yandex-team.ru/arc/commit/9107721 ]

* [terrmit](http://staff/terrmit)

 * BTRIP-2265 flag for b2b stand  [ https://a.yandex-team.ru/arc/commit/9107646 ]

[dymov-k](http://staff/dymov-k) 2022-02-04 13:08:18+03:00

0.10.21
-------
 * BTRIP-2170 aviacenter rail search  [ https://a.yandex-team.ru/arc/commit/9105587 ]

[dymov-k](http://staff/dymov-k) 2022-02-03 20:26:13+03:00

0.10.20
-------
 * BTRIP-2168 book hotels  [ https://a.yandex-team.ru/arc/commit/9104314 ]

[terrmit](http://staff/terrmit) 2022-02-03 16:46:51+03:00

0.10.19
-------
 * BTRIP-1927: add new flags for fake service  [ https://a.yandex-team.ru/arc/commit/9100907 ]

[d1568](http://staff/d1568) 2022-02-02 20:29:24+03:00

0.10.18
-------
 * BTRIP-2281: forbid search in close pt  [ https://a.yandex-team.ru/arc/commit/9100837 ]

[d1568](http://staff/d1568) 2022-02-02 20:16:06+03:00

0.10.17
-------
 * BTRIP-2277 hotelName param fix  [ https://a.yandex-team.ru/arc/commit/9095004 ]

[terrmit](http://staff/terrmit) 2022-02-02 02:22:21+03:00

0.10.16
-------
 * BTRIP-2194: add provider avia search results  [ https://a.yandex-team.ru/arc/commit/9091897 ]

[d1568](http://staff/d1568) 2022-02-01 00:42:30+03:00

0.10.15
-------
 * BTRIP-2226 fix person trip partial update  [ https://a.yandex-team.ru/arc/commit/9090571 ]

[terrmit](http://staff/terrmit) 2022-01-31 17:53:39+03:00

0.10.14
-------
 * BTRIP-2277 added hotelFilter_hotelName  [ https://a.yandex-team.ru/arc/commit/9082833 ]

[terrmit](http://staff/terrmit) 2022-01-28 16:44:29+03:00

0.10.13
-------
 * BTRIP-2201 localization for purposes  [ https://a.yandex-team.ru/arc/commit/9069297 ]

[dymov-k](http://staff/dymov-k) 2022-01-25 16:37:07+03:00

0.10.12
-------
 * BTRIP-2191 universal suggest endpoint  [ https://a.yandex-team.ru/arc/commit/9068753 ]

[dymov-k](http://staff/dymov-k) 2022-01-25 15:02:46+03:00

0.10.11
-------
 * BTRIP-2191 provider api structure  [ https://a.yandex-team.ru/arc/commit/9062918 ]

[dymov-k](http://staff/dymov-k) 2022-01-24 11:18:46+03:00

0.10.10
-------
 * fix from_staff endpoint  [ https://a.yandex-team.ru/arc/commit/9059706 ]

[terrmit](http://staff/terrmit) 2022-01-21 23:09:03+03:00

0.10.9
------
 * BTRIP-2192 added provider field  [ https://a.yandex-team.ru/arc/commit/9058440 ]

[terrmit](http://staff/terrmit) 2022-01-21 19:00:55+03:00

0.10.8
------
 * BTRIP-2215 staff pull optimization  [ https://a.yandex-team.ru/arc/commit/9056742 ]

[terrmit](http://staff/terrmit) 2022-01-21 17:17:20+03:00

0.10.7
------
 * aviacenter hotel search endpoint fix  [ https://a.yandex-team.ru/arc/commit/9041531 ]

[terrmit](http://staff/terrmit) 2022-01-17 22:58:28+03:00

0.10.6
------

* [terrmit](http://staff/terrmit)

 * BTRIP-2169 aviacenter client hotel search  [ https://a.yandex-team.ru/arc/commit/9040898 ]

[terrmit](http://staff/terrmit) 2022-01-17 19:15:22+03:00

0.10.5
------
 * fix idm sync for dismissed  [ https://a.yandex-team.ru/arc/commit/9024644 ]

[dymov-k](http://staff/dymov-k) 2022-01-12 18:48:24+03:00

0.10.4
------
 * filter logbroker writing logs  [ https://a.yandex-team.ru/arc/commit/9022287 ]

[dymov-k](http://staff/dymov-k) 2022-01-12 11:34:51+03:00

0.10.3
------
 * BTRIP-2162 BTRIP-2163 aviacenter book and get avia order  [ https://a.yandex-team.ru/arc/commit/9016829 ]

[terrmit](http://staff/terrmit) 2022-01-10 19:52:25+03:00

0.10.2
------
 * BTRIP-2133__documents_soft_delete  [ https://a.yandex-team.ru/arc/commit/8985729 ]

[dymov-k](http://staff/dymov-k) 2021-12-24 16:45:31+03:00

0.10.1
------
 * BTRIP-2151 fix dead threads while sending to errorbooster  [ https://a.yandex-team.ru/arc/commit/8981304 ]

[dymov-k](http://staff/dymov-k) 2021-12-23 16:47:43+03:00

0.10.0
------
 * BTRIP-2024 person trip services  [ https://a.yandex-team.ru/arc/commit/8978606 ]

[terrmit](http://staff/terrmit) 2021-12-23 02:23:24+03:00

0.9.11
------

[d1568](http://staff/d1568) 2021-12-22 23:58:45+03:00

0.9.10
------
BTRIP-1952: create search in aviacentr  [ https://a.yandex-team.ru/arc/commit/8978381 ]

[d1568](http://staff/d1568) 2021-12-22 23:38:41+03:00

0.9.9
-----
 * BTRIP-2096 errorbooster for worker  [ https://a.yandex-team.ru/arc/commit/8967657 ]

[dymov-k](http://staff/dymov-k) 2021-12-20 15:53:50+03:00

0.9.8
-----
 * BTRIP-2091 fix validators  [ https://a.yandex-team.ru/arc/commit/8962008 ]

[dymov-k](http://staff/dymov-k) 2021-12-17 15:38:43+03:00

0.9.7
-----
 * BTRIP-2095 retry when staff returns fallback assignment  [ https://a.yandex-team.ru/arc/commit/8952685 ]

[dymov-k](http://staff/dymov-k) 2021-12-15 14:34:49+03:00

0.9.6
-----
 * fixed await  [ https://a.yandex-team.ru/arc/commit/8952182 ]

[d1568](http://staff/d1568) 2021-12-15 13:19:54+03:00

0.9.5
-----
 * BTRIP-1918 add trip and person ids to log context         [ https://a.yandex-team.ru/arc/commit/8925199 ]
 * BTRIP-2087 required series for russian external passport  [ https://a.yandex-team.ru/arc/commit/8925198 ]
 * BTRIP-2084 travel restrictions proxy endpoint             [ https://a.yandex-team.ru/arc/commit/8925021 ]

[dymov-k](http://staff/dymov-k) 2021-12-10 15:59:24+03:00

0.9.4
-----
 * BTRIP-2033 fix person sync  [ https://a.yandex-team.ru/arc/commit/8924408 ]

[dymov-k](http://staff/dymov-k) 2021-12-10 13:56:00+03:00

0.9.3
-----
 * added migration file into ya.make  [ https://a.yandex-team.ru/arc/commit/8921221 ]

[terrmit](http://staff/terrmit) 2021-12-09 17:12:10+03:00

0.9.2
-----
 * BTRIP-2100 perston trip description into text  [ https://a.yandex-team.ru/arc/commit/8920732 ]

[terrmit](http://staff/terrmit) 2021-12-09 16:20:29+03:00

0.9.1
-----
 * BTRIP-2085 fix offline create notification  [ https://a.yandex-team.ru/arc/commit/8917540 ]

[terrmit](http://staff/terrmit) 2021-12-08 18:59:36+03:00

0.9.0
------
 * BTRIP-2085 belarus offline  [ https://a.yandex-team.ru/arc/commit/8916877 ]

[terrmit](http://staff/terrmit) 2021-12-08 17:00:11+03:00

0.8.42
------
 * BTRIP-2033 increase company name length  [ https://a.yandex-team.ru/arc/commit/8913844 ]

[dymov-k](http://staff/dymov-k) 2021-12-07 20:48:42+03:00

0.8.41
------
 * BTRIP-2033 staffapi organizations sync  [ https://a.yandex-team.ru/arc/commit/8913707 ]

[dymov-k](http://staff/dymov-k) 2021-12-07 20:07:30+03:00

0.8.40
------
 * BTRIP-1971 add prod tvm for logbroker  [ https://a.yandex-team.ru/arc/commit/8902157 ]

[dymov-k](http://staff/dymov-k) 2021-12-03 17:56:04+03:00

0.8.39
------
 * BTRIP-2067: fixed approve triger  [ https://a.yandex-team.ru/arc/commit/8898314 ]

[d1568](http://staff/d1568) 2021-12-02 20:24:42+03:00

0.8.38
------
 * BTRIP-2067: fixed approve triger  [ https://a.yandex-team.ru/arc/commit/8898123 ]

[d1568](http://staff/d1568) 2021-12-02 19:27:42+03:00

0.8.37
------
 * BTRIP-2067: fixed approve triger  [ https://a.yandex-team.ru/arc/commit/8897804 ]

[d1568](http://staff/d1568) 2021-12-02 18:30:21+03:00

0.8.36
------
 * BTRIP-2065: fixed automatic approval  [ https://a.yandex-team.ru/arc/commit/8895845 ]

[d1568](http://staff/d1568) 2021-12-02 13:21:09+03:00

0.8.35
------
 * BTRIP-2053 fix attacments creating in tracker  [ https://a.yandex-team.ru/arc/commit/8893608 ]

[dymov-k](http://staff/dymov-k) 2021-12-01 19:42:54+03:00

0.8.34
------
 * BTRIP-1971 errorbooster for backend  [ https://a.yandex-team.ru/arc/commit/8893148 ]

[dymov-k](http://staff/dymov-k) 2021-12-01 18:13:32+03:00

0.8.33
------

* [dymov-k](http://staff/dymov-k)

 * BTRIP-1334 bump sqlalchemy version  [ https://a.yandex-team.ru/arc/commit/8888560 ]

* [d1568](http://staff/d1568)

 * BTRIP-1953: fixed  [ https://a.yandex-team.ru/arc/commit/8888554 ]

[dymov-k](http://staff/dymov-k) 2021-11-30 17:45:07+03:00

0.8.32
------
 * BTRIP-2047 send need_visa to staff  [ https://a.yandex-team.ru/arc/commit/8883611 ]

[terrmit](http://staff/terrmit) 2021-11-29 17:12:34+03:00

0.8.31
------
 * BTRIP-1973 fix from-staff endpoint  [ https://a.yandex-team.ru/arc/commit/8876762 ]

[terrmit](http://staff/terrmit) 2021-11-26 16:22:43+03:00

0.8.30
------
 * BTRIP-1973 do not try to create ac trip if offline  [ https://a.yandex-team.ru/arc/commit/8876358 ]

[terrmit](http://staff/terrmit) 2021-11-26 15:23:02+03:00

0.8.29
------
 * BTRIP-1973 fix tracker comment  [ https://a.yandex-team.ru/arc/commit/8876152 ]

[terrmit](http://staff/terrmit) 2021-11-26 14:48:31+03:00

0.8.28
------
 * BTRIP-1973 fix template  [ https://a.yandex-team.ru/arc/commit/8876035 ]

[terrmit](http://staff/terrmit) 2021-11-26 14:30:52+03:00

0.8.27
------

[terrmit](http://staff/terrmit) 2021-11-26 13:09:22+03:00

0.8.26
------
 * BTRIP-1973 offline person trips  [ https://a.yandex-team.ru/arc/commit/8875368 ]

[terrmit](http://staff/terrmit) 2021-11-26 12:39:41+03:00

0.8.25
------

[dymov-k](http://staff/dymov-k) 2021-11-25 17:10:42+03:00

0.8.24
------
 * BTRIP-1925 do not fail on services not in ac  [ https://a.yandex-team.ru/arc_vcs/commit/ec9770fbf47026cec5b0a7de982a14f49394456a ]

[dymov-k](http://staff/dymov-k) 2021-11-25 17:02:24+03:00

0.8.23
------
 * BTRIP-1925 process only specified in event service  [ https://a.yandex-team.ru/arc/commit/8870696 ]

[dymov-k](http://staff/dymov-k) 2021-11-25 11:51:54+03:00

0.8.22
------

[d1568](http://staff/d1568) 2021-11-24 19:04:48+03:00

0.8.21
------

* [d1568](http://staff/d1568)

 * BTRIP-1828: add automatic approval to ok  [ https://a.yandex-team.ru/arc/commit/8868744 ]

* [dymov-k](http://staff/dymov-k)

 * releasing version 0.9   [ https://a.yandex-team.ru/arc/commit/8820298 ]
 * BTRIP-1924 ext-api fix  [ https://a.yandex-team.ru/arc/commit/8820139 ]

[d1568](http://staff/d1568) 2021-11-24 18:40:13+03:00

0.8.20
------
 * BTRIP-1924 aeroclub event handler endpoint  [ https://a.yandex-team.ru/arc/commit/8819413 ]

[dymov-k](http://staff/dymov-k) 2021-11-11 13:59:56+03:00

0.8.19
------

* [dymov-k](http://staff/dymov-k)

 * BTRIP-1935 return error to IDM if no person found  [ https://a.yandex-team.ru/arc/commit/8817064 ]

* [d1568](http://staff/d1568)

 * BTRIP-1933: add validation to create document  [ https://a.yandex-team.ru/arc/commit/8817043 ]

[dymov-k](http://staff/dymov-k) 2021-11-10 18:53:08+03:00

0.8.18
------
 * BTRIP-1828: fixed authorization in OK  [ https://a.yandex-team.ru/arc/commit/8815930 ]

[d1568](http://staff/d1568) 2021-11-10 15:37:29+03:00

0.8.17
------
 * BTRIP-1929 add context to exception messages  [ https://a.yandex-team.ru/arc/commit/8815772 ]

[dymov-k](http://staff/dymov-k) 2021-11-10 15:01:55+03:00

0.8.16
------
 * BTRIP-1903 use route dates instead of gap date  [ https://a.yandex-team.ru/arc/commit/8794561 ]

[dymov-k](http://staff/dymov-k) 2021-11-02 14:50:00+03:00

0.8.15
------
 * BTRIP-1835: can delete service  [ https://a.yandex-team.ru/arc/commit/8794282 ]

[d1568](http://staff/d1568) 2021-11-02 13:55:51+03:00

0.8.14
------
 * BTRIP-1878 fix role description  [ https://a.yandex-team.ru/arc/commit/8790294 ]

[dymov-k](http://staff/dymov-k) 2021-11-01 15:03:34+03:00

0.8.13
------
 * BTRIP-1878 add limited access role to idm  [ https://a.yandex-team.ru/arc/commit/8789317 ]

[dymov-k](http://staff/dymov-k) 2021-11-01 12:22:49+03:00

0.8.12
------
 * BTRIP-1827: create ok in trip  [ https://a.yandex-team.ru/arc/commit/8781007 ]
 * flake8 fixed                   [ https://a.yandex-team.ru/arc/commit/8780499 ]

[d1568](http://staff/d1568) 2021-10-28 21:21:13+03:00

0.8.11
------
 * BTRIP-1902: fixed  [ https://a.yandex-team.ru/arc/commit/8776308 ]

[d1568](http://staff/d1568) 2021-10-27 19:25:44+03:00

0.8.10
------
 * BTRIP-1747 trip filter  [ https://a.yandex-team.ru/arc/commit/8775060 ]

[dymov-k](http://staff/dymov-k) 2021-10-27 15:16:54+03:00

0.8.9
-----
 * BTRIP-1747 trip perm  [ https://a.yandex-team.ru/arc/commit/8774804 ]

[dymov-k](http://staff/dymov-k) 2021-10-27 14:29:13+03:00

0.8.8
-----
 * BTRIP-1747 fix permissions  [ https://a.yandex-team.ru/arc/commit/8774441 ]

[dymov-k](http://staff/dymov-k) 2021-10-27 13:25:15+03:00

0.8.7
-----
 * BTRIP-1747 fix validation errors  [ https://a.yandex-team.ru/arc/commit/8774024 ]

[dymov-k](http://staff/dymov-k) 2021-10-27 12:21:03+03:00

0.8.6
-----

* [d1568](http://staff/d1568)

 * BTRIP-1902: improvement  [ https://a.yandex-team.ru/arc/commit/8772731 ]

* [dymov-k](http://staff/dymov-k)

 * BTRIP-1747 add limited access users  [ https://a.yandex-team.ru/arc/commit/8772727 ]

[dymov-k](http://staff/dymov-k) 2021-10-26 23:47:13+03:00

0.8.5
-----

* [dymov-k](http://staff/dymov-k)

 * BTRIP-1887 send photo with text messages  [ https://a.yandex-team.ru/arc/commit/8760504 ]

* [shadchin](http://staff/shadchin)

 * Update httpx from 0.19.0 to 0.20.0  [ https://a.yandex-team.ru/arc/commit/8738466 ]

[dymov-k](http://staff/dymov-k) 2021-10-22 16:07:47+03:00

0.8.4
-----
 * BTRIP-1822 Do not try to create cancelled trips in AC  [ https://a.yandex-team.ru/arc/commit/8737020 ]

[terrmit](http://staff/terrmit) 2021-10-15 10:09:58+03:00

0.8.3
-----
 * BTRIP-1824 added SearchOptionStatus.search_response_error  [ https://a.yandex-team.ru/arc/commit/8729641 ]
 * BTRIP-1526 fix person trip details                         [ https://a.yandex-team.ru/arc/commit/8729639 ]

[dymov-k](http://staff/dymov-k) 2021-10-13 12:18:53+03:00

0.8.2
-----
 * releasing version 0.8.2                 [ https://a.yandex-team.ru/arc/commit/8724707 ]
 * fix staff trip create with route field  [ https://a.yandex-team.ru/arc/commit/8724705 ]

[terrmit](http://staff/terrmit) 2021-10-12 19:24:15+03:00

0.8.1
-----
 * BTRIP-1804 ext-person status added       [ https://a.yandex-team.ru/arc/commit/8724658 ]
 * BTRIP-1802 process failed servces        [ https://a.yandex-team.ru/arc/commit/8724657 ]
 * fix search url after its move to Deploy  [ https://a.yandex-team.ru/arc/commit/8724655 ]

[terrmit](http://staff/terrmit) 2021-10-12 03:09:11+03:00

0.8.0
-----
 * BTRIP-1788 person_trips field in TripCreate  [ https://a.yandex-team.ru/arc/commit/8715699 ]

[terrmit](http://staff/terrmit) 2021-10-08 16:53:55+03:00

0.7.5
-----
 * BTRIP-1526 delete in_progress services before approvement  [ https://a.yandex-team.ru/arc/commit/8712301 ]

[dymov-k](http://staff/dymov-k) 2021-10-07 18:42:28+03:00

0.7.4
-----
 * BTRIP-1799 optional birthday in HubProfile  [ https://a.yandex-team.ru/arc/commit/8707257 ]

[dymov-k](http://staff/dymov-k) 2021-10-06 15:51:12+03:00

0.7.3
-----

 * BTRIP-1739 conf cancellation reason  [ https://a.yandex-team.ru/arc/commit/8691360 ]

[dymov-k](http://staff/dymov-k) 2021-10-01 13:58:22+03:00

0.7.2
-----

* [terrmit](http://staff/terrmit)

 * fixes  [ https://a.yandex-team.ru/arc/commit/8687289 ]

* [dymov-k](http://staff/dymov-k)

 * BTRIP-1736 fix aeroclub city validation for conf  [ https://a.yandex-team.ru/arc/commit/8683728 ]

[terrmit](http://staff/terrmit) 2021-09-30 14:48:27+03:00

0.7.1
-----
 * PR from branch users/terrmit/hub-sync-fix  [ https://a.yandex-team.ru/arc/commit/8680737 ]

[terrmit](http://staff/terrmit) 2021-09-29 02:08:19+03:00

0.7.0
------
 * BTRIP-1547 BTRIP-1548 BTRIP-1549 BTRIP-1550 Ext Person  [ https://a.yandex-team.ru/arc/commit/8680684 ]

[terrmit](http://staff/terrmit) 2021-09-29 01:30:34+03:00

0.6.83
------
 * BTRIP-1736 send last city in route as aeroclub_city_to  [ https://a.yandex-team.ru/arc/commit/8677299 ]

[dymov-k](http://staff/dymov-k) 2021-09-28 12:23:34+03:00

0.6.82
------
 * BTRIP-1724 filter by any destination in trip_list endpoint  [ https://a.yandex-team.ru/arc/commit/8665462 ]

[dymov-k](http://staff/dymov-k) 2021-09-24 12:08:52+03:00

0.6.81
------
 * BTRIP-1735 use complex route in chat start message  [ https://a.yandex-team.ru/arc/commit/8663413 ]

[dymov-k](http://staff/dymov-k) 2021-09-23 19:23:05+03:00

0.6.80
------
 * BTRIP-1721 route in trip_list endpoint  [ https://a.yandex-team.ru/arc/commit/8652118 ]

[dymov-k](http://staff/dymov-k) 2021-09-21 14:54:37+03:00

0.6.79
------
 * BTRIP-1721 complex route - create and edit endpoints  [ https://a.yandex-team.ru/arc/commit/8648804 ]

[dymov-k](http://staff/dymov-k) 2021-09-20 18:39:17+03:00

0.6.78
------
 * BTRIP-1692 complex route - data model  [ https://a.yandex-team.ru/arc/commit/8635817 ]

[dymov-k](http://staff/dymov-k) 2021-09-16 14:06:18+03:00

0.6.77
------
 * BTRIP-1691 fix aeroclub trip creating  [ https://a.yandex-team.ru/arc/commit/8626063 ]

[dymov-k](http://staff/dymov-k) 2021-09-14 14:08:32+03:00

0.6.76
------

* [dymov-k](http://staff/dymov-k)

 * BTRIP-1691 complex route - new data format  [ https://a.yandex-team.ru/arc/commit/8623040 ]

* [d1568](http://staff/d1568)

 * delete_timings_p99_alert  [ https://a.yandex-team.ru/arc/commit/8615510 ]

[dymov-k](http://staff/dymov-k) 2021-09-13 18:24:52+03:00

0.6.75
------
 * BTRIP-1546 ext_person create endpoint  [ https://a.yandex-team.ru/arc/commit/8611303 ]

[dymov-k](http://staff/dymov-k) 2021-09-09 17:00:01+03:00

0.6.74
------
 * BTRIP-1682 add new SearchRequestStatus - SearchResponseError  [ https://a.yandex-team.ru/arc/commit/8609466 ]

[dymov-k](http://staff/dymov-k) 2021-09-09 12:45:27+03:00

0.6.73
------
 * BTRIP-1270 sending cancelled person trips to staff  [ https://a.yandex-team.ru/arc/commit/8600851 ]

[terrmit](http://staff/terrmit) 2021-09-07 13:28:14+03:00

0.6.72
------
 * BTRIP-1636 add pcr flag to meta  [ https://a.yandex-team.ru/arc/commit/8598962 ]

[dymov-k](http://staff/dymov-k) 2021-09-06 21:26:01+03:00

0.6.71
------
 * BTRIP-1635 send services to check before execution  [ https://a.yandex-team.ru/arc/commit/8598282 ]

[dymov-k](http://staff/dymov-k) 2021-09-06 18:41:45+03:00

0.6.70
------
 * BTRIP-1634 allow internal passports  [ https://a.yandex-team.ru/arc/commit/8575666 ]

[dymov-k](http://staff/dymov-k) 2021-08-31 12:36:46+03:00

0.6.69
------
 * BTRIP-1545 external_person data model  [ https://a.yandex-team.ru/arc/commit/8572992 ]

[dymov-k](http://staff/dymov-k) 2021-08-30 17:31:59+03:00

0.6.68
------
 * BTRIP-1612 add Tajikistan citizenship  [ https://a.yandex-team.ru/arc/commit/8557157 ]

[dymov-k](http://staff/dymov-k) 2021-08-25 15:07:18+03:00

0.6.67
------
 * BTRIP-1607 new ServiceState in ac  [ https://a.yandex-team.ru/arc/commit/8543675 ]

[dymov-k](http://staff/dymov-k) 2021-08-20 18:00:20+03:00

0.6.66
------
 * BTRIP-1571 wait for attachment for service  [ https://a.yandex-team.ru/arc/commit/8542359 ]

[dymov-k](http://staff/dymov-k) 2021-08-20 14:00:17+03:00

0.6.65
------
 * BTRIP-1525 fix executor when no places left  [ https://a.yandex-team.ru/arc/commit/8539589 ]

[dymov-k](http://staff/dymov-k) 2021-08-19 18:12:12+03:00

0.6.64
------
 * BTRIP-1597 fix push of ac messages with only attachments to messenger  [ https://a.yandex-team.ru/arc/commit/8538282 ]

[dymov-k](http://staff/dymov-k) 2021-08-19 14:29:16+03:00

0.6.63
------
 * BTRIP-1456 fix get documents  [ https://a.yandex-team.ru/arc/commit/8533630 ]

[dymov-k](http://staff/dymov-k) 2021-08-18 13:34:48+03:00

0.6.62
------
 * BTRIP-1456 restrict name in document to contain only cyrillic or latin characters  [ https://a.yandex-team.ru/arc/commit/8532947 ]

[dymov-k](http://staff/dymov-k) 2021-08-18 11:07:38+03:00

0.6.61
------
 * BTRIP-1520 do not sync birthday from staffapi  [ https://a.yandex-team.ru/arc/commit/8529240 ]
 * BTRIP-1521 disable execution without birthday  [ https://a.yandex-team.ru/arc/commit/8529239 ]

[dymov-k](http://staff/dymov-k) 2021-08-17 12:30:25+03:00

0.6.60
------
 * BTRIP-1504 send files to aeroclub chat  [ https://a.yandex-team.ru/arc/commit/8525088 ]
 * BTRIP-1454 broken conf_details test     [ https://a.yandex-team.ru/arc/commit/8525083 ]

[dymov-k](http://staff/dymov-k) 2021-08-16 12:16:35+03:00

0.6.59
------
 * BTRIP-1514 fix await for restore action  [ https://a.yandex-team.ru/arc/commit/8507130 ]

[dymov-k](http://staff/dymov-k) 2021-08-10 15:50:23+03:00

0.6.58
------
 * BTRIP-1514 fix edit action permissions  [ https://a.yandex-team.ru/arc/commit/8506744 ]

[dymov-k](http://staff/dymov-k) 2021-08-10 14:41:42+03:00

0.6.57
------
 * BTRIP-1495 fix drive activation for unknown org  [ https://a.yandex-team.ru/arc/commit/8493545 ]

[dymov-k](http://staff/dymov-k) 2021-08-05 22:11:55+03:00

0.6.56
------
 * BTRIP-1495 drive integration - activation/deactivation task  [ https://a.yandex-team.ru/arc/commit/8492087 ]

[dymov-k](http://staff/dymov-k) 2021-08-05 16:34:11+03:00

0.6.55
------
 * BTRIP-1420 yet another conf fields fix  [ https://a.yandex-team.ru/arc/commit/8483199 ]

[terrmit](http://staff/terrmit) 2021-08-03 16:23:47+03:00

0.6.54
------
 * BTRIP-1420 BTRIP-1516 conf fields fix  [ https://a.yandex-team.ru/arc/commit/8481881 ]

[terrmit](http://staff/terrmit) 2021-08-03 12:02:32+03:00

0.6.53
------
 * BTRIP-1494 drive integration - client  [ https://a.yandex-team.ru/arc/commit/8470235 ]

[dymov-k](http://staff/dymov-k) 2021-07-29 22:10:26+03:00

0.6.52
------
 * BTRIP-1507 fix create_trip_chats_task  [ https://a.yandex-team.ru/arc/commit/8448658 ]

[dymov-k](http://staff/dymov-k) 2021-07-23 17:29:53+03:00

0.6.51
------
 * BTRIP-1370 fix start message  [ https://a.yandex-team.ru/arc/commit/8448146 ]

[terrmit](http://staff/terrmit) 2021-07-23 15:53:11+03:00

0.6.50
------
 * BTRIP-1370 changed start message in chat  [ https://a.yandex-team.ru/arc/commit/8447855 ]
 * BTRIP-1371 service rejected notification  [ https://a.yandex-team.ru/arc/commit/8447809 ]

[terrmit](http://staff/terrmit) 2021-07-23 15:10:32+03:00

0.6.49
------
 * BTRIP-1493 drive integration - data model  [ https://a.yandex-team.ru/arc/commit/8446773 ]

[dymov-k](http://staff/dymov-k) 2021-07-23 11:34:47+03:00

0.6.48
------
 * BTRIP-1406 join chat for coordinator  [ https://a.yandex-team.ru/arc/commit/8443221 ]

[dymov-k](http://staff/dymov-k) 2021-07-22 13:38:17+03:00

0.6.47
------
 * BTRIP-1484 fix after hypercorn update  [ https://a.yandex-team.ru/arc/commit/8433139 ]

[dymov-k](http://staff/dymov-k) 2021-07-19 19:44:12+03:00

0.6.46
------

* [dymov-k](http://staff/dymov-k)

 * BTRIP-1415 sign message with ac agent name  [ https://a.yandex-team.ru/arc/commit/8432276 ]

* [shadchin](http://staff/shadchin)

 * Update aiopg from 1.2.1 to 1.3.1  [ https://a.yandex-team.ru/arc/commit/8419983 ]

[dymov-k](http://staff/dymov-k) 2021-07-19 16:58:43+03:00

0.6.45
------
 * add internal cordinator perm  [ https://a.yandex-team.ru/arc/commit/8401806 ]

[d1568](http://staff/d1568) 2021-07-09 13:07:09+03:00

0.6.44
------
 * BTRIP-1453 fix trip validation when conf_details is invalid  [ https://a.yandex-team.ru/arc/commit/8389759 ]

[dymov-k](http://staff/dymov-k) 2021-07-08 18:44:01+03:00

0.6.43
------
 * BTRIP-1372 revert seat_number validator  [ https://a.yandex-team.ru/arc/commit/8389172 ]

[dymov-k](http://staff/dymov-k) 2021-07-08 17:08:17+03:00

0.6.42
------
 * BTRIP-1327 close trip endpoints  [ https://a.yandex-team.ru/arc/commit/8384088 ]

[dymov-k](http://staff/dymov-k) 2021-07-07 13:37:20+03:00

0.6.41
------
 * BTRIP-885 use correct country name  [ https://a.yandex-team.ru/arc/commit/8362163 ]

[dymov-k](http://staff/dymov-k) 2021-07-02 18:12:34+03:00

0.6.40
------
 * BTRIP-1414: add validation len str  [ https://a.yandex-team.ru/arc/commit/8361311 ]

[d1568](http://staff/d1568) 2021-07-02 15:16:58+03:00

0.6.39
------
 * BTRIP-1253 ignore document absence for service from ac  [ https://a.yandex-team.ru/arc/commit/8358176 ]

[dymov-k](http://staff/dymov-k) 2021-07-01 16:56:00+03:00

0.6.38
------
 * BTRIP-1313 disable reserve action when seat selected  [ https://a.yandex-team.ru/arc/commit/8349933 ]

[dymov-k](http://staff/dymov-k) 2021-06-29 14:10:56+03:00

0.6.37
------
 * BTRIP-1313 return service id from endpoint  [ https://a.yandex-team.ru/arc/commit/8349493 ]

[dymov-k](http://staff/dymov-k) 2021-06-29 12:14:54+03:00

0.6.36
------
 * BTRIP-1313 save selected place for rail service  [ https://a.yandex-team.ru/arc/commit/8330805 ]

[dymov-k](http://staff/dymov-k) 2021-06-25 11:17:16+03:00

0.6.35
------
 * BTRIP-1226: add action need_warning_on_cancel  [ https://a.yandex-team.ru/arc/commit/8274911 ]

[d1568](http://staff/d1568) 2021-06-17 21:23:14+03:00

0.6.34
------

* [dymov-k](http://staff/dymov-k)

 * BTRIP-1192 notify about no places left  [ https://a.yandex-team.ru/arc/commit/8269708 ]

* [d1568](http://staff/d1568)

 * BTRIP-1274: Начали прокидывать в тикет условие отмены и ссылка на сайт  [ https://a.yandex-team.ru/arc/commit/8269696 ]

[dymov-k](http://staff/dymov-k) 2021-06-16 16:47:38+03:00

0.6.33
------
 * BTRIP-1325 fix create in ac

[dymov-k](http://staff/dymov-k) 2021-06-15 12:09:42+03:00

0.6.32
------
 * BTRIP-1227 hide search service for same city conf  [ https://a.yandex-team.ru/arc/commit/8253603 ]

[dymov-k](http://staff/dymov-k) 2021-06-09 18:37:00+03:00

0.6.31
------
 * BTRIP-1205 locks using SELECT ... FOR UPDATE  [ https://a.yandex-team.ru/arc/commit/8217997 ]

[dymov-k](http://staff/dymov-k) 2021-05-28 15:59:34+03:00

0.6.30
------
 * BTRIP-1245: send mes to ac in task  [ https://a.yandex-team.ru/arc/commit/8211208 ]
 * add flake8 config                   [ https://a.yandex-team.ru/arc/commit/8203617 ]

[d1568](http://staff/d1568) 2021-05-27 21:11:37+03:00

0.6.29
------
 * BTRIP-1209: fixed join in services column  [ https://a.yandex-team.ru/arc/commit/8199809 ]

[d1568](http://staff/d1568) 2021-05-26 14:16:31+03:00

0.6.28
------
 * BTRIP-1209: fixed  [ https://a.yandex-team.ru/arc/commit/8199156 ]

[d1568](http://staff/d1568) 2021-05-26 12:06:07+03:00

0.6.27
------
 * BTRIP-1209: author can change all pt  [ https://a.yandex-team.ru/arc/commit/8197898 ]

[d1568](http://staff/d1568) 2021-05-25 20:53:11+03:00

0.6.26
------
 * BTRIP-1211: add notify about overprice  [ https://a.yandex-team.ru/arc/commit/8193766 ]

[d1568](http://staff/d1568) 2021-05-24 18:25:46+03:00

0.6.25
------
 * BTRIP-1163: add attachments to execution service  [ https://a.yandex-team.ru/arc/commit/8183318 ]

[d1568](http://staff/d1568) 2021-05-20 13:19:35+03:00

0.6.24
------
 * BTRIP-1155 mask passport number for chief  [ https://a.yandex-team.ru/arc/commit/8174366 ]

[dymov-k](http://staff/dymov-k) 2021-05-17 18:16:14+03:00

0.6.23
------
 * BTRIP-1164 hash list and dict arguments for job_id  [ https://a.yandex-team.ru/arc/commit/8169123 ]

[dymov-k](http://staff/dymov-k) 2021-05-14 18:21:02+03:00

0.6.22
------
 * BTRIP-1113: fixed authorize services  [ https://a.yandex-team.ru/arc/commit/8168076 ]
 * BTRIP-1040: add person details        [ https://a.yandex-team.ru/arc/commit/8168067 ]

[d1568](http://staff/d1568) 2021-05-14 14:32:13+03:00

0.6.21
------
 * BTRIP-1061 fix ihub sync with multiple jobs at the same time  [ https://a.yandex-team.ru/arc/commit/8160968 ]

[dymov-k](http://staff/dymov-k) 2021-05-12 13:06:14+03:00

0.6.20
------
 * BTRIP-1076 log ext-api requests       [ https://a.yandex-team.ru/arc/commit/8158597 ]
 * BTRIP-1061 generate job id for tasks  [ https://a.yandex-team.ru/arc/commit/8158573 ]

[dymov-k](http://staff/dymov-k) 2021-05-11 16:14:37+03:00

0.6.19
------
 * BTRIP-939: fix  [ https://a.yandex-team.ru/arc/commit/8133366 ]

[d1568](http://staff/d1568) 2021-05-06 01:42:58+03:00

0.6.18
------
 * BTRIP-939: add file from ac to st

[d1568](http://staff/d1568) 2021-04-30 16:55:18+03:00

0.6.17
------
 * BTRIP-1132: add ByTime to SearchResultsOrdering  [ https://a.yandex-team.ru/arc/commit/8126402 ]

[d1568](http://staff/d1568) 2021-04-30 14:38:04+03:00

0.6.16
------
 * BTRIP-1028: add validatino to passport  [ https://a.yandex-team.ru/arc/commit/8110240 ]

[d1568](http://staff/d1568) 2021-04-26 17:51:26+03:00

0.6.15
------
 * BTRIP-1032 context in arq jobs

[dymov-k](http://staff/dymov-k) 2021-04-26 10:57:56+03:00

0.6.14
------
 * BTRIP-1022: callback create trip in ac after create profile in ihub  [ https://a.yandex-team.ru/arc/commit/8105414 ]

[d1568](http://staff/d1568) 2021-04-23 20:00:20+03:00

0.6.13
------
 * BTRIP-1042, BTRIP-830: fixed add new service  [ https://a.yandex-team.ru/arc/commit/8102778 ]

[d1568](http://staff/d1568) 2021-04-23 16:22:06+03:00

0.6.12
------
 * add job timeout to settings  [ https://a.yandex-team.ru/arc/commit/8102245 ]

[dymov-k](http://staff/dymov-k) 2021-04-23 14:30:24+03:00

0.6.11
------
 * fixed add new service from ac  [ https://a.yandex-team.ru/arc/commit/8102026 ]

[d1568](http://staff/d1568) 2021-04-23 13:28:36+03:00

0.6.10
------

* [d1568](http://staff/d1568)

 * BTRIP-1082: dont change fio profile  [ https://a.yandex-team.ru/arc/commit/8099712 ]
 * add_email_to_ihub                    [ https://a.yandex-team.ru/arc/commit/8096605 ]

* [exprmntr](http://staff/exprmntr)

 * DEVTOOLS-7781 - remove NO_LINT()

DEVTOOLS-7781  [ https://a.yandex-team.ru/arc/commit/8097952 ]

* [v-korovin](http://staff/v-korovin)

 * DEVTOOLS-8344 Migration for intranet

Migration  [ https://a.yandex-team.ru/arc/commit/8095225 ]

[d1568](http://staff/d1568) 2021-04-22 18:15:11+03:00

0.6.9
-----
 * BTRIP-1065 notify about service execution fix  [ https://a.yandex-team.ru/arc/commit/8093238 ]

[terrmit](http://staff/terrmit) 2021-04-20 21:19:14+03:00

0.6.8
-----
 * BTRIP-1025 sync deleted services in AC  [ https://a.yandex-team.ru/arc/commit/8088963 ]

[terrmit](http://staff/terrmit) 2021-04-19 17:57:16+03:00

0.6.7
-----
 * BTRIP-1019__fixed  [ https://a.yandex-team.ru/arc/commit/8083809 ]

[d1568](http://staff/d1568) 2021-04-16 18:23:31+03:00

0.6.6
-----

* [d1568](http://staff/d1568)

 * BTRIP-798 BTRIP-1019 BTRIP-930: fixed notif  [ https://a.yandex-team.ru/arc/commit/8083263 ]

* [shadchin](http://staff/shadchin)

 * CONTRIB-2054 Update httpx from 0.9.3 to 0.10.1  [ https://a.yandex-team.ru/arc/commit/8080897 ]

[d1568](http://staff/d1568) 2021-04-16 16:40:31+03:00

0.6.5
-----
 * do not spam about services execution  [ https://a.yandex-team.ru/arc/commit/8080803 ]

[terrmit](http://staff/terrmit) 2021-04-15 20:49:45+03:00

0.6.4
-----
 * BTRIP-1036 auto_execution_required=true during authorize services  [ https://a.yandex-team.ru/arc/commit/8080298 ]

[terrmit](http://staff/terrmit) 2021-04-15 18:27:37+03:00

0.6.3
-----
 * fix executor for executed person trips  [ https://a.yandex-team.ru/arc/commit/8076940 ]

[terrmit](http://staff/terrmit) 2021-04-14 19:13:59+03:00

0.6.2
-----
 * customproperties fix  [ https://a.yandex-team.ru/arc/commit/8073954 ]

[terrmit](http://staff/terrmit) 2021-04-13 22:16:30+03:00

0.6.1
-----
 * fix execute extra services  [ https://a.yandex-team.ru/arc/commit/8073866 ]

[terrmit](http://staff/terrmit) 2021-04-13 21:30:24+03:00

0.6.0
------
 * BTRIP-820 BTRIP-778 BTRIP-828 execute extra services  [ https://a.yandex-team.ru/arc/commit/8073731 ]

[terrmit](http://staff/terrmit) 2021-04-13 20:34:10+03:00

0.5.26
------
 * BTRIP-908 add operation_id and tags to logging context  [ https://a.yandex-team.ru/arc/commit/8071991 ]
 * BTRIP-972 aeroclub requests execution time              [ https://a.yandex-team.ru/arc/commit/8071942 ]

[dymov-k](http://staff/dymov-k) 2021-04-13 13:45:59+03:00

0.5.25
------
 * fixed sync statuses in staff  [ https://a.yandex-team.ru/arc/commit/8064433 ]

[d1568](http://staff/d1568) 2021-04-09 17:09:40+03:00

0.5.24
------
 * BTRIP-960: fixed city in trip from staff  [ https://a.yandex-team.ru/arc/commit/8061827 ]

[d1568](http://staff/d1568) 2021-04-08 20:30:40+03:00

0.5.23
------
 * BTRIP-929 move expiration time to settings  [ https://a.yandex-team.ru/arc/commit/8061639 ]

[dymov-k](http://staff/dymov-k) 2021-04-08 19:28:41+03:00

0.5.22
------
 * BTRIP-929 fix  [ https://a.yandex-team.ru/arc/commit/8061396 ]

[dymov-k](http://staff/dymov-k) 2021-04-08 18:24:53+03:00

0.5.21
------
 * BTRIP-929 show only 10 results  [ https://a.yandex-team.ru/arc/commit/8061329 ]

[dymov-k](http://staff/dymov-k) 2021-04-08 18:09:51+03:00

0.5.20
------
 * BTRIP-929 city suggest caching  [ https://a.yandex-team.ru/arc/commit/8060932 ]

[dymov-k](http://staff/dymov-k) 2021-04-08 16:53:00+03:00

0.5.19
------
 * BTRIP-949: fixed bonus_card type in Traveller  [ https://a.yandex-team.ru/arc/commit/8060296 ]

[d1568](http://staff/d1568) 2021-04-08 14:47:10+03:00

0.5.18
------
 * BTRIP-937: fixed status in statt trips                                       [ https://a.yandex-team.ru/arc/commit/8059710 ]
 * BTRIP-915: add unistat monitoring                                            [ https://a.yandex-team.ru/arc/commit/8059576 ]
 * BTRIP-931: not change status reserved to in_progress if in ac has servicing  [ https://a.yandex-team.ru/arc/commit/8059575 ]
 * BTRIP-932: add travel exc                                                    [ https://a.yandex-team.ru/arc/commit/8059569 ]

[d1568](http://staff/d1568) 2021-04-08 12:43:22+03:00

0.5.17
------
 * BTRIP-589 squash all migrations and sequential rev id generation  [ https://a.yandex-team.ru/arc/commit/8054432 ]

[dymov-k](http://staff/dymov-k) 2021-04-06 18:38:16+03:00

0.5.16
------

* [d1568](http://staff/d1568)

 * delete List Dict Set Typle  [ https://a.yandex-team.ru/arc/commit/8050397 ]
 * fixed openapi schemas       [ https://a.yandex-team.ru/arc/commit/8050197 ]

* [dymov-k](http://staff/dymov-k)

 * BTRIP-909 deploy migration unit in makefile  [ https://a.yandex-team.ru/arc/commit/8049672 ]

[d1568](http://staff/d1568) 2021-04-05 17:02:03+03:00

0.5.15
------
 * PR from branch users/wlame/BTRIP-770__presentation_topic

BTRIP-770__person_conference_fields  [ https://a.yandex-team.ru/arc/commit/8045709 ]

[wlame](http://staff/wlame) 2021-04-02 19:57:57+03:00

0.5.14
------
 * BTRIP-763 logging context  [ https://a.yandex-team.ru/arc/commit/8045109 ]

[dymov-k](http://staff/dymov-k) 2021-04-02 17:24:23+03:00

0.5.13
------
 * BTRIP-907: dont sync profiles without pt  [ https://a.yandex-team.ru/arc/commit/8044511 ]

[d1568](http://staff/d1568) 2021-04-02 15:15:52+03:00

0.5.12
------

* [dymov-k](http://staff/dymov-k)

 * BTRIP-902 add is_authorized attribute to service api schema  [ https://a.yandex-team.ru/arc/commit/8042305 ]

* [d1568](http://staff/d1568)

 * BTRIP-591: add attributes to blackbox       [ https://a.yandex-team.ru/arc/commit/8042303 ]
 * BTRIP-762: add monitorado conf              [ https://a.yandex-team.ru/arc/commit/8042302 ]
 * BTRIP-904: coordinator can create document  [ https://a.yandex-team.ru/arc/commit/8042296 ]

[d1568](http://staff/d1568) 2021-04-01 20:38:17+03:00

0.5.11
------
 * BTRIP-807 fix traveller id  [ https://a.yandex-team.ru/arc/commit/8041955 ]

[wlame](http://staff/wlame) 2021-04-01 19:00:21+03:00

0.5.10
------
 * BTRIP-807 fix traveller_parameters bonus card  [ https://a.yandex-team.ru/arc/commit/8040404 ]

[wlame](http://staff/wlame) 2021-04-01 13:46:51+03:00

0.5.9
-----
 * BTRIP-807 уточнил тип поля bonus_card_issuer  [ https://a.yandex-team.ru/arc/commit/8038251 ]

[wlame](http://staff/wlame) 2021-03-31 19:16:00+03:00

0.5.8
-----
 * BTRIP-807 Миграция по добавлению ссылки на бонусную карту  [ https://a.yandex-team.ru/arc/commit/8037669 ]

[wlame](http://staff/wlame) 2021-03-31 17:33:45+03:00

0.5.7
-----
 * add logic/tracker.py to ya.make  [ https://a.yandex-team.ru/arc/commit/8036841 ]

[d1568](http://staff/d1568) 2021-03-31 14:24:13+03:00

0.5.6
-----
 * BTRIP-773: add notif about change role  [ https://a.yandex-team.ru/arc/commit/8036448 ]

[d1568](http://staff/d1568) 2021-03-31 13:36:22+03:00

0.5.5
-----
 * BTRIP-781 fix in_progress status updating

BTRIP-781 fix in_progress status updating  [ https://a.yandex-team.ru/arc/commit/8034594 ]

[dymov-k](http://staff/dymov-k) 2021-03-30 19:15:54+03:00

0.5.4
-----

* [dymov-k](http://staff/dymov-k)

 * BTRIP-781 fix reserve action displaying for services

BTRIP-781 fix reserve action displaying for services  [ https://a.yandex-team.ru/arc/commit/8033246 ]

* [glazomer](http://staff/glazomer)

 * fix: возвращаем сваггер на тестинге без аутентификации  [ https://a.yandex-team.ru/arc/commit/8029541 ]

[dymov-k](http://staff/dymov-k) 2021-03-30 14:50:23+03:00

0.5.3
-----
 * fixed_push_to_ihub_bc  [ https://a.yandex-team.ru/arc/commit/7996265 ]

[d1568](http://staff/d1568) 2021-03-25 22:20:47+03:00

0.5.2
-----
 * BTRIP-849: add get_train_details  [ https://a.yandex-team.ru/arc/commit/7995796 ]

[d1568](http://staff/d1568) 2021-03-25 19:55:20+03:00

0.5.1
-----
 * get_executing_person_trip_ids fix  [ https://a.yandex-team.ru/arc/commit/7987777 ]

[terrmit](http://staff/terrmit) 2021-03-23 20:14:17+03:00

0.5.0
------
 * BTRIP-769 Change Person Trip Statuses  [ https://a.yandex-team.ru/arc/commit/7987698 ]

[terrmit](http://staff/terrmit) 2021-03-23 19:56:12+03:00

0.4.23
------
 * BTRIP-831 add name to bonus_cards  [ https://a.yandex-team.ru/arc/commit/7986420 ]

[wlame](http://staff/wlame) 2021-03-23 15:29:57+03:00

0.4.22
------
 * BTRIP-766 hotfix: middle name can be None

BTRIP-766 hotfix: middle name can be None  [ https://a.yandex-team.ru/arc/commit/7983194 ]

[dymov-k](http://staff/dymov-k) 2021-03-22 18:39:47+03:00

0.4.21
------
 * BTRIP-766 hotfix: middle name can be None

BTRIP-766 hotfix: middle name can be None  [ https://a.yandex-team.ru/arc/commit/7982964 ]

[dymov-k](http://staff/dymov-k) 2021-03-22 18:01:38+03:00

0.4.20
------
 * BTRIP-766 full name for aeroclub (with transliteration) (*recreated)

BTRIP-766 full name for aeroclub (with transliteration)  [ https://a.yandex-team.ru/arc/commit/7982629 ]

[dymov-k](http://staff/dymov-k) 2021-03-22 17:09:23+03:00

0.4.19
------
 * BTRIP-829: fixed update_trip_custom_properties  [ https://a.yandex-team.ru/arc/commit/7982327 ]

[d1568](http://staff/d1568) 2021-03-22 16:17:39+03:00

0.4.18
------
 * BTRIP-713 fix service_request values  [ https://a.yandex-team.ru/arc/commit/7979817 ]

[terrmit](http://staff/terrmit) 2021-03-21 17:27:18+03:00

0.4.17
------
 * BTRIP-713 service_request name  [ https://a.yandex-team.ru/arc/commit/7965736 ]

[terrmit](http://staff/terrmit) 2021-03-19 19:33:23+03:00

0.4.16
------
 * BTRIP-823 BTRIP-713 new AC service states  [ https://a.yandex-team.ru/arc/commit/7965445 ]

[terrmit](http://staff/terrmit) 2021-03-19 18:20:14+03:00

0.4.15
------
 * BTRIP-619: add get_airline_info form travel  [ https://a.yandex-team.ru/arc/commit/7964139 ]
 * BTRIP-819: fixed add pt to staff             [ https://a.yandex-team.ru/arc/commit/7964124 ]

[d1568](http://staff/d1568) 2021-03-19 16:00:24+03:00

0.4.14
------
 * BTRIP-797 GZipMiddleware                [ https://a.yandex-team.ru/arc/commit/7958615 ]
 * PR from branch users/terrmit/fix-dns64  [ https://a.yandex-team.ru/arc/commit/7958614 ]

[terrmit](http://staff/terrmit) 2021-03-17 22:55:34+03:00

0.4.13
------
 * BTRIP-760 delete unneeded filter condition

BTRIP-760 delete unneeded filter condition  [ https://a.yandex-team.ru/arc/commit/7957848 ]

[dymov-k](http://staff/dymov-k) 2021-03-17 18:56:43+03:00

0.4.12
------
 * BTRIP-805 do not notify about service cancellation

BTRIP-805 do not notify about service cancellation  [ https://a.yandex-team.ru/arc/commit/7956766 ]
 * BTRIP-760 aeroclub authorization speedup

BTRIP-760 aeroclub authorization speedup                      [ https://a.yandex-team.ru/arc/commit/7956764 ]

[dymov-k](http://staff/dymov-k) 2021-03-17 15:16:18+03:00

0.4.11
------
 * fix document delete  [ https://a.yandex-team.ru/arc/commit/7956546 ]

[terrmit](http://staff/terrmit) 2021-03-17 14:32:27+03:00

0.4.10
------
 * BTRIP-812 not OTHER passports  [ https://a.yandex-team.ru/arc/commit/7956428 ]

[wlame](http://staff/wlame) 2021-03-17 14:07:11+03:00

0.4.9
-----
 * set aeroclub_city_from_id for person_trip  [ https://a.yandex-team.ru/arc/commit/7955881 ]

[terrmit](http://staff/terrmit) 2021-03-17 12:30:02+03:00

0.4.8
-----
 * BTRIP-800 fix xml  [ https://a.yandex-team.ru/arc/commit/7953778 ]

[wlame](http://staff/wlame) 2021-03-16 18:37:37+03:00

0.4.7
-----
 * PR from branch users/wlame/BTRIP-800__push_bonus_cards_to_ihub

BTRIP-800 пушим бонусные карты если они есть.  [ https://a.yandex-team.ru/arc/commit/7953108 ]

[wlame](http://staff/wlame) 2021-03-16 16:32:25+03:00

0.4.6
-----
 * BTRIP-718: add post file to mes  [ https://a.yandex-team.ru/arc/commit/7948784 ]

[d1568](http://staff/d1568) 2021-03-15 15:44:13+03:00

0.4.5
-----

* [wlame](http://staff/wlame)

 * BTRIP-782 bonus_cards gateway + endpoints                    [ https://a.yandex-team.ru/arc/commit/7948651 ]
 * BTRIP-795 пушим в iHUB профилей после обновления паспотров.  [ https://a.yandex-team.ru/arc/commit/7948646 ]

* [smosker](http://staff/smosker)

 * PASSP-31314 Использование tvmauth под капотом

Убираем использование ticket_parser2 из library/tvm2 library/python-django-yauth 
Подробности в https://st.yandex-team.ru/PASSP-31314  [ https://a.yandex-team.ru/arc/commit/7948299 ]

[wlame](http://staff/wlame) 2021-03-15 15:22:05+03:00

0.4.4
-----
 * executor fix 3  [ https://a.yandex-team.ru/arc/commit/7946362 ]

[terrmit](http://staff/terrmit) 2021-03-14 17:14:16+03:00

0.4.3
-----
 * yet another executor fix  [ https://a.yandex-team.ru/arc/commit/7945575 ]

[terrmit](http://staff/terrmit) 2021-03-13 19:08:41+03:00

0.4.2
-----
 * fix executor  [ https://a.yandex-team.ru/arc/commit/7944496 ]

[terrmit](http://staff/terrmit) 2021-03-12 22:12:51+03:00

0.4.1
-----
 * fix executor  [ https://a.yandex-team.ru/arc/commit/7944432 ]
 * fix log       [ https://a.yandex-team.ru/arc/commit/7944276 ]

[terrmit](http://staff/terrmit) 2021-03-12 21:17:57+03:00

0.4.0
------
 * BTRIP-660 aeroclub services pulling  [ https://a.yandex-team.ru/arc/commit/7944177 ]

[terrmit](http://staff/terrmit) 2021-03-12 20:01:05+03:00

0.3.13
------
 * BTRIP-636 хост из переменных окружения  [ https://a.yandex-team.ru/arc/commit/7942490 ]

[wlame](http://staff/wlame) 2021-03-12 15:22:38+03:00

0.3.12
------

[wlame](http://staff/wlame) 2021-03-12 13:15:56+03:00

0.3.11
------
 * BTRIP-636 сам скрипт миграции  [ https://a.yandex-team.ru/arc/commit/7941780 ]

[wlame](http://staff/wlame) 2021-03-12 13:08:54+03:00

0.3.10
------
 * BTRIP-767 избавляемся от вайтлиста в продакшене  [ https://a.yandex-team.ru/arc/commit/7939065 ]

[wlame](http://staff/wlame) 2021-03-11 16:07:55+03:00

0.3.9
-----
 * BTRIP-549: fixed notif to st  [ https://a.yandex-team.ru/arc/commit/7938916 ]

[d1568](http://staff/d1568) 2021-03-11 15:44:15+03:00

0.3.8
-----
 * BTRIP-733 service_provider_suggest  [ https://a.yandex-team.ru/arc/commit/7936021 ]
 * BTRIP-764 исправил тип паспорта     [ https://a.yandex-team.ru/arc/commit/7935162 ]

[wlame](http://staff/wlame) 2021-03-10 19:49:35+03:00

0.3.7
-----
 * BTRIP-730 service_provider_table + migration  [ https://a.yandex-team.ru/arc/commit/7930515 ]

[wlame](http://staff/wlame) 2021-03-10 12:04:16+03:00

0.3.6
-----
 * BTRIP-724 handle text/html responses from AC  [ https://a.yandex-team.ru/arc/commit/7918050 ]

[terrmit](http://staff/terrmit) 2021-03-03 23:45:33+03:00

0.3.5
-----
 * PR from branch users/d1568/BTRIP-721_fixed  [ https://a.yandex-team.ru/arc/commit/7917432 ]

[d1568](http://staff/d1568) 2021-03-03 19:36:12+03:00

0.3.4
-----

* [d1568](http://staff/d1568)

 * BTRIP-721: push diff person to ihub  [ https://a.yandex-team.ru/arc/commit/7916998 ]

* [terrmit](http://staff/terrmit)

 * fix ServicesExecutor

Тут сразу 3 правки:
1. Убрал флаг ENABLE_DEFERRED_DOCUMENT_ADD, потому что фронт выкатился в прод.
2. Подправил check_person_trip, чтобы не спамить ошибки при каждой попытке получить actions услуги.
3. Добавил sleep(1) в периодических тасках, чтобы не было дублей.  [ https://a.yandex-team.ru/arc/commit/7916839 ]

[d1568](http://staff/d1568) 2021-03-03 18:50:07+03:00

0.3.3
-----
 * BTRIP-707 fix authorize_aeroclub_trips_task  [ https://a.yandex-team.ru/arc/commit/7910204 ]

[terrmit](http://staff/terrmit) 2021-03-01 21:28:35+03:00

0.3.2
-----
 * BTRIP-707 add task in list  [ https://a.yandex-team.ru/arc/commit/7910165 ]

[terrmit](http://staff/terrmit) 2021-03-01 21:16:01+03:00

0.3.1
-----
 * BTRIP-707 Authorize trip speed up  [ https://a.yandex-team.ru/arc/commit/7910108 ]

[terrmit](http://staff/terrmit) 2021-03-01 21:00:20+03:00

0.3.0
------
 * UnitOfWork added  [ https://a.yandex-team.ru/arc/commit/7909898 ]

[terrmit](http://staff/terrmit) 2021-03-01 19:55:19+03:00

0.2.21
------
 * Service Executor fix  [ https://a.yandex-team.ru/arc/commit/7909704 ]

[terrmit](http://staff/terrmit) 2021-03-01 19:07:45+03:00

0.2.20
------

* [wlame](http://staff/wlame)

 * BTRIP-636 миграция по добавлению полей в person_document  [ https://a.yandex-team.ru/arc/commit/7908272 ]

* [d1568](http://staff/d1568)

 * BTRIP-631: fixed start mes  [ https://a.yandex-team.ru/arc/commit/7908253 ]

[wlame](http://staff/wlame) 2021-03-01 13:57:28+03:00

0.2.19
------
 * BTRIP-449 BTRIP-571 IDM integration  [ https://a.yandex-team.ru/arc/commit/7904577 ]

[terrmit](http://staff/terrmit) 2021-02-26 21:32:41+03:00

0.2.18
------
 * ENABLE_DEFERRED_DOCUMENT_ADD flag  [ https://a.yandex-team.ru/arc/commit/7901096 ]

[terrmit](http://staff/terrmit) 2021-02-25 21:19:23+03:00

0.2.17
------

* [terrmit](http://staff/terrmit)

 * PR from branch users/terrmit/actions-fix-3

get_service_actions fix

fixes

from_staff endpoint fix  [ https://a.yandex-team.ru/arc/commit/7900787 ]

* [wlame](http://staff/wlame)

 * BTRIP-705 hotfix  [ https://a.yandex-team.ru/arc/commit/7900652 ]

[terrmit](http://staff/terrmit) 2021-02-25 19:41:01+03:00

0.2.16
------

* [terrmit](http://staff/terrmit)

 * change/remove document endpoint             [ https://a.yandex-team.ru/arc/commit/7900554 ]
 * RemoveDocumentAction                        [ https://a.yandex-team.ru/arc/commit/7900319 ]
 * fix actions                                 [ https://a.yandex-team.ru/arc/commit/7900270 ]
 * BTRIP-659 Deferred add document to service  [ https://a.yandex-team.ru/arc/commit/7900190 ]

* [wlame](http://staff/wlame)

 * BTRIP-701 fix await  [ https://a.yandex-team.ru/arc/commit/7900198 ]

[terrmit](http://staff/terrmit) 2021-02-25 18:59:29+03:00

0.2.15
------
 * BTRIP-545 поправки по выясненным правилам в стартреке  [ https://a.yandex-team.ru/arc/commit/7897584 ]

[wlame](http://staff/wlame) 2021-02-24 20:29:17+03:00

0.2.14
------

* [wlame](http://staff/wlame)

 * BTRIP-646 fill FIO in NationalPassport                                                                      [ https://a.yandex-team.ru/arc/commit/7897111 ]
 * PR from branch users/wlame/BTRIP-691__fix_parse_staff_response

Поле оказалось необязательным в данных Стаффа.  [ https://a.yandex-team.ru/arc/commit/7897107 ]

* [d1568](http://staff/d1568)

 * BTRIP-587: add new filters  [ https://a.yandex-team.ru/arc/commit/7897074 ]

[wlame](http://staff/wlame) 2021-02-24 18:32:47+03:00

0.2.13
------
 * BTRIP-588: add create chat_with_coordinator  [ https://a.yandex-team.ru/arc/commit/7867407 ]

[d1568](http://staff/d1568) 2021-02-17 21:19:57+03:00

0.2.12
------
 * fix create aeroclub trip if does not have profile if  [ https://a.yandex-team.ru/arc/commit/7867091 ]

[terrmit](http://staff/terrmit) 2021-02-17 19:58:15+03:00

0.2.11
------
 * BTRIP-661 fix person trip cancel action  [ https://a.yandex-team.ru/arc/commit/7866303 ]

[terrmit](http://staff/terrmit) 2021-02-17 16:55:05+03:00

0.2.10
------
 * fix has_person_trip_read_perm  [ https://a.yandex-team.ru/arc/commit/7865771 ]

[terrmit](http://staff/terrmit) 2021-02-17 15:11:08+03:00

0.2.9
-----
 * fixes  [ https://a.yandex-team.ru/arc/commit/7863757 ]
 * fixes  [ https://a.yandex-team.ru/arc/commit/7863679 ]

[terrmit](http://staff/terrmit) 2021-02-16 21:39:16+03:00

0.2.8
-----
 * PR from branch users/terrmit/actions-fix

actions fixes  [ https://a.yandex-team.ru/arc/commit/7863624 ]

[terrmit](http://staff/terrmit) 2021-02-16 20:47:26+03:00

0.2.7
-----

* [wlame](http://staff/wlame)

 * BTRIP-545 OAuth + approve callback for startrek  [ https://a.yandex-team.ru/arc/commit/7862817 ]

* [terrmit](http://staff/terrmit)

 * refactoring actions  [ https://a.yandex-team.ru/arc/commit/7862663 ]

[wlame](http://staff/wlame) 2021-02-16 17:13:23+03:00

0.2.6
-----
 * BTRIP-623 fix create service  [ https://a.yandex-team.ru/arc/commit/7850708 ]

[terrmit](http://staff/terrmit) 2021-02-11 18:51:50+03:00

0.2.5
-----
 * SearchRequest model fixes  [ https://a.yandex-team.ru/arc/commit/7850319 ]

[terrmit](http://staff/terrmit) 2021-02-11 17:23:12+03:00

0.2.4
-----

* [wlame](http://staff/wlame)

 * BTRIP-597 hotfix has_service_read_perm  [ https://a.yandex-team.ru/arc/commit/7848993 ]

* [terrmit](http://staff/terrmit)

 * add SearchRequest model  [ https://a.yandex-team.ru/arc/commit/7847678 ]

[wlame](http://staff/wlame) 2021-02-11 12:32:08+03:00

0.2.3
-----

* [wlame](http://staff/wlame)

 * BTRIP-597 пробрасываю коннекшон внутрь проверок прав  [ https://a.yandex-team.ru/arc/commit/7847423 ]

* [terrmit](http://staff/terrmit)

 * BTRIP-601 BTRIP-602 new aeroclub proxy endpoints  [ https://a.yandex-team.ru/arc/commit/7847422 ]

[wlame](http://staff/wlame) 2021-02-10 20:50:23+03:00

0.2.2
-----
 * BTRIP-618 get person by uid endpoint  [ https://a.yandex-team.ru/arc/commit/7846896 ]

[terrmit](http://staff/terrmit) 2021-02-10 18:41:02+03:00

0.2.1
-----
 * BTRIP-211 Document.number must be string  [ https://a.yandex-team.ru/arc/commit/7843979 ]

[terrmit](http://staff/terrmit) 2021-02-09 22:19:25+03:00

0.2.0
-------
 * BTRIP-608 handle company without aeroclub ids  [ https://a.yandex-team.ru/arc/commit/7843867 ]

[terrmit](http://staff/terrmit) 2021-02-09 21:45:06+03:00

0.1.152
-------
 * BTRIP-502 use chiefs  [ https://a.yandex-team.ru/arc/commit/7842285 ]

[wlame](http://staff/wlame) 2021-02-09 14:48:40+03:00

0.1.151
-------

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-502__sync_roles2  [ https://a.yandex-team.ru/arc/commit/7840127 ]

* [terrmit](http://staff/terrmit)

 * create profile fix  [ https://a.yandex-team.ru/arc/commit/7840032 ]

[terrmit](http://staff/terrmit) 2021-02-08 20:19:37+03:00

0.1.150
-------
 * BTRIP-594 create AC profile when create person trip
 * BTRIP-595 person trip actions as object
 * aeroclub endpoints db conn saving

[terrmit](http://staff/terrmit) 2021-02-08 17:51:32+03:00

0.1.149
-------
 * get assignment fix  [ https://a.yandex-team.ru/arc/commit/7834365 ]

[terrmit](http://staff/terrmit) 2021-02-05 21:48:54+03:00

0.1.148
-------
 * authorize trip fix  [ https://a.yandex-team.ru/arc/commit/7834226 ]

[terrmit](http://staff/terrmit) 2021-02-05 19:19:04+03:00

0.1.147
-------
 * BTRIP-573 custom property assignment  [ https://a.yandex-team.ru/arc/commit/7833975 ]

[terrmit](http://staff/terrmit) 2021-02-05 18:14:19+03:00

0.1.146
-------

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-502__sync_roles  [ https://a.yandex-team.ru/arc/commit/7833572 ]

* [terrmit](http://staff/terrmit)

 * BTRIP-592 peson gateway clean  [ https://a.yandex-team.ru/arc/commit/7833068 ]
 * person trip actions fix        [ https://a.yandex-team.ru/arc/commit/7832964 ]

[wlame](http://staff/wlame) 2021-02-05 16:44:21+03:00

0.1.145
-------

* [terrmit](http://staff/terrmit)

 * BTRIP-501 faster hub sync when one profile  [ https://a.yandex-team.ru/arc/commit/7831219 ]

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-502__yamake  [ https://a.yandex-team.ru/arc/commit/7831213 ]

[terrmit](http://staff/terrmit) 2021-02-04 21:24:48+03:00

0.1.144
-------
 * PR from branch users/wlame/BTRIP-502__sync_staff_roles  [ https://a.yandex-team.ru/arc/commit/7831133 ]

[wlame](http://staff/wlame) 2021-02-04 20:50:38+03:00

0.1.143
-------
 * fix cron jobs  [ https://a.yandex-team.ru/arc/commit/7830885 ]

[terrmit](http://staff/terrmit) 2021-02-04 19:23:56+03:00

0.1.142
-------
 * cron job fixes  [ https://a.yandex-team.ru/arc/commit/7830707 ]

[terrmit](http://staff/terrmit) 2021-02-04 18:54:24+03:00

0.1.141
-------
 * PR from branch users/wlame/BTRIP-502__sync_staffs  [ https://a.yandex-team.ru/arc/commit/7829198 ]

[wlame](http://staff/wlame) 2021-02-04 13:08:50+03:00

0.1.140
-------
 * person trip cancel fixes  [ https://a.yandex-team.ru/arc/commit/7827596 ]

[terrmit](http://staff/terrmit) 2021-02-03 21:59:16+03:00

0.1.139
-------
 * BTRIP-467 person trip cancel  [ https://a.yandex-team.ru/arc/commit/7826197 ]

[terrmit](http://staff/terrmit) 2021-02-03 15:05:32+03:00

0.1.138
-------
 * BTRIP-574 optional round_trip_departure_on  [ https://a.yandex-team.ru/arc/commit/7818828 ]

[terrmit](http://staff/terrmit) 2021-02-01 14:01:39+03:00

0.1.137
-------

* [d1568](http://staff/d1568)

 * BTRIP-570: fixed validation ac_city_id  [ https://a.yandex-team.ru/arc/commit/7813634 ]
 * releasing version 0.7                   [ https://a.yandex-team.ru/arc/commit/7793594 ]

* [cerevra](http://staff/cerevra)

 * [ticket_parser2/py] Move to deprecated/ (PASSP-27286)

<!-- DEVEXP BEGIN -->
![review](https://codereview.in.yandex-team.ru/badges/review-in_progress-yellow.svg) [![biwboris0](https://codereview.in.yandex-team.ru/badges/biwboris0-...-yellow.svg)](https://staff.yandex-team.ru/biwboris0)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/7799318 ]

[d1568](http://staff/d1568) 2021-01-30 05:13:08+03:00

0.1.136
-------

* [d1568](http://staff/d1568)

 * BTRIP-540: fixed type price  [ https://a.yandex-team.ru/arc/commit/7793572 ]

* [terrmit](http://staff/terrmit)

 * some fixes  [ https://a.yandex-team.ru/arc/commit/7793556 ]

[d1568](http://staff/d1568) 2021-01-29 02:07:57+03:00

0.1.135
-------
 * BTRIP-317 custom properties  [ https://a.yandex-team.ru/arc/commit/7793069 ]

[terrmit](http://staff/terrmit) 2021-01-28 20:40:07+03:00

0.1.134
-------
 * BTRIP-503: add get person  [ https://a.yandex-team.ru/arc/commit/7787527 ]

[d1568](http://staff/d1568) 2021-01-28 13:52:07+03:00

0.1.133
-------
 * BTRIP-553: fixed                                 [ https://a.yandex-team.ru/arc/commit/7784822 ]
 * BTRIP-553: add is_dismissed and email by person  [ https://a.yandex-team.ru/arc/commit/7784689 ]

[d1568](http://staff/d1568) 2021-01-27 16:28:37+03:00

0.1.132
-------
 * BTRIP-495: add filters to trips                       [ https://a.yandex-team.ru/arc/commit/7782828 ]
 * BTRIP-471: add validator to issued_on and expires_on  [ https://a.yandex-team.ru/arc/commit/7782827 ]

[d1568](http://staff/d1568) 2021-01-27 00:51:02+03:00

0.1.131
-------
 * added missed task  [ https://a.yandex-team.ru/arc/commit/7782396 ]

[terrmit](http://staff/terrmit) 2021-01-26 20:25:22+03:00

0.1.130
-------
 * BTRIP-477 fixes  [ https://a.yandex-team.ru/arc/commit/7781565 ]

[terrmit](http://staff/terrmit) 2021-01-26 17:17:59+03:00

0.1.129
-------
 * BTRIP-477 notifications in tracker issues  [ https://a.yandex-team.ru/arc/commit/7778967 ]

[terrmit](http://staff/terrmit) 2021-01-25 21:04:39+03:00

0.1.128
-------
 * BTRIP-500: create search for robot  [ https://a.yandex-team.ru/arc/commit/7773886 ]

[d1568](http://staff/d1568) 2021-01-23 01:50:45+03:00

0.1.127
-------
 * BTRIP-498: check perm for trips  [ https://a.yandex-team.ru/arc/commit/7773234 ]

[d1568](http://staff/d1568) 2021-01-22 16:39:05+03:00

0.1.126
-------
 * releasing version 0.6           [ https://a.yandex-team.ru/arc/commit/7769056 ]
 * fixed aeroclub_last_message_id  [ https://a.yandex-team.ru/arc/commit/7769027 ]

[d1568](http://staff/d1568) 2021-01-21 14:19:46+03:00

0.1.125
-------
 * custom property type  [ https://a.yandex-team.ru/arc/commit/7765544 ]

[terrmit](http://staff/terrmit) 2021-01-20 13:28:40+03:00

0.1.124
-------
 * BTRIP-451: add new conf param to staff  [ https://a.yandex-team.ru/arc/commit/7763991 ]
 * BTRIP-386: add perm to service          [ https://a.yandex-team.ru/arc/commit/7763984 ]

[d1568](http://staff/d1568) 2021-01-19 19:41:30+03:00

0.1.123
-------
 * BTRIP-491 dynamic custom properties  [ https://a.yandex-team.ru/arc/commit/7763184 ]

[terrmit](http://staff/terrmit) 2021-01-19 16:17:41+03:00

0.1.122
-------
 * fix redis sentinel conf in prod  [ https://a.yandex-team.ru/arc/commit/7761006 ]

[terrmit](http://staff/terrmit) 2021-01-18 21:08:00+03:00

0.1.121
-------

* [terrmit](http://staff/terrmit)

 * custom properties fix  [ https://a.yandex-team.ru/arc/commit/7758879 ]

* [shadchin](http://staff/shadchin)

 * IGNIETFERRO-1618,IGNIETFERRO-1621,IGNIETFERRO-1624 Fix flake8 checks  [ https://a.yandex-team.ru/arc/commit/7758752 ]

[terrmit](http://staff/terrmit) 2021-01-18 19:13:17+03:00

0.1.120
-------
 * company model fix  [ https://a.yandex-team.ru/arc/commit/7757636 ]

[terrmit](http://staff/terrmit) 2021-01-18 14:19:21+03:00

0.1.119
-------
 * BTRIP-483 several companies support  [ https://a.yandex-team.ru/arc/commit/7757389 ]

[terrmit](http://staff/terrmit) 2021-01-18 13:41:25+03:00

0.1.118
-------
 * BTRIP-441 Fix profile_id in aeroclub api requests  [ https://a.yandex-team.ru/arc/commit/7754213 ]

[terrmit](http://staff/terrmit) 2021-01-15 19:30:33+03:00

0.1.117
-------
 * BTRIP-478 add hypercorn config  [ https://a.yandex-team.ru/arc/commit/7750486 ]
 * change person_id values         [ https://a.yandex-team.ru/arc/commit/7750409 ]
 * BTRIP-478 white list of logins  [ https://a.yandex-team.ru/arc/commit/7750159 ]

[terrmit](http://staff/terrmit) 2021-01-14 15:52:31+03:00

0.1.116
-------
 * fixed_send_mess_to_aeroclub           [ https://a.yandex-team.ru/arc/commit/7728541 ]
 * BTRIP-453: add flag to skip aapprove  [ https://a.yandex-team.ru/arc/commit/7728354 ]

[d1568](http://staff/d1568) 2020-12-29 21:59:57+03:00

0.1.115
-------
 * BTRIP-455: send mes to aeroclub  [ https://a.yandex-team.ru/arc/commit/7725837 ]

[d1568](http://staff/d1568) 2020-12-29 15:18:07+03:00

0.1.114
-------
 * fix is_allowed_clients  [ https://a.yandex-team.ru/arc/commit/7724558 ]
 * releasing version 0.5   [ https://a.yandex-team.ru/arc/commit/7724472 ]

[d1568](http://staff/d1568) 2020-12-28 20:15:41+03:00

0.1.113
-------
 * BTRIP-465: fixed ext-api api  [ https://a.yandex-team.ru/arc/commit/7724451 ]

[d1568](http://staff/d1568) 2020-12-28 19:42:09+03:00

0.1.112
-------
 * BTRIP-453: get is_approved from staff  [ https://a.yandex-team.ru/arc/commit/7713245 ]

[d1568](http://staff/d1568) 2020-12-23 19:23:11+03:00

0.1.111
-------
 * PR from branch users/d1568/BTRIP-452__add_create_default_pcd

fixed test

BTRIP-452: add create default pcd  [ https://a.yandex-team.ru/arc/commit/7711796 ]

[d1568](http://staff/d1568) 2020-12-23 14:11:02+03:00

0.1.110
-------
 * fixed  [ https://a.yandex-team.ru/arc/commit/7710035 ]
 * fixed  [ https://a.yandex-team.ru/arc/commit/7708874 ]

[d1568](http://staff/d1568) 2020-12-22 19:49:27+03:00

0.1.109
-------
 * fixed  [ https://a.yandex-team.ru/arc/commit/7706027 ]

[d1568](http://staff/d1568) 2020-12-21 16:43:00+03:00

0.1.108
-------
 * cron fix                    [ https://a.yandex-team.ru/arc/commit/7679427 ]
 * add aeroclub accept header  [ https://a.yandex-team.ru/arc/commit/7679426 ]

[terrmit](http://staff/terrmit) 2020-12-17 15:24:52+03:00

0.1.107
-------
 * fix periodic tasks  [ https://a.yandex-team.ru/arc/commit/7674568 ]

[terrmit](http://staff/terrmit) 2020-12-15 20:54:19+03:00

0.1.106
-------
 * BTRIP-436 BTRIP-438 reserve service and periodic execute  [ https://a.yandex-team.ru/arc/commit/7671517 ]

[terrmit](http://staff/terrmit) 2020-12-14 22:22:31+03:00

0.1.105
-------
 * fixed and test  [ https://a.yandex-team.ru/arc/commit/7671313 ]

[d1568](http://staff/d1568) 2020-12-14 21:01:31+03:00

0.1.104
-------

* [d1568](http://staff/d1568)

 * BTRIP-377: add conf fields  [ https://a.yandex-team.ru/arc/commit/7670720 ]

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-431__fix_params  [ https://a.yandex-team.ru/arc/commit/7670427 ]

[d1568](http://staff/d1568) 2020-12-14 18:12:00+03:00

0.1.103
-------

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-443__add_aeroclub_profile_id_to_user  [ https://a.yandex-team.ru/arc/commit/7669659 ]

* [terrmit](http://staff/terrmit)

 * fix seats endpoint  [ https://a.yandex-team.ru/arc/commit/7669514 ]

* [d1568](http://staff/d1568)

 * releasing version 0.4  [ https://a.yandex-team.ru/arc/commit/7663559 ]

[wlame](http://staff/wlame) 2020-12-14 14:11:35+03:00

0.1.102
-------
 * fixed_docker_ext_api  [ https://a.yandex-team.ru/arc/commit/7663535 ]

[d1568](http://staff/d1568) 2020-12-11 15:31:29+03:00

0.1.101
-------
 * service model change  [ https://a.yandex-team.ru/arc/commit/7662953 ]

[terrmit](http://staff/terrmit) 2020-12-11 13:42:37+03:00

0.1.100
-------

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-431__do_not_send_empty_values  [ https://a.yandex-team.ru/arc/commit/7662706 ]

* [d1568](http://staff/d1568)

 * releasing version 0.3  [ https://a.yandex-team.ru/arc/commit/7662449 ]

[wlame](http://staff/wlame) 2020-12-11 12:29:48+03:00

0.1.99
------
 * PR from branch users/wlame/BTRIP-431__multivalues_in_filters  [ https://a.yandex-team.ru/arc/commit/7660354 ]

[wlame](http://staff/wlame) 2020-12-10 17:17:10+03:00

0.1.98
------
 * arq fix  [ https://a.yandex-team.ru/arc/commit/7657711 ]

[terrmit](http://staff/terrmit) 2020-12-09 20:18:40+03:00

0.1.97
------

* [terrmit](http://staff/terrmit)

 * mock redis in tests    [ https://a.yandex-team.ru/arc/commit/7657632 ]
 * BTRIP-403 arq support  [ https://a.yandex-team.ru/arc/commit/7657532 ]

[terrmit](http://staff/terrmit) 2020-12-09 19:53:14+03:00

0.1.96
------
 * fixed aeroclub_service_seats  [ https://a.yandex-team.ru/arc/commit/7654919 ]

[d1568](http://staff/d1568) 2020-12-09 03:53:53+03:00

0.1.95
------
 * BTRIP-375 free seats endpoint       [ https://a.yandex-team.ru/arc/commit/7652955 ]
 * BTRIP-433 return created_at in api  [ https://a.yandex-team.ru/arc/commit/7652946 ]

[terrmit](http://staff/terrmit) 2020-12-08 20:07:30+03:00

0.1.94
------

[wlame](http://staff/wlame) 2020-12-08 15:31:00+03:00

0.1.93
------
 * PR from branch users/wlame/BTRIP-392__fux_typo  [ https://a.yandex-team.ru/arc/commit/7652751 ]

[wlame](http://staff/wlame) 2020-12-08 15:06:04+03:00

0.1.92
------
 * PR from branch users/wlame/BTRIP-392__add_logging_to_sync  [ https://a.yandex-team.ru/arc/commit/7652114 ]

[wlame](http://staff/wlame) 2020-12-08 13:28:09+03:00

0.1.91
------
 * fixed_aeroclub_get_session  [ https://a.yandex-team.ru/arc/commit/7649861 ]

[d1568](http://staff/d1568) 2020-12-07 17:37:34+03:00

0.1.90
------
 * PR from branch users/wlame/BTRIP-392__sync_documents_to_hub  [ https://a.yandex-team.ru/arc/commit/7649841 ]

[wlame](http://staff/wlame) 2020-12-07 17:34:46+03:00

0.1.89
------
 * BTRIP-429:  add timeout


0.1.88
------
 * PR from branch users/wlame/BTRIP-392__sync_documents_to_hub_fix  [ https://a.yandex-team.ru/arc/commit/7648684 ]

[wlame](http://staff/wlame) 2020-12-07 13:19:04+03:00

0.1.87
------
 * BTRIP-429: fixed create ticket for conf  [ https://a.yandex-team.ru/arc/commit/7643531 ]

[d1568](http://staff/d1568) 2020-12-04 13:58:06+03:00

0.1.86
------

* [terrmit](http://staff/terrmit)

 * BTRIP-435 faster tests  [ https://a.yandex-team.ru/arc/commit/7641097 ]

* [hhell](http://staff/hhell)

 * sqlalchemy-1.3 in all datalens/backend  [ https://a.yandex-team.ru/arc/commit/7640847 ]

* [d1568](http://staff/d1568)

 * BTRIP-429: fixed create ticket  [ https://a.yandex-team.ru/arc/commit/7640745 ]

[d1568](http://staff/d1568) 2020-12-04 03:07:42+03:00

0.1.85
------
 * PR from branch users/wlame/BTRIP-420__small_fixes  [ https://a.yandex-team.ru/arc/commit/7640281 ]

[wlame](http://staff/wlame) 2020-12-03 10:32:31+03:00

0.1.84
------
 * PR from branch users/wlame/BTRIP-325__ihub_profiles_sync

Таска, которая пушит профили сотрудников, по которым есть хоть одна командировка в Hub, и после синка получает profile_id и сохраняет его в поле aeroclub_profile_id.  [ https://a.yandex-team.ru/arc/commit/7639224 ]

[wlame](http://staff/wlame) 2020-12-02 22:00:30+03:00

0.1.83
------

* [d1568](http://staff/d1568)

 * BTRIP-404: add default purposes for pt  [ https://a.yandex-team.ru/arc/commit/7639056 ]

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-329__one_more_fix  [ https://a.yandex-team.ru/arc/commit/7637380 ]

* [hhell](http://staff/hhell)

 * CONTRIB-2042: contrib/python/sqlalchemy -> contrib/python/sqlalchemy/sqlalchemy-1.2

<!-- DEVEXP BEGIN -->
![review](https://codereview.in.yandex-team.ru/badges/review-in_progress-yellow.svg) [![inngonch](https://codereview.in.yandex-team.ru/badges/inngonch-...-yellow.svg)](https://staff.yandex-team.ru/inngonch)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/7633357 ]

[d1568](http://staff/d1568) 2020-12-02 20:13:36+03:00

0.1.82
------

* [terrmit](http://staff/terrmit)

 * added search_option_result_list endpoint  [ https://a.yandex-team.ru/arc/commit/7632410 ]

* [shadchin](http://staff/shadchin)

 * Fix flake8 checks  [ https://a.yandex-team.ru/arc/commit/7630438 ]

[terrmit](http://staff/terrmit) 2020-11-30 21:56:33+03:00

0.1.81
------
 * PR from branch users/wlame/BTRIP-325__ihub_profiles_sync_add_profileid  [ https://a.yandex-team.ru/arc/commit/7618917 ]

[wlame](http://staff/wlame) 2020-11-25 13:54:44+03:00

0.1.80
------
 * BTRIP-383: add push mes from aeroclub  [ https://a.yandex-team.ru/arc/commit/7617185 ]

[d1568](http://staff/d1568) 2020-11-24 19:51:44+03:00

0.1.79
------
 * PR from branch users/wlame/BTRIP-329__profile_staff_sync_fix  [ https://a.yandex-team.ru/arc/commit/7616389 ]

[wlame](http://staff/wlame) 2020-11-24 16:19:06+03:00

0.1.78
------
 * BTRIP-387 BTRIP-393 Ручки для получения/добавления документов в услугу  [ https://a.yandex-team.ru/arc/commit/7616337 ]

[terrmit](http://staff/terrmit) 2020-11-24 16:16:01+03:00

0.1.77
------
 * PR from branch users/wlame/BTRIP-329__profile_staff_sync  [ https://a.yandex-team.ru/arc/commit/7615795 ]

[wlame](http://staff/wlame) 2020-11-24 14:05:31+03:00

0.1.76
------
 * create person fix  [ https://a.yandex-team.ru/arc/commit/7613407 ]

[terrmit](http://staff/terrmit) 2020-11-23 18:56:17+03:00

0.1.75
------
 * BTRIP-376 auth middleware fix           [ https://a.yandex-team.ru/arc/commit/7601693 ]
 * BTRIP-330 return aeroclub error in api  [ https://a.yandex-team.ru/arc/commit/7601692 ]

[terrmit](http://staff/terrmit) 2020-11-23 01:06:47+03:00

0.1.74
------

* [terrmit](http://staff/terrmit)

 * BTRIP-358 openapi improvements  [ https://a.yandex-team.ru/arc/commit/7599657 ]

[terrmit](http://staff/terrmit) 2020-11-20 12:42:35+03:00

0.1.73
------
 * remove aeroclub restrictions  [ https://a.yandex-team.ru/arc/commit/7589678 ]

[terrmit](http://staff/terrmit) 2020-11-17 11:48:36+03:00

0.1.72
------
 * fix check aeroclub rules  [ https://a.yandex-team.ru/arc/commit/7587950 ]

[terrmit](http://staff/terrmit) 2020-11-16 17:54:35+03:00

0.1.71
------
 * add traveller fix  [ https://a.yandex-team.ru/arc/commit/7587706 ]

[terrmit](http://staff/terrmit) 2020-11-16 17:16:15+03:00

0.1.70
------
 * execute all services           [ https://a.yandex-team.ru/arc/commit/7585700 ]
 * aeroclub service document fix  [ https://a.yandex-team.ru/arc/commit/7585697 ]

[terrmit](http://staff/terrmit) 2020-11-15 23:19:24+03:00

0.1.69
------
 * aeroclub service model fix  [ https://a.yandex-team.ru/arc/commit/7585689 ]

[terrmit](http://staff/terrmit) 2020-11-15 22:56:50+03:00

0.1.68
------
 * service status fix  [ https://a.yandex-team.ru/arc/commit/7585381 ]

[terrmit](http://staff/terrmit) 2020-11-15 15:36:26+03:00

0.1.67
------
 * BTRIP-360 execute services  [ https://a.yandex-team.ru/arc/commit/7585346 ]

[terrmit](http://staff/terrmit) 2020-11-15 14:58:33+03:00

0.1.66
------
 * fixed temp mes  [ https://a.yandex-team.ru/arc/commit/7582573 ]

[d1568](http://staff/d1568) 2020-11-13 18:52:04+03:00

0.1.65
------

* [d1568](http://staff/d1568)

 * BTRIP-367: fixed sync staff trip  [ https://a.yandex-team.ru/arc/commit/7576346 ]

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-312__permissions_check  [ https://a.yandex-team.ru/arc/commit/7576247 ]

[d1568](http://staff/d1568) 2020-11-11 19:48:17+03:00

0.1.64
------
 * fixed sync staff  [ https://a.yandex-team.ru/arc/commit/7571704 ]

[d1568](http://staff/d1568) 2020-11-10 14:12:33+03:00

0.1.63
------
 * BTRIP-361: send start mes  [ https://a.yandex-team.ru/arc/commit/7570045 ]

[d1568](http://staff/d1568) 2020-11-09 22:30:58+03:00

0.1.62
------
 * services fix  [ https://a.yandex-team.ru/arc/commit/7544224 ]

[terrmit](http://staff/terrmit) 2020-11-03 19:04:49+03:00

0.1.61
------
 * BTRIP-344 create aeroclub trips when create group trip  [ https://a.yandex-team.ru/arc/commit/7541496 ]
 * fix search filters                                      [ https://a.yandex-team.ru/arc/commit/7541460 ]

[terrmit](http://staff/terrmit) 2020-11-02 21:50:39+03:00

0.1.60
------
 * BTRIP-162: create chat for pt  [ https://a.yandex-team.ru/arc/commit/7536593 ]

[d1568](http://staff/d1568) 2020-10-30 22:29:20+03:00

0.1.59
------
 * PR from branch users/terrmit/small-fixes  [ https://a.yandex-team.ru/arc/commit/7536514 ]

[terrmit](http://staff/terrmit) 2020-10-30 21:38:46+03:00

0.1.58
------
 * fix tests                                        [ https://a.yandex-team.ru/arc/commit/7535979 ]
 * BTRIP-307 BTRIP-326 BTRIP-337 services workflow  [ https://a.yandex-team.ru/arc/commit/7529101 ]

[terrmit](http://staff/terrmit) 2020-10-30 18:34:35+03:00

0.1.57
------
 * PR from branch users/wlame/BTRIP-311__is_coordinator  [ https://a.yandex-team.ru/arc/commit/7486024 ]

[wlame](http://staff/wlame) 2020-10-22 13:12:54+03:00

0.1.56
------
 * PR from branch users/wlame/BTRIP-311__is_coordinator  [ https://a.yandex-team.ru/arc/commit/7485691 ]

[wlame](http://staff/wlame) 2020-10-22 11:59:31+03:00

0.1.55
------
 * BTRIP-293 create trip and service in aeroclub  [ https://a.yandex-team.ru/arc/commit/7478343 ]

[terrmit](http://staff/terrmit) 2020-10-19 23:50:27+03:00

0.1.54
------
 * weaker aeroclub models validation  [ https://a.yandex-team.ru/arc/commit/7469355 ]

[terrmit](http://staff/terrmit) 2020-10-15 17:34:13+03:00

0.1.53
------
 * BTRIP-292 Refactoring  [ https://a.yandex-team.ru/arc/commit/7466935 ]

[terrmit](http://staff/terrmit) 2020-10-14 23:14:25+03:00

0.1.52
------
 * fix aeroclub hotel model  [ https://a.yandex-team.ru/arc/commit/7456206 ]

[terrmit](http://staff/terrmit) 2020-10-12 14:36:35+03:00

0.1.51
------
 * BTRIP-249 lib async-clients added  [ https://a.yandex-team.ru/arc/commit/7440377 ]

[terrmit](http://staff/terrmit) 2020-10-06 13:47:17+03:00

0.1.50
------
 * BTRIP-238: fixed_code  [ https://a.yandex-team.ru/arc/commit/7341518 ]

[d1568](http://staff/d1568) 2020-09-17 19:06:55+03:00

0.1.49
------
 * BTRIP-238: fixed_delete_doc  [ https://a.yandex-team.ru/arc/commit/7340660 ]

[d1568](http://staff/d1568) 2020-09-17 17:09:23+03:00

0.1.48
------

* [terrmit](http://staff/terrmit)

 * sort trips by trip_id desc  [ https://a.yandex-team.ru/arc/commit/7308968 ]
 * segment aircraft none       [ https://a.yandex-team.ru/arc/commit/7308861 ]

* [d1568](http://staff/d1568)

 * BTRIP-183: inegration to staff  [ https://a.yandex-team.ru/arc/commit/7308821 ]

[terrmit](http://staff/terrmit) 2020-09-08 00:16:36+03:00

0.1.47
------
 * BTRIP-216 aeroclub proxy endpoint  [ https://a.yandex-team.ru/arc/commit/7301205 ]

[terrmit](http://staff/terrmit) 2020-09-04 15:07:35+03:00

0.1.46
------
 * BTRIP-185 BTRIP-188 BTRIP-205 person partial update and remove  [ https://a.yandex-team.ru/arc/commit/7268131 ]

[terrmit](http://staff/terrmit) 2020-08-30 21:54:57+03:00

0.1.45
------
 * BTRIP-120: fixed  [ https://a.yandex-team.ru/arc/commit/7261124 ]

[d1568](http://staff/d1568) 2020-08-27 18:44:49+03:00

0.1.44
------
 * BTRIP-207: get_all_filter_for_search  [ https://a.yandex-team.ru/arc/commit/7260912 ]
 * BTRIP-120: update staf trip           [ https://a.yandex-team.ru/arc/commit/7260907 ]

[d1568](http://staff/d1568) 2020-08-27 18:03:55+03:00

0.1.43
------
 * BTRIP-190: fix  [ https://a.yandex-team.ru/arc/commit/7252639 ]

[d1568](http://staff/d1568) 2020-08-25 14:17:45+03:00

0.1.42
------
 * BTRIP-190 add comment to trip    [ https://a.yandex-team.ru/arc/commit/7252246 ]
 * BTRIP-108: add workflow service  [ https://a.yandex-team.ru/arc/commit/7250676 ]

[d1568](http://staff/d1568) 2020-08-25 12:40:34+03:00

0.1.41
------
 * BTRIP-182: add round_trip_departure_on  [ https://a.yandex-team.ru/arc/commit/7250380 ]

[d1568](http://staff/d1568) 2020-08-24 18:55:29+03:00

0.1.40
------
 * PR from branch users/wlame/BTRIP-144__tripstaff_converter_part2  [ https://a.yandex-team.ru/arc/commit/7250151 ]

[wlame](http://staff/wlame) 2020-08-24 18:08:15+03:00

0.1.39
------
 * BTRIP-119: add tasks  [ https://a.yandex-team.ru/arc/commit/7249291 ]

[d1568](http://staff/d1568) 2020-08-24 15:10:51+03:00

0.1.38
------
 * add migration in ya make  [ https://a.yandex-team.ru/arc/commit/7249222 ]

[terrmit](http://staff/terrmit) 2020-08-24 14:39:48+03:00

0.1.37
------
 * BTRIP-110 add person login  [ https://a.yandex-team.ru/arc/commit/7249046 ]

[terrmit](http://staff/terrmit) 2020-08-24 14:12:43+03:00

0.1.36
------
 * trips from staff fix  [ https://a.yandex-team.ru/arc/commit/7248925 ]

[terrmit](http://staff/terrmit) 2020-08-24 13:33:40+03:00

0.1.35
------

* [terrmit](http://staff/terrmit)

 * trip create fix                                 [ https://a.yandex-team.ru/arc/commit/7241510 ]
 * BTRIP-159 add and remove document to/from trip  [ https://a.yandex-team.ru/arc/commit/7240244 ]
 * BTRIP-171 create trip with author               [ https://a.yandex-team.ru/arc/commit/7240240 ]

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-134__fix_citizenship_migration  [ https://a.yandex-team.ru/arc/commit/7236358 ]

* [baranovxyz](http://staff/baranovxyz)

 * скрипт для загрузки данных на stat без хардкода  [ https://a.yandex-team.ru/arc/commit/7226039 ]
 * копипаста аналитики по Baobab                    [ https://a.yandex-team.ru/arc/commit/7225289 ]

[terrmit](http://staff/terrmit) 2020-08-20 21:44:34+03:00

0.1.34
------
 * PR from branch users/wlame/BTRIP-134__migration_fix2  [ https://a.yandex-team.ru/arc/commit/7223267 ]

[wlame](http://staff/wlame) 2020-08-14 20:32:22+03:00

0.1.33
------
 * PR from branch users/wlame/BTRIP-134__migration_fix  [ https://a.yandex-team.ru/arc/commit/7223194 ]

[wlame](http://staff/wlame) 2020-08-14 20:11:36+03:00

0.1.32
------
 * PR from branch users/wlame/BTRIP-134__large_schema_update  [ https://a.yandex-team.ru/arc/commit/7222458 ]

[wlame](http://staff/wlame) 2020-08-14 16:59:14+03:00

0.1.31
------
 * BTRIP-165 staff_trip_uuid          [ https://a.yandex-team.ru/arc/commit/7214780 ]
 * BTRIP-157 response_model           [ https://a.yandex-team.ru/arc/commit/7214750 ]
 * BTRIP-145 unhandled exception fix  [ https://a.yandex-team.ru/arc/commit/7214747 ]

[terrmit](http://staff/terrmit) 2020-08-12 16:39:13+03:00

0.1.30
------

BTRIP-123 create person  [ https://a.yandex-team.ru/arc/commit/7212778 ]

[d1568](http://staff/d1568) 2020-08-12 02:54:41+03:00

0.1.29
------

* [shadchin](http://staff/shadchin)

 * PYTHONCOM-252 Prepare for enable check F401 module imported but unused  [ https://a.yandex-team.ru/arc/commit/7168584 ]

[wlame](http://staff/wlame) 2020-08-03 12:52:09+03:00

0.1.28
------

* [terrmit](http://staff/terrmit)

 * aeroclub search  [ https://a.yandex-team.ru/arc/commit/7165317 ]

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-122__assignments  [ https://a.yandex-team.ru/arc/commit/7164941 ]

[terrmit](http://staff/terrmit) 2020-07-31 21:17:09+03:00

0.1.27
------
 * PR from branch users/wlame/BTRIP-117__yamake_fix  [ https://a.yandex-team.ru/arc/commit/7164084 ]

[wlame](http://staff/wlame) 2020-07-31 16:05:24+03:00

0.1.26
------
 * PR from branch users/wlame/BTRIP-117__staff_trip_uuid_field  [ https://a.yandex-team.ru/arc/commit/7160912 ]

[wlame](http://staff/wlame) 2020-07-31 13:41:33+03:00

0.1.25
------
 * fixed uri  [ https://a.yandex-team.ru/arc/commit/7157500 ]

[d1568](http://staff/d1568) 2020-07-29 19:31:24+03:00

0.1.24
------
 * fixed migration  [ https://a.yandex-team.ru/arc/commit/7157126 ]

[d1568](http://staff/d1568) 2020-07-29 17:54:58+03:00

0.1.23
------
 * BTRIP-93 sync profile  [ https://a.yandex-team.ru/arc/commit/7156856 ]

[d1568](http://staff/d1568) 2020-07-29 16:51:24+03:00

0.1.22
------
 * PR from branch users/wlame/hotfix  [ https://a.yandex-team.ru/arc/commit/7156618 ]

[wlame](http://staff/wlame) 2020-07-29 15:45:31+03:00

0.1.21
------

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-98__fix_router  [ https://a.yandex-team.ru/arc/commit/7153140 ]

* [terrmit](http://staff/terrmit)

 * from_staff fix  [ https://a.yandex-team.ru/arc/commit/7153117 ]

[wlame](http://staff/wlame) 2020-07-28 15:35:12+03:00

0.1.20
------

* [terrmit](http://staff/terrmit)

 * some api endpoints  [ https://a.yandex-team.ru/arc/commit/7152248 ]

[wlame](http://staff/wlame) 2020-07-28 15:10:09+03:00

0.1.19
------
 * fix 401                  [ https://a.yandex-team.ru/arc/commit/7144130 ]
 * BTRIP-99 search details  [ https://a.yandex-team.ru/arc/commit/7144075 ]

[terrmit](http://staff/terrmit) 2020-07-23 23:23:48+03:00

0.1.18
------
 * fix trip-detail endpoint  [ https://a.yandex-team.ru/arc/commit/7140497 ]

[terrmit](http://staff/terrmit) 2020-07-22 23:17:48+03:00

0.1.17
------
 * Fix api/docs  [ https://a.yandex-team.ru/arc/commit/7140446 ]

[terrmit](http://staff/terrmit) 2020-07-22 22:46:46+03:00

0.1.16
------
 * BTRIP-95 references api  [ https://a.yandex-team.ru/arc/commit/7138407 ]

[terrmit](http://staff/terrmit) 2020-07-22 13:55:23+03:00

0.1.15
------
 * BTRIP-90 Aeroclub client  [ https://a.yandex-team.ru/arc/commit/7132943 ]

[terrmit](http://staff/terrmit) 2020-07-20 21:19:38+03:00

0.1.14
------
 * add some test  [ https://a.yandex-team.ru/arc/commit/7123071 ]

[d1568](http://staff/d1568) 2020-07-17 21:37:35+03:00

0.1.13
------
 * BTRIP-76: get trip api

[d1568](http://staff/d1568) 2020-07-15 11:57:57+03:00

0.1.12
------

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-48__logging

* [terrmit](http://staff/terrmit)

 * BTRIP-50 Trip create

* [d1568](http://staff/d1568)

 * fixed

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-changes_needed-yellow.svg) [![terrmit](https://codereview.common-int.yandex-team.ru/badges/terrmit-...-yellow.svg)](https://staff.yandex-team.ru/terrmit) [![uruz](https://codereview.common-int.yandex-team.ru/badges/uruz-...-yellow.svg)](https://staff.yandex-team.ru/uruz)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/7091436 ]

[wlame](http://staff/wlame) 2020-07-13 12:41:47+03:00

0.1.11
------
 * BTRIP-66: fixed db

 * BTRIP-84: add devexp    [ https://a.yandex-team.ru/arc/commit/7090195 ]

[d1568](http://staff/d1568) 2020-07-08 20:42:07+03:00

0.1.10
------

* [terrmit](http://staff/terrmit)

 * BTRIP-47 trip list from staff  [ https://a.yandex-team.ru/arc/commit/7084190 ]

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-9__auth_meta  [ https://a.yandex-team.ru/arc/commit/7082632 ]

[wlame](http://staff/wlame) 2020-07-07 14:41:52+03:00

0.1.9
-----
 * users/wlame/BTRIP-45__tvm2_auth Аутентификация пользователя в blackbox [ https://a.yandex-team.ru/arc/commit/7073462 ]

[wlame](http://staff/wlame) 2020-07-02 16:49:10+03:00

0.1.8
-----
 * added shell and dbshell entrypoints  [ https://a.yandex-team.ru/arc/commit/7040071 ]

[terrmit](http://staff/terrmit) 2020-06-26 15:50:49+03:00

0.1.2
---

* [terrmit](http://staff/terrmit)

 * Fix import           [ https://a.yandex-team.ru/arc/commit/7035581 ]
 * Trip list            [ https://a.yandex-team.ru/arc/commit/7030882 ]
 * basic pagination     [ https://a.yandex-team.ru/arc/commit/7003103 ]
 * switched to fastapi  [ https://a.yandex-team.ru/arc/commit/6930838 ]
 * initial commit       [ https://a.yandex-team.ru/arc/commit/6917561 ]

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/BTRIP-43__update_scheme  [ https://a.yandex-team.ru/arc/commit/7004946 ]
 * init tables                                         [ https://a.yandex-team.ru/arc/commit/6974540 ]

[terrmit](http://staff/terrmit) 2020-06-25 15:15:35+03:00

rrmit](http://staff/terrmit) 2020-06-25 15:15:35+03:00

heme  [ https://a.yandex-team.ru/arc/commit/7004946 ]
 * init tables                                         [ https://a.yandex-team.ru/arc/commit/6974540 ]

[terrmit](http://staff/terrmit) 2020-06-25 15:15:35+03:00

rrmit](http://staff/terrmit) 2020-06-25 15:15:35+03:00

