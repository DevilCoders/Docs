1.749
-----
 * CIA-3216 move already_exists error to warnings  [ https://a.yandex-team.ru/arc/commit/9790430 ]

[tmalikova](http://staff/tmalikova) 2022-07-29 12:38:42+03:00

1.748
-----
 * COMP-54 switch to ForeignKey  [ https://a.yandex-team.ru/arc/commit/9769138 ]

[wlame](http://staff/wlame) 2022-07-25 20:03:09+03:00

1.747
-----
 * PR from branch users/wlame/COMP-40__actionlog

COMP-40 actionlogs  [ https://a.yandex-team.ru/arc/commit/9766191 ]

[wlame](http://staff/wlame) 2022-07-25 13:36:06+03:00

1.746
-----

* [nspeganov](http://staff/nspeganov)

 * PR from branch users/nspeganov/COMP-44_two_flags

COMP-44: Add two flags to the Payment Type  [ https://a.yandex-team.ru/arc/commit/9759393 ]

[wlame](http://staff/wlame) 2022-07-24 15:48:38+03:00

1.745
-----
 * STAFF-17774 fix returning vesting data for staff robot  [ https://a.yandex-team.ru/arc/commit/9739793 ]

[tmalikova](http://staff/tmalikova) 2022-07-19 13:07:13+03:00

1.744
-----
 * STAFF-17919 no DEBUG in testing  [ https://a.yandex-team.ru/arc/commit/9734699 ]

[wlame](http://staff/wlame) 2022-07-18 15:04:19+03:00

1.743
-----
 * CIA-3229 skip empty MTH_ID  [ https://a.yandex-team.ru/arc/commit/9726405 ]

[wlame](http://staff/wlame) 2022-07-15 13:53:26+03:00

1.742
-----
 * CIA-3215 add role_types filters to calibrations suggest  [ https://a.yandex-team.ru/arc/commit/9725786 ]

[tmalikova](http://staff/tmalikova) 2022-07-15 12:49:22+03:00

1.741
-----
 * STAFF-17919 detailed income  [ https://a.yandex-team.ru/arc/commit/9715248 ]

[wlame](http://staff/wlame) 2022-07-13 15:48:27+03:00

1.740
-----
 * CIA-3225 hotfix celery router  [ https://a.yandex-team.ru/arc/commit/9704440 ]

[wlame](http://staff/wlame) 2022-07-11 18:18:45+03:00

1.739
-----
 * TOOLSDUTY-437 Обновил хосты баз данных для тестинга и прода.  [ https://a.yandex-team.ru/arc/commit/9678137 ]

[wlame](http://staff/wlame) 2022-07-05 18:31:56+03:00

1.738
-----
 * COMP-39 remove payment_plan + fix required fields  [ https://a.yandex-team.ru/arc/commit/9660639 ]

[wlame](http://staff/wlame) 2022-07-01 12:37:27+03:00

1.737
-----
 * COMP-39 hotfix  [ https://a.yandex-team.ru/arc/commit/9657460 ]

[wlame](http://staff/wlame) 2022-06-30 17:32:53+03:00

1.736
-----
 * COMP-39 hotfix comma  [ https://a.yandex-team.ru/arc/commit/9657391 ]

[wlame](http://staff/wlame) 2022-06-30 17:24:48+03:00

1.735
-----
 * COMP-39 download files

Чтобы файлы можно было скачать из приватного бакета mds сделал вьюхи для них в коде.
Пока мы не договаривались об архитектуре  АПИ в новом сервисе сделал всё максимально просто, лаконично и не использовал базовые классы вьюх, сериализаторов и FileResponse из остальной Ревьюшницы.  [ https://a.yandex-team.ru/arc/commit/9657096 ]

[wlame](http://staff/wlame) 2022-06-30 16:54:41+03:00

1.734
-----
 * PR from branch users/wlame/COMP-28__elements2

1. Добавил учёт настроек Element'ов при расчёте фактических дат выплат.
2. Заменил использование PaymentPlan на PaymentType везде. plan-это только разбивка по месяцам\процентам, человек должен оперировать типами выплат, которые внутри подразумевают некоторый план.
3. Убрал поле Schedule.element чтобы не поддерживать консистентность потом что привязка к стране непосредственно через поле (заполняемое из ручки обогащения) и через Элементы совпадала. Элементы используются только в последний момент когда они нужны — при расчёте date из raw_date в PersonPayment'ах.  [ https://a.yandex-team.ru/arc/commit/9624993 ]

[wlame](http://staff/wlame) 2022-06-23 12:17:44+03:00

1.733
-----
 * COMP-36 fix migrations  [ https://a.yandex-team.ru/arc/commit/9621281 ]

[tmalikova](http://staff/tmalikova) 2022-06-22 16:20:12+03:00

1.732
-----
 * COMP-36 add cryptography  [ https://a.yandex-team.ru/arc/commit/9621063 ]

[tmalikova](http://staff/tmalikova) 2022-06-22 15:57:02+03:00

1.731
-----

* [tmalikova](http://staff/tmalikova)

 * STAFF-17774 count deferred payments as not vested options for loans  [ https://a.yandex-team.ru/arc/commit/9620563 ]

* [wlame](http://staff/wlame)

 * COMP-28 elements + paymenttypes + refactor_models

\- Добавил модели **Elemet** и **PaymentType**.
 - Переименовал во многих местах поля, убрал избыточные "payment" в названиях полей и дал более осмысленные названия (обсуждаемо).
Например: `PersonPayment.payment_date` -> PersonPayment.raw_date и `PersonPayment.actual_payment_date` -> PersonPayment.date
 - Разбил models.py на несколько файлов. Положил choices внутрь models/
 - Админку тоже разделил на два файла аналогично моделям, но, думаю, можно будет разделить вообще по админке на файл в случае больших админок с инлайнами или с большим количеством полей.

Мне до сих пор не нравятся названия bonus и bonus_absolute в PersonPaymentSchedule, но с ними пока ничего не делал. Вообще сильно не хватает обсуждения голосом названий сущностей. Я всю дорогу ориентировался на  понимание предметной области (которое менялось) и своё чувство прекрасного.  [ https://a.yandex-team.ru/arc/commit/9610389 ]

[tmalikova](http://staff/tmalikova) 2022-06-22 15:03:06+03:00

1.730
-----

* [tmalikova](http://staff/tmalikova)

 * CIA-3166 add chief and level to api  [ https://a.yandex-team.ru/arc/commit/9596784 ]

* [wlame](http://staff/wlame)

 * COMP-26 tests  [ https://a.yandex-team.ru/arc/commit/9586618 ]

[tmalikova](http://staff/tmalikova) 2022-06-16 17:12:58+03:00

1.729
-----
 * PR from branch users/wlame/COMP-26__export_payments

COMP-26 model + admin + migration + export

[wlame](http://staff/wlame) 2022-06-08 16:28:24+03:00

1.728
-----

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/COMP-27__regular_payments

COMP-27 regular_payments + models + migration + admins + tests
Рассчёт нового поля actual_payment_date на основании дат регулярных выплат сотруднику.  [ https://a.yandex-team.ru/arc/commit/9557180 ]

* [tmalikova](http://staff/tmalikova)

 * DEVEXPMIGRATION-465 migrate from devexp to a.yaml  [ https://a.yandex-team.ru/arc/commit/9545501 ]

[wlame](http://staff/wlame) 2022-06-07 13:01:13+03:00

1.727
-----
 * COMP-17 init compensations models and some logic  [ https://a.yandex-team.ru/arc/commit/9539058 ]

[wlame](http://staff/wlame) 2022-06-02 17:05:48+03:00

1.726
-----
 * STAFF-17709 Удалил парсер bi ответов и походы за ними + убрал LAST_FULL_STRUCTURE_CHANGE_ID

Убрал всё что связано с походам в bi-ручки и удалил уже неактуальный костылик LAST_FULL_STRUCTURE_CHANGE_ID
\+ обновил тесты.  [ https://a.yandex-team.ru/arc/commit/9536114 ]

[wlame](http://staff/wlame) 2022-06-02 11:16:52+03:00

1.725
-----
 * STAFF-17709 new bi fields  [ https://a.yandex-team.ru/arc/commit/9522700 ]

[wlame](http://staff/wlame) 2022-05-31 01:42:45+03:00

1.724
-----
 * COMP-20 admin access for compensations app only  [ https://a.yandex-team.ru/arc/commit/9518117 ]

[tmalikova](http://staff/tmalikova) 2022-05-30 12:35:52+03:00

1.723
-----
 * CIA-3121 deferred_payment_mode  [ https://a.yandex-team.ru/arc/commit/9493844 ]

[tmalikova](http://staff/tmalikova) 2022-05-24 15:20:25+03:00

1.722
-----
 * CIA-2946 send pending tasks status to xiva  [ https://a.yandex-team.ru/arc/commit/9488353 ]
 * Change ".devexp.json"                       [ https://a.yandex-team.ru/arc/commit/9475561 ]

[tmalikova](http://staff/tmalikova) 2022-05-23 16:08:03+03:00

1.721
-----
 * COMP-16 add comma  [ https://a.yandex-team.ru/arc/commit/9473261 ]

[wlame](http://staff/wlame) 2022-05-19 11:40:27+03:00

1.720
-----

* [shigarus](http://staff/shigarus)

 * CIA-3102: change salary source

CIA-3102: fix salary for loan  [ https://a.yandex-team.ru/arc/commit/9469926 ]

* [wlame](http://staff/wlame)

 * PR from branch users/wlame/STAFF-17521__bi_from_yt  [ https://a.yandex-team.ru/arc/commit/9469897 ]

[wlame](http://staff/wlame) 2022-05-18 15:40:20+03:00

1.719
-----
 * PR from branch users/wlame/COMP-16__save_file

COMP-16 file import + admin  [ https://a.yandex-team.ru/arc/commit/9450209 ]

[wlame](http://staff/wlame) 2022-05-13 11:38:35+03:00

1.718
-----

[wlame](http://staff/wlame) 2022-05-12 17:26:18+03:00

1.717
-----
 * CIA-2892 force review bonus mode.  [ https://a.yandex-team.ru/arc/commit/9447140 ]

[wlame](http://staff/wlame) 2022-05-12 16:35:37+03:00

1.716
-----
 * CIA-3102: max loan sums

CIA-3102: amax loan sums  [ https://a.yandex-team.ru/arc/commit/9441995 ]

[shigarus](http://staff/shigarus) 2022-05-11 16:44:02+03:00

1.715
-----
 * CIA-2831 Создание PersonHeads только при смене цепочек руководителей.  [ https://a.yandex-team.ru/arc/commit/9423963 ]

[wlame](http://staff/wlame) 2022-05-04 14:43:04+03:00

1.714
-----

* [tmalikova](http://staff/tmalikova)

 * STAFF-17506 hardcoded report date pt2  [ https://a.yandex-team.ru/arc/commit/9414876 ]

* [dsamuylov](http://staff/dsamuylov)

 * ARCANUM-4429 feat: templates for a.yamls for devexp mirgation

<!-- TXIFM BEGIN -->

Полезные ссылки
\- <img src="https://yastatic.net/s3/cloud/arcanum/static/freeze/assets/favicons/default.png" alt="arc-logo" width="16"/> [Trunk сервиса](https://a.yandex-team.ru/arc_vcs/taxi/frontend/services/services/admin-lenta)
\- <img src="https://wiki.yandex-team.ru/favicon-32x32.png" alt="wiki-logo" width="16"/> [Вики по монорепе](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/projects/infrastructure-group/monorepo/)
\- <img src="https://teamcity.taxi.yandex-team.ru/img/icons/teamcity.svg" alt="tc-logo" width="16"/> [Custom Unstable сборка](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomUnstable?branch=services/admin-lenta&buildTypeTab=overview&mode=builds#all-projects)
\- <img src="https://teamcity.taxi.yandex-team.ru/img/icons/teamcity.svg" alt="tc-logo" width="16"/> [Custom Testing сборка](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomTesting?branch=services/admin-lenta&buildTypeTab=overview&mode=builds#all-projects)
\- <img src="https://teamcity.taxi.yandex-team.ru/img/icons/teamcity.svg" alt="tc-logo" width="16"/> [Stable сборка](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Releases_AutoRelease?branch=services/admin-lenta&buildTypeTab=overview&mode=builds#all-projects)
\- <img src="https://nanny.yandex-team.ru/favicon.ico" alt="nanny-logo" width="16"/> [Nanny unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_lenta_unstable)
\- <img src="https://nanny.yandex-team.ru/favicon.ico" alt="nanny-logo" width="16"/> [Nanny testing](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_lenta_testing)
\- <img src="https://abc.yandex-team.ru/favicon.ico" alt="abc-logo" width="16"/> [Дежурный по монорепе такси](https://abc.yandex-team.ru/services/taxiinfranaimautomation/duty/)
\- [Чат поддержки монорепы такси](https://t.me/joinchat/Fdwfq0k2PQo8-AXgtNtpfQ)
\------------------

<!-- TXIFM END -->  [ https://a.yandex-team.ru/arc/commit/9412645 ]

* [shigarus](http://staff/shigarus)

 * CIA-3119: import deferred payment

CIA-3119: import deferred payment  [ https://a.yandex-team.ru/arc/commit/9406484 ]

[tmalikova](http://staff/tmalikova) 2022-04-29 15:01:57+03:00

1.713
-----

* [tmalikova](http://staff/tmalikova)

 * CIA-3111 change errorbooster init  [ https://a.yandex-team.ru/arc/commit/9393442 ]

* [qazaq](http://staff/qazaq)

 * CIA-3120: Разрешаем дефис в логинах в ручке проверки прав  [ https://a.yandex-team.ru/arc/commit/9387643 ]

[tmalikova](http://staff/tmalikova) 2022-04-25 15:01:32+03:00

1.712
-----
 * CIA-3114: None salaries

CIA-3114: none salaries  [ https://a.yandex-team.ru/arc/commit/9369641 ]

[shigarus](http://staff/shigarus) 2022-04-19 16:13:20+03:00

1.711
-----
 * CIA-2161 fix collect person reviews for head in ext/outstaff  [ https://a.yandex-team.ru/arc/commit/9369020 ]

[tmalikova](http://staff/tmalikova) 2022-04-19 15:11:29+03:00

1.710
-----

* [shigarus](http://staff/shigarus)

 * CIA-3078: fix task transactions

CIA-3078: fix task transactions  [ https://a.yandex-team.ru/arc/commit/9364582 ]
 * CIA-2940: extend loan api

CIA-2940: extend loan api              [ https://a.yandex-team.ru/arc/commit/9364580 ]

* [tmalikova](http://staff/tmalikova)

 * fix broken requirements  [ https://a.yandex-team.ru/arc/commit/9362766 ]

[shigarus](http://staff/shigarus) 2022-04-18 21:20:42+03:00

1.709
-----
 * CIA-3056: deferred payment

CIA-3056: deffered_payment  [ https://a.yandex-team.ru/arc/commit/9343287 ]

[shigarus](http://staff/shigarus) 2022-04-13 00:50:41+03:00

1.708
-----

* [shigarus](http://staff/shigarus)

 * CIA-1491: old

CIA-1491: old  [ https://a.yandex-team.ru/arc/commit/9341041 ]

* [tmalikova](http://staff/tmalikova)

 * CIA-2886 replace all (moved from git)  [ https://a.yandex-team.ru/arc/commit/9341010 ]

* [qazaq](http://staff/qazaq)

 * Изменил владельцев Реьюшницы  [ https://a.yandex-team.ru/arc/commit/9340898 ]

* [robot-vcs-migration](http://staff/robot-vcs-migration)

 * TOARCADIA-1771 [migration] github/tools/review-draft

Note: mandatory check (NEED_CHECK) was skipped  [ https://a.yandex-team.ru/arc/commit/9336830 ]

* [wlame](http://staff/wlame)

 * Update .trendbox.yml (prepare for arcadia) (#745)

\* Update .trendbox.yml (prepare for arcadia)
Co-authored-by: Kirill Kartashov <qazaq@yandex-team.ru>  [ https://a.yandex-team.ru/arc_vcs/commit/3e699614110e602dd3a8ea8cf06841cb48498d78 ]

[shigarus](http://staff/shigarus) 2022-04-12 17:38:23+03:00

1.707
-----
 * CIA-2856: tasks api (#708)  [ https://github.yandex-team.ru/tools/review-draft/commit/81cb381a ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-04-08 17:20:32+03:00

1.706
-----
 * CIA-2908: extend admin (#738)  [ https://github.yandex-team.ru/tools/review-draft/commit/83900188 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-03-28 13:58:41+03:00

1.705
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2909: raise retries and timeout (#739)  [ https://github.yandex-team.ru/tools/review-draft/commit/61dfb98e ]
 * CIA-3040: race condition (#740)             [ https://github.yandex-team.ru/tools/review-draft/commit/8b74332f ]

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2926 fix 403 to fb with werewolf auth (#742)  [ https://github.yandex-team.ru/tools/review-draft/commit/a45653de ]
 * CIA-2973  fix delayed tasks (#734)                [ https://github.yandex-team.ru/tools/review-draft/commit/2724273c ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-03-25 20:57:35+03:00

1.704
-----
 * CIA-2912: store every update try (#730)  [ https://github.yandex-team.ru/tools/review-draft/commit/61f4c2ce ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-03-24 19:51:46+03:00

1.703
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-3041 get feedback by login (#741)  [ https://github.yandex-team.ru/tools/review-draft/commit/435b2fbd ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-03-23 16:58:42+03:00

1.702
-----
 * CIA-3033: fix db hosts (#737)  [ https://github.yandex-team.ru/tools/review-draft/commit/55992443 ]
 * CIA-2987: fix kpi call (#726)  [ https://github.yandex-team.ru/tools/review-draft/commit/3c8e5a0f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-03-22 19:34:09+03:00

1.701
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-3001 fix 500 in ids-only and add log it (#736)  [ https://github.yandex-team.ru/tools/review-draft/commit/1330dfef ]
 * Update .devexp.json                                 [ https://github.yandex-team.ru/tools/review-draft/commit/bbabfbd6 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-3003: fix csv non comma (#732)  [ https://github.yandex-team.ru/tools/review-draft/commit/e65e1326 ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-03-22 16:10:17+03:00

1.700
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2999 add x-session-id to allowed cors headers (#735)  [ https://github.yandex-team.ru/tools/review-draft/commit/928c8a92 ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-03-22 12:27:11+03:00

1.699
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2911: stop threads (#731)  [ https://github.yandex-team.ru/tools/review-draft/commit/6a281bab ]

* [Dmitry Andriyanov](http://staff/dima117a@yandex-team.ru)

 * fix: CIA-3019: Не отображается тэг группы в калибровках (#733)  [ https://github.yandex-team.ru/tools/review-draft/commit/48f77881 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-03-21 16:11:14+03:00

1.698
-----
 * CIA-2917: xls edit gradient (#728)  [ https://github.yandex-team.ru/tools/review-draft/commit/1b1c5182 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-03-17 19:02:23+03:00

1.697
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2995 add flags to /frontend/users (#729)  [ https://github.yandex-team.ru/tools/review-draft/commit/461b0e59 ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-03-17 16:43:24+03:00

1.696
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2914 fix person vs sync (#727)  [ https://github.yandex-team.ru/tools/review-draft/commit/6a107139 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-03-15 23:26:51+03:00

1.695
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2988 correct logic on product_schema_loaded field (#725)  [ https://github.yandex-team.ru/tools/review-draft/commit/eacfdc9e ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-03-15 22:13:19+03:00

1.694
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2913  gradient again (#709)  [ https://github.yandex-team.ru/tools/review-draft/commit/8a16f04c ]

* [Julia Zaretskaya](http://staff/juliazrtsk@yandex-team.ru)

 * CIA-2962: added profession field (#724)  [ https://github.yandex-team.ru/tools/review-draft/commit/42be1f61 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2981: add calibration id (#722)  [ https://github.yandex-team.ru/tools/review-draft/commit/8533a06c ]

* [Dmitry Andriyanov](http://staff/dima117a@yandex-team.ru)

 * feat: унифицировал поля в ручке для калибровок (#718)  [ https://github.yandex-team.ru/tools/review-draft/commit/5d592930 ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-03-15 14:30:54+03:00

1.693
-----

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * fix oebs logging  [ https://github.yandex-team.ru/tools/review-draft/commit/18a1260e ]

[Dmitry Prokopenko](http://staff/dmitrypro@yandex-team.ru) 2022-03-11 13:15:12+03:00

1.692
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2900: fix float serialize (#715)  [ https://github.yandex-team.ru/tools/review-draft/commit/be1cbfe0 ]
 * CIA-2958: fix build (#714)            [ https://github.yandex-team.ru/tools/review-draft/commit/434a1a57 ]
 * CIA-2952: fix freezing (#707)         [ https://github.yandex-team.ru/tools/review-draft/commit/d967a7cf ]

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2950: fix oebs  [ https://github.yandex-team.ru/tools/review-draft/commit/3babebfd ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-03-05 14:29:38+03:00

1.691
-----

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2855: multi remove  [ https://github.yandex-team.ru/tools/review-draft/commit/f0624e82 ]

[Dmitry Prokopenko](http://staff/dmitrypro@yandex-team.ru) 2022-02-18 12:30:45+03:00

1.690
-----
 * CIA-2911: eb research (#705)  [ https://github.yandex-team.ru/tools/review-draft/commit/23f2a70c ]
 * CIA-2942: monitoring (#706)   [ https://github.yandex-team.ru/tools/review-draft/commit/a529d510 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-17 10:54:37+03:00

1.689
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2858 correct logging setup (#704)  [ https://github.yandex-team.ru/tools/review-draft/commit/475407ea ]
 * CIA-2906 create stand commans (#702)   [ https://github.yandex-team.ru/tools/review-draft/commit/a1e25ec8 ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-02-16 15:25:40+03:00

1.688
-----
 * CIA-2911: fix threads count (#703)  [ https://github.yandex-team.ru/tools/review-draft/commit/1f36f965 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-15 13:24:35+03:00

1.687
-----
 * CIA-2848: fix dumb 401 (#700)  [ https://github.yandex-team.ru/tools/review-draft/commit/aebdfba5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-14 19:21:37+03:00

1.686
-----
 * CIA-2927: add more fields to person-reviews-mode-review (#699)  [ https://github.yandex-team.ru/tools/review-draft/commit/099c9993 ]

[Dmitry Andriyanov](http://staff/dima117a@yandex-team.ru) 2022-02-14 15:45:26+03:00

1.685
-----
 * CIA-2929: fix oebs sync (#701)  [ https://github.yandex-team.ru/tools/review-draft/commit/37f5e329 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-14 13:13:28+03:00

1.684
-----
 * CIA-2848: extend looging (#698)  [ https://github.yandex-team.ru/tools/review-draft/commit/98f29130 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-10 11:38:25+03:00

1.683
-----
 * CIA-2848: logging 401 (#697)                  [ https://github.yandex-team.ru/tools/review-draft/commit/1d01b88b ]
 * CIA-2911: fix errorbooster operations (#696)  [ https://github.yandex-team.ru/tools/review-draft/commit/2691e7aa ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-09 18:13:23+03:00

1.682
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * STAFF-16736 add settings for sync chunk size and move options_history sync to separate task  [ https://github.yandex-team.ru/tools/review-draft/commit/801c7bd6 ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-02-08 15:13:00+03:00

1.681
-----
 * CIA-2848: fix return (#695)  [ https://github.yandex-team.ru/tools/review-draft/commit/d3abcab9 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-08 13:18:03+03:00

1.680
-----
 * CIA-2848: fix 401 (#688)                 [ https://github.yandex-team.ru/tools/review-draft/commit/b752d197 ]
 * CIA-2904: add goals dates to api (#694)  [ https://github.yandex-team.ru/tools/review-draft/commit/f9d1f9df ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-08 12:33:15+03:00

1.679
-----
 * STAFF-16203: fix mark format (#693)  [ https://github.yandex-team.ru/tools/review-draft/commit/1f7ca5e1 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-08 12:10:58+03:00

1.678
-----
 * STAFF-16203: move loan urls (#678)  [ https://github.yandex-team.ru/tools/review-draft/commit/12c727f0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-07 20:54:20+03:00

1.677
-----
 * CIA-2783: fix env load (#691)  [ https://github.yandex-team.ru/tools/review-draft/commit/57d55128 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-07 18:08:36+03:00

1.676
-----
 * CIA-2783: errorbooster (#687)  [ https://github.yandex-team.ru/tools/review-draft/commit/b446d7f3 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-07 10:13:34+03:00

1.675
-----

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2847: fix tasks error  [ https://github.yandex-team.ru/tools/review-draft/commit/c5264a43 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2851: fix edit empty reviewers (#682)  [ https://github.yandex-team.ru/tools/review-draft/commit/40cb760e ]

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2899 new fields to mode review (#686)  [ https://github.yandex-team.ru/tools/review-draft/commit/d7e7eb25 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-02-04 14:28:22+03:00

1.674
-----
 * releasing version 1.672  [ https://github.yandex-team.ru/tools/review-draft/commit/75c6d2ca ]
 * releasing version 1.673  [ https://github.yandex-team.ru/tools/review-draft/commit/c6dee96d ]

[Dmitry Prokopenko](http://staff/dmitrypro@yandex-team.ru) 2022-01-28 18:16:29+03:00

1.672
-----

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2852: finding names  [ https://github.yandex-team.ru/tools/review-draft/commit/b70762c1 ]

[Dmitry Prokopenko](http://staff/dmitrypro@yandex-team.ru) 2022-01-28 18:02:46+03:00

1.671
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2803 delayed tasks (#681)  [ https://github.yandex-team.ru/tools/review-draft/commit/ae673db2 ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-01-28 13:23:46+03:00

1.670
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * STAFF-16679 shrink chunk sizes (#683)  [ https://github.yandex-team.ru/tools/review-draft/commit/376c63db ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-01-24 16:28:53+03:00

1.669
-----
 * CIA-2846: py2to3 fix (#680)          [ https://github.yandex-team.ru/tools/review-draft/commit/ff5dc01d ]
 * CIA-2851: log edit reviewers (#679)  [ https://github.yandex-team.ru/tools/review-draft/commit/d7fe4ab9 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-01-20 18:21:06+03:00

1.668
-----
 * CIA-2485: fix sync new persons (#677)  [ https://github.yandex-team.ru/tools/review-draft/commit/09873164 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2022-01-19 17:22:43+03:00

1.667
-----

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2418: py2to3  [ https://github.yandex-team.ru/tools/review-draft/commit/6f2fd22e ]

[Dmitry Prokopenko](http://staff/dmitrypro@yandex-team.ru) 2022-01-17 14:36:30+03:00

1.666
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2840 fix NotImplementedError (#676)  [ https://github.yandex-team.ru/tools/review-draft/commit/ee78b708 ]

* [tmalikova](http://staff/tmalikova@yandex-team.ru)

 * remove notification from staff_structure_delay and celery_queue_size alerts  [ https://github.yandex-team.ru/tools/review-draft/commit/07bc459d ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-01-14 15:58:25+03:00

1.665
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * CIA-2850 add fields to review api (#675)    [ https://github.yandex-team.ru/tools/review-draft/commit/26279b4e ]
 * CIA-2737 change alert notifications (#670)  [ https://github.yandex-team.ru/tools/review-draft/commit/c225fdfa ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2022-01-11 13:19:15+03:00

1.664
-----
 * CIA-2822: fix sync structure for not yet synced persons (#674)  [ https://github.yandex-team.ru/tools/review-draft/commit/160b9754 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-12-17 15:49:12+03:00

1.663
-----
 * CIA-2822: fix import chains for new employyes (#673)  [ https://github.yandex-team.ru/tools/review-draft/commit/74ae0cdb ]
 * CIA-2821: fix no assignments (#672)                   [ https://github.yandex-team.ru/tools/review-draft/commit/7260798f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-12-17 12:29:06+03:00

1.662
-----
 * CIA-2811: use YAUTH_MECHANISMS (#669)  [ https://github.yandex-team.ru/tools/review-draft/commit/dbc977da ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-12-16 14:43:50+03:00

1.661
-----

* [Dmitriy Chuchin](http://staff/tekkengod129@yandex-team.ru)

 * CIA-2667: use tvm for staff (#666)  [ https://github.yandex-team.ru/tools/review-draft/commit/c3f275c3 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-12-14 14:33:36+03:00

1.660
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * STAFF-15984: loan options data (#667)  [ https://github.yandex-team.ru/tools/review-draft/commit/476db9a4 ]

* [Dmitriy Chuchin](http://staff/tekkengod129@yandex-team.ru)

 * CIA-2465: add uid fix (#668)  [ https://github.yandex-team.ru/tools/review-draft/commit/b454e99b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-12-13 17:30:50+03:00

1.659
-----

* [Dmitriy Chuchin](http://staff/tekkengod129@yandex-team.ru)

 * CIA-2465: fix staff sync on testing (#639)  [ https://github.yandex-team.ru/tools/review-draft/commit/492aa9bc ]

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * Update README.md  [ https://github.yandex-team.ru/tools/review-draft/commit/0128a97c ]
 * Update README.md  [ https://github.yandex-team.ru/tools/review-draft/commit/e3b13a89 ]

[Дмитрий Чучин](http://staff/tekkengod129@yandex-team.ru) 2021-12-02 10:02:58+03:00

1.658
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2786: partial sync (#665)  [ https://github.yandex-team.ru/tools/review-draft/commit/a3e66bc9 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-11-24 17:44:21+03:00

1.657
-----
 * CIA-2781: fix notifications for changes (#664)  [ https://github.yandex-team.ru/tools/review-draft/commit/07ab1288 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-11-19 10:29:39+03:00

1.656
-----

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2742: hr roles  [ https://github.yandex-team.ru/tools/review-draft/commit/66e11a96 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2784: fix tvm (#663)  [ https://github.yandex-team.ru/tools/review-draft/commit/96b81abf ]

[Dmitry Prokopenko](http://staff/dmitrypro@yandex-team.ru) 2021-11-18 21:26:44+03:00

1.655
-----
 * CIA-2748: edit superreviewers as hr (#657)  [ https://github.yandex-team.ru/tools/review-draft/commit/a706b871 ]
 * CIA-2756: bi viewer (#659)                  [ https://github.yandex-team.ru/tools/review-draft/commit/cda0063c ]
 * Replace qloud info with deploy              [ https://github.yandex-team.ru/tools/review-draft/commit/f919e9bc ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-11-16 12:46:35+03:00

1.654
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2761: fix grouping mails (#660)  [ https://github.yandex-team.ru/tools/review-draft/commit/4a1e0423 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-11-13 17:27:54+03:00

1.653
-----
 * CIA-2755: fix wf timeouts (#658)  [ https://github.yandex-team.ru/tools/review-draft/commit/fb42e72b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-11-10 21:35:40+03:00

1.652
-----

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * STAFF-15949: add mock data for testing sync (#655)  [ https://github.yandex-team.ru/tools/review-draft/commit/87d6c173 ]

[tmalikova](http://staff/tmalikova@yandex-team.ru) 2021-10-29 15:16:32+03:00

1.651
-----

* [Stanislav Shabalin](http://staff/voux@yandex-team.ru)

 * CIA-2718: Improve readability  [ https://github.yandex-team.ru/tools/review-draft/commit/e191f5c0 ]

* [Taisiia Malikova](http://staff/tmalikova@yandex-team.ru)

 * STAFF-15949: 4 years income forecast (#653)  [ https://github.yandex-team.ru/tools/review-draft/commit/635e4642 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-10-28 18:46:00+03:00

1.650
-----

* [Stanislav Shabalin](http://staff/voux@yandex-team.ru)

 * CIA-2718: upload umbrellas view (#654)  [ https://github.yandex-team.ru/tools/review-draft/commit/efb54272 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-10-27 11:45:07+03:00

1.649
-----
 * CIA-2727: fix minus mark export (#652)  [ https://github.yandex-team.ru/tools/review-draft/commit/faece484 ]
 * Add team members to code-review         [ https://github.yandex-team.ru/tools/review-draft/commit/e8340a6b ]
 * delete excess reviewers                 [ https://github.yandex-team.ru/tools/review-draft/commit/45d7924b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-10-20 15:24:03+03:00

1.648
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2721: extend info for export (#651)  [ https://github.yandex-team.ru/tools/review-draft/commit/45c66059 ]
 * CIA-2704: fix uid serialization (#649)   [ https://github.yandex-team.ru/tools/review-draft/commit/0d993e5b ]

* [Dmitriy Chuchin](http://staff/tekkengod129@yandex-team.ru)

 * CIA-2616: failed tasks monitorings (#650)  [ https://github.yandex-team.ru/tools/review-draft/commit/4b722c63 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-10-18 17:24:24+03:00

1.647
-----

* [Stanislav Shabalin](http://staff/voux@yandex-team.ru)

 * CIA-2693: turn off umbrellas goals sync with waffle (#648)  [ https://github.yandex-team.ru/tools/review-draft/commit/b3d8d11a ]

* [Dmitriy Chuchin](http://staff/tekkengod129@yandex-team.ru)

 * CIA-2603: get umbrellas and main products by ids (#640)  [ https://github.yandex-team.ru/tools/review-draft/commit/c09db3e7 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-10-07 13:08:33+03:00

1.646
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2669: fix zero bonus (#647)  [ https://github.yandex-team.ru/tools/review-draft/commit/5e884bc ]

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2638: fix umbrella deleting  [ https://github.yandex-team.ru/tools/review-draft/commit/7c925ff ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-10-06 12:35:23+03:00

1.645
-----

* [Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru)

 * STAFF-15923: Запретить сотрудникам с ролью HRBP вообще видеть кабинет (#642)  [ https://github.yandex-team.ru/tools/review-draft/commit/68a1ea9 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2635: extend task logging (#646)  [ https://github.yandex-team.ru/tools/review-draft/commit/0cb0b7b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-10-01 18:23:02+03:00

1.644
-----
 * Cia 2635 calibration marks history (#644)  [ https://github.yandex-team.ru/tools/review-draft/commit/cd03a04 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-10-01 02:21:38+03:00

1.643
-----
 * CIA-2605: fix for deleting multiple person_review umbrellas (#643)  [ https://github.yandex-team.ru/tools/review-draft/commit/80c3cad0 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-09-30 18:15:38+03:00

1.642
-----
 * CIA-2534: chunked tasks (#641)  [ https://github.yandex-team.ru/tools/review-draft/commit/d9ef8a4 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-29 11:20:25+03:00

1.641
-----
 * CIA-2579: post for export (#638)  [ https://github.yandex-team.ru/tools/review-draft/commit/02d3de0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-24 01:06:52+03:00

1.640
-----
 * CIA-2575: VS and umbrellas import shell script (#637)  [ https://github.yandex-team.ru/tools/review-draft/commit/3421ccb0 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-09-24 00:54:52+03:00

1.639
-----

* [Stanislav Shabalin](http://staff/voux@yandex-team.ru)

 * CIA-2570: Fix 500 for missing xlsx template (#634)  [ https://github.yandex-team.ru/tools/review-draft/commit/e81f01fc ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2577: kpi weight (#636)               [ https://github.yandex-team.ru/tools/review-draft/commit/50b0cd57 ]
 * CIA-2565: fix reviewers filtering (#635)  [ https://github.yandex-team.ru/tools/review-draft/commit/0b579088 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-09-23 17:44:55+03:00

1.638
-----
 * CIA-2566: allow edit calibrators while archive (#633)  [ https://github.yandex-team.ru/tools/review-draft/commit/8e2b94d ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-23 01:57:54+03:00

1.637
-----
 * CIA-2557: fix add to calirations (#632)  [ https://github.yandex-team.ru/tools/review-draft/commit/70fc818 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-22 00:47:27+03:00

1.636
-----
 * CIA-2526: refactore kpi (#631)  [ https://github.yandex-team.ru/tools/review-draft/commit/7a8a257 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-21 01:59:36+03:00

1.635
-----
 * CIA-2528: Fix ST query for main product sync (#630)  [ https://github.yandex-team.ru/tools/review-draft/commit/8ed1b600 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-09-20 12:49:40+03:00

1.634
-----

* [Dmitriy Chuchin](http://staff/tekkengod129@yandex-team.ru)

 * CIA-2448: fix oebs connector (#629)  [ https://github.yandex-team.ru/tools/review-draft/commit/356e6ca ]
 * CIA-2448: kpi sync (#622)            [ https://github.yandex-team.ru/tools/review-draft/commit/22dd86e ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2448: fix celery call (#628)    [ https://github.yandex-team.ru/tools/review-draft/commit/88b13a5 ]
 * CIA-2516: change kpi format (#627)  [ https://github.yandex-team.ru/tools/review-draft/commit/96069ca ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-18 00:43:17+03:00

1.633
-----
 * CIA-2508: fix wrong csrf domain (#626)  [ https://github.yandex-team.ru/tools/review-draft/commit/c989db3 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-15 17:45:46+03:00

1.632
-----
 * CIA-2507: minifixes (#625)  [ https://github.yandex-team.ru/tools/review-draft/commit/96440bb ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-15 15:53:51+03:00

1.631
-----
 * CIA-25061: fix add persons (#624)  [ https://github.yandex-team.ru/tools/review-draft/commit/55fbf51 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-15 11:18:51+03:00

1.630
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2503: fix dupes (#623)  [ https://github.yandex-team.ru/tools/review-draft/commit/645ef5d ]

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2453: retry if exc got  [ https://github.yandex-team.ru/tools/review-draft/commit/91993df ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-14 18:42:42+03:00

1.629
-----

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2458: add to calibration speedup  [ https://github.yandex-team.ru/tools/review-draft/commit/566be20 ]
 * CIA-2463: export as task              [ https://github.yandex-team.ru/tools/review-draft/commit/c5d03e5 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2496: async (#617)  [ https://github.yandex-team.ru/tools/review-draft/commit/0e1e8ad ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-13 22:42:11+03:00

1.628
-----
 * Add constraint for excel templates with the same type (#620)  [ https://github.yandex-team.ru/tools/review-draft/commit/9685d11 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-09-13 14:21:17+03:00

1.627
-----
 * CIA-2459  oebs with tvm (#619)  [ https://github.yandex-team.ru/tools/review-draft/commit/eab8937 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-09-13 12:13:06+03:00

1.626
-----
 * CIA-2468: fix stats (#616)       [ https://github.yandex-team.ru/tools/review-draft/commit/06d795d ]
 * CIA-2488: wrong operator (#615)  [ https://github.yandex-team.ru/tools/review-draft/commit/508fa76 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-10 00:04:49+03:00

1.625
-----
 * CIA-2468: celery split (#614)           [ https://github.yandex-team.ru/tools/review-draft/commit/ca07e32 ]
 * CIA-2468: celery ram limit (#612)       [ https://github.yandex-team.ru/tools/review-draft/commit/47cd61a ]
 * CIA-2488: fix dates for vs sync (#613)  [ https://github.yandex-team.ru/tools/review-draft/commit/58ecae5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-09 22:12:04+03:00

1.624
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2486: change goals url (#610)  [ https://github.yandex-team.ru/tools/review-draft/commit/ef990a4 ]

* [Dmitriy Chuchin](http://staff/tekkengod129@yandex-team.ru)

 * CIA-2457: hand of id list (#607)  [ https://github.yandex-team.ru/tools/review-draft/commit/72c2340 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-09-08 14:46:20+03:00

1.623
-----
 * CIA-2419  review monitoring (#604)  [ https://github.yandex-team.ru/tools/review-draft/commit/99c0e02 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-09-06 19:12:41+03:00

1.622
-----
 * CIA-2482: add domain (#609)  [ https://github.yandex-team.ru/tools/review-draft/commit/63904f1 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-03 18:23:57+03:00

1.621
-----
 * CIA-2482: csrf (#608)  [ https://github.yandex-team.ru/tools/review-draft/commit/204b77c ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-03 17:48:10+03:00

1.620
-----
 * CIA-2482: cors (#606)  [ https://github.yandex-team.ru/tools/review-draft/commit/7aac3e0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-03 15:36:03+03:00

1.619
-----
 * CIA-2468: celery ram limit (#603)  [ https://github.yandex-team.ru/tools/review-draft/commit/249be23 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-09-01 22:19:37+03:00

1.618
-----

* [Dmitriy Chuchin](http://staff/tekkengod129@yandex-team.ru)

 * CIA-2456: set public-read default ACL for non-prod (#602)  [ https://github.yandex-team.ru/tools/review-draft/commit/65b6bc0 ]
 * set default object ACL as None (#601)                      [ https://github.yandex-team.ru/tools/review-draft/commit/2b092aa ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2455: get person review ids (#600)  [ https://github.yandex-team.ru/tools/review-draft/commit/140518e ]
 * CIA-2472: update zdm (#599)             [ https://github.yandex-team.ru/tools/review-draft/commit/56e91ed ]
 * CIA-2383: rename parameter (#598)       [ https://github.yandex-team.ru/tools/review-draft/commit/6e24b39 ]

* [Stanislav Shabalin](http://staff/voux@yandex-team.ru)

 * CIA-2430  editing  taken in average (#594)  [ https://github.yandex-team.ru/tools/review-draft/commit/eeb0afd ]

[Дмитрий Чучин](http://staff/tekkengod129@yandex-team.ru) 2021-08-31 12:05:11+03:00

1.617
-----

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2437: fix calibration mode  [ https://github.yandex-team.ru/tools/review-draft/commit/acbc2fd ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2464: calibration review ids (#597)  [ https://github.yandex-team.ru/tools/review-draft/commit/b15c278 ]

[Dmitry Prokopenko](http://staff/dmitrypro@yandex-team.ru) 2021-08-25 16:52:35+03:00

1.616
-----

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2451: add kpi_loaded to review  [ https://github.yandex-team.ru/tools/review-draft/commit/6d1a872 ]
 * CIA-2449: kpi loaded                [ https://github.yandex-team.ru/tools/review-draft/commit/e36fff6 ]
 * CIA-2454: product schema loaded     [ https://github.yandex-team.ru/tools/review-draft/commit/ab3f233 ]
 * CIA-2447: get kpi                   [ https://github.yandex-team.ru/tools/review-draft/commit/81c8fdb ]
 * CIA-2437: umbrella action           [ https://github.yandex-team.ru/tools/review-draft/commit/eb9ac60 ]

[Dmitry Prokopenko](http://staff/dmitrypro@yandex-team.ru) 2021-08-24 12:28:26+03:00

1.615
-----

* [Stanislav Shabalin](http://staff/voux@yandex-team.ru)

 * Issue CIA-2453: Fix typo in super() for s3 storage lib                        [ https://github.yandex-team.ru/tools/review-draft/commit/45fb9da ]
 * CIA-2429: Add PersonReview.taken_in_average to API fields and filters (#583)  [ https://github.yandex-team.ru/tools/review-draft/commit/ea04348 ]
 * CIA-2453 (#591)                                                               [ https://github.yandex-team.ru/tools/review-draft/commit/46565ae ]
 * CIA-2428 Add taken_in_average to model (#581)                                 [ https://github.yandex-team.ru/tools/review-draft/commit/950b79a ]

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2446: kpi model  [ https://github.yandex-team.ru/tools/review-draft/commit/2fce6f3 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2445: fix umbrella connection (#585)  [ https://github.yandex-team.ru/tools/review-draft/commit/13c71ad ]
 * CIA-2445: fix vs sync (#584)              [ https://github.yandex-team.ru/tools/review-draft/commit/95e14f2 ]
 * CIA-2443: stabilyze sync (#582)           [ https://github.yandex-team.ru/tools/review-draft/commit/7ae9116 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-08-23 12:02:57+03:00

1.614
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2422: calibration speedup (#579)          [ https://github.yandex-team.ru/tools/review-draft/commit/0d715f0 ]
 * CIA-2436: main product suggest (#578)         [ https://github.yandex-team.ru/tools/review-draft/commit/44f437a ]
 * CIA-2440: fix test (#580)                     [ https://github.yandex-team.ru/tools/review-draft/commit/a720926 ]
 * CIA-2440: umbrella in history (#577)          [ https://github.yandex-team.ru/tools/review-draft/commit/d10fd82 ]
 * CIA-2433: fix read file (#576)                [ https://github.yandex-team.ru/tools/review-draft/commit/6b28c68 ]
 * Update admin.py (#575)                        [ https://github.yandex-team.ru/tools/review-draft/commit/f093446 ]
 * CIA-2433: fix excel templ admin (#574)        [ https://github.yandex-team.ru/tools/review-draft/commit/5bfec88 ]
 * CIA-2372: add umbrella to history url (#573)  [ https://github.yandex-team.ru/tools/review-draft/commit/3be2c33 ]

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2373_umbrella_suggest_fix  [ https://github.yandex-team.ru/tools/review-draft/commit/648cead ]
 * CIA-2373_umbrella_suggest      [ https://github.yandex-team.ru/tools/review-draft/commit/3467802 ]
 * CIA-2372: umbrella api         [ https://github.yandex-team.ru/tools/review-draft/commit/d0a3f36 ]

* [Stanislav Shabalin](http://staff/voux@yandex-team.ru)

 * CIA-2374: add main_product and umbrella to csv export (#571)  [ https://github.yandex-team.ru/tools/review-draft/commit/ecb64eb ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-08-13 14:15:14+03:00

1.613
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2406: templated export (#562)       [ https://github.yandex-team.ru/tools/review-draft/commit/2c33cf3 ]
 * CIA-2366: deploy settings for releaser  [ https://github.yandex-team.ru/tools/review-draft/commit/5d7da8b ]
 * CIA-2371: fix using goals protocol      [ https://github.yandex-team.ru/tools/review-draft/commit/22cc502 ]
 * CIA-2371: fix using goals host          [ https://github.yandex-team.ru/tools/review-draft/commit/40f3fcd ]
 * CIA-2371: fix st test host              [ https://github.yandex-team.ru/tools/review-draft/commit/0b904b0 ]

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * locky (#558)  [ https://github.yandex-team.ru/tools/review-draft/commit/9d14d03 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-08-04 11:34:39+03:00

1.612
-----

* [Stanislav Shabalin](http://staff/voux@yandex-team.ru)

 * CIA-2405 excel template (#564)  [ https://github.yandex-team.ru/tools/review-draft/commit/0f6877d ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2371: main product sync (#568)    [ https://github.yandex-team.ru/tools/review-draft/commit/4bb2db3 ]
 * CIA-2370: main product scheme (#563)  [ https://github.yandex-team.ru/tools/review-draft/commit/bf31748 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-07-23 19:32:54+03:00

1.611
-----
 * CIA-2365: revert stupid (#567)  [ https://github.yandex-team.ru/tools/review-draft/commit/c574b18 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-07-20 11:41:10+03:00

1.610
-----
 * CIA-2365: fix stupid (#566)  [ https://github.yandex-team.ru/tools/review-draft/commit/478c92c ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-07-20 01:28:31+03:00

1.609
-----
 * CIA-2365: fix mutable struct bug (#565)  [ https://github.yandex-team.ru/tools/review-draft/commit/565ae09 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-07-20 00:51:57+03:00

1.608
-----
 * CIA-2365: python join (#560)  [ https://github.yandex-team.ru/tools/review-draft/commit/a1b4694 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-07-15 20:59:51+03:00

1.607
-----
 * Delay PersonReview denormalizations with Celery tasks (#554)  [ https://github.yandex-team.ru/tools/review-draft/commit/1ee39f4 ]

[Stanislav Shabalin](http://staff/voux@yandex-team.ru) 2021-07-13 12:44:32+03:00

1.606
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2409: add filtering (#557)  [ https://github.yandex-team.ru/tools/review-draft/commit/3166afb ]

* [Dmitriy Prokopenko](http://staff/dmitrypro@yandex-team.ru)

 * CIA-2379_vs_fetcher (#555)  [ https://github.yandex-team.ru/tools/review-draft/commit/9901db5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-07-09 15:59:01+03:00

1.605
-----
 * CIA-2378: calibration suggest (#553)  [ https://github.yandex-team.ru/tools/review-draft/commit/dc7549f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-07-02 14:50:17+03:00

1.604
-----
 * CIA-2376: review filter for scales (#551)    [ https://github.yandex-team.ru/tools/review-draft/commit/c865c38 ]
 * CIA-2377: add filter by calibrations (#552)  [ https://github.yandex-team.ru/tools/review-draft/commit/8cfb750 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-06-28 22:03:46+03:00

1.603
-----
 * CIA-2385: speed up get review list (#550)  [ https://github.yandex-team.ru/tools/review-draft/commit/4d202d0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-06-22 14:42:01+03:00

1.602
-----
 * CIA-2385: speed hack (#549)  [ https://github.yandex-team.ru/tools/review-draft/commit/b17ae8f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-06-21 19:37:29+03:00

1.601
-----

* [Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru)

 * CIA-2367: Подновлять фин данные из OEBS (#548)  [ https://github.yandex-team.ru/tools/review-draft/commit/b0d08ef ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2021-06-07 20:29:51+03:00

1.600
-----

* [Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru)

 * STAFF-13662: подправил условие для синка опционов (#547)  [ https://github.yandex-team.ru/tools/review-draft/commit/119dd08 ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2021-05-20 18:14:41+03:00

1.599
-----

* [Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru)

 * STAFF-14666: учёл роль смотрителя кабинета в ручка, которые отдают данные про опционы и другое (#546)  [ https://github.yandex-team.ru/tools/review-draft/commit/40f7afd ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2021-05-17 21:26:24+03:00

1.598
-----

* [Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru)

 * CIA-2346: [back] Скрыть от руклей остатки по опционам сотрудников. (#545)  [ https://github.yandex-team.ru/tools/review-draft/commit/167b471 ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2021-05-11 21:39:55+03:00

1.597
-----
 * CIA-2292: speed up add persons (#544)  [ https://github.yandex-team.ru/tools/review-draft/commit/974b2fc ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-03-30 12:31:52+03:00

1.596
-----
 * review.test.yandex-team.ru CORS added (#543)  [ https://github.yandex-team.ru/tools/review-draft/commit/45933d7 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2021-03-26 00:21:30+03:00

1.595
-----
 * CIA-2266: uwsgi listen (#542)  [ https://github.yandex-team.ru/tools/review-draft/commit/20a600a ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-03-24 19:00:39+03:00

1.594
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2266: exclude mode-calibration from master-only (#541)  [ https://github.yandex-team.ru/tools/review-draft/commit/14b3a8e ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2021-03-24 18:53:20+03:00

1.593
-----
 * CIA-2266: better db choose (#540)  [ https://github.yandex-team.ru/tools/review-draft/commit/4eabab9 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-03-24 17:46:56+03:00

1.592
-----
 * CIA-2266: more requests? (#539)  [ https://github.yandex-team.ru/tools/review-draft/commit/ed2737f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-03-24 15:58:13+03:00

1.591
-----
 * CIA-2182: review-awacs-balancer.yandex-team.ru CORS added (#538)  [ https://github.yandex-team.ru/tools/review-draft/commit/1f18dd4 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2021-03-15 14:45:40+03:00

1.590
-----
 * CIA-2211: make review workflow async (#535)  [ https://github.yandex-team.ru/tools/review-draft/commit/d78c153 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-03-09 14:56:46+03:00

1.589
-----
 * CIA-2213: Регулярно ломается синк ролей в Review (#537)  [ https://github.yandex-team.ru/tools/review-draft/commit/5ac2306 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2021-03-09 12:07:03+03:00

1.588
-----
 * CIA-2211: denormalyze chunked (#536)  [ https://github.yandex-team.ru/tools/review-draft/commit/9fae662 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-03-01 14:28:22+03:00

1.587
-----
 * CIA-2210: Сотрудник не может открыть ревьюшницу (#533)  [ https://github.yandex-team.ru/tools/review-draft/commit/adea1ba ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2021-02-26 15:40:46+03:00

1.586
-----

* [Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru)

 * CIA-2205: 500 в ручке для кабинета (#532)  [ https://github.yandex-team.ru/tools/review-draft/commit/506bf05 ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2021-02-11 19:50:30+03:00

1.585
-----
 * CIA-2148: extend review settings (#529)  [ https://github.yandex-team.ru/tools/review-draft/commit/be59c29 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2021-02-05 19:10:55+03:00

1.584
-----

* [Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru)

 * STAFF-14425: [back] У HRBP нет доступа к кабинету ряда сотрудников (#531)  [ https://github.yandex-team.ru/tools/review-draft/commit/e01a531 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-2148: pip=>21 dropped python2 (#530)  [ https://github.yandex-team.ru/tools/review-draft/commit/de690b8 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * CIA-2167: releaser qloud config (#527)  [ https://github.yandex-team.ru/tools/review-draft/commit/d61ae8b ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2021-01-26 21:59:26+03:00

1.583
-----

* [Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru)

 * STAFF-14414: [back] mark_current должен быть объектом в bi-income (#528)  [ https://github.yandex-team.ru/tools/review-draft/commit/cf0acfa ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2021-01-22 18:21:30+03:00

1.582
-----

* [Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru)

 * STAFF-14292 Совокупный доход выше 18 доступен только руководителям (#526)      [ https://github.yandex-team.ru/tools/review-draft/commit/64d9019 ]
 * STAFF-14254: [back] Подтянуть данные про грейды и оценки из BI для со… (#524)  [ https://github.yandex-team.ru/tools/review-draft/commit/da68a75 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * CIA-2167: Переезд в Y.Deploy (#525)  [ https://github.yandex-team.ru/tools/review-draft/commit/17b0481 ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2021-01-21 19:56:12+03:00

1.581
-----
 * CIA-2165: fix xls serialize (#523)  [ https://github.yandex-team.ru/tools/review-draft/commit/7b36823 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-12-21 18:55:39+03:00

1.580
-----
 * CIA-2127: any tmpl for comment (#522)  [ https://github.yandex-team.ru/tools/review-draft/commit/0575899 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-11-10 16:27:13+03:00

1.579
-----
 * CIA-2117: add bonus comment (#521)  [ https://github.yandex-team.ru/tools/review-draft/commit/252d0b5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-11-03 19:10:26+03:00

1.578
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-2021: add st_goals_url (#519)  [ https://github.yandex-team.ru/tools/review-draft/commit/3af1534 ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-11-02 22:30:27+03:00

1.577
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * add log len comment (#517)  [ https://github.yandex-team.ru/tools/review-draft/commit/5b7a242 ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-10-19 14:15:21+03:00

1.576
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-2067: add new mark for import and export (#515)  [ https://github.yandex-team.ru/tools/review-draft/commit/0176fa0 ]
 * CIA-2079: add view_participants (#516)               [ https://github.yandex-team.ru/tools/review-draft/commit/cf7fbca ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-10-07 15:53:27+03:00

1.575
-----
 * CIA-2087: Ошибочно считаем изменение тега среднего изменением оценки (#514)  [ https://github.yandex-team.ru/tools/review-draft//commit/62b92d0 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-10-05 16:51:31+03:00

1.574
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-2064: fixed MARK_LEVEL_HISTORY_RANGE (#513)  [ https://github.yandex-team.ru/tools/review-draft/commit/9325936 ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-09-22 11:45:47+03:00

1.573
-----
 * CIA-1656 Дайджест изменений в ревью подчинённых (#506)  [ https://github.yandex-team.ru/tools/review-draft/commit/af86f91 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2020-09-18 16:43:33+03:00

1.572
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * fixed (#512)  [ https://github.yandex-team.ru/tools/review-draft/commit/fa86e42 ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-09-17 18:27:43+03:00

1.571
-----
 * CIA-2054  Добавил scale_id в ручку. (#511)  [ https://github.yandex-team.ru/tools/review-draft/commit/7e7183c ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2020-09-17 12:43:01+03:00

1.570
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-2042: add new type mark (#507)  [ https://github.yandex-team.ru/tools/review-draft/commit/ad02cf2 ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-09-16 19:31:28+03:00

1.569
-----

* [Wladimir Spasskiy](http://staff/wlame@yandex-team.ru)

 * CIA-2057 снизил количество логинов в чанке синка, т.к. стабильно таймаутим при 500. (#510)  [ https://github.yandex-team.ru/tools/review-draft/commit/91e66f6 ]
 * CIA-1656 deleted icon files                                                                 [ https://github.yandex-team.ru/tools/review-draft/commit/5394f0f ]

* [Valeriy Baranov](http://staff/baranovxyz@yandex-team.ru)

 * feat: письмо с дайджестом оценок (#508)  [ https://github.yandex-team.ru/tools/review-draft/commit/d24a15e ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2020-09-16 19:25:17+03:00

1.568
-----
 * STAFF-13856: Не 500-тить при отсутствии данных о з/п (#505)  [ https://github.yandex-team.ru/tools/review-draft//commit/ac693da ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-09-04 19:05:51+03:00

1.567
-----
 * CIA-1779 не делаю лишних вычислений при проверке прав (#504)  [ https://github.yandex-team.ru/tools/review-draft/commit/358daa8 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2020-09-04 14:34:51+03:00

1.566
-----
 * CIA-2025: Кривой заголовок письма с напоминанием (#503)  [ https://github.yandex-team.ru/tools/review-draft//commit/390a78d ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-07-31 11:57:02+03:00

1.565
-----
 * STAFF-13668: new time for sync (#502)  [ https://github.yandex-team.ru/tools/review-draft/commit/9b3f338 ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2020-07-28 13:08:22+03:00

1.564
-----
 * STAFF-13637: [back] Отображать ставку из Ревьюшницы в Кабинете (#501)  [ https://github.yandex-team.ru/tools/review-draft//commit/e34683e ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-07-17 12:55:20+03:00

1.563
-----
 * STAFF-13572: Fincab viewer role (#499)  [ https://github.yandex-team.ru/tools/review-draft/commit/1a217e4 ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2020-07-14 16:18:13+03:00

1.562
-----
 * STAFF-13581: Отключил проверку CSRF для списковой ручки дохода сотрудников (#500)  [ https://github.yandex-team.ru/tools/review-draft//commit/c1289c8 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-07-14 11:26:03+03:00

1.561
-----
 * STAFF-13589: [back] Поддержать несколько логинов в ручках ревьюшницы для фин. кабинета (#498)  [ https://github.yandex-team.ru/tools/review-draft//commit/c3a1dba ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-07-09 09:19:18+03:00

1.560
-----

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * Add piecerate (#497)  [ https://github.yandex-team.ru/tools/review-draft/commit/9b0c9c9 ]

[cracker](http://staff/cracker@yandex-team.ru) 2020-07-06 15:06:32+03:00

1.559
-----

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * STAFF-13474: [back] Доработать синк с BI - удалять логины которых нет в ответе (#494)  [ https://github.yandex-team.ru/tools/review-draft/commit/9309bdb ]

[cracker](http://staff/cracker@yandex-team.ru) 2020-06-24 22:21:35+03:00

1.558
-----
 * STAFF-13348: [back] Ревьюшница - отлавливать неожиданные статусы от API BI (#495)  [ https://github.yandex-team.ru/tools/review-draft//commit/878dacd ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-06-24 16:21:45+03:00

1.557
-----

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * STAFF-13520: [back] Использовать в качстве ключа в bi rates LEGAL_ENT… (#493)  [ https://github.yandex-team.ru/tools/review-draft/commit/4b86a37 ]

[cracker](http://staff/cracker@yandex-team.ru) 2020-06-23 14:28:56+03:00

1.556
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-1979: fixed status for bonus review (#492)  [ https://github.yandex-team.ru/tools/review-draft/commit/85eb51a ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-06-16 12:05:04+03:00

1.555
-----
 * STAFF-13463: currency sync (#491)  [ https://github.yandex-team.ru/tools/review-draft/commit/c28073e ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2020-06-09 19:19:04+03:00

1.554
-----

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * STAFF-13435: [back] Дать доступ до фин. кабинета hr-партнерам (#490)  [ https://github.yandex-team.ru/tools/review-draft/commit/3132f91 ]

[cracker](http://staff/cracker@yandex-team.ru) 2020-06-04 16:34:27+03:00

1.553
-----
 * TOTP Fix (#489)  [ https://github.yandex-team.ru/tools/review-draft//commit/9750115 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-05-29 13:15:33+03:00

1.552
-----

* [denis-p](http://staff/denis-p@yandex-team.ru)

 * STAFF-13385: Fix  [ https://github.yandex-team.ru/tools/review-draft/commit/2808a28 ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2020-05-27 17:31:08+03:00

1.551
-----
 * STAFF-13385: Allow chiefs access (#488)  [ https://github.yandex-team.ru/tools/review-draft/commit/c10badd ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2020-05-27 16:45:42+03:00

1.550
-----
 * STAFF-13393: Review testing mocks (#487)  [ https://github.yandex-team.ru/tools/review-draft/commit/0a4f6a1 ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2020-05-25 13:43:22+03:00

1.549
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-2009: added celery task for fixing bonus type (#486)  [ https://github.yandex-team.ru/tools/review-draft/commit/113a551 ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-05-21 16:33:41+03:00

1.548
-----
 * STAFF-13334: Vesting (#485)  [ https://github.yandex-team.ru/tools/review-draft/commit/5220408 ]

[Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru) 2020-05-15 14:54:57+03:00

1.547
-----
 * STAFF-13264: Ручка совокупного дохода сотрудника (#483)  [ https://github.yandex-team.ru/tools/review-draft//commit/bb7509a ]
 * STAFF-13263: Ручка назначений сотрудника (#482)          [ https://github.yandex-team.ru/tools/review-draft//commit/f4922f8 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-05-14 11:53:01+03:00

1.546
-----
 * STAFF-13261, STAFF-13262: Получать и хранить данные из BI (#481)  [ https://github.yandex-team.ru/tools/review-draft//commit/8d37421 ]

[Maksim Aksenov](http://staff/aksenovma@yandex-team.ru) 2020-05-12 18:30:19+03:00

1.545
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-1914: role exporter for ficance api (#480)  [ https://github.yandex-team.ru/tools/review-draft/commit/fad4f96 ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-04-30 18:50:25+03:00

1.544
-----
 * CIA-1996: bonus rsu (#479)  [ https://github.yandex-team.ru/tools/review-draft/commit/df6a8e6 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-04-23 15:00:44+03:00

1.543
-----
 * CIA-1899: show not dismissed or in active review (#475)  [ https://github.yandex-team.ru/tools/review-draft/commit/377195d ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-04-22 19:48:12+03:00

1.542
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * Cia 1873  export xls (#471)  [ https://github.yandex-team.ru/tools/review-draft/commit/d48d120 ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-04-21 20:56:43+03:00

1.541
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-1910: added the ability to unarchive (#472)  [ https://github.yandex-team.ru/tools/review-draft/commit/d7e36b1 ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-04-17 21:29:53+03:00

1.540
-----
 * CIA-1992: filter secrets (#476)  [ https://github.yandex-team.ru/tools/review-draft/commit/36b579b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-04-17 16:09:58+03:00

1.539
-----
 * CIA-1987: add calibrator flagged action (#473)  [ https://github.yandex-team.ru/tools/review-draft/commit/1de4bcf ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-04-14 21:13:58+03:00

1.538
-----
 * CIA-1899: fix calc subordinates (#470)  [ https://github.yandex-team.ru/tools/review-draft/commit/f6b85f3 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-04-10 15:16:14+03:00

1.537
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-1926  waffle calibration auto update (#468)               [ https://github.yandex-team.ru/tools/review-draft/commit/2581beb ]
 * CIA-1921: added post to xiva for automatic update cpr (#466)  [ https://github.yandex-team.ru/tools/review-draft/commit/2923dde ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-04-01 20:39:32+03:00

1.536
-----
 * CIA-1932: fix add to review (#465)  [ https://github.yandex-team.ru/tools/review-draft/commit/914765b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-03-23 14:33:56+03:00

1.535
-----
 * freeze pygments  [ https://github.yandex-team.ru/tools/review-draft/commit/fdb2610 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-03-20 23:55:50+03:00

1.534
-----
 * disable csrf for testing  [ https://github.yandex-team.ru/tools/review-draft/commit/cb3e972 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-03-20 21:46:04+03:00

1.533
-----
 * CIA-1919: fix celery monitoring (#464)  [ https://github.yandex-team.ru/tools/review-draft/commit/9869705 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-03-18 22:18:13+03:00

1.532
-----
 * CIA-1889: extend review perm sys (#460)  [ https://github.yandex-team.ru/tools/review-draft/commit/61899f5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-03-13 14:00:07+00:00

1.531
-----
 * CIA-1902: copy calibration (#463)  [ https://github.yandex-team.ru/tools/review-draft/commit/af4d5e5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-03-05 17:02:32+00:00

1.530
-----
 * CIA-1901: extend active calibration api (#461)  [ https://github.yandex-team.ru/tools/review-draft/commit/1be0b19 ]
 * CIA-1890: add tag setting for frontend (#462)   [ https://github.yandex-team.ru/tools/review-draft/commit/19f3bfb ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-02-28 12:36:49+00:00

1.529
-----

* [Wladimir Spasskiy](http://staff/wlame@yandex-team.ru)

 * CIA-1705: exclude external persons for chiefs (#457)  [ https://github.yandex-team.ru/tools/review-draft/commit/8d3d32d ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1890: add tag setting for frontend (#454)  [ https://github.yandex-team.ru/tools/review-draft/commit/eb73ae8 ]
 * CIA-1886: add tag filtering (#456)             [ https://github.yandex-team.ru/tools/review-draft/commit/da29fec ]
 * CIA-1772: fix add admin (#458)                 [ https://github.yandex-team.ru/tools/review-draft/commit/0b3ae0c ]

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-1883: added tag_average_mark for PersonReviewsModeReviewView and … (#459)  [ https://github.yandex-team.ru/tools/review-draft/commit/60e8c89 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2020-02-25 13:27:16+03:00

1.528
-----

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-1878: added api PersonActiveCalibrationsView (#455)  [ https://github.yandex-team.ru/tools/review-draft/commit/5b83ad8 ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-02-20 14:25:15+03:00

1.527
-----

* [Wladimir Spasskiy](http://staff/wlame@yandex-team.ru)

 * CIA-1867  review salary date (#450)  [ https://github.yandex-team.ru/tools/review-draft/commit/07afd48 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1880: tag suggest (#453)  [ https://github.yandex-team.ru/tools/review-draft/commit/362fc0a ]

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * CIA-1877: marks mode for user model (#452)  [ https://github.yandex-team.ru/tools/review-draft/commit/677dab6 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2020-02-19 13:10:01+03:00

1.526
-----
 * CIA-1862: allow negative salary change  [ https://github.yandex-team.ru/tools/review-draft/commit/0c788b0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-02-11 12:49:04+00:00

1.525
-----
 * fix Dockerfile  [ https://github.yandex-team.ru/tools/review-draft/commit/b488898 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-02-11 12:37:06+00:00

1.524
-----
 * CIA-1871: return full log (#446)  [ https://github.yandex-team.ru/tools/review-draft/commit/036b0f0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-02-11 12:08:25+00:00

1.523
-----

* [Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru)

 * CIA-1875: Меньше правок для починки теста                          [ https://github.yandex-team.ru/tools/review-draft/commit/8aae996 ]
 * CIA-1875: Починил последний                                        [ https://github.yandex-team.ru/tools/review-draft/commit/0f305da ]
 * CIA-1875: Не падаю при экспорте, а пишу в лог                      [ https://github.yandex-team.ru/tools/review-draft/commit/aad68ae ]
 * CIA-1875: Починил ещё один тест                                    [ https://github.yandex-team.ru/tools/review-draft/commit/30f58c5 ]
 * CIA-1875: закинул тесты в контейнер и запускаю все из под compose  [ https://github.yandex-team.ru/tools/review-draft/commit/616fcdb ]
 * CIA-1875: Запускать тесты на postgre                               [ https://github.yandex-team.ru/tools/review-draft/commit/7c6a8f5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-02-07 11:56:20+00:00

1.522
-----
 * fix dependencies  [ https://github.yandex-team.ru/tools/review-draft/commit/f31f234 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-02-03 10:00:19+00:00

1.521
-----
 * CIA-1835: fix zero division  [ https://github.yandex-team.ru/tools/review-draft/commit/2649150 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2020-02-03 09:50:43+00:00

1.520
-----

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * CIA-1802: fix all dependencies (#445)  [ https://github.yandex-team.ru/tools/review-draft/commit/ab38130 ]

[cracker](http://staff/cracker@yandex-team.ru) 2019-11-08 20:04:50+03:00

1.519
-----

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * CIA-1802: fix celery queue monitoring (#444)  [ https://github.yandex-team.ru/tools/review-draft/commit/2f1bcd7 ]

[cracker](http://staff/cracker@yandex-team.ru) 2019-11-07 19:52:59+03:00

1.518
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * debug_hack  [ https://github.yandex-team.ru/tools/review-draft/commit/1669f83 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2019-10-30 17:16:05+03:00

1.517
-----
 * CIA-1790 добавление роли SALARY_READ экспортёрам.  [ https://github.yandex-team.ru/tools/review-draft/commit/87f7278 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2019-10-30 12:15:08+03:00

1.516
-----
 * CIA-1790 привожу к флоату всё  [ https://github.yandex-team.ru/tools/review-draft/commit/ad1a5db ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2019-10-29 12:05:35+03:00

1.515
-----
 * CIA-1784: fix export calibration roles  [ https://github.yandex-team.ru/tools/review-draft/commit/1c8566a ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-10-25 13:40:44+00:00

1.514
-----
 * CIA-1741: sync oebs handle (#440)                  [ https://github.yandex-team.ru/tools/review-draft/commit/9f2427e ]
 * CIA-1720: fix fill salary_change_absolute command  [ https://github.yandex-team.ru/tools/review-draft/commit/bd2cf0d ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-10-25 12:47:12+00:00

1.513
-----
 * CIA-1720: allow to specify absolute salary change value (#437)  [ https://github.yandex-team.ru/tools/review-draft/commit/38eac46 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-10-11 16:09:29+00:00

1.512
-----
 * add localhost for qloud statushook check  [ https://github.yandex-team.ru/tools/review-draft/commit/26d7859 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-10-10 08:50:42+00:00

1.511
-----
 * CIA-1781: add view for checking db from django (#438)  [ https://github.yandex-team.ru/tools/review-draft/commit/a8e0620 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-10-10 08:12:42+00:00

1.510
-----
 * CIA-1663 редактирование цепочки и изменение approve_level где надо.  [ https://github.yandex-team.ru/tools/review-draft/commit/623a6b5 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2019-09-26 15:55:30+03:00

1.509
-----
 * CIA-1754 fix migration  [ https://github.yandex-team.ru/tools/review-draft/commit/a9d9071 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2019-09-20 15:18:19+03:00

1.508
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1754: move tag_average_mark to last column  [ https://github.yandex-team.ru/tools/review-draft/commit/ec7ca4a ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2019-09-19 22:23:55+03:00

1.507
-----
 * CIA-1722: prohibit to approve flagged positive  [ https://github.yandex-team.ru/tools/review-draft/commit/e6fa61f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-09-09 11:42:08+00:00

1.506
-----
 * CIA-1719: subordination for dismissed (#432)  [ https://github.yandex-team.ru/tools/review-draft/commit/fed79ae ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-09-09 11:36:28+00:00

1.505
-----
 * CIA-1731: fix off-ny-one bugs in publish review results  [ https://github.yandex-team.ru/tools/review-draft/commit/5a2a43c ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-09-06 11:58:10+00:00

1.504
-----
 * CIA-1748 Ручка массового удаления PersonReview.  [ https://github.yandex-team.ru/tools/review-draft/commit/812eac4 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2019-09-04 15:00:01+03:00

1.503
-----
 * CIA-1752: speed up fetching structure changes (#430)  [ https://github.yandex-team.ru/tools/review-draft/commit/8c34300 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-09-02 16:02:48+00:00

1.502
-----
 * CIA-1726: remove auth from celery monitoring view  [ https://github.yandex-team.ru/tools/review-draft/commit/8a6985f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-08-27 14:12:21+00:00

1.501
-----
 * CIA-1726: celery monitoring             [ https://github.yandex-team.ru/tools/review-draft/commit/f06aa54 ]
 * return of fake sync                     [ https://github.yandex-team.ru/tools/review-draft/commit/d3b3eb7 ]
 * Make oebs sync works with oebs testing  [ https://github.yandex-team.ru/tools/review-draft/commit/68a695b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-08-27 09:35:11+00:00

1.500
-----
 * CIA-1730: approve lvl shows cur reviewer need to approve, not approved  [ https://github.yandex-team.ru/tools/review-draft/commit/bc2dbd3 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-07-29 12:55:14+00:00

1.499
-----
 * CIA-1698: add file import without marks  [ https://github.yandex-team.ru/tools/review-draft/commit/7c25781 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-07-25 13:32:39+00:00

1.498
-----
 * CIA-1698: add file import abs bonus  [ https://github.yandex-team.ru/tools/review-draft/commit/af0d9f7 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-07-17 07:51:28+00:00

1.497
-----
 * CIA-1718: add filtering by multiple scales  [ https://github.yandex-team.ru/tools/review-draft/commit/6782e52 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-07-09 10:03:09+00:00

1.496
-----
 * CIA-1718: add filtering by scale  [ https://github.yandex-team.ru/tools/review-draft/commit/58c7d84 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-07-08 13:24:59+00:00

1.495
-----
 * CIA-1723: fix delete last unapproved reviewer  [ https://github.yandex-team.ru/tools/review-draft/commit/1e44aa8 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-07-05 12:47:31+00:00

1.494
-----
 * CIA-1607: migrate only persons with salary  [ https://github.yandex-team.ru/tools/review-draft/commit/e705ac1 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-04-12 10:12:15+00:00

1.493
-----
 * CIA-1607: allow robot to read bonus for migration  [ https://github.yandex-team.ru/tools/review-draft/commit/bde7a05 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-04-12 08:34:50+00:00

1.492
-----
 * CIA-1607: add command to migrate abs bonuses                     [ https://github.yandex-team.ru/tools/review-draft/commit/f188f3f ]
 * CIA-1607: add borders for bonus absolute                         [ https://github.yandex-team.ru/tools/review-draft/commit/e8cb477 ]
 * CIA-1607: add action for absolute bonus; verbose for bonus_type  [ https://github.yandex-team.ru/tools/review-draft/commit/0407533 ]
 * CIA-1607: fix sending wrong bonus                                [ https://github.yandex-team.ru/tools/review-draft/commit/2565f8d ]
 * CIA-1607: fix views format and tests                             [ https://github.yandex-team.ru/tools/review-draft/commit/f19ddeb ]
 * CIA-1607: fix tests                                            [ https://github.yandex-team.ru/tools/review-draft/commit/ed72c9d ]
 * CIA-1607: add bonus type                                       [ https://github.yandex-team.ru/tools/review-draft/commit/255f8e5 ]
 * CIA-1607: migration                                              [ https://github.yandex-team.ru/tools/review-draft/commit/7e62fec ]
 * CIA-1607: add edit bonus if auto                                 [ https://github.yandex-team.ru/tools/review-draft/commit/71dade3 ]
 * CIA-1607: fix tests                                              [ https://github.yandex-team.ru/tools/review-draft/commit/8cda5d1 ]
 * CIA-1607: allow absolute bonus                                   [ https://github.yandex-team.ru/tools/review-draft/commit/2b49150 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-04-11 14:18:30+00:00

1.491
-----
 * CIA-1664: migration             [ https://github.yandex-team.ru/tools/review-draft/commit/edfe0bc ]
 * CIA-1664: add flagged positive  [ https://github.yandex-team.ru/tools/review-draft/commit/4788f56 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-03-28 08:38:53+00:00

1.490
-----
 * CIA-1658: fix calibration admin edit comment  [ https://github.yandex-team.ru/tools/review-draft/commit/babaa85 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-03-21 11:49:12+00:00

1.489
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1618: deduplicate approved users in notifications  [ https://github.yandex-team.ru/tools/review-draft/commit/eb15b83 ]
 * CIA-1655: trendox (#413)                               [ https://github.yandex-team.ru/tools/review-draft/commit/58fa827 ]

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * Update README.md  [ https://github.yandex-team.ru/tools/review-draft/commit/282f303 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-03-18 13:41:57+00:00

1.488
-----
 * CIA-1652: move to zookeeper  [ https://github.yandex-team.ru/tools/review-draft/commit/5600085 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-03-13 13:39:37+00:00

1.487
-----
 * CIA-1648: fix deduplication  [ https://github.yandex-team.ru/tools/review-draft/commit/e327003 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-02-22 17:35:24+00:00

1.486
-----
 * CIA-1626: fix incorrect staff sync  [ https://github.yandex-team.ru/tools/review-draft/commit/4586f01 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-02-22 11:53:08+00:00

1.485
-----
 * CIA-1648: fix roles dupes  [ https://github.yandex-team.ru/tools/review-draft/commit/ab25515 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2019-02-22 11:48:24+00:00

1.484
-----

* [Wladimir Spasskiy](http://staff/wlame@yandex-team.ru)

 * STAFF-10160 code review config  [ https://github.yandex-team.ru/tools/review-draft/commit/59aa11b ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * releasing version 1.483              [ https://github.yandex-team.ru/tools/review-draft/commit/5f9c433 ]
 * CIA-1627: fix unstable sort (#409)   [ https://github.yandex-team.ru/tools/review-draft/commit/9c66277 ]
 * CIA-1614: oebs can send login twice  [ https://github.yandex-team.ru/tools/review-draft/commit/fd20ead ]
 * CIA-1614: oebs can send login twice  [ https://github.yandex-team.ru/tools/review-draft/commit/a008823 ]

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * CIA-1593: Locke  [ https://github.yandex-team.ru/tools/review-draft/commit/7533871 ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2019-01-29 18:17:06+03:00

1.482
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CAB-475: add person review id to api  [ https://github.yandex-team.ru/tools/review-draft/commit/3497161 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * STAFF-10275 way to cloud mongo  [ https://github.yandex-team.ru/tools/review-draft/commit/81d51ea ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-12-07 12:26:05+03:00

1.481
-----
 * CIA-1442 & CIA-1586: extend person-review api  [ https://github.yandex-team.ru/tools/review-draft/commit/caf0d2c ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-11-28 12:39:14+03:00

1.480
-----
 * CIA-1559: fix comment notification link  [ https://github.yandex-team.ru/tools/review-draft/commit/cef18c7 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-11-16 12:28:17+03:00

1.479
-----
 * CIA-1583: fix create review without options_rsu_unit  [ https://github.yandex-team.ru/tools/review-draft/commit/9a9dbd1 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-10-31 13:44:18+03:00

1.478
-----
 * CIA-1579: add options rsu unit field  [ https://github.yandex-team.ru/tools/review-draft/commit/ab19dcb ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-10-25 11:24:05+03:00

1.477
-----
 * CIA-1562: add export comments  [ https://github.yandex-team.ru/tools/review-draft/commit/69738e0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-10-16 17:05:36+03:00

1.476
-----
 * CIA-1544: extend log oebs sync  [ https://github.yandex-team.ru/tools/review-draft/commit/40e7dc9 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-28 17:31:17+03:00

1.475
-----
 * CIA-1550: fix add calibration roles as regular participants (#396)  [ https://github.yandex-team.ru/tools/review-draft/commit/9fcdce9 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-27 16:56:03+03:00

1.474
-----
 * Upped psycopg version  [ https://github.yandex-team.ru/tools/review-draft/commit/6c52378 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-25 19:26:29+03:00

1.473
-----

* [Denis Podgorodnichenko](http://staff/denis-p@yandex-team.ru)

 * CIA-1537: Do not use pgbouncer (#390)  [ https://github.yandex-team.ru/tools/review-draft/commit/a0d6918 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-25 19:04:18+03:00

1.472
-----
 * CIA-1528: add logging  [ https://github.yandex-team.ru/tools/review-draft/commit/4a06ec0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-25 16:56:53+03:00

1.471
-----
 * CIA-1523: remove check comment     [ https://github.yandex-team.ru/tools/review-draft/commit/267c050 ]
 * CIA-1546: fix log auth middleware  [ https://github.yandex-team.ru/tools/review-draft/commit/bd259ad ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-25 15:20:57+03:00

1.470
-----
 * Fixed accidently broken test                         [ https://github.yandex-team.ru/tools/review-draft/commit/28177c5 ]
 * CIA-1452: fix workflow transaction                   [ https://github.yandex-team.ru/tools/review-draft/commit/dae54ec ]
 * CIA-1451: fix edit from calibration                  [ https://github.yandex-team.ru/tools/review-draft/commit/57d9e76 ]
 * CIA-1523: fix editing mark without changing comment  [ https://github.yandex-team.ru/tools/review-draft/commit/6bbabd2 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-24 16:14:14+03:00

1.469
-----
 * CIA-1531: add review scale id to "/mode-calibration/"  [ https://github.yandex-team.ru/tools/review-draft/commit/57036a7 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-21 16:57:19+03:00

1.468
-----
 * CIA-1538: Увеличить количество ресурсов и воркеров.  [ https://github.yandex-team.ru/tools/review-draft/commit/d65fbb3 ]

[Dmitry Prokofyev](http://staff/dmirain@yandex-team.ru) 2018-09-21 14:59:35+03:00

1.467
-----
 * CIA-1526: move celery syncs  [ https://github.yandex-team.ru/tools/review-draft/commit/2774fbf ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-19 14:20:10+03:00

1.466
-----
 * CIA-1526: reformat logging  [ https://github.yandex-team.ru/tools/review-draft/commit/9e53211 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-18 15:08:48+03:00

1.465
-----
 * CIA-1526: reformat logging  [ https://github.yandex-team.ru/tools/review-draft/commit/f2bc3b5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-18 13:03:57+03:00

1.464
-----
 * CIA-1526: reformat logging  [ https://github.yandex-team.ru/tools/review-draft/commit/a3f9854 ]
 * fix migration               [ https://github.yandex-team.ru/tools/review-draft/commit/409fd33 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-09-17 17:28:33+03:00

1.463
-----
 * CIA-1489: fix write to db excess reviewers changes due to unstable sort  [ https://github.yandex-team.ru/tools/review-draft/commit/03aa8f7 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-07-30 09:10:32+03:00

1.462
-----
 * CIA-1503: fix set empty mark  [ https://github.yandex-team.ru/tools/review-draft/commit/543bcbe ]
 * fix version number            [ https://github.yandex-team.ru/tools/review-draft/commit/c61f8ce ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-07-26 11:07:51+03:00

1.461
-----
 * CIA-1338: fix special marks                           [ https://github.yandex-team.ru/tools/review-draft/commit/7166a35 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-07-23 16:40:18+03:00

1.460
-----
 * CIA-1338: fix set review scale  [ https://github.yandex-team.ru/tools/review-draft/commit/c5b09b7 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-07-16 15:03:19+03:00

1.459
-----
 * CIA-1338: add special marks to const  [ https://github.yandex-team.ru/tools/review-draft/commit/3f124cf ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-07-06 14:46:58+03:00

1.458
-----
 * CIA-1388: add marks scales  [ https://github.yandex-team.ru/tools/review-draft/commit/e2e455d ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-07-06 13:51:18+03:00

1.457.1
-----
 * CIA-1491: fix link to person review in notifications  [ https://github.yandex-team.ru/tools/review-draft/commit/b0bd541 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-07-16 15:49:15+03:00

1.457
-----
 * Upgrade celery version  [ https://github.yandex-team.ru/tools/review-draft/commit/382f5de ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-07-04 15:31:54+03:00

1.456
-----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * WIKI-10978 Enable zero downtime migration usage  [ https://github.yandex-team.ru/tools/review-draft/commit/6a5b904 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1427: fix calibration_person_review_order            [ https://github.yandex-team.ru/tools/review-draft/commit/1a96e4b ]
 * CIA-1469: fix calculating salary change for export       [ https://github.yandex-team.ru/tools/review-draft/commit/763e6dd ]
 * CIA-1386: fix deleting excess roles while edit review    [ https://github.yandex-team.ru/tools/review-draft/commit/5a75f89 ]
 * CIA-1444: fix calibration roles is not used for actions  [ https://github.yandex-team.ru/tools/review-draft/commit/0fe48de ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-07-03 17:16:36+03:00

1.455
-----
 * CIA-1427: analyst has access to comments  [ https://github.yandex-team.ru/tools/review-draft/commit/50695ca ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-06-21 17:48:20+03:00

1.453
-----
 * CIA-1335: add hr analysts  [ https://github.yandex-team.ru/tools/review-draft/commit/035e673 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-06-20 12:54:08+03:00

1.452
-----
 * CIA-1459: fix fetching person_reviews for robot every time  [ https://github.yandex-team.ru/tools/review-draft/commit/7dc628e ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-06-09 15:00:12+03:00

1.451
-----
 * CIA-1459: add exporter role for oebs  [ https://github.yandex-team.ru/tools/review-draft/commit/7e88376 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-06-09 14:36:49+03:00

1.449
-----
 * CIA-1457: raised max parameters per request  [ https://github.yandex-team.ru/tools/review-draft/commit/35d7d69 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-06-01 14:31:21+03:00

1.448
-----
 * CIA-1460: increase timeout for request to fb up to 1 minute  [ https://github.yandex-team.ru/tools/review-draft/commit/91b28dc ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-31 17:02:21+03:00

1.447
-----
 * CIA-1290: fix include_dismissed_after_date is not editable  [ https://github.yandex-team.ru/tools/review-draft/commit/8786019 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-30 18:37:15+03:00

1.446
-----
 * CIA-1290: fix sql of fetching person heads  [ https://github.yandex-team.ru/tools/review-draft/commit/40d5474 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-30 14:42:49+03:00

1.445
-----
 * CIA-1290: fix staff sync  [ https://github.yandex-team.ru/tools/review-draft/commit/78c1bad ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-30 12:55:12+03:00

1.444
-----
 * CIA-1290: Allow to add to review dismissed persons  [ https://github.yandex-team.ru/tools/review-draft/commit/f39b515 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-29 14:30:00+03:00

1.443
-----
 * CIA-1438: add goldstar to /mode-calibration/                     [ https://github.yandex-team.ru/tools/review-draft/commit/7209864 ]
 * CIA-1371: fix bad bonus file throws 500                          [ https://github.yandex-team.ru/tools/review-draft/commit/58ec241 ]
 * Fix tests                                                        [ https://github.yandex-team.ru/tools/review-draft/commit/aa0788c ]
 * CIA-1380: add mark changes that aren't handled by notifications  [ https://github.yandex-team.ru/tools/review-draft/commit/5e30493 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-22 11:45:03+03:00

1.442
-----
 * fix using negative index in query  [ https://github.yandex-team.ru/tools/review-draft/commit/00ee746 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-11 15:10:20+03:00

1.441
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-590: Внедрить механизм межсервисной аутентификации TVM  [ https://github.yandex-team.ru/tools/review-draft/commit/7ddee32 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1478: add goodies to review details                                  [ https://github.yandex-team.ru/tools/review-draft/commit/1752ed8 ]
 * CIA-1076: global roles are not affecting most relevant review choice     [ https://github.yandex-team.ru/tools/review-draft/commit/b678dfe ]
 * CIA-1410: staff structure checks for update every 10 minutes             [ https://github.yandex-team.ru/tools/review-draft/commit/cef6d8b ]
 * CIA-1004: super reviewer can approve above his level in reviewers chain  [ https://github.yandex-team.ru/tools/review-draft/commit/41e9d45 ]
 * CIA-1420: calibrations actions answer is similar to person reviewes      [ https://github.yandex-team.ru/tools/review-draft/commit/8c24c94 ]
 * CIA-1420: only calibration admins can set discuss flag                   [ https://github.yandex-team.ru/tools/review-draft/commit/8a83834 ]
 * CIA-1376: add monitoring for unsent mails; retries now less frequent     [ https://github.yandex-team.ru/tools/review-draft/commit/39503f4 ]
 * CIA-1063: status actions now available only if transition is possible    [ https://github.yandex-team.ru/tools/review-draft/commit/5621358 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-11 14:42:03+03:00

1.440
-----
 * CIA-1429: check if field changed before checking action availability  [ https://github.yandex-team.ru/tools/review-draft/commit/08ffcd6 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-07 19:51:12+03:00

1.439
-----
 * CIA-1429: allow change money in status ANNOUNCED  [ https://github.yandex-team.ru/tools/review-draft/commit/b9f0dbf ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-07 17:29:31+03:00

1.438
-----
 * CIA-1429: allow change money in status ALLOW_ANNOUNCE  [ https://github.yandex-team.ru/tools/review-draft/commit/7322515 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-07 13:00:22+03:00

1.437
-----
 * Revert "Change csrf to exact domain on testing"  [ https://github.yandex-team.ru/tools/review-draft/commit/50b807e ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-03 20:03:03+03:00

0.436
-----
 * Change csrf to exact domain on testing  [ https://github.yandex-team.ru/tools/review-draft/commit/1caf4fb ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-05-03 19:09:06+03:00

0.435
-----
 * CIA-1284: отключить csrf для staff-structure-push (#347)  [ https://github.yandex-team.ru/tools/review-draft/commit/56ae88d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-26 19:13:44+03:00

0.434
-----
 * CIA-1421: Admin have to see calibration person reviews for drafts  [ https://github.yandex-team.ru/tools/review-draft/commit/ac39f3f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-26 15:18:40+03:00

0.433
-----
 * Отключить CSRF для анстейбла (#343)  [ https://github.yandex-team.ru/tools/review-draft/commit/32d7659 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-26 14:56:35+03:00

0.432
-----
 * CIA-1371: add 4000 if file is corrupted                                                                                                          [ https://github.yandex-team.ru/tools/review-draft/commit/a177048 ]
 * CIA-1241: adjusted calibration rights 1. Calibration person reviews list unavailable for drafts 2. Edit of calibration unavailable for archived  [ https://github.yandex-team.ru/tools/review-draft/commit/ac315c0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-25 20:21:50+03:00

0.431
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1401: only admin can see calibration drafts (#338)                  [ https://github.yandex-team.ru/tools/review-draft/commit/5a6e798 ]
 * CIA-1381: fix incorrect PersonReviewChange create for reviewers (#331)  [ https://github.yandex-team.ru/tools/review-draft/commit/8eb398d ]
 * CIA-1394: fix reviewers chains changes: (#336)                          [ https://github.yandex-team.ru/tools/review-draft/commit/3d96a47 ]

* [Elena Pravdina](http://staff/epravdina@yandex-team.ru)

 * CIA-1392: Поправить опечатку в письме (#337)  [ https://github.yandex-team.ru/tools/review-draft/commit/d04a6ee ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-25 19:35:34+03:00

0.430
-----
 * CIA-1284: Review 2.0 Отсутствует защита от CSRF атак (#327)  [ https://github.yandex-team.ru/tools/review-draft/commit/85b4822 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-25 19:27:17+03:00

0.429
-----
 * CIA-1416: extend options limit to 10kk  [ https://github.yandex-team.ru/tools/review-draft/commit/dbab901 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-24 20:50:06+03:00

0.428
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Подробности про сервис в README  [ https://github.yandex-team.ru/tools/review-draft/commit/1914dd1 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1415: extend import logging  [ https://github.yandex-team.ru/tools/review-draft/commit/aece3f7 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-24 17:52:42+03:00

0.427
-----
 * Renamed consts  [ https://github.yandex-team.ru/tools/review-draft/commit/0778f54 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-20 11:18:45+03:00

0.426
-----
 * Renamed calibrators_list to list_calibrators [ https://github.yandex-team.ru/tools/review-draft/commit/992011e ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-20 10:47:57+03:00

0.425
-----
 * CIA-1397: hide from log person review changes for archived reviews             [ https://github.yandex-team.ru/tools/review-draft/commit/eccaf61 ]
 * Revert "CIA-1376: add monitoring for unsent mails; retries now less frequent"  [ https://github.yandex-team.ru/tools/review-draft/commit/c454eb1 ]
 * CIA-1376: add monitoring for unsent mails; retries now less frequent           [ https://github.yandex-team.ru/tools/review-draft/commit/ff9d57b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-19 14:13:00+03:00

0.424
-----
 * CIA-1362: Миграция для Review.level_change_mode=AUTO  [ https://github.yandex-team.ru/tools/review-draft/commit/87d8ac3 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-17 17:12:01+03:00

0.423
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-1362: Дать верховному и суперревьюерам право менять автополя  [ https://github.yandex-team.ru/tools/review-draft/commit/d4c9f48 ]
 * New permissions for special cases                                 [ https://github.yandex-team.ru/tools/review-draft/commit/9ebca01 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-17 13:28:59+03:00

0.422
-----
 * CIA-1390: Доработать апи для кабинета  [ https://github.yandex-team.ru/tools/review-draft/commit/6dcc156 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-17 12:06:21+03:00

0.421
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1229: add errors to url "add-calibrators"                   [ https://github.yandex-team.ru/tools/review-draft/commit/91b2a44 ]
 * CIA-1360: Add check if comment is not empty while setting mark  [ https://github.yandex-team.ru/tools/review-draft/commit/b78eece ]
 * CIA-1229: make errors consistent                                [ https://github.yandex-team.ru/tools/review-draft/commit/487d782 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-17 11:53:28+03:00

0.420
-----
 * CIA-1306: Понять почему тупят POST на review.frontend.views.actions.ActionDetailView  [ https://github.yandex-team.ru/tools/review-draft/commit/63c697c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-17 11:51:42+03:00

0.419
-----
 * Fix SETTINGS_CELERY_ALWAYS_EAGER setting  [ https://github.yandex-team.ru/tools/review-draft/commit/0e78186 ]
 * More correct _get_affected_persons        [ https://github.yandex-team.ru/tools/review-draft/commit/ca2b0e6 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-17 11:47:33+03:00

0.418
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1261: Fix 403 on calibrators list for archived calibration (#317)  [ https://github.yandex-team.ru/tools/review-draft/commit/ce60139 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-17 11:46:30+03:00

0.417
-----
 * CIA-1382: Сделать менее жирные стенды (#326)  [ https://github.yandex-team.ru/tools/review-draft/commit/a460137 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-17 11:43:09+03:00

0.416
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1113: fix localization in calibrations  [ https://github.yandex-team.ru/tools/review-draft/commit/c8bae67 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-17 11:38:39+03:00

0.415
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1277: fix admin site: (#314)  [ https://github.yandex-team.ru/tools/review-draft/commit/48cfdf3 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-17 11:37:41+03:00

0.414
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Add stands deploy_hook  [ https://github.yandex-team.ru/tools/review-draft/commit/1ca40c5 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * Disable CORS for stands                                     [ https://github.yandex-team.ru/tools/review-draft/commit/1cb35b2 ]
 * removed api from stand name                                 [ https://github.yandex-team.ru/tools/review-draft/commit/bf2880f ]
 * Add "api" to stand name to exclude collision with frontend  [ https://github.yandex-team.ru/tools/review-draft/commit/b10a4f6 ]
 * CIA-1090: Fix not catching constraint err                   [ https://github.yandex-team.ru/tools/review-draft/commit/fcb0158 ]
 * CIA-1298: announce archived person reviews                  [ https://github.yandex-team.ru/tools/review-draft/commit/88d9093 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-13 12:47:47+03:00

0.413
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Fix stand image for other directories  [ https://github.yandex-team.ru/tools/review-draft/commit/693c200 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1372: enable django translation  [ https://github.yandex-team.ru/tools/review-draft/commit/56d41aa ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-09 15:56:23+03:00

0.412
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Fix settings for production env      [ https://github.yandex-team.ru/tools/review-draft/commit/cedfcaa ]
 * CORS enabled for test stands (#311)  [ https://github.yandex-team.ru/tools/review-draft/commit/e34f1fc ]
 * Refactored tests (#305)              [ https://github.yandex-team.ru/tools/review-draft/commit/5577518 ]
 * Поменял домен стендов (#309)         [ https://github.yandex-team.ru/tools/review-draft/commit/2d6d261 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * Dockefile layers optimization  [ https://github.yandex-team.ru/tools/review-draft/commit/6ea2296 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-09 14:15:03+03:00

0.411
-----
 * CIA-1189: fix errs format  [ https://github.yandex-team.ru/tools/review-draft/commit/ff4987f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-06 18:24:20+03:00

0.410
-----
 * CIA-1351: fix type errs  [ https://github.yandex-team.ru/tools/review-draft/commit/4d40796 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-06 17:57:55+03:00

0.409
-----
 * CIA-1369: add depratment to mode calibration  [ https://github.yandex-team.ru/tools/review-draft/commit/14c9beb ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-06 15:31:48+03:00

0.408
-----
 * CIA-1158: fix robot cannot set mark for archived review  [ https://github.yandex-team.ru/tools/review-draft/commit/d952048 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-05 18:50:22+03:00

0.407
-----
 * CIA-1195: Создать базу для анстейбла в PGAAS (#303)  [ https://github.yandex-team.ru/tools/review-draft/commit/cd23150 ]
 * CIA-1336: Поднять ещё стенд для тестирования (#300)  [ https://github.yandex-team.ru/tools/review-draft/commit/ffa28ff ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-05 13:01:48+03:00

0.406
-----
 * Fix robot login name  [ https://github.yandex-team.ru/tools/review-draft/commit/85461cf ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-04 12:03:55+03:00

0.405
-----
 * CIA-1352: 500 на рекомендации для калибровки, когда пустой список (#298)  [ https://github.yandex-team.ru/tools/review-draft/commit/a0d707a ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-03 18:33:54+03:00

0.404
-----
 * CIA-1275: Актуализировать доку про права (#296)  [ https://github.yandex-team.ru/tools/review-draft/commit/f58c507 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-03 16:52:01+03:00

0.403
-----
 * fix robot role and login  [ https://github.yandex-team.ru/tools/review-draft/commit/12c43e6 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-03 15:47:36+03:00

0.402
-----
 * CIA-11158: Need Person object, not auth                   [ https://github.yandex-team.ru/tools/review-draft/commit/dfea482 ]
 * Rename module due to name conflict with standard library  [ https://github.yandex-team.ru/tools/review-draft/commit/fe4de61 ]
 * Add missed migratio                                       [ https://github.yandex-team.ru/tools/review-draft/commit/988ffaf ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-03 15:03:51+03:00

0.401
-----
 * CIA-1158: fix migration  [ https://github.yandex-team.ru/tools/review-draft/commit/d91808e ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-03 12:23:28+03:00

0.400
-----
 * CIA-1158 & CIA-1159 : add subject_type for person log  [ https://github.yandex-team.ru/tools/review-draft/commit/2f9cec4 ]
 * CIA-1084: fix types                                    [ https://github.yandex-team.ru/tools/review-draft/commit/34529b8 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-04-02 12:18:07+03:00

0.399
-----
 * Fix if no feedback returns                                        [ https://github.yandex-team.ru/tools/review-draft/commit/629bf17 ]
 * CIA-1331: show fb's author in calibration if fb is not for group  [ https://github.yandex-team.ru/tools/review-draft/commit/39e9b5b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-30 16:16:10+03:00

0.398
-----
 * CIA-1346: Несоотвествие оценок в короткой и длинной истории (#293)  [ https://github.yandex-team.ru/tools/review-draft/commit/b6d5766 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-30 15:19:25+03:00

0.397
-----
 * CIA-1341: 502 при экспорте (#291)  [ https://github.yandex-team.ru/tools/review-draft/commit/3158bcf ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-29 16:44:10+03:00

0.396
-----
 * CIA-1325: Отключабельные по типам уведомления (#290)  [ https://github.yandex-team.ru/tools/review-draft/commit/9e7ee3b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-29 12:57:55+03:00

0.395
-----
 * CIA-1321: Добавил status=evaluation для wait_approval  [ https://github.yandex-team.ru/tools/review-draft/commit/c4c06f0 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-28 14:11:04+03:00

0.394
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-1270: Кронтаб celery работает по utc  [ https://github.yandex-team.ru/tools/review-draft/commit/3238ff5 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1330: fix mark_level_history for calibrations  [ https://github.yandex-team.ru/tools/review-draft/commit/f418a8e ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-28 12:54:00+03:00

0.393
-----
 * CIA-1319: Add new fields to ExtendedReviewSerializer  [ https://github.yandex-team.ru/tools/review-draft/commit/c15a978 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-27 14:14:51+03:00

0.392
-----
 * CIA-1321: Исправить ссылки в письме про напоминание  [ https://github.yandex-team.ru/tools/review-draft/commit/e8b8246 ]
 * CIA-1319: Отдавать оцениваемый период в ревью        [ https://github.yandex-team.ru/tools/review-draft/commit/b6edd91 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-27 12:46:52+03:00

0.391
-----
 * CIA-1318: history now contains 4 regular and last mid reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/ac5f3ba ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-27 10:41:31+03:00

0.390
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * django-idm-api==2.12.3  [ https://github.yandex-team.ru/tools/review-draft/commit/1bfc635 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1318: show history without year restriction   [ https://github.yandex-team.ru/tools/review-draft/commit/c9f8e8d ]
 * CIA-1285: add sort to calibration person reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/9a6f454 ]

* [romanyanke](http://staff/roman@yanke.ru)

 * fix 'evaluation' message  [ https://github.yandex-team.ru/tools/review-draft/commit/044d88c ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-26 14:49:07+03:00

0.389
-----

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1315: add calibration roles to /frontend/person-reviews/:id/comments  [ https://github.yandex-team.ru/tools/review-draft/commit/29e822f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-23 14:46:18+03:00

0.388
-----
 * CIA-1304: fix using mid review in calibration history  [ https://github.yandex-team.ru/tools/review-draft/commit/0c1d359 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-22 16:45:01+03:00

0.387
-----
 * CIA-1308: add calibration roles to /frontend/person/:login/log/  [ https://github.yandex-team.ru/tools/review-draft/commit/4183233 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-22 14:58:36+03:00

0.386
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Delete wat task                                [ https://github.yandex-team.ru/tools/review-draft/commit/b1feb64 ]
 * Fix feedback tests                             [ https://github.yandex-team.ru/tools/review-draft/commit/d37a17b ]
 * CIA-1295: Отключить миграции со старой версии  [ https://github.yandex-team.ru/tools/review-draft/commit/7079789 ]
 * CIA-1292: Скипаем отозванные отзывы            [ https://github.yandex-team.ru/tools/review-draft/commit/1caf602 ]
 * Fix changelog                                  [ https://github.yandex-team.ru/tools/review-draft/commit/bbb6c34 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1303: add reviewers roles to calibration  [ https://github.yandex-team.ru/tools/review-draft/commit/5fb69c5 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-21 19:27:38+03:00

0.385
-----
 * CIA-1301: add level_change to mark_level_history  [ https://github.yandex-team.ru/tools/review-draft/commit/ff62ac2 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-21 16:49:13+03:00

0.384
-----
 * CIA-1283: add calibration delete action  [ https://github.yandex-team.ru/tools/review-draft/commit/2318d5e ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-21 16:04:20+03:00

0.383
-----
 * CIA-1293: add filter level_changed  [ https://github.yandex-team.ru/tools/review-draft/commit/2f36688 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-21 15:53:23+03:00

0.382
-----

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-20 19:33:46+03:00

0.381
-----

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-20 19:29:47+03:00

0.380
-----
* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-1280: Более подробные access-логи   [ https://github.yandex-team.ru/tools/review-draft/commit/147c28f ]
 * Удаляем отправленные письма раз в день  [ https://github.yandex-team.ru/tools/review-draft/commit/42ef4e2 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1207: fix test for add calibrator notification  [ https://github.yandex-team.ru/tools/review-draft/commit/a2a5ac3 ]

* [romanyanke](http://staff/roman@yanke.ru)

 * CIA-1207: Письмо про калибровки (фронт)  [ https://github.yandex-team.ru/tools/review-draft/commit/f31c23c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-20 17:00:29+03:00

0.379
-----
 * Revert "CIA-1229: make errors consistent"  [ https://github.yandex-team.ru/tools/review-draft/commit/5ea6952 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-20 12:13:07+03:00

0.378
-----
 * CIA-1271: fix ordering of reviewers; fix frontend url for notifications  [ https://github.yandex-team.ru/tools/review-draft/commit/80840e7 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-19 20:24:57+03:00

0.377
-----
 * CIA-1264: создаем TOP_REVIEWER_INHERITED после выкатки нового кода  [ https://github.yandex-team.ru/tools/review-draft/commit/7027802 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-19 17:26:43+03:00

0.376
-----
 * CIA-1264: Финальный утверждающий должен видеть денежные данные в прошлом  [ https://github.yandex-team.ru/tools/review-draft/commit/92c2164 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-19 17:09:35+03:00

0.375
-----
 * CIA-1264: Ревьюеры не видят опционов, зарплаты и премий прошлых ревью  [ https://github.yandex-team.ru/tools/review-draft/commit/61f727a ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-19 16:10:12+03:00

0.374
-----
 * CIA-1264: Нет доступа к зарплатам у REVIEWER_INHERITED  [ https://github.yandex-team.ru/tools/review-draft/commit/66bdf83 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-19 14:38:08+03:00

0.373
-----
 * CIA-1264: Ревьюеры не имеют доступа к зарплате  [ https://github.yandex-team.ru/tools/review-draft/commit/d909758 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-19 14:02:31+03:00

0.372
-----
 * CIA-1229: make errors consistent  [ https://github.yandex-team.ru/tools/review-draft/commit/180aa55 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-19 11:27:21+03:00

0.371
-----
 * Show 404 only if object does not exists in db Added missing connection to wf.yandex-team.ru  [ https://github.yandex-team.ru/tools/review-draft/commit/92879d0 ]
 * CIA-1156: update review if some actions are disabled                                         [ https://github.yandex-team.ru/tools/review-draft/commit/c16c771 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-16 15:46:47+03:00

0.370
-----
 * CIA-1246: add separated url for history in calibration  [ https://github.yandex-team.ru/tools/review-draft/commit/81f3da5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-16 15:44:17+03:00

0.369
-----
 * CIA-1259: fix announce notify sends while notifies are turned off  [ https://github.yandex-team.ru/tools/review-draft/commit/2443bf1 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-16 14:36:05+03:00

0.368
-----
 * UWSGI_HARAKIRI environment variable  [ https://github.yandex-team.ru/tools/review-draft/commit/65db05c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-16 12:15:22+03:00

0.367
-----
 * CAB-336: Убрал экшны из api/person-reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/75d7b8b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-15 19:11:34+03:00

0.366
-----
 * fix type error: have to be list or tuple, not generator  [ https://github.yandex-team.ru/tools/review-draft/commit/c2bc44f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-15 17:08:27+03:00

0.365
-----
 * fix typo  [ https://github.yandex-team.ru/tools/review-draft/commit/770239b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-15 16:59:40+03:00

0.364
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * REVIEW-454: Убрать куки и токены из ответа ручек.  [ https://github.yandex-team.ru/tools/review-draft/commit/bb56b17 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1206: fix typo  [ https://github.yandex-team.ru/tools/review-draft/commit/a6e45dc ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-14 19:37:41+03:00

0.363
-----
 * CIA-1239: fix deleting everything from calibration roles  [ https://github.yandex-team.ru/tools/review-draft/commit/7e5195d ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-14 13:59:22+03:00

0.362
-----
 * Update admins must not delete calibrators   [ https://github.yandex-team.ru/tools/review-draft/commit/fa11913 ]
 * Validation error have to be passed to user  [ https://github.yandex-team.ru/tools/review-draft/commit/e05df4a ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-14 12:40:20+03:00

0.361
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-1226: 500 при нажатии обсудить в карточке калибровок  [ https://github.yandex-team.ru/tools/review-draft/commit/6c7c795 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1192: added Reply-to to emails      [ https://github.yandex-team.ru/tools/review-draft/commit/be05fef ]
 * CIA-1206: Add notifying calibrators     [ https://github.yandex-team.ru/tools/review-draft/commit/d3398ba ]
 * CIA-1222: add missing person filtering  [ https://github.yandex-team.ru/tools/review-draft/commit/cf0179b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-13 18:46:01+03:00

0.360
-----
 * Add /external/ path to CORS excludes  [ https://github.yandex-team.ru/tools/review-draft/commit/ea15613 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-07 16:21:57+03:00

0.359
-----
 * CIA-1194: post /frontend/calibration/:id/ can delete admins  [ https://github.yandex-team.ru/tools/review-draft/commit/8254fdf ]
 * CIA-1186: calibration creator does not see all calibrations  [ https://github.yandex-team.ru/tools/review-draft/commit/91b5ef0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-07 16:07:34+03:00

0.358
-----
 * CIA-1202: fix delete calibration person reviews: Filter by person_review.id while fetching from CalibrationPersonReview table is more effective and safe  [ https://github.yandex-team.ru/tools/review-draft/commit/3fb85e8 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-07 12:53:25+03:00

0.357
-----
 * CIA-1209: add missing fields to /calibrations/:id/mode-calibrations/  [ https://github.yandex-team.ru/tools/review-draft/commit/d603b04 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-07 11:47:15+03:00

0.356
-----
 * CIA-1194: extend calibration api with admins  [ https://github.yandex-team.ru/tools/review-draft/commit/862bc6b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-06 16:49:04+03:00

0.355
-----
 * CIA-1185: fix delete person reviews from calibration  [ https://github.yandex-team.ru/tools/review-draft/commit/1ec3f12 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-06 15:04:24+03:00

0.354
-----
 * fixed  [ https://github.yandex-team.ru/tools/review-draft/commit/b9d44be ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-06 14:10:42+03:00

0.353
-----
 * CIA-1188: add calibrators order: desc by adding datetime                  [ https://github.yandex-team.ru/tools/review-draft/commit/fad3a30 ]
 * CIA-1187: Add "add_to_calibration" action                                 [ https://github.yandex-team.ru/tools/review-draft/commit/13088d5 ]
 * CIA-1168: Add ordering for /frontend/calibrations/                        [ https://github.yandex-team.ru/tools/review-draft/commit/70bd8b7 ]
 * CIA-1184: denormalize roles after creating calibration and adding admins  [ https://github.yandex-team.ru/tools/review-draft/commit/a5085e1 ]
 * CIA-1145: Add wiki formatter to notifications                             [ https://github.yandex-team.ru/tools/review-draft/commit/bb1ccda ]
 * CIA-1156: merge import file urls into one                                 [ https://github.yandex-team.ru/tools/review-draft/commit/fe23b20 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-06 13:27:45+03:00

0.352
-----
 * Unstable now uses test db  [ https://github.yandex-team.ru/tools/review-draft/commit/65019e4 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-05 14:37:08+03:00

0.351
-----
 * Add post-method equals to get-method calibration/:id/mode-calibration/  [ https://github.yandex-team.ru/tools/review-draft/commit/921e594 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-02 14:45:18+03:00

0.350
-----
 * Fix grade history non-including start and stop dates  [ https://github.yandex-team.ru/tools/review-draft/commit/370b1da ]
 * CIA-1127: feedback as external component              [ https://github.yandex-team.ru/tools/review-draft/commit/27d1587 ]
 * CIA-1114: fix serialization                           [ https://github.yandex-team.ru/tools/review-draft/commit/8508fa6 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-03-02 14:13:05+03:00

0.349
-----
 * CIA-1154: Данные о ревьерах в калибровках  [ https://github.yandex-team.ru/tools/review-draft/commit/c11d3af ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-28 13:50:25+03:00

0.348
-----
 * Fix nested nested serializer case  [ https://github.yandex-team.ru/tools/review-draft/commit/d7ae715 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-28 13:38:51+03:00

0.347
-----
 * Fix dev settings name  [ https://github.yandex-team.ru/tools/review-draft/commit/827879e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-27 15:22:45+03:00

0.346
-----
 * Add MANIFEST.in for nested template dirs  [ https://github.yandex-team.ru/tools/review-draft/commit/8cd8144 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-27 15:15:14+03:00

0.345
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Fix test_stat.test_non_processed_change for *:01                  [ https://github.yandex-team.ru/tools/review-draft/commit/5a33020 ]
 * CIA-1131: Проверить добавление в фильтр сразу много логинов       [ https://github.yandex-team.ru/tools/review-draft/commit/8d97347 ]
 * CIA-1133: Забираем таймзоны пользователя из стаффа                [ https://github.yandex-team.ru/tools/review-draft/commit/8aa7298 ]
 * CIA-1154: Добавить данные для подсказок к статусам "...и еще..."  [ https://github.yandex-team.ru/tools/review-draft/commit/4c169f6 ]
 * cssutils==1.0.2 seem little broken                                [ https://github.yandex-team.ru/tools/review-draft/commit/67d1c0e ]
 * CIA-1133: Доработать бэкенд для писем
 * Test helpers for html inspect                                     [ https://github.yandex-team.ru/tools/review-draft/commit/cfea564 ]
 * CIA-1115: django-idm-api==2.12.2                                  [ https://github.yandex-team.ru/tools/review-draft/commit/200ac6d ]
 * CIA-1129: Дать права объявлять оценку всем ревьюерам              [ https://github.yandex-team.ru/tools/review-draft/commit/6fcaa9b ]
 * CIA-1106: Отдавать 404 вместо 403 на недоступное ревью            [ https://github.yandex-team.ru/tools/review-draft/commit/6edaa5d ]
 * CIA-1133: Добавил даты в моки reminder                            [ https://github.yandex-team.ru/tools/review-draft/commit/8ee2a4f ]
 * CIA-1119: Просроченные ссуды в ручке /api/v1/oebs/finance/        [ https://github.yandex-team.ru/tools/review-draft/commit/e8317ea ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-958: adjust calibration rights                                     [ https://github.yandex-team.ru/tools/review-draft/commit/be0769e ]
 * CIA-1102: add workflow actions unavailable for flagged person reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/bd65d37 ]

* [romanyanke](http://staff/roman@yanke.ru)

 * CIA-1112: Сверстать письма

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-27 14:25:59+03:00

0.344
-----
 * CIA-1120: PERSON_DEPARTMENT_CHAIN_NAMES для /reviews/:id/person-reviews/  [ https://github.yandex-team.ru/tools/review-draft/commit/b2b2656 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-19 16:52:11+03:00

0.343
-----
 * CIA-1120: Добавить данные для саджеста  [ https://github.yandex-team.ru/tools/review-draft/commit/e92bc22 ]
 * django_pgaas==0.4.0                     [ https://github.yandex-team.ru/tools/review-draft/commit/dc6a976 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-16 16:08:38+03:00

0.342
-----
 * CIA-1110: Fix reviewers filter for several reviewers on one lvl  [ https://github.yandex-team.ru/tools/review-draft/commit/b193ae6 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-02-15 12:57:59+03:00

0.341
-----
 * CIA-1105: Fix celery task name  [ https://github.yandex-team.ru/tools/review-draft/commit/9447872 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-02-13 14:27:56+03:00

0.340
-----
 * CIA-1096: Fix update excess roles  [ https://github.yandex-team.ru/tools/review-draft/commit/030d75d ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-02-13 11:21:27+03:00

0.339
-----
 * Fix bonus calculating  [ https://github.yandex-team.ru/tools/review-draft/commit/389452a ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-02-12 14:23:16+03:00

0.338
-----
 * CIA-1033: Fix get_calibration_person_reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/dc72df7 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-12 14:19:12+03:00

0.337
-----
 * CIA-1033: Forgotten calibration_id in CalibrationReview  [ https://github.yandex-team.ru/tools/review-draft/commit/d8e292e ]
 * CIA-1033: Serialize set as list                          [ https://github.yandex-team.ru/tools/review-draft/commit/040a091 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-12 14:11:09+03:00

0.336
-----
 * CIA-1042: extend subordination filter; add reviewer filter  [ https://github.yandex-team.ru/tools/review-draft/commit/eee61b4 ]
 * CIA-1046: fix roles denormalization for draft reviews       [ https://github.yandex-team.ru/tools/review-draft/commit/de5f048 ]
 * CIA-1065: migrate only non-archive reviews                  [ https://github.yandex-team.ru/tools/review-draft/commit/5d89f04 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-02-12 12:55:22+03:00

0.335
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-813: Запретить «объявлять» ревью с пустыми цепочками  [ https://github.yandex-team.ru/tools/review-draft/commit/e89caa5 ]
 * CIA-976: Вывод ошибок                                     [ https://github.yandex-team.ru/tools/review-draft/commit/b62d18e ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * fix merge  [ https://github.yandex-team.ru/tools/review-draft/commit/c170fc7 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-02-07 11:23:19+03:00

0.334
-----
 * fix const length  [ https://github.yandex-team.ru/tools/review-draft/commit/d60b6bc ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-02-06 17:17:40+03:00

0.333
-----
 * CIA-1091: add calibration creator role  [ https://github.yandex-team.ru/tools/review-draft/commit/8b1a731 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-02-06 17:02:55+03:00

0.332
-----
 * Fix test sb slave name  [ https://github.yandex-team.ru/tools/review-draft/commit/cda63b0 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-02 18:21:58+03:00

0.331
-----
 * CIA-1046: fix time comparison: need to compare with time, calculated AFTER query  [ https://github.yandex-team.ru/tools/review-draft/commit/0df1f50 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-02-02 11:41:26+03:00

0.330
-----
 * CIA-1073: fix chain update  [ https://github.yandex-team.ru/tools/review-draft/commit/49714e5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-02-01 11:13:08+03:00

0.329
-----
 * CIA-990: Добавить ссылку на подразделение в карточку  [ https://github.yandex-team.ru/tools/review-draft/commit/4020529 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-31 17:00:54+03:00

0.328
-----
 * CIA-1039: Fix first day of quarter code  [ https://github.yandex-team.ru/tools/review-draft/commit/8657ad2 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-31 15:22:30+03:00

0.327
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Поправил цикл по set, удаляющий из него элементы              [ https://github.yandex-team.ru/tools/review-draft/commit/6452161 ]
 * CIA-1077: Доступы суперревьюера должны применяться синхронно  [ https://github.yandex-team.ru/tools/review-draft/commit/3b6ff96 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1030: Add processed logins status  [ https://github.yandex-team.ru/tools/review-draft/commit/66e03d8 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-31 14:36:26+03:00

0.326
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-1028: Сделать престейбл RO           [ https://github.yandex-team.ru/tools/review-draft/commit/c303cc9 ]
 * CIA-1043: Fix reviewer role inheritance  [ https://github.yandex-team.ru/tools/review-draft/commit/4138cf5 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-959: add tests for /stat/ url                                                                                  [ https://github.yandex-team.ru/tools/review-draft/commit/ebd822e ]
 * CIA-1051: fix short history: always show last 2 marks from NORMAL reviews                                          [ https://github.yandex-team.ru/tools/review-draft/commit/b2599e0 ]
 * CIA-994: Fix export: Get city_name, fte. Remove reverse department chain. Change special values to empty strings.  [ https://github.yandex-team.ru/tools/review-draft/commit/4559238 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-30 16:23:09+03:00

0.325
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Поправил установку processed_at в StaffStructureChange  [ https://github.yandex-team.ru/tools/review-draft/commit/4b1abfc ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-959: remove auth from /stat/  [ https://github.yandex-team.ru/tools/review-draft/commit/041491f ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-29 18:02:17+03:00

0.324
-----
 * CIA-1056: Отделить запросы голс и фидбека от основного инстанса  [ https://github.yandex-team.ru/tools/review-draft/commit/81f1b13 ]
 * CIA-1039: Fix goals deadlines                                    [ https://github.yandex-team.ru/tools/review-draft/commit/8a2f607 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-29 15:07:05+03:00

0.323
-----
 * CIA-959: add monitoring url  [ https://github.yandex-team.ru/tools/review-draft/commit/34e0f0d ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-29 12:08:38+03:00

0.322
-----
 * CIA-974: fix fetch user's not announced reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/5fb741c ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-24 16:32:59+03:00

0.321
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-991: Объединить оценки B и B* для фильтрации (бэк)  [ https://github.yandex-team.ru/tools/review-draft/commit/d520f63 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-974: fix get most relevant review logic: There is most relevant id only if reviews list is not empty and there are not several active reviews.  [ https://github.yandex-team.ru/tools/review-draft/commit/82f0b6a ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-18 16:20:02+03:00

0.320
-----
 * CIA-997: Add hide superreviewrs and admins from user without access  [ https://github.yandex-team.ru/tools/review-draft/commit/fa19f12 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-18 10:37:49+03:00

0.319
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-1033: Починить трейсы из продакшна  [ https://github.yandex-team.ru/tools/review-draft/commit/2f7715f ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-1014: add fields to person-review-mode-history  [ https://github.yandex-team.ru/tools/review-draft/commit/4756f8d ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-17 12:20:12+03:00

0.318
-----
 * CIA-933: Split permission EDIT to EDIT, ADD_PERSONS, DELETE_PERSONS. Add changing chains of reviewers permission to superreviewer  [ https://github.yandex-team.ru/tools/review-draft/commit/20968c4 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-16 18:23:53+03:00

0.317
-----
 * CIA-1027: Ревьюеру недоступны ревью для роли  [ https://github.yandex-team.ru/tools/review-draft/commit/4a5a210 ]
 * dev.get_response для отладки                  [ https://github.yandex-team.ru/tools/review-draft/commit/02c784b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-16 18:03:26+03:00

0.316
-----
 * Fix Review.from_dict usage              [ https://github.yandex-team.ru/tools/review-draft/commit/9b3632a ]
 * CIA-996: Поправить права суперревьюера  [ https://github.yandex-team.ru/tools/review-draft/commit/ef89dcb ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-15 19:42:09+03:00

0.315
-----
 * CIA-974: add reviews ordering and returning most_relevant_id  [ https://github.yandex-team.ru/tools/review-draft/commit/b23fc5b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-15 19:14:37+03:00

0.314
-----
 * CIA-974: Add new status - finished review  [ https://github.yandex-team.ru/tools/review-draft/commit/2b710e8 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-12 15:31:40+03:00

0.313
-----
 * Upgrade cia_stuff version  [ https://github.yandex-team.ru/tools/review-draft/commit/04a6d30 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-11 18:47:02+03:00

0.312
-----
 * Fix deploy settings  [ https://github.yandex-team.ru/tools/review-draft/commit/347bc6b ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-11 17:53:33+03:00

0.311
-----
 * Add celery view to manually run tasks                                                                    [ https://github.yandex-team.ru/tools/review-draft/commit/d4ff9cd ]
 * CIA-1019: fix notification creation with side effect                                                     [ https://github.yandex-team.ru/tools/review-draft/commit/5bcb9a7 ]
 * CIA-998: add notification on unapprove event changed time of sending reminder about review to 10-00 MSK  [ https://github.yandex-team.ru/tools/review-draft/commit/19276e0 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2018-01-11 17:31:42+03:00

0.310
-----
 * Add env var SETTINGS_PERIOD_FOR_EMAILS_SEND  [ https://github.yandex-team.ru/tools/review-draft/commit/415be29 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-10 16:04:42+03:00

0.309
-----
 * Fix Exception: Email has no retry_counter  [ https://github.yandex-team.ru/tools/review-draft/commit/baf604c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-10 14:41:03+03:00

0.308
-----
 * DEBUG_EMAIL = 'cia-test@yandex-team.ru'                 [ https://github.yandex-team.ru/tools/review-draft/commit/9a7e1da ]
 * CIA-1010: Добавить type: "comment" в ответ …/comments/  [ https://github.yandex-team.ru/tools/review-draft/commit/c84ee83 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-10 13:39:37+03:00

0.307
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * django_pgaas==0.1.2  [ https://github.yandex-team.ru/tools/review-draft/commit/33e5440 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * CIA-951: adjusting notifications modified base.html for notifications - added footer and header login isn't a part of link to a person constructing emails not only by last 10 minutes  [ https://github.yandex-team.ru/tools/review-draft/commit/aa15160 ]
 * CIA-922: name is empty string by default for calibration                                                                                                                                [ https://github.yandex-team.ru/tools/review-draft/commit/c54144b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-10 13:08:23+03:00

0.306
-----
 * evaluation_*_date for Review admin  [ https://github.yandex-team.ru/tools/review-draft/commit/cf1ff55 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-09 17:07:31+03:00

0.305
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Поправил минимальную и максимальную зарплату  [ https://github.yandex-team.ru/tools/review-draft/commit/e6f0848 ]
 * CIA-1001: Пятисотит фильтр по подразделениям  [ https://github.yandex-team.ru/tools/review-draft/commit/e52e872 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * Fix duplicating itertools.count functionality  [ https://github.yandex-team.ru/tools/review-draft/commit/797144f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-09 15:52:25+03:00

0.304
-----
 * CIA-985: add "author" field to calibration details  [ https://github.yandex-team.ru/tools/review-draft/commit/611d821 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2017-12-27 15:51:57+03:00

0.303
-----
 * Fixed deleting person reviews from calibration: Need to delete by PersonReview.id instead of CalibrationPersonReview.id  [ https://github.yandex-team.ru/tools/review-draft/commit/8db6aec ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2017-12-27 15:12:56+03:00

0.302
-----
 * Fix type error in /frontend/calibrations/  [ https://github.yandex-team.ru/tools/review-draft/commit/8af02d5 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2017-12-26 13:55:50+03:00

0.301
-----
 * CIA-922: adjusted calibrations urls /frontend/calibrations/ POST now accepts <name>, <start_date>, <finish_date> /frontend/calibrations/:id/mode_calibration now returns:     person_review.status     person_review.action_at     person_review.person.position     person_review.person.chief  [ https://github.yandex-team.ru/tools/review-draft/commit/8eb71bf ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2017-12-25 18:57:45+03:00

0.300
-----

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2017-12-25 18:54:20+03:00

0.299
-----
 * Fix test staff empty gender handling  [ https://github.yandex-team.ru/tools/review-draft/commit/5270e44 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-22 16:38:45+03:00

0.298
-----
 * Fix celery launch  [ https://github.yandex-team.ru/tools/review-draft/commit/f464127 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-22 15:43:48+03:00

0.297
-----
 * CIA-968: Проверить отображение комментариев из старого сервиса в журнале  [ https://github.yandex-team.ru/tools/review-draft/commit/a2e185b ]
 * Update README.md                                                          [ https://github.yandex-team.ru/tools/review-draft/commit/1807c53 ]
 * Update README.md                                                          [ https://github.yandex-team.ru/tools/review-draft/commit/002e456 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-21 20:11:31+03:00

0.296
-----
 * CIA-957: split *_chain to *_chain_slugs and *_chain_names add person.department_chain_slugs to /frontend/reviews/:id/person_reviews/  [ https://github.yandex-team.ru/tools/review-draft/commit/0d89428 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2017-12-21 15:50:02+03:00

0.289
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-950: Лочится редактирование ревью при миграции  [ https://github.yandex-team.ru/tools/review-draft/commit/b872006 ]

* [Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru)

 * Fix shadowing celery package name                       [ https://github.yandex-team.ru/tools/review-draft/commit/8fd9941 ]
 * Fix excluding root path instead of self path            [ https://github.yandex-team.ru/tools/review-draft/commit/ca77258 ]
 * CIA-957: Add department_chain with slug to mode review  [ https://github.yandex-team.ru/tools/review-draft/commit/8cb5f50 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2017-12-20 17:38:52+03:00

0.288
-----
 * Improved calibrations admin  [ https://github.yandex-team.ru/tools/review-draft/commit/92ca164 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-19 20:04:54+03:00

0.287
-----
 * Merged with hotfix                 [ https://github.yandex-team.ru/tools/review-draft/commit/347e89c ]
 * Потерял STAFF_HOST/STAFF_PROTOCOL  [ https://github.yandex-team.ru/tools/review-draft/commit/ebe7e6f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-19 19:00:45+03:00

0.284
-----
 * CIA-903: Добавить сортировку валют/профессий в админку                            [ https://github.yandex-team.ru/tools/review-draft/commit/2bcd6fa ]
 * Fix replacing language from staff_person table if not found in headers or yauser  [ https://github.yandex-team.ru/tools/review-draft/commit/ff7f6e7 ]
 * CIA-954 add using language of subject to use translated version of fields         [ https://github.yandex-team.ru/tools/review-draft/commit/04ea789 ]

[Aleksandr Stovbyra](http://staff/shigarus@yandex-team.ru) 2017-12-19 17:50:27+03:00

0.283
-----
 * CIA-948: Починить фильтр по подразделениям  [ https://github.yandex-team.ru/tools/review-draft/commit/dfeb251 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-19 16:46:44+03:00

0.282
-----
 * Не работает фильтр по currency  [ https://github.yandex-team.ru/tools/review-draft/commit/9d74773 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-18 18:53:37+03:00

0.281
-----
 * GET /calibrations/:id/  [ https://github.yandex-team.ru/tools/review-draft/commit/d0c04c5 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-18 18:10:54+03:00

0.280.1
-----
 * Потерял STAFF_HOST/STAFF_PROTOCOL  [ https://github.yandex-team.ru/tools/review-draft/commit/2cbda55 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-19 18:38:13+03:00

0.280
-----
 * RestrictAccessMiddleware открыта на всех по дефолту  [ https://github.yandex-team.ru/tools/review-draft/commit/63c2209 ]
 * 600-secret.conf.local.example                        [ https://github.yandex-team.ru/tools/review-draft/commit/5cf6f74 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-18 15:33:21+03:00

0.279
-----
 * CAB-316: Разобраться почему на тесте не приходят данные по блоку "Options history"  [ https://github.yandex-team.ru/tools/review-draft/commit/c8010da ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-14 14:27:58+03:00

0.278
-----
 * Add DEBUG-LOGIN header auth for testing  [ https://github.yandex-team.ru/tools/review-draft/commit/bbf77da ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-14 13:13:03+03:00

0.277
-----
 * Fix calibrations list for review creators  [ https://github.yandex-team.ru/tools/review-draft/commit/b079dc8 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-14 12:35:27+03:00

0.276
-----
 * CIA-910: Вынес новые поля в админку  [ https://github.yandex-team.ru/tools/review-draft/commit/a803319 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-14 11:58:53+03:00

0.275
-----
 * Add ALLOWED_PATHS setting  [ https://github.yandex-team.ru/tools/review-draft/commit/f6de961 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-13 19:31:02+03:00

0.274
-----
 * Fix /v1/finance/ test fail  [ https://github.yandex-team.ru/tools/review-draft/commit/81b3708 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-13 19:06:20+03:00

0.273
-----
 * Default fields value for /v1/finance/  [ https://github.yandex-team.ru/tools/review-draft/commit/e80ce5e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-13 18:51:31+03:00

0.272
-----
 * Доработал обрезание финансовых данных для кабинета  [ https://github.yandex-team.ru/tools/review-draft/commit/08f20d7 ]
 * CIA-945: Refactored and added review create tests   [ https://github.yandex-team.ru/tools/review-draft/commit/5607fd1 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-13 17:59:18+03:00

0.271
-----
 * releasing version 0.270              [ https://github.yandex-team.ru/tools/review-draft/commit/e678b03 ]
 * Добавил notify-поля в ручку reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/c5d6ced ]
 * Move other frontend views            [ https://github.yandex-team.ru/tools/review-draft/commit/c3b3b83 ]
 * Move Calibration person reviews      [ https://github.yandex-team.ru/tools/review-draft/commit/de9847d ]
 * Moved views                          [ https://github.yandex-team.ru/tools/review-draft/commit/36d8f9f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-12 18:59:46+03:00

0.270
-----
 * Добавил notify-поля в ручку reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/3e8745b ]
 * Move stored_filters views            [ https://github.yandex-team.ru/tools/review-draft/commit/9c52c9d ]
 * Move structure_change view           [ https://github.yandex-team.ru/tools/review-draft/commit/c5fdb54 ]
 * Improve comment                      [ https://github.yandex-team.ru/tools/review-draft/commit/7ed055c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-12 18:04:08+03:00

0.269
-----
 * CIA-941: Тормозит /frontend/structure-changes/  [ https://github.yandex-team.ru/tools/review-draft/commit/751d45f ]
 * CIA-942: Ошибка при добавлении Воложа в ревью   [ https://github.yandex-team.ru/tools/review-draft/commit/e160736 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-12 16:14:26+03:00

0.268
-----
 * CIA-910: Поправить миграцию, записывать данные про опционы  [ https://github.yandex-team.ru/tools/review-draft/commit/547d3ab ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-11 19:42:23+03:00

0.267
-----
 * CIA-938: Учитывать «Слать уведомления суперревьюеру» в нотификациях  [ https://github.yandex-team.ru/tools/review-draft/commit/c701f5f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-11 17:22:21+03:00

0.266
-----
 * CIA-931: Поддержать типы ревью  [ https://github.yandex-team.ru/tools/review-draft/commit/5a80ef4 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-11 15:55:02+03:00

0.265
-----
 * Добавил тип ревью в mode-history  [ https://github.yandex-team.ru/tools/review-draft/commit/cf74fc3 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-11 15:17:29+03:00

0.264
-----
 * CIA-913: Настройка «Слать уведомления суперревьюеру»  [ https://github.yandex-team.ru/tools/review-draft/commit/f972e72 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-11 14:40:43+03:00

0.263
-----
 * Unused import                      [ https://github.yandex-team.ru/tools/review-draft/commit/cd9bb30 ]
 * More blank=True fields             [ https://github.yandex-team.ru/tools/review-draft/commit/2f8baa1 ]
 * blank=True for some Review fields  [ https://github.yandex-team.ru/tools/review-draft/commit/75a3fc8 ]
 * PEP-8                              [ https://github.yandex-team.ru/tools/review-draft/commit/fd858ea ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-07 18:49:16+03:00

0.262
-----
 * Add notification settings for Review in admin  [ https://github.yandex-team.ru/tools/review-draft/commit/f106b55 ]
 * CIA-902: Better admin                          [ https://github.yandex-team.ru/tools/review-draft/commit/5101aea ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-07 18:24:00+03:00

0.261
-----
 * CIA-902: Fix notification receivers  [ https://github.yandex-team.ru/tools/review-draft/commit/fec26f6 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-07 17:36:09+03:00

0.260
-----
 * CIA-902: Fix comments notification schedule  [ https://github.yandex-team.ru/tools/review-draft/commit/0320eee ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-07 17:12:43+03:00

0.259
-----
 * Event tasks reconfigured               [ https://github.yandex-team.ru/tools/review-draft/commit/a84e8b3 ]
 * CIA-902: Fix celery task return value  [ https://github.yandex-team.ru/tools/review-draft/commit/4d85b73 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-07 17:03:08+03:00

0.258
-----
 * CIA-902: Поправил баг в обработке нескольких changes  [ https://github.yandex-team.ru/tools/review-draft/commit/b045409 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-07 16:14:42+03:00

0.257
-----
 * CIA-902: Письма должны быть в статусе queued для отправки  [ https://github.yandex-team.ru/tools/review-draft/commit/9f95454 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-07 15:42:26+03:00

0.256
-----
 * CIA-902: Фикс ошибки админки писем  [ https://github.yandex-team.ru/tools/review-draft/commit/70e58a2 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-07 15:06:17+03:00

0.255
-----
 * CIA-902: Админка имейлов                               [ https://github.yandex-team.ru/tools/review-draft/commit/5adfebe ]
 * CIA-902: settings.DISABLE_EMAILS                       [ https://github.yandex-team.ru/tools/review-draft/commit/3b7c7a7 ]
 * releasing version 0.247.1                              [ https://github.yandex-team.ru/tools/review-draft/commit/ebfc773 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-07 14:52:23+03:00

0.254
-----
 * Forgotten comment notification celery conf  [ https://github.yandex-team.ru/tools/review-draft/commit/a1c93c2 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-06 19:41:19+03:00

0.253
-----
 * Remove unused templates.py                [ https://github.yandex-team.ru/tools/review-draft/commit/76f1f50 ]
 * Forgotten tpl files                       [ https://github.yandex-team.ru/tools/review-draft/commit/3d442c7 ]
 * Mark handled tasks that no need handling  [ https://github.yandex-team.ru/tools/review-draft/commit/c4d0327 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-06 19:34:54+03:00

0.252
-----
 * Better indexes             [ https://github.yandex-team.ru/tools/review-draft/commit/1cceb39 ]
 * CIA-902: Расписание задач  [ https://github.yandex-team.ru/tools/review-draft/commit/87f8a45 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-06 18:52:17+03:00

0.251
-----
 * CIA-902: Нотификации с нужными данными с примитивной версткой  [ https://github.yandex-team.ru/tools/review-draft/commit/060da6e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-06 18:15:14+03:00

0.250
-----
 * CIA-829: неправильный edit action для коммента  [ https://github.yandex-team.ru/tools/review-draft/commit/a1b7603 ]
 * Fix tests for currencies                        [ https://github.yandex-team.ru/tools/review-draft/commit/e9fa64f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-05 14:32:00+03:00

0.249
-----
 * CIA-681: миграция для дефолтных значений профессий и валют  [ https://github.yandex-team.ru/tools/review-draft/commit/279f512 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-05 12:48:43+03:00

0.248
-----
 * CIA-844: Фильтр: Валюта по умолчанию « ₽»       [ https://github.yandex-team.ru/tools/review-draft/commit/59aa52f ]
 * HTTP_ACCEPT_LANGUAGE also considered            [ https://github.yandex-team.ru/tools/review-draft/commit/0ecf721 ]
 * CIA-681: Собирать профессии для фильтра по ним  [ https://github.yandex-team.ru/tools/review-draft/commit/618d61e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-04 15:56:14+03:00

0.247.1
-----
 * CIA-929: Сломался пуш структуры из стаффа в продакшне  [ https://github.yandex-team.ru/tools/review-draft/commit/c815a62 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-12-07 13:49:10+03:00

0.247
-----
 * CIA-835: Доработать админку в продакшне  [ https://github.yandex-team.ru/tools/review-draft/commit/1ff3d4e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-28 13:00:07+03:00

0.246
-----
 * CIA-897: В фильтрах включать введённое значение в диапазон  [ https://github.yandex-team.ru/tools/review-draft/commit/1a8a945 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-27 16:34:34+03:00

0.245
-----
 * CIA-899: Добавить названия ревью в /frontend/person-reviews-mode-review/  [ https://github.yandex-team.ru/tools/review-draft/commit/a07fb38 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-27 15:40:46+03:00

0.244
-----
 * CIA-891: Присылать с бэкенда язык пользователя  [ https://github.yandex-team.ru/tools/review-draft/commit/d694cbf ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-23 17:44:06+03:00

0.243
-----
 * CIA-890: atomic for migration  [ https://github.yandex-team.ru/tools/review-draft/commit/3f7b075 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-23 15:26:56+03:00

0.242
-----
 * CIA-890: Пересечение id в старой и новой ревьюшнице  [ https://github.yandex-team.ru/tools/review-draft/commit/ea604c2 ]
 * Урлы для графиков                                    [ https://github.yandex-team.ru/tools/review-draft/commit/4d82e7e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-23 15:21:00+03:00

0.241
-----
 * CIA-883: Переехать на новую PGaaS базу  [ https://github.yandex-team.ru/tools/review-draft/commit/b585de3 ]
 * Update README                           [ https://github.yandex-team.ru/tools/review-draft/commit/26133a7 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-22 20:23:40+03:00

0.240
-----
 * CIA-876: Импорт суперревьюером не обновляет плюшки в авторежиме  [ https://github.yandex-team.ru/tools/review-draft/commit/6262c03 ]
 * Wiki markup generated code extended                              [ https://github.yandex-team.ru/tools/review-draft/commit/a57f390 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-21 18:34:14+03:00

0.239
-----
 * Fix wiki markup perms generation               [ https://github.yandex-team.ru/tools/review-draft/commit/1f56f55 ]
 * CIA-833: Пермишны для фильтра на ком действие  [ https://github.yandex-team.ru/tools/review-draft/commit/6ec5bee ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-21 14:47:10+03:00

0.238
-----
 * CIA-880: Вывести фильтры в админку  [ https://github.yandex-team.ru/tools/review-draft/commit/6bef9d4 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-20 20:21:28+03:00

0.237
-----
 * WARNING level for kazoo also  [ https://github.yandex-team.ru/tools/review-draft/commit/4808250 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-20 19:15:10+03:00

0.236
-----
 * Fix celery conf for tests  [ https://github.yandex-team.ru/tools/review-draft/commit/960425f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-20 18:56:00+03:00

0.235
-----
 * Common config in envconf.py  [ https://github.yandex-team.ru/tools/review-draft/commit/70ec1d0 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-20 17:59:39+03:00

0.234
-----
 * api+frontend for unstable deploying                                          [ https://github.yandex-team.ru/tools/review-draft/commit/4b10db7 ]
 * Moved debug celery tasks set                                                 [ https://github.yandex-team.ru/tools/review-draft/commit/a0ce697 ]
 * Fix TypeError: unsupported operand type(s) for +: 'int' and 'SPECIAL_VALUE'  [ https://github.yandex-team.ru/tools/review-draft/commit/0daee40 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-20 17:31:24+03:00

0.233
-----
 * Some tests and celery conf fixes                    [ https://github.yandex-team.ru/tools/review-draft/commit/c211e36 ]
 * LOGGINGL yenv: get_default_logger_conf('WARNING'),  [ https://github.yandex-team.ru/tools/review-draft/commit/90b695d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-20 17:16:07+03:00

0.232
-----
 * wat every 3 minutes  [ https://github.yandex-team.ru/tools/review-draft/commit/3716401 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-20 16:17:47+03:00

0.231
-----
 * CIA-836: Локи на периодические таски  [ https://github.yandex-team.ru/tools/review-draft/commit/1900794 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-20 16:04:05+03:00

0.230
-----
 * Fix mongo settings for other envs  [ https://github.yandex-team.ru/tools/review-draft/commit/f436915 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-20 14:41:11+03:00

0.229
-----
 * Отдельные конфиги монгобазы для анстейбла  [ https://github.yandex-team.ru/tools/review-draft/commit/9a1af1e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-20 14:29:16+03:00

0.228
-----
 * CIA-806: Долго выполняется запрос при сохранении карточки сотрудника  [ https://github.yandex-team.ru/tools/review-draft/commit/bba25f7 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-16 17:36:27+03:00

0.227
-----
 * CIA-822: Не переходит в статус Оценка, если оценка ставится импортом  [ https://github.yandex-team.ru/tools/review-draft/commit/1eb1482 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-16 15:33:10+03:00

0.226
-----
 * DISABLE_SERVER_SIDE_CURSORS for pgbouncer  [ https://github.yandex-team.ru/tools/review-draft/commit/11f5697 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-15 18:55:02+03:00

0.225
-----
 * Fix IS_PRODUCTION_DB setting  [ https://github.yandex-team.ru/tools/review-draft/commit/73ec901 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-15 18:01:53+03:00

0.224
-----
 * CIA-835: PersonReviewReaders > PersonReviewReader             [ https://github.yandex-team.ru/tools/review-draft/commit/6b27524 ]
 * CIA-835: включить создание глобальных ролей, пока мы без idm  [ https://github.yandex-team.ru/tools/review-draft/commit/e08d143 ]
 * CIA-835: для person_reviews спрятать статус и updated_at      [ https://github.yandex-team.ru/tools/review-draft/commit/67bf5f3 ]
 * CIA-835: не показывать werewolf в админке                     [ https://github.yandex-team.ru/tools/review-draft/commit/d7335a5 ]
 * CIA-835: Админка пятисотит для несаппортов                    [ https://github.yandex-team.ru/tools/review-draft/commit/27de4f8 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-15 16:57:12+03:00

0.223
-----
 * CIA-829: Добавить возможность отредактировать комментарий  [ https://github.yandex-team.ru/tools/review-draft/commit/0754c43 ]
 * Fix for fte                                                [ https://github.yandex-team.ru/tools/review-draft/commit/8fd8f7b ]
 * Extract comments views in module                           [ https://github.yandex-team.ru/tools/review-draft/commit/03b8dfb ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-15 15:23:14+03:00

0.222
-----
 * CIA-860: добавить в результаты /reviews/:id/person-reviews/ slug подразделения          [ https://github.yandex-team.ru/tools/review-draft/commit/b495a80 ]
 * CIA-851: добавить в результаты /person-reviews-mode-review/ информацию о подразделении  [ https://github.yandex-team.ru/tools/review-draft/commit/0a3cf03 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-14 12:01:01+03:00

0.221
-----
 * CIA-786: status в выгрузке           [ https://github.yandex-team.ru/tools/review-draft/commit/33c3882 ]
 * CIA-810: Добавить 2 поля в выгрузку  [ https://github.yandex-team.ru/tools/review-draft/commit/4444d9f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-14 11:22:52+03:00

0.220
-----
 * CIA-854: Починить ежедневную миграцию  [ https://github.yandex-team.ru/tools/review-draft/commit/8ddabbb ]
 * Unused import                          [ https://github.yandex-team.ru/tools/review-draft/commit/0723657 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-13 16:23:18+03:00

0.219
-----
 * Fix apply_mock  [ https://github.yandex-team.ru/tools/review-draft/commit/6c5829f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-02 20:00:29+03:00

0.218
-----
 * Fix FinanceAdmin error  [ https://github.yandex-team.ru/tools/review-draft/commit/f71699a ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-02 19:43:18+03:00

0.217
-----
 * CIA-824: Некорректное изменение при загрузке данных из файла  [ https://github.yandex-team.ru/tools/review-draft/commit/7b42a24 ]
 * Fix export for persons without departments                    [ https://github.yandex-team.ru/tools/review-draft/commit/01859af ]
 * Remove unused                                                 [ https://github.yandex-team.ru/tools/review-draft/commit/a3ee1f0 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-02 19:06:40+03:00

0.216
-----
 * Revert "Locks for celerybeat tasks"  [ https://github.yandex-team.ru/tools/review-draft/commit/08ea67d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-02 17:36:03+03:00

0.215
-----
 * Fix stupid typo  [ https://github.yandex-team.ru/tools/review-draft/commit/1aed3dd ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-02 17:11:12+03:00

0.214
-----
 * TMP staff sync every 5 minutes  [ https://github.yandex-team.ru/tools/review-draft/commit/ee53808 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-02 16:57:50+03:00

0.213
-----
 * @get_lock_or_do_nothing > @get_lock_or_do_nothing()  [ https://github.yandex-team.ru/tools/review-draft/commit/db9cce0 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-02 16:04:30+03:00

0.212
-----
 * Locks for celerybeat tasks  [ https://github.yandex-team.ru/tools/review-draft/commit/4592fe5 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-02 15:50:21+03:00

0.211
-----
 * Fix 500 for existing staff change  [ https://github.yandex-team.ru/tools/review-draft/commit/2720a2f ]
 * Дырка от _STAFF_PROD_NETS_         [ https://github.yandex-team.ru/tools/review-draft/commit/ec09fef ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-02 14:13:58+03:00

0.210
-----
 * CIA-826: Изменение уровня — входное значение для прогноза плюшек  [ https://github.yandex-team.ru/tools/review-draft/commit/bc7e311 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-01 19:54:59+03:00

0.209
-----
 * CIA-820: Не показывать черновики в списке ревью, если нет доступа редактировать их  [ https://github.yandex-team.ru/tools/review-draft/commit/d842cde ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-01 17:46:25+03:00

0.208
-----
 * CIA-776: Не отображаются отзывы и цели  [ https://github.yandex-team.ru/tools/review-draft/commit/3321950 ]
 * No exception for ids/feedback           [ https://github.yandex-team.ru/tools/review-draft/commit/db5fb59 ]
 * CIA-776: Лишние цели                    [ https://github.yandex-team.ru/tools/review-draft/commit/10aaca3 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-01 16:58:41+03:00

0.207
-----
 * Отсортировал список ревью  [ https://github.yandex-team.ru/tools/review-draft/commit/25f1976 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-01 15:40:34+03:00

0.206
-----
 * Fix для _get_grade_event  [ https://github.yandex-team.ru/tools/review-draft/commit/8addcd2 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-01 14:18:35+03:00

0.205
-----
 * CIA-827: В карточке для всех ревью показывается последний грейд и зп  [ https://github.yandex-team.ru/tools/review-draft/commit/dc0b0f6 ]
 * Default 0 for level in goodie                                         [ https://github.yandex-team.ru/tools/review-draft/commit/043ba32 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-11-01 13:23:33+03:00

0.204
-----
 * Fix migration chain for only self in approvers  [ https://github.yandex-team.ru/tools/review-draft/commit/131adc3 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-31 19:29:33+03:00

0.203
-----
 * Default value for level in Goodies  [ https://github.yandex-team.ru/tools/review-draft/commit/609811c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-31 19:17:52+03:00

0.202
-----
 * Fix goodies migration  [ https://github.yandex-team.ru/tools/review-draft/commit/93ccb87 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-31 18:41:36+03:00

0.201
-----
 * Fix migration for Goodies  [ https://github.yandex-team.ru/tools/review-draft/commit/8e9c48c ]
 * Upd README.md              [ https://github.yandex-team.ru/tools/review-draft/commit/3fbc85f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-31 17:27:40+03:00

0.200
-----
 * CORS hosts for prestable and production  [ https://github.yandex-team.ru/tools/review-draft/commit/326d193 ]
 * Fix repr for ReviewExtended              [ https://github.yandex-team.ru/tools/review-draft/commit/a75d739 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-31 16:55:52+03:00

0.199
-----
 * Test for prestable settings  [ https://github.yandex-team.ru/tools/review-draft/commit/3caab58 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-31 16:51:34+03:00

0.198
-----
 * CIA-809: Вкрутить временную проверку прав  [ https://github.yandex-team.ru/tools/review-draft/commit/6e60136 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-31 13:44:51+03:00

0.197
-----
 * CIA-808: Редактирование ревью доступно согласователю (бэк)  [ https://github.yandex-team.ru/tools/review-draft/commit/78d5281 ]
 * Описание пермишшнов в вики-разметке                         [ https://github.yandex-team.ru/tools/review-draft/commit/edcc874 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-30 19:30:04+03:00

0.196
-----
 * Remove old comment field  [ https://github.yandex-team.ru/tools/review-draft/commit/7b89bd9 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 19:32:09+03:00

0.195
-----
 * CIA-766: 500 при сохранении пустого фильтра  [ https://github.yandex-team.ru/tools/review-draft/commit/1b0f2f6 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 18:28:41+03:00

0.194
-----
 * CIA-754: Не работает фильтр по валюте  [ https://github.yandex-team.ru/tools/review-draft/commit/ba8b370 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 18:13:57+03:00

0.193
-----
 * CIA-753: Не работает фильтр по профессиям  [ https://github.yandex-team.ru/tools/review-draft/commit/285daf9 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 18:08:10+03:00

0.192
-----
 * CIA-756: 500 при выборе пользователя в требуется решение  [ https://github.yandex-team.ru/tools/review-draft/commit/9f2b6fd ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 18:04:06+03:00

0.191
-----
 * CIA-797: Анонсированный сотрудник не видит в своем ревью ничего  [ https://github.yandex-team.ru/tools/review-draft/commit/9f9e6e0 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 17:47:07+03:00

0.190
-----
 * CIA-786: Fix fte export  [ https://github.yandex-team.ru/tools/review-draft/commit/917196e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 17:18:22+03:00

0.189
-----
 * kotpy as admin in ALL reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/647e577 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 16:26:51+03:00

0.188
-----
 * Fix approve_level migration  [ https://github.yandex-team.ru/tools/review-draft/commit/22cd5c8 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 16:04:22+03:00

0.187
-----
 * Более частые синхронизации  [ https://github.yandex-team.ru/tools/review-draft/commit/0363c5d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 15:42:29+03:00

0.186
-----
 * Alter varchars to text in Person  [ https://github.yandex-team.ru/tools/review-draft/commit/d8200f7 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 15:29:31+03:00

0.185
-----
 * Add logging for staff_sync  [ https://github.yandex-team.ru/tools/review-draft/commit/f4b81aa ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 15:12:27+03:00

0.184
-----
 * CIA-549: Фиксы по миграции  [ https://github.yandex-team.ru/tools/review-draft/commit/541ac8e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 14:42:20+03:00

0.183
-----
 * CIA-700: необязательные администраторы  [ https://github.yandex-team.ru/tools/review-draft/commit/058e6be ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-27 12:59:36+03:00

0.182
-----
 * Доработки по статусам  [ https://github.yandex-team.ru/tools/review-draft/commit/f24b0d5 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-26 20:06:35+03:00

0.181
-----
 * CIA-786: Переделать формат выгрузки на совместимый со старым  [ https://github.yandex-team.ru/tools/review-draft/commit/2f94448 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-26 17:45:16+03:00

0.180
-----
 * URL_LOGIN_RE с минусом  [ https://github.yandex-team.ru/tools/review-draft/commit/a8fc715 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-26 12:34:35+03:00

0.179
-----
 * CIA-700: необязательные суперревьюеры  [ https://github.yandex-team.ru/tools/review-draft/commit/97abdec ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-25 16:47:14+03:00

0.178
-----
 * CIA-792: Пятисотка при сохранении карточки сотрудника из-за голдстаров  [ https://github.yandex-team.ru/tools/review-draft/commit/cf38048 ]
 * Some stuff moving                                                       [ https://github.yandex-team.ru/tools/review-draft/commit/bc0de3c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-25 14:18:07+03:00

0.177
-----
 * CIA-799: Убрать статус «Оценка» для безоценочных ревью  [ https://github.yandex-team.ru/tools/review-draft/commit/76ef634 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-24 17:46:18+03:00

0.176
-----
 * CIA-787: small bugfixes                   [ https://github.yandex-team.ru/tools/review-draft/commit/e218fe2 ]
 * CIA-787: approve_level  в ответе actions  [ https://github.yandex-team.ru/tools/review-draft/commit/9a0b832 ]
 * CIA-787: полные значения статусов в diff  [ https://github.yandex-team.ru/tools/review-draft/commit/a5031fd ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-24 15:06:55+03:00

0.175
-----
 * Remove unused code and field  [ https://github.yandex-team.ru/tools/review-draft/commit/ec20b2d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-23 19:44:30+03:00

0.174
-----
 * Fix migrations  [ https://github.yandex-team.ru/tools/review-draft/commit/66f4ce3 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-23 18:50:59+03:00

0.173
-----
 * Global role unique                       [ https://github.yandex-team.ru/tools/review-draft/commit/2b91cc5 ]
 * After merge fixes                        [ https://github.yandex-team.ru/tools/review-draft/commit/812abb5 ]
 * CIA-787: Разделить журнал и комменты     [ https://github.yandex-team.ru/tools/review-draft/commit/fafeb5c ]
 * unique together fro global roles         [ https://github.yandex-team.ru/tools/review-draft/commit/5ec0d38 ]
 * Удалил notification_counter для Changes  [ https://github.yandex-team.ru/tools/review-draft/commit/23292d9 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-23 18:44:56+03:00

0.172
-----
 * Little more logging  [ https://github.yandex-team.ru/tools/review-draft/commit/96fe99c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-23 12:43:24+03:00

0.171
-----
 * id & start_date for reviews in history  [ https://github.yandex-team.ru/tools/review-draft/commit/a1174d0 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-20 17:47:46+03:00

0.170
-----
 * ubuntu==16.04  [ https://github.yandex-team.ru/tools/review-draft/commit/96adfb9 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-20 15:51:51+03:00

0.169
-----
 * Не реверсить цепочки от стаффа  [ https://github.yandex-team.ru/tools/review-draft/commit/f656757 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-20 12:20:11+03:00

0.168
-----
 * id in updated  [ https://github.yandex-team.ru/tools/review-draft/commit/fbd6370 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-19 17:11:30+03:00

0.167
-----
 * Fix _get_chiefs_for_person  [ https://github.yandex-team.ru/tools/review-draft/commit/4e81dba ]
 * No know action chosen       [ https://github.yandex-team.ru/tools/review-draft/commit/aa34921 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-19 13:39:14+03:00

0.166
-----
 * unapprove for actions in form  [ https://github.yandex-team.ru/tools/review-draft/commit/ff5c836 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-18 18:42:27+03:00

0.165
-----
 * CIA-651: Два списка оценок для фронтенда  [ https://github.yandex-team.ru/tools/review-draft/commit/cf6d71c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-18 17:30:25+03:00

0.164
-----
 * CIA-746: Двигать approve_level на нужного апрувящего  [ https://github.yandex-team.ru/tools/review-draft/commit/2f0f343 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-18 17:00:10+03:00

0.163
-----
 * Add action unapprove  [ https://github.yandex-team.ru/tools/review-draft/commit/234a9d8 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-18 16:06:12+03:00

0.162
-----
 * CIA-745: миграция статусов  [ https://github.yandex-team.ru/tools/review-draft/commit/a864da4 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-18 15:07:58+03:00

0.161
-----
 * CIA-745: Добавить статусы person_review  [ https://github.yandex-team.ru/tools/review-draft/commit/8b9aa8a ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-18 14:22:36+03:00

0.160
-----
 * CIA-737: Оценка — обязательное поле  [ https://github.yandex-team.ru/tools/review-draft/commit/3a242f9 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-16 20:03:09+03:00

0.159
-----
  * Clean build

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-16 19:08:05+03:00

0.158
-----
 * Revert "CIA-737: Оценка — обязательное поле [бэкенд]"  [ https://github.yandex-team.ru/tools/review-draft/commit/73578d1 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-16 18:41:01+03:00

0.157
-----
 * POST для PersonReviewExportView  [ https://github.yandex-team.ru/tools/review-draft/commit/4284a50 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-16 17:59:37+03:00

0.156
-----
 * CIA-761: 500 на DELETE /frontend/stored-filters/:id/  [ https://github.yandex-team.ru/tools/review-draft/commit/bd98a35 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-16 14:44:20+03:00

0.155
-----
 * Add notify_events for ReviewExtended  [ https://github.yandex-team.ru/tools/review-draft/commit/41ebffc ]
 * Add test helper for http DELETE       [ https://github.yandex-team.ru/tools/review-draft/commit/b743702 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-16 13:30:22+03:00

0.154
-----
 * CIA-647: ошибка сериалзиции одноуровневых ревьюеров  [ https://github.yandex-team.ru/tools/review-draft/commit/c0b9f1e ]
 * Скипаем и логируем ошибки сериализации               [ https://github.yandex-team.ru/tools/review-draft/commit/6aac2ff ]
 * Конфигурация базы переменными окружения              [ https://github.yandex-team.ru/tools/review-draft/commit/2e39b18 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-16 12:38:39+03:00

0.153
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * gender для timeline  [ https://github.yandex-team.ru/tools/review-draft/commit/3380c18 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-743: Изменить пермишны редактирования ревьюеров  [ https://github.yandex-team.ru/tools/review-draft/commit/54f188d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-12 18:13:46+03:00

0.152
-----
 * fix                                        [ https://github.yandex-team.ru/tools/review-draft/commit/db365cc ]
 * CIA-633: Обязательный CORS на /frontend/*  [ https://github.yandex-team.ru/tools/review-draft/commit/f301d0d ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-12 15:25:15+03:00

0.151
-----
 * add actions to person reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/40d0e7d ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-12 14:38:27+03:00

0.150
-----
 * remainder notification type is not required  [ https://github.yandex-team.ru/tools/review-draft/commit/d09415e ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-12 14:11:27+03:00

0.149
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * some fixes                                    [ https://github.yandex-team.ru/tools/review-draft/commit/a3216ce ]
 * fix mark_level_history                        [ https://github.yandex-team.ru/tools/review-draft/commit/a4b3d00 ]
 * CIA-737: Оценка — обязательное поле [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/ad686c2 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-12 13:23:29+03:00

0.148
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-738: Хранить ивенты зарплат и грейдов отдельно с датами  [ https://github.yandex-team.ru/tools/review-draft/commit/6d2c0a5 ]
 * actions in person_review list                                [ https://github.yandex-team.ru/tools/review-draft/commit/16d324d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-12 11:25:19+03:00

0.147
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * fix serializable fields in views  [ https://github.yandex-team.ru/tools/review-draft/commit/8b159b9 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-11 20:04:42+03:00

0.146
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-721: Скорость ответа на большом ревью                                          [ https://github.yandex-team.ru/tools/review-draft/commit/36523e4 ]
 * CIA-721: Скорость ответа на большом ревью (fix oebs_utils)                         [ https://github.yandex-team.ru/tools/review-draft/commit/aff49c6 ]
 * CIA-721: Скорость ответа на большом ревью (fix permissions)                        [ https://github.yandex-team.ru/tools/review-draft/commit/592aff9 ]
 * CIA-721: Скорость ответа на большом ревью (fix setters)                            [ https://github.yandex-team.ru/tools/review-draft/commit/903565b ]
 * CIA-721: Скорость ответа на большом ревью (split read and write permissions)       [ https://github.yandex-team.ru/tools/review-draft/commit/293bcb4 ]
 * CIA-721: Скорость ответа на большом ревью (fix setters)                            [ https://github.yandex-team.ru/tools/review-draft/commit/09b1279 ]
 * CIA-721: Скорость ответа на большом ревью (remove args logging for small speedup)  [ https://github.yandex-team.ru/tools/review-draft/commit/74bbf4a ]
 * CIA-721: Скорость ответа на большом ревью (remove duplicate queries)               [ https://github.yandex-team.ru/tools/review-draft/commit/b7a6052 ]
 * CIA-735: Руководитель видит себя в списке сотрудников на ревью                     [ https://github.yandex-team.ru/tools/review-draft/commit/5f54bd5 ]
 * CIA-722: Доработать настройки нотификаций                                          [ https://github.yandex-team.ru/tools/review-draft/commit/df3879c ]
 * CIA-720: Доработки по добавлению людей в ревью                                     [ https://github.yandex-team.ru/tools/review-draft/commit/1473899 ]
 * CIA-693: Привести в порядок сериализацию                                           [ https://github.yandex-team.ru/tools/review-draft/commit/b4fca2b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-11 19:23:09+03:00

0.145
-----
 * NOT_CHANGED removed  [ https://github.yandex-team.ru/tools/review-draft/commit/6fb2965 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-10 15:48:17+03:00

0.144
-----
 * CIA-647: ? и - для проставления оценок  [ https://github.yandex-team.ru/tools/review-draft/commit/c19bded ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-10 12:51:20+03:00

0.143
-----
 * CIA-723: Возможно ретраить походы в pgaas        [ https://github.yandex-team.ru/tools/review-draft/commit/c40adb1 ]
 * CIA-719: Добавить данных в контекст логирования  [ https://github.yandex-team.ru/tools/review-draft/commit/bb94e37 ]
 * CIA-727: Сделать ручку finance-raw               [ https://github.yandex-team.ru/tools/review-draft/commit/85fd710 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-09 17:34:52+03:00

0.142
-----
 * fix person_review actions response fields  [ https://github.yandex-team.ru/tools/review-draft/commit/0831a3c ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-09 14:49:37+03:00

0.141
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Refactoring of already fixed bug  [ https://github.yandex-team.ru/tools/review-draft/commit/8ac0aac ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-715: Ограничения decimal/integer полей  [ https://github.yandex-team.ru/tools/review-draft/commit/faae483 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-06 13:52:29+03:00

0.140
-----
 * fix reviewers permissions check  [ https://github.yandex-team.ru/tools/review-draft/commit/9b64d01 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-04 18:13:18+03:00

0.139
-----

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-04 18:05:10+03:00

0.138
-----

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-04 18:00:59+03:00

0.137
-----
 * fix reviewers flattening  [ https://github.yandex-team.ru/tools/review-draft/commit/aaba045 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-04 17:59:57+03:00

0.136
-----
 * releasing version 0.135                       [ https://github.yandex-team.ru/tools/review-draft/commit/d1dc062 ]
 * Поправил ошибки при выставлении автозначений  [ https://github.yandex-team.ru/tools/review-draft/commit/9aab6a0 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-04 17:44:58+03:00

0.135
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Поправил ошибки при выставлении автозначений  [ https://github.yandex-team.ru/tools/review-draft/commit/9aab6a0 ]
 * CIA-686: fix for test                         [ https://github.yandex-team.ru/tools/review-draft/commit/6f0477b ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-686: Не видно добавления сотрудников в ревью  [ https://github.yandex-team.ru/tools/review-draft/commit/16dc05d ]
 * CIA-586: Сделать пермишны менее запутанными       [ https://github.yandex-team.ru/tools/review-draft/commit/8e843b1 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-10-04 17:44:28+03:00

0.134
-----
 * reset auto_increment fields after migration  [ https://github.yandex-team.ru/tools/review-draft/commit/ffc634b ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-03 17:18:42+03:00

0.133
-----

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-03 16:03:36+03:00

0.132
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Тест настроек для всех окружений  [ https://github.yandex-team.ru/tools/review-draft/commit/4987850 ]
 * Small tests improvements          [ https://github.yandex-team.ru/tools/review-draft/commit/32fff9d ]
 * test_api_idm formatting fixes     [ https://github.yandex-team.ru/tools/review-draft/commit/60938a6 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * fix                                          [ https://github.yandex-team.ru/tools/review-draft/commit/06db18f ]
 * fix admin views                              [ https://github.yandex-team.ru/tools/review-draft/commit/2543ad9 ]
 * CIA-697: Настраиваемые даты для нотификаций  [ https://github.yandex-team.ru/tools/review-draft/commit/b5ecf0f ]
 * CIA-621: Репликация базы                     [ https://github.yandex-team.ru/tools/review-draft/commit/a11e91b ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-03 15:37:47+03:00

0.131
-----
 * fix gender verbose  [ https://github.yandex-team.ru/tools/review-draft/commit/399a776 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-02 17:58:54+03:00

0.130
-----
 * CIA-691: Присылать gender вместе с пользователем  [ https://github.yandex-team.ru/tools/review-draft/commit/1146bd5 ]
 * fix person_review approve level                   [ https://github.yandex-team.ru/tools/review-draft/commit/6aa36a6 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-10-02 16:02:03+03:00

0.129
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Add RUB in currencies         [ https://github.yandex-team.ru/tools/review-draft/commit/20a0df8 ]
 * Delete unused _is_eveluation  [ https://github.yandex-team.ru/tools/review-draft/commit/ce3a6f3 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-620: Сделать окружение production  [ https://github.yandex-team.ru/tools/review-draft/commit/fd54e88 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-28 13:06:59+03:00

0.128
-----
 * CIA-647: Мелкие баги/задачи [бэкенд]         [ https://github.yandex-team.ru/tools/review-draft/commit/ccb7ae9 ]
 * CIA-689: Не сохраняется type, goldstar_mode  [ https://github.yandex-team.ru/tools/review-draft/commit/adfa842 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-27 19:13:20+03:00

0.127
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-549: Миграция данных [бэкенд] (production credentials)  [ https://github.yandex-team.ru/tools/review-draft/commit/c9afdb6 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-27 16:37:15+03:00

0.126
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-549: Миграция данных [бэкенд] comments  [ https://github.yandex-team.ru/tools/review-draft/commit/a5ebdbd ]
 * CIA-641: Ручка рекомендаций калибрующих     [ https://github.yandex-team.ru/tools/review-draft/commit/7644838 ]
 * CIA-620: Сделать окружение production       [ https://github.yandex-team.ru/tools/review-draft/commit/7767d5f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-27 14:09:43+03:00

0.125
-----

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-27 11:12:16+03:00

0.124
-----
 * fix user global roles              [ https://github.yandex-team.ru/tools/review-draft/commit/4d685cd ]
 * CIA-549: Миграция данных [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/b588c0b ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-27 10:59:04+03:00

0.123
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-658: Компонент api                      [ https://github.yandex-team.ru/tools/review-draft/commit/b3d1329 ]
 * Fix ReplicationMiddleware in settings_test  [ https://github.yandex-team.ru/tools/review-draft/commit/86651b9 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-655: Выдавать читателя и суперчитателя в админке                    [ https://github.yandex-team.ru/tools/review-draft/commit/bc61ce7 ]
 * fix person_review marks history                                         [ https://github.yandex-team.ru/tools/review-draft/commit/f5c1e59 ]
 * CIA-654: Ручки для отладки доступов                                     [ https://github.yandex-team.ru/tools/review-draft/commit/ed016f0 ]
 * CIA-653: Роли на калибровке CIA-652: Ручки добавления в калибровку      [ https://github.yandex-team.ru/tools/review-draft/commit/bea9f4a ]
 * CIA-642: Балк ручка для actions в калибровке                            [ https://github.yandex-team.ru/tools/review-draft/commit/ea0fcd1 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-26 16:20:20+03:00

0.122
-----
 * Admin forced master  [ https://github.yandex-team.ru/tools/review-draft/commit/f91b464 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-25 19:26:20+03:00

0.121
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-646: Хранить автора калибровок и ревью                           [ https://github.yandex-team.ru/tools/review-draft/commit/df8bf5a ]
 * CIA-635: Не разрешать саморуководительство в новой ревьюшнице        [ https://github.yandex-team.ru/tools/review-draft/commit/35ebd7c ]
 * CIA-649: Пробрасывать DEBUG_LOGIN при хождении в фидбечницу и goals  [ https://github.yandex-team.ru/tools/review-draft/commit/3c9ecdc ]
 * CIA-647: Мелкие баги/задачи [бэкенд]                                 [ https://github.yandex-team.ru/tools/review-draft/commit/8782b56 ]
 * CIA-651: Два списка оценок для фронтенда                             [ https://github.yandex-team.ru/tools/review-draft/commit/54c3f0c ]
 * CIA-640: Переименовать discuss >> flagged                            [ https://github.yandex-team.ru/tools/review-draft/commit/3cacb3a ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-20 22:19:25+03:00

0.120
-----
 * fix cors options  [ https://github.yandex-team.ru/tools/review-draft/commit/778c4a6 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-19 20:30:01+03:00

0.119
-----
 * CIA-633: Обязательный CORS на /frontend/*                                                                                                                                             [ https://github.yandex-team.ru/tools/review-draft/commit/1594770 ]
 * CIA-621: Репликация базы                                                                                                                                                              [ https://github.yandex-team.ru/tools/review-draft/commit/2be6cfe ]
 * CIA-599: Ручка списка калибруемых для режима калибровки [бэкенд] CIA-598: Ручка списка калибруемых для режима редактирования [бэкенд] CIA-602: Редактирование на калибровке [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/89d6fda ]
 * CIA-602: Редактирование на калибровке [бэкенд]                                                                                                                                        [ https://github.yandex-team.ru/tools/review-draft/commit/b61d7e6 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-19 18:18:48+03:00

0.118
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * OEBS sync fixes            [ https://github.yandex-team.ru/tools/review-draft/commit/4d5b82e ]
 * Fix production OEBS hosts  [ https://github.yandex-team.ru/tools/review-draft/commit/0e0ac91 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-633: Обязательный CORS на /frontend/*  [ https://github.yandex-team.ru/tools/review-draft/commit/e273043 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-19 16:28:03+03:00

0.117
-----
 * POST для /person-reviews-mode-review/  [ https://github.yandex-team.ru/tools/review-draft/commit/99786ca ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-18 17:50:54+03:00

0.116
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-623: Тесты на нотификации  [ https://github.yandex-team.ru/tools/review-draft/commit/e96a1d2 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-18 16:25:33+03:00

0.115
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-543: API для кабинета [бэкенд]: hr partnership  [ https://github.yandex-team.ru/tools/review-draft/commit/a3de5ea ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-18 16:21:02+03:00

0.114
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-628: Переменный список полей для /reviews/  [ https://github.yandex-team.ru/tools/review-draft/commit/3d188f4 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-18 16:15:50+03:00

0.113
-----
 * CORS для unstable  [ https://github.yandex-team.ru/tools/review-draft/commit/4cc0d0f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-15 16:13:33+03:00

0.112
-----
 * PERSON_POSITION и REVIEW_NAME в DEFAULT_FOR_REVIEWS_MODE_HISTORY  [ https://github.yandex-team.ru/tools/review-draft/commit/3edd923 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-15 15:48:52+03:00

0.111
-----
 * Revert "CIA-628: Переменный список полей для /reviews/"  [ https://github.yandex-team.ru/tools/review-draft/commit/edea38f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-15 14:40:26+03:00

0.110
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-530: Журнал и комменты [бэкенд] fix         [ https://github.yandex-team.ru/tools/review-draft/commit/24dd997 ]
 * CIA-628: Переменный список полей для /reviews/  [ https://github.yandex-team.ru/tools/review-draft/commit/18ad4c9 ]
 * CIA-539: Редактирование цепочек [бэкенд] fix    [ https://github.yandex-team.ru/tools/review-draft/commit/0b015bc ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-15 11:47:39+03:00

0.109
-----
  * rebuild
  
[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-14 16:53:37+03:00

0.108
-----
 * django-ids==0.8  [ https://github.yandex-team.ru/tools/review-draft/commit/13d8fba ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-14 16:34:27+03:00

0.107
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * add more person info for review admins and super reviewers  [ https://github.yandex-team.ru/tools/review-draft/commit/bcf302c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-13 16:56:14+03:00

0.106
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-558: Экшны для ревью fix  [ https://github.yandex-team.ru/tools/review-draft/commit/98dd8a5 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-13 16:13:19+03:00

0.105
-----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-539: Редактирование цепочек [бэкенд] fix  [ https://github.yandex-team.ru/tools/review-draft/commit/a28b428 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-13 15:14:34+03:00

0.104
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-587: Статус ревью в ручке reviews/<id>/        [ https://github.yandex-team.ru/tools/review-draft/commit/f22d035 ]
 * Для экшнов нужно собирать для всех статусов Ревью  [ https://github.yandex-team.ru/tools/review-draft/commit/371bfa9 ]
 * Разрешаем черновики для Admin и Superreviewer      [ https://github.yandex-team.ru/tools/review-draft/commit/4317f73 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-600: Ручка действий над калибровкой [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/ba2e296 ]
 * CIA-603: Выдача ролей на калибровку [бэкенд]      [ https://github.yandex-team.ru/tools/review-draft/commit/50a0c19 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-12 16:54:24+03:00

0.103
-----
 * 500 на редактирование цепочек #2  [ https://github.yandex-team.ru/tools/review-draft/commit/258b31f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-12 12:40:41+03:00

0.102
-----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * 500 на редактировании цепочек  [ https://github.yandex-team.ru/tools/review-draft/commit/8908dc9 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * rename reviewers chain bulk edit parameter position_person to person_to  [ https://github.yandex-team.ru/tools/review-draft/commit/f04ad36 ]
 * rename reviewers chain bulk edit parameter position_person to person_to  [ https://github.yandex-team.ru/tools/review-draft/commit/3792416 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-12 12:19:14+03:00

0.101
-----
 * add person review id at person reviews view  [ https://github.yandex-team.ru/tools/review-draft/commit/f1b85d4 ]
 * CIA-601: Список калибровок [бэкенд]          [ https://github.yandex-team.ru/tools/review-draft/commit/403c3f9 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-11 17:12:35+03:00

0.100
-----
 * fix celery dev hosts config  [ https://github.yandex-team.ru/tools/review-draft/commit/720a7ae ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-11 15:28:53+03:00

0.99
----
 * fix celery dev hosts config  [ https://github.yandex-team.ru/tools/review-draft/commit/a1a00c3 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-11 15:21:20+03:00

0.98
----

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-11 15:09:07+03:00

0.97
----
 * fix celery hosts config  [ https://github.yandex-team.ru/tools/review-draft/commit/b24be39 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-11 14:52:34+03:00

0.96
----
 * CIA-566: Переименование констант для редактирование цепочек  [ https://github.yandex-team.ru/tools/review-draft/commit/e7b586d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-11 14:01:07+03:00

0.95
----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-597: Ручка редактирования калибровки [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/e41f275 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-11 12:22:26+03:00

0.94
----

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-11 12:21:28+03:00

0.93
----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-547: Нотификации [бэкенд]                [ https://github.yandex-team.ru/tools/review-draft/commit/6aae7b1 ]
 * fix celery config                            [ https://github.yandex-team.ru/tools/review-draft/commit/327c195 ]
 * CIA-596: Ручка создания калибровки [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/5dae90b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-08 13:35:01+03:00

0.92
----
 * fix goldstar verbose  [ https://github.yandex-team.ru/tools/review-draft/commit/cd85330 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-07 17:51:49+03:00

0.91
----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * fix review admin delete view                            [ https://github.yandex-team.ru/tools/review-draft/commit/c01830e ]
 * STAFF-8277: Кабинет: перейти на ручки новой ревьюшницы  [ https://github.yandex-team.ru/tools/review-draft/commit/aa85690 ]
 * CIA-609: Добавить логин в логи                          [ https://github.yandex-team.ru/tools/review-draft/commit/87ae94c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-07 13:24:54+03:00

0.90
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Remove unused vars  [ https://github.yandex-team.ru/tools/review-draft/commit/6d28b02 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * add celery component to releaser config  [ https://github.yandex-team.ru/tools/review-draft/commit/e24b395 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-06 18:33:59+03:00

0.89
----
 * Не ходим в staff-api для werewolf  [ https://github.yandex-team.ru/tools/review-draft/commit/8cb3838 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-09-06 12:27:29+03:00

0.88
----

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-04 19:18:51+03:00

0.87
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Add modifiers                             [ https://github.yandex-team.ru/tools/review-draft/commit/522a95f ]
 * Новая версия assemble для person_reviews  [ https://github.yandex-team.ru/tools/review-draft/commit/6f5dc1d ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-591: Откат апрува                                                  [ https://github.yandex-team.ru/tools/review-draft/commit/9e933cb ]
 * CIA-548: Забирать из стаффа данные об изменениях с цепочками [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/60c1741 ]
 * CIA-546: Ручка загрузки денежных данных из бухгалтерии [бэкенд]        [ https://github.yandex-team.ru/tools/review-draft/commit/9a09309 ]
 * CIA-557: Наследование ролей [бэкенд]                                   [ https://github.yandex-team.ru/tools/review-draft/commit/d789ef5 ]
 * CIA-568: Celery                                                        [ https://github.yandex-team.ru/tools/review-draft/commit/4f99cee ]
 * CIA-537: Добавление сотрудников в ревью [бэкенд]                       [ https://github.yandex-team.ru/tools/review-draft/commit/529d7c7 ]
 * CIA-506: Админка [бэкенд]                                              [ https://github.yandex-team.ru/tools/review-draft/commit/4abd84f ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-09-04 19:18:15+03:00

0.86
----
 * CIA-568: Celery  [ https://github.yandex-team.ru/tools/review-draft/commit/dd32915 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-30 19:30:27+03:00

0.85
----
 * CIA-539: Редактирование цепочек [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/5217ee8 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-30 18:28:51+03:00

0.84
----
 * fix review status filter serialization add more person info at person review list  [ https://github.yandex-team.ru/tools/review-draft/commit/4767652 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-30 17:08:21+03:00

0.83
----
 * fix person add form  [ https://github.yandex-team.ru/tools/review-draft/commit/c533a60 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-29 19:12:38+03:00

0.82
----
 * add request debug logging  [ https://github.yandex-team.ru/tools/review-draft/commit/729c6ea ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-29 18:16:48+03:00

0.81
----
 * fix add persons form  [ https://github.yandex-team.ru/tools/review-draft/commit/40bec31 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-29 17:50:55+03:00

0.80
----
 * fix structure changes view  [ https://github.yandex-team.ru/tools/review-draft/commit/da64116 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-29 15:41:03+03:00

0.79
----
 * fix structure changes view  [ https://github.yandex-team.ru/tools/review-draft/commit/85e1576 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-29 15:37:02+03:00

0.78
----
 * CIA-537: Добавление сотрудников в ревью [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/e7b01d9 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-29 15:24:20+03:00

0.77
----
 * skip authentication for idm in werewolf middleware  [ https://github.yandex-team.ru/tools/review-draft/commit/61bdb68 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-29 12:51:12+03:00

0.76
----
 * skip authentication for idm  [ https://github.yandex-team.ru/tools/review-draft/commit/cb6c4ba ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-29 12:20:07+03:00

0.75
----
 * generator fixed                             [ https://github.yandex-team.ru/tools/review-draft/commit/f727747 ]
 * date вместо time в structure_change         [ https://github.yandex-team.ru/tools/review-draft/commit/7d42ef8 ]
 * person вместо login для type в persons-add  [ https://github.yandex-team.ru/tools/review-draft/commit/fc62983 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-29 12:01:59+03:00

0.74
----
 * add django idm api certificate middleware  [ https://github.yandex-team.ru/tools/review-draft/commit/6ea6f98 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-28 20:29:41+03:00

0.73
----
 * change idm-api version  [ https://github.yandex-team.ru/tools/review-draft/commit/a5767f3 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-28 19:56:21+03:00

0.72
----
 * Revert "change mongo db user"  [ https://github.yandex-team.ru/tools/review-draft/commit/1b32dca ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-28 19:50:52+03:00

0.71
----
 * change mongo db user     [ https://github.yandex-team.ru/tools/review-draft/commit/689049b ]
 * fix excel import/export  [ https://github.yandex-team.ru/tools/review-draft/commit/76e2f32 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-28 19:36:31+03:00

0.70
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * DISCUSS for some roles  [ https://github.yandex-team.ru/tools/review-draft/commit/9c84ee4 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-28 18:07:02+03:00

0.69.2
------

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-28 16:44:44+03:00

0.69.1
----

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-28 16:40:31+03:00

0.69
----

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-28 16:17:41+03:00

0.68
----
 * CIA-568: Celery                                                                                          [ https://github.yandex-team.ru/tools/review-draft/commit/28f9276 ]
 * CIA-507: Интеграция с IDM                                                                                [ https://github.yandex-team.ru/tools/review-draft/commit/e86e7e4 ]
 * CIA-567: Ручка выгрузки денежных данных CIA-546: Ручка загрузки денежных данных из бухгалтерии [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/684fa87 ]

[conyashka](http://staff/conyashka@yandex-team.ru) 2017-08-28 16:12:09+03:00

0.67
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Возвращаем обновленные данные в actions  [ https://github.yandex-team.ru/tools/review-draft/commit/fcd21a0 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-543: API для кабинета [бэкенд] (review stats)  [ https://github.yandex-team.ru/tools/review-draft/commit/e833ba2 ]
 * CIA-506: Админка [бэкенд] fix static files         [ https://github.yandex-team.ru/tools/review-draft/commit/bf1846c ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-24 19:08:25+03:00

0.66
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Tmp fix debug panel sql escape  [ https://github.yandex-team.ru/tools/review-draft/commit/fa2c65f ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-506: Админка [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/1d25284 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-24 15:45:55+03:00

0.65
----
 * allow_announce lost in serialization  [ https://github.yandex-team.ru/tools/review-draft/commit/ce1d2c9 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-24 15:16:39+03:00

0.64
----

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-24 14:56:12+03:00

0.63
----

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-24 14:49:17+03:00

0.62.1
----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-506: Админка [бэкенд]           [ https://github.yandex-team.ru/tools/review-draft/commit/eccfa67 ]
 * CIA-543: API для кабинета [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/e7fd124 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-24 14:11:23+03:00

0.61
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Fix auto goodies bug  [ https://github.yandex-team.ru/tools/review-draft/commit/6dde6b4 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-506: Админка [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/f31769f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-24 12:35:00+03:00

0.60
----
 * Fix get_goals signature  [ https://github.yandex-team.ru/tools/review-draft/commit/c1f651f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-23 11:49:09+03:00

0.59
----
 * CIA-498: Автоматически проставляемые ништяки  [ https://github.yandex-team.ru/tools/review-draft/commit/24208fa ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-22 21:31:57+03:00

0.58
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-498: добавил в _AUTO_ в actions  [ https://github.yandex-team.ru/tools/review-draft/commit/91a6c4c ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-574: Глобальные экшны в user                                       [ https://github.yandex-team.ru/tools/review-draft/commit/43dc77b ]
 * CIA-558: Экшны для ревью                                               [ https://github.yandex-team.ru/tools/review-draft/commit/19c69d2 ]
 * CIA-544: API для OEBS [бэкенд]                                         [ https://github.yandex-team.ru/tools/review-draft/commit/1d18dd0 ]
 * CIA-548: Забирать из стаффа данные об изменениях с цепочками [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/7977384 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-22 18:36:25+03:00

0.57
----
 * Починил пустой таймлайн  [ https://github.yandex-team.ru/tools/review-draft/commit/b6cab8b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-22 15:12:28+03:00

0.56
----
 * Staff improvements  [ https://github.yandex-team.ru/tools/review-draft/commit/2c63043 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-22 12:14:38+03:00

0.55
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * django-ids==0.6  [ https://github.yandex-team.ru/tools/review-draft/commit/174880e ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-558: Экшны для ревью  [ https://github.yandex-team.ru/tools/review-draft/commit/28d1630 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-22 10:41:36+03:00

0.54
----
 * django-ids==0.5  [ https://github.yandex-team.ru/tools/review-draft/commit/55712d2 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-21 21:18:01+03:00

0.53
----
 * django-ids==0.4  [ https://github.yandex-team.ru/tools/review-draft/commit/1f3a746 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-21 21:05:28+03:00

0.52
----
 * django-ids for git  [ https://github.yandex-team.ru/tools/review-draft/commit/c75e6f9 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-21 20:11:53+03:00

0.51
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * django-ids==0.3  [ https://github.yandex-team.ru/tools/review-draft/commit/110e930 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-557: Наследование ролей [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/7c7437d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-21 19:14:19+03:00

0.50
----
 * Токены для хождения в стафф и оебс  [ https://github.yandex-team.ru/tools/review-draft/commit/c887af3 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-21 18:06:36+03:00

0.49
----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-553: Список ревью [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/c03ce29 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-21 14:54:02+03:00

0.48
----
 * Revert to common cert  [ https://github.yandex-team.ru/tools/review-draft/commit/f4bc096 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 17:29:20+03:00

0.47
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * float/decimal incostitency                [ https://github.yandex-team.ru/tools/review-draft/commit/2679399 ]
 * Supereviewer can do actions at any stage  [ https://github.yandex-team.ru/tools/review-draft/commit/7dc9368 ]
 * Formatting                                [ https://github.yandex-team.ru/tools/review-draft/commit/ef963c0 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-553: Список ревью [бэкенд]                            [ https://github.yandex-team.ru/tools/review-draft/commit/c34adec ]
 * CIA-562: Ручка списка PersonReview для режима добавления  [ https://github.yandex-team.ru/tools/review-draft/commit/9446104 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 17:00:54+03:00

0.46
----
 * Decimal для salary_change и bonus в actions  [ https://github.yandex-team.ru/tools/review-draft/commit/825a6a3 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 15:24:08+03:00

0.45
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Не пятисотить, когда пользователя нет в базе  [ https://github.yandex-team.ru/tools/review-draft/commit/96bc37b ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-553: Список ревью [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/fb8b1f0 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 15:13:39+03:00

0.44
----
 * review_test для тестинга  [ https://github.yandex-team.ru/tools/review-draft/commit/02183ab ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 14:11:50+03:00

0.43
----
 * Add /etc/allCAs.pem in Dockerfile  [ https://github.yandex-team.ru/tools/review-draft/commit/b5b02c9 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 13:19:11+03:00

0.42
----
 * Stupid syntax error in settings  [ https://github.yandex-team.ru/tools/review-draft/commit/e9912b2 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 13:08:34+03:00

0.41
----
 * unstable DB_OPTIONS fixed  [ https://github.yandex-team.ru/tools/review-draft/commit/77a8429 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 13:04:48+03:00

0.40
----
 * unstable DB_PORT fixed  [ https://github.yandex-team.ru/tools/review-draft/commit/f58f3c1 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 12:59:58+03:00

0.39
----
 * Add pgaas settings  [ https://github.yandex-team.ru/tools/review-draft/commit/4b738a1 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 12:54:15+03:00

0.38
----
 * Add auth in every response  [ https://github.yandex-team.ru/tools/review-draft/commit/6edd845 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 12:30:37+03:00

0.37
----
 * Удаляю аутентификацию для Werewolf  [ https://github.yandex-team.ru/tools/review-draft/commit/6cf6e44 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 12:18:01+03:00

0.36
----
 * Обработка ошибка http-запросов  [ https://github.yandex-team.ru/tools/review-draft/commit/fc32086 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 12:10:41+03:00

0.35
----
 * Поправил get_ranges  [ https://github.yandex-team.ru/tools/review-draft/commit/235cf34 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-18 11:34:50+03:00

0.34
----
 * Испортил сериализацию таймлайна предыдущим фиксом  [ https://github.yandex-team.ru/tools/review-draft/commit/12d70d4 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-17 19:28:45+03:00

0.33
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-498: Результат action сериализуется как timeline  [ https://github.yandex-team.ru/tools/review-draft/commit/a0b2896 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-559: Поправить функциональные тесты  [ https://github.yandex-team.ru/tools/review-draft/commit/e750fcb ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-17 18:02:06+03:00

0.32
----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-562: Ручка списка PersonReview для режима добавления  [ https://github.yandex-team.ru/tools/review-draft/commit/409c158 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-17 15:04:14+03:00

0.31
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Дырки в ридми  [ https://github.yandex-team.ru/tools/review-draft/commit/7ba9636 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-539: Редактирование цепочек [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/72e1951 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-17 12:56:58+03:00

0.30
----
 * CIA-561: Доработка формы создания                      [ https://github.yandex-team.ru/tools/review-draft/commit/0d77f40 ]
 * CIA-552: Цели из голс & CIA-551: Отзывы из фидбечницы  [ https://github.yandex-team.ru/tools/review-draft/commit/68dbba0 ]
 * Rename modules                                         [ https://github.yandex-team.ru/tools/review-draft/commit/3defd6f ]
 * json is default content type                           [ https://github.yandex-team.ru/tools/review-draft/commit/6510e27 ]
 * Fix typo in module name                                [ https://github.yandex-team.ru/tools/review-draft/commit/f6aa995 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-16 18:27:22+03:00

0.29
----
 * disabled APPEND_SLASH  [ https://github.yandex-team.ru/tools/review-draft/commit/1502d75 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-15 10:24:58+03:00

0.28
----

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-497: Хранимые фильтры [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/18ae613 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-15 09:48:15+03:00

0.27
----
 * Фиксы таймлайна  [ https://github.yandex-team.ru/tools/review-draft/commit/60caceb ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-14 19:55:27+03:00

0.26
----
 * Поправил сериализацию данных  [ https://github.yandex-team.ru/tools/review-draft/commit/7a7df78 ]
 * Криво смержил урлы            [ https://github.yandex-team.ru/tools/review-draft/commit/8767984 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-14 18:50:13+03:00

0.25
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-530: Журнал и комменты   [ https://github.yandex-team.ru/tools/review-draft/commit/88e66d5 ]
 * Fix 500 for anonymous users  [ https://github.yandex-team.ru/tools/review-draft/commit/4a818f6 ]

* [conyashka](http://staff/conyashka@yandex-team.ru)

 * CIA-538: Удаление сотрудников из ревью [бэкенд]          [ https://github.yandex-team.ru/tools/review-draft/commit/1f2796b ]
 * CIA-537: Добавление сотрудников в ревью [бэкенд]         [ https://github.yandex-team.ru/tools/review-draft/commit/1214484 ]
 * CIA-536: Ручка создания и редактирования ревью [бэкенд]  [ https://github.yandex-team.ru/tools/review-draft/commit/e28cded ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-14 18:23:45+03:00

0.24
----
 * Deps filter should accept slug not id  [ https://github.yandex-team.ru/tools/review-draft/commit/0b1d31e ]
 * Flat actions list                      [ https://github.yandex-team.ru/tools/review-draft/commit/72a0223 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-11 11:16:36+03:00

0.23
----
 * get & post for person-reviews with filters  [ https://github.yandex-team.ru/tools/review-draft/commit/f181033 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-09 16:32:52+03:00

0.22
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * CIA-533: Ручки для экшнов над ревьюируемым  [ https://github.yandex-team.ru/tools/review-draft/commit/414477d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-09 15:58:54+03:00

0.21
----
 * Add CORS  [ https://github.yandex-team.ru/tools/review-draft/commit/6ff2eb2 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-08 15:30:57+03:00

0.20
----
 * is_staff for everyone  [ https://github.yandex-team.ru/tools/review-draft/commit/52cd96d ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-04 18:52:47+03:00

0.19
----
 * Everyone is superuser  [ https://github.yandex-team.ru/tools/review-draft/commit/7075dce ]
 * Fix release.hjson      [ https://github.yandex-team.ru/tools/review-draft/commit/2a87261 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-04 18:47:27+03:00

0.18
----
 * Refactored base forms classes  [ https://github.yandex-team.ru/tools/review-draft/commit/d84a73b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-04 17:00:38+03:00

0.17
----
 * Serialize only requested fields  [ https://github.yandex-team.ru/tools/review-draft/commit/5be6d5b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-04 15:03:15+03:00

0.16
----
 * Small fixes  [ https://github.yandex-team.ru/tools/review-draft/commit/47f6d79 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-04 14:50:51+03:00

0.15
----
 * Параметр filters  [ https://github.yandex-team.ru/tools/review-draft/commit/4370bdd ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-04 14:17:03+03:00

0.14
----
 * CIA-532: Список экшнов для ревьюируемого  [ https://github.yandex-team.ru/tools/review-draft/commit/6c22d67 ]
 * CIA-495: Пермишны для полей ревьюируемых  [ https://github.yandex-team.ru/tools/review-draft/commit/4b9d97e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-08-03 18:03:18+03:00

0.13
----
 * static-map for django-admin  [ https://github.yandex-team.ru/tools/review-draft/commit/1d54097 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-24 15:07:46+03:00

0.12
----
 * CIA-529: Ручка с данными пользователя  [ https://github.yandex-team.ru/tools/review-draft/commit/0607314 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-21 19:50:39+03:00

0.11
----
 * Fix default for persons-review-history  [ https://github.yandex-team.ru/tools/review-draft/commit/131bf64 ]
 * CIA-498: Карточка ревьюируемого         [ https://github.yandex-team.ru/tools/review-draft/commit/d7a2971 ]
 * Fix prgrs typo                          [ https://github.yandex-team.ru/tools/review-draft/commit/8a681e2 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-21 16:39:26+03:00

0.10
----
 * needs_discuss > discuss  [ https://github.yandex-team.ru/tools/review-draft/commit/1481550 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-20 12:55:19+03:00

0.9
---
 * УБрал ненужные department-поля  [ https://github.yandex-team.ru/tools/review-draft/commit/3c8715f ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-19 21:05:35+03:00

0.8
---
 * Вернул salary:{}  [ https://github.yandex-team.ru/tools/review-draft/commit/4b9f521 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-19 21:04:30+03:00

0.7
---
 * level_change is flat too    [ https://github.yandex-team.ru/tools/review-draft/commit/1cc24c4 ]
 * lib package                 [ https://github.yandex-team.ru/tools/review-draft/commit/5734051 ]
 * Fucking gitignore with lib  [ https://github.yandex-team.ru/tools/review-draft/commit/58b81f1 ]
 * Teamcity testrun            [ https://github.yandex-team.ru/tools/review-draft/commit/872b954 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-19 20:54:57+03:00

0.6
---
 * CIA-496: Фильтры ревьируемых                      [ https://github.yandex-team.ru/tools/review-draft/commit/d66279e ]
 * CIA-494: Формирование полей ревьюируемых (тесты)  [ https://github.yandex-team.ru/tools/review-draft/commit/88c975b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-19 19:34:42+03:00

0.5
---
 * cia-stuff==1.0.7       [ https://github.yandex-team.ru/sibirev/review-draft/commit/7568a6b ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-06 19:45:28+03:00

0.4
---
 * Fix DB_HOST fallback  [ https://github.yandex-team.ru/sibirev/review-draft/commit/a363b9e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-06 17:48:20+03:00

0.3
---
 * yenv==0.8  [ https://github.yandex-team.ru/sibirev/review-draft/commit/40201cd ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-06 17:23:09+03:00

0.2
---
 * CIA-494: Формирование полей ревьюируемых     [ https://github.yandex-team.ru/sibirev/review-draft/commit/3ab6ef7 ]
 * CIA-517: Прототип синка с оебс               [ https://github.yandex-team.ru/sibirev/review-draft/commit/2a51ee4 ]
 * CIA-506: Драфт админки                       [ https://github.yandex-team.ru/sibirev/review-draft/commit/61fe76b ]
 * CIA-501: Рандомайзеры для данных             [ https://github.yandex-team.ru/sibirev/review-draft/commit/0880359 ]
 * CIA-501: Фейковые данные для тестирования    [ https://github.yandex-team.ru/sibirev/review-draft/commit/fbe3893 ]
 * CIA-504: Прототип синхронизации со стаффом   [ https://github.yandex-team.ru/sibirev/review-draft/commit/1066454 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-06 17:04:51+03:00

0.1
---

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-05-26 20:50:17+03:00

irev/review-draft/commit/1066454 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-07-06 17:04:51+03:00

0.1
---

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-05-26 20:50:17+03:00

1+03:00

0.1
---

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2017-05-26 20:50:17+03:00

