141.80
------
 * IDM-12508 Отключаем bulk ручку  [ https://a.yandex-team.ru/arc/commit/9775045 ]

[smosker](http://staff/smosker) 2022-07-26 19:04:41+03:00

141.79
------

* [mmarat248](http://staff/mmarat248)

 * IDM-12254: fix sandbox approver  [ https://a.yandex-team.ru/arc/commit/9767412 ]

[smosker](http://staff/smosker) 2022-07-25 16:13:28+03:00

141.78
------

* [mmarat248](http://staff/mmarat248)

 * IDM-12437: add failed-review-roles monitoring        [ https://a.yandex-team.ru/arc/commit/9758601 ]
 * IDM-12226: fix appMetrica application key            [ https://a.yandex-team.ru/arc/commit/9757690 ]
 * IDM-12254: fix UserWrapper                           [ https://a.yandex-team.ru/arc/commit/9756989 ]
 * IDM-12429: add errors description                    [ https://a.yandex-team.ru/arc/commit/9754022 ]
 * IDM-11502: add setting to onhold state on exception  [ https://a.yandex-team.ru/arc/commit/9753128 ]

[smosker](http://staff/smosker) 2022-07-22 14:43:02+03:00

141.77
------

* [smosker](http://staff/smosker)

 * ABC-13356 Ручка со списком ролей для абц сервиса              [ https://a.yandex-team.ru/arc/commit/9749847 ]
 * IDM-12448 Возвращаем tvm как способ авторизации по умолчанию  [ https://a.yandex-team.ru/arc/commit/9725323 ]

* [mmarat248](http://staff/mmarat248)

 * IDM-11988: add request_type field to RoleForm         [ https://a.yandex-team.ru/arc/commit/9746102 ]
 * IDM-12226: fix mapping

IDM-12226: fix mapping        [ https://a.yandex-team.ru/arc/commit/9739142 ]
 * IDM-12226: add app_name to Appmetrica role responses  [ https://a.yandex-team.ru/arc/commit/9737781 ]

[smosker](http://staff/smosker) 2022-07-20 23:34:42+03:00

141.76
------

* [mmarat248](http://staff/mmarat248)

 * IDM-12254: prevent timeout with a large number of confirmers  [ https://a.yandex-team.ru/arc/commit/9722576 ]

* [smosker](http://staff/smosker)

 * VIEWER-945 Фикс названия бакета  [ https://a.yandex-team.ru/arc/commit/9721845 ]

[smosker](http://staff/smosker) 2022-07-14 17:50:44+03:00

141.75
------

* [smosker](http://staff/smosker)

 * VIEWER-945 Получаем роли в Webauth через S3-MDS  [ https://a.yandex-team.ru/arc/commit/9720473 ]

* [kir-choo](http://staff/kir-choo)

 * IDM-12124: Поправил формирование поискового запроса для FTS по RoleNode

[RUN LARGE TESTS]  [ https://a.yandex-team.ru/arc/commit/9720237 ]

[smosker](http://staff/smosker) 2022-07-14 14:14:55+03:00

141.74
------

* [smosker](http://staff/smosker)

 * Revert "IDM-12254: prevent timeout with a large number of confirmers"

This reverts commit 4f9972df45ee90d4d9677226cbb1ac964e4951c6, reversing
changes made to 071a688feef2f9af3c40746f720cf48acb265d42.  [ https://a.yandex-team.ru/arc/commit/9709937 ]
 * IDM-12258 Возможность выключить таску                                                                                                                                                                     [ https://a.yandex-team.ru/arc/commit/9696728 ]
 * IDM-12424 Правка логирования выполнения воркфлоу                                                                                                                                                          [ https://a.yandex-team.ru/arc/commit/9696690 ]

* [mmarat248](http://staff/mmarat248)

 * IDM-12254: prevent timeout with a large number of confirmers  [ https://a.yandex-team.ru/arc/commit/9707693 ]
 * IDM-12258: fix command                                        [ https://a.yandex-team.ru/arc/commit/9706411 ]
 * IDM-12258: Создавать тикет если не удалось пересмотреть роль  [ https://a.yandex-team.ru/arc/commit/9687797 ]

[smosker](http://staff/smosker) 2022-07-12 17:16:36+03:00

141.73
------
 * IDM-11706: return uuid as default param  [ https://a.yandex-team.ru/arc_vcs/commit/0a868f7ccc742eca2088c65d8c4ec2de870d2864 ]

[mmarat248](http://staff/mmarat248) 2022-07-04 13:12:18+03:00

141.72
------
 * IDM-12361: Переделал RoleNode add/change/remove методы на bulk-запросы  [ https://a.yandex-team.ru/arc/commit/9619220 ]

[kir-choo](http://staff/kir-choo) 2022-06-27 17:15:24+05:00

141.71
------
 * IDM-12351 Не ждем лока роли бесконечно при запросах через апи  [ https://a.yandex-team.ru/arc/commit/9595503 ]

[smosker](http://staff/smosker) 2022-06-16 14:33:13+03:00

141.70
------
 * IDM-12154: Исправил функцию построения индекса        [ https://a.yandex-team.ru/arc/commit/9586247 ]
 * Настойка для отключения логирования CommandTimestamp  [ https://a.yandex-team.ru/arc/commit/9586224 ]
 * IDM-12321: Очередь для DelayedRoleRequests            [ https://a.yandex-team.ru/arc/commit/9583503 ]

[kir-choo](http://staff/kir-choo) 2022-06-15 15:02:52+03:00

141.69
------
 * IDM-12312 отказ от update_or_create  [ https://a.yandex-team.ru/arc/commit/9561068 ]

[smosker](http://staff/smosker) 2022-06-07 22:53:25+03:00

141.68
------

* [smosker](http://staff/smosker)

 * IDM-12308 Выборочный мониторинг для ExecuteDelayedRoleRequests  [ https://a.yandex-team.ru/arc/commit/9553688 ]
 * IDM-12304 Не ходим в базу в ручке ping                          [ https://a.yandex-team.ru/arc/commit/9552938 ]

* [kir-choo](http://staff/kir-choo)

 * IDM-12154: FTS по полям RoleNode в саджестах

\- Поправил human-сериализацию subject-ов
\- Поправил валидацию и тесты на auth_factor                                                                                                                                                    [ https://a.yandex-team.ru/arc/commit/9542305 ]
 * IDM-12277: Пишем в логи uWSGI Worker ID + мелкий рефакторинг

\- При рендеринге шаблонов к username пользователя в конце добавляем @ для создания ссылки
 - Поправил опечатку в миграции
 - Поправил в функции can_rerequest_role
 - Механизм аутентификации систем по умолчанию - no  [ https://a.yandex-team.ru/arc/commit/9542128 ]
 * [FIX] IDM-11822: Регулярная задача по обновлению кеша правил фаервола

[FIX] IDM-11822: Регулярное обновление кеша правил фаервола
 - Добавил команду для обновления кеша правил
 - Добавил uWSGI cron задачу                                                                         [ https://a.yandex-team.ru/arc/commit/9524989 ]

[smosker](http://staff/smosker) 2022-06-06 18:09:23+03:00

141.67
------
 * IDM-12262 Правка саджеста по логинам созданным IDM  [ https://a.yandex-team.ru/arc/commit/9510795 ]

[smosker](http://staff/smosker) 2022-05-27 14:06:38+03:00

141.66
------
 * [FIX] IDM-11822: Оптимизация запросов для фаервола
   - Добавил кеширования запроса

[kir-choo](http://staff/kir-choo) 2022-05-26 12:44:57+03:00

141.65
------
 * IDM-12229: При запросе списка ролей мы предварительно подгружаем информацию о полях роли  [ https://a.yandex-team.ru/arc/commit/9463275 ]
 * IDM-12110: Поправил шаблон approve_role                                                                                                                                                                [ https://a.yandex-team.ru/arc/commit/9458379 ]
 * IDM-12229: При запросе списка ролей мы предварительно подгружаем информацию о полях роли                                                                                                               [ https://a.yandex-team.ru/arc/commit/9457667 ]
 * IDM-12146: Убираем лишние запросы в MembershipResource                                      [ https://a.yandex-team.ru/arc/commit/9443818 ]
 - Убираем логирование ожидаемых исключений в workflow
 - Оптимизация запроса связанных персональных ролей

[kir-choo](http://staff/kir-choo) 2022-05-17 15:56:47+03:00

141.64
------

* [smosker](http://staff/smosker)

 * IDM-11338 Поддержка заморозки членства пользователя  [ https://a.yandex-team.ru/arc/commit/9426199 ]

* [kir-choo](http://staff/kir-choo)

 * IDM-12033: Не отсылаем СМС для ролей системы Yandex.ID если secret_context пустой  [ https://a.yandex-team.ru/arc/commit/9423447 ]
 * IDM-12134: Некоторым системам не отдаем паспортные логины созданные не IDM         [ https://a.yandex-team.ru/arc/commit/9423445 ]
 * IDM-12177: Поднял версию UWSGI                                                     [ https://a.yandex-team.ru/arc/commit/9414377 ]

[smosker](http://staff/smosker) 2022-05-04 22:50:21+03:00

141.63
------
 * [FIX] IDM-12086: При отправке tvm_ids в tirole конвертировать из set в tuple                                                                                    [ https://a.yandex-team.ru/arc/commit/9398063 ]
 * IDM-11768: При ошибке синхронизации системы создаем Action с информацией                                                                                        [ https://a.yandex-team.ru/arc/commit/9396743 ]
 * IDM-12142: Логируем контекст TVM аутентификации

\- Используем TVM-миддлварь из django_yauth c подмененным user-дескпритором и tvm-клиентом
\- Не логируем /ping  [ https://a.yandex-team.ru/arc/commit/9396739 ]

[kir-choo](http://staff/kir-choo) 2022-04-27 15:36:04+03:00

141.62
------

* [kir-choo](http://staff/kir-choo)

 * [MIGRATION] IDM-12086: Редактирование настройки системы выгрузки ролей в tirole

\- Добавил поле export_to_tirole
 - Сделал поле tvm_tirole_ids редактируемым через API
 - Поменял логику сигналов для выгрузки
 - Добавил mock для Mongo  [ https://a.yandex-team.ru/arc/commit/9378547 ]
 * PR from branch users/kir-choo/refactor/integration

\- Рефакторинг racktables
\- Рефакторинг conductor_groups                                                                                                                               [ https://a.yandex-team.ru/arc/commit/9374854 ]
 * [FIX] IDM-12125: Баг при смене типа поля узла                                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/9362846 ]
 * [FIX] IDM-12032: Баг при вычислении членств в группах personal_granted_at                                                                                                                                                                 [ https://a.yandex-team.ru/arc/commit/9356112 ]
 * Исключил из выборки ролей группы находящиеся в процессе отзыва                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9355507 ]

* [smosker](http://staff/smosker)

 * Change "a.yaml"  [ https://a.yandex-team.ru/arc/commit/9369541 ]
 * Change "a.yaml"  [ https://a.yandex-team.ru/arc/commit/9363013 ]

[kir-choo](http://staff/kir-choo) 2022-04-25 17:30:34+03:00

141.61
------

* [kir-choo](http://staff/kir-choo)

 * [FIX] IDM-11822: Упростил проверку разрешений для запроса фаервола                                                                                                                                                                                                     [ https://a.yandex-team.ru/arc/commit/9351126 ]
 * PR from branch users/kir-choo/fix/arcadia-stuff

Мелочи для переезда

\- Добавил a.yaml
\- Добавил информацию об установке зависимостей в README
\- Добавил .arcignore                                                                                                    [ https://a.yandex-team.ru/arc/commit/9335632 ]
 * IDM-12027: Фильтрация по нескольким пользователям в поле requester ручки ApproveRequest (#2723)                                                                                                                                                                        [ https://a.yandex-team.ru/arc_vcs/commit/1f54c4f4ffe4a239e15df395ad36e63cf5ac249b ]
 * IDM-11911: При возникновении ошибки во время выдачи связанной роли создаем ее в статусе "failed" (#2715)

\* IDM-11911: При возникновении ошибки во время выдачи связанной роли создаем action у роли
\* Добавил Juggler-событияе для алерта на ошибки невыданных ролей  [ https://a.yandex-team.ru/arc_vcs/commit/0975da526ea31625ea4108781b8d8b82ecd72649 ]

* [smosker](http://staff/smosker)

 * Change "a.yaml"               [ https://a.yandex-team.ru/arc/commit/9337692 ]
 * IDM-12022 Тест idm в аркадии  [ https://a.yandex-team.ru/arc/commit/9335923 ]

* [robot-vcs-migration](http://staff/robot-vcs-migration)

 * TOARCADIA-17 [migration] github/idm/backend

Note: mandatory check (NEED_CHECK) was skipped  [ https://a.yandex-team.ru/arc/commit/9332729 ]

[smosker](http://staff/smosker) 2022-04-14 15:30:21+03:00

141.60
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-6630: Добавил выдачу дополнительных полей в ручке ApproveRequest (#2719)            [ https://github.yandex-team.ru/idm/backend/commit/6988cf02f ]
 * IDM-12062: Добавил префикс self/ в имени создаваемого porto-контейнера (#2718)          [ https://github.yandex-team.ru/idm/backend/commit/8a82e1ea1 ]
 * IDM-12032: Фактическое поле выдачи групповой/песональной роли (#2717)                   [ https://github.yandex-team.ru/idm/backend/commit/947dd7822 ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2022-04-05 13:02:36+03:00

141.59
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-12044 Правка отправки delayedrolerequest (#2716)  [ https://github.yandex-team.ru/idm/backend/commit/0610cceb1 ]

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-12027: Добавил фильтрацию по reason и requester в ручке approverequest (#2714)  [ https://github.yandex-team.ru/idm/backend/commit/2e6d18aed ]
 * IDM-11809: Перенос окончания срока пересмотра с выходных дней (#2713)               [ https://github.yandex-team.ru/idm/backend/commit/f41d2613d ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2022-03-28 14:52:16+03:00

141.58
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * [IDM-11822] Экспорт групп в Puncher (#2712)  [ https://github.yandex-team.ru/idm/backend/commit/bb476c3ce ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2022-03-16 14:15:48+03:00

141.57
------
 * IDM-12009 fix type  [ https://github.yandex-team.ru/idm/backend/commit/5a0431385 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2022-03-10 18:39:17+03:00

141.56
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-12009 Переходим на tvm2 с сертификата для системы idm (#2711)  [ https://github.yandex-team.ru/idm/backend/commit/b25b9be8a ]

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-12004: Исправлены баги связанные с переполнением очереди (#2710)  [ https://github.yandex-team.ru/idm/backend/commit/c8a72b7f2 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2022-03-10 17:58:22+03:00

141.55
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * [FIX] IDM-1769: У невыданных нет поля system_specific (#2709)  [ https://github.yandex-team.ru/idm/backend/commit/99b6b5708 ]
 * IDM-11766: Исправил баг с отправкой событий в Juggler (#2708)  [ https://github.yandex-team.ru/idm/backend/commit/275ad4ff6 ]
 * IDM-11748: Актуализируем YAML-формат дерева ролей  (#2707)     [ https://github.yandex-team.ru/idm/backend/commit/f72a9411e ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2022-03-03 15:57:35+03:00

141.54
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11973 Добавляем is_robot в ручку Users (#2706)  [ https://github.yandex-team.ru/idm/backend/commit/25355c5ff ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2022-02-25 17:49:12+03:00

141.53
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11814 Не запускаем таски подсчета метрик в тестинге (#2705)  [ https://github.yandex-team.ru/idm/backend/commit/eb9d2c5cf ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2022-02-25 15:44:23+03:00

141.52
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-9602 Синхронизация ответственных за tvm приложения из прода (#2704)  [ https://github.yandex-team.ru/idm/backend/commit/9032faaf1 ]
 * IDM-11928 Правка емейла о роботе, если сам отзываешь роль (#2703)        [ https://github.yandex-team.ru/idm/backend/commit/9e687327d ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2022-02-25 14:40:30+03:00

141.51
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-11141: Migration to deploy (#2702)  [ https://github.yandex-team.ru/idm/backend/commit/8fc635686 ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2022-02-22 15:58:19+03:00

141.50
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11928 Правка емейлов (#2701)                  [ https://github.yandex-team.ru/idm/backend/commit/8e64a6c26 ]
 * IDM-11593 Правка прокидывания переменной (#2700)  [ https://github.yandex-team.ru/idm/backend/commit/cfbd15627 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2022-02-22 15:21:01+03:00

141.49
------

* [Vladimir koljasinskij](http://staff/smosker@yandex-team.ru)

 * Revert "IDM-11748: Формат ответа YAML-плагина совместим с JSON-плагином (#2696)"  [ https://github.yandex-team.ru/idm/backend/commit/3a463ef11 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11928 Отправка уведомлений по роботам (#2699)         [ https://github.yandex-team.ru/idm/backend/commit/33a77bc0b ]
 * IDM-11593 прокидываем причину запроса в воркфлоу (#2698)  [ https://github.yandex-team.ru/idm/backend/commit/f0c1f59e4 ]

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-11769: Отображение имен полей у роли (#2695)                         [ https://github.yandex-team.ru/idm/backend/commit/e6a5d6bc4 ]
 * IDM-11912: Параметр is_broken может меняться через API (#2697)           [ https://github.yandex-team.ru/idm/backend/commit/7f78388d9 ]
 * IDM-11748: Формат ответа YAML-плагина совместим с JSON-плагином (#2696)  [ https://github.yandex-team.ru/idm/backend/commit/ea007efff ]
 * [FIX] IDM-11853: Workflow container creation error (#2692)               [ https://github.yandex-team.ru/idm/backend/commit/ea9e07e2b ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2022-02-18 14:01:52+03:00

141.48
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11921 Правка получения паспортного логина (#2694)  [ https://github.yandex-team.ru/idm/backend/commit/b16495b8b ]

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-11897: Валидация API URL систем (#2689)  [ https://github.yandex-team.ru/idm/backend/commit/9ddf445f0 ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2022-02-14 14:30:02+03:00

141.47
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * [FIX] IDM-6630: Счетчик метрики (#2693)        [ https://github.yandex-team.ru/idm/backend/commit/e91a7f6ef ]
 * [FIX] IDM-11720: Разделил ошибки логики IDM и Workflow (#2691)  [ https://github.yandex-team.ru/idm/backend/commit/6086b3a0d ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2022-02-10 13:13:29+03:00

141.46
------

* [Vladimir koljasinskij](http://staff/smosker@yandex-team.ru)

 * Revert "Revert "PASSP-35896: Remove role external_counter_grant from SID67 exclusions (#2684)" (#2687)"  [ https://github.yandex-team.ru/idm/backend/commit/92f356d02 ]

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-6630: Add Metrkia counter suggest (#2686)  [ https://github.yandex-team.ru/idm/backend/commit/427de6548 ]
 * IDM-11720: URL not defined error (#2688)       [ https://github.yandex-team.ru/idm/backend/commit/cbbc3036f ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2022-02-03 15:22:07+03:00

141.45
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-11843: Dont use Sentry/Raven (#2682)                                                        [ https://github.yandex-team.ru/idm/backend/commit/1d144f122 ]
 * IDM-11766: Juggler Events (#2681)                                                               [ https://github.yandex-team.ru/idm/backend/commit/33ebd0439 ]
 * Localization templates (#2678)                                                                  [ https://github.yandex-team.ru/idm/backend/commit/13d5b89fd ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11865 разрешаем только суперпользователю выключать системы (#2685)  [ https://github.yandex-team.ru/idm/backend/commit/b008c7413 ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2022-01-31 16:47:32+03:00

141.44
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-11750: Fix localizations in temaplte emails/head.txt (#2677)  [ https://github.yandex-team.ru/idm/backend/commit/2ac23ef25 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11767 Обработка исключения при блокировке пользователя (#2676)  [ https://github.yandex-team.ru/idm/backend/commit/e204b2f79 ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2021-12-30 18:57:05+05:00

141.43
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * [IDM-11750] Localization problems (#2673)                                [ https://github.yandex-team.ru/idm/backend/commit/9ec8766c3 ]
 * IDM-9396: Change error message of comment_required role request (#2674)  [ https://github.yandex-team.ru/idm/backend/commit/493235d7d ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2021-12-27 22:35:42+05:00

141.42
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11535 Прокидываем ttl_days в воркфлоу (#2675)  [ https://github.yandex-team.ru/idm/backend/commit/932599751 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-12-27 14:08:40+03:00

141.41
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11762 Добавляем очередь для пинкодницы (#2672)  [ https://github.yandex-team.ru/idm/backend/commit/17898e40a ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-12-14 15:50:59+03:00

141.40
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11731 Поддержка синхронизации деревьев из аркадии (#2670)  [ https://github.yandex-team.ru/idm/backend/commit/46ec680d8 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-12-10 11:24:31+03:00

141.39
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * [BUGFIX] IDM-11628: Fix cache keys (#2671)             [ https://github.yandex-team.ru/idm/backend/commit/e380b0aef ]
 * IDM-11749: Fix queryset filters for bulk task (#2669)  [ https://github.yandex-team.ru/idm/backend/commit/0d8dff37a ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2021-12-09 17:07:04+03:00

141.38
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * revert IDM-11573 (#2668)  [ https://github.yandex-team.ru/idm/backend/commit/f57567e81 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-12-06 21:56:38+03:00

141.37
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-9396: Add comment_required field in RoleNode (#2664)  [ https://github.yandex-team.ru/idm/backend/commit/f92b4d6a8 ]
 * IDM-11628: Automate depriving validation (#2661)          [ https://github.yandex-team.ru/idm/backend/commit/74a2c6e87 ]
 * IDM-11722: Fix constance tuple error (#2665)              [ https://github.yandex-team.ru/idm/backend/commit/a48d13706 ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2021-12-02 18:30:57+03:00

141.36
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * Pre-selecting groups in roles query (#2663)  [ https://github.yandex-team.ru/idm/backend/commit/af774166c ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2021-11-25 16:06:15+05:00

141.35
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-10340: Fetch profound role node tree in YAML format (#2659)               [ https://github.yandex-team.ru/idm/backend/commit/1ae5cda67 ]
 * IDM-11639: Filter response data by query parameter `fields` (#2660)           [ https://github.yandex-team.ru/idm/backend/commit/90f0634a2 ]
 * IDM-11640 [Re-Revert]:  (#2658)                                               [ https://github.yandex-team.ru/idm/backend/commit/dd3f69b66 ]
 * IDM-11640: Add IDM responsibilities when request role on large group (#2654)  [ https://github.yandex-team.ru/idm/backend/commit/e922deccf ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11579 Правка падения тестов (#2656)  [ https://github.yandex-team.ru/idm/backend/commit/ef2e0f41a ]

* [Vladimir koljasinskij](http://staff/smosker@yandex-team.ru)

 * Revert "IDM-11640: Add IDM responsibilities when request role on large group (#2654)"  [ https://github.yandex-team.ru/idm/backend/commit/86c870232 ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2021-11-16 17:41:58+03:00

141.34
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-10507 Логируем ключи контекста (#2646)  [ https://github.yandex-team.ru/idm/backend/commit/1638e4450 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-11-01 09:28:23+03:00

141.33
------

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-11633: Log invalid json body in batch resource (#2653)  [ https://github.yandex-team.ru/idm/backend/commit/751d95137 ]
 * IDM-11573 Add ApproveRequestBulk resource (#2648)           [ https://github.yandex-team.ru/idm/backend/commit/60862a5eb ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2021-10-29 11:10:23+03:00

141.32
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11592 правка limit в get_all_users (#2652)  [ https://github.yandex-team.ru/idm/backend/commit/895e1f2dc ]

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * IDM-11580: RoleNode review required (#2650)  [ https://github.yandex-team.ru/idm/backend/commit/f098d956c ]

[kir-choo](http://staff/kir-choo@yandex-team.ru) 2021-10-21 16:25:07+03:00

141.31
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11592 Возможность ограничить число пользователей в all_users_with_role (#2649)          [ https://github.yandex-team.ru/idm/backend/commit/474e3ba0e ]
 * IDM-11585 Делаем подсчет количества логинов для подписи в мониторинге ассинхронным (#2645)  [ https://github.yandex-team.ru/idm/backend/commit/a56c20281 ]

* [Kirill Churkin](http://staff/kir-choo@yandex-team.ru)

 * Optimize update of UserPasswordLogin objects from roles (#2647)  [ https://github.yandex-team.ru/idm/backend/commit/10e835037 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-10-18 17:09:49+03:00

141.30
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11576 правка алерта hanging-depriving-roles (#2644)          [ https://github.yandex-team.ru/idm/backend/commit/79533e197 ]
 * IDM-11428 правка алерта active-roles-of-inactive-groups (#2643)  [ https://github.yandex-team.ru/idm/backend/commit/392e957ee ]
 * IDM-10507 Отправка смс по групповым ролям (#2642)                [ https://github.yandex-team.ru/idm/backend/commit/dffaffe7c ]

* [Nikita Slyusarev](http://staff/nslus@yandex-team.ru)

 * Let `inheritance_settings` always be a dict (#2641)  [ https://github.yandex-team.ru/idm/backend/commit/0ccf95055 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-10-07 18:52:09+03:00

141.29
------

* [Nikita Slyusarev](http://staff/nslus@yandex-team.ru)

 * IDM-11510: pass inheritance settings to group workflow (#2640)  [ https://github.yandex-team.ru/idm/backend/commit/bdbdc094e ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-09-16 19:48:04+03:00

141.28
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11487 правка теста (#2639)                                            [ https://github.yandex-team.ru/idm/backend/commit/0df8f0c80 ]
 * IDM-11487 Создаем тикеты если не удалось заблокировать AD учетки (#2638)  [ https://github.yandex-team.ru/idm/backend/commit/57322e8d2 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-09-14 13:24:48+03:00

141.27
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11386 Пушим данные о ролях в tirole (#2629)  [ https://github.yandex-team.ru/idm/backend/commit/3fe9959f4 ]

* [Vladimir koljasinskij](http://staff/smosker@yandex-team.ru)

 * Правка проверки количества при запуске расхождений  [ https://github.yandex-team.ru/idm/backend/commit/a0553a558 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-09-03 23:41:51+03:00

141.26
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11434 Мониторинг на количество часов с момента успешного синка (#2635)                            [ https://github.yandex-team.ru/idm/backend/commit/0542f895b ]
 * IDM-11435 Возможность ограничение количества расхождений, которое можно решить автоматически (#2637)  [ https://github.yandex-team.ru/idm/backend/commit/466c577da ]
 * IDM-11459 реже обновляем статистику по системам (#2636)                                               [ https://github.yandex-team.ru/idm/backend/commit/d2fc5c970 ]
 * Алерт для количества расхождений по системам (#2634)                                                  [ https://github.yandex-team.ru/idm/backend/commit/e084fc466 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-08-31 15:35:58+03:00

141.25
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * ABC-11076 Поддержка использования date в workflow (#2633)  [ https://github.yandex-team.ru/idm/backend/commit/3e0e71dfa ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-08-12 23:07:46+03:00

141.24
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * ABC-11076 Добавляем возможность получать date_joined (#2632)  [ https://github.yandex-team.ru/idm/backend/commit/58aa4a0da ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-08-12 17:56:39+03:00

141.23
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * IDM-11376 Правка алертов (#2628)                              [ https://github.yandex-team.ru/idm/backend/commit/500ac3231 ]
 * Ограничиваем количество отдаваемых записей в истории (#2630)  [ https://github.yandex-team.ru/idm/backend/commit/03ea2dab8 ]
 * ABC-11076 Добавляем возможность получать date_joined (#2631)  [ https://github.yandex-team.ru/idm/backend/commit/6ebaef0b4 ]

[Vladimir koljasinskij](http://staff/smosker@yandex-team.ru) 2021-08-12 16:33:51+03:00

141.22
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-11325: Выдаём перс.роли по групповой только в unaware системах (#2626)  [ https://github.yandex-team.ru/idm/backend/commit/fa559ed44 ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2021-06-28 15:02:29+03:00

141.21
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-11288: Переводим в depriving только активные ноды (#2625)  [ https://github.yandex-team.ru/idm/backend/commit/0f4364bd0 ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2021-06-13 20:49:06+03:00

141.20
------

* [Vladimir Spasskiy](http://staff/wlame@yandex-team.ru)

 * IDM-10213 Восстанавливаем роль из DEPRIVING_VALIDATION (#2618)  [ https://github.yandex-team.ru/idm/backend/commit/3e4d8ce6b ]

[Wladimir Spasskiy](http://staff/wlame@yandex-team.ru) 2021-05-31 18:33:54+03:00

141.18
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-11076: Не перестраиваем дерево в рамках запроса на перемещение узла (#2624)           [ https://github.yandex-team.ru/idm/backend/commit/b5cd9d42e ]
 * IDM-11076: Делаем insert-запросы в closuretree с меньшим кол-вом походов по сети (#2622)  [ https://github.yandex-team.ru/idm/backend/commit/18beb184e ]
 * IDM-11076: Затаскиваем closuretree к себе в репозиторий (#2620)                           [ https://github.yandex-team.ru/idm/backend/commit/b2d17f31f ]
 * IDM-11076: Оптимизация перемещения узлов (ставим один таск на пуши в Поиск) (#2619)       [ https://github.yandex-team.ru/idm/backend/commit/de8769062 ]

* [Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru)

 * IDM-11167: Поправил комментарий  [ https://github.yandex-team.ru/idm/backend/commit/1361e2da6 ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2021-05-19 16:40:50+03:00

141.17
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-11167: Union в запросе за правами по системе вместо Or  [ https://github.yandex-team.ru/idm/backend/commit/9e50fc3ec ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2021-04-26 15:05:24+03:00

141.16
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-11149: Обратно меняем подзапросы местами (revert коммита) (#2617)        [ https://github.yandex-team.ru/idm/backend/commit/053c2f9e3 ]
 * IDM-11164: При генерации логина заменяем в слаге системы "_" на "-" (#2615)  [ https://github.yandex-team.ru/idm/backend/commit/5b519d208 ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2021-04-20 14:50:58+03:00

141.15
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-11149: Меняем подзапросы местами в get_permitted_query  [ https://github.yandex-team.ru/idm/backend/commit/a5e4715b1 ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2021-04-09 18:42:55+03:00

141.14
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-11032: Используем правильное время при выгрузке ролей в YT (#2611)  [ https://github.yandex-team.ru/idm/backend/commit/fd2025e2b ]
 * IDM-10987: Ручка отзыва ролей асинхронно (#2612)                        [ https://github.yandex-team.ru/idm/backend/commit/8874d4e03 ]
 * Поправил утилиту для создания таблиц с ролями в YT                      [ https://github.yandex-team.ru/idm/backend/commit/b6901b45d ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2021-03-29 19:51:14+03:00

141.13
------

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10776: Ручка запроса ролей асинхронно (#2599)  [ https://github.yandex-team.ru/idm/backend/commit/6f02af980 ]
 * delete b2b (#2595)                                 [ https://github.yandex-team.ru/idm/backend/commit/9274ef4b7 ]

* [Anastasiia Pereverzeva](http://staff/pixel@yandex-team.ru)

 * IDM-10892: yml На запрос роли с симуляцией в public api (#2607)                                     [ https://github.yandex-team.ru/idm/backend/commit/ec871c044 ]
 * IDM-10901: yml на разные политики систем по работе с групповыми ролями (#2605)                      [ https://github.yandex-team.ru/idm/backend/commit/fdde0f03e ]
 * IDM-10884: yml на запрос групповой роли с 3 подтверждающими (#2594)                                 [ https://github.yandex-team.ru/idm/backend/commit/1eccbe550 ]
 * IDM-10870: yml на список всех систем (#2609)                                                        [ https://github.yandex-team.ru/idm/backend/commit/259f788e6 ]
 * IDM-10871: yml на запрос роли с подтверждением одним подтверждающим (#2593)                         [ https://github.yandex-team.ru/idm/backend/commit/45d2271bb ]
 * IDM-10865: YML на api frontend для Отчёта с ролями (#2589)                                          [ https://github.yandex-team.ru/idm/backend/commit/6ef653769 ]
 * IDM-10874: yml на права редактирования воркфлоу (#2606)                                             [ https://github.yandex-team.ru/idm/backend/commit/ea178a8c8 ]
 * IDM-10869: yml на отчёты по системе (#2592)                                                         [ https://github.yandex-team.ru/idm/backend/commit/73bfb91de ]
 * IDM-10875: ямлы на воркфлоу системы (#2598)                                                         [ https://github.yandex-team.ru/idm/backend/commit/76eee80ba ]
 * IDM-10855: YML на запрос и отзыв персональной роли (#2585)                                          [ https://github.yandex-team.ru/idm/backend/commit/ce407b7bc ]
 * IDM-10857: YML на кейсы, когда запрос роли невозможен (#2587)                                       [ https://github.yandex-team.ru/idm/backend/commit/66de67392 ]
 * IDM-10873: yml на роли для конкретной системы (#2608)                                               [ https://github.yandex-team.ru/idm/backend/commit/2c2a5796b ]
 * IDM-10894: ямл на добавление/удаление ноды в public api (#2604)                                     [ https://github.yandex-team.ru/idm/backend/commit/96a371e33 ]
 * IDM-10896: ямлы на список пользователей в public api (#2603)                                        [ https://github.yandex-team.ru/idm/backend/commit/e34cbfc6f ]
 * IDM-10866: yml на api/frontend для действий в верхних отчётах (#2590)                               [ https://github.yandex-team.ru/idm/backend/commit/e9f708600 ]
 * IDM-10890: ямл на ручку roles в public api (#2602)                                                  [ https://github.yandex-team.ru/idm/backend/commit/2d12dbb12 ]
 * IDM-10868: yml на api для inconsistencies (#2591)                                                   [ https://github.yandex-team.ru/idm/backend/commit/e82a023b4 ]
 * IDM-10858: YML на запрос роли с уволенными необязательными подтверждающими + довыдача роли (#2586)  [ https://github.yandex-team.ru/idm/backend/commit/47f158f46 ]
 * IDM-10895: ямл на ручку дерева ролей в public api (#2600)                                           [ https://github.yandex-team.ru/idm/backend/commit/181be4952 ]
 * IDM-10856: YML на запрос и отзыв групповой роли (#2588)                                             [ https://github.yandex-team.ru/idm/backend/commit/6aea33480 ]
 * IDM-10887: ямл на batch-ручку (#2601)                                                               [ https://github.yandex-team.ru/idm/backend/commit/694200c22 ]
 * IDM-10872: yml на синхронизацию системы (#2596)                                                     [ https://github.yandex-team.ru/idm/backend/commit/76fe0fd8e ]
 * IDM-10903: yml на запрос роли до даты (#2597)                                                       [ https://github.yandex-team.ru/idm/backend/commit/7a4f16f24 ]
 * IDM-10861: YML на api фронта для "Моих ролей" (#2582)                                               [ https://github.yandex-team.ru/idm/backend/commit/54c561bd4 ]
 * IDM-10864: YML на api frontend для "Мои роли. Таб "Отчёты" (#2581)                                  [ https://github.yandex-team.ru/idm/backend/commit/f608fb78f ]
 * IDM-10859: YML на запрос роли со сроком (#2584)                                                     [ https://github.yandex-team.ru/idm/backend/commit/c03b98055 ]
 * IDM-10862: YML на api фронта для "Мои роли. Таб "Группы" (#2583)                                    [ https://github.yandex-team.ru/idm/backend/commit/019be72e4 ]
 * IDM-10863: YML на api/frontend для таба "Запросы" (#2580)                                           [ https://github.yandex-team.ru/idm/backend/commit/01b0c9fc6 ]

* [cracker](http://staff/cracker@yandex-team.ru)

 * add missed import  [ https://github.yandex-team.ru/idm/backend/commit/39877ae15 ]

[cracker](http://staff/cracker@yandex-team.ru) 2021-03-03 17:20:23+03:00

141.12
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-10833: Посистемные лимиты на пересмотр ролей (#2570)           [ https://github.yandex-team.ru/idm/backend/commit/83472c5e3 ]
 * IDM-10770: Команды для создания репл.таблиц с ролями в YT (#2566)  [ https://github.yandex-team.ru/idm/backend/commit/a67871646 ]

* [cracker](http://staff/cracker@yandex-team.ru)

 * improve make stand command  [ https://github.yandex-team.ru/idm/backend/commit/61cdd3b9a ]

[cracker](http://staff/cracker@yandex-team.ru) 2021-02-09 10:59:04+03:00

141.11
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-10773: Выгружаем роли в YT, только когда необходимо (#2569)  [ https://github.yandex-team.ru/idm/backend/commit/3493e2d4c ]

* [Nikolay Ilchenko](http://staff/tavria@yandex-team.ru)

 * IDM-10414: Вкрутить палмсинк (#2568)  [ https://github.yandex-team.ru/idm/backend/commit/03eff59d8 ]

[cracker](http://staff/cracker@yandex-team.ru) 2021-02-04 18:20:34+03:00

141.10
------

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10588: [Мониторинг] Отладка monitoring-idm-error-count (#2565)       [ https://github.yandex-team.ru/idm/backend/commit/1598bce55 ]
 * IDM-10796: Актуализировать мониторинги после изменений в синках (#2567)  [ https://github.yandex-team.ru/idm/backend/commit/b2ee65860 ]

[cracker](http://staff/cracker@yandex-team.ru) 2021-01-19 15:11:22+03:00

141.9
-----

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10493: Объединить синки разных типов групп в одну таску (#2555)  [ https://github.yandex-team.ru/idm/backend/commit/42865b928 ]

[cracker](http://staff/cracker@yandex-team.ru) 2021-01-15 18:20:45+03:00

141.8
-----

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10668: Добавить возможность менять плагин узлов (#2562)  [ https://github.yandex-team.ru/idm/backend/commit/b3e74f923 ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2020-12-25 16:50:31+03:00

141.7
-----

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10617: Ручка, которая отдает роли по системе из YT (#2563)  [ https://github.yandex-team.ru/idm/backend/commit/4cf4c59d7 ]
 * IDM-10586: Эксперименты с дин. таблицами (#2560)                [ https://github.yandex-team.ru/idm/backend/commit/a3bc567c6 ]
 * IDM-10513: Работа в тасках с чанками (#2556)                    [ https://github.yandex-team.ru/idm/backend/commit/1a7b783c2 ]
 * Команда для выкатки тестинга (#2564)                            [ https://github.yandex-team.ru/idm/backend/commit/b568f3953 ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2020-12-25 14:09:02+03:00

141.6
-----

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-10365: Небольшие фиксы по валидации отзывов (#2561)  [ https://github.yandex-team.ru/idm/backend/commit/98b4cb324 ]

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10140: Не закрывается окно после одобрения роли (#2559)  [ https://github.yandex-team.ru/idm/backend/commit/7ed4b2ab4 ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2020-12-15 14:18:23+03:00

141.5
-----

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-10365: Валидация отзыва ролей (#2557)  [ https://github.yandex-team.ru/idm/backend/commit/16a6ec6a6 ]

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10064: Фикс страницы диагностики для просмотра yaml в info (#2558)  [ https://github.yandex-team.ru/idm/backend/commit/b6c6b36cd ]

[Kirill Kartashov (qazaq)](http://staff/qazaq@yandex-team.ru) 2020-12-10 16:58:23+03:00

141.4
-----

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-10064: Загрузка узлов через yaml (#2553)  [ https://github.yandex-team.ru/idm/backend/commit/3d6c7a379 ]

[cracker](http://staff/cracker@yandex-team.ru) 2020-12-08 14:25:09+03:00

141.3
-----

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10472: разнести во времени запуски синк групп и людей (#2552)       [ https://github.yandex-team.ru/idm/backend/commit/b0d23ca19 ]
 * IDM-10473: Поддeржать в cron командах django_tools_log_context (#2554)  [ https://github.yandex-team.ru/idm/backend/commit/9ebf680f9 ]

[cracker](http://staff/cracker@yandex-team.ru) 2020-11-18 16:45:44+03:00

141.2
-----

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-10282: Получение узлов AD по unique_id для независимой от дерева выдачи ref ролей (#2526)  [ https://github.yandex-team.ru/idm/backend/commit/d76bf501e ]

[cracker](http://staff/cracker@yandex-team.ru) 2020-11-05 19:39:09+03:00

141.1
-----

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * IDM-6524: Версии celery/kombu/vine, совместимые с мультихостом для монго-брокера + правильный конфиг (#2549)  [ https://github.yandex-team.ru/idm/backend/commit/e7827ab32 ]

[cracker](http://staff/cracker@yandex-team.ru) 2020-11-05 13:01:25+03:00

141.0
-------
 * Перестало хватать памяти для команды idm_update_passport_logins (#2547)  [ https://github.yandex-team.ru/idm/backend/commit/c78e5a472 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2020-10-22 19:58:42+03:00

140.220
-------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-10403: Исправления синхронизации групп со staff-api (#2540)  [ https://github.yandex-team.ru/idm/backend/commit/f0a4a703f ]

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10399: Поправлены сигналы по системочленствам для настройки алертов (#2541)  [ https://github.yandex-team.ru/idm/backend/commit/b121259a2 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-10-09 16:42:54+03:00

140.215
-------

* IDM-10410 release

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-10116: ускорение синка пользователей (#2523)  [ https://github.yandex-team.ru/idm/backend/commit/1b87a2f88 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-10-05 15:37:29+03:00

140.214
-------
 * IDM-10390 release

 * IDM-10314: merge PR's for release (#2538)  [ https://github.yandex-team.ru/idm/backend/commit/8cf141543 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-10-01 13:26:57+03:00

140.213
-------

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10349: Add async unistat cache update (#2539)  [ https://github.yandex-team.ru/idm/backend/commit/e3ee4cb57 ]

[cracker](http://staff/cracker@yandex-team.ru) 2020-09-30 19:38:29+03:00

140.212
-------
* IDM-10378 - release

* [Nikita Sukhorukov](http://staff/cracker@yandex-team.ru)

 * IDM-10349: Соломка перед релизами (#2536)  [ https://github.yandex-team.ru/idm/backend/commit/7940123aa ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-10338: red button (#2535)  [ https://github.yandex-team.ru/idm/backend/commit/0928b051c ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-09-30 13:29:41+03:00

140.201
-------
 * IDM-9917: revert2 (#2518)  [ https://github.yandex-team.ru/idm/backend/commit/9c7163ad8 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-31 16:07:45+03:00

140.200
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-10194: не отзывать роли, для которых не требуется логин (#2519)       [ https://github.yandex-team.ru/idm/backend/commit/f8ad0ff39 ]
 * Не пытаться запрашивать роль ответственного, если такая уже есть (#2522)  [ https://github.yandex-team.ru/idm/backend/commit/19508f985 ]
 * Удалить alert db (#2521)                                                  [ https://github.yandex-team.ru/idm/backend/commit/acad099ae ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-7967: Ходить в Разлогинивалку СИБ  с tvm2 (#2520)  [ https://github.yandex-team.ru/idm/backend/commit/a4266c937 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-08-31 09:53:48+03:00

140.199
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-10032: Запретить синхронизировать систему без tvm-приложения (#2477)  [ https://github.yandex-team.ru/idm/backend/commit/265bf8624 ]
 * IDM-10230: Выбирать системы отдельно (#2207)                              [ https://github.yandex-team.ru/idm/backend/commit/306c96bac ]
 * Более лучший пайплайн (#2514)                                             [ https://github.yandex-team.ru/idm/backend/commit/553da59cf ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-4936: Проверить работу галочек автообновления (#1249)                       [ https://github.yandex-team.ru/idm/backend/commit/a1d573b3d ]
 * IDM-9930: Удалить право обхода двойной авторизации изменения воркфлоу… (#2443)  [ https://github.yandex-team.ru/idm/backend/commit/e941e7741 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-08-28 16:09:28+03:00

140.198
-------
 * IDM-9917: add switch (#2516)  [ https://github.yandex-team.ru/idm/backend/commit/85d30b473 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-25 12:02:38+03:00

140.197
-------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-24 15:41:50+03:00

140.196
-------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-24 15:41:06+03:00

140.195
-------
 * Revert "IDM-10064: Возможность завести дерево ролей не через ручку info (#2501)" (#2515)  [ https://github.yandex-team.ru/idm/backend/commit/dab4d86ff ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-24 15:16:44+03:00

140.194
-------
 * IDM-9917: add group type filter for indirect memberships views (#2513)  [ https://github.yandex-team.ru/idm/backend/commit/74b77a5ae ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-19 20:17:02+03:00

140.193
-------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-10064: Возможность завести дерево ролей не через ручку info (#2501)  [ https://github.yandex-team.ru/idm/backend/commit/26b992ae1 ]

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-08-19 14:25:28+05:00

140.192
-------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9917: fix staff sync (#2511)                         [ https://github.yandex-team.ru/idm/backend/commit/2413900d1 ]
 * IDM-10160: add test case for breaking a systems (#2504)  [ https://github.yandex-team.ru/idm/backend/commit/d03275363 ]

* [Anastasiia Isaeva](http://staff/pixel@yandex-team.ru)

 * IDM-10166: Добавлен testcase.yml для проверки экспериментальной тулзы (#2508)  [ https://github.yandex-team.ru/idm/backend/commit/370b97921 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-18 15:43:59+03:00

140.191
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-10148: ручка для запуска доктестов (#2512)                                                         [ https://github.yandex-team.ru/idm/backend/commit/1361988b4 ]
 * f (#2509)                                                                                              [ https://github.yandex-team.ru/idm/backend/commit/1cd4cced4 ]
 * IDM-9593: IDM-9596: тесты (#2505)                                                                      [ https://github.yandex-team.ru/idm/backend/commit/1cc5c5c16 ]
 * idm-9559: Тест на перезапрос ролей при переходе пользователя из подразделения в подразделение (#2507)  [ https://github.yandex-team.ru/idm/backend/commit/f2106a3f4 ]
 * IDM-9722: Система. Синхронизация узлов. Добавление нового узла (#2506)                                 [ https://github.yandex-team.ru/idm/backend/commit/1256708f5 ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * fix test (#2510)  [ https://github.yandex-team.ru/idm/backend/commit/12e6a7497 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-08-14 06:29:10+03:00

140.190
-------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-11 17:15:38+03:00

140.189
-------
 * IDM-9917: revert (#2503)  [ https://github.yandex-team.ru/idm/backend/commit/a68365849 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-11 17:04:48+03:00

140.188
-------
 * IDM-9917: fix inheritance (#2502)  [ https://github.yandex-team.ru/idm/backend/commit/a19c5a421 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-11 12:23:18+03:00

140.187
-------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9917: fix always inherit service scopes (#2499)  [ https://github.yandex-team.ru/idm/backend/commit/de68ba806 ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Получать свежий объект логина при проверке (#2500)  [ https://github.yandex-team.ru/idm/backend/commit/e0b33d5a7 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-07 12:39:47+03:00

140.186
-------
 * IDM-10054: Запрос связанных ролей может падать из-за недоступности кеша (#2497)  [ https://github.yandex-team.ru/idm/backend/commit/8cb4d8b7f ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-08-06 10:47:49+03:00

140.185
-------
 * fix idm_error->requested transition (#2498)  [ https://github.yandex-team.ru/idm/backend/commit/022b2ba45 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-05 20:17:25+03:00

140.184
-------
 * IDM-9917: fix default value for api (#2496)  [ https://github.yandex-team.ru/idm/backend/commit/88584a57f ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-08-05 13:39:36+03:00

140.183
-------
 * IDM-10065: fix  [ https://github.yandex-team.ru/idm/backend/commit/3d3d5fcaa ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-08-04 09:48:07+03:00

140.182
-------
 * IDM-10065: Отчет по подключенным системам (#2495)  [ https://github.yandex-team.ru/idm/backend/commit/eba17b651 ]
 * IDM-9620: тест на запрос групповой роли (#2493)    [ https://github.yandex-team.ru/idm/backend/commit/215f05afb ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-08-03 12:48:03+03:00

140.181
-------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * merge migrations                                           [ https://github.yandex-team.ru/idm/backend/commit/205c00c4e ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-07-30 14:59:25+03:00

140.180
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * save-docker-layers (#2494)  [ https://github.yandex-team.ru/idm/backend/commit/be6cf888b ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9485: сверка не работает с полем subject_type (#2491)  [ https://github.yandex-team.ru/idm/backend/commit/3779a4294 ]
 * IDM-9917: role inheritance in ABC tree (#2483)             [ https://github.yandex-team.ru/idm/backend/commit/744c427d6 ]
 * IDM-7596: pass UID to system (#2487)                       [ https://github.yandex-team.ru/idm/backend/commit/06f4a66af ]
 * add monitoring url (#2492)                                 [ https://github.yandex-team.ru/idm/backend/commit/1bb133720 ]

* [Anastasiia Isaeva](http://staff/pixel@yandex-team.ru)

 * IDM-9760: Тест на процесс истечения срока жизни роли. Импортированная роль (#2489)  [ https://github.yandex-team.ru/idm/backend/commit/95040f6b8 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-07-30 14:49:56+03:00

140.179
-------
 * Фикс миграций  [ https://github.yandex-team.ru/idm/backend/commit/1f8b70a06 ]

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-07-28 17:40:44+03:00

140.178
-------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9961: Добавление новых систем в webauth без перевыкатки (#2485)  [ https://github.yandex-team.ru/idm/backend/commit/addf7db43 ]

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-07-28 17:22:52+03:00

140.177
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Всякие фиксы (#2488)  [ https://github.yandex-team.ru/idm/backend/commit/00bdaad3b ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9121: merge migrations (#2484)  [ https://github.yandex-team.ru/idm/backend/commit/739348c1e ]

* [Anastasiia Isaeva](http://staff/pixel@yandex-team.ru)

 * IDM-9759: Тест на случай, когда роль в статусе "нужно перезапросить" не перезапрошена вовремя (#2468)  [ https://github.yandex-team.ru/idm/backend/commit/a50307f55 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-27 16:20:30+03:00

140.176
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-10039: обновление библиотек (#2480)  [ https://github.yandex-team.ru/idm/backend/commit/cfd58753f ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-10075: Починить админку систем  [ https://github.yandex-team.ru/idm/backend/commit/49586ba4a ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-22 09:50:57+03:00

140.175
-------
 * IDM-9121: add monitoring for `idm_error` roles (#2482)  [ https://github.yandex-team.ru/idm/backend/commit/cc9ddd3bd ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-07-21 19:40:47+03:00

140.174
-------
 * IDM-9121: New role state `idm_error` (#2473)  [ https://github.yandex-team.ru/idm/backend/commit/4291511c5 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-07-17 12:46:20+03:00

140.173
-------
 * remove redundant review days/date (#2475)  [ https://github.yandex-team.ru/idm/backend/commit/29b4b39c8 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-07-16 14:01:37+03:00

140.172
-------

* [alexsaplin](http://staff/alexsaplin@yandex-team.ru)

 * Удаление ненужного файла с миграцией  [ https://github.yandex-team.ru/idm/backend/commit/6ff681e94 ]

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9984: Найти место в коде и оптимизировать запрос depriving_at <= %s (#2481)  [ https://github.yandex-team.ru/idm/backend/commit/f2f51b5c5 ]

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-07-16 13:52:15+03:00

140.171
-------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9984: Найти место в коде и оптимизировать запрос depriving_at <= %s (#2479)  [ https://github.yandex-team.ru/idm/backend/commit/fdcba10f9 ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Сравнить зависимости с Аркадией (#2476)  [ https://github.yandex-team.ru/idm/backend/commit/c8da87ef3 ]

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-07-15 16:05:14+03:00

140.170
-------
 * IDM-10033: не перехватывать исключения в транзакции (#2478)  [ https://github.yandex-team.ru/idm/backend/commit/37da28e4f ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-15 10:57:12+03:00

140.169
-------
 * IDM-9981: фикс логирования в батч-ручке (#2474)  [ https://github.yandex-team.ru/idm/backend/commit/791f158a5 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-14 10:07:54+03:00

140.168
-------
 * Еще фикс миграций  [ https://github.yandex-team.ru/idm/backend/commit/fde8e5fef ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-13 12:12:33+03:00

140.167
-------
 * Ненужная миграция  [ https://github.yandex-team.ru/idm/backend/commit/78fa9de67 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-13 10:25:57+03:00

140.166
-------
 * IDM-7914: еще правки                 [ https://github.yandex-team.ru/idm/backend/commit/bfb4b7082 ]
 * IDM-9981: metrics_framework (#2471)  [ https://github.yandex-team.ru/idm/backend/commit/53c677571 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-10 14:37:20+03:00

140.165
-------
 * Удалить use_speedup (#2439)                               [ https://github.yandex-team.ru/idm/backend/commit/703c2fd6b ]
 * IDM-10015: Получать ответственных за один запрос (#2451)  [ https://github.yandex-team.ru/idm/backend/commit/a7c7d5437 ]
 * IDM-7914: еще правки                                      [ https://github.yandex-team.ru/idm/backend/commit/f9c3f3618 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-10 13:53:59+03:00

140.164
-------
 * IDM-7914: правки конфига  [ https://github.yandex-team.ru/idm/backend/commit/f53edca6e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-09 13:30:29+03:00

140.163
-------
 * IDM-7914: формат tvm_id  [ https://github.yandex-team.ru/idm/backend/commit/d0e3c342e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-09 12:40:08+03:00

140.162
-------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9553: Разделить валидацию отзыва ролей по инициаторам отзыва (#2466)  [ https://github.yandex-team.ru/idm/backend/commit/1431d8bc7 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-09 10:37:21+03:00

140.161
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7914: ходить в паспорт с твм (#2457)  [ https://github.yandex-team.ru/idm/backend/commit/aa56513d7 ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * fix passport support url (#2455)  [ https://github.yandex-team.ru/idm/backend/commit/890c312fb ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-09 10:35:28+03:00

140.160
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Возвращаемся на uruz/closuretree (#2470)  [ https://github.yandex-team.ru/idm/backend/commit/45c9f387e ]

* [Anastasiia Isaeva](http://staff/pixel@yandex-team.ru)

 * IDM-9741: TestpalmId для теста воркфлоу. get_head_of_or_zam (#2463)  [ https://github.yandex-team.ru/idm/backend/commit/784c26ce3 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-08 17:57:27+03:00

140.159
-------
 * fix (#2469)  [ https://github.yandex-team.ru/idm/backend/commit/3fb18a9aa ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-08 13:55:29+03:00

140.158
-------
 * IDM-9981: правки (#2467)  [ https://github.yandex-team.ru/idm/backend/commit/f68e5e86f ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-08 13:00:05+03:00

140.157
-------
 * IDM-10006: Ubuntu 20.04 (#2393)  [ https://github.yandex-team.ru/idm/backend/commit/f1cec750b ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-07 18:21:59+03:00

140.156
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7276 IDM-9981: фиксы (#2465)  [ https://github.yandex-team.ru/idm/backend/commit/d56ac23f3 ]

* [Anastasiia Isaeva](http://staff/pixel@yandex-team.ru)

 * IDM-9758: TestpalID для теста про протухание запрошенной роли без аппрува (#2464)   [ https://github.yandex-team.ru/idm/backend/commit/b8bd9aa70 ]
 * IDM-9545: Проставила tespalmId для теста на проверку механизма threshold'a (#2462)  [ https://github.yandex-team.ru/idm/backend/commit/1871832d4 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-07 13:58:06+03:00

140.155
-------
 * IDM-7276: quote  [ https://github.yandex-team.ru/idm/backend/commit/b0689e44e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-07 10:59:55+03:00

140.154
-------
 * IDM-7277: redis3 (#2461)   [ https://github.yandex-team.ru/idm/backend/commit/d1dabeede ]
 * IDM-7276: celery4 (#2460)  [ https://github.yandex-team.ru/idm/backend/commit/0640141fd ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-06 15:22:56+03:00

140.153
-------
 * IDM-9981: TEMPLATES  [ https://github.yandex-team.ru/idm/backend/commit/15bc03e74 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-06 14:54:19+03:00

140.152
-------
 * IDM-9981: DISABLE_SERVER_SIDE_CURSORS  [ https://github.yandex-team.ru/idm/backend/commit/c5fb43a76 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-06 13:22:23+03:00

140.151
-------
 * IDM-9981: django 2.2 (#2397)  [ https://github.yandex-team.ru/idm/backend/commit/9351e2529 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-07-06 12:56:13+03:00

140.150
-------
 * IDM-9847: fix role redundant ttl not being erased (#2459)  [ https://github.yandex-team.ru/idm/backend/commit/d5b356e93 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-07-02 12:21:03+03:00

140.149
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Revert "Revert "IDM-9847: fix; re-calc expiration and review dates on wf rerun (#2454)""  [ https://github.yandex-team.ru/idm/backend/commit/26721d292 ]
 * Revert "Revert "Role: don't keep both ttl_days and ttl_date (#2444)""                     [ https://github.yandex-team.ru/idm/backend/commit/f352d96b8 ]

* [Anastasiia Isaeva](http://staff/pixel@yandex-team.ru)

 * IDM-9742: Test all_heads_of inn workflow (#2456)  [ https://github.yandex-team.ru/idm/backend/commit/89318c109 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-30 18:35:46+03:00

140.148
-------
 * Revert "IDM-9847: fix; re-calc expiration and review dates on wf rerun (#2454)"  [ https://github.yandex-team.ru/idm/backend/commit/ae2e2b51f ]
 * Revert "Role: don't keep both ttl_days and ttl_date (#2444)"                     [ https://github.yandex-team.ru/idm/backend/commit/fad94ab2a ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-30 18:18:03+03:00

140.147
-------
 * IDM-9845: фильтровать по дате (#2458)  [ https://github.yandex-team.ru/idm/backend/commit/0456f441c ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-30 15:11:36+03:00

140.146
-------
 * IDM-9847: fix; re-calc expiration and review dates on wf rerun (#2454)  [ https://github.yandex-team.ru/idm/backend/commit/1a6769ea5 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-06-30 14:54:35+03:00

140.145
-------
 * IDM-9845: rename params  [ https://github.yandex-team.ru/idm/backend/commit/3af19e33e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-30 10:56:16+03:00

140.144
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9845: не перезапрашивать роли, если не меняются обязанности (#2448)  [ https://github.yandex-team.ru/idm/backend/commit/7e1c25c92 ]
 * IDM-9874: холдить членства на 15 минут, чтобы не было гонок (#2450)      [ https://github.yandex-team.ru/idm/backend/commit/fb327b22c ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9916: improve how bad nodes are counted (#2449)  [ https://github.yandex-team.ru/idm/backend/commit/1bdd85cfb ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-29 11:59:37+03:00

140.143
-------
 * Обновить версию ct (#2452)  [ https://github.yandex-team.ru/idm/backend/commit/cf1f1d6fa ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-24 23:45:10+03:00

140.142
-------
 * Role: don't keep both ttl_days and ttl_date (#2444)  [ https://github.yandex-team.ru/idm/backend/commit/a8dd0538b ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-06-24 12:55:20+03:00

140.141
-------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9915: node suggest not working with ctrl+v (#2447)  [ https://github.yandex-team.ru/idm/backend/commit/4d5b3165a ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9336: искать только активные узлы (#2446)  [ https://github.yandex-team.ru/idm/backend/commit/d3005498a ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-06-23 16:00:59+03:00

140.140
-------
 * Отселить пайплайн в отдельную очередь (#2442)  [ https://github.yandex-team.ru/idm/backend/commit/5603693f1 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-22 11:13:35+03:00

140.139
-------
 * Revert "Revert "IDM-9552: Добавить в апи параметр "Валидировать ли отзыв". default=false (#2431)""  [ https://github.yandex-team.ru/idm/backend/commit/3c4cc89d5 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-18 15:52:29+03:00

140.138
-------
 * Revert "IDM-9552: Добавить в апи параметр "Валидировать ли отзыв". default=false (#2431)"  [ https://github.yandex-team.ru/idm/backend/commit/3307dd249 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-18 09:12:50+03:00

140.137
-------
 * fix try_userify  [ https://github.yandex-team.ru/idm/backend/commit/f371fdfa2 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-17 15:47:28+03:00

140.136
-------
 * try_userify (#2441)  [ https://github.yandex-team.ru/idm/backend/commit/cabbcf979 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-17 12:57:19+03:00

140.135
-------
 * IDM-9899: Не восстанавливать узлы, которые уже начали удаляться (#2440)  [ https://github.yandex-team.ru/idm/backend/commit/d14d731aa ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-16 17:48:57+03:00

140.134
-------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9811: do not send passport login notification for no_robots group roles (#2433)  [ https://github.yandex-team.ru/idm/backend/commit/dcd40a9a2 ]
 * IDM-9530: Use slave db (#2436)                                                       [ https://github.yandex-team.ru/idm/backend/commit/1b7e7cbd3 ]
 * add debug resource; behaviour is controlled by switches (#2438)                      [ https://github.yandex-team.ru/idm/backend/commit/3b40e4ef7 ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9881: проверять, что паспортный логин соответствует внутреннему (#2437)  [ https://github.yandex-team.ru/idm/backend/commit/1ee6d87c8 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-06-11 15:12:06+03:00

140.133
-------
 * IDM-9552: Добавить в апи параметр "Валидировать ли отзыв". default=false (#2431)  [ https://github.yandex-team.ru/idm/backend/commit/a21fb2df4 ]
 * Revert "Revert "IDM-5764: implement db retry on cursor-level (#2359)"" (#2434)    [ https://github.yandex-team.ru/idm/backend/commit/1cdaffd57 ]
 * IDM-9756: тест на регулярный пересмотр персональных ролей (#2430)                 [ https://github.yandex-team.ru/idm/backend/commit/f12339d44 ]
 * IDM-9753: тест на создание/удаление персональных ролей (#2429)                    [ https://github.yandex-team.ru/idm/backend/commit/0a9cf7495 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-09 11:24:20+03:00

140.132
-------
 * Еще более новый пайплайн (#2432)  [ https://github.yandex-team.ru/idm/backend/commit/ba4a058e4 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-04 22:18:44+03:00

140.131
-------
 * Revert "IDM-5764: implement db retry on cursor-level (#2359)"  [ https://github.yandex-team.ru/idm/backend/commit/83058b921 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-02 17:03:18+03:00

140.130
-------
 * Revert "IDM-9807: fix cursor-level retry; recreating a cursor after reconnect (#2420)"  [ https://github.yandex-team.ru/idm/backend/commit/ac7f5ec2f ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-02 14:11:11+03:00

140.129
-------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9806: fix suggest not using proxied suggest (#2428)  [ https://github.yandex-team.ru/idm/backend/commit/333141ea9 ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Пересчитывать только активные узлы (#2427)  [ https://github.yandex-team.ru/idm/backend/commit/0e5540d3b ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-06-02 11:19:15+03:00

140.128
-------
 * IDM-9806: fix suggest not working on groups (#2426)  [ https://github.yandex-team.ru/idm/backend/commit/633225b36 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-06-01 16:31:34+03:00

140.127
-------
 * IDM-9447: удалить код про ad_groups (#2425)  [ https://github.yandex-team.ru/idm/backend/commit/09a1f83f3 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-29 16:24:00+03:00

140.126
-------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9761: Мониторинг и алерт на долгое время выдачи ролей (#2423)  [ https://github.yandex-team.ru/idm/backend/commit/6c6051c2e ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9798: Новый пайплайн (#2289)  [ https://github.yandex-team.ru/idm/backend/commit/a19d7241f ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9818: fix system form not able to set field to None (#2424)  [ https://github.yandex-team.ru/idm/backend/commit/530ed69d3 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-29 10:26:41+03:00

140.125
-------
 * IDM-9571: fix yql syntax (#2422)  [ https://github.yandex-team.ru/idm/backend/commit/f3ba5423b ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-27 11:31:09+03:00

140.124
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Worklofw python3 doctest (#2391)                               [ https://github.yandex-team.ru/idm/backend/commit/8116dbe09 ]
 * IDM-9571: График ошибок узел в дереве ролей не найден (#2419)  [ https://github.yandex-team.ru/idm/backend/commit/060c29ca5 ]
 * IDM-9786: отзывать роли сразу при удалении узла (#2421)        [ https://github.yandex-team.ru/idm/backend/commit/abf155a9f ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9807: fix cursor-level retry; recreating a cursor after reconnect (#2420)  [ https://github.yandex-team.ru/idm/backend/commit/a09a34065 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-27 10:35:47+03:00

140.123
-------
 * Убрать auto_now_add (#2418)                                     [ https://github.yandex-team.ru/idm/backend/commit/e45c45775 ]
 * IDM-9544: Тест на блокировку уволенных в AD (#2416)             [ https://github.yandex-team.ru/idm/backend/commit/546058001 ]
 * IDM-9757: тест на регулярный пересмотр групповых ролей (#2414)  [ https://github.yandex-team.ru/idm/backend/commit/61b3ce674 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-26 10:22:10+03:00

140.122
-------
 * IDM-9772: добавить use_workflow_for_deprive в настройки (#2412)  [ https://github.yandex-team.ru/idm/backend/commit/8b45ca4f0 ]
 * Добавить количество запусков (#2413)                             [ https://github.yandex-team.ru/idm/backend/commit/3bfff07d7 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-20 19:28:27+03:00

140.121
-------
 * IDM-9613: не удалять из ad-групп при включенном флаге (#2411)  [ https://github.yandex-team.ru/idm/backend/commit/4654b1424 ]
 * IDM-9740: фикс формата                                         [ https://github.yandex-team.ru/idm/backend/commit/bc6f36313 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-19 15:56:39+03:00

140.120
-------
 * Порядок миграций  [ https://github.yandex-team.ru/idm/backend/commit/992d6a47a ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-19 13:24:39+03:00

140.119
-------
 * IDM-9740: добавить логи про несуществующий узел (#2410)  [ https://github.yandex-team.ru/idm/backend/commit/0b2669f73 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-19 12:34:28+03:00

140.118
-------
 * fix conflict email (#2409)  [ https://github.yandex-team.ru/idm/backend/commit/f62fbcf41 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-05-18 17:24:19+03:00

140.117
-------
 * fix validation (#2408)  [ https://github.yandex-team.ru/idm/backend/commit/49e660dc1 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-05-18 12:55:56+03:00

140.116
-------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-05-18 12:46:07+03:00

140.115
-------

* [Mira Sharf](http://staff/mirasharf@yandex-team.ru)

 * IDM-9462-1: Delete prefix in firewall-declaration (#2404)  [ https://github.yandex-team.ru/idm/backend/commit/bef249405 ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * add ticket comment (#2407)  [ https://github.yandex-team.ru/idm/backend/commit/9c83030ca ]

[Mira Sharf](http://staff/mirasharf@yandex-team.ru) 2020-05-16 18:47:32+03:00

140.114
-------
 * IDM-9498: implement serialization for conflict wrappers (#2406)  [ https://github.yandex-team.ru/idm/backend/commit/48cb09d25 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-05-15 14:28:06+03:00

140.113
-------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9499: create conflict_comment action (#2396)  [ https://github.yandex-team.ru/idm/backend/commit/6920cdf2f ]

[Mira Sharf](http://staff/mirasharf@yandex-team.ru) 2020-05-14 18:23:14+03:00

140.112
-------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9498: find_conflicts is available from withing WF (#2395)  [ https://github.yandex-team.ru/idm/backend/commit/bb38971e3 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-14 12:54:07+03:00

140.111
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9456: не откладывать системочленства (#2403)  [ https://github.yandex-team.ru/idm/backend/commit/8e69b1736 ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9497: extract find_conflicts (#2387)  [ https://github.yandex-team.ru/idm/backend/commit/e864c4c4d ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-14 12:24:01+03:00

140.110
-------
 * IDM-9573: считать только полезные запуски пайплайна (#2400)  [ https://github.yandex-team.ru/idm/backend/commit/907fe9e14 ]
 * IDM-9572: Оценивать состояние дерева ABC (#2399)             [ https://github.yandex-team.ru/idm/backend/commit/4955788d8 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-14 12:04:06+03:00

140.109
-------

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-13 15:08:40+03:00

140.108
-------
 * Сверка членств запускается раз в сутки (#2402)  [ https://github.yandex-team.ru/idm/backend/commit/c2fc8a5cf ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-13 15:07:24+03:00

140.107
-------
 * IDM-9470: fix checking per-system permission (#2401)  [ https://github.yandex-team.ru/idm/backend/commit/68e479fd8 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-05-12 18:34:49+03:00

140.106
-------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-05-08 20:09:05+03:00

140.105
-------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-05-08 19:56:26+03:00

140.104
-------
 * add migration for new role (#2398)  [ https://github.yandex-team.ru/idm/backend/commit/b9813613e ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-05-08 19:06:57+03:00

140.103
-------
 * IDM-9446: новый формат  [ https://github.yandex-team.ru/idm/backend/commit/13ac57c49 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-07 19:44:58+03:00

140.102
-------
 * IDM-9469: fix original_requester not being wrapped (#2394)  [ https://github.yandex-team.ru/idm/backend/commit/d7229b05d ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-05-07 17:40:04+03:00

140.101
-------
 * IDM-9446: Переинтерпретируем ad_groups как ref_roles (#2370)  [ https://github.yandex-team.ru/idm/backend/commit/74808a18e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-07 10:27:01+03:00

140.100
-------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9470: depriver that can deprive without workflow (#2375)  [ https://github.yandex-team.ru/idm/backend/commit/1beba20b9 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-05-06 12:47:18+03:00

140.99
------
 * Импорты для контейнера воркфлоу  [ https://github.yandex-team.ru/idm/backend/commit/962f519f1 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-30 19:52:02+03:00

140.98
------
 * fix py2 compatibility (#2390)  [ https://github.yandex-team.ru/idm/backend/commit/8c5e14853 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-30 19:07:47+03:00

140.97
------
 * IDM-9469: Reproduce original deprive process with wf-deprive (#2389)  [ https://github.yandex-team.ru/idm/backend/commit/0d1aa3e40 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-30 17:21:31+03:00

140.96
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Обновить ABC_TVM_MANAGER_ROLE  [ https://github.yandex-team.ru/idm/backend/commit/d0baac7e5 ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9469: fix wf-deprive deal with fired; fix empty approvers behaviour (#2386)  [ https://github.yandex-team.ru/idm/backend/commit/357641bfe ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-30 16:44:06+03:00

140.95
------
 * Revert "Revert "IDM-9375: При перемещении и одновременном пересоздании узла дерева ролей по тому же пути, unique_id не работает (#2355)""  [ https://github.yandex-team.ru/idm/backend/commit/f337c9912 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-30 12:55:51+03:00

140.94
------
 * IDM-9566: Использовать StrictForeignKey в users/models.py (#2371)  [ https://github.yandex-team.ru/idm/backend/commit/36e8cd06a ]
 * IDM-9549: не обновлять хеш в cauth (#2385)                         [ https://github.yandex-team.ru/idm/backend/commit/f907c2ab3 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-30 11:12:04+03:00

140.93
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9556: Один раз проверять необходимость логина для узла (#2384)  [ https://github.yandex-team.ru/idm/backend/commit/e18cc5eb5 ]

140.92
------
 * Revert "Revert (#2383)"  [ https://github.yandex-team.ru/idm/backend/commit/52f8f7bbc ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-27 13:37:45+03:00

140.91
------
 * Revert (#2383)  [ https://github.yandex-team.ru/idm/backend/commit/7b73d357b ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-27 13:30:56+03:00

140.90
------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * IDM-9439: fix weekend behaviour (#2381)  [ https://github.yandex-team.ru/idm/backend/commit/c36b76247 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-27 12:57:50+03:00

140.89
------
 * IDM-9462: Prefix in firewall-declaration (#2379)  [ https://github.yandex-team.ru/idm/backend/commit/fa319903e ]

[Mira Sharf](http://staff/mirasharf@yandex-team.ru) 2020-04-27 12:33:25+03:00

140.88
------
 * Добавить update_fields (#2380)  [ https://github.yandex-team.ru/idm/backend/commit/65d52b2fd ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-27 11:49:27+03:00

140.87
------
 * IDM-9533: не писать контекст в логи (#2377)                     [ https://github.yandex-team.ru/idm/backend/commit/6c18c4052 ]
 * IDM-9535: оптимизировать проверку необходимости логина (#2378)  [ https://github.yandex-team.ru/idm/backend/commit/c4333de0b ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-27 11:30:34+03:00

140.86
------
 * Миграции                   [ https://github.yandex-team.ru/idm/backend/commit/f1841d75d ]
 * Revert "Порядок миграций"  [ https://github.yandex-team.ru/idm/backend/commit/bf32978a4 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-24 16:56:41+03:00

140.85
------
 * Порядок миграций  [ https://github.yandex-team.ru/idm/backend/commit/164369724 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-24 16:52:02+03:00

140.84
------
 * [IDM-9469]: implement workflow for deprive (#2361)  [ https://github.yandex-team.ru/idm/backend/commit/621128d92 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-24 16:30:13+03:00

140.83
------
 * order by slug (#2376)  [ https://github.yandex-team.ru/idm/backend/commit/41bb01128 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-24 13:24:08+03:00

140.82
------
 * Ускорение получения одного approverequest (#2364)     [ https://github.yandex-team.ru/idm/backend/commit/773ce435b ]
 * Update .devexp.json                                   [ https://github.yandex-team.ru/idm/backend/commit/ab05aa4ba ]
 * Update .devexp.json                                   [ https://github.yandex-team.ru/idm/backend/commit/84c21124b ]
 * IDM-9522: Не берется лок в допинывалке ролей (#2372)  [ https://github.yandex-team.ru/idm/backend/commit/a4e743e7e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-23 17:55:42+03:00

140.81
------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-23 12:21:05+03:00

140.80
------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * [IDM-9439] fix command in cron task  [ https://github.yandex-team.ru/idm/backend/commit/e0b2e7776 ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9465: stop (#2369)  [ https://github.yandex-team.ru/idm/backend/commit/fe810a922 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-23 12:20:33+03:00

140.79
------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-22 12:02:54+03:00

140.78
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * fix tests  [ https://github.yandex-team.ru/idm/backend/commit/1866d669b ]

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * [IDM-9439] Spread system sync over daytime, to decrease peak load (#2354)  [ https://github.yandex-team.ru/idm/backend/commit/b8c9bdd7a ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-22 12:01:44+03:00

140.77
------

* [Mira Sharf](http://staff/mirasharf@yandex-team.ru)

 * IDM-8641: fields_data in email templates (#2353)  [ https://github.yandex-team.ru/idm/backend/commit/ae1bff8f8 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-21 15:15:46+03:00

140.76
------
 * import return  [ https://github.yandex-team.ru/idm/backend/commit/2a06c0aec ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-21 14:38:30+03:00

140.75
------
 * import return                                                 [ https://github.yandex-team.ru/idm/backend/commit/c5df8e375 ]
 * IDM-9495: обрабатывать отрицательные id (#2362)               [ https://github.yandex-team.ru/idm/backend/commit/9f704826b ]
 * IDM-9506: отзывать персональные роли уволенных сразу (#2363)  [ https://github.yandex-team.ru/idm/backend/commit/650837252 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-21 14:29:09+03:00

140.74
------
 * IDM-9471: raise Return() in workflow (#2360)  [ https://github.yandex-team.ru/idm/backend/commit/6f9c8f8f8 ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-20 13:21:00+03:00

140.73
------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-16 14:42:17+03:00

140.72
------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-16 14:37:29+03:00

140.71
------

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-16 14:34:21+03:00

140.70
------
 * IDM-5764: implement db retry on cursor-level (#2359)  [ https://github.yandex-team.ru/idm/backend/commit/06b6ce27d ]

[Georgy Usatenko](http://staff/ksticks@yandex-team.ru) 2020-04-16 14:22:06+03:00

140.69
------
 * batch tvmmiddleware  [ https://github.yandex-team.ru/idm/backend/commit/7591adab6 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-14 15:18:43+03:00

140.68
------
 * f  [ https://github.yandex-team.ru/idm/backend/commit/58c6fbd09 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-14 14:13:27+03:00

140.67
------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-9459: Ошибка при выдаче роли "name 'all_heads_of' is not defined" (#2357)  [ https://github.yandex-team.ru/idm/backend/commit/4511965a1 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-14 13:38:24+03:00

140.66
------
 * Revert "IDM-9375: При перемещении и одновременном пересоздании узла дерева ролей по тому же пути, unique_id не работает (#2355)"  [ https://github.yandex-team.ru/idm/backend/commit/76845921c ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-14 10:27:57+03:00

140.65
------
 * IDM-9063: Восстанавливать удаленные SystemRoleField при PATCH (#2358)  [ https://github.yandex-team.ru/idm/backend/commit/0480fbe3b ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-14 10:12:11+03:00

140.64
------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9375: При перемещении и одновременном пересоздании узла дерева ролей по тому же пути, unique_id не работает (#2355)  [ https://github.yandex-team.ru/idm/backend/commit/95a7e8658 ]

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-04-13 15:10:12+05:00

140.63
------

* [Georgy Usatenko](http://staff/ksticks@yandex-team.ru)

 * [IDM-9434] Проставляем need_intrasearch_push_method перед выполнением… (#2351)  [ https://github.yandex-team.ru/idm/backend/commit/2c7df4b59 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-09 13:20:55+03:00

140.62
------

* [Egor Polyakov](http://staff/poegva@yandex-team.ru)

 * IDM-9391: email_cc в персональных ролях (#2347)  [ https://github.yandex-team.ru/idm/backend/commit/65e0d6d99 ]

[poegva](http://staff/poegva@yandex-team.ru) 2020-04-09 12:43:56+03:00

140.61
------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9216: Что-то придумать с проверкой уволенных в воркфлоу (#2352)  [ https://github.yandex-team.ru/idm/backend/commit/2e179d71d ]

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-04-08 22:27:53+05:00

140.60
------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9216: Что-то придумать с проверкой уволенных в воркфлоу (#2348)  [ https://github.yandex-team.ru/idm/backend/commit/5ef3c83fe ]

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-04-08 18:45:31+05:00

140.59
------
 * IDM-9331: initial properties (#2350)  [ https://github.yandex-team.ru/idm/backend/commit/9ae64aa8a ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-08 14:19:20+03:00

140.58
------

* [Egor Polyakov](http://staff/poegva@yandex-team.ru)

 * IDM-8810: Графики о количестве перезапрошенных ролей (#2343)  [ https://github.yandex-team.ru/idm/backend/commit/ada7af783 ]

[poegva](http://staff/poegva@yandex-team.ru) 2020-04-06 13:58:30+03:00

140.57
------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9216: Что-то придумать с проверкой уволенных в воркфлоу (#2346)  [ https://github.yandex-team.ru/idm/backend/commit/72d170a87 ]

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-04-06 15:43:39+05:00

140.56
------
 * Revert "Revert "IDM-9216: Что-то придумать с проверкой уволенных в воркфлоу (#2331)""  [ https://github.yandex-team.ru/idm/backend/commit/a731fffb1 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-06 12:46:53+03:00

140.55.1
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9331: initial properties (#2350)                    [ https://github.yandex-team.ru/idm/backend/commit/debc5f182 ]

* [Egor Polyakov](http://staff/poegva@yandex-team.ru)

 * IDM-8810: Графики о количестве перезапрошенных ролей (#2343)  [ https://github.yandex-team.ru/idm/backend/commit/ce049c0f1 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-08 14:57:45+03:00

140.55
------
 * Revert "IDM-9216: Что-то придумать с проверкой уволенных в воркфлоу (#2331)"  [ https://github.yandex-team.ru/idm/backend/commit/2936cf507 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-06 12:29:41+03:00

140.54
------

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-03 14:37:10+03:00

140.53
------
 * Отдавать rolefields в editable_fields (#2341)                         [ https://github.yandex-team.ru/idm/backend/commit/c7ecfdead ]
 * IDM-9417: Ретраящиеся ошибки от системы перестали ретраиться (#2344)  [ https://github.yandex-team.ru/idm/backend/commit/2093c72bd ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-03 14:34:43+03:00

140.52
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * remove typehints        [ https://github.yandex-team.ru/idm/backend/commit/a6530536a ]
 * IDM-9375: тест (#2335)  [ https://github.yandex-team.ru/idm/backend/commit/212fca51c ]

* [Alexey Ryzhov](http://staff/binny@yandex-team.ru)

 * IDM-9384-1: одинаковый choices для полей plugin_type в *SystemEditForm (#2338)  [ https://github.yandex-team.ru/idm/backend/commit/8096871cc ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * Update .devexp.json  [ https://github.yandex-team.ru/idm/backend/commit/82f2727e4 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-04-03 12:11:31+03:00

140.51
------

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-04-02 15:53:16+05:00

140.50
------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9216: Что-то придумать с проверкой уволенных в воркфлоу (#2331)  [ https://github.yandex-team.ru/idm/backend/commit/3fc017157 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-9332: role.fetch_parent() (#2342)           [ https://github.yandex-team.ru/idm/backend/commit/91a3976e6 ]
 * releasing version 140.45                        [ https://github.yandex-team.ru/idm/backend/commit/792c64ab6 ]
 * IDM-9332: Оптимизация is_force_deprive (#2337)  [ https://github.yandex-team.ru/idm/backend/commit/9b0596c09 ]

* [poegva](http://staff/poegva@yandex-team.ru)

 * releasing version 140.49  [ https://github.yandex-team.ru/idm/backend/commit/57ed38359 ]
 * releasing version 140.48  [ https://github.yandex-team.ru/idm/backend/commit/5e58034d9 ]
 * releasing version 140.47  [ https://github.yandex-team.ru/idm/backend/commit/34f1ec0b5 ]

* [Egor Polyakov](http://staff/poegva@yandex-team.ru)

 * releasing version 140.46                                             [ https://github.yandex-team.ru/idm/backend/commit/14c32596a ]
 * IDM-8810: Графики о количестве перезапрошенных ролей (#2339)         [ https://github.yandex-team.ru/idm/backend/commit/e764f9a46 ]
 * IDM-9280 Брать ответственных за сервисную группу из сервиса (#2336)  [ https://github.yandex-team.ru/idm/backend/commit/1503c0b8b ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * releasing version 140.44  [ https://github.yandex-team.ru/idm/backend/commit/4fbfc9bb9 ]

[alexsaplin](http://staff/alexsaplin@yandex-team.ru) 2020-04-02 15:51:41+05:00

140.49
------

[poegva](http://staff/poegva@yandex-team.ru) 2020-04-02 12:57:41+03:00

140.48
------

[poegva](http://staff/poegva@yandex-team.ru) 2020-04-02 12:45:46+03:00

140.47
------

[poegva](http://staff/poegva@yandex-team.ru) 2020-04-02 12:43:33+03:00

140.46
------
 * IDM-8810: Графики о количестве перезапрошенных ролей (#2339)         [ https://github.yandex-team.ru/idm/backend/commit/e764f9a46 ]
 * IDM-9280 Брать ответственных за сервисную группу из сервиса (#2336)  [ https://github.yandex-team.ru/idm/backend/commit/1503c0b8b ]

[Egor Polyakov](http://staff/poegva@yandex-team.ru) 2020-04-02 11:57:29+03:00

140.45
------
 * IDM-9332: Оптимизация is_force_deprive (#2337)  [ https://github.yandex-team.ru/idm/backend/commit/9b0596c09 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2020-03-31 12:59:13+03:00

140.44
------

* [Alexey Saplin](http://staff/alexsaplin@yandex-team.ru)

 * fix: tests fix                                          [ https://github.yandex-team.ru/idm/backend/commit/15f3758c1 ]
 * fix: minor fixes                                        [ https://github.yandex-team.ru/idm/backend/commit/795aec7f0 ]
 * IDM-9174: Добавить трейс в action.data, если упал синк  [ https://github.yandex-team.ru/idm/backend/commit/0b857d96f ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-31 12:43:13+03:00

140.43
------
 * IDM-9384 Разрешить редактировать поля (адрес ручки и tvm_id) ответств… (#2333)  [ https://github.yandex-team.ru/idm/backend/commit/8cbb65528 ]
 * IDM-9371: поправить сообщение об ошибке (#2329)                                 [ https://github.yandex-team.ru/idm/backend/commit/90b9ae8ce ]

[Alexey Ryzhov](http://staff/binny@yandex-team.ru) 2020-03-30 15:32:01+03:00

140.42
------
 * Исправлен конфликт миграций  [ https://github.yandex-team.ru/idm/backend/commit/b3a57c273 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-03-30 13:23:15+03:00

140.41
------
 * IDM-9330: добавлено профилирование вызовов workflow (#2332)  [ https://github.yandex-team.ru/idm/backend/commit/d6ffd00d4 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-03-27 14:22:19+03:00

140.40
------
 * IDM-9121: New state failed_in_idm (#2320)  [ https://github.yandex-team.ru/idm/backend/commit/0c5be3015 ]

[Mira Sharf](http://staff/mirasharf@yandex-team.ru) 2020-03-26 11:04:28+03:00

140.39
------
 * IDM-9370: перевыбрасывать исключение от базы при nowait (#2330)  [ https://github.yandex-team.ru/idm/backend/commit/2d05ae6c4 ]
 * IDM-9366: Добавить группу в легкий ответ апи (#2328)             [ https://github.yandex-team.ru/idm/backend/commit/5ab23b000 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-25 14:15:44+03:00

140.38
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9334: считать метрики за день (#2326)                                   [ https://github.yandex-team.ru/idm/backend/commit/3641982d4 ]
 * IDM-9362: отзывать роли, у которых в экшене нет стейта (#2325)              [ https://github.yandex-team.ru/idm/backend/commit/3ff078988 ]
 * IDM-9360: Не отзывать роли в статусе depriving_validation из синка (#2324)  [ https://github.yandex-team.ru/idm/backend/commit/5c6a03a04 ]

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-9306 Не отрываем группы перенанятым (#2327)  [ https://github.yandex-team.ru/idm/backend/commit/a78f0d3b3 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-24 11:51:17+03:00

140.37
------

* [Saplin Aleksei](http://staff/alexsaplin@yandex-team.ru)

 * IDM-9322: Письма про неконсистентности не приходят ответственным за с… (#2323)  [ https://github.yandex-team.ru/idm/backend/commit/2c0d061c3 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-23 17:26:02+03:00

140.36
------
 * IDM-9332: Cache is empty в отзыве ролей часто загорается (#2321)  [ https://github.yandex-team.ru/idm/backend/commit/7472e136e ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2020-03-20 15:01:43+03:00

140.35
------
 * фикс миграции  [ https://github.yandex-team.ru/idm/backend/commit/43a11a5cb ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-20 14:05:06+03:00

140.34
------
 * IDM-9345: Ручка со списком полей (#2322)  [ https://github.yandex-team.ru/idm/backend/commit/b79c6eeb8 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-20 13:58:19+03:00

140.33
------
 * IDM-9030: Перестать бесконечно перезапрашивать персональные роли (#2271)  [ https://github.yandex-team.ru/idm/backend/commit/0cd6736c3 ]

[Alexey Ryzhov](http://staff/binny@yandex-team.ru) 2020-03-19 16:39:44+03:00

140.32
------
 * IDM-9335: select_related (#2319)  [ https://github.yandex-team.ru/idm/backend/commit/fbc8957bc ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-18 12:44:48+03:00

140.31
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9303: выполнять works_in_dep в контейнере (#2316)  [ https://github.yandex-team.ru/idm/backend/commit/80d76e213 ]

* [Mira Sharf](http://staff/mirasharf@yandex-team.ru)

 * IDM-9311: Plugin generic self (#2317)  [ https://github.yandex-team.ru/idm/backend/commit/faa4ca543 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-16 17:58:50+03:00

140.30
------
 * log  [ https://github.yandex-team.ru/idm/backend/commit/5d19ab336 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-16 11:32:33+03:00

140.29
------
 * Не ждать лок при выдаче роли (#2318)  [ https://github.yandex-team.ru/idm/backend/commit/3c478ba99 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-13 13:10:29+03:00

140.28
------

* [Mira Sharf](http://staff/mirasharf@yandex-team.ru)

 * IDM-9248: Processing is_exclusive (#2307)  [ https://github.yandex-team.ru/idm/backend/commit/a81f4cf43 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-12 11:22:49+03:00

140.27
------
 * Удалить ненужные столбцы (#2315)  [ https://github.yandex-team.ru/idm/backend/commit/65b08814d ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-11 15:04:32+03:00

140.26
------

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-9225: get_service_chain_of_heads возвращает только активных подтверждающих (#2314)  [ https://github.yandex-team.ru/idm/backend/commit/5a9089d41 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-11 13:34:44+03:00

140.25
------

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-9225: Разные гроуп врапперы в разных средах (#2313)  [ https://github.yandex-team.ru/idm/backend/commit/34bccc962 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-03-10 18:45:07+03:00

140.24
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * В образ добавлен pg_repack (#2312)                                  [ https://github.yandex-team.ru/idm/backend/commit/b70b855c5 ]
 * IDM-9284: Отсутствие обработки subject_type в системе self (#2309)  [ https://github.yandex-team.ru/idm/backend/commit/702603af8 ]

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-9225: получаем группы пользователя из wf (#2311)  [ https://github.yandex-team.ru/idm/backend/commit/69f319b84 ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9286: не пытаться отозвать неактивные роли (#2310)  [ https://github.yandex-team.ru/idm/backend/commit/3631efb6d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-03-10 17:29:41+03:00

140.23
------

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-9225: Для сервисной группы chain_of_heads идет по дереву сервисов (#2304)  [ https://github.yandex-team.ru/idm/backend/commit/711cecca0 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-10 12:14:14+03:00

140.22
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9158: ошибка при добавлении/удалении в ad-группу (#2302)  [ https://github.yandex-team.ru/idm/backend/commit/fdeb5b868 ]
 * prefetch_related (#2308)                                      [ https://github.yandex-team.ru/idm/backend/commit/0e8960902 ]

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-9225: В подтверждающих сервиса добавляем лидей из роли "ответвенный" (#2306)  [ https://github.yandex-team.ru/idm/backend/commit/570b2e8c4 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-10 10:41:34+03:00

140.21.1
------
 * IDM-9286: не пытаться отозвать неактивные роли (#2310)  [ https://github.yandex-team.ru/idm/backend/commit/671d26d52 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-10 14:17:04+03:00

140.21
------
 * IDM-9263: ускорение синка (#2305)  [ https://github.yandex-team.ru/idm/backend/commit/bd9098d2a ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-06 11:16:40+03:00

140.20
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-9230 график времени выполнения сверок (#2301)  [ https://github.yandex-team.ru/idm/backend/commit/2dda042 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2020-03-05 11:57:32+03:00

140.19
------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-9252: Убрать gnoma@ из тестовых писем (#2303)  [ https://github.yandex-team.ru/idm/backend/commit/45a74d5a9 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Актуализирована старая миграция  [ https://github.yandex-team.ru/idm/backend/commit/b8cc65ed0 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2020-03-04 14:58:45+03:00

140.18
------
 * Поправлена запись таймстемпов для пушей членств (#2300)  [ https://github.yandex-team.ru/idm/backend/commit/ec3e1b7ab ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-03-04 12:55:30+03:00

140.17
------
 * IDM-8900: audit_backend=memory по умолчанию (#2259)  [ https://github.yandex-team.ru/idm/backend/commit/86221696e ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-03-03 17:37:06+03:00

140.16
------
 * Не пытаться фейлить подтвержденные роли (#2299)  [ https://github.yandex-team.ru/idm/backend/commit/f98342d8a ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-03 14:14:41+03:00

140.15
------
 * Добавить в контекст unique_id (#2298)            [ https://github.yandex-team.ru/idm/backend/commit/df169720c ]
 * Проверять стейт роли в начале RoleAdded (#2297)  [ https://github.yandex-team.ru/idm/backend/commit/820fcbdaa ]
 * Имортировать только модуль с метриками (#2296)   [ https://github.yandex-team.ru/idm/backend/commit/58b21c430 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-03 13:41:32+03:00

140.14
------
 * IDM-9139: разделять deprive и redeprive (#2294)  [ https://github.yandex-team.ru/idm/backend/commit/179624b6e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-03 11:25:26+03:00

140.13
------
 * IDM-9157: Фикс формата ошибки (#2295)  [ https://github.yandex-team.ru/idm/backend/commit/87d9f7ddf ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2020-03-02 20:37:53+03:00

140.12
------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-9157: Мониторинг на залежавшиеся сиды (#2290)  [ https://github.yandex-team.ru/idm/backend/commit/2adebad2b ]

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-9137 время в depriving_validation (#2292)  [ https://github.yandex-team.ru/idm/backend/commit/55d3a0c6f ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Поправлен тест на таймстемпы; report_inconsistencies теперь считается успешным в случае отсутстуия расхождений (#2293)  [ https://github.yandex-team.ru/idm/backend/commit/2cb89fb72 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2020-03-02 19:29:27+03:00

140.11
------
 * IDM-9153: логировать время выполнения сверки (#2288)  [ https://github.yandex-team.ru/idm/backend/commit/ee74a3624 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-02 17:14:41+03:00

140.10
------
 * Порядок миграций  [ https://github.yandex-team.ru/idm/backend/commit/42a17a50d ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-02 13:23:19+03:00

140.9
-----

* [Mira Sharf](http://staff/mirasharf@yandex-team.ru)

 * IDM-9201: is_exclusive (#2277)  [ https://github.yandex-team.ru/idm/backend/commit/61bd4daa2 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-03-02 13:14:54+03:00

140.8
-----

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-8390 Дубликаты алиасов (#2267)  [ https://github.yandex-team.ru/idm/backend/commit/961f53728 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-28 16:42:32+03:00

140.7
-----
 * IDM-9139: экшены про первый пуш в систему (#2274)  [ https://github.yandex-team.ru/idm/backend/commit/ee26e3400 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-28 16:27:31+03:00

140.6
-----
 * IDM-9152: поправлено добавление metainfo новым и старым системам  [ https://github.yandex-team.ru/idm/backend/commit/dbbafeb44 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-02-28 13:47:47+03:00

140.5
-----
 * IDM-9152: Мониторинг на последнее успешное завершение сверки (#2284)  [ https://github.yandex-team.ru/idm/backend/commit/0a50020a6 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-02-28 13:27:55+03:00

140.4
-----
 * Сбрасываю removed_from_groups (#2287)  [ https://github.yandex-team.ru/idm/backend/commit/9a91a118c ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2020-02-28 12:20:45+03:00

140.3
-----
 * IDM-9215: ретраи в проверке is_writable (#2286)  [ https://github.yandex-team.ru/idm/backend/commit/a51aebc06 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-28 12:05:28+03:00

140.2
-----
 * IDM-9159: Фикс условия, разделил метод (#2285)  [ https://github.yandex-team.ru/idm/backend/commit/209360e04 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2020-02-28 11:27:18+03:00

140.1
-----
 * IDM-9207: Выпилить manual_readonly (#2280)  [ https://github.yandex-team.ru/idm/backend/commit/1d7ca5850 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-27 15:26:36+03:00

140.0
-------
 * IDM-9159: Мониторинг на блокировку в AD (#2279)  [ https://github.yandex-team.ru/idm/backend/commit/8fd4102c6 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2020-02-27 14:47:36+03:00

139.110
-------
 * поле TVM ID в *SystemEditForm может принимать только валидные значения (#2282)  [ https://github.yandex-team.ru/idm/backend/commit/7b1a3da68 ]

[Alexey Ryzhov](http://staff/binny@yandex-team.ru) 2020-02-27 13:56:31+03:00

139.109
-------
 * Кешировать необходимость логина (#2283)  [ https://github.yandex-team.ru/idm/backend/commit/8987031f0 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-27 13:26:50+03:00

139.108
-------
 * IDM-9124: не получать все тикеты сразу, так как там пока могут быть невалидные (#2281)  [ https://github.yandex-team.ru/idm/backend/commit/468ed494e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-26 18:36:59+03:00

139.107
-------
 * Миграция  [ https://github.yandex-team.ru/idm/backend/commit/d21d5f737 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-26 17:32:22+03:00

139.106
-------
 * IDM-9136: depriving_validation (#2269)  [ https://github.yandex-team.ru/idm/backend/commit/dd94a4432 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-26 16:48:12+03:00

139.105
-------
 * IDM-9014: Поддержать саджест по TVM в поле метод аутентификации на экране настроек системы (#2254)  [ https://github.yandex-team.ru/idm/backend/commit/ac46f72e2 ]

[Alexey Ryzhov](http://staff/binny@yandex-team.ru) 2020-02-26 12:58:31+03:00

139.104
-------
 * Убрать гарантию контейнеру  [ https://github.yandex-team.ru/idm/backend/commit/71507b703 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-25 16:45:58+03:00

139.103
-------
 * IDM-9198: Логировать запросы в мидлварях (#2276)  [ https://github.yandex-team.ru/idm/backend/commit/c837eb1e6 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-25 16:12:08+03:00

139.102
-------
 * Нужен инт, а не роль  [ https://github.yandex-team.ru/idm/backend/commit/07e229494 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-25 14:27:57+03:00

139.101
-------
 * IDM-9145: закрывать тикет синхронно для групповых ролей, которые не пушатся (#2275)  [ https://github.yandex-team.ru/idm/backend/commit/ec027dd12 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-25 13:22:38+03:00

139.100
-------

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * IDM-9138 комментарий и импорт                        [ https://github.yandex-team.ru/idm/backend/commit/bd51f74 ]
 * IDM-9138 поменьше копипасты                          [ https://github.yandex-team.ru/idm/backend/commit/a0da875 ]
 * IDM-9138 range                                       [ https://github.yandex-team.ru/idm/backend/commit/f843c87 ]
 * IDM-9138 правки                                      [ https://github.yandex-team.ru/idm/backend/commit/2598b21 ]
 * Посистемные графики скорости выдачи/отрывания ролей  [ https://github.yandex-team.ru/idm/backend/commit/328bf95 ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9145: Закрывать тикет обсуждения в отдельном шаге RoleAdded (#2270)  [ https://github.yandex-team.ru/idm/backend/commit/b9b1c3c ]
 * IDM-9190: Обновить конфиг релизера (#2272)                               [ https://github.yandex-team.ru/idm/backend/commit/a254095 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2020-02-25 09:48:23+03:00

139.99
------
 * Убрать cron  [ https://github.yandex-team.ru/idm/backend/commit/03aa98eff ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-20 10:18:08+03:00

139.98
------
 * IDM-9142: Чаще допинывать роли (#2265)  [ https://github.yandex-team.ru/idm/backend/commit/0f789f876 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-19 19:09:34+03:00

139.97
------

* [Mira Sharf](http://staff/mirasharf@yandex-team.ru)

 * IDM-9175: migrate_actions (#2268)  [ https://github.yandex-team.ru/idm/backend/commit/f41e8957e ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9170: Не делать rehash на все дерево каждый раз (#2262)  [ https://github.yandex-team.ru/idm/backend/commit/1aef11285 ]
 * логи celery (#2266)                                          [ https://github.yandex-team.ru/idm/backend/commit/141352498 ]
 * IDM-9154: NodePipeline батчами (#2263)                       [ https://github.yandex-team.ru/idm/backend/commit/1d74bd14c ]
 * IDM-9143: оптимизация допинывалки ролей (#2264)              [ https://github.yandex-team.ru/idm/backend/commit/281498137 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-19 17:34:36+03:00

139.96
------

* [Mira Sharf](http://staff/10015+mirasharf@users.noreply.github.yandex-team.ru)

 * IDM-9110: RoleNodeResponsibilityAction (#2260)  [ https://github.yandex-team.ru/idm/backend/commit/87badb4de ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Parent без last_request (#2261)  [ https://github.yandex-team.ru/idm/backend/commit/aab676def ]

[Mira Sharf](http://staff/mirasharf@yandex-team.ru) 2020-02-18 13:05:59+03:00

139.95
------
 * Ускорение пайплайна (#2258)  [ https://github.yandex-team.ru/idm/backend/commit/c358e2022 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-14 16:30:53+03:00

139.94
------
 * Усорение пайплайна (#2256)                               [ https://github.yandex-team.ru/idm/backend/commit/defd1f61f ]
 * IDM-9115: Брать разные локи в допинывалке ролей (#2257)  [ https://github.yandex-team.ru/idm/backend/commit/8d19e183d ]
 * Удалять responsibility и aliases отдельно (#2255)        [ https://github.yandex-team.ru/idm/backend/commit/3f6f45ec0 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-14 13:49:09+03:00

139.93
------
 * IDM-8900: теперь таска не вешает atomic_retry, экшны пишутся для сист… (#2253)  [ https://github.yandex-team.ru/idm/backend/commit/4c7a76f6c ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-02-14 12:51:44+03:00

139.92
------
 * Revert "Revert "IDM-8900: ручка для запуска синка системочленств (#2243)""  [ https://github.yandex-team.ru/idm/backend/commit/2162ea8bf ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-13 13:19:10+03:00

139.91
------
 * Revert "IDM-8900: ручка для запуска синка системочленств (#2243)"  [ https://github.yandex-team.ru/idm/backend/commit/c334ca4ae ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-13 13:17:41+03:00

139.90
------
 * IDM-9109: Не обновлять nodeset постоянно (#2249)                               [ https://github.yandex-team.ru/idm/backend/commit/5982a61c4 ]
 * IDM-9107:  Перестать использовать save без update_fields для RoleNode (#2250)  [ https://github.yandex-team.ru/idm/backend/commit/e5877eba4 ]
 * IDM-9108: Зачем тут транзакция??? (#2251)                                                [ https://github.yandex-team.ru/idm/backend/commit/70a24e75e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-13 12:11:07+03:00

139.89
------
 * IDM-9042: у наших расхождений теперь не проставляется remote_username и remote_group (#2248)  [ https://github.yandex-team.ru/idm/backend/commit/c1b81c78b ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-02-12 19:29:00+03:00

139.88
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-9042: поправлены remote_data и remote_path у не наших расхождений (#2247)  [ https://github.yandex-team.ru/idm/backend/commit/88effb0ec ]

* [Alexey Ryzhov](http://staff/binny@yandex-team.ru)

 * IDM-9015 Люди с ролью разработчик и суперпользователь в системе IDM м… (#2235)  [ https://github.yandex-team.ru/idm/backend/commit/0247b6e90 ]

[Alexey Ryzhov](http://staff/binny@yandex-team.ru) 2020-02-12 15:02:52+03:00

139.87
------
 * IDM-9042: фикс нерелевантного remote_hash (#2246)  [ https://github.yandex-team.ru/idm/backend/commit/07f22afe1 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-02-11 19:17:05+03:00

139.86
------
 * IDM-9042: наши расхождения на неактивных узлах (#2245)  [ https://github.yandex-team.ru/idm/backend/commit/a3c30920f ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-02-11 17:35:48+03:00

139.85
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-8900: ручка для запуска синка системочленств (#2243)  [ https://github.yandex-team.ru/idm/backend/commit/232c876 ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8549 депапортнизация  [ https://github.yandex-team.ru/idm/backend/commit/d302d00 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2020-02-11 17:01:25+03:00

139.84
------
 * IDM-9042: для расхождений про неизвестных пользователей/группы теперь проставляется узел, если он существует (#2242)  [ https://github.yandex-team.ru/idm/backend/commit/fda6e5686 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-02-11 15:00:26+03:00

139.83
------
 * IDM-9042: Сверка ролей в памяти (#2237)  [ https://github.yandex-team.ru/idm/backend/commit/3e3fbe3b2 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-02-11 13:26:43+03:00

139.82
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-9072 внешние роботы не попадают под внешнюю галку (#2241)  [ https://github.yandex-team.ru/idm/backend/commit/5683261 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2020-02-11 13:00:27+03:00

139.81
------
 * IDM-9083: system в user.has_role (#2240)  [ https://github.yandex-team.ru/idm/backend/commit/b738c484b ]
 * Поднять countdown для выдачи роли         [ https://github.yandex-team.ru/idm/backend/commit/4e55c31e0 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-11 11:27:17+03:00

139.80
------
 * IDM-9073: не брать лок, а ретраить ошибки (#2239)                                  [ https://github.yandex-team.ru/idm/backend/commit/6741f94ef ]
 * IDM-9061: Не загружать все роли в память (#2238)                                   [ https://github.yandex-team.ru/idm/backend/commit/d69ad7fa1 ]
 * IDM-9075: Не делать джойн с GroupClosure при раскрытии персональных ролей (#2236)  [ https://github.yandex-team.ru/idm/backend/commit/114cf6f9f ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-10 13:13:04+03:00

139.79
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Попробовать `iterator`  [ https://github.yandex-team.ru/idm/backend/commit/7d83276c0 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-07 10:35:28+03:00

139.78
------
 * IDM-8885: Четырёхсотим на дублирующийся unique_id в POST (#2228)  [ https://github.yandex-team.ru/idm/backend/commit/f3adbdc4b ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2020-02-06 15:25:14+03:00

139.77
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9060: Если группе нужен логин, то не надо проверять это для каждой роли (#2233)  [ https://github.yandex-team.ru/idm/backend/commit/82e764e1e ]
 * IDM-8927: Отзывать все активные роли в выключенных системах (#2231)                  [ https://github.yandex-team.ru/idm/backend/commit/450a3a7ab ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-06 12:22:44+03:00

139.76
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9034: обрабатывать - в слаге (#2232)                             [ https://github.yandex-team.ru/idm/backend/commit/8a7c86436 ]
 * CAUTH-1785: каждые полчаса проверять связанные роли в walle (#2229)  [ https://github.yandex-team.ru/idm/backend/commit/5eab69cdd ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-05 15:50:38+03:00

139.75
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9000: нельзя `-` в названии индекса (#2230)  [ https://github.yandex-team.ru/idm/backend/commit/c2e726391 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-02-05 13:12:16+03:00

139.74
------

* [Maksim Tiulin](http://staff/max-tyulin@yandex-team.ru)

 * Построение фильтра для ролей с учетом индексов для fields_data (#2226)  [ https://github.yandex-team.ru/idm/backend/commit/1a40cf6d2 ]
 * Обработка индексов для field_data (IDM-9000) (#2227)                    [ https://github.yandex-team.ru/idm/backend/commit/699ecdabe ]

[MaxTyulin](http://staff/max-tyulin@yandex-team.ru) 2020-02-04 11:44:34+03:00

139.73
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9012: не делать хак на странице открытой для всех системы (#2217)  [ https://github.yandex-team.ru/idm/backend/commit/0c13757 ]
 * IDM-9012: Избавиться от хака с подзапросом (#2203)                     [ https://github.yandex-team.ru/idm/backend/commit/49aba22 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-8882 Единая функция изменения узла (#2220)  [ https://github.yandex-team.ru/idm/backend/commit/1198e2e ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * releasing version 139.61.2  [ https://github.yandex-team.ru/idm/backend/commit/cef975a ]
 * releasing version 139.61.1  [ https://github.yandex-team.ru/idm/backend/commit/17d89c2 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2020-02-03 14:22:11+03:00

139.72
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8861 Правка доли пятисоток (#2225)  [ https://github.yandex-team.ru/idm/backend/commit/4c73e02 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2020-01-31 11:07:50+03:00

139.71
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8861 yqlv1 (#2216)  [ https://github.yandex-team.ru/idm/backend/commit/5f9c045 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2020-01-31 10:49:22+03:00

139.70
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9032: Не запускать таску по пушу членств, если она запускалась менее пяти минут назад (#2224)  [ https://github.yandex-team.ru/idm/backend/commit/fed34ae06 ]
 * IDM-9033: Ускорить ручку получения одной роли (#2221)                                              [ https://github.yandex-team.ru/idm/backend/commit/a54a70477 ]
 * IDM-8978: Сделать графики по пятисоткам в процентах (#2223)                                        [ https://github.yandex-team.ru/idm/backend/commit/c82851aac ]
 * Выбирать id групп отдельно (#2222)                                                                 [ https://github.yandex-team.ru/idm/backend/commit/38a1aa3d2 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-31 10:31:24+03:00

139.69
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9012: не делать хак на странице открытой для всех системы (#2217)  [ https://github.yandex-team.ru/idm/backend/commit/a4ab5bbd8 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-30 10:46:07+03:00

139.68
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9012: Избавиться от хака с подзапросом (#2203)  [ https://github.yandex-team.ru/idm/backend/commit/4738a1a3c ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-29 14:50:38+03:00

139.67
------
 * IDM-8881: случай с несуществующим путём и конфликтующими slug/parent (#2215)  [ https://github.yandex-team.ru/idm/backend/commit/843fe1c1b ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-01-28 17:52:30+03:00

139.66
------

* [Maksim Tiulin](http://staff/max-tyulin@yandex-team.ru)

 * Добавлены поля для фильтров в системе (IDM-8965) (#2214)  [ https://github.yandex-team.ru/idm/backend/commit/2ebcb84e0 ]

[MaxTyulin](http://staff/max-tyulin@yandex-team.ru) 2020-01-28 13:14:08+03:00

139.65
------
 * Revert "IDM-8963: ускорить убивание контейнера (#2212)"  [ https://github.yandex-team.ru/idm/backend/commit/7e0802176 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-24 16:51:38+03:00

139.64
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8776 Поиск блокирующих запросов (#2213)  [ https://github.yandex-team.ru/idm/backend/commit/f7dec71 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2020-01-24 13:48:15+03:00

139.63
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8963: ускорить убивание контейнера (#2212)  [ https://github.yandex-team.ru/idm/backend/commit/622ef7db3 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-24 10:15:28+03:00

139.62
------
 * IDM-8881: Делаем нечестный upsert с использованием get_or_create (#2210)  [ https://github.yandex-team.ru/idm/backend/commit/e017c85ec ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-01-23 20:29:56+03:00

139.61.2
--------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9012: не делать хак на странице открытой для всех системы (#2217)  [ https://github.yandex-team.ru/idm/backend/commit/0c137579e ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-30 10:47:59+03:00

139.61.1
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-9012: Избавиться от хака с подзапросом (#2203)  [ https://github.yandex-team.ru/idm/backend/commit/49aba22c9 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-29 14:59:19+03:00

139.61
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Ручка для webauth (#2211)  [ https://github.yandex-team.ru/idm/backend/commit/85d052348 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-22 12:59:30+03:00

139.60
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8883: Адресация по unique_id (#2209)                              [ https://github.yandex-team.ru/idm/backend/commit/5c1081fde ]


139.59
------

* [Maksim Tiulin](http://staff/max-tyulin@yandex-team.ru)

 * IDM-8913 Доп. проверка на связанные роли при обсуждении (#2208)  [ https://github.yandex-team.ru/idm/backend/commit/c24892efb ]

[MaxTyulin](http://staff/max-tyulin@yandex-team.ru) 2020-01-20 10:57:37+03:00

139.58
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8951 Поменять хосты для пушей в isearch (#2206)  [ https://github.yandex-team.ru/idm/backend/commit/d4729ff ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2020-01-17 16:11:53+03:00

139.57
------
 * IDM-8879: Пишем логи, выгрепываем потребителей (#2204)  [ https://github.yandex-team.ru/idm/backend/commit/5424a7afe ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-01-17 12:53:25+03:00

139.56
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-6596: не писать про отзыв ролей при перемещении (#2205)  [ https://github.yandex-team.ru/idm/backend/commit/b007752b9 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-16 20:13:48+03:00

139.55
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8692: Прокидывать комментарий в роль из воркфлоу (#2201)  [ https://github.yandex-team.ru/idm/backend/commit/b5da70db9 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-16 12:54:03+03:00

139.54
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Разбить core.models на отдельные файлы (#2202)  [ https://github.yandex-team.ru/idm/backend/commit/fc2d11cac ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-15 10:39:01+03:00

139.53
------
 * Повысить трешолд в тестинге  [ https://github.yandex-team.ru/idm/backend/commit/e4b5a5656 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-14 15:13:57+03:00

139.52
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-8575: прокидывание дополнительных флагов для связанных ролей (#2200)  [ https://github.yandex-team.ru/idm/backend/commit/2839a9162 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-13 15:09:12+03:00

139.51
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8911: Получать количество объектов отдельно от списка для всех ручек (#2199)  [ https://github.yandex-team.ru/idm/backend/commit/dda1fddcb ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-13 15:06:48+03:00

139.50
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8853: ускорить пуш членств (#2196)  [ https://github.yandex-team.ru/idm/backend/commit/ab8dce882 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2020-01-13 14:26:37+03:00

139.49
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8910 Разрешаем robot-idm отзывать персональные роли уволенных (#2198)  [ https://github.yandex-team.ru/idm/backend/commit/c965198 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2020-01-13 10:49:27+03:00

139.48
------
 * IDM-8827: сделано переключение версии YQL-синтаксиса  [ https://github.yandex-team.ru/idm/backend/commit/5098af55f ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-01-09 19:25:40+03:00

139.47
------
 * IDM-8827: убраны лишние запятые в yql-командах  [ https://github.yandex-team.ru/idm/backend/commit/97302202f ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-01-09 19:07:10+03:00

139.46
------
 * IDM-8827: добавлены команды по построению графиков выполнения workflow (#2197)  [ https://github.yandex-team.ru/idm/backend/commit/142753f8e ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2020-01-09 18:47:58+03:00

139.45
------
 * IDM-8827: время запуска и убивания контейнера теперь записывается в log_context (#2195)  [ https://github.yandex-team.ru/idm/backend/commit/08c9fb9cf ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-12-26 17:31:21+03:00

139.44
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8864: создавать трансфер только если группы отличаются (#2194)  [ https://github.yandex-team.ru/idm/backend/commit/6a5e9ad55 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-26 14:25:05+03:00

139.43
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Исключить неактивные системы (#2193)  [ https://github.yandex-team.ru/idm/backend/commit/2b304ae19 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-8575: изменена настройка для фронта, сгенерирован файл переводов (#2192)  [ https://github.yandex-team.ru/idm/backend/commit/f9d9659cd ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-12-24 18:21:34+03:00

139.42
------
 * IDM-8575: Роли с мгновенным отзывом персональных (#2190)  [ https://github.yandex-team.ru/idm/backend/commit/513509534 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-12-24 13:58:30+03:00

139.41.1
------
 * IDM-8827: время запуска и убивания контейнера теперь записывается в log_context (#2195) [ https://github.yandex-team.ru/idm/backend/commit/08c9fb9cf ]

[v-sopov](http://staff/v-sopov@yandex-team.ru) 2019-12-26 17:31:21+03:00

139.41
------
 * Не делать заголовок интом  [ https://github.yandex-team.ru/idm/backend/commit/93414c6b0 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-20 11:55:28+03:00

139.40
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8854: Не навешивать сид в тестовой метрике (#2191)  [ https://github.yandex-team.ru/idm/backend/commit/92b23f371 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-19 15:58:27+03:00

139.39
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8739: Пишем request_id в пушах в систему (#2187)                [ https://github.yandex-team.ru/idm/backend/commit/33fd705d2 ]
 * IDM-8828: исключить tvm-приложения из выгрузки для панчера (#2189)  [ https://github.yandex-team.ru/idm/backend/commit/6522ed3e1 ]
 * IDM-8691: выдавать роль после пуша членств (#2186)                  [ https://github.yandex-team.ru/idm/backend/commit/09a651c18 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-18 13:42:01+03:00

139.38
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8689: alert db (#2188)  [ https://github.yandex-team.ru/idm/backend/commit/de62b3f9a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-17 18:17:04+03:00

139.37
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8618: перевыбирать parent после каждого подтверждения (#2182)  [ https://github.yandex-team.ru/idm/backend/commit/6d10465ca ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-16 14:03:10+03:00

139.36
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8767: Передавать unique-id узла при пуше роли в систему (#2184)            [ https://github.yandex-team.ru/idm/backend/commit/b2d15fd0c ]
 * IDM-8833: Попробовать выставить гарантию по цпу контейнеру с воркфлоу (#2185)  [ https://github.yandex-team.ru/idm/backend/commit/4e4c4810b ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * fixed tests                                  [ https://github.yandex-team.ru/idm/backend/commit/f9f4ba4fe ]
 * IDM-8799: Удалить двухфакторную авторизацию  [ https://github.yandex-team.ru/idm/backend/commit/ff991d26e ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-16 13:40:50+03:00

139.35
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8825: Добавить fields при походе в ABC (#2183)  [ https://github.yandex-team.ru/idm/backend/commit/27d802fc0 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-13 12:31:05+03:00

139.34
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8740: писать request_id системы в логи (#2181)  [ https://github.yandex-team.ru/idm/backend/commit/bf641df96 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * less (#2180)  [ https://github.yandex-team.ru/idm/backend/commit/52c05d687 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-12 21:06:54+03:00

139.33
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8631: сразу удалять членства в группах, на которых нет ролей (#2179)  [ https://github.yandex-team.ru/idm/backend/commit/461265ba9 ]
 * IDM-8621: искать активне дубли членств перед удалением (#2178)            [ https://github.yandex-team.ru/idm/backend/commit/f1f423723 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-12 13:35:59+03:00

139.32
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8693: silent в ручках воркфлоу (#2176)          [ https://github.yandex-team.ru/idm/backend/commit/45feebb4a ]
 * IDM-8694: комментарий про отложенный отзыв (#2177)  [ https://github.yandex-team.ru/idm/backend/commit/6786a4a36 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-11 12:21:19+03:00

139.31
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8788: Кешировать объекты в воркфлоу (#2171)  [ https://github.yandex-team.ru/idm/backend/commit/de5a8cbe4 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-09 11:22:13+03:00

139.30
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8783 графики на detail запросы rolenodes со slug_path (#2172)  [ https://github.yandex-team.ru/idm/backend/commit/ea86a76 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-12-06 14:00:28+03:00

139.29
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8762: сделать tvm фактором по умолчанию (#2169)  [ https://github.yandex-team.ru/idm/backend/commit/5f3c1b192 ]
 * IDM-8763: Лишние каунты (#2168)                      [ https://github.yandex-team.ru/idm/backend/commit/c8d5e14ee ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-04 18:25:59+03:00

139.28
------
 * Обработка отсутствия объектов в миграции 0009_add_fields_to_role_and_system_2 (#2170)  [ https://github.yandex-team.ru/idm/backend/commit/4deb2f80d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-12-04 17:23:01+03:00

139.27
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8505: Тесты на использование select_related (#2166)  [ https://github.yandex-team.ru/idm/backend/commit/4b8d65d72 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-12-04 13:59:44+03:00

139.26
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8702: only_meta (#2164)  [ https://github.yandex-team.ru/idm/backend/commit/521fe61e6 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-29 11:22:37+03:00

139.25
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8616 Графики по кодам ответов ручек (#2165)  [ https://github.yandex-team.ru/idm/backend/commit/88a99e3 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-11-28 09:50:06+03:00

139.24
------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-8577 Писать меньше mass_action (#2160)  [ https://github.yandex-team.ru/idm/backend/commit/bbe991409 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-8522: Циклы при выдаче связанных ролей (#2159)  [ https://github.yandex-team.ru/idm/backend/commit/5d94dfa35 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-11-27 23:15:22+03:00

139.23
------
 * IDM-8698 Ускорить работу команды (#2163)  [ https://github.yandex-team.ru/idm/backend/commit/bffe434b4 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-26 18:38:42+03:00

139.22
------
 * IDM-8698 Обновлять департаментную группу при увольнении/найме (#2162)  [ https://github.yandex-team.ru/idm/backend/commit/a7555493d ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-26 17:00:05+03:00

139.21
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8688: Не делать лишний каунт (#2158)  [ https://github.yandex-team.ru/idm/backend/commit/e1640e146 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-25 21:09:05+03:00

139.20
------
 * IDM-8551 Создавать столбцы в миграции в другом порядке (#2157)  [ https://github.yandex-team.ru/idm/backend/commit/ebd10f040 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-25 19:25:23+03:00

139.19
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Починил тест (#2156)  [ https://github.yandex-team.ru/idm/backend/commit/1027291c2 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8551 Роли зависают в статусе "Отзывается" (#2154)  [ https://github.yandex-team.ru/idm/backend/commit/7bddb2806 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-25 17:24:29+03:00

139.18.2
--------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8688: Не делать лишний каунт (#2158)  [ https://github.yandex-team.ru/idm/backend/commit/59c08f5d8 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-26 13:03:12+03:00

139.18.1
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Починил тест (#2156)                                                  [ https://github.yandex-team.ru/idm/backend/commit/6efbe0db5 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-25 17:28:39+03:00

139.18
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Не использовать подзапрос в ручке для роботов (#2155)  [ https://github.yandex-team.ru/idm/backend/commit/5351162c1 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-25 16:32:56+03:00

139.17
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8680: ускорять проверку прав  только при просмотре ролей (#2152)  [ https://github.yandex-team.ru/idm/backend/commit/128ccf5f9 ]
 * Limits (#2153)                                                        [ https://github.yandex-team.ru/idm/backend/commit/41cfdca04 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-8507: обрабатывать multi-status результат пуша батча (#2145)  [ https://github.yandex-team.ru/idm/backend/commit/d284d2f4a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-25 11:54:33+03:00

139.16
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8376 Приоритет активной ноды в синке ролей (#2135)  [ https://github.yandex-team.ru/idm/backend/commit/2b398f8 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-11-22 18:13:19+03:00

139.15
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8563 Важная доработка YQL запроса (#2151)  [ https://github.yandex-team.ru/idm/backend/commit/4b65d8c ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-11-22 17:45:55+03:00

139.14
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8563 2xx_responses_count - невалидное имя поля в statface (#2150)  [ https://github.yandex-team.ru/idm/backend/commit/ad36aca ]
 * IDM-8563 Добавляем подсчет походов отчет по временам ответов (#2148)   [ https://github.yandex-team.ru/idm/backend/commit/d212c08 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-11-22 16:24:05+03:00

139.13.1
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8680: ускорять проверку прав  только при просмотре ролей (#2152)  [ https://github.yandex-team.ru/idm/backend/commit/2357f6a42 ]
 * Limits (#2153)                                                        [ https://github.yandex-team.ru/idm/backend/commit/0d6c4d408 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-25 14:20:05+03:00

139.13
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Магия с лимитами (#2146)  [ https://github.yandex-team.ru/idm/backend/commit/813377776 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-22 14:00:45+03:00

139.12
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8672: Не пытаться отзывать роли в выключенных и сломанных системах (#2149)  [ https://github.yandex-team.ru/idm/backend/commit/9abc74cbf ]
 * ujson (#2147)                                                                   [ https://github.yandex-team.ru/idm/backend/commit/528eb57ad ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-22 13:50:59+03:00

139.11
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Фильтровать nodeclosure по системе (#2144)  [ https://github.yandex-team.ru/idm/backend/commit/1ae00a8ad ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-21 19:19:40+03:00

139.10
------
 * IDM-8656 Обновление департаментной группы в транзакции (#2143)  [ https://github.yandex-team.ru/idm/backend/commit/368d0c480 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-21 18:32:58+03:00

139.9
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Ускорить attributes (#2142)  [ https://github.yandex-team.ru/idm/backend/commit/10e2fd30a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-21 15:58:12+03:00

139.8
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8660: отзывать временные роли (#2140)  [ https://github.yandex-team.ru/idm/backend/commit/71c648532 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-21 15:28:21+03:00

139.7
-----
 * IDM-8656 add_members() только для пользователей (#2141)  [ https://github.yandex-team.ru/idm/backend/commit/7a597efd1 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-21 15:22:09+03:00

139.6
-----
 * IDM-8402 Отзыв роли из подтвержденного статуса (#2132)  [ https://github.yandex-team.ru/idm/backend/commit/b1f3f03 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-11-20 17:46:01+03:00

139.5
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8520: поправить формат логирования (#2137)            [ https://github.yandex-team.ru/idm/backend/commit/d0ed78341 ]
 * Отдавать в members только активных пользователей (#2136)  [ https://github.yandex-team.ru/idm/backend/commit/936111b10 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-20 15:19:58+03:00

139.4
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8644: определять язык заранее (#2138)  [ https://github.yandex-team.ru/idm/backend/commit/b5f7fe1d4 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-20 13:26:51+03:00

139.3
-----
 * IDM-8562 Посистемные графики по логам приложения на время ответа ручек (#2130)  [ https://github.yandex-team.ru/idm/backend/commit/2ba744f13 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-20 12:55:51+03:00

139.2
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8644: Меньше раз сериализовать систему (#2134)  [ https://github.yandex-team.ru/idm/backend/commit/62bfd6c7e ]
 * Делать сплит один раз (#2133)                       [ https://github.yandex-team.ru/idm/backend/commit/68ab22983 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-8627: Добавить plugin_type в список секретных полей  [ https://github.yandex-team.ru/idm/backend/commit/d21894198 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-20 12:45:29+03:00

139.1
-----
 * IDM-8423 Fix мониторингов заблокированных в AD пользователей (#2131)  [ https://github.yandex-team.ru/idm/backend/commit/a952239 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-11-19 17:09:06+03:00

139.0
-------
 * IDM-8580: Экспортируем в unistat время выполнения периодических задач (#2119)  [ https://github.yandex-team.ru/idm/backend/commit/0f17016d0 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-11-19 16:52:48+03:00

138.253
-------
 * IDM-8538: Добавить графики по времени ответа для ручек с айдишником (#2127)  [ https://github.yandex-team.ru/idm/backend/commit/202d2cf39 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-11-19 15:59:30+03:00

138.252
-------
 * IDM-8423-2 настройки LDAP для тестинга (#2129)  [ https://github.yandex-team.ru/idm/backend/commit/a13a464 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-11-19 15:07:18+03:00

138.251
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8409: наследовать команды от IdmBaseCommand (#2117)  [ https://github.yandex-team.ru/idm/backend/commit/e1103bae0 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-19 13:00:10+03:00

138.250
-------
 * IDM-8260 Баг в саджесте по пользователям (#2120)  [ https://github.yandex-team.ru/idm/backend/commit/aee1298 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-11-19 11:49:51+03:00

138.249
-------
 * IDM-8561 Добавить название системы в логи POST в /role/<id> /rolerequests (#2123)  [ https://github.yandex-team.ru/idm/backend/commit/409ebbfce ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-18 17:30:19+03:00

138.248
-------
 * IDM-8423 CASE END (#2122)  [ https://github.yandex-team.ru/idm/backend/commit/c5e8aa5 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-11-18 12:31:53+03:00

138.247
-------
 * releasing version 138.246  [ https://github.yandex-team.ru/idm/backend/commit/c06516b3c ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-18 12:22:16+03:00

138.246
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8620: groupby может вернуть две копии (#2121)  [ https://github.yandex-team.ru/idm/backend/commit/cb2766299 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-18 12:22:08+03:00

138.245
-------
 * IDM-8423 Мониторинг на блокировку в AD (#2118)  [ https://github.yandex-team.ru/idm/backend/commit/f351cb5 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-11-18 11:53:56+03:00

138.244
-------
 * IDM-8417 Перенести синк департаментных групп в синк людей (#2116)  [ https://github.yandex-team.ru/idm/backend/commit/34254aa15 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-15 16:40:12+03:00

138.243
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8592: убрать дубликаты ролей (#2115)  [ https://github.yandex-team.ru/idm/backend/commit/4ed73074c ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-13 10:54:35+03:00

138.242.2
---------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8520: поправить формат логирования (#2137)            [ https://github.yandex-team.ru/idm/backend/commit/f5451d1d8 ]
 * Отдавать в members только активных пользователей (#2136)  [ https://github.yandex-team.ru/idm/backend/commit/7cd9a2dba ]
 * IDM-8644: определять язык заранее (#2138)                 [ https://github.yandex-team.ru/idm/backend/commit/d4c526876 ]
 * IDM-8644: Меньше раз сериализовать систему (#2134)        [ https://github.yandex-team.ru/idm/backend/commit/c560fac36 ]
 * Делать сплит один раз (#2133)                             [ https://github.yandex-team.ru/idm/backend/commit/59b492764 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-20 15:24:04+03:00

138.242.1
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8620: groupby может вернуть две копии (#2121)  [ https://github.yandex-team.ru/idm/backend/commit/bc6072dfe ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-19 15:52:23+03:00

138.242
-------
 * IDM-8579: добавлен чёрный список систем, для которых проверка workflow на уволенных не выполняется (#2114)  [ https://github.yandex-team.ru/idm/backend/commit/939d747ad ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-11-12 14:09:26+03:00

138.241
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8422: мониторинг активных ролей на неактивные группы (#2110)  [ https://github.yandex-team.ru/idm/backend/commit/c6c7763a9 ]
 * IDM-8419: мониторинг на превышение лимита уволенных (#2109)       [ https://github.yandex-team.ru/idm/backend/commit/e4763117a ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8324 Фикс импорта метрики (#2112)                    [ https://github.yandex-team.ru/idm/backend/commit/124ec8c07 ]
 * IDM-8324 Выполнять таски в отдельной компоненте (#2111)  [ https://github.yandex-team.ru/idm/backend/commit/9e5fa454a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-11-12 11:49:08+03:00

138.240
-------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8324 Метрика времеми выдачи и количества выдаваемых ролей (#2108)  [ https://github.yandex-team.ru/idm/backend/commit/11f8b78a6 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-11 13:21:56+03:00

138.239
-------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8413 Разные статусы мониторинга hanging-*-roles от времени зависания (#2104)  [ https://github.yandex-team.ru/idm/backend/commit/e4ce1a9 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-11-08 12:12:58+03:00

138.238
-------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-8421: Мониторинги на размер очередей через unistat (#2105)  [ https://github.yandex-team.ru/idm/backend/commit/36846c120 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-8527 Вернула проверку в deprive_or_decline (для b2b) (#2107)  [ https://github.yandex-team.ru/idm/backend/commit/ddf4c0fe6 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-11-08 11:48:32+03:00

138.237
-------
 * IDM-8527 500->400 при отзыве роли в сломанной или выключенной системе (#2102)  [ https://github.yandex-team.ru/idm/backend/commit/d7aec5b ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-11-06 18:02:23+03:00

138.236
-------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8470 Ошибка с org_id в batch ручке (#2103)  [ https://github.yandex-team.ru/idm/backend/commit/433ed56 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-11-06 17:28:02+03:00

138.235
-------
 * IDM-8473 Фикс мониторинга (#2101)  [ https://github.yandex-team.ru/idm/backend/commit/36136fc53 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-01 17:00:10+03:00

138.234
-------
 * IDM-8473 Отложено отзывать связанную групповую роль (#2100)  [ https://github.yandex-team.ru/idm/backend/commit/c7f629352 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-11-01 12:37:17+03:00

138.233
-------
 * IDM-8497 Использовать поля из prefetch_related (#2098)  [ https://github.yandex-team.ru/idm/backend/commit/65a761ff0 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-31 18:42:48+03:00

138.232
-------
 * IDM-8473 Отзывать связанные роли, если родительская активна (#2099)  [ https://github.yandex-team.ru/idm/backend/commit/8ef0749c5 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-31 14:49:49+03:00

138.231
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8403: создавать юзера при запросе роли для него (#2093)  [ https://github.yandex-team.ru/idm/backend/commit/ee659356c ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-31 12:07:16+03:00

138.230
-------
 * IDM-8377 Отзывать роли при выключении системы (#2092)  [ https://github.yandex-team.ru/idm/backend/commit/8b9f47e47 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-30 11:21:56+03:00

138.229
-------
 * IDM-8321 Улучшить логирование тасок (#2094)  [ https://github.yandex-team.ru/idm/backend/commit/328e149 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-10-29 18:08:33+03:00

138.228
-------

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-29 10:35:45+03:00

138.227
-------
 * IDM-8473 Уменьшение лимитов на отзыв ролей в тестинге (#2097)  [ https://github.yandex-team.ru/idm/backend/commit/abd975b17 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-29 10:26:06+03:00

138.226
-------
 * IDM-8459: Ещё один фикс метрики  [ https://github.yandex-team.ru/idm/backend/commit/86b5a5648 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2019-10-28 20:57:04+03:00

138.225
-------
 * IDM-8473 Отзывать роли уволенных сразу (#2095)  [ https://github.yandex-team.ru/idm/backend/commit/3166433df ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-28 19:38:17+03:00

138.222
-------

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-8256: Правлю 5-минутные графики         [ https://github.yandex-team.ru/idm/backend/commit/34f0d0a77 ]
 * IDM-8459: И ещё раз правлю метрику (#2091)  [ https://github.yandex-team.ru/idm/backend/commit/9a629ea21 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * releasing version 138.215.2                      [ https://github.yandex-team.ru/idm/backend/commit/a22c2c01a ]
 * releasing version 138.215.1                      [ https://github.yandex-team.ru/idm/backend/commit/855bbec19 ]
 * Revert "Revert "IDM-8380: вернул фичу (#2078)""  [ https://github.yandex-team.ru/idm/backend/commit/aefac4c76 ]
 * releasing version 138.86.1                       [ https://github.yandex-team.ru/idm/backend/commit/388b416ea ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Делать values_list после unwrap (#2085)          [ https://github.yandex-team.ru/idm/backend/commit/295926d0d ]
 * IDM-8023: сериализация ошибок (#1940)            [ https://github.yandex-team.ru/idm/backend/commit/6b226b2bf ]
 * IDM-4919: глобальные функции (#1937)             [ https://github.yandex-team.ru/idm/backend/commit/60eb673af ]
 * IDM-7982: не десериализовать лишнее (#1938)      [ https://github.yandex-team.ru/idm/backend/commit/744cf05b8 ]
 * IDM-7982: initial_properties в воркфлоу (#1936)  [ https://github.yandex-team.ru/idm/backend/commit/7b4fb8f2a ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * releasing version 138.144.5                                          [ https://github.yandex-team.ru/idm/backend/commit/f28aced36 ]
 * IDM-8244 Поменять порядок параметров в сигнатуре has_role() (#2016)  [ https://github.yandex-team.ru/idm/backend/commit/54fc20ba5 ]
 * releasing version 138.144.4                                          [ https://github.yandex-team.ru/idm/backend/commit/6b9467da6 ]
 * IDM-8200 Отдавать только id роли, если передать no_meta (#2013)      [ https://github.yandex-team.ru/idm/backend/commit/13ea0e7c0 ]
 * releasing version 138.144.3                                          [ https://github.yandex-team.ru/idm/backend/commit/abd0a525c ]
 * IDM-8229 has_role() Принимает pk узла (#2011)                        [ https://github.yandex-team.ru/idm/backend/commit/34e333fd8 ]
 * releasing version 138.144.2                                          [ https://github.yandex-team.ru/idm/backend/commit/5110ef956 ]
 * IDM-7531 Партнерский интерфейс в исключениях для sid67 (#2007)       [ https://github.yandex-team.ru/idm/backend/commit/e35ac4e6d ]
 * releasing version 138.144.1                                          [ https://github.yandex-team.ru/idm/backend/commit/d872264e1 ]
 * IDM-8222 Сортировать сервисы в саджесте по длине имени (#2004)       [ https://github.yandex-team.ru/idm/backend/commit/d9c463a56 ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * releasing version 138.120.1  [ https://github.yandex-team.ru/idm/backend/commit/6aa1ef4e2 ]

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8111 user_groups в разрешении расхождений (#1968)  [ https://github.yandex-team.ru/idm/backend/commit/2d99ed946 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2019-10-28 16:22:12+03:00

138.221
-------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * COMPUTERPROBLEM-294 код для мониторингов 400 (#2087)  [ https://github.yandex-team.ru/idm/backend/commit/ac740f2af ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-25 18:45:41+03:00

138.220
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Убрать лишние команды (#2089)  [ https://github.yandex-team.ru/idm/backend/commit/d7f3ad095 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-8459: Поправил метрику (#2086)  [ https://github.yandex-team.ru/idm/backend/commit/5f7332c23 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-25 18:09:32+03:00

138.219
-------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8465 Отзывать роли в отдельной очереди и отдельной компоненте (#2088)  [ https://github.yandex-team.ru/idm/backend/commit/dbc7f600c ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * Revert "IDM-8361: ретраить DoesNotExists побольше (#2073)"  [ https://github.yandex-team.ru/idm/backend/commit/2f80e7eeb ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-25 17:55:00+03:00

138.218
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Делать values_list после unwrap (#2085)  [ https://github.yandex-team.ru/idm/backend/commit/0dd2f5fa9 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * Revert "Revert "IDM-8380: вернул фичу (#2078)""  [ https://github.yandex-team.ru/idm/backend/commit/d12fa207d ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-25 11:07:59+03:00

138.217
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8361: ретраить DoesNotExists побольше (#2073)  [ https://github.yandex-team.ru/idm/backend/commit/db7af452c ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-8414: Избавиться от токена Директа (#2079)  [ https://github.yandex-team.ru/idm/backend/commit/2d93de780 ]
 * What about that metric? (#2075)                 [ https://github.yandex-team.ru/idm/backend/commit/255336c86 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-24 11:31:40+03:00

138.216
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * COMPUTERPROBLEM-292: ускорение (#2084)  [ https://github.yandex-team.ru/idm/backend/commit/cf436ced8 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-23 18:22:26+03:00

138.215.2
---------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Делать values_list после unwrap (#2085)  [ https://github.yandex-team.ru/idm/backend/commit/295926d0d ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-24 19:24:12+03:00

138.215.1
-------
 * Revert "Revert "IDM-8380: вернул фичу (#2078)""  [ https://github.yandex-team.ru/idm/backend/commit/aefac4c76 ]

138.215
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * COMPUTERPROBLEM-292: сбросить expire_at (#2083)  [ https://github.yandex-team.ru/idm/backend/commit/e6e8d7989 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * Revert "IDM-8380: вернул фичу (#2078)"  [ https://github.yandex-team.ru/idm/backend/commit/f441bb031 ]
 * Revert "Удалить лишнее (#2080)"         [ https://github.yandex-team.ru/idm/backend/commit/b3dce3f6c ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-23 15:32:08+03:00

138.214
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * COMPUTERPROBLEM-292: вернуть фильтр по системе (#2082)  [ https://github.yandex-team.ru/idm/backend/commit/fac0d6449 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-23 15:03:37+03:00

138.213
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Удалить лишнее (#2080)         [ https://github.yandex-team.ru/idm/backend/commit/f8c4b9799 ]
 * IDM-8380: вернул фичу (#2078)  [ https://github.yandex-team.ru/idm/backend/commit/68380b67a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-22 18:25:45+03:00

138.212
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8380: временно выключил (#2077)  [ https://github.yandex-team.ru/idm/backend/commit/02d0879e2 ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * FIRE-32480 Не матчились ad группы с игнорлистом  [ https://github.yandex-team.ru/idm/backend/commit/e39d61822 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-22 11:10:29+03:00

138.211
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * fix sync_with_gaps (#2076)  [ https://github.yandex-team.ru/idm/backend/commit/4023d6bbe ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * releasing version 138.210  [ https://github.yandex-team.ru/idm/backend/commit/26391792d ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-22 10:12:38+03:00

138.210
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8007: Запретить пересмотры ролей для TVM-приложений (#2063)  [ https://github.yandex-team.ru/idm/backend/commit/dfdd44709 ]
 * kwargs (#2071)                                                   [ https://github.yandex-team.ru/idm/backend/commit/0bc577bc9 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7985 Мониторинги теперь отвечают 412 вместо 500 (#2072)  [ https://github.yandex-team.ru/idm/backend/commit/97ba5609e ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-21 17:45:32+03:00

138.209
-------
 * IDM-8256 Фикс 5-минутных графиков (#2070)  [ https://github.yandex-team.ru/idm/backend/commit/4a88ab38f ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-21 12:32:03+03:00

138.208
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8398: Не использовать count_estimate на странице пользователя (#2069)  [ https://github.yandex-team.ru/idm/backend/commit/30454e68c ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-19 13:57:31+03:00

138.207
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8380: еще поля (#2068)  [ https://github.yandex-team.ru/idm/backend/commit/7bfa53e38 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-18 17:56:58+03:00

138.206
-------
 * IDM-8372: Членства уволенных в статусе onhold (#2065)  [ https://github.yandex-team.ru/idm/backend/commit/35cfd6f98 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-10-18 17:45:22+03:00

138.205
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8380: Ускорение сериализации в ручке ролей (#2062)  [ https://github.yandex-team.ru/idm/backend/commit/046877f07 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-18 14:53:11+03:00

138.204
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Unwrap nodes (#2066)  [ https://github.yandex-team.ru/idm/backend/commit/b4c1f4f01 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-8389 Добавить логи в add_role_async (#2067)  [ https://github.yandex-team.ru/idm/backend/commit/b44c75676 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-18 13:18:48+03:00

138.203
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8359: не учитывать членства во вложенных группах при выдаче ролей (#2061)  [ https://github.yandex-team.ru/idm/backend/commit/306e52755 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8373 Поправить ручку batch в b2b (#2064)  [ https://github.yandex-team.ru/idm/backend/commit/af9f5e8b5 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-16 17:09:25+03:00

138.202
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8354: еще одно место с parent (#2060)  [ https://github.yandex-team.ru/idm/backend/commit/7c6c64564 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-15 14:05:32+03:00

138.201
-------
 * IDM-8261: fix (#2059)  [ https://github.yandex-team.ru/idm/backend/commit/c9d9806aa ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-10-15 12:59:26+03:00

138.200
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8082: правильный параметр (#2058)  [ https://github.yandex-team.ru/idm/backend/commit/bda74e994 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-15 12:32:19+03:00

138.199
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8354: Убрать из API role.parent.parent (#2057)  [ https://github.yandex-team.ru/idm/backend/commit/661eec2eb ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-15 11:08:07+03:00

138.198
-------
 * IDM-8256 Считать статистику по времени ответа ручек в api (#2056)  [ https://github.yandex-team.ru/idm/backend/commit/2358a50e5 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-15 10:55:53+03:00

138.197
-------
 * IDM-8236 Мониторинг отзывающих, превысивших threshold на отзыв (#2052)  [ https://github.yandex-team.ru/idm/backend/commit/7c1a4f5a4 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-15 10:43:14+03:00

138.196
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Пришло время раскомментировать (#2053)  [ https://github.yandex-team.ru/idm/backend/commit/2acb5a495 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-14 18:21:14+03:00

138.195
-------
 * IDM-8341 Не учитывать новых сотрудников в мониторинге (#2050)  [ https://github.yandex-team.ru/idm/backend/commit/ddebf0279 ]
 * IDM-8082 Фикс миграции (#2055)                                 [ https://github.yandex-team.ru/idm/backend/commit/ef50e73a0 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-14 16:59:44+03:00

138.194
-------
 * IDM-8082 Ограничить количество одновременно отзываемых ролей (#2042)  [ https://github.yandex-team.ru/idm/backend/commit/067e00c11 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-14 16:18:46+03:00

138.193
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8237: возможность остановить отзыв ролей (#2029)  [ https://github.yandex-team.ru/idm/backend/commit/898158bcc ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-11 18:34:50+03:00

138.192
-------
 * IDM-8135 Фильтровать matching role по action_id (#2041)  [ https://github.yandex-team.ru/idm/backend/commit/75e0631 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-10-11 16:31:10+03:00

138.191
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8261: properties (#2051)  [ https://github.yandex-team.ru/idm/backend/commit/b2aae0462 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-11 12:46:28+03:00

138.190
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8339: Удалить resource_uri из апи (#2047)  [ https://github.yandex-team.ru/idm/backend/commit/da2cdcb38 ]
 * Правка пермишенов (#2049)                      [ https://github.yandex-team.ru/idm/backend/commit/10de8d0e0 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-8261: Не выдаются связанные роли в системе Y.Browser Bitbucket (#2048)  [ https://github.yandex-team.ru/idm/backend/commit/97bf4cfac ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-11 10:31:33+03:00

138.189
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Убрать uri за флаг (#2046)  [ https://github.yandex-team.ru/idm/backend/commit/62080be7f ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-10 18:34:22+03:00

138.188
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8332: Не проверять права на роль, если пришли из запроса (#2045)  [ https://github.yandex-team.ru/idm/backend/commit/60c11d9c2 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-10 15:52:51+03:00

138.187
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8302: ускорить ручку систем (#2031)  [ https://github.yandex-team.ru/idm/backend/commit/e4f24da9e ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-10 15:35:33+03:00

138.186
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8325: еще немного взаимодействия с AD (#2044)  [ https://github.yandex-team.ru/idm/backend/commit/82c51870f ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-10 15:08:43+03:00

138.185
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8325: починить взаимодействие с AD (#2043)  [ https://github.yandex-team.ru/idm/backend/commit/4aa10398d ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-10 10:50:07+03:00

138.184
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8280: print (#2039)                                                         [ https://github.yandex-team.ru/idm/backend/commit/ac97270d8 ]
 * IDM-8315: Отселить выдачу и ретраи выдачи ролей в отдельные компоненты (#2040)  [ https://github.yandex-team.ru/idm/backend/commit/ba818f05c ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-09 13:34:03+03:00

138.183
-------
 * IDM-8307: импорт  [ https://github.yandex-team.ru/idm/backend/commit/2a13403cd ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-08 13:58:21+03:00

138.182
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8307: График количества зависающих ролей (#2037)  [ https://github.yandex-team.ru/idm/backend/commit/4ccb88292 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8283 Отдавать в b2b is_synced_with_staff=True в ручке /users/ (#2038)  [ https://github.yandex-team.ru/idm/backend/commit/5ddc23592 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-08 13:51:49+03:00

138.181
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8280: больше нет e.message (#2035)  [ https://github.yandex-team.ru/idm/backend/commit/6b25aaac9 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8283 Доработки для фронта в b2b (#2030)  [ https://github.yandex-team.ru/idm/backend/commit/67b567c28 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-10-08 10:39:59+03:00

138.180
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8280: админка (#2034)  [ https://github.yandex-team.ru/idm/backend/commit/94fb648da ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-07 18:57:14+03:00

138.179
-------
 * IDM-8280-11: static  [ https://github.yandex-team.ru/idm/backend/commit/d7a26e036 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-07 18:00:08+03:00

138.178
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8280: fix celery (#2033)  [ https://github.yandex-team.ru/idm/backend/commit/b0853829d ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8280 yql upgrade (#2032)  [ https://github.yandex-team.ru/idm/backend/commit/7bf09c6bd ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-07 17:17:17+03:00

138.177
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8280: force_bytes <-> force_text (#2028)  [ https://github.yandex-team.ru/idm/backend/commit/19debbc54 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8256 Статистика по времени ответа ручек (#2026)  [ https://github.yandex-team.ru/idm/backend/commit/663135c91 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-04 14:29:29+03:00

138.176
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8280: фиксы (#2027)  [ https://github.yandex-team.ru/idm/backend/commit/7beee3409 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-04 10:12:24+03:00

138.175
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8280: переезд на python3 (#1889)  [ https://github.yandex-team.ru/idm/backend/commit/244b309ad ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-03 21:47:17+03:00

138.174
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8257: меньше проверок в ручкх ролей и запросов (#2025)  [ https://github.yandex-team.ru/idm/backend/commit/64b838afa ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-03 18:21:11+03:00

138.173
-------
 * Revert "Revert "Revert "IDM-8177: При ошибках разрешать неконсистентость в пользу системы, если роль в нужном статусе (#1997)"""  [ https://github.yandex-team.ru/idm/backend/commit/2eb3a2732 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-03 16:37:35+03:00

138.172
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7964: Бесконечные ретраи при ошибках добавления/удаления роли (#2023)  [ https://github.yandex-team.ru/idm/backend/commit/20c770cc9 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-10-02 13:55:12+03:00

138.171
-------
 * Revert "Revert "IDM-7964: Бесконечные ретраи при ошибках добавления/удаления роли (#1996)""                              [ https://github.yandex-team.ru/idm/backend/commit/3c4137244 ]
 * Revert "Revert "IDM-8177: При ошибках разрешать неконсистентость в пользу системы, если роль в нужном статусе (#1997)""  [ https://github.yandex-team.ru/idm/backend/commit/3fe4b5096 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-02 11:08:49+03:00

138.170
-------
 * IDM-8130 поправлен ответ ручки add_role (#2022)  [ https://github.yandex-team.ru/idm/backend/commit/e542053 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-10-01 18:13:14+03:00

138.169
-------
 * IDM-8130 поправлен ответ ручки get_all_roles (#2021)  [ https://github.yandex-team.ru/idm/backend/commit/4888967 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-10-01 15:17:39+03:00

138.168
-------

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-01 12:13:22+03:00

138.167
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-8177: При ошибках разрешать неконсистентость в пользу системы, если роль в нужном статусе (#1997)  [ https://github.yandex-team.ru/idm/backend/commit/6951e9509 ]
 * Поправил опечатку (#2020)                                                                              [ https://github.yandex-team.ru/idm/backend/commit/b20cac615 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * Revert "IDM-8177: При ошибках разрешать неконсистентость в пользу системы, если роль в нужном статусе (#1997)"  [ https://github.yandex-team.ru/idm/backend/commit/5075a2965 ]
 * Revert "IDM-7964: Бесконечные ретраи при ошибках добавления/удаления роли (#1996)"                              [ https://github.yandex-team.ru/idm/backend/commit/121b9f524 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-10-01 12:12:57+03:00

138.166
-------
 * IDM-8130 mimino passport для тестинга (#2019)  [ https://github.yandex-team.ru/idm/backend/commit/84ac541 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-09-30 15:03:53+03:00

138.165
-------
 * IDM-8243 в SyncGroupMembershipSystemRelations пушить в систему JSON правильного вида (#2018)  [ https://github.yandex-team.ru/idm/backend/commit/77dc7ae99 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-30 14:38:56+03:00

138.164
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7964: Бесконечные ретраи при ошибках добавления/удаления роли (#1996)  [ https://github.yandex-team.ru/idm/backend/commit/f21f9b8a6 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-30 13:45:36+03:00

138.163
-------
 * IDM-8130 mimini bb для тестинга (#2017)  [ https://github.yandex-team.ru/idm/backend/commit/c136a8c ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-09-30 13:25:05+03:00

138.162
-------
 * IDM-8244 Поменять порядок параметров в сигнатуре has_role() (#2016)  [ https://github.yandex-team.ru/idm/backend/commit/406025083 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-30 12:25:14+03:00

138.161
-------
 * IDM-8130 новые IDM_FRONTEND_TVM_ID (#2015)  [ https://github.yandex-team.ru/idm/backend/commit/b0e4364 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-09-27 17:56:52+03:00

138.160
-------
 * IDM-8130 passport_login -> passport-login (#2014)  [ https://github.yandex-team.ru/idm/backend/commit/46c2040 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-09-27 15:51:18+03:00

138.159
-------
 * IDM-8130 Доработки для django_idm_api (#2012)  [ https://github.yandex-team.ru/idm/backend/commit/7ab6974 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-09-27 14:27:16+03:00

138.158
-------
 * IDM-8200 Отдавать только id роли, если передать no_meta (#2013)  [ https://github.yandex-team.ru/idm/backend/commit/a00153d75 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-27 14:08:09+03:00

138.157
-------

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-27 12:33:43+03:00

138.156
-------
 * IDM-8130 В дерево узлов добавлено поле passportlogin (#2009)  [ https://github.yandex-team.ru/idm/backend/commit/c4a4ea6 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-09-27 10:27:48+03:00

138.155
-------

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-09-27 10:19:37+03:00

138.154
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-5101: рефакторинг (#2008)  [ https://github.yandex-team.ru/idm/backend/commit/00cb15177 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-26 22:23:16+03:00

138.153
-------
 * IDM-8229 has_role() Принимает pk узла (#2011)  [ https://github.yandex-team.ru/idm/backend/commit/1de0a496f ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-26 21:46:11+03:00

138.152
-------
 * IDM-8229 has_role() умеет принимать RoleNode (#2010)  [ https://github.yandex-team.ru/idm/backend/commit/ee96df00b ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-26 20:16:19+03:00

138.151
-------
 * IDM-7531 Партнерский интерфейс в исключениях для sid67 (#2007)  [ https://github.yandex-team.ru/idm/backend/commit/42df3879a ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-26 17:36:16+03:00

138.150
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-5101: cron (#2006)  [ https://github.yandex-team.ru/idm/backend/commit/fa03d5883 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8222 Remove ipdb (#2005)                                                   [ https://github.yandex-team.ru/idm/backend/commit/85723f747 ]
 * IDM-8209 Формировать правила firewall для aware_of_memberships систем (#2001)  [ https://github.yandex-team.ru/idm/backend/commit/de6205b60 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-8130 Пустить наш фронт в IDM в b2b (#2002)  [ https://github.yandex-team.ru/idm/backend/commit/980633bb4 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-26 15:38:06+03:00

138.149
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8083: перенес метод в QuerySet (#2003)  [ https://github.yandex-team.ru/idm/backend/commit/efe23e800 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-26 14:12:03+03:00

138.148
-------
 * IDM-8222 Сортировать сервисы в саджесте по длине имени (#2004)  [ https://github.yandex-team.ru/idm/backend/commit/6ab5eb1ed ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-26 14:02:12+03:00

138.147
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8207: выключить сеть в воркфлоу (#1999)  [ https://github.yandex-team.ru/idm/backend/commit/788ef9fa4 ]
 * IDM-7487: bigint (#1998)                     [ https://github.yandex-team.ru/idm/backend/commit/a2855498e ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-23 22:59:30+03:00

138.146
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-8084: Массовые действия для deprive_or_decline (#1993)  [ https://github.yandex-team.ru/idm/backend/commit/d576d84ed ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-23 16:02:44+03:00

138.145
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8083: Научиться быстро перевыдавать роли (#1990)       [ https://github.yandex-team.ru/idm/backend/commit/6aea0d14e ]
 * IDM-5101: Уведомления о протухании временной роли (#1994)  [ https://github.yandex-team.ru/idm/backend/commit/6e2014e49 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-23 13:25:58+03:00

138.144.5
---------
 * IDM-8244 Поменять порядок параметров в сигнатуре has_role() (#2016)  [ https://github.yandex-team.ru/idm/backend/commit/54fc20ba5 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-30 12:34:27+03:00

138.144.4
---------
 * IDM-8200 Отдавать только id роли, если передать no_meta (#2013)  [ https://github.yandex-team.ru/idm/backend/commit/13ea0e7c0 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-27 17:55:23+03:00

138.144.3
---------
 * IDM-8229 has_role() Принимает pk узла (#2011)  [ https://github.yandex-team.ru/idm/backend/commit/34e333fd8 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-26 22:01:22+03:00

138.144.2
---------
 * IDM-7531 Партнерский интерфейс в исключениях для sid67 (#2007)  [ https://github.yandex-team.ru/idm/backend/commit/e35ac4e6d ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-26 20:27:12+03:00

138.144.1
-------
* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8222 Сортировать сервисы в саджесте по длине имени (#2004)  [ https://github.yandex-team.ru/idm/backend/commit/d9c463a56 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-26 14:32:18+03:00

138.144
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7487: тесты (#1992)  [ https://github.yandex-team.ru/idm/backend/commit/c3961a9 ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7807 Отлавливаем SyntaxError и еще  [ https://github.yandex-team.ru/idm/backend/commit/edc3686 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-09-19 14:59:23+03:00

138.143
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8180: ускорение ручки юзеров (#1989)  [ https://github.yandex-team.ru/idm/backend/commit/06a3dd34f ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-19 12:08:08+03:00

138.142
-------
 * IDM-7487: int  [ https://github.yandex-team.ru/idm/backend/commit/208c4f743 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-18 23:22:32+03:00

138.141
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7487: принимать tvm-тикеты (#1986)  [ https://github.yandex-team.ru/idm/backend/commit/0a86b53d6 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-7567: Триггеры для новых полей (#1983)  [ https://github.yandex-team.ru/idm/backend/commit/7df9f4a20 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-18 19:58:40+03:00

138.140
-------
 * IDM-8172 Правка ручки systems (#1988)  [ https://github.yandex-team.ru/idm/backend/commit/d4e35521f ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-18 14:11:55+03:00

138.139
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-8087: Добавил фильтр по активным группам (#1987)  [ https://github.yandex-team.ru/idm/backend/commit/7d37013ee ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-18 14:06:52+03:00

138.138
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8074: синхронизировать TVM-приложения из прода (#1985)  [ https://github.yandex-team.ru/idm/backend/commit/fac2dd1b3 ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * Команда для правки уже созданных неправильных экшенов (#1982)  [ https://github.yandex-team.ru/idm/backend/commit/9d0885452 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-18 11:35:30+03:00

138.137
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-6498: Поправил множественное число (#1984)  [ https://github.yandex-team.ru/idm/backend/commit/6bb2f8a4d ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-17 19:38:36+03:00

138.136
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8157: По умолчанию воркфлоу должен быть в песочнице (#1981)  [ https://github.yandex-team.ru/idm/backend/commit/56ea5b7db ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-17 15:23:59+03:00

138.135
-------
 * IDM-7567: Убрал default из определения полей (#1980)  [ https://github.yandex-team.ru/idm/backend/commit/8286e1945 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-09-16 19:28:06+03:00

138.134
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8155: ставить версию из changelog (#1979)  [ https://github.yandex-team.ru/idm/backend/commit/2967ea378 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-7567: Таска по копированию Action.pk в новые поля (#1976)  [ https://github.yandex-team.ru/idm/backend/commit/b2df81faa ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-16 16:51:36+03:00

138.133
-------
 * IDM-8149: Добавить tvm_id фронта IDM в тестинг b2b (#1978)  [ https://github.yandex-team.ru/idm/backend/commit/a6923271e ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-09-13 17:40:55+03:00

138.132
-------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8127 Пробрасывать организацию в связанные роли (#1977)                            [ https://github.yandex-team.ru/idm/backend/commit/fb12db17f ]
 * IDM-8043 Персональные роли в awaiting, если ресурс не привязан к оргaнизации (#1971)  [ https://github.yandex-team.ru/idm/backend/commit/fb3ee397f ]
 * IDM-8072 Отвязывание ресурса от организации (#1973)                                   [ https://github.yandex-team.ru/idm/backend/commit/111955eaa ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-13 16:41:33+03:00

138.131
-------
 * IDM-8134 У экшена в data не список, а словарь (#1975)  [ https://github.yandex-team.ru/idm/backend/commit/79689cf58 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-12 19:30:30+03:00

138.130
-------
 * IDM-8134 500 в ручке actions (#1974)  [ https://github.yandex-team.ru/idm/backend/commit/48c5ac3cf ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-12 14:55:17+03:00

138.129
-------
 * IDM-8071: Поправить api для того чтобы отрезать префикс организациям (#1970)  [ https://github.yandex-team.ru/idm/backend/commit/1acf30ae2 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-09-12 13:30:49+03:00

138.128
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8107: запретить редактировать auth_factor (#1972)  [ https://github.yandex-team.ru/idm/backend/commit/a780e1bae ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-11 15:46:20+03:00

138.127
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-8019: Приоритет языка со стаффа (#1969)  [ https://github.yandex-team.ru/idm/backend/commit/372dd2270 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-10 20:18:03+03:00

138.126
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8107: запретить редактировать base_url и tvm_id (#1963)  [ https://github.yandex-team.ru/idm/backend/commit/cddc65722 ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-8019: Поддержка Accept Language (#1960)  [ https://github.yandex-team.ru/idm/backend/commit/194c706b1 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Переименованы тесты в trendbox                             [ https://github.yandex-team.ru/idm/backend/commit/603a08adb ]
 * IDM-8070: Дописываем org_ к айдишнику организации (#1964)  [ https://github.yandex-team.ru/idm/backend/commit/f5ef99403 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-10 16:06:39+03:00

138.125
-------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8111 user_groups в разрешении расхождений (#1968)  [ https://github.yandex-team.ru/idm/backend/commit/ba296e9 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-09-10 15:00:38+03:00

138.124
-------
 * IDM-8058 Фикс миграции (#1967)  [ https://github.yandex-team.ru/idm/backend/commit/03f9f25be ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-09 16:41:27+03:00

138.123
-------
 * IDM-8058 Отключение автоматического разрешения неконсистентностей (#1965)  [ https://github.yandex-team.ru/idm/backend/commit/83561fc02 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-09 16:02:42+03:00

138.122
-------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8109 Починить API в b2b (#1966)  [ https://github.yandex-team.ru/idm/backend/commit/57f9ad0c5 ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-6498: Отступы и логины (#1957)                                                                                   [ https://github.yandex-team.ru/idm/backend/commit/83fa81d84 ]
 * IDM-8087: Отдавать возможность поставить галки with_robots, external для ролей на вики-группы и ABC-сервисы (#1959)  [ https://github.yandex-team.ru/idm/backend/commit/87a11a4a0 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-09 15:15:20+03:00

138.121
-------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-8044 Добавить ручки /systems, /rolenodes, /inconsistencies, /actions в b2b (#1958)  [ https://github.yandex-team.ru/idm/backend/commit/d9c66d18e ]
 * IDM-8102 Запуск тестов в разных тасках (#1962)                                          [ https://github.yandex-team.ru/idm/backend/commit/7664bd0cd ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-8033: Положил в action.data код ответа системы (#1946)  [ https://github.yandex-team.ru/idm/backend/commit/f97f28f31 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-06 12:55:42+03:00

138.120.1
-------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-8111 user_groups в разрешении расхождений (#1968)  [ https://github.yandex-team.ru/idm/backend/commit/2d99ed9 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-09-10 18:50:50+03:00

138.120
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8096: пересоздавать списки в контексте (#1961)  [ https://github.yandex-team.ru/idm/backend/commit/6828a3416 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-05 20:35:14+03:00

138.119
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8088: Не запускать пайплайн в апи для cauth (#1956)  [ https://github.yandex-team.ru/idm/backend/commit/52157d5c6 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-04 19:20:00+03:00

138.118
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-6498: Поправил отображение большого количества подтверждающих (#1955)  [ https://github.yandex-team.ru/idm/backend/commit/1875c56fd ]
 * IDM-8005: request_new_system_responsibles intranet_only (#1951)            [ https://github.yandex-team.ru/idm/backend/commit/f6ea0cb15 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-04 17:58:32+03:00

138.117
-------
 * Убрать tvm_middleware  [ https://github.yandex-team.ru/idm/backend/commit/1f17b140f ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-04 13:57:12+03:00

138.116
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7487: allowed_clients (#1954)  [ https://github.yandex-team.ru/idm/backend/commit/ce7c8e40a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-04 12:10:38+03:00

138.115
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8063: Отзывать только выданные по групповым роли внешних/роботов (#1953)  [ https://github.yandex-team.ru/idm/backend/commit/d12fd6752 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-04 11:25:23+03:00

138.114
-------

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2019-09-03 21:39:28+03:00

138.113
-------

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-03 21:31:46+03:00

138.112
-------
 * хотфикс  [ https://github.yandex-team.ru/idm/backend/commit/25ce0852f ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-03 21:20:11+03:00

138.111
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-6498: Исправил шаблон письма об отзыве роли (#1950)  [ https://github.yandex-team.ru/idm/backend/commit/002054855 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-03 19:59:16+03:00

138.110
-------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-7936: Поддержать batch-запросы и ручку approverequests в b2b (#1927)  [ https://github.yandex-team.ru/idm/backend/commit/03e94991e ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7800: Добавил в текст тикета обсуждения запроса роли комментарий при запросе роли (#1942)  [ https://github.yandex-team.ru/idm/backend/commit/5bd5e18a7 ]
 * Добавил создание экшенов при восcтановлении tvm-групп (#1948)                                  [ https://github.yandex-team.ru/idm/backend/commit/325a34537 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-09-03 14:34:07+03:00

138.109
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * lower slug (#1952)  [ https://github.yandex-team.ru/idm/backend/commit/f2c0982ca ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-03 12:18:32+03:00

138.108
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-6498: Изменил шаблон уведомлений о запросе роли (#1939)    [ https://github.yandex-team.ru/idm/backend/commit/db9a46366 ]
 * IDM-7956: Сокращение числа писем об удаляющихся нодах (#1943)  [ https://github.yandex-team.ru/idm/backend/commit/1e398baee ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-03 10:07:24+03:00

138.107
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * Поменял механизм удаления system.creator (#1949)  [ https://github.yandex-team.ru/idm/backend/commit/c04bbca9b ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-02 18:53:40+03:00

138.106
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7693: Добавил новые типы экшенов (#1933)  [ https://github.yandex-team.ru/idm/backend/commit/5937d8f7f ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-02 17:53:41+03:00

138.105
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-8005: Поправил команду для запроса ролей  после создания системы (#1947)  [ https://github.yandex-team.ru/idm/backend/commit/59dea91ef ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-09-02 16:15:55+03:00

138.104
-------

* [Valentin Shubin](http://staff/shubinv@yandex-team.ru)

 * IDM-7487 добавлена TVMMiddleware и тесты для неё (#1934)  [ https://github.yandex-team.ru/idm/backend/commit/32cb690da ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-09-02 15:46:48+03:00

138.103
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-8005: Крон команда и мониторинг (#1945)  [ https://github.yandex-team.ru/idm/backend/commit/c5a557085 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-08-30 19:01:15+03:00

138.102
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * Миграция для SystemRolePush (#1944)  [ https://github.yandex-team.ru/idm/backend/commit/3001a7c7a ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-08-30 16:05:14+03:00

138.101
-------

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-08-30 13:01:55+03:00

138.100
-------
 * Порядок миграций  [ https://github.yandex-team.ru/idm/backend/commit/58274f650 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-30 12:10:37+03:00

138.99
------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-8005: Исправление багов бэкенда при создании и настройке систем (#1941)  [ https://github.yandex-team.ru/idm/backend/commit/aeed5048e ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-08-30 10:38:42+03:00

138.98
------

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * releasing version 138.60.2  [ https://github.yandex-team.ru/idm/backend/commit/b0e1ae964 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7874: all_heads, head, internal_head перенесены в plain (#1902)  [ https://github.yandex-team.ru/idm/backend/commit/c117d938a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-29 17:56:22+03:00

138.97
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-8023: сериализация ошибок (#1940)  [ https://github.yandex-team.ru/idm/backend/commit/f582c5540 ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * Починил отзыв ролей (#1932)                                      [ https://github.yandex-team.ru/idm/backend/commit/216b6bc4a ]
 * IDM-7974: Поправить плагины для работы с новыми полями  (#1930)  [ https://github.yandex-team.ru/idm/backend/commit/2a11389e3 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-29 17:07:05+03:00

138.96
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-4919: глобальные функции (#1937)  [ https://github.yandex-team.ru/idm/backend/commit/ac031c4f4 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-27 16:47:18+03:00

138.95
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7982: не десериализовать лишнее (#1938)  [ https://github.yandex-team.ru/idm/backend/commit/3853eaa9a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-27 12:55:42+03:00

138.94
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7982: initial_properties в воркфлоу (#1936)  [ https://github.yandex-team.ru/idm/backend/commit/182a5c8e5 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-27 10:50:13+03:00

138.93
------
 * list  [ https://github.yandex-team.ru/idm/backend/commit/b23883c63 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-26 16:41:06+03:00

138.92
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Добавить пермишенов создателю (#1935)  [ https://github.yandex-team.ru/idm/backend/commit/b1edee74d ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-26 16:18:56+03:00

138.91
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7983: перейти на новые поля (#1929)  [ https://github.yandex-team.ru/idm/backend/commit/e6325bcc7 ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * Поправил значения по умолчанию в форме для новых полей (#1931)  [ https://github.yandex-team.ru/idm/backend/commit/55078c921 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-26 10:45:48+03:00

138.90
------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7970: Поправил логику выдачи персональных ролей по новым правилам (#1926)  [ https://github.yandex-team.ru/idm/backend/commit/c2af3267b ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-21 13:36:55+03:00

138.89
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7973: lowercase slug (#1928)  [ https://github.yandex-team.ru/idm/backend/commit/a6955bbed ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7927: Прокидывать в workflow новые поля (#1913)  [ https://github.yandex-team.ru/idm/backend/commit/e5e6a24b6 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-20 15:58:49+03:00

138.88
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7829: request_fields (#1925)  [ https://github.yandex-team.ru/idm/backend/commit/626ebc145 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-19 18:20:22+03:00

138.87
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7864: синхронизация ролей и ресурсов (#1916)  [ https://github.yandex-team.ru/idm/backend/commit/67bdde193 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7799 Отрпавлять deleted=1 при отзыве роли удаленной группы (#1924)  [ https://github.yandex-team.ru/idm/backend/commit/598323b3f ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7796: Расширенный Доступ в Атлас (#1923)                        [ https://github.yandex-team.ru/idm/backend/commit/af09b963c ]
 * Отдавать необходимость галок в отдельной ручке для фронтаc (#1911)  [ https://github.yandex-team.ru/idm/backend/commit/349f18e69 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-19 10:18:32+03:00

138.86
------
 * IDM-7948 Не писать в логи токены, если они есть в url (#1922)  [ https://github.yandex-team.ru/idm/backend/commit/2060f7205 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-15 17:04:42+03:00

138.85
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7865: локи в b2b (#1921)  [ https://github.yandex-team.ru/idm/backend/commit/08feb78c5 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-15 11:36:00+03:00

138.84
------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7754: Отдавать правильную и понятную ошибку при запросе роли с смс-информированием на tvm приложение (#1918)  [ https://github.yandex-team.ru/idm/backend/commit/660691078 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-08-15 10:27:28+03:00

138.83
------
 * IDM-7948 не писать токен в логи (#1920)  [ https://github.yandex-team.ru/idm/backend/commit/c978edf7f ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-14 21:26:41+03:00

138.82
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * slug (#1917)  [ https://github.yandex-team.ru/idm/backend/commit/fd09ebd34 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7948 Не писать токен в логи (#1919)  [ https://github.yandex-team.ru/idm/backend/commit/1a7821b1a ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7871: Добавить поддержку новых полей в апи (#1897)  [ https://github.yandex-team.ru/idm/backend/commit/d83348397 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-14 20:54:16+03:00

138.81
------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7809 Сеттинги и тесты (#1910)  [ https://github.yandex-team.ru/idm/backend/commit/d2890fa04 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-13 15:55:34+03:00

138.80
------
 * lock_by_select  [ https://github.yandex-team.ru/idm/backend/commit/4a0a4122c ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-13 15:53:48+03:00

138.79
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Использовать zdm (#1906)  [ https://github.yandex-team.ru/idm/backend/commit/841004ba6 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7919 Починить 403 при походах в нас с tvm в b2b (#1912)  [ https://github.yandex-team.ru/idm/backend/commit/9523b3426 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-13 15:29:41+03:00

138.78
------
 * IDM-7892 Писать логи приложения idm (#1915)  [ https://github.yandex-team.ru/idm/backend/commit/f339bb88f ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-12 19:34:22+03:00

138.77
------
 * IDM-7892 Логирование синка дерева узлов (#1914)  [ https://github.yandex-team.ru/idm/backend/commit/4b0a62169 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-12 18:12:19+03:00

138.76
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7649: фикс (#1909)  [ https://github.yandex-team.ru/idm/backend/commit/125fbb820 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-09 14:44:58+03:00

138.75
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7649 Сбрасываем хэш при синке департаментных групп (#1908)  [ https://github.yandex-team.ru/idm/backend/commit/0bea0fd ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-08-08 19:25:22+03:00

138.74
------

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-08 17:17:23+03:00

138.73
------

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-08 15:46:01+03:00

138.72
------

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-08 15:43:14+03:00

138.71
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7875: проверять org_id в уникальности роли (#1904)  [ https://github.yandex-team.ru/idm/backend/commit/9aa4cfd18 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-08 15:10:37+03:00

138.70
------
 * IDM-7879 Отвечать на ping в b2b (#1907)  [ https://github.yandex-team.ru/idm/backend/commit/d8954156c ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-08 10:11:20+03:00

138.69
------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7867: Добавить 3 поля в Role и System (#1905)  [ https://github.yandex-team.ru/idm/backend/commit/e19f48b94 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-08-07 14:02:57+03:00

138.68
------
 * Revert "IDM-7867: Добавить 3 поля в Role и System (#1896)"  [ https://github.yandex-team.ru/idm/backend/commit/c52dd8899 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-07 12:06:24+03:00

138.67
------
 * Фикс миграций  [ https://github.yandex-team.ru/idm/backend/commit/f9aca30e0 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-07 11:49:48+03:00

138.66
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Не импортировать лишнее (#1903)  [ https://github.yandex-team.ru/idm/backend/commit/1293c6742 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-07 11:42:32+03:00

138.65
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7866: отзывать роли без оповещения при удалении организации (#1898)  [ https://github.yandex-team.ru/idm/backend/commit/d0325bd3d ]
 * IDM-7707: еще фикс песочницы (#1877)                                     [ https://github.yandex-team.ru/idm/backend/commit/df7c6e306 ]
 * IDM-7707: правки воркфлоу (#1872)                                        [ https://github.yandex-team.ru/idm/backend/commit/8215f3843 ]
 * Апи по умолчанию json (#1868)                                            [ https://github.yandex-team.ru/idm/backend/commit/defde814a ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7879 Добавить /ping в исключения в b2b (#1900)  [ https://github.yandex-team.ru/idm/backend/commit/d77804715 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * releasing version 138.64    [ https://github.yandex-team.ru/idm/backend/commit/750497f68 ]
 * releasing version 138.60.1  [ https://github.yandex-team.ru/idm/backend/commit/463b6bb3a ]
 * releasing version 138.41.2  [ https://github.yandex-team.ru/idm/backend/commit/41a622768 ]
 * releasing version 138.41.1  [ https://github.yandex-team.ru/idm/backend/commit/f40a4ff59 ]
 * releasing version 138.41    [ https://github.yandex-team.ru/idm/backend/commit/c7835b2c6 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7874: all_heads, head, internal_head перенесены в plain (#1902)  [ https://github.yandex-team.ru/idm/backend/commit/e39c08541 ]
 * IDM-7874: is_external теперь прокидывается в wf как функция (#1899)  [ https://github.yandex-team.ru/idm/backend/commit/ab4408b09 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-07 10:23:25+03:00

138.64
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7866: отзывать роли без оповещения при удалении организации (#1898)  [ https://github.yandex-team.ru/idm/backend/commit/d0325bd3d ]
 * IDM-7707: еще фикс песочницы (#1877)                                     [ https://github.yandex-team.ru/idm/backend/commit/df7c6e306 ]
 * IDM-7707: правки воркфлоу (#1872)                                        [ https://github.yandex-team.ru/idm/backend/commit/8215f3843 ]
 * Апи по умолчанию json (#1868)                                            [ https://github.yandex-team.ru/idm/backend/commit/defde814a ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7879 Добавить /ping в исключения в b2b (#1900)  [ https://github.yandex-team.ru/idm/backend/commit/d77804715 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * releasing version 138.60.1  [ https://github.yandex-team.ru/idm/backend/commit/463b6bb3a ]
 * releasing version 138.41.2  [ https://github.yandex-team.ru/idm/backend/commit/41a622768 ]
 * releasing version 138.41.1  [ https://github.yandex-team.ru/idm/backend/commit/f40a4ff59 ]
 * releasing version 138.41    [ https://github.yandex-team.ru/idm/backend/commit/c7835b2c6 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7874: all_heads, head, internal_head перенесены в plain (#1902)  [ https://github.yandex-team.ru/idm/backend/commit/e39c08541 ]
 * IDM-7874: is_external теперь прокидывается в wf как функция (#1899)  [ https://github.yandex-team.ru/idm/backend/commit/ab4408b09 ]
 * IDM-7874: is_external теперь прокидывается в wf как функция (#1899)  [ https://github.yandex-team.ru/idm/backend/commit/c7722390f ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-07 10:21:57+03:00

138.63
------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7867: Добавить 3 поля в Role и System (#1896)  [ https://github.yandex-team.ru/idm/backend/commit/528804b30 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-08-06 12:30:21+03:00

138.62
------

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-06 10:48:18+03:00

138.61
------
 * IDM-7766 Исправлены заголовки запроса (#1895)  [ https://github.yandex-team.ru/idm/backend/commit/674dc7af0 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-06 10:12:15+03:00

138.60.2
--------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7874: all_heads, head, internal_head перенесены в plain (#1902)  [ https://github.yandex-team.ru/idm/backend/commit/c117d938a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-06 18:07:26+03:00

138.60.1
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7874: is_external теперь прокидывается в wf как функция (#1899)  [ https://github.yandex-team.ru/idm/backend/commit/ab4408b09 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-06 16:34:05+03:00

138.60
------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7666 Fix в PATCH системы (#1894)  [ https://github.yandex-team.ru/idm/backend/commit/a7a017fea ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-05 19:45:04+03:00

138.59
------
 * IDM-7766 Фикс миграций (#1893)  [ https://github.yandex-team.ru/idm/backend/commit/b89b06214 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-08-05 16:33:55+03:00

138.58
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Приводить Context к dict (#1892)  [ https://github.yandex-team.ru/idm/backend/commit/3dff20bee ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-05 15:05:37+03:00

138.57
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7857: проверять членства на активность (#1891)  [ https://github.yandex-team.ru/idm/backend/commit/99bdc7f13 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7766 Фикс импорта (#1890)  [ https://github.yandex-team.ru/idm/backend/commit/8b80d10ef ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-05 13:43:07+03:00

138.56
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-4919: globals вместо locals (#1888)  [ https://github.yandex-team.ru/idm/backend/commit/cc30cbb49 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-05 11:03:59+03:00

138.55
------
 * IDM-7667: актуализированы доступные поля и ограничения (#1887)  [ https://github.yandex-team.ru/idm/backend/commit/0dd66890a ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-08-02 17:55:55+03:00

138.54
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7851: поддержать тип пользователя в ручке тестирования воркфлоу (#1886)  [ https://github.yandex-team.ru/idm/backend/commit/3f15da9 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7765 Отзывать роли пользователя при выходе из организации (#1885)  [ https://github.yandex-team.ru/idm/backend/commit/a242518 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7766 Таска по синхронизации пользователей с Коннектом (#1882)  [ https://github.yandex-team.ru/idm/backend/commit/2c49e51 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-08-02 17:20:34+03:00

138.53
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * PATCH такой же как GET (#1884)  [ https://github.yandex-team.ru/idm/backend/commit/77d3b3ff7 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-01 16:21:05+03:00

138.52
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7795: last_request_comment (#1880)  [ https://github.yandex-team.ru/idm/backend/commit/866a28914 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7765 emails как список (#1883)  [ https://github.yandex-team.ru/idm/backend/commit/abc3323f7 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-08-01 14:25:43+03:00

138.51
------

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-31 18:20:17+03:00

138.50
------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7742: Количество узлов в статусе depriving (#1881)  [ https://github.yandex-team.ru/idm/backend/commit/8bcfbeaf1 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-31 17:54:57+03:00

138.49
------
 * IDM-7742: Количество узлов в статусе depriving  [ https://github.yandex-team.ru/idm/backend/commit/aeca7ac7f ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-31 17:20:08+03:00

138.48
------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7666 add is_broken field (#1879)  [ https://github.yandex-team.ru/idm/backend/commit/56b3bc199 ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7742 Количество узлов в статусе depriving (#1873)          [ https://github.yandex-team.ru/idm/backend/commit/542826ea7 ]
 * IDM-7747: График успешных/не успешных синков деревьев (#1878)  [ https://github.yandex-team.ru/idm/backend/commit/6f4b2611d ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-31 16:03:13+03:00

138.47
------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7768 Обработка org_id в API IDM (#1874)          [ https://github.yandex-team.ru/idm/backend/commit/f7ae9cb ]
 * IDM-7666 Доработки для ручки PATCH /systems (#1876)  [ https://github.yandex-team.ru/idm/backend/commit/b4f072c ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-7788: Добавил сеттинги IDM_B2B_ROBOT (#1870)  [ https://github.yandex-team.ru/idm/backend/commit/4fe84ad ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-07-31 14:12:44+03:00

138.46
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7707: еще фикс песочницы (#1877)       [ https://github.yandex-team.ru/idm/backend/commit/8f6a6c524 ]
 * IDM-7820: удалить старые миграции (#1875)  [ https://github.yandex-team.ru/idm/backend/commit/27390f078 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * releasing version 138.45  [ https://github.yandex-team.ru/idm/backend/commit/c3dba9cce ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-31 10:19:55+03:00

138.45
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7820: поменьше миграций (#1871)  [ https://github.yandex-team.ru/idm/backend/commit/c2ef2c309 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-30 19:44:36+03:00

138.44
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7707: правки воркфлоу (#1872)  [ https://github.yandex-team.ru/idm/backend/commit/a85101db9 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-30 16:41:10+03:00

138.43
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7667: Ручка пермишенов редактирования системы (#1869)  [ https://github.yandex-team.ru/idm/backend/commit/bd2a3ed37 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7769 Отключить лишнюю функциональность в Коннекте (#1865)  [ https://github.yandex-team.ru/idm/backend/commit/ecbb777c0 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-7788: В зависимости от флага передавать путь при загрузке сеттингов (#1853)  [ https://github.yandex-team.ru/idm/backend/commit/9a7f82f02 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-30 16:26:33+03:00

138.42
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7804: проставлять юзера из заголовка (#1862)  [ https://github.yandex-team.ru/idm/backend/commit/f23e22a58 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-29 15:57:54+03:00

138.41.2
--------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7707: еще фикс песочницы (#1877)  [ https://github.yandex-team.ru/idm/backend/commit/df7c6e306 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-31 14:22:32+03:00

138.41.1
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7707: правки воркфлоу (#1872)  [ https://github.yandex-team.ru/idm/backend/commit/8215f3843 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-30 16:53:21+03:00

138.41
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Апи по умолчанию json (#1868)  [ https://github.yandex-team.ru/idm/backend/commit/d4c99628b ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-29 14:27:22+03:00

138.40
------
 * Исправлены миграции (#1867)  [ https://github.yandex-team.ru/idm/backend/commit/5a2abf307 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-29 13:33:10+03:00

138.39
------
 * deserialize  [ https://github.yandex-team.ru/idm/backend/commit/434bb7b20 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-29 12:08:42+03:00

138.38
------
 * Serializable  [ https://github.yandex-team.ru/idm/backend/commit/560cdd2d5 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-29 11:33:34+03:00

138.37
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Alllist (#1866)  [ https://github.yandex-team.ru/idm/backend/commit/14c4afca4 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-29 11:18:24+03:00

138.36
------
 * Починил тесты  [ https://github.yandex-team.ru/idm/backend/commit/5d481e03f ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-28 17:27:29+03:00

138.35
------
 * Еще миграции  [ https://github.yandex-team.ru/idm/backend/commit/1ed688d58 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-26 17:54:10+03:00

138.34
------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7733 Добавил обработку случая, когда группа и родитель имеют разн… (#1863)  [ https://github.yandex-team.ru/idm/backend/commit/0a03288e1 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-26 17:29:12+03:00

138.33
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Только группы пользователей в groupify (#1864)  [ https://github.yandex-team.ru/idm/backend/commit/b47af9e8d ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * releasing version 138.6.1  [ https://github.yandex-team.ru/idm/backend/commit/15e40e9e2 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-26 17:25:17+03:00

138.32
------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7666 Ручка PATCH редактирования системы (#1852)  [ https://github.yandex-team.ru/idm/backend/commit/bf29d2619 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-26 17:23:19+03:00

138.31
------
 * Миграции  [ https://github.yandex-team.ru/idm/backend/commit/9b8121404 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-26 16:57:43+03:00

138.30
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Переливать json получше (#1861)                  [ https://github.yandex-team.ru/idm/backend/commit/b18007a98 ]
 * IDM-7764: ручка для пушей от Директории (#1850)  [ https://github.yandex-team.ru/idm/backend/commit/be3b63b94 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-26 16:17:39+03:00

138.29
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Правка мидлвари (#1860)  [ https://github.yandex-team.ru/idm/backend/commit/02776bbcd ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-25 20:59:36+03:00

138.28
------
 * Переименование миграции  [ https://github.yandex-team.ru/idm/backend/commit/4437eb1ca ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-25 20:35:42+03:00

138.27
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7792: переливать данные в новые поля (#1857)  [ https://github.yandex-team.ru/idm/backend/commit/9ba4939db ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7645 Поправил время в метриках (#1859)  [ https://github.yandex-team.ru/idm/backend/commit/08bd7fcf6 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-25 20:27:44+03:00

138.26
------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * Поправил миграции (#1858)                 [ https://github.yandex-team.ru/idm/backend/commit/7cdf2e9e4 ]
 * feature/IDM-7733: Поправил форму (#1856)  [ https://github.yandex-team.ru/idm/backend/commit/c3dfd4204 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-25 19:45:06+03:00

138.25
------
 * IDM-7699 Перешел на текстовый id в кондукторном саджесте  [ https://github.yandex-team.ru/idm/backend/commit/11dcbe0 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-25 19:06:19+03:00

138.24
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7787 Написать новый плагин для систем в Коннекте (#1851)  [ https://github.yandex-team.ru/idm/backend/commit/58db3f184 ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7645 Измерить время работы pipeline (#1834)  [ https://github.yandex-team.ru/idm/backend/commit/55067369a ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-25 18:38:44+03:00

138.23
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7819: django 1.9 (#1854)  [ https://github.yandex-team.ru/idm/backend/commit/bd127da58 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-25 16:25:35+03:00

138.22
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7665 Случай пустого description (#1849)  [ https://github.yandex-team.ru/idm/backend/commit/a6af396 ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * Поправил тест (#1846)  [ https://github.yandex-team.ru/idm/backend/commit/0059da9 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-25 16:13:39+03:00

138.21
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Поменять параметр (#1848)  [ https://github.yandex-team.ru/idm/backend/commit/19d8f3fd2 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-24 17:27:04+03:00

138.20
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7717: не создавать сервисы несколько раз (#1847)  [ https://github.yandex-team.ru/idm/backend/commit/dfe93747a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-24 17:10:17+03:00

138.19
------
 * IDM-7665 Поправил config trendbox              [ https://github.yandex-team.ru/idm/backend/commit/5223786 ]
 * IDM-7665 Обертка создателя и self может везде  [ https://github.yandex-team.ru/idm/backend/commit/af71a39 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-24 12:40:19+03:00

138.18
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * base_field (#1841)  [ https://github.yandex-team.ru/idm/backend/commit/096a6934c ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * Feature/IDM 7647 График времени синка систем (#1833)  [ https://github.yandex-team.ru/idm/backend/commit/f81fe2cf6 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-24 11:45:58+03:00

138.17
------
 * IDM-7668 Отдавать доп. поля ответственным за систему и команде (#1844)  [ https://github.yandex-team.ru/idm/backend/commit/42532bf73 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-24 11:22:06+03:00

138.16
------
 * Прокидывать UserWrapper.get_robot_owners в контейнер (#1843)  [ https://github.yandex-team.ru/idm/backend/commit/7f27189a8 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-23 16:57:22+03:00

138.15
------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-773 Теперь возвращаются только активные роли (#1842)  [ https://github.yandex-team.ru/idm/backend/commit/5edf50490 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-23 16:39:54+03:00

138.14
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7665 Ручка создания системы (#1839)  [ https://github.yandex-team.ru/idm/backend/commit/9616572 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-23 15:02:55+03:00

138.13
------
 * IDM-7699: импорт кондукторных групп, саджест по ним (#1840)  [ https://github.yandex-team.ru/idm/backend/commit/907247940 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-23 13:42:07+03:00

138.12
------
 * IDM-7668 Расширить ручку GET для систем (#1838)  [ https://github.yandex-team.ru/idm/backend/commit/b900d5b76 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-23 11:35:04+03:00

138.11
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7717: проверять права для ролей TVM-приложений (#1837)  [ https://github.yandex-team.ru/idm/backend/commit/e9a53e6ee ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-23 10:37:12+03:00

138.10
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7716: синхронизировать ответственных за TVM (#1835)  [ https://github.yandex-team.ru/idm/backend/commit/5e08a5946 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-22 12:14:31+03:00

138.9
-----

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7733 Добавил обработку департаментов (#1824)  [ https://github.yandex-team.ru/idm/backend/commit/ab8167ce6 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-19 13:02:02+03:00

138.8
-----
 * Переименование миграций  [ https://github.yandex-team.ru/idm/backend/commit/4bbb3add4 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-19 12:55:23+03:00

138.7
-----

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7747: График успешных/не успешных синков деревьев (#1832)  [ https://github.yandex-team.ru/idm/backend/commit/fb0fad208 ]
 * IDM-7298: Убрал из кода 'use_priority' (#1827)                 [ https://github.yandex-team.ru/idm/backend/commit/ddd314b58 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-19 12:14:35+03:00

138.6.1
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Только группы пользователей в groupify (#1864)  [ https://github.yandex-team.ru/idm/backend/commit/b47af9e8d ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-26 17:08:22+03:00

138.6
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7741: добавить mixin (#1831)  [ https://github.yandex-team.ru/idm/backend/commit/f24c0e9ff ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-18 16:10:21+03:00

138.5
-----

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7714: ручка диффа ролей (#1817)  [ https://github.yandex-team.ru/idm/backend/commit/6f1f94496 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-18 14:54:31+03:00

138.4
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7741: RoleWrapper (#1830)  [ https://github.yandex-team.ru/idm/backend/commit/e0a095d81 ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7641fix-3 Исправил ошибку при закрытии тикета (#1829)  [ https://github.yandex-team.ru/idm/backend/commit/3d6bc1d0a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-18 14:33:26+03:00

138.3
-----
 * IDM-7739: 'NoneType' object has no attribute 'get_descendant_memberships' (#1828)  [ https://github.yandex-team.ru/idm/backend/commit/36605aa56 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-07-17 20:22:57+03:00

138.2
-----

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7641 Поправил закрытие тикета (#1826)  [ https://github.yandex-team.ru/idm/backend/commit/fe6f08f60 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7664: добавлено поле creator, его учёт в проверке прав; пермишн безопасников выдан ответственным/участникам команды  [ https://github.yandex-team.ru/idm/backend/commit/fc538458a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-17 16:53:22+03:00

138.1
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7620: проверять, что id - int (#1819)                  [ https://github.yandex-team.ru/idm/backend/commit/0ab629b53 ]
 * IDM-7732: Снять ограничение на длину имени у User (#1822)  [ https://github.yandex-team.ru/idm/backend/commit/a0bf0129f ]
 * IDM-7673: запрос быстрее (#1823)                           [ https://github.yandex-team.ru/idm/backend/commit/286bd0240 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-17 15:30:47+03:00

138.0
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * Feature/idm 7695 (#1810)  [ https://github.yandex-team.ru/idm/backend/commit/ce3b84e4b ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-16 10:41:12+03:00

137.126
-------
 * IDM-7614: добавлена метрика размера celery-очередей по количеству задач в MongoDB (#1821)  [ https://github.yandex-team.ru/idm/backend/commit/660bc4dc8 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-15 16:20:07+03:00

137.125
-------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7165 [Testing] и whitelist номеров (#1815)  [ https://github.yandex-team.ru/idm/backend/commit/f1fdd81 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-15 14:50:41+03:00

137.124
-------
 * IDM-6979 Исправлен поярдок миграций (#1820)  [ https://github.yandex-team.ru/idm/backend/commit/15b18529d ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-15 10:49:20+03:00

137.123
-------
 * IDM-6979 Разрешить разрешать расхождения в пользу IDM (#1812)  [ https://github.yandex-team.ru/idm/backend/commit/ff1fb3ac5 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-15 10:34:25+03:00

137.122
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7625: проставлять suggest_ok_* (#1816)  [ https://github.yandex-team.ru/idm/backend/commit/9d8d733cb ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-15 10:04:07+03:00

137.121
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7624: крон (#1814)  [ https://github.yandex-team.ru/idm/backend/commit/50a640ee7 ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7691: функция, которая получает изменения при перемещении сервиса (#1809)  [ https://github.yandex-team.ru/idm/backend/commit/d3cbdc63d ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-12 10:27:42+03:00

137.120
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7624: проверять slug_path у запушенных узлов (#1813)  [ https://github.yandex-team.ru/idm/backend/commit/6db4d629a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-11 19:38:51+03:00

137.119
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7623: Добавить в базу поля pushed_at и moved_at (#1808)  [ https://github.yandex-team.ru/idm/backend/commit/f94b8751b ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-11 16:17:25+03:00

137.118
-------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7670 Проверка прав системы и равенства юзеров (#1811)  [ https://github.yandex-team.ru/idm/backend/commit/72e76d7 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-11 15:01:21+03:00

137.117
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7673: починить два мониторинга (#1806)  [ https://github.yandex-team.ru/idm/backend/commit/c02f298cc ]

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7680: Получать галку из API ABC (#1807)  [ https://github.yandex-team.ru/idm/backend/commit/48a963f0d ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-11 10:57:04+03:00

137.116
-------
 * IDM-7675 Добавить id узла в пуши на удаление в intrasearch (#1805)  [ https://github.yandex-team.ru/idm/backend/commit/3541aaf9d ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-10 11:52:53+03:00

137.115
-------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7670 Прокинул еще методов в sb workflow (#1804)  [ https://github.yandex-team.ru/idm/backend/commit/286288c ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-10 10:53:12+03:00

137.114
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7641-6: Ручка обсуждения запроса роли (#1803)  [ https://github.yandex-team.ru/idm/backend/commit/3f2fd9862 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-10 10:25:22+03:00

137.113
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7641-3: Ручка обсуждения запроса роли (#1802)  [ https://github.yandex-team.ru/idm/backend/commit/a29af3e83 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-09 19:11:27+03:00

137.112
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7641: Ручка обсуждения запроса роли (#1800)  [ https://github.yandex-team.ru/idm/backend/commit/12c33f9f8 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-09 17:18:06+03:00

137.111
-------
 * IDM-7642 Отдавать tvm-app в фильтрах по пользователю (#1798)  [ https://github.yandex-team.ru/idm/backend/commit/122756f26 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-09 11:14:23+03:00

137.110
-------

* [Yury Mironov](http://staff/stupidhobbit@yandex-team.ru)

 * IDM-7641: Ручка обсуждения запроса роли (#1792)  [ https://github.yandex-team.ru/idm/backend/commit/e7fdeb092 ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7590 Сериализация НеWorkflowError и таймауты  [ https://github.yandex-team.ru/idm/backend/commit/c54ec23a6 ]

[Yura Mironov](http://staff/stupidhobbit@yandex-team.ru) 2019-07-08 20:15:52+03:00

137.109
-------
 * IDM-7639 Починить карточку роли для tvm_app (#1790)                                             [ https://github.yandex-team.ru/idm/backend/commit/955e4ad53 ]
 * IDM-7635 Рассылать письма о членствах, к которым необходимо привязать паспортный логин (#1794)  [ https://github.yandex-team.ru/idm/backend/commit/074e482c2 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-08 18:58:20+03:00

137.108
-------

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7590 Проверка доступности метода из контейнера  [ https://github.yandex-team.ru/idm/backend/commit/e760eb935 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-08 14:54:21+03:00

137.107
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7642: Поддержать tvm-приложения в ручке /api/frontend/users/<id>/ (#1791)  [ https://github.yandex-team.ru/idm/backend/commit/f08f10017 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-08 14:53:25+03:00

137.106
-------
 * IDM-7590 Добавил недостающих функций для запуска wf cauth  [ https://github.yandex-team.ru/idm/backend/commit/9c02f71 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-08 10:53:50+03:00

137.105
-------
 * Теперь можно фильтровать returnable роли (#1793)  [ https://github.yandex-team.ru/idm/backend/commit/b6a7163da ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-05 19:18:41+03:00

137.104
-------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7610 &gt; в plain text письмах (#1786)  [ https://github.yandex-team.ru/idm/backend/commit/1bcf34524 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-04 14:11:08+03:00

137.103
-------
 * IDM-7546: использовать одну константу  [ https://github.yandex-team.ru/idm/backend/commit/9828ca6f5 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-02 16:35:21+03:00

137.102
-------
 * IDM-7421 Пропускать модули при сериализации  [ https://github.yandex-team.ru/idm/backend/commit/38d6287 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-02 16:13:34+03:00

137.101
-------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7421 Доработка generic плагина для работы с tvm_app (#1788)  [ https://github.yandex-team.ru/idm/backend/commit/b6a5a46 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-02 15:06:33+03:00

137.100
-------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7115: валидировать длительность роли (#1785)  [ https://github.yandex-team.ru/idm/backend/commit/5d49c8e16 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-01 22:47:10+03:00

137.99
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7546: саджест по TVM-прилоежниям (#1783)  [ https://github.yandex-team.ru/idm/backend/commit/26bb2a8c5 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-01 20:19:19+03:00

137.98
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7582: Добавить поле с саджестом макросов (#1781)  [ https://github.yandex-team.ru/idm/backend/commit/f9d2cc164 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7592 Сделать мониторинг на пользователей без департаментных групп (#1776)  [ https://github.yandex-team.ru/idm/backend/commit/3e35cc646 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7422: ordering + page_size  [ https://github.yandex-team.ru/idm/backend/commit/797a78357 ]
 * Теперь modified_at работает     [ https://github.yandex-team.ru/idm/backend/commit/c59579871 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-01 18:13:41+03:00

137.97
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7422: синхронизация твм-приложений (#1777)  [ https://github.yandex-team.ru/idm/backend/commit/7d51e935a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-01 15:56:01+03:00

137.96
------
 * Поправлен url Racktables  [ https://github.yandex-team.ru/idm/backend/commit/465a80673 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-01 13:17:23+03:00

137.95
------
 * IDM-7590 Поправил нумерацию миграций  [ https://github.yandex-team.ru/idm/backend/commit/5128bee ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-01 11:42:01+03:00

137.94
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7590 Запуск доктестов в контейнере (#1779)  [ https://github.yandex-team.ru/idm/backend/commit/dea2ebd ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7606: Улучшить в саджестах фильтр по ID  [ https://github.yandex-team.ru/idm/backend/commit/ee5ee40 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7423 Добавляем настройку в "работает с tvm" для систем (#1778)  [ https://github.yandex-team.ru/idm/backend/commit/8123bfc ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-01 11:22:40+03:00

137.93
------
 * Поправлены аргументы команды idm_sync_macros  [ https://github.yandex-team.ru/idm/backend/commit/2f0e347f7 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-06-28 15:54:27+03:00

137.92
------
 * Разрешены конфликты миграций (теперь правильно)  [ https://github.yandex-team.ru/idm/backend/commit/04cd5523d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-06-28 13:39:09+03:00

137.91
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Разрешены конфликты миграций                      [ https://github.yandex-team.ru/idm/backend/commit/7aabdabb0 ]
 * IDM-7545: Саджест ручку саджеста Маросов (#1774)  [ https://github.yandex-team.ru/idm/backend/commit/4a1c9eed0 ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Корректная сериализация Recipient и WorkflowSyntaxError (#1773)  [ https://github.yandex-team.ru/idm/backend/commit/ddd222cee ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * releasing version 137.90  [ https://github.yandex-team.ru/idm/backend/commit/c3edeae60 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-06-28 12:49:43+03:00

137.90
------
 * IDM-7418 Добавляем новое поле: тип tvm_app / user (#1775)  [ https://github.yandex-team.ru/idm/backend/commit/46dea1b92 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-06-27 17:13:44+03:00

137.89
------

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * Временно не выполнять доктесты в контейнере  [ https://github.yandex-team.ru/idm/backend/commit/c31a9ec24 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Исправлена проблема с получением и workflow UserWrapper вместо User  [ https://github.yandex-team.ru/idm/backend/commit/e5b2528a2 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-25 19:04:21+03:00

137.88
------
 * IDM-7493: временно отключена изоляция сети контейнеров  [ https://github.yandex-team.ru/idm/backend/commit/73e1ad3b7 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-06-25 13:20:59+03:00

137.87
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7530 Фикс роста очереди на добавление узлов (#1767)  [ https://github.yandex-team.ru/idm/backend/commit/5c4dbc9bd ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * Обновление po mo файлов  [ https://github.yandex-team.ru/idm/backend/commit/cb79b15f4 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * Запускалка кода в контейнере  [ https://github.yandex-team.ru/idm/backend/commit/62f3379b0 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7493: Код запуска контейнера (#1763)  [ https://github.yandex-team.ru/idm/backend/commit/2d324e845 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-25 12:26:28+03:00

137.86
------
 * IDM-7496 В переменную group контекста приезжал GroupWrapper(groupify(external_id))  [ https://github.yandex-team.ru/idm/backend/commit/51e76d3 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-06-24 16:19:19+03:00

137.85
------
 * IDM-7496 Поддержка тестирования групповых ролей в доктестах  [ https://github.yandex-team.ru/idm/backend/commit/cb778b3 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-06-24 12:47:21+03:00

137.84
------
 * IDM-7561 Обработка дополнительных параметров в доктестах workflow  [ https://github.yandex-team.ru/idm/backend/commit/682cb62 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-06-21 16:58:49+03:00

137.83
------
 * IDM-7567 Убрал ограничение minvalue=1  в форме отчета (#1766)  [ https://github.yandex-team.ru/idm/backend/commit/78f7ce80f ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-06-21 16:44:51+03:00

137.82
------
 * IDM-7567 Поправлен порядок сортировки из-за отрицательных pk (#1764)  [ https://github.yandex-team.ru/idm/backend/commit/c61c4cb2e ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-06-21 14:28:16+03:00

137.81
------
 * IDM-5207: ручка для СИБ  [ https://github.yandex-team.ru/idm/backend/commit/1d8976d55 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-19 21:05:15+03:00

137.80
------
 * IDM-7506 Перенос времени запуска таски по сверке с системой (#1760)  [ https://github.yandex-team.ru/idm/backend/commit/95a332480 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-06-18 18:35:17+03:00

137.79
------
 * blank=True  [ https://github.yandex-team.ru/idm/backend/commit/a33e1850a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-18 18:13:28+03:00

137.78
------
 * IDM-7228: поправлены конфликты в миграциях  [ https://github.yandex-team.ru/idm/backend/commit/75c94fe73 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-06-18 14:35:46+03:00

137.77
------
 * IDM-7228: Добавить настройку системы  для работы с новым workflow (#1757)  [ https://github.yandex-team.ru/idm/backend/commit/974418edf ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-06-18 13:17:22+03:00

137.76
------
 * IDM-7134: фикс миграции  [ https://github.yandex-team.ru/idm/backend/commit/dbe6fccb2 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-17 11:47:26+03:00

137.75
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7214: Права систем смотреть на другие системы (#1755)  [ https://github.yandex-team.ru/idm/backend/commit/27c58fd73 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7134: убрать отложенные членства  [ https://github.yandex-team.ru/idm/backend/commit/99c17e161 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-14 17:43:08+03:00

137.74
------
 * IDM-7344 Перестать логировать токен (#1753)                           [ https://github.yandex-team.ru/idm/backend/commit/e918f41 ]
 * IDM-5304 Добавила условие is_key=False в команду, убрала лок (#1754)  [ https://github.yandex-team.ru/idm/backend/commit/fcaee78 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-06-10 16:31:30+03:00

137.73
------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-5304 Допинывалка нод в intrasearch (#1752)  [ https://github.yandex-team.ru/idm/backend/commit/0a75889 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * Добавлены переводы  [ https://github.yandex-team.ru/idm/backend/commit/db4a0b0 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-06-07 20:56:32+03:00

137.72
------
 * IDM-7303 Поправил запись лога  [ https://github.yandex-team.ru/idm/backend/commit/3425974 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-06-06 10:53:41+03:00

137.71
------

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * releasing version 137.56.2                       [ https://github.yandex-team.ru/idm/backend/commit/991f36300 ]
 * IDM-7437: отключить письма про захолженные роли  [ https://github.yandex-team.ru/idm/backend/commit/5ab2ce778 ]
 * IDM-7432: удалять членства уволенных             [ https://github.yandex-team.ru/idm/backend/commit/10e59e163 ]
 * IDM-7361: постоянно чинить дерево ABC            [ https://github.yandex-team.ru/idm/backend/commit/e87530360 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * releasing version 137.56.1                                                                       [ https://github.yandex-team.ru/idm/backend/commit/7f1f027e5 ]
 * IDM-7301: Настройка про паспортные логины для систем с политикой "aware_for_membership" (#1736)  [ https://github.yandex-team.ru/idm/backend/commit/6d9b45b4d ]

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7303 Добавляем pl при входе в группу с ролью в aware_of_memberships системе (#1741)  [ https://github.yandex-team.ru/idm/backend/commit/c29577207 ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * Запустил makemessages  [ https://github.yandex-team.ru/idm/backend/commit/a12ae110a ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-6701 добавить в апи id и статус узла, начать фильтровать по статусу (#1749)  [ https://github.yandex-team.ru/idm/backend/commit/b2bc34001 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-06-05 12:25:33+03:00

137.70
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7456: обновление django-idm-api (#1750)  [ https://github.yandex-team.ru/idm/backend/commit/9691d6782 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-04 19:15:02+03:00

137.69
------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * releasing version 137.68  [ https://github.yandex-team.ru/idm/backend/commit/3e0388a ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * releasing version 137.67  [ https://github.yandex-team.ru/idm/backend/commit/36b8f09 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-06-03 14:41:45+03:00

137.68
------
 * IDM-5073 Опечатка (#1748)  [ https://github.yandex-team.ru/idm/backend/commit/c98f065 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-06-03 14:41:33+03:00

137.67
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7223 Тест на склеивание трансферов (#1745)  [ https://github.yandex-team.ru/idm/backend/commit/08af4f1 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-05-31 18:44:38+03:00

137.66
------
 * IDM-5073 Fix tests  [ https://github.yandex-team.ru/idm/backend/commit/10112ed ]
 * IDM-5073 Переводы   [ https://github.yandex-team.ru/idm/backend/commit/b2cffba ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-05-31 17:17:42+03:00

137.65
------
 * IDM-6905 Убрать узлы с ответственными из выборки (#1746)  [ https://github.yandex-team.ru/idm/backend/commit/c5498ec2e ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-31 14:35:55+03:00

137.64
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7302 Привязка логинов к членствам в aware_of_memberships системах (#1735)  [ https://github.yandex-team.ru/idm/backend/commit/da73cde1e ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7437: отключить письма про захолженные роли  [ https://github.yandex-team.ru/idm/backend/commit/b83a811b2 ]
 * IDM-7432: удалять членства уволенных             [ https://github.yandex-team.ru/idm/backend/commit/5a9e1aa01 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-05-30 19:33:52+03:00

137.63
------
 * IDM-7361: постоянно чинить дерево ABC  [ https://github.yandex-team.ru/idm/backend/commit/822142877 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-05-30 12:10:29+03:00

137.62
------
 * IDM-6905 Новый плагин для сверки IDM с самим собой (#1740)  [ https://github.yandex-team.ru/idm/backend/commit/dc3f8e0ea ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-30 11:04:02+03:00

137.61
------
 * IDM-6905 Ускорить выдачу ручки get-roles (#1738)  [ https://github.yandex-team.ru/idm/backend/commit/5525f24b2 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-28 11:33:39+03:00

137.60
------
 * IDM-7301: Настройка про паспортные логины для систем с политикой "aware_for_membership" (#1736)  [ https://github.yandex-team.ru/idm/backend/commit/e965c79ec ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-05-27 21:23:10+03:00

137.59
------
 * IDM-6905 Исправлена выдача в ручке get-roles (#1737)  [ https://github.yandex-team.ru/idm/backend/commit/39dcdc6c7 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-27 18:56:45+03:00

137.58
------
 * IDM-6905 Переход на постраничную пагинацию (ручка get-roles) (#1734)  [ https://github.yandex-team.ru/idm/backend/commit/67461460c ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-27 16:47:07+03:00

137.57
------

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-27 16:05:59+03:00

137.56
------
 * IDM-7372: фильтровать только нужные роли ABC  [ https://github.yandex-team.ru/idm/backend/commit/86a861859 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-05-22 19:15:47+03:00

137.55
------
 * IDM-7335 Фикс роста sequence при синхронизации опосредованных членств (#1723)  [ https://github.yandex-team.ru/idm/backend/commit/167aacea0 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-22 10:59:27+03:00

137.54
------
 * IDM-7262: Исправил порядок миграций (#1732)  [ https://github.yandex-team.ru/idm/backend/commit/a4cc3da7f ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-05-21 14:37:18+03:00

137.53
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7262 Отслеживать изменения паспортных логинов (#1713)  [ https://github.yandex-team.ru/idm/backend/commit/44f25b472 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-05-20 20:01:47+03:00

137.52
------
 * Фикс названия миграции  [ https://github.yandex-team.ru/idm/backend/commit/a050b1c5a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-05-17 18:05:43+03:00

137.51
------
* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * Удалить старое поле                      [ https://github.yandex-team.ru/idm/backend/commit/ec4e8597b ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-17 16:57:13+03:00

137.50
------
 * IDM-7264 Исправлена опечатка в письмах (#1729)  [ https://github.yandex-team.ru/idm/backend/commit/1b19c2cb9 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-16 19:10:12+03:00

137.49
------
 * IDM-7264 Не отправлять письмо неактивным участникам групп (#1728)  [ https://github.yandex-team.ru/idm/backend/commit/3c5798754 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-16 17:51:35+03:00

137.48
------
 * IDM-7245 context manager for logging errors from Redis cache  [ https://github.yandex-team.ru/idm/backend/commit/a1ff83e ]
 * IDM-7245 в get_many возвращаем {} вместо None                 [ https://github.yandex-team.ru/idm/backend/commit/290c0bd ]
 * IDM-7245 Wrappers for set_many, get_many, delete_many         [ https://github.yandex-team.ru/idm/backend/commit/621bc9c ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-05-16 16:59:33+03:00

137.46
------
 * IDM-7260 Исправлена ошибка повторных отправок писем (#1727)  [ https://github.yandex-team.ru/idm/backend/commit/f57e572eb ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-16 10:08:03+03:00

137.45
------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7245 Обрабатываем IndexError в методах кэша, чтобы не падать, когда недоступен Redis  [ https://github.yandex-team.ru/idm/backend/commit/847d317 ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7333 Поправил syntax_error в миграции  [ https://github.yandex-team.ru/idm/backend/commit/2ab93f7 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-05-14 13:59:01+03:00

137.44
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7333 Переполняется membership_id в таблице action (#1724)  [ https://github.yandex-team.ru/idm/backend/commit/4fbb5f2 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-05-13 21:03:26+03:00

137.43
------
 * IDM-7264 Поправить рассылку писем о необходимости дорегистрировать паспортные логины (#1721)  [ https://github.yandex-team.ru/idm/backend/commit/dc6ce0950 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-13 14:27:47+03:00

137.42
------
 * IDM-6951: зафиксировать порядок локов  [ https://github.yandex-team.ru/idm/backend/commit/3fd82711e ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-05-13 11:03:36+03:00

137.41
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7260 Исправлены миграции (#1719)  [ https://github.yandex-team.ru/idm/backend/commit/553625751 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-7220: В названии тикета SOD указывать ФИ  [ https://github.yandex-team.ru/idm/backend/commit/e96b1e39a ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-08 14:31:01+03:00

137.40
------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * IDM-7245 Add polosate to specialReviewers     [ https://github.yandex-team.ru/idm/backend/commit/21f8cf0f8 ]
 * IDM-7245 Если redis таймаутится, ловим трейс  [ https://github.yandex-team.ru/idm/backend/commit/a8630df73 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7260 Рассылать письма о членствах, к которым необходимо привязать паспортный логин (#1714)  [ https://github.yandex-team.ru/idm/backend/commit/fce349aed ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * Увеличение размера id у GroupMembership  [ https://github.yandex-team.ru/idm/backend/commit/935354cce ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-05-08 13:41:48+03:00

137.39.1
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7333 Переполняется membership_id в таблице action (#1724)  [ https://github.yandex-team.ru/idm/backend/commit/f46feea ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * Увеличение размера id у GroupMembership  [ https://github.yandex-team.ru/idm/backend/commit/188bf85 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-05-13 22:43:02+03:00


137.39
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Исправил порядок миграций (#1716)  [ https://github.yandex-team.ru/idm/backend/commit/67f746446 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * releasing version 137.32.1                                                           [ https://github.yandex-team.ru/idm/backend/commit/6d2eb446d ]
 * IDM-7252: Связанные отложенные роли не отозвались после отзыва родительской (#1707)  [ https://github.yandex-team.ru/idm/backend/commit/57f1e1e7a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-05-06 16:14:36+03:00

137.38
------
 * IDM-7263 Добавление синка неконсистентностей в cron  [ https://github.yandex-team.ru/idm/backend/commit/744c580 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-04-30 15:23:24+03:00

137.37
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7263 Не пушим удаление членств с отличием в pl (#1712)  [ https://github.yandex-team.ru/idm/backend/commit/cb2e5dd ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7263 Сломались тетсы из-за конфликта с 7126  [ https://github.yandex-team.ru/idm/backend/commit/3e0b96b ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-04-29 13:22:34+03:00

137.36
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7263 Паспортные логины в синхронизации системочленств (#1710)  [ https://github.yandex-team.ru/idm/backend/commit/0dd10a5 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-04-26 11:37:40+03:00

137.35
------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-7126: Отложенный выход из группы (#1709)  [ https://github.yandex-team.ru/idm/backend/commit/a7b411e1e ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-04-25 15:21:52+03:00

137.34
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7130 Таска по сверке системочленств (#1705)  [ https://github.yandex-team.ru/idm/backend/commit/638399f ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-04-25 14:02:38+03:00

137.33
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Update .devexp.json  [ https://github.yandex-team.ru/idm/backend/commit/ad9a00c1e ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-7252: Связанные отложенные роли не отозвались после отзыва родительской (#1707)  [ https://github.yandex-team.ru/idm/backend/commit/397d87936 ]

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7261 Добавить паспортный логин в пуши системочленств (#1708)  [ https://github.yandex-team.ru/idm/backend/commit/0dc1d5441 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-04-23 14:04:14+03:00

137.32
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-7229: логировать выполнения воркфлоу (#1704)  [ https://github.yandex-team.ru/idm/backend/commit/b4464111a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-04-18 15:21:31+03:00

137.31
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7129 Не обновлялось поле updated_at (#1703)  [ https://github.yandex-team.ru/idm/backend/commit/1af177b ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-04-17 16:05:42+03:00

137.30
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7162 Фикс MultipleObjectsReturned при синхронизации (#1702)  [ https://github.yandex-team.ru/idm/backend/commit/778c50da7 ]

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7129 Таска по запушиванию системочленств (#1698)  [ https://github.yandex-team.ru/idm/backend/commit/0bb064452 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-16 17:31:09+03:00

137.29
------
 * IDM-7224 Исправлена ошибка при логировании (#1701)  [ https://github.yandex-team.ru/idm/backend/commit/e5d429d82 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-16 14:33:50+03:00

137.28
------
 * IDM-7162 Исправлен constraint в моделе GroupMembership (#1700)  [ https://github.yandex-team.ru/idm/backend/commit/03c10167a ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-15 12:01:01+03:00

137.27
------
 * IDM-7162 Исправлен SQL в миграции и синхронизации членств (#1699)  [ https://github.yandex-team.ru/idm/backend/commit/751064afb ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-12 13:32:32+03:00

137.26
------
 * IDM-7162 Переходим к использованию groupmembership везде (#1695)  [ https://github.yandex-team.ru/idm/backend/commit/ed21f94e4 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-11 12:32:40+03:00

137.25
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-6700 Логи дублей узлов в саджесте (#1696)  [ https://github.yandex-team.ru/idm/backend/commit/b26494b ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-04-10 13:26:41+03:00

137.24
------
 * IDM-7053 Не отвечать 500 при заказе роли на чужой паспортный логин (#1697)  [ https://github.yandex-team.ru/idm/backend/commit/5031f6f60 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-08 13:03:40+03:00

137.23
------
 * IDM-7039 Добавил тест на число походов в db, убрал лишний джоин  [ https://github.yandex-team.ru/idm/backend/commit/efc44b0 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-04-04 13:47:40+03:00

137.22
------
 * IDM-7182: реализация cache.add для нашей реализации кеша (#1693)  [ https://github.yandex-team.ru/idm/backend/commit/a9faad4d2 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-04-03 12:31:40+03:00

137.21
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7182: Более мягкая обработка отсутствия мастера у redis (#1692)  [ https://github.yandex-team.ru/idm/backend/commit/59fdccb7c ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7039 привел queryset в RoleNodeResource в соответствие с полями, использованными в RoleNode.parent_path  [ https://github.yandex-team.ru/idm/backend/commit/c66ea6a69 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-04-03 12:19:51+03:00

137.20
------
 * IDM-7053 Фикс миграции (#1691)  [ https://github.yandex-team.ru/idm/backend/commit/5600056fc ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-02 17:46:43+03:00

137.19
------
 * IDM-7053 Поправлен файл миграции (#1690)  [ https://github.yandex-team.ru/idm/backend/commit/d148d9d80 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-02 17:33:09+03:00

137.18
------
 * IDM-7053 Cвязь user-passportlogin привести к 1-M (#1683)  [ https://github.yandex-team.ru/idm/backend/commit/075e37727 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-02 17:05:38+03:00

137.17
------
 * IDM-7128 Регулярное разворачивание связи "система-членство" (#1685)  [ https://github.yandex-team.ru/idm/backend/commit/dc9ac1e37 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-02 13:50:18+03:00

137.16
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7161 Делаем таску по синхронизации опосредованных членств (#1687)  [ https://github.yandex-team.ru/idm/backend/commit/c792ed6f9 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * Revert "Merge pull request #1688 from idm/feature/7039"  [ https://github.yandex-team.ru/idm/backend/commit/ca06d42ca ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-02 12:15:38+03:00

137.15
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7160 Добавляем в GroupMembership колонку "непосредственное членство" (#1686)  [ https://github.yandex-team.ru/idm/backend/commit/442def3 ]

* [chirkinvf](http://staff/chirkinvf@yandex-team.ru)

 * IDM-7039: поменять выдачу в ручке v1 для RoleNodeResource  [ https://github.yandex-team.ru/idm/backend/commit/3e498b8 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-04-01 19:48:55+03:00

137.14
------
 * IDM-6638: вернул и починил redis-кеш (#1684)  [ https://github.yandex-team.ru/idm/backend/commit/94fa3cb83 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-28 16:46:10+03:00

137.13
------
 * Откат IDM-6638  [ https://github.yandex-team.ru/idm/backend/commit/a48745a71 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-27 18:50:49+03:00

137.12
------
 * IDM-6638: версия redis-py зафиксирована на 2.10.6  [ https://github.yandex-team.ru/idm/backend/commit/46c20857e ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-27 14:52:36+03:00

137.11
------
 * IDM-6638: изменение формата хостов redis  [ https://github.yandex-team.ru/idm/backend/commit/1e6025955 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-27 14:38:22+03:00

137.10
------
 * IDM-6638: теперь динамическое определение мастера redis работает во всех функциях дефолтного бекенда (#1682)  [ https://github.yandex-team.ru/idm/backend/commit/831ec658d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-27 13:52:39+03:00

137.9
-----

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-6638: поправлена зависимость  [ https://github.yandex-team.ru/idm/backend/commit/0699a7691 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7125 Добавить новую политику системы в отношении групп (#1675)  [ https://github.yandex-team.ru/idm/backend/commit/fb5491d33 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-27 12:57:03+03:00

137.8
-----
 * IDM-6638: выпилен memcached (#1680)                                     [ https://github.yandex-team.ru/idm/backend/commit/816597dde ]
 * IDM-6638: Периодически залипает кеш и дерево ролей не доезажет (#1673)  [ https://github.yandex-team.ru/idm/backend/commit/f265cc66d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-26 19:54:52+03:00

137.7
-----
 * IDM-7051 Рассылаем сообщения только при включенном флаге (#1679)  [ https://github.yandex-team.ru/idm/backend/commit/874badb84 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-03-26 14:52:12+03:00

137.6
-----
 * IDM-7051 Убраны повторяющиеся паспортные логины (#1678)  [ https://github.yandex-team.ru/idm/backend/commit/c38fac43f ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-03-26 14:14:58+03:00

137.5
-----
 * Фиксы по IDM-7050 (#1677)  [ https://github.yandex-team.ru/idm/backend/commit/d1b8b3e47 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-26 11:43:24+03:00

137.4
-----
 * IDM-7051 Рассылать письма о недорегистрированных паспортных логинах (#1674)  [ https://github.yandex-team.ru/idm/backend/commit/0b8d21039 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-03-26 10:58:33+03:00

137.3
-----

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Фиксы по IDM-7050 (#1676)  [ https://github.yandex-team.ru/idm/backend/commit/259838535 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7124 Добавить новые модели (#1672)  [ https://github.yandex-team.ru/idm/backend/commit/9d45cc849 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-25 14:41:24+03:00

137.2
-----
 * IDM-7050: теперь при отрыве старых ролей отрываются только те роли, которые можно оторвать  [ https://github.yandex-team.ru/idm/backend/commit/ea3b02742 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-22 14:01:52+03:00

137.1
---
 * IDM-6996 Рассылаем письма о необходимости привязать паспортный логин (#1671)                    [ https://github.yandex-team.ru/idm/backend/commit/f84788cf2 ]
 * IDM-7049 Регистрируем и привязываем логин к группе, если у пользователя ещё нет логина (#1666)  [ https://github.yandex-team.ru/idm/backend/commit/d9a0baffc ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-03-21 18:02:49+03:00

137
---
 * IDM-7050: прицепляемый логин теперь добавляется в fields_data (#1670)  [ https://github.yandex-team.ru/idm/backend/commit/2c16a018f ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-21 14:54:35+03:00

136
---
 * IDM-7050: поправлены не непосредственные членства (#1669)  [ https://github.yandex-team.ru/idm/backend/commit/d6d43581c ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-19 20:12:12+03:00

135
---

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7050: аттач к членству => аттач к персональным ролям (#1668)       [ https://github.yandex-team.ru/idm/backend/commit/c3ac88b8f ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-19 18:50:11+03:00

134
---

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-5284: Прошлое условие затрагивало не все кейсы родительской роли (#1653)  [ https://github.yandex-team.ru/idm/backend/commit/46c6df451 ]

[Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru) 2019-03-19 15:36:36+03:00

133
---
 * IDM-7050: починить случай с attributes=None (#1667)  [ https://github.yandex-team.ru/idm/backend/commit/5406d971b ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-19 13:14:53+03:00

132
---

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7050: Таска по допиныванию ролей в конечный статус (#1665)  [ https://github.yandex-team.ru/idm/backend/commit/1f60c0941 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * COMPUTERPROBLEM-148: Тест параметра send_sms роли (#1664)  [ https://github.yandex-team.ru/idm/backend/commit/1752971dc ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-19 12:16:17+03:00

131
-----

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7048: добавлены тесты (всё уже работает, как должно) (#1661)       [ https://github.yandex-team.ru/idm/backend/commit/ae75aad09 ]
 * IDM-7045 + IDM-7046: паспортные логины для персональных ролей (#1656)  [ https://github.yandex-team.ru/idm/backend/commit/80ddafccc ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6994: Добавил проверку regex логина (#1663)  [ https://github.yandex-team.ru/idm/backend/commit/67173c057 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-18 18:16:34+03:00

130.7
-----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6994: Добавил проверку regex логина (#1663)  [ https://github.yandex-team.ru/idm/backend/commit/58982cb93 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-18 16:39:08+03:00

130.6
-----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * Заменил сообщение на пустую строку, поменял текст сообщения (#1662)  [ https://github.yandex-team.ru/idm/backend/commit/4d3b3fa8d ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * Исправлена ошибка при попытке отправить письмо о групповой роле в статусе onhold (#1660)  [ https://github.yandex-team.ru/idm/backend/commit/b0c6f0b60 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-03-15 16:53:17+03:00

130.5
-----
 * IDM-6473 Убрал кириллицу  [ https://github.yandex-team.ru/idm/backend/commit/3e45d31 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-03-15 15:02:55+03:00

130.4
-----

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-6473 Обновил ylock (#1658)  [ https://github.yandex-team.ru/idm/backend/commit/ba7cc4c ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-03-15 13:21:40+03:00

130.3
-----
 * IDM-6994: bug fix (#1657)  [ https://github.yandex-team.ru/idm/backend/commit/cc6186945 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-03-14 22:04:55+03:00

130.2
-----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6994: Ручка от бэка, которая задаёт логин или регистрирует его (#1650)  [ https://github.yandex-team.ru/idm/backend/commit/d54491bed ]

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-5284: Прошлое условие затрагивало не все кейсы родительской роли (#1653)  [ https://github.yandex-team.ru/idm/backend/commit/0b86b3e29 ]

[Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru) 2019-03-14 13:11:15+03:00

130.1
---

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-6473: Съехать с коммунального Zookeeper (#1655)  [ https://github.yandex-team.ru/idm/backend/commit/5682f68 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-03-13 13:31:53+03:00

130
-----
 * IDM-7066: Не разрешаются неконсистентности system_has_we_dont на групповые роли (#1654)  [ https://github.yandex-team.ru/idm/backend/commit/06f10857e ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-11 13:27:07+03:00

129.1
---
 * IDM-6851 Уведомлять о скором отзыве перезапрошенной роли (#1651)  [ https://github.yandex-team.ru/idm/backend/commit/473e23daa ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-03-07 19:49:23+03:00

129
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-7044: поле типа passport логин сделано необязательным (#1652)  [ https://github.yandex-team.ru/idm/backend/commit/f14741b81 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * releasing version 128.14.1                                       [ https://github.yandex-team.ru/idm/backend/commit/e901b972a ]
 * IDM-7028 Фикс узлов, исключаемых для навешивания sid-67 (#1649)  [ https://github.yandex-team.ru/idm/backend/commit/ecb8393af ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-03-07 14:42:47+03:00

128.16
------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6991: В данные таблицы "Членства" на странице человека добавляем … (#1647)  [ https://github.yandex-team.ru/idm/backend/commit/17f635355 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-7028 Фикс узлов, исключаемых для навешивания sid-67 (#1649)  [ https://github.yandex-team.ru/idm/backend/commit/e30cb39ca ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-03-01 13:19:52+03:00

128.15
------

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-6679: При переносе ABC-сервиса не пересчитываются узлы-потомки (#1645)  [ https://github.yandex-team.ru/idm/backend/commit/43bb5a3 ]

[vladimir](http://staff/chirkinvf@yandex-team.ru) 2019-02-28 15:57:10+03:00

128.14
------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6990: начать хранить ForeignKey на passport login в модели member… (#1640)  [ https://github.yandex-team.ru/idm/backend/commit/07de6386a ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * Убрал флаг verify_ssl=0 (#1648)  [ https://github.yandex-team.ru/idm/backend/commit/e22af9cc6 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-26 17:10:33+03:00

128.13
------

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-6992: Доработать ручку с доступными для регистрации логинами, чтобы она не учитывала узел дерева  (#1644)  [ https://github.yandex-team.ru/idm/backend/commit/383b02e5e ]

[Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru) 2019-02-26 16:08:43+03:00

128.12
------
 * Исправлен dsn для Sentry (#1646)  [ https://github.yandex-team.ru/idm/backend/commit/15b7b0478 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-26 15:11:33+03:00

128.11
------
 * Не проверять сертификат при походах в Sentry (#1643)  [ https://github.yandex-team.ru/idm/backend/commit/9687bd78e ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-26 14:28:39+03:00

128.10
------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6993: Добавляем глобальную роль и permission в систему IDM (#1642)  [ https://github.yandex-team.ru/idm/backend/commit/e492aa346 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * Обновлен DSN для Sentry (#1641)  [ https://github.yandex-team.ru/idm/backend/commit/78621ef6e ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-25 15:29:38+03:00

128.9
-----

* [vladimir](http://staff/chirkinvf@yandex-team.ru)

 * IDM-6382 Добавил систему admetrica в список исключений на навешивание сида.  [ https://github.yandex-team.ru/idm/backend/commit/5bc7f65a2 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-6942 Мониторинг целостности дерева групп и команда починки таблицы groupclosure (#1637)  [ https://github.yandex-team.ru/idm/backend/commit/f548d985e ]
 * IDM-6782 Убрать поле description_formatted (#1639)                                           [ https://github.yandex-team.ru/idm/backend/commit/916b3b702 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-19 13:53:46+03:00

128.8
-----

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-6853: Отключить регулярный пересмотр для роботов  [ https://github.yandex-team.ru/idm/backend/commit/abc6aaec0 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-14 16:15:14+03:00

128.7
-----
 * Новый контейнер трендбокс              [ https://github.yandex-team.ru/idm/backend/commit/bfcb3795f ]
 * IDM-6947: увеличить размер имени узла  [ https://github.yandex-team.ru/idm/backend/commit/5442aa799 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-02-13 11:10:32+03:00

128.6
-----

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-6798: plugin.get_all_roles возвращает json где passport-login может быть None (#1634)  [ https://github.yandex-team.ru/idm/backend/commit/a9d7f7b62 ]

[Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru) 2019-02-04 16:52:34+03:00

128.5
-----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * Add reviewers (#1632)  [ https://github.yandex-team.ru/idm/backend/commit/9f97dc4db ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-6850: опечатка в автоматической рассылке Управлятора  [ https://github.yandex-team.ru/idm/backend/commit/fca373efb ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-01-29 16:38:19+03:00

128.4
-----

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-6819: Сломаны дайджесты (#1631)  [ https://github.yandex-team.ru/idm/backend/commit/924a7ba49 ]

[Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru) 2019-01-23 14:05:50+03:00

128.3
-----
 * IDM-6770: Присылаем слишком много писем про роботов их владельцам  [ https://github.yandex-team.ru/idm/backend/commit/ba8e197 ]

[vladimir](http://staff/chirkinvf@yandex-team.ru) 2019-01-10 18:25:37+03:00

128.2
-----
 * IDM-6735 Принимать параметр 'no_meta' при пагинации (#1629)  [ https://github.yandex-team.ru/idm/backend/commit/bf956c8c4 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-12-29 18:27:09+03:00

128.1
-----
 * IDM-5695: Отправлять уведомления про роли робота ответственному за него  [ https://github.yandex-team.ru/idm/backend/commit/8b0d343 ]

[vladimir](http://staff/chirkinvf@yandex-team.ru) 2018-12-29 13:34:28+03:00

128.0
-----
 * IDM-6734: Увеличить размер ошибки в action  [ https://github.yandex-team.ru/idm/backend/commit/f5f7f777b ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2018-12-27 14:28:34+03:00

127.6
-----
 * IDM-6257: Клиентский сертификат в idm requests отпинывается в nginx  [ https://github.yandex-team.ru/idm/backend/commit/470d44c ]

[vladimir](http://staff/chirkinvf@yandex-team.ru) 2018-12-24 18:57:29+03:00

127.5
-----

* [zivot](http://staff/zivot@yandex-team.ru)

 * IDM-6671: Синк юзеров ломается на отсутствующем robot_owners (#1624)  [ https://github.yandex-team.ru/idm/backend/commit/bca0fb8ca ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-6698: Добавить АппМетрику в список sid67-исключений  [ https://github.yandex-team.ru/idm/backend/commit/b970a9c30 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-12-21 22:38:36+03:00

127.4
-----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6671: Синк юзеров ломается на отсутствующем robot_owners (#1624)  [ https://github.yandex-team.ru/idm/backend/commit/745dcbf3e ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2018-12-20 21:56:49+03:00

127.3
-----

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-6646: Не открывается просмотр роли в админке  [ https://github.yandex-team.ru/idm/backend/commit/7f7efa3ed ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6531: Доработать систему прав внутри IDM (#1623)  [ https://github.yandex-team.ru/idm/backend/commit/ae207f527 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2018-12-20 13:22:59+03:00

127.2
-----

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-6528: Использовать affiliation в коде для поиска руководителей внешних пользователей  [ https://github.yandex-team.ru/idm/backend/commit/8d72fce58 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-6611: проверять узлы на публичность перед пушами в intrasearch  [ https://github.yandex-team.ru/idm/backend/commit/f1eeded24 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-12-18 19:25:21+03:00

127.1
-----

* [zivot](http://staff/zivot@yandex-team.ru)

 * IDM-6526: Начать синхронизировать признаки (#1612)  [ https://github.yandex-team.ru/idm/backend/commit/3510f1e07 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2018-12-17 15:13:58+03:00

127.0
------

* [zivot](http://staff/zivot@yandex-team.ru)

 * IDM-6527: Вытащить новые признаки как методы workflow (#1615)  [ https://github.yandex-team.ru/idm/backend/commit/7b344de ]

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-6012: Не обновляется expire_at и отзываются роли  [ https://github.yandex-team.ru/idm/backend/commit/3ece5bb ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-6631: Разрешить разработчикам IDM чинить системы  [ https://github.yandex-team.ru/idm/backend/commit/06ba42f ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-5937 Изменил тип исключения (#1618)  [ https://github.yandex-team.ru/idm/backend/commit/3c2ef76 ]

[Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru) 2018-12-14 16:24:27+03:00

126.13
------

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-6535: fix unit test                                                                                          [ https://github.yandex-team.ru/idm/backend/commit/260176def ]
 * IDM-6533: переименование свойств в миграции для совместимости                                                    [ https://github.yandex-team.ru/idm/backend/commit/941c0bff7 ]
 * IDM-6619: Добавил в файл кодировку                                                                               [ https://github.yandex-team.ru/idm/backend/commit/38d2c6b26 ]
 * IDM-6535: Убрал из меты index_together и unique_together т.к. миграция ручная. Добавил констраинт в on_conflict  [ https://github.yandex-team.ru/idm/backend/commit/b09f55f02 ]
 * IDM-6533: Миграция                                                                                               [ https://github.yandex-team.ru/idm/backend/commit/1a00cf8c5 ]
 * IDM-6533: переименование свойств в миграции для совместимости                                                    [ https://github.yandex-team.ru/idm/backend/commit/422993666 ]

* [Vladimir Chirkin](http://staff/chirkinvf@yandex-team.ru)

 * IDM-6619: поменять char-field на text-field  [ https://github.yandex-team.ru/idm/backend/commit/a7908d136 ]

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-6534: Удалить лишних ответствтенных из базы. Перевесить экшены смёржить экшены (#1608)  [ https://github.yandex-team.ru/idm/backend/commit/ac85e917a ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2018-12-14 14:24:23+03:00

126.11
-----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6529 Начать синкать пользователей через v3  [ https://github.yandex-team.ru/idm/backend/commit/fbe6f8bde ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-6505 Обработка неконсистентностей с node=None (#1597)  [ https://github.yandex-team.ru/idm/backend/commit/41147e5cc ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2018-12-10 20:51:58+03:00

126.8
-----
 * IDM-6515: atomic теперь определяем по profile_type  [ https://github.yandex-team.ru/idm/backend/commit/72828e53a ]
 * IDM-6515: на слейвы теперь ходим без atomic         [ https://github.yandex-team.ru/idm/backend/commit/4f3c4bd3e ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-12-04 19:30:56+03:00

126.7
-----
 * IDM-6515: поправлен вызов родительского конструктора                                 [ https://github.yandex-team.ru/idm/backend/commit/3912b4e77 ]
 * IDM-6515: зафиксировано название idm-ного хендлера                                   [ https://github.yandex-team.ru/idm/backend/commit/db6aeba92 ]
 * IDM-6515: убрана ненужная переменная                                                 [ https://github.yandex-team.ru/idm/backend/commit/8b367c1d0 ]
 * IDM-6515: теперь батч-процессор наследуется от нормального хендлера                  [ https://github.yandex-team.ru/idm/backend/commit/1efb1fd31 ]
 * IDM-6515: добавлено восстановление оригинальных middleware после выполнения запроса  [ https://github.yandex-team.ru/idm/backend/commit/322d7ad0d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-12-04 16:22:16+03:00

126.6
-----
 * IDM-6515: добавлен флаг, проверяющий, что мы попали в IdmReplicationMiddleware  [ https://github.yandex-team.ru/idm/backend/commit/3ee9c1fd4 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-12-03 19:13:25+03:00

126.5
-----

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-6523: Выводить подробности ошибки отзыва ролей через API  [ https://github.yandex-team.ru/idm/backend/commit/fc9b1dd56 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-6515: поправлено логирование non_atomic_requests  [ https://github.yandex-team.ru/idm/backend/commit/88cba1594 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-12-03 15:47:29+03:00

126.4
-----

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-6508: Обновил конфиг ревьюшницы  [ https://github.yandex-team.ru/idm/backend/commit/87c28a74b ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-6515: добавлены кишочки routers                       [ https://github.yandex-team.ru/idm/backend/commit/7884cb581 ]
 * Парочка правок для записи в Sentry                        [ https://github.yandex-team.ru/idm/backend/commit/bb3939740 ]
 * IDM-6515: поправлено логирование через tools_log_context  [ https://github.yandex-team.ru/idm/backend/commit/dbf188cea ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-12-03 15:27:01+03:00

126.3
-----
 * IDM-6515: зачинили Sentry для batch-запросов                                                       [ https://github.yandex-team.ru/idm/backend/commit/ef0fca622 ]
 * IDM-6515: добавлено обнуление forced_state, улучшено логирование через Sentry и tools_log_context  [ https://github.yandex-team.ru/idm/backend/commit/cc3d64994 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-30 18:38:27+03:00

126.2
-----

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-6508: Пофиксил конфиг ревьюшницы             [ https://github.yandex-team.ru/idm/backend/commit/57ebd11da ]
 * IDM-6508: Сквозное ревью + уведомления по почте  [ https://github.yandex-team.ru/idm/backend/commit/45c8d844b ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6343 Переименовал миграцию  [ https://github.yandex-team.ru/idm/backend/commit/304360b61 ]
 * IDM-6525 Добавить поля в модель пользователя (#1595)                [ https://github.yandex-team.ru/idm/backend/commit/0b5b02e82 ]
 * IDM-6530 Переименовать is-robot в is-idm-robot во всём IDM (#1593)  [ https://github.yandex-team.ru/idm/backend/commit/7505b0cbd ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2018-11-30 13:31:02+03:00

126.1
-----
 * IDM-6343: транзакции вставлены только в пару отдельных переходов  [ https://github.yandex-team.ru/idm/backend/commit/683e03c75 ]
 * IDM-6343: все шаги допинывалки завёрнуты в atomic                 [ https://github.yandex-team.ru/idm/backend/commit/b8e29d9f8 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-23 16:34:27+03:00

126.0
------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6343 Реализовать механизм продвижения по статусам  [ https://github.yandex-team.ru/idm/backend/commit/d1eefdae7 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-6343: новая таска зарегистрирована в celery                                                                                         [ https://github.yandex-team.ru/idm/backend/commit/7de68c8e6 ]
 * IDM-6343: теперь случай is_modified=False в compare() логируется                                                                        [ https://github.yandex-team.ru/idm/backend/commit/9d4e245df ]
 * IDM-6343: теперь во всех местах вместо прямого запуска допинывалки запускается неблокирующая таска                                      [ https://github.yandex-team.ru/idm/backend/commit/b7c8abbdd ]
 * IDM-6343: обновляем level при перемещении узла, поправлены тесты                                                                        [ https://github.yandex-team.ru/idm/backend/commit/b8621820b ]
 * IDM-6343: теперь для PUT допинывалка запускается только после (возможного) перемещения узла                                             [ https://github.yandex-team.ru/idm/backend/commit/f2c475e0d ]
 * IDM-6343: в некоторые тесты добавлен запуск допинывалки                                                                                 [ https://github.yandex-team.ru/idm/backend/commit/dc71ef554 ]
 * IDM-6343: поправлен PUT, поправлено определение потомков в допинывалке, убран лок при допинывании после запроса, скорректированы тесты  [ https://github.yandex-team.ru/idm/backend/commit/390a1c4cf ]
 * IDM-6343: добавлены вызовы допинывалки в некоторых тестах                                                                               [ https://github.yandex-team.ru/idm/backend/commit/5febfa73a ]
 * IDM-6343: удалён in-place перепрогон workflow при переносе узла                                                                         [ https://github.yandex-team.ru/idm/backend/commit/e99a296b5 ]
 * IDM-6343: проверка на переименование теперь производится внутри ModificationItem                                                        [ https://github.yandex-team.ru/idm/backend/commit/b81dbf3ae ]
 * IDM-6343: поправлено создание объекта очереди                                                                                           [ https://github.yandex-team.ru/idm/backend/commit/2b394e297 ]
 * IDM-6343: убрана ломающая всё ненужная строчка                                                                                          [ https://github.yandex-team.ru/idm/backend/commit/f923f1b9b ]
 * IDM-6343: поправлена работа с пушами в интрапоиск                                                                                       [ https://github.yandex-team.ru/idm/backend/commit/d836dbf73 ]
 * Поправлено прокидывание системы в очередь, добавлены select for update в pipeline                                                       [ https://github.yandex-team.ru/idm/backend/commit/ce2ba68e9 ]
 * IDM-6343: удалена таска RecalculateChildrenTask                                                                                         [ https://github.yandex-team.ru/idm/backend/commit/6ce6a2b38 ]
 * IDM-6343: поправлены TODO, удалены специфичные методы для разных статусов                                                               [ https://github.yandex-team.ru/idm/backend/commit/8c7fe8577 ]
 * IDM-6343: пара мелких правок, TODOшки для исследования                                                                                  [ https://github.yandex-team.ru/idm/backend/commit/473134f13 ]
 * IDM-6343: поправлен pipeline                                                                                                            [ https://github.yandex-team.ru/idm/backend/commit/d69f9447b ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-11-22 22:18:06+03:00

125.13
------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6071 Графики размера очереди добавления/удаления узлов в Intrasearch  [ https://github.yandex-team.ru/idm/backend/commit/424ec4af3 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-11-22 13:30:11+03:00

125.12
------
 * IDM-6475 Обрабатывать исключение в groupify  [ https://github.yandex-team.ru/idm/backend/commit/2a534a4f3 ]
 * IDM-6478 Обновить django_pgaas. (#1589)      [ https://github.yandex-team.ru/idm/backend/commit/9690fe7a4 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-11-21 15:50:46+03:00

125.11
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-6431 Отправлять еженедельные дайджесты всем, если система не использует приоритеты           [ https://github.yandex-team.ru/idm/backend/commit/1404a6def ]
 * Правки по ревью                                                                                  [ https://github.yandex-team.ru/idm/backend/commit/565a6a273 ]
 * Правки по ревью                                                                                  [ https://github.yandex-team.ru/idm/backend/commit/5043f1a79 ]
 * IDM-6430 Все запросы отображаем в числе запросов в шапке Все запросы отдаём по фильтру основной  [ https://github.yandex-team.ru/idm/backend/commit/5032367d0 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-11-19 21:24:34+03:00

125.10
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * Исправлены тесты для postgres Исправлен пагинатор                       [ https://github.yandex-team.ru/idm/backend/commit/eb5b51921 ]
 * Тесты IDM на postgresql                                                 [ https://github.yandex-team.ru/idm/backend/commit/789011049 ]
 * Откатил директорию, добавил директорию в volumes                        [ https://github.yandex-team.ru/idm/backend/commit/f706acf21 ]
 * IDM-6429 проставить использующим приоритеты системам флаг при миграции  [ https://github.yandex-team.ru/idm/backend/commit/b26ca05e0 ]
 * Поправил директорию                                                     [ https://github.yandex-team.ru/idm/backend/commit/3c19a5cff ]
 * Повторно изменил дирректорию отчета                                     [ https://github.yandex-team.ru/idm/backend/commit/7b0aeb7fa ]
 * Изменил директорию, из которой публикуется отчет                        [ https://github.yandex-team.ru/idm/backend/commit/911a9a644 ]
 * Добавить pytest-html                                                    [ https://github.yandex-team.ru/idm/backend/commit/df4197642 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-6440: Не отзываются связанные роли у уволенного сотрудника  [ https://github.yandex-team.ru/idm/backend/commit/28d1a8646 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Поправлена сборка образа в .trendbox.yml        [ https://github.yandex-team.ru/idm/backend/commit/43e788ac8 ]
 * Выпилены порты из docker-compose.yml            [ https://github.yandex-team.ru/idm/backend/commit/f008acf41 ]
 * Использован старый локальный конфиг датасорсов  [ https://github.yandex-team.ru/idm/backend/commit/2589ee044 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-19 15:05:35+03:00

125.9
-----
 * IDM-6442: в два раза увеличено количество воркеров для очереди sync_big                         [ https://github.yandex-team.ru/idm/backend/commit/11d4d6703 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-12 16:44:43+03:00

125.8
-----

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-6392: Устранение коллизии с 0148 миграцией                [ https://github.yandex-team.ru/idm/backend/commit/424156bda ]
 * IDM-6392: + поле "использовать приоритеты" и ручная миграция  [ https://github.yandex-team.ru/idm/backend/commit/372c8ee69 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-6342 Добавить дополнительные поля в модели  [ https://github.yandex-team.ru/idm/backend/commit/c3e0dc68c ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2018-11-09 17:31:36+03:00

125.7
-----
 * IDM-6339 Ускорить select.  [ https://github.yandex-team.ru/idm/backend/commit/2c5499a5c ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-11-07 21:26:08+03:00

125.6
-----
 * Добавлена переменная окружения C_FORCE_ROOT  [ https://github.yandex-team.ru/idm/backend/commit/d4a416359 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-06 17:55:20+03:00

125.5
-----
 * Specify uwsgi-stats socket location  [ https://github.yandex-team.ru/idm/backend/commit/a30232d5d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-06 17:28:50+03:00

125.4
-----

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-6393: Подключаю ревьюшницу для IDM  [ https://github.yandex-team.ru/idm/backend/commit/f1ec417d1 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-6413: www-data -> root, поправлен test_crontab, перенесены команды в cron-e  [ https://github.yandex-team.ru/idm/backend/commit/184839a77 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-06 16:18:47+03:00

125.3
-----

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * IDM-6288: Интеграция Вики и IDM  [ https://github.yandex-team.ru/idm/backend/commit/9e341d39b ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2018-11-02 21:02:36+03:00

125.2
-----
 * IDM-6413: перенёс все dev-зависимости на этап сборки  [ https://github.yandex-team.ru/idm/backend/commit/600cc8ecb ]
 * IDM-6413: добавлен uwsgi-stats и uwsgitop             [ https://github.yandex-team.ru/idm/backend/commit/e75004228 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-02 19:07:24+03:00

125.1
-----
 * IDM-6386: учитывать UWSGI_WORKERS  [ https://github.yandex-team.ru/idm/backend/commit/1c55d3c8b ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-01 16:36:59+03:00

125.0
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-6312 Добавить поле описания системы для саджеста.  [ https://github.yandex-team.ru/idm/backend/commit/fcb3c7b9d ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-10-24 15:09:37+03:00

124.20
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-6311: Отдавать 404 вместо 400, если у узла нет parent  [ https://github.yandex-team.ru/idm/backend/commit/fab742d66 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-10-18 13:39:11+03:00

124.19
------
 * feature/IDM-6277_fix_final_flag  [ https://github.yandex-team.ru/idm/backend/commit/139f7e0e7 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-16 20:42:07+03:00

124.18
------
 * IDM-5658: Пагинация по id > X  [ https://github.yandex-team.ru/idm/backend/commit/ee3ffff28 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-10-16 17:26:27+03:00

124.17
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-6016 Неконсистентность после отзыва роли. (#1550)  [ https://github.yandex-team.ru/idm/backend/commit/e84b947d2 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-16 16:11:10+03:00

124.16
------
 * Увеличить API_V1_LOGS_DELAY                                                           [ https://github.yandex-team.ru/idm/backend/commit/360c9b8a4 ]
 * feature/IDM-6278: Добавил TASK_NAME, переписал populate_data                          [ https://github.yandex-team.ru/idm/backend/commit/8caacff13 ]
 * feature/IDM-6278: Динамический график перцентилей времени ответа batch ручки          [ https://github.yandex-team.ru/idm/backend/commit/ff1d9e0ee ]
 * feature/IDM-6277: TASK_NAME для логов                                                 [ https://github.yandex-team.ru/idm/backend/commit/b2ed51cb9 ]
 * feature/IDM-6277: Убрал ненужные if, pass                                             [ https://github.yandex-team.ru/idm/backend/commit/b0665ec71 ]
 * feature/IDM-6277: Убрал дублирование                                                  [ https://github.yandex-team.ru/idm/backend/commit/1ca47a3d4 ]
 * feature/IDM-6277: График количества хороших/плохих ответов для batch от cauth робота  [ https://github.yandex-team.ru/idm/backend/commit/58feccba2 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-16 13:23:17+03:00

124.15
------
 * IDM-6296: Ручка списка систем стала медленно отвечать  [ https://github.yandex-team.ru/idm/backend/commit/2fd923ea3 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-15 20:00:29+03:00

124.14
------
 * IDM-6165: уменьшить количество систем на каждом графике  [ https://github.yandex-team.ru/idm/backend/commit/7d57ed2b5 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-15 10:59:39+03:00

124.13
------
 * Исправлен тип значения IDM_OLD_BATCH_USERS  [ https://github.yandex-team.ru/idm/backend/commit/58efd84da ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-12 19:45:32+03:00

124.12
------
 * fix/add_missing_requirement  [ https://github.yandex-team.ru/idm/backend/commit/2985f66a8 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-12 18:13:06+03:00

124.11
------
 * fix/rename_base_classes  [ https://github.yandex-team.ru/idm/backend/commit/f15c5d738 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-12 16:12:01+03:00

124.10
------
 * feature/IDM-6229_command_names: Переименовал команды  [ https://github.yandex-team.ru/idm/backend/commit/a0f9608f0 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-12 15:37:07+03:00

124.9
-----
 * feature/IDM-6272_return_cursor  [ https://github.yandex-team.ru/idm/backend/commit/8faa0ab1f ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-12 14:54:26+03:00

124.8
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-6165: больше графиков  [ https://github.yandex-team.ru/idm/backend/commit/3398e2119 ]

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * feature/IDM-6229: Переименовал настройку                                                 [ https://github.yandex-team.ru/idm/backend/commit/3d755e473 ]
 * feature/IDM-6229: Перенес файлы, добавил cron в uwsgi.ini                                [ https://github.yandex-team.ru/idm/backend/commit/bd22d0e87 ]
 * IDM-6229: Перевыпустил токен, добавил обработку исключении                               [ https://github.yandex-team.ru/idm/backend/commit/ed250d10a ]
 * Динамические графики api/v1                                                              [ https://github.yandex-team.ru/idm/backend/commit/4f37f5449 ]
 * feature/IDM-6272: Рабочее логирование подзапросов batch ручки через кастомный заголовок  [ https://github.yandex-team.ru/idm/backend/commit/44feb68b6 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-12 14:28:09+03:00

124.7
-----
 * feature/6272: убрал cursor  [ https://github.yandex-team.ru/idm/backend/commit/b9c890843 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-11 20:32:23+03:00

124.6
-----
 * feature/IDM-6272: Поправил путь до provider  [ https://github.yandex-team.ru/idm/backend/commit/b67892ae4 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-11 17:13:56+03:00

124.5
-----
 * IDM-6266: проставлять приоритет, если у всех notify=False  [ https://github.yandex-team.ru/idm/backend/commit/678db7c08 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-11 16:19:21+03:00

124.4
-----
 * feature/IDM-6272: Перенес настройку, добавил логирование    [ https://github.yandex-team.ru/idm/backend/commit/cfa2bdb05 ]
 * feature/IDM-6272: Заголовок для подзапросов                 [ https://github.yandex-team.ru/idm/backend/commit/07fd714f0 ]
 * feature/IDM-6272: логирование post json body и status_code  [ https://github.yandex-team.ru/idm/backend/commit/2b016089b ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-11 14:21:57+03:00

124.3
-----
 * IDM-6183 Ускорить пагинацию при выдаче ролей в API IDM. (#1545)  [ https://github.yandex-team.ru/idm/backend/commit/fd9f21f94 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-10-10 14:58:08+03:00

124.2
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-6015: запускать тесты в трендбоксе  [ https://github.yandex-team.ru/idm/backend/commit/c885fa6d3 ]
 * IDM-6253: удалить токены из коды        [ https://github.yandex-team.ru/idm/backend/commit/a23e85fb0 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-5483 Фикс ручки status, константа OLD_BATCH_USERS, тесты  [ https://github.yandex-team.ru/idm/backend/commit/062469436 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5494: Переписал логику подлиннее, но с комментариями, добавил логов      [ https://github.yandex-team.ru/idm/backend/commit/418bfb499 ]
 * IDM-5494: Перенёс ручку статуса в v1 api                                     [ https://github.yandex-team.ru/idm/backend/commit/0610d3072 ]
 * IDM-5494: Удалил хак с middleware, т.к. этой middleware теперь нет в списке  [ https://github.yandex-team.ru/idm/backend/commit/8535f554b ]
 * IDM-5494: усечённый набор миддлварей для подзапросов, флаг tolerate_4xx      [ https://github.yandex-team.ru/idm/backend/commit/6da373534 ]
 * IDM-5494: Распилил батч-ресурс на модули                                     [ https://github.yandex-team.ru/idm/backend/commit/b4077e44c ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5494: из батч-запросов удалена replicated-миддлварь                                                   [ https://github.yandex-team.ru/idm/backend/commit/0e8ceb97c ]
 * IDM-5494: правки batch-ручки и тестов для корректного отката транзакции по флагу                          [ https://github.yandex-team.ru/idm/backend/commit/778bfea5a ]
 * IDM-5494: теперь пятисотящая ручка может отдавать другие статусы и обновлять timestamp произвольной роли  [ https://github.yandex-team.ru/idm/backend/commit/f3d956b68 ]
 * IDM-5494: поправлено привязывание существующих паспортных логинов к новым пользователям                   [ https://github.yandex-team.ru/idm/backend/commit/8e0c9482c ]
 * IDM-5494: в тестовый api добавлена пятисотящая ручка                                                      [ https://github.yandex-team.ru/idm/backend/commit/d1337fc5b ]
 * IDM-5506: добавлен флаг rollback_on_4xx, написан тест                                                     [ https://github.yandex-team.ru/idm/backend/commit/5e92d5ab1 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-10 12:22:52+03:00

124.1
-----
 * IDM-5985 Выпилить поля responsibles и team из ручки /api/frontend/systems/<name>.  [ https://github.yandex-team.ru/idm/backend/commit/c5c5f9c49 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-10-08 13:55:02+03:00

124.0
------
 * IDM-6249: фикс пермишнов на подтверждение роли  [ https://github.yandex-team.ru/idm/backend/commit/2eb2ab97e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-04 15:45:42+03:00

123.15
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-6165: нельзя начинать название метрики с цифры  [ https://github.yandex-team.ru/idm/backend/commit/bde50781d ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-6220: добавлено автоподтверждение ролей при переносе указанных в админке пользователей  [ https://github.yandex-team.ru/idm/backend/commit/c216709da ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-01 18:18:03+03:00

123.14
------
 * IDM-6165: нельзя начинать название метрики с цифры  [ https://github.yandex-team.ru/idm/backend/commit/541f40ab3 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-01 18:07:27+03:00

123.13
------
 * IDM-6165: replace('-', '_')  [ https://github.yandex-team.ru/idm/backend/commit/3a15ea4ee ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-01 15:44:55+03:00

123.12
------
 * Revert "IDM-5985 Выпилить поля responsibles и team из ручки /api/frontend/systems/<name>."  [ https://github.yandex-team.ru/idm/backend/commit/d0ab601c8 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-01 15:28:15+03:00

123.11
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-6165: пушить нули  [ https://github.yandex-team.ru/idm/backend/commit/1421c25c5 ]

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * feature/IDM-5466: Добавил log.info                              [ https://github.yandex-team.ru/idm/backend/commit/a80b7cc92 ]
 * feature/IDM-5466: Лок для каждого stage в poke hanging roles    [ https://github.yandex-team.ru/idm/backend/commit/d343741bb ]
 * feature/IDM-4772: if to elif                                    [ https://github.yandex-team.ru/idm/backend/commit/f7b52ecce ]
 * feature/IDM-4772: Поправил сообщение об ошибке и починил тесты  [ https://github.yandex-team.ru/idm/backend/commit/317648baf ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-6218: поправлено создание логина в паспорте  [ https://github.yandex-team.ru/idm/backend/commit/574c6cc3e ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-01 13:34:58+03:00

123.10
------
 * IDM-6165: график отморозки  [ https://github.yandex-team.ru/idm/backend/commit/d030b4bf4 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-09-27 17:48:49+03:00

123.9
-----
 * IDM-6065: проигнорированные запросы делать обработанными  [ https://github.yandex-team.ru/idm/backend/commit/4c9ac591b ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-09-27 16:07:36+03:00

123.8
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-6065: проигнорированные запросы делать обработанными  [ https://github.yandex-team.ru/idm/backend/commit/a18764f18 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-5985 Выпилить поля responsibles и team из ручки /api/frontend/systems/<name>.       [ https://github.yandex-team.ru/idm/backend/commit/5fc282381 ]
 * IDM-5215 Ломается воркфлоу с system.all_users_with_role при сохранении узла в админке.  [ https://github.yandex-team.ru/idm/backend/commit/761fb37b8 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-09-27 15:48:19+03:00

123.7
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-6025: ручка обработки отморозки (#1530)  [ https://github.yandex-team.ru/idm/backend/commit/5b0f3e0c5 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Удалены отозванные токены из настроек  [ https://github.yandex-team.ru/idm/backend/commit/d46a022d9 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-09-27 14:05:49+03:00

123.6
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-6164: Пересматривать приоритет при отморозке (#1525)  [ https://github.yandex-team.ru/idm/backend/commit/944d793ff ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-6209: поправлен порядок взятия блокировок, добавлены транзакции  [ https://github.yandex-team.ru/idm/backend/commit/ad398b9a5 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-26 17:53:26+03:00

123.5
-----
 * IDM-6026: добавить в ApproveRequest возможность отморозки (#1524)  [ https://github.yandex-team.ru/idm/backend/commit/4eb3a38c9 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-09-24 16:58:46+03:00

123.4
-----
 * Поправлен порядок обновления пользователей, полученных из staff-api  [ https://github.yandex-team.ru/idm/backend/commit/aae59bcc1 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-24 16:39:18+03:00

123.3
-----
 * IDM-6143: добавлен тест на это                                         [ https://github.yandex-team.ru/idm/backend/commit/070997e4e ]
 * IDM-6143: поправлен перепросчёт приоритетов в случае перезапроса роли  [ https://github.yandex-team.ru/idm/backend/commit/e92db72ee ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-24 15:47:19+03:00

123.2
-----

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-4261 Перезапрос роли не учитывает, что набор полей мог измениться.  [ https://github.yandex-team.ru/idm/backend/commit/27708f70e ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5403: Пустое сообщение при ForbiddenError  [ https://github.yandex-team.ru/idm/backend/commit/d12651aee ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-09-24 14:51:12+03:00

123.1
-----
 * Узлы тестовой метрики убраны из списка узлов, на которые не вешается sid67 (система выключена)  [ https://github.yandex-team.ru/idm/backend/commit/af381f21d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-21 17:05:24+03:00

123.0
------

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * IDM-4860: возвращать ошибку workflow, если узел не существует.  [ https://github.yandex-team.ru/idm/backend/commit/57e787e50 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-09-21 14:33:06+03:00

122.16
------

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * releasing version 122.15  [ https://github.yandex-team.ru/idm/backend/commit/3b1d2a275 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-6144: добавлены тесты на login.is_subscribable                                         [ https://github.yandex-team.ru/idm/backend/commit/9b78a8df1 ]
 * IDM-6144: поправлен баг с созданием нового логина (некорректная проверка на уникальность)  [ https://github.yandex-team.ru/idm/backend/commit/c5707c39c ]
 * IDM-6144: поправлена запись в базу статуса логина                                          [ https://github.yandex-team.ru/idm/backend/commit/3450bdaa3 ]
 * IDM-6144: добавлены тесты                                                                  [ https://github.yandex-team.ru/idm/backend/commit/37035b087 ]
 * IDM-6144: актуализированы to_subscribe и to_unsubscribe в кверисете                        [ https://github.yandex-team.ru/idm/backend/commit/a65069096 ]
 * IDM-6144: добавлены проверки на узлы при выдаче роли                                       [ https://github.yandex-team.ru/idm/backend/commit/b76399484 ]
 * IDM-6144: поправлен баг с фильтрацией допустимых систем                                    [ https://github.yandex-team.ru/idm/backend/commit/1c5f533a1 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-18 16:47:49+03:00

122.15
------
 * feature/tvm_new_version: Поменял exception для TVM             [ https://github.yandex-team.ru/idm/backend/commit/ab42c6518 ]
 * feature/IDM-6134: Удаление синка департаментов                 [ https://github.yandex-team.ru/idm/backend/commit/bfafa36ed ]
 * feature/IDM-6070: Добавил request_log_context в batch запросы  [ https://github.yandex-team.ru/idm/backend/commit/bbd563701 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-09-14 19:18:18+03:00

122.14
------
 * IDM-6135: Апнул версию django_tools_log_context  [ https://github.yandex-team.ru/idm/backend/commit/2c312b56f ]
 * IDM-6135: 500 в админке IDM в тестинге           [ https://github.yandex-team.ru/idm/backend/commit/2684e092a ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2018-09-10 22:22:54+03:00

122.13
------

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * feature/IDM-6070: Обновил django_tools_log_context  [ https://github.yandex-team.ru/idm/backend/commit/e2c5b1a48 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-09-07 20:18:22+03:00

122.12
------
 * IDM-6125: IDM неправильно определяет присутствие  [ https://github.yandex-team.ru/idm/backend/commit/9f066465d ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-09-07 18:04:00+03:00

122.11
------
 * IDM-6066: новая ручка newhire  [ https://github.yandex-team.ru/idm/backend/commit/d0da47183 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-09-07 13:34:24+03:00

122.10
------
 * Revert "Merge pull request #1476 from idm/feature/5581-2"   [ https://github.yandex-team.ru/idm/backend/commit/94ffa976d ]
 * Revert "Merge pull request #1502 from idm/bugfix/IDM-6054"  [ https://github.yandex-team.ru/idm/backend/commit/5971564bc ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-09-03 21:07:23+03:00

122.9
-----

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * feature/IDM-5971: Добавил дату пересчета основного приоритета     [ https://github.yandex-team.ru/idm/backend/commit/8624968dc ]
 * feature/IDM-5872: Изменил фильтры по статусам для approverequest  [ https://github.yandex-team.ru/idm/backend/commit/dd136b074 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-09-03 20:24:16+03:00

122.8
-----
 * feature/IDM-6076: Убрал системы abc-типа, поправил тесты                                                     [ https://github.yandex-team.ru/idm/backend/commit/a270c12a8 ]
 * IDM-6076: Рассылка уведомлений апруверам основного приоритета                                                [ https://github.yandex-team.ru/idm/backend/commit/567395247 ]
 * IDM-5869: Отправка уведомлений основным апруверам при созданий новой роли. Убрал check_gaps. Поправил тесты  [ https://github.yandex-team.ru/idm/backend/commit/1365dde76 ]
 * IDM-5969: Мониторинг для ошибок синхронизации                                                                [ https://github.yandex-team.ru/idm/backend/commit/00d9fa0da ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-08-31 20:57:59+03:00

122.7
-----

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * IDM-5971: Пересчет основного приоритета и отправка письма при смене основного приоритета  [ https://github.yandex-team.ru/idm/backend/commit/29bd80bb1 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5970: Увеличил таймаут, добавил проверку на не 200 и авторизацию по токену  [ https://github.yandex-team.ru/idm/backend/commit/7e060ebcd ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-08-31 18:14:41+03:00

122.6
-----

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * IDM-6084: Изменил repr у Approver, AnyApprover. Добавил метод для отображения у ApproveRequest  [ https://github.yandex-team.ru/idm/backend/commit/ea35d382a ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-08-31 14:13:18+03:00

122.5
-----

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * IDM-5872: Фильтры по role_id, статусу и приоритету                                                           [ https://github.yandex-team.ru/idm/backend/commit/9a40d75a9 ]
 * IDM-5869: Отправка уведомлений основным апруверам при созданий новой роли. Убрал check_gaps. Поправил тесты  [ https://github.yandex-team.ru/idm/backend/commit/1b9d40991 ]
 * IDM-5969: Частичные обновления для синхронизации. Убрал старую функцию для синхронизации с Гэпом.            [ https://github.yandex-team.ru/idm/backend/commit/c5fc88dd9 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5872: Статистика считается теперь только для основного приоритета  [ https://github.yandex-team.ru/idm/backend/commit/504459d46 ]
 * IDM-5872: Константы, перевод                                           [ https://github.yandex-team.ru/idm/backend/commit/3d85a534d ]
 * IDM-5872: Немного сократил код и переименовал none -> all              [ https://github.yandex-team.ru/idm/backend/commit/e614d0f05 ]
 * IDM-5869: Переименовал миграции                                        [ https://github.yandex-team.ru/idm/backend/commit/49e917aa5 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-08-30 21:27:51+03:00

122.4
-----

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * Поправил импорты                                         [ https://github.yandex-team.ru/idm/backend/commit/d41dc81b7 ]
 * feature/IDM-6077: Фильтрация пустых OR-групп в workflow  [ https://github.yandex-team.ru/idm/backend/commit/be9f02c68 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Добавить минутный countdown для RecalculateChildrenTask                                                              [ https://github.yandex-team.ru/idm/backend/commit/129ff64ae ]
 * IDM-6054: добавлен сброс хеша родителя при удалении/восстановлении, фетч корневого узла после перехеширвания дерева  [ https://github.yandex-team.ru/idm/backend/commit/9c292078b ]
 * IDM-6054: поправлен mark_active, добавлено взятие консистентного лока в mark_depriving                               [ https://github.yandex-team.ru/idm/backend/commit/bec9d7a91 ]
 * IDM-6054: уточнён порядок узлов в методе get_descendants                                                             [ https://github.yandex-team.ru/idm/backend/commit/8a5e1c097 ]
 * IDM-6054: удалить таску по обнулению хешей предков при удалении узла                                                 [ https://github.yandex-team.ru/idm/backend/commit/98ff5f319 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-08-29 21:47:36+03:00

122.3
-----
 * Merge pull request #1502 from idm/bugfix/IDM-6054  [ https://github.yandex-team.ru/idm/backend/commit/18c7ea38b ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-08-29 16:59:41+03:00

122.2
-----
 * IDM-6074: Незаполненное поле паспортного логина приводит к {'passport-login': ''}  [ https://github.yandex-team.ru/idm/backend/commit/98bb9ebc1 ]
 * IDM-5969: Поправил импорт                                                          [ https://github.yandex-team.ru/idm/backend/commit/29d6e3f1f ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-08-29 11:20:19+03:00

122.1
-----
 * IDM-5969: Синхронизация с гэпом и мониторинг (#1499)  [ https://github.yandex-team.ru/idm/backend/commit/fda534a15 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-08-28 16:45:48+03:00

122.0
------

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * IDM-5867: Добавил get_chain_of_heads для групп, убрал флаг repeat, для руководителей не учитывается их департамент                             [ https://github.yandex-team.ru/idm/backend/commit/025eb6ad8 ]
 * IDM-5867: Функция для работы с деревом руководителей и заместителей                                                                            [ https://github.yandex-team.ru/idm/backend/commit/a93b790f5 ]
 * IDM-5866: Добавил аргументы функции для any_from, approver. Сохраняю приоритеты в базу. Добавил приоритеты для UserWrapper. Добавил миграцию.  [ https://github.yandex-team.ru/idm/backend/commit/7407bf2bd ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-27 18:31:23+03:00

121.28
------
 * IDM-6048: подставлять devnull@ вместо email в тестинге  [ https://github.yandex-team.ru/idm/backend/commit/a4a0aa667 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-23 14:52:21+03:00

121.27
------
 * Возомжность управлять max_timedelta из админки  [ https://github.yandex-team.ru/idm/backend/commit/dabecb68 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-16 11:55:12+03:00

121.26
------

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5581: Перепрогонять wf для потомков при перемещении по unique_id  [ https://github.yandex-team.ru/idm/backend/commit/8a6fd6203 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5581: слайс заменён на reversed, поправлен комментарий                                                     [ https://github.yandex-team.ru/idm/backend/commit/a6068e680 ]
 * IDM-5581: поправлена связка мигание-перенос, тесты                                                             [ https://github.yandex-team.ru/idm/backend/commit/ad9d60ee0 ]
 * IDM-5581: тест на мигание узлов дерева ролей                                                                   [ https://github.yandex-team.ru/idm/backend/commit/9771e415b ]
 * IDM-5581: поправлено повторное удаление узлов и перемещение после мигания                                      [ https://github.yandex-team.ru/idm/backend/commit/f68cfb86e ]
 * IDM-5581: мелкие правки + ещё тесты                                                                            [ https://github.yandex-team.ru/idm/backend/commit/513c1ac7f ]
 * IDM-5581: убран двойной пересчёт workflow при перемещении через POST, добавлен тест на перемещение через POST  [ https://github.yandex-team.ru/idm/backend/commit/a0be0ff9f ]
 * IDM-5581: поправлены отчёты, порядок modification-move, возврат значений из push_* и много других мелочей      [ https://github.yandex-team.ru/idm/backend/commit/5c5f7dd43 ]
 * IDM-5581: поправлен перенос узла через POST с unique_id, мелкие правки по полям                                [ https://github.yandex-team.ru/idm/backend/commit/75563f6de ]
 * IDM-5581: удалён лишний логгер для тестового окружения                                                         [ https://github.yandex-team.ru/idm/backend/commit/09ece9fea ]
 * IDM-5581: поправлено перемещение потомков узлов                                                                [ https://github.yandex-team.ru/idm/backend/commit/ab89382d6 ]
 * IDM-5581: перемещение узлов реализовано через ExternalIDQueue                                                  [ https://github.yandex-team.ru/idm/backend/commit/2d72213d8 ]
 * IDM-5581: из apply удалено восстановление узлов (дублируется в compare)                                        [ https://github.yandex-team.ru/idm/backend/commit/e4cd4b0c1 ]
 * IDM-5581: переделано получение класса и external_id в очереди                                                  [ https://github.yandex-team.ru/idm/backend/commit/c10fcf3b1 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-08-15 15:02:15+03:00

121.25
------
 * IDM-5536: проверять IP пользователя в x-forwarded-for       [ https://github.yandex-team.ru/idm/backend/commit/5e990a5b ]
 * IDM-5907: отвечать 400, если у системы не прописант tvm_id  [ https://github.yandex-team.ru/idm/backend/commit/c3bc4e8a ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-15 12:59:11+03:00

121.24
------
 * IDM-5907: использовать форму                                                    [ https://github.yandex-team.ru/idm/backend/commit/d1a5c376 ]
 * IDM-5907: передавать выбранное в системе значение auth_factor в ручке саджеста  [ https://github.yandex-team.ru/idm/backend/commit/ae2ba325 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-14 17:29:50+03:00

121.23
------
 * IDM-5823: Увеличить максимальную длину сообщения об ошибке при сохранении в Action  [ https://github.yandex-team.ru/idm/backend/commit/31937a93b ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-08-14 14:44:03+03:00

121.22
------
 * IDM-5907: добавил blank=True для tvm_id        [ https://github.yandex-team.ru/idm/backend/commit/ec64df2e ]
 * IDM-5905: ходить во внутренний blackbox с TVM  [ https://github.yandex-team.ru/idm/backend/commit/e2761a60 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-14 14:06:50+03:00

121.21
------
 * IDM-5907: Ходить в системы с TVM тикетом (#1485)  [ https://github.yandex-team.ru/idm/backend/commit/861e47db ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-13 18:48:40+03:00

121.20
------
 * IDM-4885: нельзя подтвердить роль в неактивной системе  [ https://github.yandex-team.ru/idm/backend/commit/5856dde4 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-13 16:24:25+03:00

121.19
------
 * IDM-5966: мониторинг сломанных деревьев  [ https://github.yandex-team.ru/idm/backend/commit/57de12d9 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-13 12:53:22+03:00

121.18
------
 * IDM-5972: немного поменял расписание синка с Центром, чтобы полный синк успевал завершаться  [ https://github.yandex-team.ru/idm/backend/commit/7d1a07de ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-08-09 16:59:42+03:00

121.17
------
 * IDM-5972: Долгая синхронизация со Стаффом (#1484)  [ https://github.yandex-team.ru/idm/backend/commit/6292f612 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-08-09 16:27:05+03:00

121.16
------
 * IDM-5964: исправлен комментарий к тесту                   [ https://github.yandex-team.ru/idm/backend/commit/d21cb02b ]
 * IDM-5694: не использовать map                             [ https://github.yandex-team.ru/idm/backend/commit/bc580217 ]
 * IDM-5964: В мониторинге зависших ролей сумма не сходится  [ https://github.yandex-team.ru/idm/backend/commit/57cf4043 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-07 18:36:07+03:00

121.15
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Тесты теперь проходят (#1480)  [ https://github.yandex-team.ru/idm/backend/commit/ad9df0b6 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5544: Ошибка в логгировании при увольнении в тестинге                                           [ https://github.yandex-team.ru/idm/backend/commit/084deb21 ]
 * IDM-5544: Падает разрешение неконсистентности вида "в системе роль, про узел которой не знает idm"  [ https://github.yandex-team.ru/idm/backend/commit/c59ed612 ]
 * IDM-5594: Переименовать "неконсистентности" в "расхождения" на бекенде                              [ https://github.yandex-team.ru/idm/backend/commit/ed9181ea ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-185: запрет на создание узла, у чьего предка есть returnable-узлы, тесты на это  [ https://github.yandex-team.ru/idm/backend/commit/e870db52 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-03 18:12:33+03:00

121.14
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-5006: доработка команды idm_oneoff_fix_system_tree (#1479)  [ https://github.yandex-team.ru/idm/backend/commit/841d913b ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5934: сотруднику без департаментов теперь возвращается пустой список департаментов, в которых он состоит (#1477)  [ https://github.yandex-team.ru/idm/backend/commit/5ca59794 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-08-02 17:18:45+03:00

121.13
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-5801: django_log_context  [ https://github.yandex-team.ru/idm/backend/commit/1ae9f2c6 ]

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * IDM-5865: Добавил функцию для подсчета количества approverequest у ру… (#1468)  [ https://github.yandex-team.ru/idm/backend/commit/2d6a7bd6 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Поправлен конфиг uwsgi для игнора IOError                                    [ https://github.yandex-team.ru/idm/backend/commit/05035544 ]
 * В продовом окружении тоже включена многопоточная обёртка над Sentry          [ https://github.yandex-team.ru/idm/backend/commit/204e942c ]
 * Кастомная обёртка над транспортами, пропихивающая наши цепочки сертификатов  [ https://github.yandex-team.ru/idm/backend/commit/9037ad63 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-31 13:30:09+03:00

121.12
------
 * IDM-5853: доработка мониторинга  [ https://github.yandex-team.ru/idm/backend/commit/995fcf17 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-27 17:52:15+03:00

121.11
------
 * IDM-5853: более информативный мониторинг зависших ролей  [ https://github.yandex-team.ru/idm/backend/commit/53a6cc7e ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-27 15:06:27+03:00

121.10
------
 * IDM-5903: Пушить updated_at в интрасёрч при удалении узла (#1470)                         [ https://github.yandex-team.ru/idm/backend/commit/d3ef5d4bd ]
 * IDM-5900: duplicate key value violates unique constraint при запросе роли из АВС (#1471)  [ https://github.yandex-team.ru/idm/backend/commit/941ca5550 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-07-26 22:03:30+03:00

121.9
-----
 * Move to another Sentry installation  [ https://github.yandex-team.ru/idm/backend/commit/85f1cbda3 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-07-26 20:15:20+03:00

121.8
-----
 * IDM-5888: ходить в blackbox с tvm тикетом  [ https://github.yandex-team.ru/idm/backend/commit/06d438c4 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-26 13:35:46+03:00

121.7
-----
 * IDM-5843: перенес функции из settings в utils  [ https://github.yandex-team.ru/idm/backend/commit/663aab24 ]
 * IDM-5843: Ходить в PGAAS напрямую              [ https://github.yandex-team.ru/idm/backend/commit/48284766 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-26 11:10:49+03:00

121.6
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-5879: тесты на постгресе (#1465)  [ https://github.yandex-team.ru/idm/backend/commit/95ae95859 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5852: поправлено хождение в тестовую и продовую разлогинивалку (#1467)  [ https://github.yandex-team.ru/idm/backend/commit/b29d8159d ]
 * IDM-5883: раскрыты имена переменных в однострочнике (sic!)                  [ https://github.yandex-team.ru/idm/backend/commit/794b49da9 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-07-25 17:17:25+03:00

121.5
-----

* [Tamirlan Omarov](http://staff/tamirok@yandex-team.ru)

 * Added url for getting approvers by approve_id  [ https://github.yandex-team.ru/idm/backend/commit/351d80798 ]

* [zivot](http://staff/zivot@yandex-team.ru)

 * IDM-5753: Роль на доступ к /admin/oebs-conflicts/ (#1462)  [ https://github.yandex-team.ru/idm/backend/commit/63bd580d3 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5883: список внутренних переходов теперь симметричен (#1466)  [ https://github.yandex-team.ru/idm/backend/commit/16b0a50a5 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-07-24 17:58:38+03:00

121.4
-----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-5794: Дать запускать сверку ролей разработчикам IDM  [ https://github.yandex-team.ru/idm/backend/commit/cc0a856e ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5578: Пушим необходимые данные для удаления, но только их  [ https://github.yandex-team.ru/idm/backend/commit/dff55d8a ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-07-19 17:33:05+03:00

121.3
-----
 * IDM-5506: поправлен пересчёт потомков при отсутствии экшна  [ https://github.yandex-team.ru/idm/backend/commit/b4dcbd0ef ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-07-18 13:50:56+03:00

121.2
-----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-5775: В тестинге откладываются роли из-за удаления группы, но группа активна  [ https://github.yandex-team.ru/idm/backend/commit/376b8f42a ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5578: При перемещении узла пушим в интрасёрч всех потомков не в таске             [ https://github.yandex-team.ru/idm/backend/commit/76993488f ]
 * IDM-5824: Саджест пятисотит на пользователях без группы                               [ https://github.yandex-team.ru/idm/backend/commit/c5866ed7d ]
 * IDM-5765: Удалил команду синхронизации “дат из oebs” (на самом деле из Staff API v1)  [ https://github.yandex-team.ru/idm/backend/commit/f2740a682 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5833: аналогично устроена проверка прав для RoleNodeSet                          [ https://github.yandex-team.ru/idm/backend/commit/ef37bf0cb ]
 * IDM-5833: фильтровать ответственность на узлы по системе в ручках /roles и /actions  [ https://github.yandex-team.ru/idm/backend/commit/60430c5e2 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-07-17 16:13:32+03:00

121.1
-----
 * IDM-5660: новые токены директа не привязаны к IP  [ https://github.yandex-team.ru/idm/backend/commit/c4f93c9d ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-17 14:55:39+03:00

121.0
-----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-5796: добавить scope в ручку /frontend/permissions/all (#1446)              [ https://github.yandex-team.ru/idm/backend/commit/78e861ac7 ]
 * IDM-5810: добавить параметр --system в команду idm_subscribe_passport… (#1445)  [ https://github.yandex-team.ru/idm/backend/commit/94685ed6b ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5581: Поправил падающие тесты и скобки, из-за которых они падали  [ https://github.yandex-team.ru/idm/backend/commit/82a63d6f7 ]
 * IDM-4814: Карточка роли тоже должна быть быстрой                      [ https://github.yandex-team.ru/idm/backend/commit/82b3f7137 ]
 * IDM-4814: Уменьшил число отдаваемых полей                             [ https://github.yandex-team.ru/idm/backend/commit/2b6f3e9b6 ]
 * releasing version 120.18                                              [ https://github.yandex-team.ru/idm/backend/commit/2a247fe3f ]
 * releasing version 120.17                                              [ https://github.yandex-team.ru/idm/backend/commit/bb1dd32dd ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5662: Научиться перестраивать дерево по запросу (#1418)                                                                  [ https://github.yandex-team.ru/idm/backend/commit/85f796f84 ]
 * IDM-5581: добавлены тесты на перепрогон workflow при переносе через unique_id                                                [ https://github.yandex-team.ru/idm/backend/commit/56373e068 ]
 * IDM-5581: теперь при перемещении узла через unique_id перепрогоняется workflow                                               [ https://github.yandex-team.ru/idm/backend/commit/2bb236c6c ]
 * IDM-4814: Кастомная сериализация связанных ApproveRequest'ов, удалён dehydrate_for_related у UserResource, поправлены тесты  [ https://github.yandex-team.ru/idm/backend/commit/9de1bfa85 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-07-16 19:39:25+03:00

120.35
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-5796: добавить scope в ручку /frontend/permissions/all (#1446)              [ https://github.yandex-team.ru/idm/backend/commit/78e861ac ]
 * IDM-5810: добавить параметр --system в команду idm_subscribe_passport… (#1445)  [ https://github.yandex-team.ru/idm/backend/commit/94685ed6 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5581: Поправил падающие тесты и скобки, из-за которых они падали  [ https://github.yandex-team.ru/idm/backend/commit/82a63d6f ]
 * releasing version 120.18                                              [ https://github.yandex-team.ru/idm/backend/commit/2a247fe3 ]
 * releasing version 120.17                                              [ https://github.yandex-team.ru/idm/backend/commit/bb1dd32d ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5581: добавлены тесты на перепрогон workflow при переносе через unique_id   [ https://github.yandex-team.ru/idm/backend/commit/56373e06 ]
 * IDM-5581: теперь при перемещении узла через unique_id перепрогоняется workflow  [ https://github.yandex-team.ru/idm/backend/commit/2bb236c6 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-16 09:57:17+03:00

120.34
------

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-4814: Карточка роли тоже должна быть быстрой  [ https://github.yandex-team.ru/idm/backend/commit/82b3f713 ]
 * IDM-4814: Уменьшил число отдаваемых полей         [ https://github.yandex-team.ru/idm/backend/commit/2b6f3e9b ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-4814: Кастомная сериализация связанных ApproveRequest'ов, удалён dehydrate_for_related у UserResource, поправлены тесты  [ https://github.yandex-team.ru/idm/backend/commit/9de1bfa8 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-11 17:13:21+03:00

120.33
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-5797 Увеличение времени харакири для /api/testapi/  [ https://github.yandex-team.ru/idm/backend/commit/f0c29e45 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5579: Добавил новую задачу в конфиг celery  [ https://github.yandex-team.ru/idm/backend/commit/b914bc4e ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5574: аналогично доработан POST, добавлены проверки на unique_id в тестах                 [ https://github.yandex-team.ru/idm/backend/commit/1acbc4a0 ]
 * IDM-5574: отсутствующий unique_id при валидации формы теперь не превращается в пустую строку  [ https://github.yandex-team.ru/idm/backend/commit/8e777674 ]
 * IDM-5574: добавлен падающий тест                                                              [ https://github.yandex-team.ru/idm/backend/commit/826aed36 ]
 * IDM-5579: добавить перепросчёт потомков при обновлении name, name_en и при upsert'ах          [ https://github.yandex-team.ru/idm/backend/commit/f685df92 ]
 * IDM-5579: в очереди теперь не выполняется перепросчёт потомков при вызове из api              [ https://github.yandex-team.ru/idm/backend/commit/6fd2b661 ]
 * IDM-5579: простановка имён потомков при перемещении выполняется в таске                       [ https://github.yandex-team.ru/idm/backend/commit/0f347679 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-10 19:06:20+03:00

120.32
------

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5506: пересчёт потомков в rebuild_fullnames корректно проходит при создании узлов  [ https://github.yandex-team.ru/idm/backend/commit/5462be67 ]
 * IDM-5506: небольшие правки по обнаружению узла-предка и по прописыванию fullname       [ https://github.yandex-team.ru/idm/backend/commit/8c4b689f ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-10 14:13:45+03:00

120.31
------
 * IDM-5708: Исправлен test_newldap_connector                                         [ https://github.yandex-team.ru/idm/backend/commit/f1b71b7a ]
 * IDM-5708: Переводить last_request.is_done в True при переводе любой роли в onhold  [ https://github.yandex-team.ru/idm/backend/commit/e0764945 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-09 21:19:08+03:00

120.30
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-5790 Кириллическая буква i в Account.properties['cn']  [ https://github.yandex-team.ru/idm/backend/commit/d83e7ff5 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * IDM-5667: Перестать кодировать сообщения об ошибках в html  [ https://github.yandex-team.ru/idm/backend/commit/d3f1222d ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5782: поправлено восстановление сервисов при синхронизации с ABC  [ https://github.yandex-team.ru/idm/backend/commit/897a9835 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-07-09 15:51:00+03:00

120.29
------
 * Поправлены пути к настройкам datasources  [ https://github.yandex-team.ru/idm/backend/commit/75ee3a71 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-07-06 19:17:45+03:00

120.28
------

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * IDM-5766 запуск dbshell                                   [ https://github.yandex-team.ru/idm/backend/commit/60c12ec8 ]
 * IDM-5773: не пишем пароль в логи                          [ https://github.yandex-team.ru/idm/backend/commit/a55accf1 ]
 * IDM-5762: mongo в docker-compose                          [ https://github.yandex-team.ru/idm/backend/commit/8579a7a6 ]
 * IDM-5762: postgres в docker-compose                       [ https://github.yandex-team.ru/idm/backend/commit/54808041 ]
 * IDM-5762: Не запускать крон для системы qloud в тестинге  [ https://github.yandex-team.ru/idm/backend/commit/c20dcafd ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-07-06 19:06:21+03:00

120.20
------

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * releasing version 120.16  [ https://github.yandex-team.ru/idm/backend/commit/e5fd001d ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * IDM-5747: IDM: Не могу поправить Workflow                                                               [ https://github.yandex-team.ru/idm/backend/commit/8a064fe7 ]
 * IDM-5683: Отключить хождение по редиректам в диагностике при использовании requests                     [ https://github.yandex-team.ru/idm/backend/commit/73a684f2 ]
 * IDM-5726: Добавить мониторинг количества импортированных сидов                                          [ https://github.yandex-team.ru/idm/backend/commit/3d8eb9c3 ]
 * Добавил в исключения тестовую метрику                                                                   [ https://github.yandex-team.ru/idm/backend/commit/85a94c82 ]
 * Added postgresql client to dev reqs                                                                     [ https://github.yandex-team.ru/idm/backend/commit/8ff06432 ]
 * IDM-5679: Починил тесты cauth                                                                           [ https://github.yandex-team.ru/idm/backend/commit/4446915f ]
 * IDM-5679: Переписал функции workflow на использование групп                                             [ https://github.yandex-team.ru/idm/backend/commit/b9c46eee ]
 * IDM-5679: Поставил @skip тестам, которые когда-нибудь нужно починить                                    [ https://github.yandex-team.ru/idm/backend/commit/b30b8228 ]
 * IDM-5679: Переименовал в отчётах поле department в department_group                                     [ https://github.yandex-team.ru/idm/backend/commit/978384b5 ]
 * IDM-5679: Добавил в функцию groupify возможность нахождения группы по слагу                             [ https://github.yandex-team.ru/idm/backend/commit/a8d43624 ]
 * IDM-5679: Переписал саджесты на группы                                                                  [ https://github.yandex-team.ru/idm/backend/commit/c7af581e ]
 * IDM-5679: Удалил админку департаментов                                                                  [ https://github.yandex-team.ru/idm/backend/commit/8e10f0a1 ]
 * IDM-5679: Переписал вьюху сабжектов на группы                                                           [ https://github.yandex-team.ru/idm/backend/commit/2a548b4e ]
 * IDM-5679: Переписал поиск устаревших департаментов на группы                                            [ https://github.yandex-team.ru/idm/backend/commit/15ab2c11 ]
 * IDM-5679: Переписал определение мобильного номера на v3                                                 [ https://github.yandex-team.ru/idm/backend/commit/ba670a23 ]
 * IDM-5679: Переписал авторизацию при синхронизациях со Стаффом                                           [ https://github.yandex-team.ru/idm/backend/commit/c45e9d14 ]
 * IDM-5679: Удалил старый тест на неработающую функциональность вместе с этой функциональностью           [ https://github.yandex-team.ru/idm/backend/commit/95415ae8 ]
 * IDM-5678: Сломалась проверка сертификатов в собственном client-api IDM при переезде в Qloud             [ https://github.yandex-team.ru/idm/backend/commit/2fbcc85f ]
 * IDM-5677: Сломалась проверка сертификатов для _requester при переезде в Qloud                           [ https://github.yandex-team.ru/idm/backend/commit/3238a3ee ]
 * IDM-5454: First build                                                                                   [ https://github.yandex-team.ru/idm/backend/commit/c26d41fb ]
 * IDM-5454: Converted changelog                                                                           [ https://github.yandex-team.ru/idm/backend/commit/ea8b7d6a ]
 * IDM-5454: crontab is in new format now                                                                  [ https://github.yandex-team.ru/idm/backend/commit/10a7b80d ]
 * IDM-5454: Cannot use majortom anymore                                                                   [ https://github.yandex-team.ru/idm/backend/commit/3232e374 ]
 * IDM-5454: No direct tokens in testing                                                                   [ https://github.yandex-team.ru/idm/backend/commit/0664cf6c ]
 * IDM-5454: E-mail config for Qloud                                                                       [ https://github.yandex-team.ru/idm/backend/commit/3ceb7326 ]
 * IDM-5454: Logging adapted for Qloud                                                                     [ https://github.yandex-team.ru/idm/backend/commit/948ec983 ]
 * IDM-5454: No more graphite                                                                              [ https://github.yandex-team.ru/idm/backend/commit/910ebc6f ]
 * IDM-5454: LDAP fixes                                                                                    [ https://github.yandex-team.ru/idm/backend/commit/ff00a842 ]
 * IDM-5454: validator upgraded for newest visudo                                                          [ https://github.yandex-team.ru/idm/backend/commit/6606bdcc ]
 * IDM-5454: Docker                                                                                        [ https://github.yandex-team.ru/idm/backend/commit/bca0503c ]
 * IDM-5628: Небольшие правки по командам. Теперь считаем приоритетным кратчайший логин из созданных IDM.  [ https://github.yandex-team.ru/idm/backend/commit/9589d209 ]
 * IDM-5628: Переименовал миграцию, поправил сообщение                                                     [ https://github.yandex-team.ru/idm/backend/commit/0c934c39 ]
 * IDM-5506: Убрал пробелы                                                                                 [ https://github.yandex-team.ru/idm/backend/commit/8f6284fe ]
 * IDM-5506: Реорганизовал немного код                                                                     [ https://github.yandex-team.ru/idm/backend/commit/3373c5a9 ]
 * IDM-5587: Переносы строк                                                                                [ https://github.yandex-team.ru/idm/backend/commit/c1209a96 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5765: выпилена команда find_renamed_departments                                                              [ https://github.yandex-team.ru/idm/backend/commit/7328bd93 ]
 * IDM-5765: поправить проброс токена при походе в стаффовский users_dates.json                                     [ https://github.yandex-team.ru/idm/backend/commit/40f14f2f ]
 * IDM-5765: поправить проброс токена при походе в стаффовский users_dates.json                                     [ https://github.yandex-team.ru/idm/backend/commit/86411608 ]
 * IDM-5755: поменять порядок применения опций при подключении к ldap                                               [ https://github.yandex-team.ru/idm/backend/commit/409589ff ]
 * IDM-5731: подновлён конфиг для releaser                                                                          [ https://github.yandex-team.ru/idm/backend/commit/f58394bd ]
 * IDM-5731: поместить разные типы тасков в разные компоненты                                                       [ https://github.yandex-team.ru/idm/backend/commit/5e35ef18 ]
 * IDM-5516: заменить дефолтную версию celery на пропатченную                                                       [ https://github.yandex-team.ru/idm/backend/commit/bdfa70fb ]
 * IDM-5679: поправлен delete() у тестового клиента                                                                 [ https://github.yandex-team.ru/idm/backend/commit/a7a23c6f ]
 * IDM-5679: поправлены тесты на посылку sms                                                                        [ https://github.yandex-team.ru/idm/backend/commit/e6d861b8 ]
 * IDM-5679: micro заменён на nano                                                                                  [ https://github.yandex-team.ru/idm/backend/commit/e33e5452 ]
 * IDM-5679: поправлен тест на синк групп                                                                           [ https://github.yandex-team.ru/idm/backend/commit/75e586c4 ]
 * IDM-5679: тесты на хождение в свой client-api теперь прокидывают данные клиентского сертификата                  [ https://github.yandex-team.ru/idm/backend/commit/bc935787 ]
 * IDM-5679: добавил нормальный текстовый редактор в dev-сборку                                                     [ https://github.yandex-team.ru/idm/backend/commit/3bbb91f3 ]
 * IDM-5624: в тесты workflow добавлено прокидывание системы                                                        [ https://github.yandex-team.ru/idm/backend/commit/68d6dd17 ]
 * Мелкие правки, добавлена возможность копирования определённых ролей и тест на это                                [ https://github.yandex-team.ru/idm/backend/commit/bca50a3a ]
 * IDM-5628: при регистрации логинов мы проставляем флаг, что их создали именно мы                                  [ https://github.yandex-team.ru/idm/backend/commit/ac6b742d ]
 * IDM-5628: тест теперь проверяет, что мы не отправляем письма при создании ролей                                  [ https://github.yandex-team.ru/idm/backend/commit/eb2b2d72 ]
 * IDM-5628: поправлен вывод списка ролей, переименованы файлы команд и тестов                                      [ https://github.yandex-team.ru/idm/backend/commit/f8ed06b0 ]
 * IDM-5628: в команде копирования ролей поправлены баги, добавлены тесты                                           [ https://github.yandex-team.ru/idm/backend/commit/adf173d8 ]
 * IDM-5628: добавлена команда для копирования ролей в метрике                                                      [ https://github.yandex-team.ru/idm/backend/commit/96ba31b4 ]
 * IDM-5628: добавлена миграция                                                                                     [ https://github.yandex-team.ru/idm/backend/commit/fab7699f ]
 * IDM-5628: логинам в базе добавлены поля, добавлена команда для их простановки                                    [ https://github.yandex-team.ru/idm/backend/commit/c11a9547 ]
 * IDM-5506: теперь поведение определяется параметром create; поправлены тесты, добавлен тест на изменение алиасов  [ https://github.yandex-team.ru/idm/backend/commit/8d8d2636 ]
 * IDM-5506: небольшие правки в api, добавлены новые тесты на put                                                   [ https://github.yandex-team.ru/idm/backend/commit/f5ec337b ]
 * IDM-5506: put-запросы и NodeAdditionItem переделаны под создание узлов и upsert                                  [ https://github.yandex-team.ru/idm/backend/commit/3ab7b09b ]
 * IDM-5506: теперь insert_raw вызывает insert_object, а не наоборот                                                [ https://github.yandex-team.ru/idm/backend/commit/fbc47838 ]
 * IDM-5506: поправлена простановка дат, тесты теперь проверяют это                                                 [ https://github.yandex-team.ru/idm/backend/commit/06bedf43 ]
 * Добавлен миксин с upsert'ом, логика сохранения RoleNode вынесена в отдельный метод                               [ https://github.yandex-team.ru/idm/backend/commit/147ba314 ]
 * IDM-5506: в dev-зависимости добавлены ipdb и pytest-sugar                                                        [ https://github.yandex-team.ru/idm/backend/commit/429d2733 ]
 * IDM-5506: добавлено создание индексов на узлы в тестах                                                           [ https://github.yandex-team.ru/idm/backend/commit/f14c1cc5 ]
 * IDM-5624: теперь при подсчёте количества аппруверов учитываются вообщ… (#1415)                                   [ https://github.yandex-team.ru/idm/backend/commit/d456afdc ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-07-05 12:45:30+03:00
=======
120.18
------

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * Added postgresql client to dev reqs                                                            [ https://github.yandex-team.ru/idm/backend/commit/8ff06432 ]
 * IDM-5679: Починил тесты cauth                                                                  [ https://github.yandex-team.ru/idm/backend/commit/4446915f ]
 * IDM-5679: Переписал функции workflow на использование групп                                    [ https://github.yandex-team.ru/idm/backend/commit/b9c46eee ]
 * IDM-5679: Поставил @skip тестам, которые когда-нибудь нужно починить                           [ https://github.yandex-team.ru/idm/backend/commit/b30b8228 ]
 * IDM-5679: Переименовал в отчётах поле department в department_group                            [ https://github.yandex-team.ru/idm/backend/commit/978384b5 ]
 * IDM-5679: Добавил в функцию groupify возможность нахождения группы по слагу                    [ https://github.yandex-team.ru/idm/backend/commit/a8d43624 ]
 * IDM-5679: Переписал саджесты на группы                                                         [ https://github.yandex-team.ru/idm/backend/commit/c7af581e ]
 * IDM-5679: Удалил админку департаментов                                                         [ https://github.yandex-team.ru/idm/backend/commit/8e10f0a1 ]
 * IDM-5679: Переписал вьюху сабжектов на группы                                                  [ https://github.yandex-team.ru/idm/backend/commit/2a548b4e ]
 * IDM-5679: Переписал поиск устаревших департаментов на группы                                   [ https://github.yandex-team.ru/idm/backend/commit/15ab2c11 ]
 * IDM-5679: Переписал определение мобильного номера на v3                                        [ https://github.yandex-team.ru/idm/backend/commit/ba670a23 ]
 * IDM-5679: Переписал авторизацию при синхронизациях со Стаффом                                  [ https://github.yandex-team.ru/idm/backend/commit/c45e9d14 ]
 * IDM-5679: Удалил старый тест на неработающую функциональность вместе с этой функциональностью  [ https://github.yandex-team.ru/idm/backend/commit/95415ae8 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * IDM-5679: поправлен delete() у тестового клиента                                                 [ https://github.yandex-team.ru/idm/backend/commit/a7a23c6f ]
 * IDM-5679: поправлены тесты на посылку sms                                                        [ https://github.yandex-team.ru/idm/backend/commit/e6d861b8 ]
 * IDM-5679: micro заменён на nano                                                                  [ https://github.yandex-team.ru/idm/backend/commit/e33e5452 ]
 * IDM-5679: поправлен тест на синк групп                                                           [ https://github.yandex-team.ru/idm/backend/commit/75e586c4 ]
 * IDM-5679: тесты на хождение в свой client-api теперь прокидывают данные клиентского сертификата  [ https://github.yandex-team.ru/idm/backend/commit/bc935787 ]
 * IDM-5679: добавил нормальный текстовый редактор в dev-сборку                                     [ https://github.yandex-team.ru/idm/backend/commit/3bbb91f3 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-06-27 17:29:39+03:00

120.17
------
 * IDM-5678: Сломалась проверка сертификатов в собственном client-api IDM при переезде в Qloud  [ https://github.yandex-team.ru/idm/backend/commit/2fbcc85f6 ]
 * IDM-5677: Сломалась проверка сертификатов для _requester при переезде в Qloud                [ https://github.yandex-team.ru/idm/backend/commit/3238a3ee0 ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-06-21 20:27:30+03:00


120.16
------
 * IDM-5454 Docker  [ https://github.yandex-team.ru/idm/backend/commit/73745684 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2018-06-19 18:38:55+03:00

120.0
---

* first build

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2018-06-04 12:04:28+03:00


117.10
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5554: Функция SystemWrapper.all\_users\_with\_roles() требует слишком много памяти

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5542: Поправил ошибку перевода
  * IDM-5542: Поправил забытый импорт
  * IDM-5542: Добавил деталей при ошибке нарушения уникальности при перезапросе роли
  * IDM-5542: Поправил тесты, падающие из-за неверного скоупинга фикстуры
  * IDM-5552: Фильтры get\_alike должны повторять фильтры is\_unique

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-25 21:10:34

117.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-3942: Не рассылаем уведомления при отзыве задублированной роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-17 19:18:58

117.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5495: Логировать read-only

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-17 17:00:10

117.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5274: Переделал генерацию workflow
  * IDM-5274: Починил пропавшие куски админки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-15 23:40:07

117.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5048: Перевёл тест на simple систему
  * IDM-5048: Дочерние роли не требуют подтверждений

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-14 21:31:55

117.5
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5274: Выгрузка матрицы конфликтов в воркфлоу OEBS (#1393)

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-3942: Оптимизация миграций: выбираем только pk, увеличил размер пачки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-14 18:02:50

117.4
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5503: Уменьшить лимиты cgroup

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-3942: Обновление gitignore
  * IDM-3942: Мокаем gap (походы в него не были замоканы)
  * IDM-3942: Выводим самые медленные тесты
  * IDM-3942: Бросаем SystemExit (чтобы поймать места, где except Exception)
  * IDM-3942: Улучшен запрет на сетевые обращения в юнит-тестах
  * IDM-3942: Добавлено поле is\_returnable, created теперь входит в returnable
  * IDM-3942: Функции создания уникальных индексов с where
  * IDM-3942: Создаём уникальные индексы в тестах
  * IDM-3942: Можно запросить 2 одинаковые роли с 1 формы запроса
  * IDM-3942: Изменён подход к локам ролей
  * IDM-3942: Указываем статус существующих ролей тогда, когда это возможно
  * IDM-3942: Новый тест
  * IDM-3942: Для тех фикстур, где это можно сделать, повышен scope до 'session'
  * IDM-3942: Миграции

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-3942: добавлена команда для удаления дублирующихся ролей
  * IDM-3942: поправлены старые тесты
  * IDM-3942: поправлен неактуальный тест

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-14 13:04:53

117.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5489: Выключаем подпись sid67
  * IDM-5401: Перепрогонять воркфлоу в таске
  * IDM-5415: Ходить в reqwizard с wizclient=idm
  * IDM-5452: Тесты

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-03 20:53:39

117.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5462: Up django-replicated

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * Fix development config

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-04-28 16:05:38

117.1
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5481: Обернуть uwsgi в cgroup

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Revert "IDM-5468 check master is\_alive in get with 20 seconds downtime"

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-04-27 17:42:20

117.0
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5407: теперь в интрапоиск ходим через отдельную библиотеку

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5447 CharField -> SlugField
  * IDM-5452 remove node is\_public check in RoleNodeSet suggest (#1384)
  * IDM-5462 django\_replicated up
  * IDM-5468 check master is\_alive in get with 20 seconds downtime

 * [zivot](https://staff.yandex-team.ru/zivot)

  * IDM-5048: Остановить рост количества дочерних ролей в статусе "Ошибка" (#1381)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-04-25 19:58:42

116.10.1
---

  * Пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-08 19:51:43

116.10
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5503: Уменьшить лимиты cgroup

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-08 19:11:58

116.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5452 remove node is\_public check in RoleNodeSet suggest (#1384)

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5481: Обернуть uwsgi в cgroup

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-03 15:33:49

116.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Revert "IDM-5452 remove node is\_public check in RoleNodeSet suggest (#1384)"
  * Revert "IDM-5468 check master is\_alive in get with 20 seconds downtime"
  * Revert "IDM-5462 django\_replicated up"
  * IDM-5489: Выключаем подпись sid67

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-04-30 15:14:28

116.7
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5452 remove node is\_public check in RoleNodeSet suggest (#1384)
  * IDM-5462 django\_replicated up
  * IDM-5468 check master is\_alive in get with 20 seconds downtime

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-04-25 20:04:36

116.5
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5182: Поменял метод удаления для сервисов

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5412: Разрешаем расхождения для систем с inconsistency\_policy == ‘trust’

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-04-03 16:41:37

116.4
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5182: Добавил метод удаления для сервисов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-03-28 16:42:31

116.3
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5182: Уменьшил page\_size для abc-api

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-03-27 20:10:37

116.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4874: Обновил replicated до 2.5

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5182: Перейти с plan-api на abc-api v3

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-03-27 16:48:09

116.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4976: Снял django\_db, порефакторил тесты, поправил падавший тест
  * IDM-4976: Поправил pg-only тесты
  * IDM-5351: Исправил забытую команду
  * IDM-4874: В связи с обновлением django-replicated нужно откатывать транзакцию только тогда, когда она существует, а теперь её при чтении не существует
  * IDM-4933: Поправил случай, когда внутренней роли не существует
  * IDM-4874: Переписал poke-методы в atomic\_retry-безопасном стиле

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-03-07 22:25:16

116.0
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5351 new base command

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4976: Дописал и обновил django-pgaas
  * IDM-4976: Добавил ретраев по коду
  * IDM-4976: Стал ретраить все вьюхи
  * IDM-4976: Написал тестов на ретраи
  * IDM-4874: Обновить django-replicated
  * IDM-4976: Удалил следы переезда в Постгрес
  * IDM-4874: Обновить django-replicated
  * IDM-4976: replicated требует двух коннекшенов. удаляю middleware при прогоне тестов
  * IDM-4976: Очищаю кеш пермишенов в каждом тесте
  * IDM-4976: Оптимизирую создание кеша пермишенов
  * IDM-4976: Удалил старый тест
  * IDM-4976: Вернул PingException
  * IDM-4976: Попробуем reusedb
  * IDM-4976: Магия для починки тестов
  * IDM-4976: Поставил django\_db в двух файлах, где его почему-то не было
  * IDM-4976: И ещё один django\_db

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-03-06 15:01:11

115.10
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5350 No send mail for invalid fer\_role node

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-03-02 14:10:05

115.9
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5347 split DN by / and ,

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-03-01 13:49:38

115.8
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5280: Добавить настройку "не ломать систему при обнаружении неконсистентносетй"  (#1365)
  * IDM-5343: Проверка полного отчёта на отсуствие в нём неконсистентностей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-27 01:48:27

115.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5335: Использовать groupmembership вместо поля members

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-24 11:38:42

115.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Перенёс обработку перемещений в другую очередь
  * IDM-5288: Медленно работает перепрогон workflow
  * IDM-5284: Подправил конфигурацию для разработки
  * IDM-5284: Изменил зависимость на последний в официальном репо. Нужно обновить на 2.1, когда она выйдет
  * IDM-5284: Поправил конфиг для тестов
  * IDM-5284: Перепрогонять воркфлоу при перемещении узла для ролей с родительскими
  * IDM-5284: Поправил падающие тесты
  * IDM-5263: Поменял очередь и список компонент в настройках
  * IDM-5263: Изменить поведение при нахождении неконсистентности в SOX-системах
  * IDM-5263: Улучшил формат сообщения о неконсистентности
  * IDM-5263: Добавил обработку stringify
  * IDM-5291: Не отправляли письма про необходимость перезапроса
  * IDM-5291: Добавил тест на формат crontab, нашёл ещё проблем, поправил их

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-21 11:36:57

115.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5222: Сократил срок заявок, которые мы считаем активными в Наниматоре, с 14 до 7 дней в прошлом, и расширил до года в будущем.

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-07 19:42:28

115.4
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5255: добавить в cron запуск допинывалки ролей для Qloud

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Удалил переход в requested, тесты его больше не используют
  * Убедился, что менять можно только три поля: review\_at, node, system\_specific
  * IDM-5261: Превышение порога на число уволенных пользователей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-07 16:33:05

115.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5254: Добавил проверок на повторный запуск

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-05 14:49:31

115.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Фикс разрешения перемещения пользователей в celery-задаче

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-05 14:21:11

115.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Фикс разрешения перемещения пользователей в celery-задаче

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-05 12:40:23

115.0
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5209 убрал сложную проверку

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5200: Одинаково обрабатывать пустое необязательное поле при запросе через систему и через idm
  * IDM-5222: Проверка на свежесть всех статусов
  * IDM-5222: Выключил синхронизацию со Splunk до перехода на v3
  * TOOLSUP-28076: Сохраняю письма про подтверждение ролей в базу
  * IDM-5222: Переписал работу с LDAP. Разделил блокировку и перенос в Old Users
  * IDM-5222: Добавил статусы “ошибка” для добавления и удаления из AD-группы
  * IDM-5222: Поправил импорты и тесты
  * IDM-5222: Добавил тестов, поправил логгирование
  * IDM-5222: Переписал тесты ldap, создаю action только если действие случилось
  * IDM-XXXX: Разрешать перемещения в celery-тасках
  * IDM-5222: Доблокировка из любых недоблокированных состояний
  * IDM-5222: Фикс testapi

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-4933: добавлен тест на неконсистентности типа UNKNOWN\_ROLE
  * IDM-4933: теперь depriving-узлы считаются активными и не создают неконсистентность типа 'неизвестная роль'

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-02 23:16:16

114.24
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5350 No send mail for invalid fer\_role node

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-03-02 14:29:04

114.23
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5335: Использовать groupmembership вместо поля members

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-22 18:09:21

114.22
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5288: Медленно работает перепрогон workflow
  * IDM-5284: Изменил зависимость на последний в официальном репо. Нужно обновить на 2.1, когда она выйдет
  * IDM-5284: Перепрогонять воркфлоу при перемещении узла для ролей с родительскими
  * IDM-5284: Поправил падающие тесты
  * IDM-5263: Поменял очередь и список компонент в настройках
  * IDM-5263: Изменить поведение при нахождении неконсистентности в SOX-системах
  * IDM-5263: Улучшил формат сообщения о неконсистентности
  * IDM-5263: Добавил обработку stringify
  * IDM-5291: Не отправляли письма про необходимость перезапроса
  * IDM-5291: Добавил тест на формат crontab, нашёл ещё проблем, поправил их

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-21 11:47:07

114.21
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5222: Проверка на свежесть всех статусов
  * IDM-5222: Выключил синхронизацию со Splunk до перехода на v3
  * TOOLSUP-28076: Сохраняю письма про подтверждение ролей в базу
  * IDM-5222: Переписал работу с LDAP. Разделил блокировку и перенос в Old Users
  * IDM-5222: Добавил статусы “ошибка” для добавления и удаления из AD-группы
  * IDM-5222: Поправил импорты и тесты
  * IDM-5222: Добавил тестов, поправил логгирование
  * IDM-5222: Переписал тесты ldap, создаю action только если действие случилось
  * IDM-5222: Доблокировка из любых недоблокированных состояний
  * IDM-5222: Фикс testapi
  * Перенёс обработку перемещений в другую очередь
  * IDM-5222: Сократил срок заявок, которые мы считаем активными в Наниматоре, с 14 до 7 дней в прошлом, и расширил до года в будущем.

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-09 12:47:26

114.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5261: Превышение порога на число уволенных пользователей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-07 17:29:13

114.19
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5255: добавить в cron запуск допинывалки ролей для Qloud

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-05 16:39:34

114.18
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-XXXX: Разрешать перемещения в celery-тасках
  * Фикс разрешения перемещения пользователей в celery-задаче
  * Фикс разрешения перемещения пользователей в celery-задаче
  * IDM-5254: Добавил проверок на повторный запуск

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-05 14:58:37

114.17
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-4933: теперь depriving-узлы считаются активными и не создают неконсистентность типа 'неизвестная роль'

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-02-01 19:35:14

114.15
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5180: from\_api теперь является опциональным элементом в data

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-29 17:34:42

114.14
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5180: добавлено периодическое доудаление узлов в dumb-системах
  * IDM-5180: теперь случай с удалёнными узлами не учитывается при разрешении неконсистентностей
  * IDM-4933: для логики разрешения неконсистентностей добавлен тест (#1350)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-29 16:07:41

114.13
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5180: если мы находим уже существующее действие удаления узла, мы используем его
  * IDM-5180: увеличен интервал задержки таски
  * IDM-5180: проброс узла и системы в таску

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-25 19:57:40

114.12
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5180: убран atomic при удалении узла
  * IDM-5180: в тасках удаления узла action теперь подцепляется через or\_retry

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-24 17:45:37

114.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5099: Тормозит сохранение воркфлоу
  * Revert "IDM-5210 crutch for python bug"
  * Revert "IDM-5210 remove recursion from get\_roles\_tree()"

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-23 19:55:30

114.10
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5210 crutch for python bug

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-23 13:23:14

114.9
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5210 remove recursion from get\_roles\_tree()

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-22 19:51:55

114.8
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5180: удалён select\_for\_update() из отзыва ролей при удалении узла
  * IDM-5180: добавить проброс requester в mark\_depriving

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-22 15:31:12

114.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5205: PEP-8
  * IDM-5205: Удалил xfail тесты
  * IDM-5205: Удалил староватую логику
  * IDM-5205: PEP-8
  * IDM-5205: Передавать подробности про смену подразделения в историю роли
  * IDM-5205: Перестал писать робокоммент при подтверждении
  * IDM-5205: Поменял формулировки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-19 13:44:29

114.6
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5209 убрал сложную проверку

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5218: считать пустую строку dependencies за None
  * IDM-5218: считать пустую строку options за None

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-19 13:32:54

114.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Не ходить в проверке в ручку ping

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-18 12:16:48

114.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5208: Невозможно подтвердить роль

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-17 01:17:47

114.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-3544: Обрабатывать удалённые группы. Отдаём дату отзыва группы в API.
  * Добавил настройки слейва по умолчанию
  * IDM-4933: Поправил название константы
  * IDM-4933: Добавил order\_by
  * IDM-4933: Поменял тип скобочек
  * IDM-5180: Добавил файл ограничения памяти для новой очереди

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-4933: реализовано отложенное удаление узлов при синхронизации
  * IDM-4933: добавлены и поправлены тесты
  * IDM-4933: теперь depriving узлы тоже могут быть восстановлены (создаётся новый узел и переносятся роли), написан тест, проверяющий корректный отзыв или восстановление узлов и связанных ролей при удалении узла
  * IDM-4933: теперь удаление depriving-узла форсируется при его замещении полученным из системы; переименование параметра в mark\_depriving()
  * IDM-4933: поправлены старые тесты, полагающиеся на мгновенное удаление узла
  * IDM-4933: поправлено форсированное удаление узлов при переносе
  * IDM-4933: поправлены тесты
  * IDM-4933: реализован код отправки уведомлений
  * IDM-4933: report\_problem() при отсутствии рассылок у системы теперь может отправлять письма всем ответственным
  * IDM-4933: небольшие правки в тестах
  * IDM-4933: правки в коде отправки уведомлений и в шаблоне
  * IDM-4933: добавлены тесты; переименованы команды, файлы, функции
  * IDM-4933: написаны тесты для get\_node\_by\_unique\_id()
  * IDM-4933: мелкие правки
  * IDM-4933: добавлен Least из Django 1.9, mark\_depriving() переделана под его использование
  * IDM-4933: Least теперь используется вместе с Coalesce при не-postgres базах
  * IDM-4933: тесты теперь добавляют задержку между mark\_depriving() и deprive\_nodes()
  * IDM-4933: поправлено восстановление узлов без unique\_id
  * IDM-4933: восстановление улов теперь сбрасывает хеш и вынесено в отнельную функцию
  * IDM-5055: добавлена возможность отзывать только узлы из переданного списка
  * IDM-5055: пометка удаляемых узлов и их удаление перемещены в celery-таски
  * IDM-5055: удаление ролей перенесено в отдельный таск, добавлена регулярная команда для доудаления ролей
  * IDM-5055: правки по тестам
  * IDM-5055: добавлен dictinct при фильтрации подвисших узлов
  * IDM-5055: добавлена миграция для Action
  * IDM-5055: прокидывание дополнительных параметров в действия

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-16 20:58:52

114.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4641: Поправил ещё раз, добавил тест

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-15 19:05:32

114.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5200: Одинаково обрабатывать пустое необязательное поле при запросе через систему и через idm
  * IDM-5191: Роли в состоянии approved не попадают в system.all\_users\_with\_role
  * IDM-4641: Поправил сохранение данных в базу

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-15 17:56:27

114.0
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-3294: Добавить на страницу группы поле с описанием

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5147: Саджест систем case-sensitive
  * IDM-4641: Починил тесты

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-01-11 19:52:23

113.18
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5035: Поправил ещё один баг в majortom

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-29 20:50:34

113.17
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5035: Поправил ещё один баг в majortom

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-29 20:00:27

113.16
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5035: Поправлен баг в majortom

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-29 19:41:52

113.15
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5021: Добавил per-system роли просматривающего роли и просматривающего workflow
  * IDM-5021: В конфликтах нужно указывать только полный slug, подстроки не должны работать
  * IDM-5021: Конфликты должны срабатывать только для указанной системы, а не для всех

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-27 19:02:39

113.14
---

  * IDM-5021: Добавил per-system роли просматривающего роли и просматривающего workflow

 [Alexey Boriskin](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-27 19:02:30

113.13
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-2186: Запускать локально для конкретной системы (#1321)

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5164: Поправил сборку/разборку кверисета

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-26 16:58:09

113.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5164: Радикально уменьшил количество запросов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-26 15:38:54

113.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5142: Попытка починить большие выгрузки
  * IDM-3410: Поправил падающие тесты

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-25 20:52:25

113.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-3410: Перестал использовать клиентский сертификат там, где он не нужен
  * IDM-3410: Поправил баг с недопроброшенным decision-ом
  * IDM-3410: Добавил возможность вызова команды с границами времени создания заявки, поправил логику вычисления дат, включил команду

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-20 21:58:16

113.9
---

  * IDM-3410 Временно отключил запуск idm\_decide\_transfers

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-12-14 21:34:01

113.8
---

  * IDM-5089: добавлен review\_at в тестовый API, добавлен сброс даты пересмотра при пересмотре роли

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-13 18:38:35

113.7
---

  * resend

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-12 15:31:07

113.6
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5089: правка по дате пересмотра

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-11 17:21:46

113.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-3410: Отселил newhire в отдельный модуль
  * IDM-3410: Распилил STAFF\_URL на две части
  * IDM-3410: Не пересматривать роли человека, если виш-форма так сказала
  * IDM-3410: Поправил падавшие тесты, выпилил флаг запрета перезапроса

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-10 01:01:54

113.4
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-5130: Стрипать строчку при поиске по системе
  * IDM-5133: Не отправлять "пустые" оповещения о неактивных пользователях в AD

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5035: Подключил django-alive и majortom
  * IDM-5035: Обновил версию majortom, поправил вывод команды alivestate, чтобы он был в monrun-формате

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-09 17:14:54

113.3
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5089: теперь дата пересмотра всегда отдаётся на фронтенд

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-08 18:09:03

113.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Pin OpenSSL to avoid errors like https://github.com/pyca/pyopenssl/issues/728

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-07 14:03:38

113.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5111: Перенёс фикстуру cauth в общий conftest
  * IDM-5111: Поиск нод по алиасам в воркфлоу
  * IDM-5021: Реализация межсистемного конфликта ролей в IDM
  * IDM-4976: Вкрутить ретраи в IDM

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-06 20:56:28

113.0
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5089: Выносим срок пересмотра в систему, воркфлоу и API (#1309)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-12-01 19:06:34

112.33
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5092: За исключением системы ABC, шлём дайджест о необходимых к подтверждению ролях всем неотсутствующим подтверждающим

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-24 13:44:30

112.32
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5090: Ошибка в кешировании саджеста. Refs TOOLSUP-25613

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-22 19:26:44

112.31
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5075: Отселил всё про увольнение и синхронизацию сервисов в отдельные очереди. Больше очередей богу очередей!

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-20 18:16:14

112.30
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5080: Синхронизировать Стафф в быстрой очереди
  * IDM-5075: Стал писать больше логов, добавил информацию о том, сколько памяти съела таска за время своей работы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-20 17:11:26

112.29
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4927: Кеширую верхнеуровный саджест для каждой системы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-18 16:51:55

112.28
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5042: Разрешить ответственным чинить системы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-17 13:57:59

112.27
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5016: Добавил дискриминирующий фильтр, и запрос ускорился

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-16 17:44:42

112.26
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4951: Добавил опцию синхронного запуска к idm\_block\_ad\_users

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-16 12:46:47

112.25
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5060: Поправил падающий тест и поменял условие на правильное
  * IDM-4864: Обновить django-tanker и переводы
  * IDM-2116: Отключил отсылку писем владельцу при наличии подтверждающих

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-15 20:36:49

112.24
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5060: Добавил возможность синхронного запуска с помощью параметра --block

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-15 14:40:44

112.23
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4927: Поправил падающие тесты и опечатку

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-14 20:44:11

112.22
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4927: Попытка ускорение саджеста за счёт уменьшения количества джойнов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-14 20:05:49

112.21
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5040: Перешёл на общий ресурс-предок при запуске команд

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-14 18:19:27

112.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5063: Добавил возможность передавать в API время с явной таймзоной

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-14 15:45:51

112.19
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-2116: Отселил письма в отдельную очередь

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5053: Уведомить владельцев перезапрошенных ролей, которые еще не были подтверждены

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-14 14:12:06

112.18
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Починил падающий из-за проблем с таймзоной тест
  * IDM-4964: Поправил падавшие из-за нестабильности сортировки тесты. В рамках одного уровня и статуса добавлена сортировка по username
  * IDM-4948: Синхронизация групп забивает очередь
  * Revert "IDM-4812: Отдаём группу пользователя только для detail"
  * IDM-4948: Дописал тест для случая с approved ролями, но он изначально и не падал. Оставил, чтобы закрепить поведение тестом.
  * IDM-5065: Вернуть  поле department в ручку /users  для поискового саджеста

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-13 14:13:00

112.17
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5016: Добавил индекс, который должен ускорить запрос внутри get\_owners
  * IDM-5016: Поправил обработку создания индексов CONCURRENTLY

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-09 20:43:59

112.16
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4941: Пожертвовал джойном, чтобы не делать слишком сложную миграцию
  * IDM-4951: Отпилил удаление виртуалок уволенных сотрудников (кажется, это не наш бизнес и ручки давно нет)
  * IDM-4951: Тестинг должен точнее соответствовать продакшену: запускаем блокировку пользователей в AD, добавление и удаление из AD-групп, отзываем роли у уволенных в тестинге
  * IDM-4951: Уточнил комментарий
  * IDM-4951: Расширил возможность получения deprivable ролей на другие модели
  * IDM-4951: Убрал лишние импорты
  * IDM-4951: Удалил настройку OEBS\_DATA\_PROCESSING, объединил два менеджера модели User в один, удалил валидацию количества в команде idm\_deprive\_roles, команда теперь занимается исключительно отзывом ролей у уволенных и ничем иным
  * IDM-4951: Переименовал таск
  * IDM-4951: Перенёс код блокировки в менеджер, команда idm\_block\_ad\_users теперь работает в двух режимах: быстром и полном. В быстром режиме она блокирует неактивных пользователей с флагом ldap\_active=True, в полном – проверяет всех неактивных в AD.
  * IDM-4951: Исправил циклическую зависимость
  * IDM-4951: Поправил тесты на idm\_deprive\_roles, решил, что нужно при отзыве sent ролей отсылать пуш в remove-role
  * IDM-4951: Перенёс и починил тесты на idm\_block\_ad\_users
  * IDM-5045: Починил попутно сломанные тесты
  * IDM-5045: Добавил возможность сообщения об инцидентах отдельным письмом
  * IDM-5060: Переписал и включил предохранитель блокировки большого количества пользователей
  * IDM-5060: Переписал и включил предохранитель блокировки большого количества пользователей для команды отзыва ролей
  * IDM-5063: Добавил поле updated в API
  * IDM-5045: Починил давно сломанные в fulltest тесты
  * IDM-5045: Поменял название очереди на FIRE

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-5042: Разрешить ответственным чинить системы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-09 18:30:34

112.15
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5004: функция хеширования узлов изменена на CRC32
  * IDM-4908: удалён лишний проход с рехешированием в UpdatableNode.synchronize()
  * IDM-4908: убрана преждевременная запись хеша при синхронизации нод
  * IDM-4908: хеш узлов теперь хранится в шестнадцатеричном виде, тестовые системы теперь не перехешируются при создании
  * IDM-4908: добавлен правильынй просчёт хеша при добавлении узлов, обнуление хешей предков при удалении узла
  * IDM-4908: в тесты добавлена проверка на корректность проставления хеша при перемещении узла

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Фикс для development-сервера

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-01 20:02:01

112.14
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-4896: Разрешить ответственным системы видеть действия, связанные с системой
  * IDM-4896: Оптимизировал фильтр

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5045: Застревает очередь roles в тестинге idm

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-01 17:43:35

112.13
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-4674: Добавил логирование скоупов
  * IDM-4674: проверка атрибута, отключение логгера в тестах

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-24 20:52:40

112.12
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-4996: При синхронизации теперь не учитываются роли, чей статус был изменён во время сверки
  * IDM-4996: теперь время начала синхронизации мы берём из action
  * IDM-4996: добавлен тест, поправлен баг
  * IDM-4996: в тест добавлены depriving-роли

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-2116: Возможность при запросе роли выключать уведомления
  * IDM-2116: Подкрутил настройки для разработки
  * IDM-5016: Конкурентно создаю индекс по rolenodeclosure
  * IDM-2116: Подкрутил миграцию

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-24 18:06:08

112.11.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Добавил в список зависимостей contextlib2, чтобы работал raven

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-23 17:43:15

112.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Фикс сборки. Попробуем собрать psycopg по-старому, а django\_extesions нужно даунгрейднуть.
  * Поправил ворнинг про import\_path
  * Поправил ворнинг про requires\_system\_checks
  * Поправил ворнинг про юникод
  * IDM-5015: Обрезаем длинные имена вручную
  * Ещё одна попытка исправить psycopg2
  * Пришлось запинить старую версию cryptography и pip, чтобы сборка заработала

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-4951: теперь при переблокировке пользователей в LDAP вместо ldap\_active проверяется is\_active, а ldap\_active начинает указывать на фактическое состояние пользователя в LDAP
  * IDM-4951: удалена команда idm\_process\_data\_from\_oebs
  * IDM-4951: check\_users\_ldap\_status выводит только неконсистентные данные и на stdout, удалена check\_users\_ldap\_status
  * IDM-4951: команда проверки несогласованности IDM и LDAP переименована в idm\_check\_users\_ldap\_status
  * IDM-4951: теперь у Лёши не течёт кровь из глаз из-за бэкслэшей
  * IDM-5036: теперь конкурентное создание индекса не используется в тестах
  * IDM-5036: для обновлённой версии pytest-django изменены настройки тестовой базы
  * IDM-5036: правки по ревью

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-23 17:13:54

112.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5023: Слишком широкий паттерн-матчинг в описании конфликтов
  * IDM-5023: Запинил версию pip, обновил половину библиотек, чтобы пакет снова начал собираться
  * IDM-5026: Понизил уровень блокировки для select for update
  * IDM-5026: Сделал, чтобы все индексы создавались конкуретно
  * IDM-5026: Revert psycopg2 upgrade
  * Try to fix psycopg2
  * Trying to fix build: fix raven
  * Наконец пофиксил сборку
  * Выбросил множество левых ненужных зависимостей
  * IDM-5026: Избавился от djblets, которые перестали собираться в колесо

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-18 00:30:22

112.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4971: Тестинг пятисотит, если пришедшего пользователя нет на Стаффе
  * IDM-5016: Перенёс код в более подходящее место (не изменяя логики)
  * IDM-5016: Переписал на N запросов (надеюсь, это будет работать не бесконечное время)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-10 19:28:42

112.8
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5005: добавлены тесты, проверяющие, что на все персонально-пользовательские роли создана только одна неконсистентность

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-06 14:43:23

112.7
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-4941: В отчётах не работает фильтр по узлу

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-04 19:13:51

112.6
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-5002: Логировать system.slug вместо system в idm\_check\_certs

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-5009: Сломана сортировка по системе

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-03 20:53:10

112.5
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-4990: Поменять хост для СИБ
  * IDM-4997: Не отзывать сессии уволенных в тестинге

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-445: добавлен скрипт для проверки сертификатов систем

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-4941: Переход на новую фикстуру в тестах
  * IDM-4941: Поправил тесты после под новую фикстуру
  * IDM-4941: В отчётах не работает фильтр по узлу
  * IDM-4941: Миграция денормализации actions

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-09-29 13:25:16

112.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4980: Некорректный порядок подтверждающих в карточке роли
  * IDM-4977: Поправил 500 при не дефолтной сортировке
  * IDM-4977: Переделал схему с case sensitivity на чистый lower case
  * IDM-4967: Починил удаление системы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-09-15 18:21:11

112.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4977: Переименовал errors в exceptions
  * IDM-4977: Разбил менеджеры на отдельные файлы (не выдержал)
  * IDM-4977: Удалил артефакт от мёржа
  * IDM-4977: Backoff policy for locking a role
  * IDM-4977: Избавиться от запросов, которые съедают место временными файлами

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-4915: теперь клиентский сертификат проверяется на допустимость домена в CN

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * IDM-4967: Тест удаления родительского черновика

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-09-14 22:02:09

112.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4927: Два джойна по parent работают быстрее, чем один по closuretree

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-09-06 22:58:26

112.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Поправил перевод причины запроса роли при регулярном пересмотре
  * IDM-4964: Добавить поддержку получения hr-партнеров в workflow IDM

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * IDM-4953: Сделать команду для починки поломанных перенесенных узлов
  * IDM-4953 fix find broken nodes

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-09-06 09:36:12

112.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4723: Поправил код при ретраях, чтобы их было меньше, если лок успешен
  * IDM-4930: IDM уходит в ридонли из-за незакрытых транзакций

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-30 15:55:15

111.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4883: Добавил поле длинного таймаута, по умолчанию 10 минут

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-03 17:47:44

111.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4856: Не возвращается запросивший роль

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-03 12:56:45

111.10
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4888: Проверять, что actual\_wf не None в ручке /<workflow\_id>/commit
  * IDM-4794: Поправить idm\_check\_groups, чтобы оно учитывало onhold роли удалённых групп

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Revert "IDM-4888: Проверять, что actual\_wf не None в ручке /<workflow\_id>/commit"
  * IDM-4888: Начал создавать approved версию workflow при создании системы
  * IDM-4916: Логировать домены приходящих с сертификатом роботов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-02 20:13:08

111.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4912: Поменять список статусов сервисов в синхронизации с ABC

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-01 17:14:21

111.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4723: Добавил ретраев на лок
  * IDM-4907: Поправил падающие тесты (нужно было оставить конфиг для development)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-31 18:50:46

111.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4904: Слишком долгий интервал перед повторным отзывом роли
  * IDM-4903: Нет проверки прав на чтение воркфлоу через сабсет
  * IDM-4907: Ходить в тестинге в тестовую посылалку SMS
  * RULES-4230: Новая стратегия для celery
  * RULES-4230: Не подменять root logger, пробрасывать исключения в eager режиме

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-31 17:33:21

111.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4898: Отзывать узлы и роли при удалении узла через API без таски

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-25 20:24:54

111.5
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4845: Багфикс from\_api + тест на from\_api==False

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-746: Спрятал письма за опцию командной строки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-25 10:57:34

111.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4845: Переименовал from\_web в from\_api и поправил баг, где смешиваются from\_web и from\_api

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-20 23:08:29

111.3
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * IDM-4884: Добавить фильтр ручки узлов по полю parent

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4367: Заменил строки на константы в тестах
  * IDM-4367: Поменял порядок выполнения тасок, чтобы неконсистентность не разрешалась, пока роль не запрошена
  * IDM-4367: Код ошибочно проставтавлял комментарий про уволенность пользователя при разрешении обычной неконсистентности в SOX-системе
  * IDM-4367: Поправил несоздающийся тикет в Стартреке

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-20 21:24:51

111.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-746: Поправил орфографию и тесты
  * IDM-4770: Переместил и переделал функцию calculate\_hash
  * IDM-4770: Переформатировал index\_together
  * IDM-4770: Переписал функции разрешимости
  * IDM-4770: Разрешение прежде не разрешимых неконсистентностей
  * IDM-4770: Использую один oauth-токен для всех сервисов
  * IDM-4770: Перенёс тесты про отчёты в отдельный файл
  * IDM-4770: Unused imports
  * IDM-4770: Typo
  * IDM-4770: Вынес политики в константы
  * IDM-4770: Сделал mock\_ids\_repo более общим
  * IDM-4770: Создаю тикет для SOX-систем вместо того, чтобы отсылать письмо

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-17 15:56:36

111.1
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4844: Добавить логгирования при удалении и добавлении узла через API
  * IDM-4847: Объединять элементы очереди изменения дерева ролей в пачки-транзакции
  * IDM-4367: Более строгое разрешение неконсистентностей
  * IDM-4252: Плохая ошибка подтверждения роли в сломанной системе
  * IDM-1560: Написать миграцию, удаляющую лишних пользователей
  * IDM-746: Слать письма, если ночная синхронизация ролей не удалась
  * IDM-4842: Починить проставление parent\_id у экшена при синхронизации дерева
  * IDM-4845: Невозможно отделить удаление узла при синхронизации от действия через API
  * IDM-4843: В экшены не проставляется impersonator\_id, если узел был удалён через api
  * IDM-4851: Опечатка в описании поля

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4873: Router запрещает relation с роботом
  * IDM-4863: sazhin: заблокирован аккаунт

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-14 22:12:07

111.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4852: В девелопе падают тесты
  * IDM-4852: Тесты не собираются на тимсити

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-03 18:31:21

110.36
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4873: Router запрещает relation с роботом

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-14 16:23:39

110.35
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4838: Тормозит выдача сервисов в саджесте системы ABC

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-22 19:00:40

110.34
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4821: Регистр в слаге и саджесте наносят ответный удар

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-21 15:30:22

110.33
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4839: Не запрашивается роль в тестинге

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-21 14:33:06

110.32
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4821: Регистр в слаге и саджесте

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-20 20:24:09

110.31
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4814: Денормализовал причину запроса и комментарий
  * IDM-4814: Перестал считать статистику для вложенных ApproveRequest-ов, это должно убрать квадратичность запроса
  * IDM-4814: Перестал отдавать объект workflow для запроса роли. У нас он есть, но зачем отдавать его?
  * IDM-4821: Регистр в слаге и саджесте

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-20 18:48:18

110.30
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4812: collate нужно указывать внутри upper у правого операнда, а не левого

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-19 18:52:31

110.29
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4812: collate нужно указывать внутри upper, а не снаружи

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-19 17:08:45

110.28
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4812: Починил хрупкие тесты
  * IDM-4812: Стал явно указывать collation при составлении lookup-ов типа icontains/istartswith

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-19 15:37:50

110.27
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4812: Пришлось восстановить все unique constraint-ы, чтобы их потом можно было снимать

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-17 14:16:28

110.26
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4812: Фикс миграции

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-16 21:13:21

110.25
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4812: Отдаём группу пользователя только для detail
  * IDM-4812: Отловил большое количество забытых select\_related
  * IDM-4812: Дополнительный фильтр по системе отсеивает большое число узлов
  * IDM-4808: Сломали системы
  * IDM-4808: Просто поправил код
  * IDM-4825: Сделал поиск по slug-у регистронезависимым
  * IDM-4825: Поиск по системам работает не очень хорошо

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-16 20:23:31

110.24
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4813: Обрабатывать изменения регистра в параметрах роли
  * IDM-4815: Ускоряю прогон тестов
  * IDM-4815: Починил падавшие на постгресе тесты
  * IDM-4810: Задублировались узлы в Статистике

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-14 20:34:37

110.23
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4807: Падаем при поиске по системам
  * IDM-4809: Сломалась синхронизация сервисных групп

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-13 20:33:31

110.22
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: workaround для починки batch-ресурса
  * Revert "IDM-4270: Обновил django-replicated"
  * IDM-4270: Маленькое, но важное изменение в поиске узлов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-11 18:31:46

110.21
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Починил django-replicated ещё раз
  * IDM-4270: Фикс имени vaccarium@ для закрытия коннектов при форке uWSGI

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-09 21:16:57

110.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Починил django-replicated

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-09 19:23:10

110.19
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Обновил django-replicated

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-09 18:52:08

110.18
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Фикс саджеста

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-09 16:59:48

110.17
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Поправил ошибку в случае, когда пагинатор используется со списком, а не кверисетом

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-09 14:59:47

110.16
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Поправил падающие тесты

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-08 21:27:20

110.15
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Попытка упростить запросы, избегая, тем не менее, появления дублирующихся записей
  * IDM-4270: Меньше джойнов для бога джойнов
  * IDM-4270: Используем оценки count(*) вместо точных значений для ускорения запросов
  * IDM-4270: Ускорил выборки с rolenodeset и internalobjectpermission
  * IDM-4270: Переписал public\_query понятнее

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-08 17:46:43

110.14
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Revert "IDM-4270: Фикс миграции"
  * Revert "IDM-4270: Денормализация для ускорения public-части выборок ролей"

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-07 17:49:15

110.13
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Фикс миграции
  * IDM-4270: Закешировал робота

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-07 12:17:59

110.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Добавил индексов на горячие поля системы
  * IDM-4270: Проставил всем CharField-ам или null, или default
  * IDM-4270: Сохранил на всякий случай скрипт, дропающий все таблицы
  * IDM-4270: debug-фикстура
  * IDM-4270: Мир fields, война excludes
  * IDM-4270: Элиминировал серьёзное количество LEFT JOIN-ов
  * IDM-4270: Перезагрузил вьюхи
  * IDM-4270: Денормализация для ускорения public-части выборок ролей
  * IDM-4790: Починка сломанных хотфиксом функций и тестов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-07 11:50:22

110.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4781: Решили показывать рубиновую корону в интерфейсе

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-02 18:24:12

110.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4790: Отправляем нотификации на лишние рассылки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-02 16:50:38

110.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Поправил миграцию. Зря доверился выводу sqldiff

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-01 23:34:05

110.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Чиню проблему с сертификатом

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-01 21:55:04

110.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4781: Поддержать рубиновую корону
  * IDM-4270: Ускорение выборок по approverequest-ам
  * IDM-4270: Поправил тип durationfield-а в модели системы
  * IDM-4270: Если список approverequest-ов запрашивает с подтверждающим, можно отбросить сложную проверку прав
  * IDM-4270: Добавил параметры SSL в конфигурацию баз (интересно, как работало без этого)
  * IDM-4270: Повторяю попытки достучаться до базы 10 раз

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-01 21:41:52

110.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Промахнулся с полем. Поправил миграцию

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-31 22:26:56

110.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Ускорение

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-31 21:25:52

110.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4739: Оптимизация отзыва ролей
  * IDM-4270: Переписал проверяющий права запрос на несколько OR-подзапросов
  * IDM-4270: Сделал свой auth backend, чтобы делать меньше запросов в базу
  * IDM-4270: requester может быть None
  * IDM-4428: Запросивший должен видеть роли, которые он запросил
  * IDM-4270: Поправил падавшие тесты на количество запросов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-31 13:06:45

110.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Поправил настройки для dev-а
  * IDM-4270: Включил кеширование сессий

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-27 13:54:26

110.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Поправил падающие тесты
  * IDM-4270: Поправил настройки на dev

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-26 15:10:36

110.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Поправил ошибку в closuretree

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-25 19:33:02

110.0
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4722: Из доктеста не пробрасывается узел
  * IDM-4771: Завести рассылку idm-notification-test@yandex-team.ru и слать письма из тестинга туда

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Поправил отсутствующий import
  * IDM-4270: Поправил closuretree
  * IDM-4270: Поправил database backend под Postgre
  * IDM-4270: Если срабатывает ON CONFLICT, то RETURNING не возвращает результатов. Не стоит ожидать их, если их нет
  * IDM-4270: Настройки БД
  * IDM-4270: Поправил conftest
  * IDM-4270: Поправил тесты, зависящие от случайности при выборках из базы
  * IDM-4270: Поправил тесты, зависящие от времени
  * IDM-4270: Поправил запросы, не работавшие из-за строгой проверки типов PG
  * IDM-4270: Поправил поиск и разрешение неконсистентностей
  * IDM-4270: Удалил oneoff-команду, чтобы не переписывать SQL
  * IDM-4270: Переписал старый саджест на ORM
  * IDM-4270: Переписал SQL VIEW под PG
  * IDM-4270: Переписал SQL в команде idm\_restore\_updated
  * IDM-4270: Поправил сортировку неконсистентностей
  * IDM-4270: Поправил проблемы с порядком NULL
  * IDM-4270: Убрал все упоминания MySQL, а также MySQL-специфичные костыли
  * IDM-4270: Переименовал везде в тестах @mysqlonly на @thickdb
  * RULES-4270: Поправил проблемы с сортировкой
  * IDM-4270: Явная сортировка подтверждающих по умолчанию
  * IDM-4270: Добавил в fabfile команду для запуска Docker
  * IDM-4270: Заменил параметры коннекта к БД

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-25 18:08:39

109.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Настройки коннекта к pgaas

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-11 12:49:11

109.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4790: Починка сломанных хотфиксом функций и тестов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-07 19:50:44

109.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4781: Поддержать рубиновую корону
  * IDM-4781: Решили показывать рубиновую корону в интерфейсе
  * IDM-4790: Отправляем нотификации на лишние рассылки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-06-02 18:30:38

109.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Поправил отсутствующий import

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-25 16:57:33

109.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4270: Миграционный скрипт и зависимость
  * IDM-4270: SQL-скрипт для анализа сломанных внешних ключей
  * IDM-4270: Удалил неиспользуемые настройки
  * IDM-4270: Настройки
  * IDM-4270: Удалил дичь
  * IDM-4270: Вернул определение direct-токена для тестинга
  * IDM-4270: Обновил локальные настройки
  * IDM-4270: Перенёс django-extensions в основной список и добавил в INSTALLED\_APPS
  * IDM-4270: Удалил или переименовал в .example все .local-файлы
  * IDM-4270: Добавил libpq-dev в сборку
  * IDM-4270: Пробросил config в settings\_pg

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-25 16:03:26

109.7
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4721: Пофиксил импорт

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-19 19:36:38

109.6
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4766: Починить пуши узлов в саджест
  * IDM-4721: Ворнинг в форме и письмо на рассыку если связанная роль не может быть выдана
  * IDM-4769: Неправильное сообщение при каскадном холде

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4720: Сузил область транзакции, чтобы она была внутри лока
  * IDM-4756: Поправил отзыв роли через testapi

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-19 18:40:26

109.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4744: Баги дедупликатора
  * IDM-4756: Разрешил передавать \_requester в querystring для запросов без body
  * IDM-4756: Разрешил отзывать недопротухшие роли через параметр now\_is/--now-is команды idm\_deprive\_roles
  * IDM-4720: Race condition с паспортными логинами

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4260: Небольшие правки
  * IDM-4260: Отложенный отзыв ролей при удалении группы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-18 18:56:34

109.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-3555: Ошибка в переименовании ноды

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4747: Правильный порядок composite индекса для role
  * IDM-4747: Подчистил SQL

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-05-17 19:39:36

109.3
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4428: Выдать права запросившему на отзыв роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-16 19:36:07

109.2.1
---

  * Пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-16 18:55:06

109.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4744: Удалить дубликаты узлов в Qloud
  * RULES-4718: Перешёл везде на один сертификат, новый
  * IDM-4667: Поменял порядок операций в миграции, чтобы она проходила

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4741: Сделать флаг "Использовать мини-форму" для системы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-16 16:47:19

109.1
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * IDM-4732: Не работает саджест по людям
  * IDM-4739: Не откладывать роли бывших
  * IDM-4753: Падает тест про саджест
  * IDM-4747: Ускорить синхронизацию департаментных групп
  * RULES-4724: Брать названия статусов сервиса как есть

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-05-12 21:26:57

109.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4513: Дописал тест на синхронизацию одновременно дерева и ролей, который я забыл написать при реализации фичи
  * RULES-4731: Связанные роли не отзываются при синхронизации
  * RULES-1989: Реализация мягкого конфликта ролей
  * IDM-4429: не могу изменить visibility для узла
  * RULES-1989: Поменял match на search
  * IDM-4450: Конфликтуют только роли одной системы, исправлен порядок аргументов для проверки без вайлдкардов
  * IDM-4458: Убрал поиск по ролям за отдельную фичу

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4723: Использовать в поиске по ролям intrasearch

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-28 18:00:19

108.43
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * IDM-4450: Конфликтуют только роли одной системы, исправлен порядок аргументов для проверки без вайлдкардов
  * IDM-4458: Убрал поиск по ролям за отдельную фичу

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4723: Использовать в поиске по ролям intrasearch

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-28 18:25:27

108.42
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Revert "RULES-4723: Использовать в поиске по ролям intrasearch"

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-20 13:39:56

108.41
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4723: Использовать в поиске по ролям intrasearch
  * RULES-4723: Использовать в поиске по ролям intrasearch

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4731: Связанные роли не отзываются при синхронизации
  * RULES-1989: Реализация мягкого конфликта ролей
  * IDM-4429: не могу изменить visibility для узла
  * RULES-1989: Поменял match на search

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-19 17:59:04

108.40
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4714: Ошибка в списке полей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-14 19:39:33

108.39
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4720: Ручка узлов стала медленной

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4672: Сломался idm
  * RULES-4715: Нельзя перезапросить проимпортированную роль

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-14 17:28:30

108.38
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4714: Сломана синхронизация сервисов
  * Ускорение поиска ролей по алиасам с помощью поиска только по началу строки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-13 20:02:49

108.37
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4708: Миграция

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-11 21:28:01

108.36
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4698: Если изменений нет, но ошибки быть не должно

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-10 14:36:36

108.35
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Немного ускорил синхронизацию групп

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-07 20:53:15

108.34
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4513: Синхронизация ролей по кнопке должна быть в выделенной очереди
  * RULES-4513: Улучшения в everysync
  * RULES-4513: Добавил лок в idm\_auto\_update\_roles

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-07 17:24:11

108.33
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4676: Фикс для вики-групп имени Феликса

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-07 11:48:32

108.32
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4662: Добавил ускоряющий саджест индекс

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-06 19:53:24

108.31
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4676: Поправил KeyError в сервисных и вики-группах

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-06 18:41:30

108.30
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4676: Поправил KeyError

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-06 18:14:34

108.29
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4707: Фильтр по ролям без parent в api тормозит

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-06 16:46:40

108.28
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Пофиксил зависание тестов (виновато сочетание freezefun и min\_lock\_time)
  * RULES-3408: Ограничить редактирование систем через api

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-06 15:08:39

108.27
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4691: Улучшить логгирование в пушах
  * RULES-4698: Шлём пуш про удаление узла при изменении его slug-а
  * RULES-4698: Защищаюсь от отката транзакций с помощью стандартной схемы с передачей id экшена в таску

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-05 20:33:47

108.26
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4676: Считаем, что уволенные пользователи не могут быть членами групп или ответственными за группы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-05 19:51:07

108.25
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4641: Исправление ошибки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-05 17:46:29

108.24
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * Убрана настройка AD\_LDAP\_USERS\_CN

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4692: Отправлять пуши про перемещённые узлы
  * RULES-4676: Не отзывается персональная роль, выданная на основе групповой, уволенному пользователю
  * RULES-4698: Разрешить менять slug узла дерева ролей через API
  * RULES-4676: Не отзывается персональная роль, выданная на основе групповой, уволенному пользователю
  * RULES-4230: Поднял лимиты очередям default, sync\_small
  * RULES-4513: Автообновление узлов дропает таск, если лок не взялся, остальные случаи ждут лок
  * RULES-4513: Небольшой рефакторинг
  * RULES-4513: Каждый час обновляем статистику по ролям и узлам для систем, отправляем в очередь для тяжёлых запросов только те синхронизации, которые включают в себя синхронизацию узлов
  * RULES-4513: Перестал ставить таски слишком часто
  * RULES-4513: Миграции

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-04-04 12:51:23

108.22.2
---

  * Ещё пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-28 17:56:02

108.22.1
---

  * Пересборка с dev-python

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-28 17:16:48

108.22
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4687: Добавил воркер и лимит для очереди ретраев

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-27 17:03:38

108.21
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4687: Изолировать очереди операций с ролями для массивных систем
  * RULES-4513: Поправил лог

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-27 16:55:57

108.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4513: Удалил старые задачи синхронизации
  * RULES-4513: Объединил задачи синхронизации узлов и ролей
  * RULES-4667: Посмотреть что изменилось для списка ролей
  * RULES-4513: Поправил лимит, т.к. на тестинге очередь зависала
  * RULES-4513: Начал записывать время последней успешной сверки
  * RULES-4513: Уменьшил лимит, чтобы большие системы точно пролезли
  * RULES-4513: Разбил ручные синхронизации на две очереди в зависимости от размера системы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-24 15:06:48

108.19
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4684: Для систем со слешами в slug-ах саджест работает неправильно

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-23 16:31:05

108.18
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4230: Добавил копирование файлов с ограничениями памяти

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-21 16:22:24

108.17
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4662: Перестал отдавать aliases в саджесте узлов
  * RULES-4230: Проставил всем воркерсетам maxtaskperchild
  * RULES-4230: Кастомизировал потребление памяти по воркерсетам
  * RULES-4230: Мониторинг очередей
  * RULES-4230: Поправил регулярку
  * RULES-4230: Удалил celerybeat
  * RULES-4230: init.d -> service

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-21 16:04:22

108.16
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4230: Обновление celery до максимальной 3.x версии

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-20 18:06:23

108.15
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4664: system\_\_contains смотрит только в slug и name/name\_en
  * RULES-4662: Пофикшены MySQL тесты
  * RULES-4664: Добавлено поле is\_favorite в список систем

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4661: Ускорение за счёт удаления обращения к department на каждом запросе
  * RULES-4661: Ошибка мёржа

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-20 13:20:52

108.14
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4661: Отселил отчёты в отдельную очередь, оптимизировал выгрузку

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-17 18:41:20

108.13
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4664: Саджест по сервисам
  * RULES-4664: Поле state в системе
  * RULES-4664: Фильтр по подстроке в системах
  * RULES-4664: Сортировка по сервису и системе
  * RULES-4664: Мелкие доработки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-17 16:19:31

108.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4661: Увеличил максимальное количество строк в отчёте до 500000
  * RULES-4660: idm\_add\_users\_to\_ad\_groups отдает 500
  * RULES-4662: Ускорить саджест (ещё)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-17 13:25:41

108.11
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4636: Убрать удаление запрошенных ролей для уволенных юзеров из idm\_deprive\_roles

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4123: Поправил ошибку логгирования

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-15 18:57:27

108.10
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4636: Убрать удаление запрошенных ролей для уволенных юзеров из idm\_deprive\_roles

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4123: Поправил ошибку логгирования

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-15 18:55:47

108.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4613: Перевёл из error/exception в warning те места, где исключение гасится, но не является ошибкой
  * RULES-4613: Перевёл из error/exception в warning те случаи .exception, когда исключение перевыбрасывается
  * RULES-4613: Поменял везде с inflect('en') на get\_ident()
  * RULES-4613: Убрал более ненужный raise
  * RULES-4613: Перевёл некоторые команды на SmartCommand и добавил в неё логгирование при ошибках
  * RULES-4123: Добавить retry при сетевых ошибках

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-14 14:57:54

108.8.1
---

  * Пересборка №3

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-14 09:58:35

108.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4654: Падает синхронизация групп из-за depriving ролей, которые нельзя перевести в onhold
  * RULES-4655: Не пересматривать роли, выданные после перемещения

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4651: заменён log на self.log в тасках, добавлен продовый INTRASEARCH\_PUSH\_URL в конфиг
  * RULES-4628: Отпилить синхронизацию с LDAP

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-13 19:58:35

108.7.2
---

  * Пересборка №2

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-13 18:19:01

108.7.1
---

  * Пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-13 17:44:34

108.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4230: Исправил проблему с незарегистрированной задачей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-13 16:33:33

108.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4230: Откатываем отладочный код

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-13 14:44:06

108.5
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4651: Не работают пуши в проксированный саджест (?)

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4643: Исправление ошибки с перезапросом роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-10 20:02:03

108.4
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4589: Синхронизировать дерево сервисов
  * RULES-4467: Новая ручка списка систем

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-09 19:34:13

108.3
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4647-2: Увеличить таймаут саджеста

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4643: Перезапрос роли не отзывает связанные роли
  * RULES-4643: Убрал валенок с пульта

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-09 18:32:56

108.2
---

  * RULES-4646: Пятисотки в новом саджесте
  * RULES-4647: Увеличить таймаут саджеста

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-03-09 17:03:20

108.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4952: Опечатка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-09 10:48:50

108.0
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4589: Синхронизировать дерево сервисов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-07 19:50:21

107.23
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4662: Перестал отдавать aliases в саджесте узлов

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4684: Для систем со слешами в slug-ах саджест работает неправильно

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-03-23 17:33:32

107.22
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4661: Увеличил максимальное количество строк в отчёте до 500000

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-16 17:15:55

107.21
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4655: Не пересматривать роли, выданные после перемещения
  * RULES-4654: Падает синхронизация групп из-за depriving ролей, которые нельзя перевести в onhold

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4651: заменён log на self.log в тасках, добавлен продовый INTRASEARCH\_PUSH\_URL в конфиг

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-14 16:42:18

107.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4643: Исправление ошибки с перезапросом роли

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4646: Пятисотки в новом саджесте
  * RULES-4651: Не работают пуши в проксированный саджест (?)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-10 20:13:38

107.19
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4647: Увеличить таймаут саджеста
  * RULES-4647-2: Увеличить таймаут саджеста

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4643: Перезапрос роли не отзывает связанные роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-09 18:40:23

107.18
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4550: Попытки запустить задачу синхронно приводили к крешу транзакции

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-06 19:49:46

107.17
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4550: Правки по отзыву и запросу роли после синхронизации групп

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-06 15:22:06

107.16
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4637: Мигрировать менеджеров ролей ABC
  * RULES-4550: Больше логов
  * RULES-4550: Ускорил отзыв лишних ролей
  * RULES-4550: Исправил баг, связанный с тем, что при перемещении в группу с неразрешённым перемещением для него создавалось user\_group перемещение
  * RULES-4550: Разрешаем дочерние перемещения, по которым не было принято решение, так же, как и групповое

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-03 02:11:05

107.15
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4550: Ошибка в названии действий
  * RULES-4550: Обвешал потенциально медленные операции логами

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-03-02 13:25:08

107.14
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4634: Решил установить минимальный таймаут лока в 10 секунд глобально
  * RULES-4634: Сделать команду idm\_sync\_groups частично синхронной
  * RULES-4635: Перевыдавать granted роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-28 17:17:04

107.13
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4634: Решил установить минимальный таймаут лока в 10 секунд глобально
  * RULES-4634: Сделать команду idm\_sync\_groups частично синхронной
  * RULES-4635: Перевыдавать granted роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-28 16:57:41

107.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4550: Правки ошибки в админке

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-27 22:01:15

107.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4550: Дочерние перемещения должны создаваться только один раз

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-27 18:42:48

107.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4388: Закрасить старые ручки для фаерволла
  * RULES-4621: Закрасить неиспользуемые ручки testapi

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-22 15:48:59

107.9
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4620: Логгировать id узлов про синхронизации
  * RULES-4162-2: В отчёт к персональным ролям добавить подтверждающего

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4550: Улучшения по ручному пересмотру
  * RULES-4550: Перемещения добавлены как ресурс в API

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-21 19:06:38

107.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4550: Улучшения в обработке перемещений

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-20 21:17:55

107.7
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4162: В отчёт к персональным ролям добавить подтверждающего
  * RULES-4614: Добавить фильтры по id в suggest для users, groups и subjects
  * RULES-4587: Доработать пуши/админку так, чтобы они учитывали узлы, создаваемые через админку

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4611: Синхронизация групп падает, если в очереди add является потомком move
  * Починка тестов через деактивацию перевода при выходе из теста с фикстурой client

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-20 18:09:15

107.6
---

  * RULES-4604: Добавить ворнинг про роль у родительской группы

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-02-16 13:04:27

107.5
---

  * RULES-4591: В саджесте есть узлы с visibility:false

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-02-14 18:24:22

107.4
---

  * RULES-4595: Обновление сбивает выбранную ноду

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-02-13 18:37:22

107.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4550: Ручной запуск механизма пересмотра при структурных изменениях

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-04 12:51:05

107.1.1
---

  * Пересборка

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-02-03 18:44:37

107.1
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4353: Фикс ошибки в intrasearch\_push

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-03 17:00:48

107.0.1
---

  * Пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-03 16:44:10

107.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4584: Баг в локах
  * RULES-4584: Переименовал diration->duration
  * RULES-4584: Поправил декоратор graphite\_duration
  * RULES-4584: Поправил лок в idm\_check\_and\_resolve
  * Revert "RULES-4353: Делать пуш в ручку поиска при изменении/добавлении/удалении узла"

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4353: Делать пуш в ручку поиска при изменении/добавлении/удалении узла
  * RULES-4353: Делать пуш в ручку поиска при изменении/добавлении/удалении узла

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-02-03 16:04:54

106.27
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4611: Синхронизация групп падает, если в очереди add является потомком move

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-17 12:47:02

106.26
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Revert "RULES-4353: Делать пуш в ручку поиска при изменении/добавлении/удалении узла"

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-02 18:00:56

106.25
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4584: Баг в локах
  * RULES-4584: Переименовал diration->duration
  * RULES-4584: Поправил декоратор graphite\_duration
  * RULES-4584: Поправил лок в idm\_check\_and\_resolve

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4353: Делать пуш в ручку поиска при изменении/добавлении/удалении узла

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-02-02 16:06:52

106.24
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4354: Возвращение ids==1.3.7 в requirements

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-31 16:24:56

106.23
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4354: Переключение саджеста по флагу

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-31 16:02:35

106.22
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4573: Убрал старый TODO
  * RULES-4573: IDMу плохо от удаления сервиса

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-31 15:47:58

106.21
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4562: Команда idm\_check\_and\_resolve берёт глобальный лок вместо посистемного
  * RULES-4562: Ускоряем get\_owners индексами

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-30 23:36:11

106.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4560: Не коммитится workflow

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-30 13:40:33

106.19
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Revert "RULES-4354: Фикс саджеста узлов (выдирается слаг из id), фикс фильтров (если их нет, то параметр query больше не передаётся)"
  * Revert "RULES-4354: Сделать проксированный саджест"
  * RULES-4354: Фикс спорадических тест фейлов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-30 13:02:38

106.18
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4354: Фикс саджеста узлов (выдирается слаг из id), фикс фильтров (если их нет, то параметр query больше не передаётся)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-27 18:32:05

106.17
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4354: Сделать проксированный саджест

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-27 16:50:48

106.16
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * Убран id из запроса к системе в тесте
  * RULES-4554: Добавить поле parent\_path в ручку узлов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-26 19:17:47

106.15
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Revert "RULES-4354: Сделать проксированный саджест"

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-25 20:22:39

106.14
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4507: При массовом отзыве принимаем параметры как из query, так и из body и требуем хотя бы одного фильтрационного параметра

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-25 18:40:16

106.13
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4354: Сделать проксированный саджест

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-25 17:10:41

106.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3254: Фикс миграции: удаление по уровням

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-25 13:41:50

106.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3254: atomic=False и удаление по уровням
  * RULES-3254: Перенос детей неактивных групп так, что их родителями становится база

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-24 19:17:46

106.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3254: Фикс миграции

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-24 15:58:24

106.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4349: Откатываю передачу id роли в плагин
  * RULES-4507: Ручка для кнопки «Отозвать все личные роли»
  * RULES-4367: Фильтр по ролям без parent в api
  * RULES-4349: Отзыв роли по комбинации owner+path+fields\_data
  * RULES-3254: Удалил ненужную строку
  * RULES-3254: Перезапрашиваем роли пользователей, находящихся внутри перемещаемых групп
  * RULES-3254: Ускорение миграции за счёт сырых delete-запросов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-24 15:03:44

106.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3254: Добавил зависимость, чтобы миграция работала
  * RULES-3254: Поправил IntegrityError в миграции
  * RULES-3254: Сделал миграцию рестартуемой и транзакционной
  * RULES-3254: Запускаем синхронизацию групп в таске

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4443: Отдавать систему в ручке rolenodes

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-23 15:01:10

106.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3254: Поправил генерацию диффа для сравнения деревьев

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-20 19:21:49

106.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3254: Фикс миграции
  * RULES-3254: Поправил ошибку при попытке посмотреть изменения дерева ролей
  * RULES-3254: Поправил падающий на тимсити тест

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-20 15:53:14

106.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3254: Экстрагировал дочерние элементы очереди из родительских элементов добавления и удаления
  * RULES-3254: Перемещать группы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-20 09:55:18

106.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4537: Пробрасывать на страницу системы настраиваемый таймаут

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-19 13:07:55

106.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4522: Поправил формулировку ворнинга

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-16 18:36:40

106.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4522: Учитывать поля при проверке на владение ролью

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-16 17:56:48

106.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4522: Проблема с ворнинг-сообщением при запросе роли на группу
  * RULES-4439: Некоторые переменные не долетают до блока тестирования workflow
  * RULES-3182: Удалить класс RoleAsNode

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-15 01:34:43

106.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4502: Робот ошибочно подтверждает роли, отправленные на регулярный пересмотр
  * RULES-3084: Автоподтверждение approverequest

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-11 15:13:47

105.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4439: Некоторые переменные не долетают до блока тестирования workflow
  * RULES-4522: Проблема с ворнинг-сообщением при запросе роли на группу
  * RULES-4522: Учитывать поля при проверке на владение ролью
  * RULES-4522: Поправил формулировку ворнинга

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-16 18:44:21

105.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4502: Робот ошибочно подтверждает роли, отправленные на регулярный пересмотр

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-01-11 12:05:44

105.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4484: Род глагола берется не оттуда

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-27 10:07:41

105.9
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4464: Ломается idm в продакшене

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-26 17:58:19

105.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4473: Поправить формат requester, impersonator в ручке действий

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-26 17:54:14

105.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4338: Убрал свойство successful
  * RULES-4338: Убрал свойство api\_url
  * RULES-4338: Новый объект requester и разделение поля user на user и requester
  * RULES-4338: Правки API в связи со всеобщей реквестиризацией
  * RULES-4338: Правки тестов в связи с реквестеризацией
  * RULES-4338: Денормализация действий

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-26 16:03:42

105.6
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4442: В проверке на уникальность слага учитывать систему
  * RULES-4365: Придумать как локализовать информационное сообщение в форме

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-23 18:23:40

105.5.1
---

  * Пересборка

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2016-12-23 15:08:28

105.5
---

  * RULES-4459: Добавить метод has\_role в группы

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2016-12-23 14:43:39

105.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4455: Перевыдать без подтверждения роли
  * RULES-4095: Предупреждать при запросе личной роли, что уже есть такая

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4365-2: Придумать как локализовать информационное сообщение в форме

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-22 01:56:53

105.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4447: Редактировать notify queue через админку

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-20 17:47:44

105.2
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4365: Придумать как локализовать информационное сообщение в форме

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-20 17:08:45

105.1
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4415: Добавить индекс для ускорения выдачи всех узлов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-19 12:06:10

105.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4429: Допинывалка учитывает неактивность систем не на всех стадиях

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-15 21:30:03

104.12.1
---

  * Пересборка в правильную ветку

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-21 17:48:11

104.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4455: Перевыдать без подтверждения роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-21 17:44:36

104.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4447: Редактировать notify queue через админку

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-20 18:08:18

104.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4428: Undefined группы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-14 16:27:08

104.9.2
---

  * Пересборка ещё раз

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2016-12-09 19:19:12

104.9.1
---

  * Пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-09 18:48:54

104.9
---

  * RULES-4410: Задавать кастомный таймаут для системы

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2016-12-09 18:28:19

104.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4403: Добавить переход из rerequested в rerequested
  * RULES-3967: Неправильно отображается дата (бекенд)
  * RULES-4406: Потеряли поле approved в /approverequests

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-09 13:11:01

104.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3867: Отдавать подробные описания объектов ApproveRequest

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-08 16:12:39

104.6.3
---

  * Вторая пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-08 14:33:01

104.6.2
---

  * Пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-07 19:44:56

104.6.1
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4350: Добавить фильтр по дате изменения в ручки пользователей, групп, узлов
  * RULES-3041: Выводить должность в таблицу очереди запросов
  * RULES-4376: В отчёт по ролям добавить тип группы, если роль выдана на группу

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4230: Не ставлю ненужных задач
  * RULES-4230: Запретил префетчинг тасок
  * RULES-4230: Хардкор-отладка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-07 19:25:02

104.5.1
---

  * Пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-06 20:01:15

104.5
---

  * RULES-4337: Проверять сертификат только при наличии \_requester

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2016-12-06 17:13:26

104.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4297: Отпилить синхронизацию кастомных групп из ABC
  * RULES-4381: Закрасить неиспользуемые ручки testapi

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4337: Проверять сертификат только при наличии \_requester

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-06 13:07:53

104.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4378: Оптимизировать выгрузку для firewall

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4213: Присылать на фронт дату в UTC

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-02 20:30:20

104.2
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4352: Добавить фильтр по value-узлам в ручке узлов
  * RULES-4351: Научиться в ручке узлов отдавать узлы всех систем

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4371: Отдать ресурсы пользователей и групп в v1

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-01 20:26:00

104.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4195: Английские названия групп в англоязычном интерфейсе на странице пользователя
  * RULES-4195: Английские названия систем в англоинтерфейсе

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4337: Проверять сертификат только при наличии \_requester

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-30 17:33:26

104.0
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * 'RULES-4300: Добавить данных в таблицу запросов

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4195: Обновил версию django-tanker
  * RULES-4195: Поправил баг с непереведённым описанием системы
  * RULES-4195: Поправил тест, упавший из-за некорректного перевода
  * RULES-4195: Заменил во всём проекте (кроме шаблонов) использование system.name на system.get\_name
  * RULES-4195: Удалил лишние и неиспользуемые фильтры и теги
  * RULES-4195: Поправил шаблоны: заменил system.name на system.get\_name, |username на |who
  * RULES-4195: Поправил проблему с шапкой/подвалом plain text писем

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-30 12:23:51

103.11.1
---

  * Пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-08 14:13:39

103.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4230: Не ставлю ненужных задач
  * RULES-4230: Запретил префетчинг тасок
  * RULES-4230: Хардкор-отладка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-07 19:35:47

103.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4378: Оптимизировать выгрузку для firewall

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-12-05 14:03:01

103.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4230: Проставляем last\_sync\_at после синхронизации

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-29 14:04:00

103.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4195: Обновить переводы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-28 18:08:19

103.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4230: Ошибки в названиях очередей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-24 21:19:31

103.6
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4078: При синхронизации ролей в экшены не проставляется система

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4262: Можно запросить 2 одинаковые роли с 1 формы запроса
  * RULES-4230: Правки админки
  * RULES-4329: Не выводится английское название системы на странице списка
  * RULES-4328: Запретил не вводить английское название для системы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-24 19:43:29

103.5
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4078: При синхронизации ролей в экшены не проставляется система
  * RULES-4078: Падают тесты на MySQL
  * RULES-3989: Выводить информационное сообщение при запросе роли

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4308: Нет ответственных у некоторых сервисов
  * RULES-4230: Переделал схему запуска периодических синхронизаций
  * RULES-4230: Разобраться с очередями celery

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-23 19:41:51

103.4
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4298: Доработать NodeWrapper

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Revert RULES-3890: Оптимизировать саджест при работе с большими деревьями

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-22 17:11:31

103.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3890: Удалил сортировку, из-за которой всё падало на MySQL

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-18 18:32:09

103.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3890: Оптимизировать саджест при работе с большими деревьями
  * RULES-4074: Зафиксировал тестом ответ статусом 'approved' при автоаппруве
  * RULES-3890: Поменял подход к саджесту, чтобы избежать использования group by
  * RULES-3890: Добавил переиндексации в крон
  * RULES-3890: Миграции

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-18 17:04:47

103.1
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-3799: Подсчёт количества строк в таске, а не при запросе
  * RULES-4097: Системы без ролей в firewall
  * RULES-3534: Workflow не работает при определённом порядке аппруверов
  * RULES-3801: Сделать в отчётах по ролям фильтр «sox-системы»

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-17 13:46:39

103.0
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4275: Новая версия mysqlclient
  * RULES-4205: Дефолтное сообщение об ошибке для AccessDenied()
  * RULES-4281: Сортировка по id группы в membership
  * RULES-4218: Фильтр по нескольким id в ручке ролей
  * RULES-4227: 404 а не 500 при запросе к несуществующей группе

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-14 16:44:58

102.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4279: 400 при починке системы
  * RULES-4280: Более аккуратное удаление cgroup

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-10 17:09:31

102.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4163: Добавить id в поля запроса к системе add-role
  * RULES-4163: Миграции для нового плагина

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * RULES-4267: Новые версии pillow и lxml

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-10 15:30:08

102.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4253: Не работает перевод роли по "state":"requested" в api/v1

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-07 20:31:26

102.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4229: В групповом воркфлоу метод systemify тоже должен быть доступен

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-07 13:35:26

102.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4220: Пересчет подтверждающих
  * RULES-4229: Добавить в workflow метод systemify

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-11-02 16:17:59

102.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * TOOLSADMIN-3734: sleep 1, чтобы задачи успевали остановиться
  * RULES-4192: Починка упавшего теста
  * RULES-4178: Задача должна выполняться на том хосте, на котором поставлена

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-26 17:29:44

102.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * TOOLSADMIN-3734: Задаём cpuset.cpus в базовом скрипте

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-24 18:58:30

102.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * TOOLSADMIN-3734: Сделал диапазон CPU зависящим от общего числа CPU
  * RULES-4178: Настроил route для задачи мониторинга, оказалось что оно не попадает в очередь по умолчанию автоматически
  * RULES-4193: Метод system.all\_users\_with\_role работает неверно при попытке обратиться к несуществующему узлу
  * RULES-4192: Метод user.all\_roles в воркфлоу сломан

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-4190: Обрабатывать в batch get параметры

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-24 17:36:29

102.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * TOOLSADMIN-3734: Добавил зависимость от cgroup-bin

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-21 17:26:40

102.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * TOOLSADMIN-3734: Ограничить потребление CPU idm-ом в продакшене
  * RULES-4178: Мониторинг yandex-tools-idm-celery не работает

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-21 17:00:10

102.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4049: При перемещении групп не срабатывает отложенный отзыв
  * При сохранении перевыбираем систему по pk, чтобы разрешить смену slug-a
  * RULES-3535: Присылать всю историю изменений workflow

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-20 11:24:12

101.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * TOOLSADMIN-3734: Ограничить потребление CPU idm-ом в продакшене
  * TOOLSADMIN-3734: Добавил зависимость от cgroup-bin
  * TOOLSADMIN-3734: Сделал диапазон CPU зависящим от общего числа CPU
  * TOOLSADMIN-3734: Задаём cpuset.cpus в базовом скрипте
  * RULES-4192: Метод user.all\_roles в воркфлоу сломан
  * RULES-4193: Метод system.all\_users\_with\_role работает неверно при попытке обратиться к несуществующему узлу
  * RULES-4178: Мониторинг yandex-tools-idm-celery не работает
  * RULES-4178: Настроил route для задачи мониторинга, оказалось что оно не попадает в очередь по умолчанию автоматически
  * RULES-4049: При перемещении групп не срабатывает отложенный отзыв
  * При сохранении перевыбираем систему по pk, чтобы разрешить смену slug-a

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-4190: Обрабатывать в batch get параметры

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-24 19:29:26

101.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3759: Перенёс проверку в метод пользователя
  * RULES-3759: Добавил несколько методов queryset и использовал их
  * RULES-3759: Перестал слать письма при переходе роли в onhold
  * RULES-3759: Дайджест про отложенные роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-17 23:22:41

101.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3843: Пара оптимизаций по памяти
  * RULES-4137: Добавить переводы в ручку /approverequests/
  * RULES-4134: Отображать в карточке правильную группу
  * RULES-4134: Отзываем группы из depriving всегда, а не только когда есть очередь
  * RULES-4132: slots=True для элементов очереди
  * RULES-4132: Немного оптимизаций
  * RULES-4132: Фиксы фетчера

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-17 09:50:14

101.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4009: Фильтр по узлу на странице неконсистентностей теперь работает так же, как на странице ролей: фильтрует не по точному совпадению, а показывает все неконсистентности связанные с узлами, нижележащими по отношению к переданному
  * RULES-4062: Удалил пермишен core.view\_inconsistencies. Завязываемся везде на core.view\_roles
  * RULES-4062: Добавил в команду idm\_sync\_permissions и функцию sync\_permissions возможность частичной синхронизации, например, только добавления или только удаления полномочий

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-11 23:57:48

101.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4103: Перезапросить отозванные роли
  * RULES-4009: 500 при фильтре неконсистентностей по ноде
  * RULES-4062: Сделать правильную проверку прав на промотр неконсистентностей
  * RULES-4109: Убрать спам на idm-notifications из-за нового корневого узла
  * RULES-4009: Переименовал названия параметров
  * RULES-4102: Перенёс логику фильтрации в менеджеры
  * RULES-4102: Доступ к групповым ролям в языке описания workflow
  * RULES-3971: В шаблоны сообщений на рассылку не пробрасывается комментарий
  * RULES-4011: Не резолвится неконсистентность из-за уволенного
  * RULES-3800: Изменил список полей в админке, добавил фильтр по признаку SOX

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-10 21:49:35

101.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4088: Починка пересмотра после поломки из-за унификации пересмотра и перезапроса

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-05 14:35:13

101.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4092: Фикс состояния активности роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-05 01:05:56

101.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4092: Перезапрашивать отозванные роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-05 00:24:20

101.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4088: Отключения пересмотра при смене подразделения
  * RULES-3800: Добавить системе признак sox

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-04 13:13:35

101.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3463: Поправил выявившиеся проблемы синхронизации

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-03 16:20:42

101.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4060: Миграции
  * RULES-3463: Убрал логику поиска наименьшего общего предка
  * RULES-3463: Переименовал model\_managers в managers для единообразия
  * RULES-3463: Добавил зависимость от attrs и описал canonical-объекты
  * RULES-3463: Удалил хешеры, специфичные для модели и упростил базовый хешер
  * RULES-3463: Фетчеры отдают canonical-объекты вместо словарей
  * RULES-3463: as\_canonical/from\_canonical методы
  * RULES-3463: Упростил структуру базовых классов
  * RULES-3463: Новая логика в моделях для поддержки работы с canonical-объектами
  * RULES-3346: Удалил класс результирующей очереди
  * RULES-3463: Новые классы очереди и элементов очереди
  * RULES-3463: Удалил apply\_* методы
  * RULES-3463: Обновил add\_*/remove\_*/change\_*/deprive методы
  * RULES-3463: Переместил функции добавления/удаления участников и перемещения группы в тестах в tests/utils
  * RULES-3463: Удалил неиспользуемую функцию
  * RULES-3463: Поправил json-клиент, чтобы он возвращал в результирующем словаре юникод
  * RULES-3463: Добавил функцию для проверки стабильности хеширования
  * RULES-3463: Все updatable-узлы теперь имеют один базовый менеджер
  * RULES-3463: Обновил API для работы с деревом ролей
  * RULES-3463: Обновил тесты в соответствии с новой логикой
  * RULES-3463: Стилевые правки
  * RULES-3463: Сбрасываем хеш при перемещении узла
  * RULES-3463: Миграции
  * RULES-3463: Переделал (ре-)хешинг, оптимизировал (кажется) число запросов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-09-30 14:34:39

100.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4102: Перенёс логику фильтрации в менеджеры
  * RULES-4102: Доступ к групповым ролям в языке описания workflow
  * RULES-4011: Не резолвится неконсистентность из-за уволенного
  * RULES-3971: В шаблоны сообщений на рассылку не пробрасывается комментарий
  * RULES-4109: Убрать спам на idm-notifications из-за нового корневого узла

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-11 14:38:54

100.6.1
---

  * Пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-06 16:30:32

100.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4103: Перезапросить отозванные роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-06 15:16:25

100.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4088: Отключения пересмотра при смене подразделения
  * RULES-4092: Перезапрашивать отозванные роли
  * RULES-4092: Фикс состояния активности роли
  * RULES-4092: Починка пересмотра после поломки из-за унификации пересмотра и перезапроса
  * RULES-4060: Миграции
  * RULES-4100: Убрать логику поиска наименьшего общего предка при синхронизации групп

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-10-05 15:51:16

100.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4060: При переносе поддерева теряется право ответственного за ноду

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-09-28 11:34:21

100.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-4005: Не пятисотить на перезапрос роли, если подтверждающий уволен

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * Исправлено логирование перемещения узлов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-09-21 15:15:44

100.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3903: Сортировка по user, group, subject
  * RULES-3969: Не отдаём human/human\_short во вложенные объекты node в frontend api
  * RULES-3960: Неправильная сортировка на вкладке запросов изменения воркфлоу

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-09-08 18:05:13

100.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3942: Валидатор sudo падает на русских буквах
  * RULES-3966: Неконсистентность type=we\_have\_system\_dont не отображается при фильтре по пользователю

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3827: Перенос поддерева ролей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-09-07 13:38:37

100.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3891: Синхронизация CAuth падает из-за неверной строки формата
  * RULES-3939: Ошибка при запросе роли в CAuth
  * RULES-3939: Записываем в экшены робота, который модифицирует дерево
  * RULES-3947: Письмо об отклонении запроса роли на рассылку
  * RULES-3905: Переименовал файл тестов для консистентности
  * RULES-3905: Ручка для саджеста состояний неконсистентности
  * RULES-3904: Ручка для саджеста по типам неконсистентностей
  * RULES-3903: Ручка неконсистентностей
  * RULES-3903: Улучшил обработку имперсонирования
  * RULES-3903: Добавил возможность фильтрации по username/group\_id без указания, что это – username или group\_id

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-09-01 20:21:17

99.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3942: Валидатор sudo падает на русских буквах
  * RULES-3947: Письмо об отклонении запроса роли на рассылку

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-09-06 14:38:41

99.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3939: Ошибка при запросе роли в CAuth
  * RULES-3939: Записываем в экшены робота, который модифицирует дерево

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-29 22:59:30

99.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3891: Синхронизация CAuth падает из-за неверной строки формата

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-26 18:35:18

99.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3930: Обрабатывать в API названия полей и алиасов в виде строк, а не вложенных словарей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-25 20:21:36

99.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3891: Синхронизация узлов дерева CAuth падает с ошибкой, если ответственный за хост увольняется во время синхронизации
  * RULES-3914: Поправил ворнинг gettext-а
  * RULES-3914: Изменил настройку танкера, чтобы получить ключ в качестве исходного текста для перевода
  * RULES-3914: Обновил po-файлы
  * RULES-3914: Нет переводов для статусов Импортирована, Ожидание, Передана в систему

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-25 18:08:47

99.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3741: Не отправлять уведомления о ролях при выходе из группы, если роль в системе остается активной
  * RULES-3918: Не хватает данных в выгрузке пользователей
  * RULES-3921: Убрать алиасы из саджеста ролей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-24 18:01:24

99.6
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-3387: Улучшить логирование в тасках

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3889: Синхронизация узлов: изменить формулировку в попапе
  * RULES-3891: Синхронизация узлов дерева CAuth падает с ошибкой

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-22 17:22:43

99.5
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3788: Переименовать Управлятор в IDM на беке

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3817: Система получала 502 при обращении к ручкам idm
  * RULES-3838: Поправить письмо про существующий логин
  * RULES-3783: В api-ручках научиться при limit=0 отдавать счётчики количества
  * RULES-3252: Скрипт yandex-tools-idm-celery не останавливает celery
  * RULES-3880: Поломка Управлятора из-за неудалившихся ответственностей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-19 16:33:58

99.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3837: Разрешить в диагностике дергать ручки сломанных систем
  * RULES-3857: Обновить версию pytz
  * RULES-3798: Команда idm\_check\_and\_resolve с check\_only=true не создает неконсистентности
  * RULES-3866: Научиться обрабатывать случаи, когда руководитель и зам — один человек.
  * RULES-3862: Добавить дополнительные текcтовые поля в ручки действий
  * RULES-3842: Дубликаты узлов дерева

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-16 16:52:55

99.3
---

  * RULES-3487: Удалить System.contacts
  * RULES-3755: В информацию о системе отдавать участников команды
  * RULES-3735: Плохое отображение AnyApprover
  * RULES-3742: Отображать ответственных за ноду в админке
  * RULES-3709: Брать название системы для ручки /systems/ с учётом локали
  * RULES-3695: Отдавать в ручке про группу заместителей её руководителя
  * RULES-2137: Отказаться от работы с паспортными паролями

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2016-08-04 13:17:51

99.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2327: Вернул случайно перезатёртый consumer

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-26 13:58:30

99.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2327: Поправил манифест и удалил из конфига удалённый контекст-процессор

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-26 12:37:29

99.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2327: Выбросил ycssjs
  * RULES-2327: Выбросил неиспользуемый код
  * RULES-2327: Переименовал rules
  * RULES-2327: Переименование upravlyator в idm
  * RULES-2327: Переименовал мета-информацию
  * RULES-2327: Переименовал upravlyator\_tags в idm\_tags
  * RULES-2327: Добавил db\_table везде
  * RULES-2327: Вынес админку testenv в сам testenv
  * RULES-2327: Удалил неиспользуемые шаблонные теги
  * RULES-2327: Удалил неиспользуемую функцию для работы с changelog-ом
  * RULES-2327: Создание приложения core
  * RULES-2327: Перенёс database backend в приложение framework
  * RULES-2327: Перенёс базовый класс админки в framework
  * RULES-2327: Перенёс миксины в framework
  * RULES-2327: Перенёс базовый класс задачи в framework
  * RULES-2327: Выделил приложение core и перенёс в него таски, workflow, плагины, management-команды, шаблоны и шаблонные теги
  * RULES-2327: Вынес общую функцию из management-команд в splunk.py
  * RULES-2327: Поправил импорты
  * RULES-2327: Перенёс миграции
  * RULES-2327: Миграции
  * RULES-2327: Удалил контекcт-процессоры
  * RULES-2327: Перенёс Requester в framework
  * RULES-2327: Перенёс mail backend в notifications
  * RULES-2327: Сделал метод pending\_approve\_requests методом ApproveRequestManager-a
  * RULES-2327: Запихнул middleware во framework
  * RULES-2327: Перенёс splunk в утиль

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-25 22:06:47

98.21
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3891: Синхронизация узлов дерева CAuth падает с ошибкой
  * RULES-3252: Скрипт yandex-tools-idm-celery не останавливает celery
  * RULES-3880: Поломка Управлятора из-за неудалившихся ответственностей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-22 17:37:01

98.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3817: Система получала 502 при обращении к ручкам idm

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-17 09:56:27

98.19
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3842: Дубликаты узлов дерева

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-16 16:28:42

98.18
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3866: Научиться обрабатывать случаи, когда руководитель и зам — один человек.

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-12 15:54:06

98.17
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3837: Разрешить в диагностике дергать ручки сломанных систем

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-08-09 15:55:39

98.16
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3796: Разобраться с синхронизацией вики-групп

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-29 09:29:01

98.15
---

  * RULES-3809: Ломается API над нодами при наличии ответственных

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-28 13:54:37

98.14
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3794: Забытый импорт

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-26 18:46:26

98.13
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3794: Показываем свои роли в CAuth для любого пользователя
  * RULES-3796: Разобраться с синхронизацией вики-групп

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-26 18:32:24

98.12
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3768: Участник команды системы не может запросить подтверждение изменения воркфлоу

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3670: Добавил аргумент since в команду синхронизации, который отзывает группы, как если бы текущее время было равно since
  * RULES-3670: Включил предобработку для argparse-based команд, запускаемых через testapi
  * RULES-3670: Не продляем depriving бесконечно

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-21 16:48:50

98.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3657: Синхронизация должна падать, если нужно добавить участником или ответственным пользователя, которого мы ещё не забрали со Стаффа

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3767: Неправильное описание типа идентификации неконсистентности

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-21 14:24:39

98.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3723: Убрал тестовый костыль
  * RULES-3723: Нет сообщения об ошибке выдачи роли в режиме read only
  * RULES-3723: Поменял порядок middleware, выбросил ненужную нам WaffleMiddleware, отказался от LocaleMiddleware в пользу I18NMiddleware
  * RULES-3723: Изолирую тесты друг от друга: раньше они могли иметь общий кеш
  * RULES-3723: Стал прогонять middleware для HTTP-подзапросов
  * RULES-3597: Ссылки на тестинги staff и abc из тестинга и дева IDM
  * RULES-3753: Поправить обработку email'ов в wf cauth

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-20 13:17:06

98.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3733: На экране диагностики дефолтно выбирать сертификат и библиотеку, прописанные в системе
  * RULES-3690: Письмо про наличие неконсистентностей не содержит подробностей про отсутствующие узлы
  * RULES-3510: Доработал команду, удаляющую данные

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-19 11:04:45

98.8
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3560: Участник команды не может отзывать роли
  * RULES-3712: Потеряли rehash и проверку на неответ системы при переезде на новые ручки

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3569: Поправил падавший на MySQL тест
  * RULES-3510: Изменил импорты
  * RULES-3510: Ответственные за ноду
  * RULES-3510: Отфильтровываем внутренние роли на узлы с ответственностями из get-all-roles
  * RULES-3510: Добавил защиту для ручки add-role
  * RULES-3510: Удалил функцию create\_role\_node\_structure, которая дублировала существующую функциональность
  * RULES-3510: Поправил тесты на воркфлоу CAuth
  * RULES-3510: Добавил тест на обнаруженный баг в обработке флага notify
  * RULES-3510: Добавил удаляющую роли в CAuth одноразовую команду и тест на неё
  * RULES-3729: Не работает фильтр по ключевому слову
  * RULES-3628: Поправил неопределённость, из-за которой падал один тест
  * RULES-3628: Удалил неиспользуемые настройки
  * RULES-3628: Удалил DeletableNode, в проекте оно не используется, а только мешает
  * RULES-3628: Поправил API групп: отдаём единый ключ 'name', который зависит от языка пользователя
  * RULES-3670: Удалять группу не сразу
  * RULES-3628: Добавил флаг для принудительного отзыва depriving групп и поправил падавший тест
  * RULES-3628: Удалил хак для MPTT
  * RULES-3628: Перенёс метод apply() в элементы очереди, упростил код
  * RULES-3628: Обрабатываю случай, когда группа сначала пропала, а потом появилась в другом месте
  * RULES-3628: Устранить мигание персональной роли
  * RULES-3628: Перестал указывать в данных роли, какое членство привело к её выдаче
  * RULES-3628: Миграция
  * RULES-3572: Забытая миграция

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-14 11:23:33

98.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3685: Функция does\_have\_role падает с ошибкой
  * RULES-3703: Заменить заголовок диффа узлов с h1 на h3. + удалил неиспользуемые части шаблона и инлайновые стили
  * RULES-3569: Починил запуск синхронизации ролей
  * RULES-3716: Для случая ошибки коннекта выводим undefined

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-13 00:22:22

98.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2216: Вернул STATIC\_URL, без которого плохо админке

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-11 13:37:32

98.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3676: Не отзываем роли в onhold по истечении трёх дней
  * RULES-3676: Добавил в action комментарий, если роль выдаётся или отзывается без оповещения системы.
  * RULES-3689: В карточке запрошенной роли отображать только те OR-группы, от которых действительно требуется подтверждение

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2216: Удалить остатки старых отчетов
  * RULES-3575: Отдавать переводы статуса ролей
  * RULES-3641: Удалить старые ручки системы
  * RULES-3641: Убрал лего
  * RULES-3669: Переключать язык на беке из данных ЧЯ

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-11 12:44:37

98.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3620: Не отрывается 67 сид у бывших сотрудников
  * RULES-3673: Добавил логгирования для отладки поломки Кондуктора

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-06 15:40:57

98.3
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1434: Ручки для экрана диагностики
  * RULES-1434: pep8
  * RULES-3643: Обновить django\_yauth до 3.56
  * RULES-3643: pep8
  * RULES-3572: Вернуть waffle и через него переключать RO режим
  * RULES-3660: Убрать заголовок Content-Type из ручки про изменения дерева
  * RULES-3599: Операция recover у системы

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3647: Допинывалка отзывает роли в статусе "Отложена"
  * RULES-3612: Письмо о поломке не содержит подробностей о неконсистентностях на стороне системы
  * RULES-3612: Не включаем систему в отчёт, если в ней нет неконсистентностей
  * RULES-3612: Отсылаем сообщения о поломке в системе на рассылку системы
  * RULES-3612: Вернул глобальный lock на команду
  * RULES-3612: Отрефакторил команду, чтобы разрешение неконсистентностей не запускалось, если при проверке системы были проблемы
  * RULES-1434: Поправил падающий тест
  * RULES-3665: Допинывалка ролей ломается на выключенной системе

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-05 20:49:18

98.2
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3569: Ручки для экрана синхронизации

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-04 13:52:23

98.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3597: Генерировать внешнюю ссылку на группу

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-01 14:33:54

98.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3570: Убить страницу с переименованными подразделениями
  * RULES-3571: Убить экраны нотификаций
  * RULES-3598: Саджесты для экрана диагностики

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3605: Не выгружается отчёт по изменениям workflow в xls
  * RULES-3286: Разрешить заместителям запрашивать роль для подчинённых

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-30 15:46:10

97.14.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3676: Не отзываем роли в onhold по истечении трёх дней
  * RULES-3676: Добавил в action комментарий, если роль выдаётся или отзывается без оповещения системы.

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-07 16:33:55

97.13.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3612: Письмо о поломке не содержит подробностей о неконсистентностях на стороне системы
  * RULES-3612: Не включаем систему в отчёт, если в ней нет неконсистентностей
  * RULES-3612: Отсылаем сообщения о поломке в системе на рассылку системы
  * RULES-3612: Вернул глобальный lock на команду
  * RULES-3612: Отрефакторил команду, чтобы разрешение неконсистентностей не запускалось, если при проверке системы были проблемы
  * RULES-3665: Допинывалка ролей ломается на выключенной системе
  * RULES-3620: Не отрывается 67 сид у бывших сотрудников
  * RULES-3673: Добавил логгирования для отладки поломки Кондуктора
  * RULES-3647: Допинывалка отзывает роли в статусе "Отложена"

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-07-06 16:29:59

97.12.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3605: Не выгружается отчёт по изменениям workflow в xls

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-30 14:43:42

97.11.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3594: Ломается админка при поиске по неконсистентностям
  * RULES-3579: Убрал DISTINCT, вернул подзапрос
  * RULES-3579: Добавил индексов для аппрувреквестов и узлов дерева ролей
  * RULES-3579: Раскрыл подзапросы в список айдишников
  * RULES-3579: Перестал использовать хинтинг

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-27 17:02:24

97.10.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3574: Плохая ссылка в письме про отзыв роли
  * RULES-3484: Убрать логику подсчета номера страницы для роли/действия
  * RULES-3574: Имя сотрудника в письме об отзыве роли

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3432: Корректно обрабатываем случай отсутствия автора или подтверждающего

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-23 16:35:06

97.9.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3513: Забытая миграция

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3433: Поменять шаблоны уведомлений на рассылку

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-23 11:37:02

97.8.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3565: Сломан режим silent в обновлении дерева ролей
  * RULES-3417: Добавить в пользователя ссылку на департаментную группу
  * RULES-3328: Использовать группы во внутренней логике определения прав
  * RULES-3417: Переделал запрос с подзапросов на один большой JOIN

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-22 20:36:09

97.7.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3513: Обошёл ограничения MySQL

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-22 18:27:57

97.6.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3532: Нет кнопки Отозвать у роли в onhold

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3434: Учёл возможность рассинхронизации данных
  * RULES-3513: Поправил фикстуру, которая создавала ситуацию, которой в реальной жизни не должно случаться и этим мешала
  * RULES-3513: В ручку membership по человеку отдавать все группы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-22 17:55:03

97.5.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3432: Удалил неиспользуемый класс
  * RULES-3432: Добавить данные в отчёт по изменениям workflow
  * RULES-3434: Синхронизировать кастомные роли из ABC: Баг с несовпадением slug-ов в staff api и plan api

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-21 10:30:35

97.4.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3436: Удалил смущающие initial
  * RULES-3436: Удалил лишнее
  * RULES-3436: Добавил в API возможность задать unique\_id
  * RULES-3436: Не удалять роли при перемещении узла
  * RULES-3538: Добавлять в action починки системы того, кто починил
  * RULES-3544: Не работает блок проверки worfklow

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3515: Фильтр по типу группы в ручке групп человека - мультивыбор
  * RULES-3498: В отчёт по ролям системы добавить данные - групповые роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-17 17:35:13

97.3.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3434: Синхронизировать кастомные роли из ABC
  * Добавил возможность запустить тесты под профайлером
  * RULES-3533: Добавить expire\_at в список полей /api/testapi/roles/{role\_id}/

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3498: улучшен импорт
  * RULES-3498: В отчёт по ролям системы добавить данные

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-16 12:29:11

97.2.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3445: Больше логгирования для тестинга
  * RULES-3445: USE INDEX ('primary') для Count-запросов
  * RULES-3445: Оптимизация медленного OR-а
  * RULES-3445: Индексы для ускорения выборок
  * RULES-3445: Фикс длинного запроса
  * RULES-3445: Оптимизация бутылочного горлышка

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3515: Фильтр по типу группы в ручке групп человека
  * RULES-3523: Добавить саджест по типам групп

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-14 14:55:39

97.1.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2970: Не отзывать персональную роль при выходе из группы
  * RULES-2970: префикс IDM для констант
  * RULES-3505: Добавить ручку /actions в api v1
  * RULES-3508: Поддержать фильтр по нескольким группам в /api/frontend/membership

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Up middle digit in version by default

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-10 15:17:43

97.0.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2848: Отправлять ссылку на карточку роли в письмах
  * RULES-2848: домен в настройках
  * RULES-2484: template tag
  * RULES-3388: Проставлять membership/responsibility в action-ах входа/выхода в группу
  * RULES-3507: Сделать саджест по группам

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2848: Фикс тестов на MySQL
  * RULES-3507: Добавил метод get\_name к группе

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-09 22:14:53

0.96.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3504: Вызов отчетов без фильтров на почту ломает управлятор

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3302: суперюзер может применять свои изменения

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-07 18:52:31

0.96.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3431: Фикс миграции-2
  * RULES-3495: Добавить поля в select\_related
  * RULES-3497: Проблема с кодировкой при форматировании ошибки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-06 20:43:21

0.96.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3431: Фикс миграции
  * RULES-3401: Фильтр "персональные роли" применяется и в group-aware системах
  * RULES-3461: Учитывать алиасы ноды при фильтрации ролей

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3481: Фильтр по id в ручке действий
  * RULES-3480: Фильтр по id в ручке ролей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-06 15:57:09

0.96.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3446: Если политика системы – "не пересматривать роли при перемещении групп", то роли не перемещаются вместе с группой
  * RULES-3474: Сейчас в тестинге не запрашивается роль. Выдаём всегда on\_page=1, чтобы не выполнять сложный запрос на мастере после запроса роли
  * RULES-3477: Не открывается карточка роли
  * RULES-3477: Изменил порядок миграций

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3421: Некрасиво пятисотит GET /api/frontend/rolerequests/
  * RULES-3416: В ресурсе система брать ответственных из ролей
  * RULES-3431: Поправить date\_leaved в членствах групп

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-03 15:19:34

0.96.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3169: Протекают внешние логины с точкой при синхронизации
  * RULES-3458: Поддержать \_requester'а в POST'е роли
  * RULES-3444: Отпилить проверку на уволенность в уведомлениях

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-06-01 15:44:32

0.96.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3402: Если при запросе роли в системе с необязательным наличием паспортного логина указать существующий, но ничего не выбрать - роль запросится с "system\_specific":{"passport-login":""}
  * RULES-3412: Ошибка при выдаче роли в Метрике. This reverts commit 1d0694
  * RULES-3423: Плохо синхронизировались поля в CAuth
  * RULES-3423: Добавил хелпер для логгирования времени выполнения произвольного блока кода
  * RULES-3423: Упростил код синхронизации, использовал start\_stop\_actions, стал проставлять parent в action-ах аналогично синхронизации ролей
  * RULES-3423: Перестал пробрасывать пользователя в функцию отзыва ролей, выданных на удалённые узлы
  * RULES-3401: Не создавать персональные роли для aware систем
  * RULES-3456: Добавить команду, которая удаляла бы всю информацию о системе

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3302: Запретить применять свои изменения в воркфлоу
  * RULES-3396: Если у роли is\_public=false, то дату регулярного пересмотра в карточке этой роли не надо отображать
  * RULES-3425: Лишние сотрудники в  департаментных группах - команда для фикса
  * RULES-3425: Лишние сотрудники в  департаментных группах - тест на отзыв членства

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2021: Рефаторинг ручки /meta
  * RULES-3410: Добавить поддержку множественного выбора в ручку /api/frontend/membership/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-06-01 13:05:18

0.96.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3392: Видно число связанных ролей в карточке основной роли, если среди связанных только роль с visability=false
  * RULES-3391: При запросе роли с visability=false через связанную отправляется письмо
  * RULES-3308: Перенести логику TransitionResource в ресурс роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-05-25 18:03:38

0.95.29
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3477: Изменил порядок миграций

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-03 14:37:08

0.95.28
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3474: Сейчас в тестинге не запрашивается роль. Выдаём всегда on\_page=1, чтобы не выполнять сложный запрос на мастере после запроса роли
  * RULES-3477: Не открывается карточка роли

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-06-02 18:57:34

0.95.27
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3401: Не создавать персональные роли для aware систем
  * RULES-3423: Плохо синхронизировались поля в CAuth
  * RULES-3423: Добавил хелпер для логгирования времени выполнения произвольного блока кода
  * RULES-3423: Упростил код синхронизации, использовал start\_stop\_actions, стал проставлять parent в action-ах аналогично синхронизации ролей
  * RULES-3423: Перестал пробрасывать пользователя в функцию отзыва ролей, выданных на удалённые узлы
  * RULES-3456: Добавить команду, которая удаляла бы всю информацию о системе

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-05-31 16:29:45

0.95.26
---

  * RULES-3425: Лишние сотрудники в  департаментных группах - команда для фикса

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2016-05-27 14:14:49

0.95.25
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3412: Ошибка при выдаче роли в Метрике. This reverts commit 1d0694

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-05-26 12:51:53

0.95.24
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3017: Привязать все роли к нодам: правки для хотфикса

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-05-24 19:25:37

0.95.23
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3166: руководители сервисов

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3370: Лишние роли на основе групповой
  * RULES-3370: .* вместо .id, чтобы избежать defer-like поведения и лишних запросов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-24 13:27:18

0.95.22
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3100: Удалил TODO: for\_update
  * RULES-3100: Убрал for\_update везде
  * RULES-3100: Удалил for\_update везде в тестах

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3369: Падает рендер экшена
  * RULES-3368: Ошибка в работе с алиасами нод в /api/v1

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-23 17:36:21

0.95.21
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-3100: отключил команду idm\_check\_roles\_ttl\_days
  * RULES-3166: просим у API Планера поле is\_senior

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3379: Вынести запрос связанных ролей в отдельную таску

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-20 20:32:36

0.95.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3373: Перенёс создание хешей из миграции в oneoff-команду
  * RULES-3384: Починить RoleAsNode

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3347: не приходят отчеты на почту

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-20 15:36:39

0.95.19
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3166: фикс работы с ids api
  * RULES-3354: Обновить ids

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3360: Сломалась логика сверки связанных ролей
  * RULES-3100: Поправил тест, падающий из-за отсутствия update\_fields
  * RULES-3373: Сделать отдельную таблицу с хешами ролей
  * RULES-3374: Не приезжают данные в таблицу ролей: попытка демаскировки причины ошибки

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-3370: Лишние роли на основе групповой

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-19 23:18:12

0.95.18
---

  * RULES-3100: убрал save по умолчанию всех полей роли
  * RULES-3372: Выводить traceback в ошибках бека всегда

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-19 15:41:44

0.95.17
---

  * RULES-3100: убрал select\_for\_update() везде кроме oneoff команд

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-19 13:13:25

0.95.16
---

  * RULES-3100: увеличил до 16 пул воркеров очереди roles
  * RULES-3100: помечаем отзываемую роль for\_update

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-19 01:27:31

0.95.15
---

  * RULES-3371: Убрать констрейнты FK у неконсистентностей
  * RULES-3100: Ещё убираем for\_update, чтобы диагностировать причину дедлоков

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-19 01:13:46

0.95.14
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3100: Временно убрал for\_update, чтобы диагностировать причину дедлоков

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-05-18 20:05:02

0.95.13
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3100: Добавил задачу в нужную очередь
  * RULES-3100: Отчёты только для активных систем
  * RULES-3100: Поправил падающий тест
  * RULES-3355: Создаём отчёты только для generic-plugin систем
  * RULES-3100: Per-system локи для поиска и разрешения неконсистентностей
  * RULES-3363: При ночном прогоне стала зависать команда idm\_check\_approvers\_difference
  * RULES-3100: Понижение уровня изоляции транзакций до READ COMMITTED
  * RULES-3355: Поправил неверный фильтр, который ломал тесты

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3353: Команда idm\_sync\_groups падает с ошибкой

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-05-18 19:20:23

0.95.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3100: Убрал глобальный атомик

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-05-18 13:15:02

0.95.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3356: Поддержал в бекенде композитные индексы по текстовым полям. Код скопирован из базового класса, так как толком переопределить это место нельзя

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-05-17 21:31:57

0.95.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3100: Дедлоки при запросе внутренней роли
  * RULES-3100: Переписал синхронизацию с хранимой процедуры на SQL-операторы в коде
  * RULES-3100: Удалил фикстуру, загружающую хранимые процедуры
  * RULES-3355: idm\_check\_and\_resolve отдает 502 через 5 минут при запуске с check\_only:true
  * RULES-3356: Сделать индексы для использования в синхронизации

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3352: Несуществующая команда отдает 200 и в ответе пишет error

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-05-17 21:02:48

0.95.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3348: Объединил команды idm\_check\_roles и idm\_resolve\_inconsistencies, чтобы они работали под общим локом
  * RULES-3348: Удалил поле is\_active у MatchingRole (оно было не очень нужно), с остальных полей снял db\_constraint
  * RULES-3348: MatchingRole не коммитятся, поэтому не стоит иметь их в админке

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-16 17:44:50

0.95.8
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3272: Фильтруем очередь запросов по параметру approver
  * RULES-3336: Падает синхронизация сервисный групп

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-3232: фикс валидации формы участников групп
  * RULES-3345: Атомарные транзакции при изменении дерева

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-13 16:05:17

0.95.7
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2942: Плейсхолдеры для полей ролей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-06 18:55:58

0.95.6
---

  * RULES-2526: фикс фильтрации узлов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-06 02:17:54

0.95.5
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3277: Считать hash для узлов добавленных через API

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3018: Большая миграция, удаляющая поля

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2526: Обрабатывать фильтр по ключевым словам в роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-06 00:37:32

0.95.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3017: Привязать все роли к нодам
  * RULES-3291: Оптимизировать поиск дубликатов ролей
  * RULES-3018: Избавиться от поля data в ролях
  * RULES-3018: Подчистил после неконсистентностей
  * RULES-3018: Удалил response\_to\_json
  * RULES-3018: Миграции: data теперь nullable + индекс по fields\_data
  * RULES-3232: Поменял значение по умолчанию

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-05 18:10:38

0.95.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3232: В ручке membership отдавать дочерние членства
  * RULES-3217: Поправил миграции, чтобы проставить inconsistency\_id=NULL у Action-ов с некорректными inconsistency\_id

 * [Andrey Bulgakov](https://staff.yandex-team.ru/Andrey%20Bulgakov)

  * RULES-3172 Починка и оптимизация миграций
  * RULES-3170 Избавляемся от many-to-many в коде

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-3331: Перестали прокидывать токен в запрос за отсутствиями

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-05-04 23:25:19

0.95.2
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ULES-3312: Не использовать Department для проверки прав

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2967: Сортировать по роли в таблице нужно сначала по названию узла роли, а затем по id, если узлы одинаковые
  * RULES-3258: проверка базового урла
  * RULES-2856: Отдавать версию и ro состояние в каждой ручке API
  * RULES-3285: Тормозит синхронизация со Стаффом

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2165: Запретить создавать групповую роль на саму себя
  * RULES-3316: Механизм разрешения неконсистентностей не ломает систему, когда неконсистентностей много и если среди них есть неконсистентности и о пользователе, и о роли
  * RULES-3313: Время создания неконсистентностей для одного события отличается на 3 часа

 * [Andrey Bulgakov](https://staff.yandex-team.ru/Andrey%20Bulgakov)

  * RULES-3170 Замена MPTT на CTT

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-04-29 19:26:09

0.95.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3217: Удалять неконсистентности при синхронизации
  * RULES-3217: Миграции
  * RULES-3271: Сихронизация ролей, выданных на основе групповой
  * RULES-3305: Нужна возможность видеть и менять ноду у роли в testapi

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3257: Добавить опцию вызова ручки без сертификата в дёргатель ручек
  * RULES-3292: Сделать поле scope обязательным у системных ролей
  * RULES-3258: Сделать команду, проверяющую проверку системами сертификата
  * RULES-2855: Поддержать фильтр по сломаности в ручке систем
  * RULES-3237: Поменять ссылки в письмах

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-04-27 17:59:20

0.95.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3052: Деинсталляция приложения reversion и связанных компонентов
  * RULES-3150: Форма запроса роли для системы CAuth сейчас сильно тупит
  * RULES-3288: Не показываем руководителя, если он не непосредственный
  * RULES-2379: Ускорить синхронизацию ролей

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2168: Флаг активности и дата в групповых членствах
  * RULES-2169: Не удалять старые групповые членства
  * RULES-2131: Ручка по составу группы
  * RULES-3166: Поддержать ответственных сервисных групп и ролевых подгрупп
  * RULES-3264: Обрабатывать несколько действий из фильтра
  * RULES-3266: Обрабатывать несколько наборов ролей из фильтров

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-04-25 14:21:35

0.94.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Починил вывод сломанных систем на старом фронте и поменял цвет
  * Revert "RULES-2965: Обрабатывать удаленные группы"

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-04-21 14:42:35

0.94.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3247: Добавить в админку параметр ручки
  * RULES-2919: Миграция для переименования планерной группы в сервисную
  * RULES-3052: Удалить reversion артефакты из базы

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2965: Обрабатывать удаленные группы

 * [Andrey Bulgakov](https://staff.yandex-team.ru/Andrey%20Bulgakov)

  * RULES-3171 ClosureTable для древовидных моделей и процедура-миграция

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-04-20 19:38:09

0.93.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3247: Добавить в админку параметр ручки

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-04-18 12:28:02

0.93.7
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3174: добавочные фильтры по id

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-04-14 16:55:49

0.93.6
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3174: Дополнительный параметр саджеста для предзаполнения контрола

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-04-14 14:14:24

0.93.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3178: Таски должны ретраиться при отсутствии Action

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1839: fix handles view

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2016-04-12 19:02:33

0.93.4
---

  * RULES-1839: curl и requests по выбору
  * RULES-3183: Ошибка записи в лог при запросе роли

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2016-04-12 18:06:42

0.93.3
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-3128: Убрать stats счетчики из ручки ролей + RULES-3124

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3031: Убить /exists и /queue саджесты
  * RULES-3194: Добавить флаг is\_favorite в ручку системы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-04-08 17:48:13

0.93.2
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3006: Передавать список избранных систем
  * RULES-3006: get rid of AUTH\_USER\_MODEL

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-04-01 14:35:38

0.93.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3117: Не запрашиваются некоторые роли
  * RULES-2516: Убрал неиспользуемые импорты
  * RULES-2516: Инструменты для дергания новой ручки
  * RULES-2516: Перенёс тесты неконсистентностей в один каталог
  * RULES-2516: Убрал бесполезную теперь фикстуру simple\_system\_w\_meta
  * RULES-2516: Новая ручка get\_roles со списком ролей
  * RULES-3150: Форма запроса роли для системы CAuth сейчас сильно тупит

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-3132: Убрать deprecated роли в IDM

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2919: Синхронизировать ролевые подгруппы сервисов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-31 16:21:56

0.93.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1839: Оставить по возможности только requests
  * RULES-3049: Не отзываем роли у удаленных групп
  * RULES-3049: fix roles depriving
  * RULES-3049: command fix
  * RULES-3109: Сделать миграцию, исправляющую историю подтверждений

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2986: Передавать тип группы в саджест
  * RULES-1839: Потеряли длинный timeout для ручек плагина
  * RULES-3118: Пользователю с атрибутом is\_staff стало нельзя попасть в админку
  * RULES-3122: Обновить yauth
  * RULES-3120: Меньше ненужных сохранений
  * RULES-3120: Обновляем только необходимые поля
  * RULES-3120: Сделать транзакции более атомарными при синхронизации
  * RULES-3120: Обновление django-idm-api до 2.2, чтобы при выдаче ролей у пользователей обновлялись только поля is\_staff и is\_superuser
  * RULES-3049: Обернул команду в транзакцию
  * RULES-3129: Из-за ошибки в crontab выключился cron
  * RULES-3100: Меньше ненужных сохранений
  * RULES-3100: Дедлоки при запросе роли
  * RULES-3100: Понижение уровня изоляции транзакций до READ COMMITTED
  * Revert "RULES-3100: Понижение уровня изоляции транзакций до READ COMMITTED": Изменение уровня изоляции транзакций требует изменения формата бинлога, что нужно тестировать и небыстро.
  * RULES-3100: Убрал select for update из всех регулярных команд, не использующих ввод пользователя
  * RULES-3100: Используем gap-lock при запросе роли через фронтэнд или API

 * [Andrey Bulgakov](https://staff.yandex-team.ru/Andrey%20Bulgakov)

  * RULES-3123 Используем mptt для поиска поддерева
  * RULES-3116 Одинаковое название required у поля при добавлении и отображении
  * RULES-3123 Индекс на slug\_path

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-28 13:33:58

0.92.14
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Revert "RULES-3100: Понижение уровня изоляции транзакций до READ COMMITTED": Изменение уровня изоляции транзакций требует изменения формата бинлога, что нужно тестировать и небыстро.
  * RULES-3100: Убрал select for update из всех регулярных команд, не использующих ввод пользователя
  * RULES-3100: Используем gap-lock при запросе роли через фронтэнд или API

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-25 17:16:19

0.92.13
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3100: Меньше ненужных сохранений
  * RULES-3100: Дедлоки при запросе роли
  * RULES-3100: Понижение уровня изоляции транзакций до READ COMMITTED

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-25 14:43:44

0.92.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3129: Из-за ошибки в crontab выключился cron

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-23 19:25:44

0.92.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3049: Обернул команду в транзакцию

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-23 17:41:30

0.92.10
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3049: fix roles depriving

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-23 17:17:48

0.92.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3118: Пользователю с атрибутом is\_staff стало нельзя попасть в админку
  * RULES-3122: Обновить yauth
  * RULES-3120: Меньше ненужных сохранений
  * RULES-3120: Обновляем только необходимые поля
  * RULES-3120: Сделать транзакции более атомарными при синхронизации
  * RULES-3120: Обновление django-idm-api до 2.2, чтобы при выдаче ролей у пользователей обновлялись только поля is\_staff и is\_superuser

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-3049: Не отзываем роли у удаленных групп

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-23 16:44:41

0.92.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3108: Увеличить лимит на странице систем до 200
  * RULES-2726: Некорректная история подтверждений-3

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-21 16:34:24

0.92.7
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2726: Некорректная история подтверждения

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-21 10:07:09

0.92.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3026: Политика работы с неконсистентностями у систем
  * RULES-3026: Реордеринг миграций

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-21 09:51:31

0.92.5
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2726: Некорректная история подтверждения

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3081: Игнорировать подтверждающих при прогоне воркфлоу при форсированном импорте ролей
  * RULES-2841: Заменил AccessDenied на отсутствие аппруверов
  * RULES-2841: Добавил строчку про невидимость связанных ролей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-17 16:59:09

0.92.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1999: Неверная строка форматирования для лога

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-16 16:55:52

0.92.3
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-3064: Роль "Редактор дерева ролей" не дает зайти на видимую вкладку "Управление ролями" - 403

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2841: Написать правильный воркфлоу для CAuth
  * RULES-3044: Добавить фильтрацию по системе в команду idm\_add\_users\_to\_ad\_groups
  * RULES-3070: Саджест внутренних ролей работает неправильно для суперпользователей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-15 23:13:14

0.92.2
---

  * RULES-3045: Убрать из /meta права и число запросов на подтверждение
  * RULES-3051: Убрать сохранение новый ревизий в reversion
  * RULES-1647: фикс миграции
  * RULES-1647: не отдает роли без пользователей в get\_all\_roles

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-11 21:58:06

0.92.1
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1647: фикс отзыва некорректной роли
  * RULES-3025: Закрасить экран splunk

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3047: Восстановил возможность запуска тестов локально на MySQL
  * RULES-3047: При запуске тестов на MySQL некоторые из них падают
  * RULES-2987: Сделать NodeWrapper для воркфлоу

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-11 13:52:04

0.92.0-1
---

  * Пересборка

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-10 16:46:43

0.92.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2853: Перестать использовать is\_superuser в логике бека
  * RULES-2834: Кастомные валидаторы для полей роли

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1999: Добавить стейт imported для ролей, созданных по неконсистентности
  * RULES-2211: Работа над ошибками
  * RULES-2960: Ручка саджеста дублирует узлы
  * RULES-3001: Делать rehash только для нужных нод
  * RULES-2853: Meta-миграция из-за изменения структуры пермишенов
  * RULES-2691: Добавил дополнительную проверку в тесте
  * RULES-2691: Добавил метод для получения имени системы на нужном языке
  * RULES-2691: Убрал все обращения к role.info
  * RULES-2691: Возвращаем при переходе созданный action
  * RULES-2691: create\_approve\_request принимает action
  * RULES-2691: Фильтрация cc на тестинге
  * RULES-2691: Новая логика проставления email\_cc
  * RULES-2691: Отправлять уведомления на рассылку
  * RULES-2691: Миграция
  * RULES-2832: Запустить пересмотр ролей в OEBS
  * RULES-2832: Запустить пересмотр ролей в OEBS: фикс

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2966: Отфильтровывать наборы скрытых ролей
  * RULES-2843: Саджест internal ролей для фильтра
  * RULES-2844: Поддержать фильтр по internal роли в ручке ролей
  * RULES-3013: Поменять брокер  Celery
  * RULES-1647: Наведение порядка во внутренних ролях Управлятора
  * RULES-2859: Ручка /permissions в API
  * RULES-2941: Оптимизировать нашу get\_all\_roles

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-10 16:26:22

0.91.13
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2832: Запустить пересмотр ролей в OEBS: фикс

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-09 18:42:55

0.91.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2832: Запустить пересмотр ролей в OEBS

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-03-09 18:09:37

0.91.11
---

  * RULES-3013: Поменять брокер  Celery

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-03 16:51:33

0.91.10-1
---

  * Убрал лишние миграции

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-01 17:49:26

0.91.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-3001: Делать rehash только для нужных нод

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-01 17:44:26

0.91.9
---

  * RULES-2972: фикс миграции

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-26 13:16:22

0.91.8
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2972: Смигрировать системные роли Управлятора

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2643: Управление уведомлениями для CAuth: применил миграцию заново

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-02-25 17:53:13

0.91.7
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2884: Локализовать название системы
  * RULES-2929: Не показывать подтверждающих при запросе подтверждающим
  * RULES-2840: Запрос связанной роли с visibility=false
  * RULES-2909: Сделать возможность отключать перезапрос ролей системы при смене подразделения
  * RULES-2120: Запрос роли для подтверждающего создает запрос
  * RULES-2917: Разрешить редактировать workflow
  * RULES-2956: Для роли в статусе review\_request не должно быть поля Будет перезапрошена

 * [Andrey Bulgakov](https://staff.yandex-team.ru/Andrey%20Bulgakov)

  * RULES-2889 Batch-ресурс

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-19 15:40:26

0.91.6
---

  * RULES-2910: вернул пока поля в саджест

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-11 18:57:47

0.91.5
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2914: Перестали автоматически разрешаться неконсистентности для тестовой системы

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2913: Неправильно выводится время пересмотра роли
  * RULES-2910: Прокидывать полные данные о полях в /rolerequestfields/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-11 17:31:31

0.91.4
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  *  RULES-2152: фикс миграции internal role

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2835: невидимые роли быстрофикс

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-10 14:06:44

0.91.3
---

  * RULES-2152: фикс названия поля в миграции

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-09 23:12:42

0.91.2
---

  * RULES-2152: фикс миграций и админки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-09 23:07:41

0.91.1
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2877: Отдавать в ручку для карточки роли поля про временную роль

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2152: Проверка прав доступа через дерево

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-09 22:47:45

0.91.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2869: Шлем уведомления по отозванным ролям
  * releasing version 0.89.13
  * RULES-2886: Допереименовать rolenodegroup в set
  * RULES-2886: Миграции
  * RULES-2900: Отправляем некорректные уведомления
  * RULES-2900: Убрал дубликат теста
  * RULES-2900: Отправляем некорректные уведомления
  * RULES-2900: Убрал дубликат теста
  * RULES-2836: Удалил AbstractSystemRole
  * RULES-1875: Проверять пользователей в блоке тестирования Workflow
  * RULES-2836: Управление уведомлениями для апруверов
  * RULES-2836: Война с \_\_repr\_\_
  * RULES-2836: Миграция для Meta

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2835: невидимые роли не отображаются в таблице
  * RULES-2835: невидимые роли не отображаются в саджесте
  * RULES-2835: невидимые роли нельзя запросить из интерфейса
  * RULES-2835: про невидимые роли не высылаются письма
  * RULES-2835: невидимые роли не пересматриваются
  * RULES-2835: невидимые роли не пересматриваются при смене подразделения
  * RULES-2835: невидимые роли может запрашивать только пользователь с правом request\_system\_roles
  * RULES-2835: невидимые роли нельзя запросить при наличии подтверждающих в workflow
  * RULES-2895: Убрать поле requester из rolerequest
  * RULES-2538: Поле запрещающее редактировать дерево ролей у системы через API

 * [Andrey Bulgakov](https://staff.yandex-team.ru/Andrey%20Bulgakov)

  * RULES-2671 Сортировка по алиасам во frontend-api

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2836: фикс миграций

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-09 15:25:41

0.90.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2894: Демаскировать исключение

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-02-04 15:24:01

0.90.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2211: Попробовать смигрировать историю изменений деревьев ролей
  * RULES-2739: Фикс для пользователей 32-битных систем
  * RULES-2869: Шлем уведомления по отозванным ролям
  * RULES-2874: Странности в саджесте по rolestate
  * RULES-2881: Не отзывается роль

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-02-03 17:58:44

0.90.1
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2821: additional logging
  * RULES-2862: Убрать caplog в тестах
  * RULES-2816: Слетает visibility при редактировании роли через api
  * RULES-2739: stabilize test
  * RULES-2838: Фильтр по типу роли в ручке ролей
  * RULES-2739: fix mptt procedures

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Апдейт сборки
  * Апдейт зависимостей

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2821: Поправил падающие тесты
  * RULES-2739: Поправил падающие тесты
  * Заигнорировал временную папку pytest
  * RULES-2770: Привести в соответствие таблицу AD-групп и таблицу ролей OEBS
  * Заменил вызов на pillow-совместимый в рамках озеленения тестов
  * RULES-2770: Забытая миграция

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2016-01-29 11:40:09

0.90.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2739: Ускорить обновление дерева ролей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-25 19:38:01

0.89.14
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2900: Отправляем некорректные уведомления
  * RULES-2900: Убрал дубликат теста

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-02-05 16:22:38

0.89.13
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2869: Шлем уведомления по отозванным ролям

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-29 14:52:23

0.89.12
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2828: Неправильно определяем руководителя у руководителей

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2833: Не разрешаются неконсистентности

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-22 19:54:03

0.89.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2822: При ответе testapi ловим только CommandError

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-21 17:31:32

0.89.10
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс зависимостей и апдейт версий

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2815: Добавить опцию синхронного запуска команды синхронизации групп
  * RULES-2815: Удалил опцию асинхронного запуска команд в testapi

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-20 16:56:07

0.89.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2813: Добавить sqlparse в зависимости

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-19 16:38:59

0.89.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2793: Увеличить количество воркеров
  * RULES-2797: Не проставляется признак sid=67 пользователю
  * RULES-2795: Ускорить выдачу ручки для вьюверов
  * RULES-2788: Починил упавший тест
  * RULES-2788: Расставил try/except, чтобы синхронизация не ломалась, если что-то не так с переводом ролей в need\_request
  * RULES-2808: Не нужно пытаться отозвать в связи с протуханием связанные роли
  * RULES-2805: Ошибки Column 'last\_login' cannot be null при создании пользователя
  * RULES-2811: Добавить сортировку в api
  * RULES-2788: Убрал try/except обёртки вокруг сигналов
  * RULES-2806: Ошибки синхронизации дерева ролей Управлятора в тестинге

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2788: improve logging

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-19 16:13:04

0.89.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2786: Сделать полегче проверку прав для запросов в api за ролями системы
  * RULES-2789: Нужно обернуть manage.py-команды в @atomic, select\_for\_update должен быть выполнен внутри транзакции
  * RULES-2788: Роль не переходит в need\_request
  * RULES-2682: Не отдавать фронтэнду данные о возможном отзыве/перезапросе, если система сломана

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2790: Поправить тесты workflow

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-14 16:03:30

0.89.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2697: Не работает синхронизация набора нод
  * RULES-2633: Вынес проверку на то, что роль может быть автоматически подтверждена, если будет запрошена тем же пользователем, который запрашивал её в прошлый раз, в отдельную функцию
  * RULES-2633: Добавил системе метод is\_operational(), означающий активность и несломанность, и использовал его везде, куда смог дотянуться
  * RULES-2633: Стиль в center.py
  * RULES-2626: Писать правильный комментарий о причине перезапроса
  * RULES-2633: Добавил метод ask\_rerequest и использовал его для перезапроса групповых ролей
  * RULES-2633: Переименовал метод и убрал тесты, касающиеся пересмотра ролей
  * RULES-2633: Убрать старую логику перезапроса ролей при смене подразделения
  * RULES-2763: Не отсылаем письма про оставшиеся подтверждения из-за Connection Refused
  * RULES-2764: Не работает отправка писем с длинными паролями
  * RULES-2769: Показываем в интерфейсе пароли
  * RULES-2769: Поправил код так, чтобы тесты не падали и сохранялось предыдущее поведение
  * RULES-2634: Перенёс функцию is\_user\_absent в idm/sync/gap
  * RULES-2634: Перенёс функцию service\_is\_readonly в idm/utils/replication
  * RULES-2634: Перенёс функции по работе с ченджлогом в idm/utils/changelog
  * RULES-2771: Починить страницу /changelog
  * RULES-2634: Перенёс функции по генерации diff-ов в idm/utils/diff
  * RULES-2634: Перенёс функции, вычищающие из данных пароли, в idm/utils/cleansing
  * RULES-2634: Перенёс функцию normalize\_ad\_group в idm/utils/ldap
  * RULES-2634: Перенёс пару уродливых функций в idm/views, где они используются
  * RULES-2634: Заменил make\_local на localtime
  * RULES-2634: Радикально почистил idm/utils, оставил там только min\_with\_none, reverse и json
  * RULES-2634: Добавил функцию, аналогичную get\_object\_or\_404, но фейлящую задачу при неуспехе
  * RULES-2634: Использовал в задачах функцию get\_object\_or\_fail\_task и расставил в нужных местах transaction.atomic
  * RULES-2634: Проверять состояние роли перед действием
  * RULES-2634: Добавил опцию for\_update к методу get\_object\_or\_fail\_task
  * RULES-2634: Начал проставлять атрибут for\_update и использовать флаг for\_update = True
  * RULES-2634: Проставил в соответствующих местах кода select\_for\_update()
  * RULES-2634: Поправил падающие тесты, местами отрефакторил тесты
  * RULES-2634: Уменьшил количество блокируемых при подтверждении/отклонении ApproveRequest-а объектов
  * RULES-2772: Поправить опечатку в узле дерева ролей
  * RULES-2746: Ломаются системы в продакшне (Стафф, Кондуктор, BACKA, Видеоплатформа)
  * RULES-2634: Поправил падающий на MySQL тест

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2744: Валидация нод при добавлении через API
  * RULES-2761: Добавить --force в idm\_subscribe\_passport\_logins
  * RULES-1989: Внести конфликты ролей в OEBS

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-13 16:46:18

0.89.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Поправил падающие тесты
  * RULES-2745: При обновлении дерева ролей сохраняем неправильную версию choices

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-22 16:08:01

0.89.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Обновил django-mptt, чтобы не конфликтовать с пакетом south

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-17 20:46:53

0.89.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2733: Создать wsgi.py для обновления до Django 1.8

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-17 18:35:45

0.89.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Отключил создание guardian-ом анонимного пользователя

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-17 17:48:49

0.89.1
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс зависимости от libcurl

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-17 17:34:23

0.89.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2621: Не дает запрашивать роль
  * releasing version 0.87.31
  * RULES-1834: Поправил тесты, которые падали из-за проблем с permission-ами
  * RULES-2637: Убрал дублирование в тестах
  * RULES-2637: Не выдавать персональные роли повторно
  * RULES-2569: Удалил забытый print
  * RULES-2569: Поправил миграцию
  * RULES-2635: Миграция для удаления двойных запросов
  * RULES-2717: Отзываем перезапрошенные роли в Стаффе
  * RULES-2717: Немного привёл в порядок работу с неконсистентностями вне приложения inconsistencies
  * RULES-2717: Удалил несколько проверок на заведённость роли по неконсистентности, добавил тест. Проверки находились в переходах из requested->approved, approved->granted, requested->declined, в которые никогда не попадает роль, заведённая по неконсистентности, так как она не бывает в состояниях requested и approved.
  * RULES-2688: Закопать /me/expire и /user/<login>/expire
  * RULES-2717: Поправил падающий тест
  * RULES-2279: Неправильные причины запроса роли
  * Fabfile edits

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1824: Переезд на Django 1.8
  * RULES-1824: миграции
  * RULES-1824: remove south migrations
  * RULES-1824: create view in tests
  * RULES-2569: Новое состояние для роли: система уведомлена
  * RULES-2498: Унести перезапросы в новый интерфейс
  * RULES-2491: Убрать костыль Бункера

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс сборочных зависимостей

 * [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/Alexey%20Boriskin%20(uruz))


 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-17 17:16:35

0.88.23
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2788: Роль не переходит в need\_request

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-19 19:24:42

0.88.22
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2795: Ускорить выдачу ручки для вьюверов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-15 18:40:27

0.88.21
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2793: Увеличить количество воркеров

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-14 21:23:04

0.88.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2786: Сделать полегче проверку прав для запросов в api за ролями системы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2016-01-14 17:29:24

0.88.19
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2763: Не отсылаем письма про оставшиеся подтверждения из-за Connection Refused
  * RULES-2764: Не работает отправка писем с длинными паролями

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-30 12:37:45

0.88.18
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2717: Отзываем перезапрошенные роли в Стаффе
  * RULES-2717: Немного привёл в порядок работу с неконсистентностями вне приложения inconsistencies
  * RULES-2717: Удалил несколько проверок на заведённость роли по неконсистентности, добавил тест. Проверки находились в переходах из requested->approved, approved->granted, requested->declined, в которые никогда не попадает роль, заведённая по неконсистентности, так как она не бывает в состояниях requested и approved.

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс сборочных зависимостей
  * Фикс зависимости от libcurl

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-22 16:46:18

0.88.17
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2705: Исправил опечатки
  * RULES-2700: Не учитывать групповые роли при поиске неконсистентностей для unaware-систем
  * RULES-2705: Пятисотит экран неконсистентностей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-11 17:33:53

0.88.16
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2693: Стиль тестов на сломанную систему
  * RULES-2693: Плохое сообщение о сломанной системе
  * RULES-2694: Механизм разрешения неконсистентностей работает даже если превышен лимит неконсистентностей для системы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-10 15:24:17

0.88.15
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2689: При запросе роли выводить ошибки введённых пользователем данных в подсловаре fields\_data словаря errors
  * RULES-2636: Проверять состояние запроса перед подтверждением
  * RULES-2692: Не создаются неконсистентности
  * RULES-2692: Ускорение генерации письма с отчётом
  * RULES-2687: Можно запросить временную роль на вчерашнюю дату

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-09 18:08:47

0.88.14
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2678: Обновить переводы
  * RULES-2678: Обновить переводы - compiled files

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-12-08 11:51:42

0.88.13
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

    RULES-2517: Доработка неконсистентностей

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2619: Если не найден ресурс в API, то 404-я страница возвращает текст, а не json
  * RULES-2651: Отдавать данные о сроке действия роли в форму запроса strike back

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-12-07 17:38:53

0.88.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2518: Получение детей ноды через прямой запрос через parent
  * RULES-2518: Не запрашивается роль для Бункер/powny-www
  * RULES-2518: Добавил опцию dry-run
  * RULES-2518: Отфильтровываем удалённые узлы
  * RULES-2557: Не работает воркфлоу в тестинге
  * RULES-2568: Сломалась синхронизация стаффовых групп
  * RULES-2572: Использовать явную сортировку по \_id в синхронизации Стаффа
  * RULES-2590: Предотвращающая двойную отправку данных в систему логика не должна учитывать неактивные роли
  * RULES-2591: При переводе внутри большого подразделения нужно сохранять персональную роль, выданную по групповой
  * RULES-2595: Иногда при синхронизации групп нет общего предка
  * RULES-2595: Иногда при синхронизации групп нет общего предка
  * RULES-2591: При переводе внутри большого подразделения нужно сохранять персональную роль, выданную по групповой
  * RULES-2617: Принимать choices полей в формате value/name
  * RULES-2621: Не дает запрашивать роль

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Таска deploy-local для fabric

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1824: Переезд на Django 1.8
  * RULES-2618: API v1 не проверяет OAuth-токен
  * RULES-2640: Наведение порядка в репозитории
  * RULES-2598: Обрабатывать в /rolerequest поля временной роли
  * RULES-2588: Отдавать данные о сроке действия роли в форму запроса

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-12-04 13:25:05

0.88.11
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2086: Прокинуть в testapi ручки systems и workflow
  * RULES-2560: Не приходят отчеты в тестинге
  * RULES-2560: fix tests
  * RULES-2232: Проверять паспортный логин в большом паспорте при создании
  * RULES-2586: Добавить в v1/rolenodes двухфакторную авторизацию
  * RULES-2592: Не выводить в v1/rolenodes неактивные ноды

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Таска deploy-local для fabric
  * RULES-2567: Передавать в ручке про человека id его департаментной группы

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2572: Использовать явную сортировку по \_id в синхронизации Стаффа
  * RULES-2568: Сломалась синхронизация стаффовых групп
  * RULES-2590: Предотвращающая двойную отправку данных в систему логика не должна учитывать неактивные роли
  * RULES-2571: Ошибка в саджесте ролей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-11-26 15:30:12

0.88.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2376: Ручки add-role, remove-role научить работать с группами
  * RULES-2531: Перевёл choicefield\_with\_other на choicefield + options.custom
  * RULES-2531: Переделал отдачу choices для фронтэнда
  * RULES-2545: Расширить длину поля plugin\_type
  * RULES-2549: Поправить падающие тесты
  * RULES-2549: Отрефакторил тесты LDAP
  * RULES-2557: Не работает воркфлоу в тестинге

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2553: Учитывать переданный type\_filter при отдаче данных о роли
  * RULES-2554: Проверять в ручке permissions групповую политику

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2533: Разобраться с переводами в Танкере

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-11-20 10:29:29

0.88.9
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1798: фикс тестов

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2518: Тест на корректную склейку результатов next-url. Дело оказалось не в этом, но тест полезный, как мне кажется.
  * RULES-2518: Получение детей ноды через прямой запрос через parent
  * RULES-2518: Не запрашивается роль для Бункер/powny-www
  * RULES-2518: Добавил опцию dry-run
  * RULES-2518: Отфильтровываем удалённые узлы

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2017: Избавиться от слова 'доступ' на беке
  * RULES-2329: Убить поле пользователя is\_werewolf
  * RULES-2521: Ошибка KeyError в получении rolerequests
  * RULES-2440: Публичное API над узлами дерева ролей
  * RULES-2521: fix tests

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-11-13 17:26:35

0.88.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2508: Локализация полей в клиентском API
  * RULES-2508: Добавил методов для сериализации узлов, полей и синонимов как в /info/
  * RULES-2378: Миграция, добавляющая поле 'dependencies' для полей узла дерева ролей

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1798: Добавить dumb плагин для систем без API

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-11-09 02:01:05

0.88.7
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2457: фикс тестов
  * RULES-2360: ещё оптимизация выборки экшенов
  * RULES-2005: дефолтное значение для переменной CELERY\_ALWAYS\_EAGER
  * RULES-2360: фильтрация объектов с учетом прав через подзапрос

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2005: Починил тесты при запуске с MySQL
  * RULES-2360: Починил падавшие на MySQL тесты
  * RULES-2502: Добавить в API фронтэнда информацию о том, может ли поле быть заполнено для всех
  * RULES-2503: При задании id группы узлов очередь изменений должна быть пустой. RULES-2504: Переименовать RoleNodeGroup в RoleNodeSet
  * RULES-2378: Зависимые поля ролей
  * RULES-2374: Добавляю синонимы в API для фронтэнда

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-11-07 01:28:08

0.88.6
---

  * RULES-2483: Добавить поле on\_page для карточки действия
  * RULES-2457: Ресурс проверки прав для запроса роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-11-02 20:24:17

0.88.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2398: Ошибка в саджесте сотрудников
  * releasing version 0.87.23

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-826: Отчеты в формате xls

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2360: Поправил падающий тест
  * RULES-2425: В коммите этом кода стиль Йоды магистра убрал я
  * RULES-2425: Отправлять запрос всем при пересмотрах
  * RULES-2430: Починить обработку доктестов

 * [Alexander Koshelev](https://staff.yandex-team.ru/Alexander%20Koshelev)

  * Revert "RULES-2425: Отправлять запрос всем при пересмотрах"

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2425: В коммите этом кода стиль Йоды магистра убрал я
  * RULES-2425: Отправлять запрос всем при пересмотрах
  * RULES-2422: Сообщения об ошибках при отправке формы
  * RULES-2377: Кастомные типы полей
  * RULES-2377: Поправил тесты, которые стали падать из-за новой валидации данных
  * RULES-2377: Миграция
  * RULES-2374: Добавить алиасы в клиентское API

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2448: Ручка действий: не прилетают данные для связанных полей

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2372: Группировка ролей

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2005: Отказаться от django-celery

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2449: Переименовать поле фильтра actions в action для отчета по действиям
  * RULES-2455: Избавится от поля can\_request\_role\_for с саджесте
  * RULES-2456: Удалить ресурс AvailableSystemsSuggestResource

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2453: Не выдалась роль при запросе одним из аппруверов: выключаю сломанную команду. Refs RULES-2400
  * RULES-2467: Создавать честные approverequest по количеству подтверждений
  * RULES-2470: Дублирование ролей
  * RULES-2468: Если роль запрашивается на группу, но не ответственным этой группы, то она не должна автоматически подтверждаться

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1502: Излишнее блокирование
  * RULES-2462: Доработать фильтрацию action'ов
  * RULES-2450: Удалить ненужную таблицу UserDepartmentChange

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2292: Перезапрос подвисших ролей
  * RULES-2430: Починить обработку доктестов
  * RULES-2453: Не выдалась роль при запросе одним из аппруверов: выключаю сломанную команду. Refs RULES-2400
  * RULES-2468: Если роль запрашивается на группу, но не ответственным этой группы, то она не должна автоматически подтверждаться
  * RULES-2444: Использовать новые фичи API системы в дереве ролей Управлятора
  * RULES-2444: Добавил инлайнов и blank=True, чтобы сделать админку узлов более удобной
  * RULES-2470: Дублирование ролей. Перенёс код в manage.py-команду, чтобы включить задачу в хотфикс
  * RULES-2470: Дублирование ролей. Перенёс код в manage.py-команду, чтобы включить задачу в хотфикс
  * releasing version 0.87.24

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2005: Новая запускалка для celery
  * RULES-2360: более хитрая дегидрация для related полей
  * RULES-2360: select\_related только для list экшенов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-10-30 19:56:51

0.88.4
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2431: Удалить ручку role и ресурс OldRole из API v1

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2245: Обновить django-dbtemplates
  * RULES-2360: Доработка api ручки экшенов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-10-19 15:33:19

0.88.3
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2331: Вернуть правильную дату обновления ролей
  * RULES-2367: Поправил падавшие тесты
  * RULES-2286: Переделал и subject на full\_name
  * RULES-2398: Ошибка в саджесте сотрудников

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2306: Привести передачу ролей к одному виду
  * RULES-2369: Связать объекты Workflow через parent

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-10-15 15:03:38

0.88.2
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2286: Убрать fullname из user в ручках
  * RULES-2408: Человекочитаемое описание неконсистентности
  * RULES-2366: Смигрировать экшен resolve
  * RULES-2367: Убрать system\_slug из экшена started\_sync\_with\_system

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-10-08 17:44:54

0.88.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2373: Саджест должен учитывать RoleNodeAlias
  * RULES-2395: Ошибки при попытке выдать связанную роль
  * RULES-2292: Перезапрос подвисших ролей

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2324: Добавить полей в action
  * RULES-2406: Вернуть фильтр по роли в /actions

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-10-07 07:45:44

0.88.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2244: Обновить django-ajax-selects
  * RULES-2243: Обновить django-guardian
  * RULES-2326: Внести notification в upravlyator
  * RULES-2358: Свести api ручки actions и reports в одну

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2326: Поправил путь для patterns

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-10-06 10:25:23

0.87.31
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2621: Не дает запрашивать роль

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-12-03 13:57:51

0.87.30
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2595: Иногда при синхронизации групп нет общего предка
  * RULES-2591: При переводе внутри большого подразделения нужно сохранять персональную роль, выданную по групповой

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-11-30 15:18:19

0.87.29
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2590: Предотвращающая двойную отправку данных в систему логика не должна учитывать неактивные роли
  * Fabfile edits

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-11-25 19:36:42

0.87.28-1
---

  * пересборка

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-11-24 15:28:35

0.87.28
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2557: Не работает воркфлоу в тестинге
  * RULES-2568: Сломалась синхронизация стаффовых групп
  * RULES-2572: Использовать явную сортировку по \_id в синхронизации Стаффа

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Таска deploy-local для fabric

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-11-24 14:25:29

0.87.27
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2518: Отфильтровываем удалённые узлы

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-11-12 15:05:46

0.87.26
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2518: Добавил опцию dry-run

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-11-12 13:36:39

0.87.25
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2518: Получение детей ноды через прямой запрос через parent
  * RULES-2518: Не запрашивается роль для Бункер/powny-www

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-11-12 11:29:06

0.87.24
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2292: Перезапрос подвисших ролей
  * RULES-2430: Починить обработку доктестов
  * RULES-2453: Не выдалась роль при запросе одним из аппруверов: выключаю сломанную команду. Refs RULES-2400
  * RULES-2468: Если роль запрашивается на группу, но не ответственным этой группы, то она не должна автоматически подтверждаться
  * RULES-2470: Дублирование ролей. Перенёс код в manage.py-команду, чтобы включить задачу в хотфикс

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-10-30 14:47:03

0.87.23
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2398: Ошибка в саджесте сотрудников

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-10-09 14:36:34

0.87.22
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2385: Не отзывается связанная роль

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-10-01 17:58:24

0.87.21
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2281: Поправил запрос, добавил логгирования

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2304: отдельная очередь для синхронизации дерева ролей

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-10-01 16:56:21

0.87.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2320: Показывать больше, чем 100 байтов ответа системы. Также изменил и протестировал обработку ответов систем
  * RULES-1966: Добавил опцию notify\_everyone, которая шлёт письма всем подтверждающим. Опцию check\_gaps модифицировал так, что она отсылает письма первому подтверждающему в каждой ИЛИ-группе, вне зависимости от наличия/отсутствия
  * RULES-2363: Не добавляются пользователи в AD
  * RULES-2363: Причесал и переименовал manage.py-команду normalize\_ad\_groups, добавил тест
  * RULES-1966: Добавил проверку, что если в или-группе все отсутствуют на месте, то шлём всем в этой или-группе
  * RULES-1966: Уточнил комментарий
  * RULES-2281: Перенёс менеджер в отдельный файл
  * RULES-2281: Убрал функцию, использовавшуюся в одном месте
  * RULES-2281: Удалил ещё несколько функций и файл
  * RULES-2281: Отрефакторил тесты неконсистентностей
  * RULES-2281: Убрал префикс u у строк
  * RULES-2281: Дублирование ролей
  * RULES-2281: Добавил миграцию, отзывающую дублирующиеся роли
  * RULES-1779: Поправил упавший тест
  * RULES-2188: Пропадает комментарий при отзыве
  * RULES-2321: Не разрешать запрашивать роли на нелистовые узлы дерева ролей

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1779: Расширить письмо про паспортный логин - ссылка на восстановление

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-10-01 14:58:18

0.87.19
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2313: Отписывать логины без активных ролей
  * RULES-2290: Ошибка в сборе паспортных логинов
  * RULES-2297: Не осуществлять сверку неактивных систем

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2303: Выводить data для неизвестной роли
  * RULES-2312: Прокидывать инициатора синхронизации дерева ролей везде
  * RULES-2145: В саджесте не находилсяся пользователь дефисом в username в поиске по subject-ам
  * RULES-2307: Больше логинга при синхронизации дерева ролей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-24 17:49:10

0.87.18
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2301: Падает синхронизация при неизвестной роли

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2300: DoesNotExist при запросе роли постороннему
  * RULES-2304: Попробовать донастроить celery

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-23 15:26:39

0.87.17
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2285: Правильно обрабатывать ошибки в api ручках
  * RULES-2289: Оптимизация синхронизации дерева ролей
  * RULES-2285: Поправил падающие из-за порчи транзакции тесты

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-22 17:52:00

0.87.16
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2273: Отдельный пул воркеров для тасок над ролями

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2274: separate passport tasks

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-21 15:47:19

0.87.15
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2274: Уметь обрабатывать неизвестные паспорту логины

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2273: Отдельный пул воркеров для тасок над ролями

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-21 14:53:51

0.87.14
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2271: Ответы систем, отвечающих на ручку добавления роли кодом '0' текстом, перестали считаться успешными

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-18 18:32:16

0.87.13
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2261: Поправить админку ролей
  * RULES-2267: Выпилить RoleLogWriter
  * RULES-2266: Не работает получение ролей из Бункера

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2269: Некорректная работа со склонятором

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2262: Руководитель не может запросить роль для сотрудника, если у него есть ограниченные права в системе

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-18 15:52:21

0.87.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2255: Стал запускать пересчёт fullname-ов только в случае непервоначальной синхронизации и только в случае, если переименования были
  * RULES-2255: Ускорение хеширования
  * RULES-2255: Не забираем данные из систем в silent-режиме
  * RULES-2255: select с дальнейшим сопоставлением slug/pk, чтобы работать в среде с конкурентными insert-ами

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2116: Управлятор как система отвечает трейсбеком на попытку выдать уже существующую роль

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-17 18:21:12

0.87.11
---

  * RULES-2253: Прокинуть userify и groupify в wf

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-17 00:01:47

0.87.10
---

  * RULES-2253: Прокинуть userify и groupify в wf
  * RULES-2251: Давать запрашивать роль всем для всех

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-16 21:17:12

0.87.9
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1418: requests instead of pycurl

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2240: Увеличил лимиты
  * RULES-2231: Поправил ошибку с необъявленной переменной
  * RULES-2038: Поправил взятие md5 от текста
  * RULES-2240: Ускорение саджеста

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-16 18:50:43

0.87.8
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1418: Снимать sid=67 при отзыве роли
  * RULES-2228: Сохранять workflow в RoleRequest

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2067: Человекопонятные названия ролей
  * RULES-2038: Переименовал файл queue в queues, слишком многие модули не умеют в six
  * RULES-2240: Расставил в некоторых местах select\_related, поправил несколько некорректных использований
  * RULES-2240: Добавил тестов на количество запросов
  * RULES-2242: Не приезжают ответственные для групп
  * RULES-2231: Удалил неиспользуемые теперь шаблоны и скрипты
  * RULES-2231: Убрал неиспользуемые импорты
  * RULES-2231: Поправил миграцию
  * RULES-2231: Добавил индекс по полю value\_path, поскольку по нему производятся выборки
  * RULES-2231: Улучшил вьюху system\_roles\_management, добавил опции тихого режима и частичного просмотра
  * RULES-2231: Оптимизировать процесс первичного импорта дерева ролей

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2040: Обрабатывать поле requester в ручках API

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-16 11:03:56

0.87.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2226: Ошибка на странице отчётов по ролям

 * [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/Alexey%20Boriskin%20(uruz))


 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-09-12 23:18:30

0.87.6
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2225: Ошибка в проверке паспортного логина

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2038: Вернул случайно убранный ребилд
  * RULES-2038: Проимпортировал celery-таски, это должно помочь celery найти их
  * RULES-2225: Тест на ошибку при проверке паспортного логина

 * [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/Alexey%20Boriskin%20(uruz))


 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-09-12 22:10:03

0.87.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * releasing version 0.87.0

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * releasing version 0.87.1
  * releasing version 0.87.2
  * releasing version 0.87.3
  * releasing version 0.87.4

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)


 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-09-11 21:00:16

0.87.4
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2131: fix tests
  * RULES-2201: Уметь обрабатывать несколько занчений параметра user в ручке /api/frontend/reports/actions
  * RULES-2132: Ручка с полной информацией о группе - все поля групп

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-02 17:19:33

0.87.3
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2131: Ручка по составу группы
  * RULES-2193: Сделать правки по ручке /api/frontend/roles/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-01 13:14:52

0.87.2
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2132: Ручка с полной информацией о группе

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2179: Индексы в таблице Action
  * RULES-2192: Дополнительные параметры у ручки ролей

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2162: Фикс тестов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-09-01 10:01:52

0.87.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2145: В саджесте не находится пользователь inna-k
  * RULES-2163: Равнозначные подтверждающие стали обязательными
  * RULES-2184: Не отправляем пароли: тест на проброс переменных в контекст

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2170: Возможность получения саджеста систем группы

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-08-25 13:51:03

0.87.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2064: В письмах о выдаче роли не хватает информации о том, кто запросил роль
  * RULES-2033: Протестировать регулярный пересмотр групповых ролей
  * RULES-2078: Поправил падающий тест
  * RULES-2078: Fix admin
  * RULES-2001: Сделать ручку в testapi по перезапросу роли

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1921: Ручка для отчетов по ролям
  * RULES-1998: workflow/test должен принимать роль в виде path вдобавок к текущему формату
  * RULES-1922: Ручка для отчетов по действиям
  * RULES-2078: some cleanups, while i am here
  * RULES-2181: Удалять pyc файлы перед тестами
  * RULES-2182: Опечатка в ресурсе User

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-08-20 14:22:16

0.86.30
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1905: Исправить использование одного паспортного логина несколькими пользователями
  * RULES-2078: Не дает запрашивать роль на логин в другой системе
  * RULES-1905: fix test

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2173: Не уехали роли в систему
  * RULES-2162: Не приходит пароль

 * [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/Alexey%20Boriskin%20(uruz))


 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-08-14 12:33:50

0.86.26
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Revert "RULES-2116: Управлятор как система отвечает трейсбеком на попытку выдать уже существующую роль"

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2144: Персональные роли выдаются по групповой уволенным пользователям

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-08-10 15:49:46

0.86.25
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1779: Расширить письмо про паспортный логин
  * RULES-2136: /suggest/roles/all/ не должен реагировать на параметр user
  * RULES-2138: Искать в админке ролей по fields-data
  * RULES-2143: Выкинуть остатки удаленной ручки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-08-06 15:23:41

0.86.24
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2106: Включить в деве тестинге нужный cron
  * RULES-2095: При дублировании роли отзываем последнюю
  * RULES-2116: Управлятор как система отвечает трейсбеком на попытку выдать уже существующую роль
  * RULES-2122: Невалидные департаменты в workflow
  * RULES-1882: Потеря параметров при retry
  * RULES-2104: Выданы связанные роли на отозванные
  * RULES-2119: Слишком большое количество записей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-08-05 12:55:53

0.86.23
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2104: Не выдаём связанные роли на неактивные пользовательские

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-31 18:07:07

0.86.22
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2088: Отзывать запрошенную роль
  * RULES-2093: Не работает саджест в шапке
  * RULES-2104: Выданы связанные роли на отозванные

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2096: Оптимизация миграции action'ов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2092: Сломался idm\_update\_permission\_groups
  * RULES-2098: IndexError в очереди запросов
  * RULES-2101: Ошибка в поле ListRolePathField
  * RULES-2108: Оптимизировать выдачу detail данных про людей и системы

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-31 17:44:33

0.86.21
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1995: workflow/test падает при плохом параметре
  * RULES-1994: Прогонять workflow на тесты при аппруве
  * RULES-2085: Прокинуть ручку frontend/rolerequests в публичное апи

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2079: При отзыве групповой роли ответственным не уходят письма о том, что роль была отозвана
  * RULES-2079: Поправил падающий тест

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1978: Починить ручку /api/testapi/users/{login}/ad-restore/

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-30 14:55:46

0.86.20
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-2023: Не давать запрашивать групповую роль там где нельзя
  * RULES-2012: Не отправлять письма при получении групповой роли
  * RULES-2012: Переход на асинхронную отправку всей почты через django-celery-email
  * RULES-1955: Протестировать BasePermittedObjectManager.get\_permitted\_query
  * RULES-2050: Обработка комментария при действии над ролью

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1555: Переезд ручки firewall
  * RULES-2059: /frontend/rolerequests/ падает при запросе роли без системы
  * RULES-2058: /frontend/rolerequests/ падает при некорректной роли
  * RULES-2020: Ошибка в отзыве роли
  * RULES-1996: workflow/test отвечает 200 OK при неизвестном пользователе
  * RULES-1996: fix tests
  * RULES-2061: Вытащить ручку /roles в api v1
  * RULES-2072: Закопать /frontend/

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2028: Убить nginx конфиги idm-old
  * RULES-2025: вывод урла в случае ошибки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-29 19:02:55

0.86.19
---

  * RULES-2030: id актуального запроса подтверждения в ресурсе роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-23 20:57:33

0.86.18
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2019: Роль Наблюдатель (Viewer)

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2025: Выводить заголовки при проверке системных ручек
  * RULES-2030: id актуального запроса в ресурсе роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-23 18:35:43

0.86.17
---

  * RULES-1935: правильные счетчики с учетом фильтров
  * RULES-2015: включаем протухание ролей каждые 15 минут
  * RULES-2015: не проверяем при подтверждении протухание роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-22 17:09:18

0.86.16
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1980: Добавить в ресурс роли флаги действий
  * RULES-1960: Стал создавать role request-ы даже если нет подтверждающих
  * RULES-1960: Протестировать логику перезапроса роли
  * RULES-2002: Добавить синхронизацию групп в крон
  * RULES-1676: Перезапрос роли для пользователя
  * RULES-2016: Ручка для получения информации о группе по её id

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-2006: Дублирующаяся выдача у /suggest/subjects/exist
  * RULES-2009: Перенести апи тестов в api
  * RULES-1921: simplify imports

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-2015: Фикс ручки подтверждения роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-21 20:14:49

0.86.15
---

  * RULES-1991: фильтрация групп и пользователей через ИЛИ

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-17 13:39:11

0.86.14
---

  * RULES-1992: Использовать for\_list представление для related объектов
  * RULES-1991: Поддержка фильтра по группе в ручке ролей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-17 09:40:39

0.86.13
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1171: Отдавать списки действий и состояний ролей
  * RULES-1962: Добавить роли которые подтверждает пользователь в permitted
  * RULES-1944: Неправильный паспортный логин
  * RULES-1986: Лишнее получение списка workflow

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1969: Допинывать недовыданные персональные роли
  * RULES-1717: Запуск тестов на sqlite по ключу -L или --sqlite
  * RULES-1717: Миграция, создающая VIEW

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1935: фикс фильтрации по нескольким пользователям и группам

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-16 18:40:28

0.86.12
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1935: Рефакторинг ручки отдачи очереди запросов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1935: доделки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-15 15:15:37

0.86.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1974: Ручка /roles/{id}/ не должна падать, если у роли нет ни одного rolerequest-a
  * RULES-1956: Проверить и протестировать отправку diff групповых workflow при аппруве workflow

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * TOOLSADMIN-2362: Пропали дырки до zookeeper с idm.dev.yandex-team.ru

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-14 18:11:19

0.86.10
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1938: Ручка саджеста людей/групп для фильтра очереди

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1957: Починить синхронизацию групп на dev, добавить логгирования
  * RULES-1904: Не саджестятся некоторые пользователи по имени
  * RULES-1957: Фикс тестов

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-07-13 20:10:30

0.86.9
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1927: admin fix

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1937: Поправил падавшие тесты
  * RULES-1953: Доработка ручки списка ролей
  * RULES-1958: Апдейт ручки запроса для групповой роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-10 14:07:00

0.86.8
---

  * RULES-1927: Добавить несколько FK в Action - ссылка на себя
  * RULES-1927: Добавить несколько FK в Action - RoleRequest
  * RULES-1927: Добавить несколько FK в Action - ApproveRequest
  * RULES-1927: Добавить несколько FK в Action - roles
  * RULES-1936: Ручка саджеста систем для фильтра очереди
  * RULES-1937: Ручка саджеста ролей для фильтра очереди

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-07-09 17:04:47

0.86.7
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1776: используем транзакцию в idm\_move\_actions
  * RULES-1925: AttributeError в отчетах ad
  * RULES-1947: Доработать шаблон письма о выдаче связной роли
  * RULES-1717: фикс конфига баз для тестов

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1717: Правки в логике для перевода тестов на mysql
  * RULES-1717: Перевод тестов на mysql
  * RULES-1717: Распилил тесты саджеста в соответствии с самим саджестом
  * RULES-1717: Ручка саджеста людей/групп для формы

 [Alexey Boriskin](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2015-07-08 15:36:08

0.86.6
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1776: Свести все action в одну таблицу - удаление UserRoleAction
  * RULES-1776: Свести все action в одну таблицу - удаление SystemBreakdownLog
  * RULES-1776: Свести все action в одну таблицу - удаление UserADAction
  * RULES-1776: Свести все action в одну таблицу - удаление UserDepartmentChange
  * RULES-1776: move long migration to command

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1920: Добавлен модуль с полями для использования в формах
  * RULES-1920: Доработать ручку test для wf групп

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-06 14:20:01

0.86.5
---

  * RULES-1760: Запрашивать роль в Управляторе из системы
  * RULES-1923: Опечатка в логировании

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-07-03 10:55:42

0.86.4
---

  * RULES-1847: Сделать совместную blackbox+cert аутентификацию
  * RULES-1714: remove glader@ from recipients

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-07-01 20:54:07

0.86.3
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1902: Предлагает другой паспортный логин при выборе роли
  * RULES-1908: Правильная фильтрация ролей с учетом scope

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1900: Дублируются предложения паспортных логинов при выдаче новой роли

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-07-01 11:37:41

0.86.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1727: Логика выдачи групповой роли

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1881: Логирование ретраев

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-30 14:25:22

0.86.1
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1885: Перенос миграций
  * RULES-1886: Активность в отключенной системе
  * RULES-1889: Ошибка в проверке workflow
  * RULES-1838: Переехать на simplejson

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1890: Подтвержденная, но не выданная роль попадает в неактивные

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1897: 500 при запросе уже имеющейся роли в API v1
  * RULES-1898: Автообновлять роли Стаффа раз в минуту

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-29 20:01:16

0.86.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1846: Включить oauth

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1884: Сделать состоянием по умолчанию для роли created, а не requested

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-25 16:31:17

0.85.31
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1925: AttributeError в отчетах ad

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1900: Дублируются предложения паспортных логинов при выдаче новой роли

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1947: Доработать шаблон письма о выдаче связной роли
  * RULES-1924: Запрос связных ролей при перезапросе

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-07-09 17:44:58

0.85.30
---

  * RULES-1908: Правильная фильтрация ролей с учетом scope

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-30 21:36:07

0.85.29
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1884: Сделать состоянием по умолчанию для роли created, а не requested
  * RULES-1890: Подтвержденная, но не выданная роль попадает в неактивные

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1886: Активность в отключенной системе
  * RULES-1889: Ошибка в проверке workflow
  * RULES-1881: Логирование ретраев

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1897: 500 при запросе уже имеющейся роли в API v1
  * RULES-1898: Автообновлять роли Стаффа раз в минуту

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-06-30 14:50:19

0.85.28
---

  * RULES-1873: Не удалять пользователя из NoInteractiveLogonUsers
  * RULES-1520: Celery таски не могут найти экшены в БД

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-06-24 15:16:32

0.85.27
---

  * bump version

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-06-24 14:40:51

0.85.26
---

  * RULES-1794: Фильтры: На странице пользователя в саджесте отображаются системы просматривающего

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-06-24 13:59:17

0.85.25
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1728: Исправления задачи синхронизации групп
  * RULES-1728: Обновление updated\_at при сихронизации

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1871: Не учитывать связные роли при смене подразделения
  * RULES-1872: Починить отзыв связной роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-24 10:43:17

0.85.24
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1674: фикс вывода названия роли в отчете по ролям
  * RULES-1862: Удалить ненужные модели

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1674: На входе md5-хешера ожидается байт-строка

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1850: Убрать внутреннюю аутентификацию по токену

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-23 13:06:32

0.85.23
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1852: fix test

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1674: фикс работы с base\_url в базовом плагине

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-22 14:35:24

0.85.22
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1852: Архивировать отчеты

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1806: использование yalogin\_required
  * RULES-1858: Страница дерганья ручек отдельной системы
  * RULES-1674: Избавиться от модели GenericPlugin

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-22 10:40:27

0.85.21
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1815: Растащить саджесты на отдельные ресурсы

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-19 19:51:34

0.85.20
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1851: Не доудалять роли, если система неактивна
  * RULES-1815: Растащить саджесты на отдельные ресуры

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1821: правильно учитываем inactive type

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-19 19:18:40

0.85.19
---

  * RULES-1821: фикс подсчета страницы с учетом группировки по табам

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-19 14:31:45

0.85.18
---

  * RULES-1828: всегда показываем editor для changelog
  * RULES-1821: учитываем параметр &limit= при подсчете страниц

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-18 14:15:21

0.85.17
---

  * RULES-1825: фикс админки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-18 10:44:48

0.85.16
---

  * UNRELEASED

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-18 10:39:03

0.85.15
---

  * RULES-1825: Фикс миграции

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-18 10:28:39

0.85.14
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1837: Ошибка логирования

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1825: Переименовать поле ref у роли в parent

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-18 10:20:32

0.85.13
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1773: Не прописывается резервный емейл для паспортных логинов
  * RULES-1831: Не создается отчет

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1830: Добавил поле group\_policy в систему
  * RULES-1728: Добавил поле для хранения кода группового workflow
  * RULES-1830: Миграция по добавлению полей группового workflow и групповой политики
  * RULES-1830: Исключение поля из API, чтобы не падали тесты

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1828: фикс fabfile'а

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-17 20:21:52

0.85.12
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1821: Информация для ссылки на роль в ручке API

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1701: deployment process

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-06-16 19:28:03

0.85.11
---

  * UNRELEASED

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-06-16 19:25:32

0.85.10
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1728: Поправил места, забытые при перетаскивании FK на role

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-06-16 18:58:45

0.85.9
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1728: Исправление миграции, поле в m2m таблице не переименовывалось

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-15 11:50:17

0.85.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1658: Исправление миграции

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-11 17:57:25

0.85.7-1
---

  * Пересборка

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-11 17:14:35

0.85.7
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1814: Перейти на ids 1.0

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1797: Поправил миграцию

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1818: Фильтрация по ролям

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1728: Модель данных групповых ролей

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1658: ещё фикс сборки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-11 16:07:13

0.85.6
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1805: Некоторые изменения воркфлоу не выводятся в истории

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1658: users становится полноценным приложением

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1813: Не давать отзывать связную роль

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1780: Отказаться от использования Стаффа в проверке подразделения
  * RULES-1537: Левые паспортные логины
  * RULES-1797: История воркфлоу: Пропал лог из отчетов, На страницу приезжает не вся история
  * RULES-1743: return can\_request\_role\_for

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1485: Разрешаем выбор паспортного логина даже для систем с ограничением "один логин на все роли"

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1658: фикс сборки

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1788: Ручка /testapi/roles/<id>/approve перестала работать правильно

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1796: Восстановить тесты из test\_add\_role

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-09 18:21:30

0.85.5
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1777: Сохранять во внешнем Паспорте реальное ФИО человека

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1802: Перенёс тест в папку

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1762: не используем плагины в миграции

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1802: Унифицировать код симуляции выдачи роли и реальной выдачи роли

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1806: Навести порядок в проверке аутентификации
  * RULES-1594: Навести порядок с использованием transaction.atomic
  * RULES-1809: Поменять в ответах API idm-robot на robot-idm

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1743: Саджест людей заменяющий multicomplete

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-05 14:11:31

0.85.4
---

  * RULES-1762: фикс инициализации плагинов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-03 20:07:10

0.85.3
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1762: fix migration

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-03 18:51:25

0.85.2
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1800: Разнести ресурсы апи

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1485: Генерить не больше одного паспортного логина

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1771: Убить старые экраны
  * RULES-1790: Ручка отдающая все связные роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-03 18:17:03

0.85.1
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1767: Удалить остатки старых workflow
  * RULES-1795: Упорядочить тесты

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1771: Убить старые экраны
  * RULES-1799: Добавить число связных ролей в данные о роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-02 16:19:18

0.85.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1739: Нужно корректно отвечать при выставлении роли некорректного экшина
  * RULES-1363: выключить новый сертификат у всех

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1771: Убить старые экраны
  * RULES-1728: Модель данных групповых ролей

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1769: Привязывать неконсистентность к системе

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1762: Повторно выдалась та же роль на тот же логин
  * RULES-1781: Удалить ручку просмотра логов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1670: Распилить ресурсы frontend на модули
  * RULES-1739: Нужно корректно отвечать при выставлении роли некорректного экшина
  * RULES-1702: Выдавать информацию о связной роли в списках
  * RULES-1790: Ручка отдающая все связные роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-01 17:47:06

0.84.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1746: Убрал забытый print

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1683: additional logging

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1759: В системе Управлятор заведен доступ в обход Управлятора.

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-25 13:08:43

0.84.10
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1655: fix test
  * RULES-1748: Пользователь без имени

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1746: Доработать роль ИБ

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-21 16:09:39

0.84.9
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1641: fix notification test
  * RULES-1694: Ускорить подключение систем

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1669: Перевести /client-api/ на новый сертификат

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-20 18:57:53

0.84.8
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1655: fix migration

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1693: Поправил миграцию

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-19 16:59:49

0.84.7
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1693: Улучшен вывод информации о выданных/отозванных ролях

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1540: additional logging

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1693: Вынес FK на system и inconsistency в Action
  * RULES-1693: Добавил Action в админку
  * RULES-1693: Создаём Action при неуспехе синхронизации, выводим в Action успешного завершения синхронизации количество созданных и отозванных ролей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-19 15:42:13

0.84.6
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1598: fix test api

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-18 23:06:25

0.84.5
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1598: Нужны ручки подтверждения\отклонения роли из соответствующих статусов
  * RULES-1655: Workflow  в интерфейсе и в админке различается

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-18 22:09:34

0.84.4
---

  * RULES-1712: Ручка саджеста пользователей без callback
  * RULES-1641: version 0.84

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-05-15 09:00:03

0.84.3
---

  * RULES-1633: фикс отключения фильтра по типу для счетчиков
  * RULES-1622: Возможность исключать системы из регулярного пересмотра

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-13 14:40:30

0.84.2
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1633: Отдавать счетчики вместе с ролями

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1633: фикс счетчиков ролей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-12 17:19:34

0.84.1
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1673: Ломается саджест людей когда нету департамента
  * RULES-1685: Добавить перенос строки в конце выдачи agranat.m4
  * RULES-1682: TypeError при отдаче очереди запросов
  * RULES-1679: Фильтры: не всегда отрабатывает саджест

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-12 12:07:29

0.84.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1625: Добавить подразделение в данные саджеста людей
  * RULES-1627: Ручка саджеста систем для формы

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1651: Починить падающий тест dismiss user

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1579: Нужна ручка удаления неконсистентности

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1646: Вести логи неконсистентностей

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1363: Переезд на новый сертификат
  * RULES-1568: Ручка саджеста ролей для списка ролей

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-795: создание пермишенов в idm\_update\_permission\_groups

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-795: Управлятор: Завести новые роли

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-05-06 15:25:48

0.83.18
---

  * RULES-1648: Роль не дает полномочий

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-30 16:06:54

0.83.17
---

  * RULES-1645: Починить пермишены ролей в Управляторе

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-29 19:56:14

0.83.16
---

  * RULES-1611: фикс миграции

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-29 17:18:57

0.83.15
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1613: Ручка саджеста для списка систем
  * RULES-1629: Просмотр рабочих копий wf в админке

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-28 16:55:38

0.83.14
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1611: Использовать прямой FK для пермишенов

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1559: правка тестов LDAP

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1611: дописал тестов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-28 15:04:42

0.83.13
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1485: transaction.commit и transaction.rollback запрещены внутри atomic-блоков
  * RULES-1485: transaction больше не mock-ается. Вызов transaction.rollback() запрещён внутри atomic-блоков. В связи с тем, что у нас ATOMIC\_REQUESTS=1, каждая вьюха обёрнута в atomic блок. Раньше тесты не падали только потому, что transaction.rollback был подменён.

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1624: Поднять число воркеров celery
  * RULES-1623: Особо учитывать суперпользователей в фильтрах

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-27 17:18:46

0.83.12
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1559: работа с новыми настройками LDAP

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1619: Падает ручка при запросе роли на dev
  * RULES-1605: Отсутствует блока запроса роли (djuma@)

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-27 13:57:32

0.83.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1604: Не отрисовывается паспортный логин

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1603: Синхронизация дерева ролей в тестинге поломалась
  * RULES-1605: Отсутствует блока запроса роли (djuma@)

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1604: В URL, относящихся к системе, нужно использовать регулярное выражение, валидирующее slug, а не username

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1554: Закрасить старую ручку с ролями для фронта

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1611: Использовать прямой FK для пермишенов
  * RULES-1617: Не использовать декоратор staff\_member\_required
  * RULES-1618: Убрать лишнее использование plugins.get

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-25 22:39:57

0.83.10
---

  * RULES-1579: Нужна ручка удаления неконсистентности
  * RULES-1587: Передавать поля роли в fields\_data
  * RULES-1599: Прописывать path у каждой роли
  * RULES-1568: Ручка саджеста ролей для списка ролей
  * RULES-1357: html в комментариях action
  * RULES-1571: Апдейт ручки ролей системы

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-04-23 13:30:45

0.83.9
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1593: Оторвать зависимость ручки от параметра users
  * RULES-1567: Ручка саджеста людей для списка ролей

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1584: Пустые роли в саджесте
  * RULES-1595: Не портить рабочую копию при сборке

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-22 10:24:11

0.83.8
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1524: Ошибка в синхронизации данных с AD
  * RULES-1521: Сломалось взаимодействие со splunk
  * RULES-1584: Пустые роли в саджесте

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1565: Добавил статистику в отчёт, доработал создание action-а в случае, если пользователь неактивен

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Revert "Revert "RULES-1564: Выставить timeout uwsgi""

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-04-20 16:49:17

0.83.7
---

  * RULES-1422: Скрипт сборки пакета

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-04-14 20:53:29

0.83.6
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1565: Асинхронная работа с неконсистентностями

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1520: Celery таски не могут найти экшены в БД

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-14 19:31:44

0.83.5
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1563: Адрес тестового Blackbox не соответствует адресу тестового паспорта

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1422: Скрипт сборки пакета
  * RULES-1457 roles suggest

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-04-14 14:30:47

0.83.4
---

  * Revert "RULES-1564: Выставить timeout uwsgi"

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-13 19:55:37

0.83.3
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1525 additional logging in curl\_requests
  * RULES-1539 check user permissions for workflow
  * RULES-1528 fix loggers name
  * RULES-1551 generate rules for firewall
  * RULES-1542 patch all external calls
  * RULES-1552 raw fields in admin page

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1517: Инстанс для похода во внешний blackbox брать из настроек
  * RULES-1479: Подтверждающий подтверждает сам себя
  * RULES-1558: Ошибка во время ошибки: unhashable type
  * RULES-1409: Дублируются роли при обнаружении неконсистентности и синхронизации
  * RULES-1562: Устранить ошибку "unqualified exec is not allowed in function"

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1202: выдача связных ролей в случае импорта ролей из системы
  * RULES-1564: Выставить timeout uwsgi

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-13 19:06:47

0.83.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * RULES-1499: Отсутствующий руководитель не является руководителем

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1515: *.conf.local не должны попадать в пакет
  * RULES-1202: прокидка scope в симуляцию workflow

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1518 turn off ldap re-blocking
  * RULES-1404 default approvers

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Модуль decorator используется в тестах, но его нет в dev-зависимостях
  * Перенёс mysqldb зависимость из debian зависимостей в pip-зависимости
  * Локально конструкция socket.gethostbyname(socket.gethostname()) падает с исключением

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1516: фикс зависимости от mysqldb
  * RULES-1202: выдача связных ролей в случае импорта ролей из системы
  * RULES-1530: Почистить файлы в репозитории
  * RULES-1530: scripts/* не кладем в пакет

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-06 13:06:15

0.83.1-1
---

  * Пересборка

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-02 19:11:51

0.83.1
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1510: Билеты: Ошибка

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-02 18:59:10

0.83.0
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1511: Повторное блокирование в AD: Добавить адресата в отчеты

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Revert "Merge pull request #114 from idm/feature/1457"
  * RULES-1476: Смигрировать на django\_idm\_api
  * RULES-1477: Учет прав внутри Управлятора с ограничениями
  * RULES-1202: Выдавать права внутри Управлятора админам групп в Стаффе

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-02 15:13:43

0.82.11
---

  * RULES-1422 build hotfixes
  * RULES-1508 fix can\_approve
  * RULES-1501 fix test

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-04-01 18:33:46

0.82.10
---

  * RULES-1501 fix workflow link
  * RULES-1507 changelog in conductor

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-04-01 17:16:47

0.82.9
---

  * RULES-1501 fix workflow link

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-31 16:58:54

0.82.8
---

  * RULES-1500 system option - check certificate

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-30 17:43:25

0.82.7
---

  * UNRELEASED

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-30 17:36:34

0.82.6
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1495 add yandex\_money to rood departments

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1497: Выпилить xscript из старой верстки
  * RULES-1497: фикс статик урла

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-27 20:23:27

0.82.5
---

  * RULES-1494 remove apostol from team emails

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-27 10:46:02

0.82.4
---

  * RULES-1490 fir workflow test

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-26 13:46:21

0.82.3
---

  * RULES-1451 drop unused packages

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-24 16:14:04

0.82.2
---

  * RULES-1451 build script
  * RULES-1389 fix plugin error message
  * RULES-1451 sort dependencies
  * RULES-1451 update dependencies

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-24 11:28:37

0.82.1
---

  * RULES-1465 collect commands duration to graphite
  * RULES-1467 diff in wf save handle
  * RULES-1451 djblets 0.7.30
  * RULES-1389 show system error message in role history

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-23 14:12:48

0.82.0
---

  * RULES-941 lock command
  * RULES-1452 lock and translation decorators
  * RULES-1441 change admin email
  * RULES-1430 additional logging
  * RULES-1430 requests in transactions
  * RULES-1460 remove use\_master
  * RULES-1391 frontend api for workflow
  * RULES-1459 Django 1.6.11
  * RULES-1451 add role to error log message
  * Version 0.82

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-20 11:03:01

0.81.0
---

  * RULES-941 lock command
  * RULES-1439 fix passport logins collection
  * RULES-941 additional logging
  * Version 0.81

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-11 15:34:51

0.80.8
---

  * UNRELEASED

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-05 10:20:33

0.80.7
---

  * UNRELEASED

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-05 10:15:55

0.80.6
---

  * UNRELEASED

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-05 09:44:03

0.80.5
---

  * Version 0.80.4
  * RULES-1338 use master db for actions

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-04 23:21:53

0.80.4
---

  * RULES-1422 update pillow version

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-04 22:16:06

0.80.3
---

  * RULES-1423 fix logins generation

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-04 18:15:50

0.80.2
---

  * RULES-1422 build script

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-04 16:16:11

0.80.1
---

  * RULES-1386 Django 1.6.10
  * RULES-1397 passport logins
  * RULES-1371 fix expire date
  * RULES-952 separate depriving of fired users and expired roles
  * RULES-1401 save approvers in action comment during review\_request
  * RULES-941 reblock AD users
  * RULES-1416 remove old ldap credentials
  * RULES-1410 test for 'all\_users\_with\_role'
  * RULES-889 check if user already in old ones

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-03-04 12:30:14

0.79.0-10
---

  * RULES-1384 role humanization
  * RULES-1339 filter roles log for autotests

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-02-10 11:43:32

0.79.0-9
---

  * RULES-1367 view broken systems by permission

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-02-09 19:44:13

0.79.0-8
---

  * RULES-1367 is\_developer in meta handle

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-02-09 12:19:19

0.79.0-7
---

  * RULES-1375 idm mail header
  * RULES-1382 upravlyator version for sentry

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-02-09 11:31:26

0.79.0-6
---

  * RULES-1336 inactive roles wouldn't be rerequested
  * RULES-1359 lowercase passport logins
  * RULES-1358 role aggregation handle
  * RULES-1375 send mail from development onlly to team emails

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-02-06 09:49:23

0.79.0-5
---

  * RULES-1331 rerequested\_at in frontent api - inactive roles

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-01-30 16:47:51

0.79.0-4
---

  * RULES-1337 refresh roles by robot-idm
  * RULES-1331 rerequested\_at in frontent api

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-01-30 16:09:48

0.79.0-3
---

  * RULES-1345 fix libcurl version

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-01-28 12:56:02

0.79.0-2
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1342 Неправильный класс ошибки requests

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1345 fix passport validation
  * RULES-1345 fix libcurl version
  * RULES-1345 role data without role

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-01-28 12:19:52

0.79.0-1
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1301: block and deprive users
  * Rules-1332: environment in emails
  * RULES-1202 revert
  * Rules-1332: email header prefix in settings

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1336 Отдавать дополнительные параметры роли
  * RULES-1340 Список сломанных систем в ручке meta
  * RULES-1330 Неправильно определяется причина запроса роли

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-01-24 12:46:23

0.78.0-10
---

  * Пересборка

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2015-01-20 15:57:09

0.78.0-9
---

  * RULES-1329: log, filtered by time

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2015-01-20 14:09:48

0.78.0-8
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * Increase inflector timeout
  * Fix inflector

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2015-01-16 12:11:50

0.78.0-7
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1324 Ретраи в RoleRemoved

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2015-01-15 20:25:28

0.78.0-6
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1296 — Перенести очередь в redis

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1321: fix role humanizing
  * RULES-1263: users inflection

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2015-01-15 17:44:07

0.78.0-5
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-946: password cannot contain some punctuation signs

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2015-01-13 20:39:30

0.78.0-4
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-946: fix

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2015-01-13 18:24:45

0.78.0-3
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1287 Использовать механизмы django\_yauth в тестах
  * RULES-992 Не выдавать права пользователю, которого нет на стаффе

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-946: random passport passwords

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2015-01-13 13:43:42

0.78.0-2
---

  Пересборка

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-12-22 18:37:49

0.78.0-1
---

  *

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2014-12-22 16:13:52

0.78.0
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1210 Фикс
  * RULES-1243 Удалил устаревшие настройки django\_intranet\_auth
  * RULES-1096 Избавиться от внешней статики
  * RULES-962 Сохранять состояние баз в локальный memcached
  * RULES-1300 Получение версии при сборке пакета
  * RULES-1113 Правильная версия django-multic
  * RULES-1298 Фикс мониторинга celery

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1296 — Перенести очередь в redis

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2014-12-22 14:20:19

0.77.0-6
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1210 Фикс

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-12-11 16:44:47

0.77.0-5
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * Удалены неиспользуемые права

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-12-11 13:13:26

0.77.0-4
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * Зависимость от yandex-environment-intranet

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-12-10 18:46:45

0.77.0-3
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1243 Фикс миграций после удаления django\_intranet\_auth

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-12-10 17:36:05

0.77.0-2
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1291 Комментарии к действиям над запросом роли в API

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-12-10 16:31:08

0.77.0-1
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1243 Улучшенная аутентификация в API
  * RULES-1210 Отключение кеша плагинов

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1280 gzipped json in reversion
  * RULES-1272 compress versions table

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2014-12-10 14:26:13

0.76.0-3
---

  * Пересборка

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-12-08 18:55:27

0.76.0-2
---

  * RULES-1270 Поправил версию libcurl-dev
  * RULES-1278 Текущее состоянии роли в данных очереди запросов

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-12-08 14:52:43

0.76.0-1
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-1270 — Починить запуск юнит-тестов в TeamCity

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1274 Правильная обработка запросов ролей с параметрами

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-12-04 15:39:06

0.75.0-4
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1241 Генерация паспортных логинов для систем
  * RULES-1241 PEP-8
  * RULES-1259 Фильтр запросов ролей по approved
  * RULES-1253 Фильтр запросов ролей по системе
  * RULES-1255 Человеческое описание роли в запросах ролей
  * RULES-1258 Данные о причинах заявки в запросах ролей
  * RULES-1259 Фильтр запросов ролей по состоянию запроса
  * RULES-1254 Список систем с запросами ролей
  * RULES-1254 Названия систем в списке систем с запросами ролей
  * RULES-1256 фикс команды ping
  * RULES-1267 Отдавать в логи роли ошибку, которую отдает система
  * RULES-1268 Информация про действия над запросом роли в API

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1202 staff groups

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2014-11-28 16:34:06

0.75.0-3
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1246 Права на просмотр роли

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1247 Письма про уволенных

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2014-11-28 13:32:55

0.75.0-2
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1248 - исправлено кэширование отсутствующих сотрудников

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2014-11-18 18:49:38

0.75.0-1
---

 * [Mikhail Polykovskij](https://staff.yandex-team.ru/Mikhail%20Polykovskij)

  * RULES-1205 discard workflow, saved by user
  * RULES-1212 show full diff in workflow history
  * RULES-1012 notify about fired users in workflows
  * RULES-1087 view diff between dev and system workflow
  * RULES-1087 observe renamed departments in workflow

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1219 Ошибка при отдаче информации по ролям
  * RULES-1123 Ручки для экрана отчетов
  * RULES-903 Забирать номер телефона из центра перед отправкой СМС
  * RULES-1231 Показываем всегда все доступные роли

 [Mikhail Polykovskij](https://staff.yandex-team.ru/glader@yandex-team.ru) 2014-11-10 16:50:38

0.73.0-3
---

  * RULES-1179 Обновил список адресов для нотификаций
  * Пересборка из-за неправильного ченджлога

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-10-28 14:49:16

0.73.0-2
---

  * RULES-1198 Фикс тестов

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-10-27 20:18:11

0.73.0-1
---

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-1152: username робота Управлятора в API теперь "idm-robot"
  * RULES-1122: API для получения списка запросов ролей, их подтверждения и отказа
  * RULES-1168: оставил ручку /login-as/ лишь на тестинге и девелопменте

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1170 Скрипт для анализа переименованных департаментов
  * RULES-673 Фикс разлогинивания уволенных сотрудников
  * RULES-1186 Юникодное логгирование в аудите
  * RULES-1180 Исправил страницу дергателя ручек
  * RULES-1179 Изменил адреса для нотификаций

 [Vladimir Moskva](https://staff.yandex-team.ru/vladmos@yandex-team.ru) 2014-10-27 15:28:54

0.72.0-1
---

  * RULES-1153: позволяем pytz обновляться самостоятельно
  * RULES-1128: в объекте запрошенной роли отдается информация об оставшихся для нее подтверждениях
  * RULES-1152: при симуляции запроса роли список аппруверов отдается так же, как и в оставшихся подтверждающих запрошенной роли

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-10-14 16:24:21

0.71.0-2
---

  * RULES-1144: команда для удаления дубликатов теперь требует явного указания флага, чтобы начать удалять + удаляет исходные неконсистентности

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-10-13 18:34:01

0.71.0-1
---

  * RULES-1144: команда для удаления дубликатов записей о ролях

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-10-13 17:49:08

0.70.0-9
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1103 Более правильная зависимость libcurl

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-10-10 15:54:42

0.70.0-8
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1103 Правильная зависимость libcurl

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-10-10 14:26:30

0.70.0-7
---

  * RULES-1103: поправил POST запросы в переходе на pycurl - был баг с заполнением тела запроса и стоял не тот content-type + тесты
  * RULES-1103: добавил в debian зависимости пакета нужную для pycurl версию libcurl4-openssl-dev
  * RULES-1131: теперь в админке всем членам команды Управлятора видны все подключенные туда модели (хотя править их может по-прежнему лишь суперадмин)

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-10-09 23:56:47

0.70.0-6
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-961 Переезд с pylibmc на python-memcached
  * RULES-961 Удалил лишние build depends
  * RULES-1120 Management-команда для нормализации дерева ролей
  * RULES-1103 Опечатка в названии класса

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-10-09 19:33:47

0.70.0-5
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1103 Обвязка над pycurl для работы SNI
  * RULES-1103 Переход на новый интерфейс к CURL в работе с системами
  * RULES-1103 Улучшенное форматирование ответа в /handles/
  * RULES-1120 Хранение описания ролей всегда в расширенном формате

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-1122: в ручке /meta теперь отдается количество запросов на подтверждение ролей ждущих реакции пользователя + тест

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-10-09 16:04:42

0.70.0-4
---

  * RULES-1009: проверка наличия роли у человека для workflow перенесена в объект обертки пользователя + у объекта системы появилась возможность запросить всех пользователей с определенной ролью
  * RULES-712: стаффовое API переехало за https

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-10-02 17:38:57

0.70.0-3
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-673 Сбрасывать сессию в Паспорте при увольнении
  * RULES-1083 Дополнительная информация о пользователе в API
  * RULES-1094 Встроенный генератор QR-кодов
  * RULES-1083 Вынес итератор по департаментам в общий метод
  * RULES-1094 QR-коды для длинных паролей в аттачментах к нотификациям
  * RULES-1110 Убрать бывших сотрудников из саджеста в форме запроса

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-1009: проверка наличия роли у человека для workflow
  * RULES-1108: ручки API фронтенда, отдающие одиночный объект роли, теперь отдают в его данных флаг can\_be\_deprived

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-10-02 13:15:38

0.70.0-2
---

  * RULES-1086: ручка синхронизации ролей системы в API фронтенда
  * RULES-1097: ручка списка ролей API фронтенда теперь отдает этот список без разделения на активные/запрошенные/неактивные, но добавился фильтр по типу + тест на это поведение

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-26 16:07:59

0.70.0-1
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1078 Автоматическое подключение конфига nginx для api из postinst

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-952: добавил обработку параметра threshold команде отзыва ролей и деактивации пользователей

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-24 12:43:02

0.69.0-20
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1075 Перенес /system/handles/ в /handles/

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-23 15:22:04

0.69-19
---

  * RULES-1063: Добавил в ручку /passport-logins/ API фронтенда варианты выбора паспортных логинов. Теперь ее надо запрашивать, передавая query параметр system

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-22 18:30:59

0.69-18
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1061 Открыл API для фронтенда в продакшене

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-1064: добавил в ручку информации о пользователе данные о его паспортных логинах

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-19 13:15:25

0.69-17
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1042 Более корректное поведение ручки автокомплита для ролей

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-979: фикс перепутанных разрешений по системным ролям
  * RULES-1052: починил сломанные тесты

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1042 Объединение двух мультикомплитных ручек пользователя в одну

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-1052: исправил сломанный импорт в тестах
  * RULES-1034: добавил в ручку формы проверки на уже уволенного пользователя
  * RULES-1057: улучшил логирование захвата локов командами из cron'а
  * RULES-1051: поддержал в API фронтенда возможность запрашивать временные роли

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-18 18:37:04

0.69-16
---

  * RULES-1029: в админке и API фронтенда добавлено описание для систем

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-17 13:10:54

0.69-15
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1042 Автокомплит пользователей для запроса ролей
  * RULES-1042 Учел пожелания в ПР

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-1034: ручка /frontend/systems/ теперь при указании query параметра user дофильтровывает возвращаемый список согласно правам запрашивающего, может использоваться для формы запроса ролей на странице пользователя
  * RULES-1034: вынес ручку для формы запроса ролей на странице пользователя в отдельный ресурс /frontend/rolerequestform/, вернул прежнюю функциональность ручке систем

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-16 22:21:14

0.69-13
---

  * RULES-952: забыл перенести код в API тестировщиков

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-16 16:13:51

0.69-12
---

  * RULES-979: фикс комментариев в ручке отдачи ролей

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-16 15:42:45

0.69-11
---

  * RULES-979: отдаю для каждой роли в ручке списка ролей API статус "может быть отозвана" в зависимости от того, кто запрашивал роль
  * RULES-979: отключаю ненужный метод получания списка ролей пользователя в API, т.к. фронтенд пользуется вариантом roles/?user=<login>

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-16 13:22:27

0.69-10
---

  * RULES-952: восстановление пользователя в AD теперь работает с отдельным полем модели, а не с данными json поля
  * RULES-979: переименовал ручку /current-permissions/ в /meta/
  * RULES-979: отдаю 403 в ручке ролей если прав на запрос у человека нет

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-15 23:21:05

0.69-9
---

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-996 Хождение в LDAP-серверы в постоянном порядке для уменьшения неконсистентности
  * RULES-993 Обработка ошибок в API
  * RULES-993 Улучшения в обработке ошибок

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-979: вернул историю ролей в API тестировщиков
  * RULES-1018: возвращаю информацию о состоянии read-only в той же ручке, что и разрешения

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-11 16:53:22

0.69-8
---

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-979: отдаю список действующих прав пользователю на фронтенд

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-999: Убрал настройку UNITTEST. Явный мок через conftest.py
  * RULES-999: Растащил unittest\_settings.py по грануляркам
  * RULES-999: функция-прослойка в inflect для того чтобы правильно сделать мок

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-979: вынес все используемые разрешения Управлятора в настройки, поправил ручку их отдачи фронтенду
  * RULES-979: добавил проверки прав в API фронтенда
  * RULES-979: добавил проверки прав начальников отделов в API фронтенда

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-11 12:22:38

0.69-7
---

  * RULES-1013: ручка /ping бэкенда теперь отвечает и по адресу /ping-backend чтобы фронтенд мог ее удобно запрашивать

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-10 15:30:55

0.69-6
---

  * RULES-999: дополнительные параметры в таргет test
  * RULES-1005 Собственная ручка поиска по людям
  * RULES-1005 Smoke-тест на мультикомплит
  * RULES-999: дополнительные параметры в таргет test
  * RULES-1005 Собственная ручка поиска по людям
  * RULES-1005 Smoke-тест на мультикомплит
  * RULES-952: поправил неправильно указанные DC тестового инстанса AD в настройках

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-10 12:56:30

0.69-5
---

  * RULES-999: явно указал модули, в которых находятся celery-таски плагинов

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-04 14:59:19

0.69-4
---

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-999: для корректного запуска юнит-тестов на билд-агентах убрал raise при неправильной настройке токенов директа

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * RULES-999: добавил python-debian в зависимости сборки
  * RULES-999: запуск тестов в окружении development.unittest
  * RULES-999: при тестах логи пишутся в консоль

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-999: поправил падающие тесты
  * RULES-999: для тимсити-агента, запускающего unit-тесты, необходимо иметь все Depends зависимости из control-файла в Build-depends секции
  * RULES-973: убрал is\_absent из ответа, и добавил номер, на который отсылается смс
  * RULES-952: добавил в игнор-лист групп AD на тестинге и девелопменте роботные группы, которые там отрывать не надо
  * RULES-1002: прикрутил ajax к many-to-many полю в форме departments в админке, чтобы она не тормозила при большом количестве сотрудников в отделе
  * RULES-1000: вернул обработку людей с contract\_end\_date в процедуре idm\_deprive\_roles, до тех пор, пока механизм обработки данных от OEBS не будет включен до конца

 * [Vladimir Moskva](https://staff.yandex-team.ru/Vladimir%20Moskva)

  * RULES-1003 Удалил устаревшие разработческие конфиги

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-03 18:40:11

0.69-3
---

  * вернул nose в зависимости сборки
  * поправил сигнатуру вызова worklfow в тестах
  * убрал мешающий unit тестам вызов reload\_plugins, оставшийся от старых nose тестов
  * убрал CELERY\_ALWAYS\_EAGER для девелопмента и тестинга
  * убрал забытые принты в тестах + немного PEP-8

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-02 17:31:22

0.69-1
---

  * RULES-973: ручка запроса роли в API фронтенда теперь при симуляции возвращает не просто строку, а структуру со списком аппуроверов

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-01 14:43:36

0.68.1
---

  * RULES-1000: вернул обработку людей с contract\_end\_date в процедуре idm\_deprive\_roles, до тех пор, пока механизм обработки данных от OEBS не будет включен до конца

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-09-03 18:32:25

0.68-3
---

  * RULES-986: починил отображение ролей новых систем, выпилил модель RoleDescription за ненадобностью
  * RULES-984: поправил локальную для тестинга проблему отображения неконсистентностей

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-29 16:49:26

0.68-2
---

  * RULES-791: для того, чтобы впилить откат блокировки, отрефакторил классы в sync.ldap
  * RULES-791: разнес админки соответствующим по подмодулям, чтобы можно было удобно добавить откат блокировки в AD
  * RULES-791: откат блокировки пользователей в AD, оформлен как действие в админке
  * RULES-952: ручки блокирования в AD, увольнения в AD, восстановления уволенных в AD пользователей для тестировщиков

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-28 14:42:26

0.68-1
---

  * RULES-952: вынес список OU активных пользователей в настройки для удобной работы с тестовым LDAP
  * RULES-952: сделал возможность асинхронного запуска команд для тестировщиков

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-25 15:23:45

0.68
---

  * RULES-952: на тестовом инстансе  AD другие DC и он работает по LDAP а не по LDAPS

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-22 18:03:21

0.67.1
---

  * RULES-977: дурацкая описка при переносе не позволяла открывать список исключений Splunk + тесты чтобы это больше не повторилось

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-22 14:10:25

0.67-1
---

  * RULES-933: вкрутил для нормальной работы в админке ajax для поля contacts (ответственных)
  * RULES-974: обновляемся до Django 1.5.9 всвязи с вышедшим security-fix'ом
  * RULES-975: включаем djcelery в админке

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-21 17:20:28

0.67
---

  * RULES-934: ручка в API фронтенда, возвращающая описание ролей системы

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-21 16:10:32

0.66-16
---

  * RULES-971: теперь можно рассказывать Управлятору о паспортных логина пользователя через админку
  * RULES-935: для стабилизации работы тестов включаю celery в синхронном режиме

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-20 15:06:27

0.66-15
---

  * RULES-933: email'ы системы в API фронтенда отдаются списком + тест на это
  * RULES-970: убрал Сашу art@ из получателей отчета о проблемах синхронизации с центром, добавил рассылку

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-18 15:02:27

0.66-14
---

  * RULES-712: миграция на новое поле - флаг блокировки пользователя в LDAP
  * RULES-963: выпилил более ненужный код, относящийся к старой процедуре взаимодействия с OEBS
  * RULES-933: у систем появилось поле contacts - ответственные за систему. Заполняется через админку, отдается  через API фронтенду
  * RULES-969: в целях унификации все ответы API фронтендеров и тестировщиков, которые отдаются без тела, теперь имеют http код 204
  * RULES-970: убрал ненужные TODO из кода, добавил нужных + PEP-8
  * RULES-970: починил тесты добавления ролей и синхронизации данных с системами
  * RULES-970: перевел команду idm\_drop\_virtual\_machines на использование requests  + написал тесты для нее
  * RULES-970: убрал пару неиспользуемых файлов из проекта
  * RULES-970: PEP-8 правки в командах работы со splunk и выставления sid67 внешним паспортным логинам

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-15 17:57:16

0.66-13
---

  * RULES-712: перенес все, относящееся к пользователю, в отдельный модуль upravlyator.user
  * RULES-712: сделал команду синхронизации данных об окончании даты контракта и даты NDA со стаффом + тесты на нее
  * RULES-712: переделал команду блокировки пользователей по данным из OEBS, упростил все по спецификации из таска
  * RULES-942: включаю выполнение по расписанию авторазрешения неконсистентностей + поправил описания команд
  * RULES-902: API фронтенда при создании запроса на роль возвращает в ответе данные созданной роли с кодом 201. Также роли в состоянии "approved" попадают в список "requested" в ручке списка ролей пользователя

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-13 17:01:12

0.66-12
---

  * RULES-902: ручка списка ролей для фронтенда теперь  возвращает 3 списка - "active", "inactive", "requested"

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-11 19:22:42

0.66-11
---

  * RULES-885: вынес код, работающий лишь на тестинге, в отдельный модуль
  * RULES-885: сделал белый список в админке, куда можно отправлять письма с тестинга. Также в этот список попадают email'ы команды и email'ы систем. Письма с тестинга теперь можно узнать по отправителю.

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-10 20:10:53

0.66-10
---

  * RULES-934: ручка в API тестировщиков и фронтэнда, позволяющая восстановить сломанную систему

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-09 10:22:30

0.66-9
---

  * RULES-917: поправил некорретное отображение даты последнего изменения workflow
  * RULES-890:  поправлен механизм регулярного пересмотра - теперь работает для ролей старше 360ти дней, не учитывает дату последнего обновления workflow систем, добавляет в логи событие автоматической перевыдачи роли, если у той нет подтверждающих
  * перевел тесты data\_sync на pytest
  * RULES-890: поправил тесты регулярного пересмотра ролей в связи с последними изменениями логики в этом месте
  * RULES-955: явным образом запрашиваю пользователя при открытии очереди запросов ролей
  * обновил Django до 1.5.8

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-07 19:38:40

0.66-8
---

  * RULES-954: заменил текст ошибки ненайденного правила обработки запроса роли

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-06 16:13:46

0.66-7
---

  * RULES-942: откат случайно закоммиченного кода из прошлого коммита

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-06 15:55:33

0.66-6
---

  * RULES-951: доработал ручку обновления роли в API  для тестировщиков - теперь позволяет менять у роли пользователя и систему, что нужно для тестов механизма неконсистентностей + тесты
  * RULES-953: проверка на celery будет загораться лишь если после последнего выполнения таска обновления сигнальной таблицы прошло больше 12ти минут
  * RULES-942: перевел тесты, относящиеся к неконсистентностям на py.test
  * RULES-942: отрефакторил текущий вариант авто- и ручного разрешения неконсистентностей, вынес прогон workflow над ролью в отдельный метод, чтобы убрать копипасту
  * RULES-942: поправил механизм разрешения неконсистентностей - теперь он создает роли в состоянии "Перезапрошена", а не "Запрошена" как раньше + тесты на это поведение

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-06 15:35:40

0.66-5
---

  * RULES-856: поправил формат данных, принимаемый ручкой запроса роли в API тестеровщиков

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-04 10:43:33

0.66-4
---


  * RULES-856: поправил формат данных, принимаемый ручкой запроса роли в API тестеровщиков

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-04 10:43:33

0.66-4
---

  * RULES-951: доработал команды проверки и разрешения неконсистентностей для тестировщиков - теперь они принимают доп параметры для тонкой настройки работы

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-08-01 01:47:27

0.66-3
---

  * RULES-856: добавил ручку создания запроса на выдачу роли в API для тестировщиков
  * RULES-951: добавил ручки списка неконсистентностей в API для тестировщиков
  * покрыл тестами API для тестировщиков

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-31 18:27:59

0.66-2
---

  * RULES-910: роль в статусе "Запрошена" будет отсылаться на новый фронтэнд как активная.

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-30 20:22:17

0.66-1
---

  * RULES-948: ручка для отзыва роли

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-30 18:48:37

0.65.2
---

  * RULES-949: временно отключаем удаление исчезнувших из дерева ролей системы для Бункера

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-31 15:04:25

0.65.1
---

  * RULES-927: вынес в кэш описание ролей

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-29 14:29:59

0.65-5
---

  * RULES-944: снизил уровень логирования ошибок workflow при ежедневной проверке до WARNING
  * сделал логи в паре мест более sentry-friendly (чтобы сентри группировала их по шаблонам сообщений) + PEP-8 правки
  * RULES-927: на всякий случай в fallback на получении описания роли сделал пошире отлов exception'ов

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-28 17:59:53

0.65-4
---

  * RULES-931: сделал ручку логов по роли доступной ввиде ресурса actions
  * RULES-940: сделал ручку создания запроса на получения роли
  * RULES-939: сделал ручку проверки запроса на получание роли
  * RULES-924: поправил код ответа ручки, делающей роль протухшей

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-25 18:14:38

0.65-3
---

  * RULES-924: т.к. нужна тестировщикам нужна специальная ручка правки ролей, вынес API для них в отдельный namespace и отдельный модуль, отнаследов его от API фронтэнда
  * RULES-924: собственно добавил ручку обновления информации о роли
  * RULES-924: восстановил ручки удаления роли для тестеров, потерянные после переноса в отдельный модуль

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-25 12:53:27

0.64.1
---

  * RULES-937: поправил ошибку определения заместителей в случае, когда начальник отдела в нем не работает

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-23 17:55:13

0.65-2
---

  * RULES-932: тестовый Управлятор теперь заводит логины внешнего паспорта через тест инстанс паспорта
  * RULES-927: переместил fallback выше по стеку вызовов, потому что прошлый вариант пытался найти запись в той же транзакции и падал с DoesNotExist
  * RULES-902: включил сортировку по пользователям и системам для ролей, для чего сделал им кастомные поля и завел базовый класс для API
  * RULES-934: сделал альтернативный вариант обращения за данными о ролях системы в формате frontend/rolesmeta/?system=self
  * RULES-922: отключил старый тестовый механизм блокировки сотрудников по данным из ОЕБС
  * RULES-931: ручка с историей действий по роли
  * RULES-929: trailing slash в ссылках в интерфейсе теперь опциональны

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-21 23:21:48

0.64
---

  * RULES-846: откатываю обратно из-за проблем с logging.handlers.WatchedFileHandler в idm.roles логгере

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-17 18:48:54

0.63
---

  * RULES-836: убрал старый вариант обработки логов ошибок взаимодействия с системами
  * RULES-927: давлю integrity error от базы при получении описания роли + немного логов в это место
  * RULES-924: ручка регулярного пересмотра ролей получила параметры --system, --since, и --force
  * RULES-910: добавил возможность сортировки ручке ролей пользователя
  * RULES-925: добавил на тестинге в ответ ручки со списком ролей пользователя статус роли, чтобы тестировщикам было удобно

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-17 16:44:37

0.62
---

  * RULES-910: разделил ответ ручки ролей в API фронтэнда на активные и неактивные роли
  * RULES-916: ручка систем в API фронтэнда, отдающая в том числе и структуру ролей системы

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-14 12:50:48

0.61
---

  * RULES-910: отрефакторил аутентификацию, добавил логов, чтобы удобнее было дебажить новое API
  * RULES-913: добавлены роли для безопасников и хэлпов, безопасникам уходят персональные уведомления об изменении workflow

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-10 18:36:34

0.60-2
---

  * RULES-910: переименовал api для фронтэнда в более подходящий по смыслу вариант;
  * RULES-910: сменил адреса ресурсов пользователя и роли по REST - на их же множественное число;
  * RULES-910: воткнул фильтр ролей по логинам пользователей, по системам и по состоянию.
  * добавил логирования в случае, когда лок нельзя взять в зукипере
  * улучшил логи, которые пишутся при деактивации пользователя в AD

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-10 01:38:14

0.58
---

  * RULES-910: перенес api v1 в отдельный package
  * RULES-910: подновил django-tastypie, используемую в проекте
  * RULES-910: добавил в api v2 ручки пользователя и роли пользователя
  * добавил логирования в процесс обновления департаментов из центра
  * для удобства работы, добавил URL запрашиваемой системы в ручки system/handles
  * для удобства работы, добавил в поиск в департаментах в админке их id и  slug

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-08 16:53:23

0.57
---

  * RULES-897: в команду починки пользователей, у которых стоит неправильный статус ldap\_active в базе, добавлено логирование и очистка логинов, считанных из файла
  * RULES-906: убираю вызов get\_user\_model() в SSL auth бэкенде, ломающий multi\_db конфигурацию для некоторых пользователей

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-07 16:18:25

0.56
---

  * RULES-908: аутентификация по токенам теперь работает и для https
  * вынес захардкоженные логин-пароль от старого LDAP в datasourses; использую тестовый AD и для девелопмента

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-03 18:42:22

0.55
---

  * поправил имя логгера в management команде, чтобы соответствовало ее имени
  * Для тестинга используется тестовый инстанс AD

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-02 18:57:24

0.54
---

  * RULES-906: из-за len() queryset валился при обработке на любой slave базе
  * добавил логирования в процесс синхронизации изменений в дереве ролей систем
  * Включил авто-обновление ролей бункера на тестинге
  * RULES-897: команды для сверки и исправления ситуации с дважды уволенными людьми
  * RULES-897: учитываем возможность снова пришедших в компанию сотрудников при синхронизации данных с Центром

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-07-02 17:17:30

0.53
---

  * RULES-846: забытый фильтр по аппруверу для ручки API очереди запросов на подтверждение для тестировщиков
  * RULES-846: ручка в API для тестировщиков, позволяющая вручную сделать любую роль протухшей

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-26 15:47:28

0.52
---

  * RULES-895: поправил ошибку переноса кода, допущенную при выделение workflow в отдельный package

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-25 16:46:16

0.51
---

  * RULES-892: для бункера автообновление ролей раз в минуту

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-25 16:19:27

0.50
---

  * RULES-895: сделал для workflow отдельный package
  * RULES-895: теперь в workflow доступно представление роли как ноды дерева ролей
  * RULES-898: починил интерфейс настройки автообновления ролей систем

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-25 13:54:26

0.49
---

  * RULES-891: ходим в API система с хедером Accept="application/json; charset=utf8"
  * RULES-887: ходим в мастер еще и на system-workflow-edit ручку
  * RULES-893: разделителем в логе действий с ролями стал \t, вместо неудобных пробелов

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-23 12:56:13

0.48
---

  * RULES-887: для view, ломающегося при работе со репликой бд, добавил исключение в роутер. Возвращаю работу с репликами.
  * RULES-856: ручка для тестировщиков, возвращающая hash запросов ролей

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-17 17:08:46

0.47
---

  * RULES-887: отключаю поддержку нескольких реплик из-за бага на продакшне.

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-16 20:27:16

0.46-1
---

  * RULES-884: добавил обработку варианта, когда CENTER API вернул пустой список подразделений + тест на это место
  * RULES-883: у базы на продакшне теперь 2 read-only копии, добавил настройки для их корректной поддержки
  * RULES-869: при отзыве ролей на стороне системы роли в Управляторе роли тоже получают статус "Отозвана", а не "Отзывается", как было раньше

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-16 17:46:12

0.45
---

  * RULES-856: для нормального разделения тестовых вьюшек от продакшновых, вынес все хелперы и ошибки в отдельные модули и отрефакторил views.py по PEP-8
  * RULES-856: на девелопменте и тестинге ходим в API тестового центра
  * RULES-856: перенес вьюшку call\_command в отдельный модуль + тест для нее
  * RULES-856: вытащил в API Управлятора список ролей пользователя в состоянии "Необходимо перезапросить"

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-11 22:44:54

0.44
---

  * RULES-880: возвращаю BOM для читаемости csv файлов отчетов в виндовом excel

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-11 13:34:40

0.43
---

  * RULES-879: отчет по активным ролям

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-11 13:03:14

0.42
---

  * исправления мониторингов в связи с переходом на https и отключением cron на тестинге

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-11 12:01:30

0.41
---

  * Вынес неконсистентности в отдельную подпапку
  * передвинул csrf миддлварь повыше
  * RULES-869: если у нас есть роль, а в системе - нет, то при принятии неконсистентности роль у нас удалится

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-10 19:46:48

0.40
---

  * RULES-875: отчеты теперь сразу посылаются аттачем в письме

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-09 19:39:45

0.39
---

  * В отчете по ролям отображаются все роли, которые были выданы в интересующий нас промежуток
  * RULES-875: отчеты отдаются через memcached, а не через локальную файловую систему app-сервера

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-09 18:29:49

0.38
---

  * RULES-856: ручка для запуска management команд в тестинге

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-06-05 17:49:09

0.37
---

  * RULES-862: Добавил команду удаления запросов, дублирующих уже выданные роли
  * RULES-862: Автоматическое разрешение неконсистентностей помечает их как разрешенные при запросе ролей
  * RULES-862: Убрал автоматическое разрешение ролей из крона

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-05-29 17:36:19

0.36
---

  * RULES-862: Починил приняние неконсистентностей со стороны системы в интерфейсе - теперь роли после него выдаются сразу.
  * RULES-862: Добавил команду, выдающую зависшие в состоянии "Подтверждено" после разрешения неконсистентностей роли
  * RULES-862: Починил поиск по неконсистентностям в админке

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-05-26 15:53:58

0.35
---

  * RULES-860: меняю директивы nginx-enable-mod для переезда апи на отдельный слб
  * указал правильный путь архива с changelog для показа версии в интерфейсе

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-05-22 18:16:46

0.34
---

  * забытая настройка для monrun'а celery
  * Починил тесты. Теперь они запускаются через py.test
  * убрал более ненужную ручку таблицы состояния всех подключенных систем - переезд закончился, смысла в ней больше нет
  * Починил команду idm\_check\_approves\_difference - теперь она корректно работает с ошибками workflow, посылает письма лишь команде Управлятора и не ломается вся при ошибке подсчета в одной из систем.
  * правильные права папкам с логами в postinst

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-05-22 18:01:46

0.33
---

  * RULES-850: Возвращаю создание объектов неконсистентностей системы при регулярной проверке, возвращаю неконсистентности в админку
  * Сделал monrun проверку живости celery

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-05-15 18:32:01

0.32
---

  * временно отключаю отсылку логов ошибок ответственным по системам
  * RULES-840: пишем логи действий с ролями также отдельно в файл, чтобы их потом могли отсылать в SPLUNK
  * перевожу development на отдельную базу, добавил настройку для django\_intranet\_auth
  * RULES-810: разработчики и аудиторы могут смотреть в админку в режиме read-only

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-05-12 17:41:07

0.31-32
---

  * костыль для Директа, к которому ходим с токенами, привязанными к IP наших серверов

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-30 17:44:52

0.31-31
---

  * добавил проверки на анонимуса при попытке добавления роли через API

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-30 16:40:01

0.31-30
---

  * фикс аутентификации по сертификату для API

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-30 15:06:04

0.31-29
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс пути до сертификата в деве

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * фикс cron команды на генерацию правил для firewall

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-30 14:47:22

0.31-28
---

  * правильная версия djangpo\_russian

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-29 16:47:55

0.31-27
---

  * поправил url центра в продакшне еще раз

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-29 15:16:57

0.31-26
---

  * поправил url центра в продакшне
  * поправил команду синхронизации с центром в cron'е

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-29 14:52:44

0.31-24
---

  * добавил разработчикам возможность дергать системные ручки info
  * добавил в проверяемые дырки дырку для складывания логов безопасникам

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-29 00:06:07

0.31-23
---

  * запускаем cron на продакшне

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-28 21:04:50

0.31-22
---

  * убрал хардкод ldap хоста из кода
  * добавил недостающих настроек из django\_intranet\_auth
  * добавил кастомную read-only миддлварь с управлением из админки
  * врубил вафлю для проверки сертификата клиента
  * забытый шаблон с кнопкой read-only режима для админки

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-28 20:15:11

0.31-21
---

  * правильная ссылка на staff для продакшна

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-28 14:46:51

0.31-20
---

  * временно убрал поход в склонятор в real-time'е

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-24 21:16:53

0.31-19
---

  * сделал отдельный misc.production конфиг с нужными там настройками

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-24 20:28:39

0.31-18
---

  *  * в settings поправлены настройки BLACKBOX\_PASSPORT\_URL и RAVEN\_CONFIG.  * из settings убраны более ненужные настройки URL\_1C, DIRECT\_URL  * исправлено распознавание дырок для zookeeper'а

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-24 18:00:23

0.31-17
---

  * добавил management команду проверки дырок для систем

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-24 14:34:30

0.31-16
---

  * в настройках ALLOWED\_HOSTS теперь разрешены любые, т.к. они ломали балансер
  * запилил management команду, проверяющую дырки для проекта. Дырки ищутся в настройках автоматом.

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-24 13:04:04

0.31-15
---

  * добавил в зависимости  simplejson==2.3.2

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-23 22:54:42

0.31-14
---

  * выпилил из проекта более ненужный stratostat

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-23 22:27:00

0.31-12
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Зависимость от libmemcached6

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-23 20:52:23

0.31-11
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Правильный кеш бекэнд

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * избавился от зависимости python-apt, у которой вызов open cache занимал по 4 секунды
  * слешка поправил кэширование несклоняемых слов + мелкие украшательства

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-23 19:30:08

0.31-10
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Правильное использование memcached

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-23 15:45:16

0.31-9
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс относительных импортов в utils/\_\_init\_\_.py

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-23 13:41:28

0.31-8
---

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * выпилил SENTRY\_DSN из datasources унес CENTER\_API\_URL в настройки, зависящие от окружения
  * поправил пользователя, от которого в cron запускалась команда генерации правил для firewall

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Эти зависимости переехали в base.txt
  * Подключаем ylock
  * Использование локов в management командах
  * Отключаем access лог uwsgi

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-22 16:58:13

0.31-7
---

  * корректно указал версию выкаченного пакета 0.31-6ubuntu1
  * фикс бага при обращении к центру
  * убрал упоминание более не нужной папки логов celery

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-21 18:50:48

0.31-6ubuntu1
---

  * Сделал страницу просмотра состояния систем для суперпользователя
  * Перенес из datasources не относящиеся к ним настройки

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-21 16:58:10

0.31-5
---

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * убрал зависимость от memcache-multiple, т.к. сейчас этот пакет не ставится в дев- и тест- окружения
  * перенес шаблоны отчетов в общую папку к остальным шаблонам
  * Добавил логирование ошибок в sentry
  * Добавил MEDIA\_ROOT в настройки
  * Обернул обращения в центр в try: except

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-21 12:52:52

0.31-4
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Отладочная пересборка
  * Обновил cron
  * Сетинги тоже в пакет надо положить
  * Фикс опечатки в bash'е
  * Фикс конфигов
  * Фикс манифеста
  * Фаб таска для рестартов
  * Правильные настройки в manage.py

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * RULES-829: Добавил в дебианизацию конфиг memcached

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Включаем в девелопмента debug
  * Зависимость от правильного robe

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * поправил версию python-ldap в зависимостях
  * Добавил недостающих зависимостей
  * Добавил development комплект настроек
  * поправил плохое название

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Зависимость от nginx и подкление конфига в postinst

 * [Timur Zaripov](https://staff.yandex-team.ru/Timur%20Zaripov)

  * поправил outfile в конфиге memcached и добавил зависимость в control
  * Поправил management команду генерации правил для firewall
  * ручка ping ходит через https
  * корректно отображаем changelog

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-18 14:47:27

0.31-1
---

  * Отладочная пересборка

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-16 17:32:45

0.31
---

  * RULES-818: Поправлена сборка пакета для пеезда к админам вертикальных сервисов. Пакет переименован в yandex-tools-idm
  * RULES-818: Поправлены пути к логам в командах
  * RULES-818: Добавлена ручка /ping для балансеров
  * RULES-818: Добавлено логирование в месте обращения к склонятору + simplejson заменен на json

 [Timur Zaripov](https://staff.yandex-team.ru/q210@yandex-team.ru) 2014-04-16 16:53:16

0.21
---

  * В отчетах по ролям временные границы вновь применяются к дате последнего изменения роли. RULES-823.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-09 17:56:05

0.20
---

  * Исправлен баг, при котором ошибка при перезапросе ролей сотрудником мешала корректной обработке изменений про него, пришедших из центра. RULES-812.
  * В csv отчета по ролям появилась колонка "код роли", содержащая служебную информацию о ролях. RULES-800.
  * Файл fabfile.py поправлен таким образом, чтобы команды обновления changelog и коммита его в репозиторий были отдельными.
  * Файл fabfile.py поправлен таким образом, чтобы метки тикетов в changelog'е перемещались в конец коммит-мессаджа.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-07 21:28:31

0.19.0
---

  * В тестовом окружении включена отправка всех писем на специальные ящики. RULES-793.
  * В отчете по изменениям workflow теперь присутствует автор изменений и его комментарий. RULES-809.
  * При отсутствии правил для обработки запрошенной роли, выводим сообщение об ошибке. RULES-807.
  * В отчет по ролям добавлена возможность сортировки по пользователям. RULES-775.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-01 19:31:54

0.18.6
---

  * RULES-799: approvers всегда должны быть указаны в workflow + исправления тестов
  * Создаем тикет в кондукторе, для выкладки пакета в тестинг. RULES-802.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-26 21:56:13

0.18.5
---

  * фикс бага в plugins/generic.get\_roles запросе для больших деревьев ролей

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-26 17:16:46

0.18.4
---

  * RULES-789: добавил в корневые департаменты департамент ассессоров поиска "as"

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-24 16:32:24

0.18.3
---

  * RULES-790: фикс баги в команде проверки данных из Splunk

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-21 18:05:26

0.18.2
---

  * Исправлена 500 ошибка на странице редактирования шаблонов писем. RULES-769.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-19 14:35:28

0.18.1
---

  * RULES-781:  фикс для писем на пустые адреса + тесты

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-18 15:06:17

0.18.0
---

  * Устранена неполадка в работе механизма выбора роли. RULES-759.
  * RULES-776: добавил email gnoma@yandex-team.ru в получатели уведомлений об изменениях workflow
  * RULES-765: добавил роль Разработчика в Общие роли Управлятора
  * Сохранение данных от OEBS целиком в файл. RULES-777.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-17 15:35:51

0.17.71
---

  * Исправлена команда рассылающая логи разработчикам систем. RULES-773.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-07 18:15:25

0.17.70
---

  * Поправден баг в процедуре, забирающей уволенных сотрудников из OEBS. RULES-772.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-07 13:12:35

0.17.69
---

  * Тестовый режим блокировки сотрудников с последующим отзывом доступов через неделю. RULES-712.
  * Обязательные python-пакеты добавлены в зависимости.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-06 12:48:46

0.17.68
---

  * Исправлена конфигурация логгеров, чтобы фиксировать пятисотки. RULES-768.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-06 11:49:12

0.17.67
---

  * Теперь ошибки workflow лучше обрабатываются и даже выводится строка в которой произошла ошибка. RULES-763.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-04 15:03:37

0.17.66
---

  * Убрал nscd из зависимостей, так как он конфликтует с cauth и непонятно для чего нужен.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-03 16:02:26

0.17.65
---

  * Теперь все view, принимающие POST, используют транзакции. RULES-694.
  * Прооптимизирован процесс синхронизации с Center и LDAP. RULES-761.
    Теперь синхронизация должна проходить за 10-20 секунд.


 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-28 13:24:47

0.17.64
---

  * Исправлена ошибка с недозагрузкой частей составной роли при открытии пермалинка. RULES-758.
  * Исправлена ошибка с отсутствием декодирования параметров пермалинка. RULES-757.
  * В девелоперской среде не кэшируем шаблоны.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-25 17:49:23

0.17.63
---

  * Исправлена ошибка из-за которой по пермалинку вибиралась БД OEBS вместо просто OEBS. RULES-755.
  * Улучшен поиск по нескольким словам. RULES-638.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-25 15:25:31

0.17.62
---

  * Исправлена склонялка в продакшене. RULES-754.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-24 15:29:26

0.17.61
---

  * Добавлен коммент к полю no\_email. RULES-752.
  * Исправлено неверное отображение количества запросов, ожидающих подтверждения. Отрефакторены тесты. RULES-750, RULES-753.
  * Добавлено отображение AD-групп на странице с данными роли. RULES-730.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-24 12:55:55

0.17.60
---

  * В отчете по действиям поле действия разделено на составные части. RULES-674.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-19 16:19:05

0.17.59
---

  * Из вызова save() для сохранения даты выдачи роли удален параметр update\_fields. RULES-727.
  * Поправлено исполнение тестов в соответствии с измененными отчетами. RULES-727.
  * Отчеты по ролям используют для сортировки и фильтрации ролей поле granted\_at. RULES-727.
  * Добавлено ограничение на длину генерируемого паспортного логина. RULES-731.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-18 23:30:34

0.17.58
---

  * Снова исправлена ошибка в команде process\_data\_from\_splunk. RULES-749.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-13 15:16:27

0.17.57
---

  * Исправлена ошибка в команде process\_data\_from\_splunk. RULES-749.
  * Сделана нормализация AD групп при сохранении их в базу. RULES-744.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-13 14:55:40

0.17.56
---

  * Исправлен баг, позволяющий удалять информацию о доступах, через API. RULES-742.
  * Поправлена ошибка в обработке флага visibility для невидимых ролей. RULES-716.
  * Сообщения об ошибках, получаемые celery, приводятся к unicode. RULES-732.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-10 18:16:16

0.17.55
---

  * Добавлена management команда для нормализации ссылок на AD группы. RULES-736.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-05 18:53:26

0.17.54
---

  * Пересборка из-за того, что как-то неправильно залился пакет на secdist.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-30 18:12:49

0.17.53
---

  * Небольшой фикс неопределенной переменной. RULES-724.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-30 17:33:45

0.17.52
---

  * Добавлена дополнительная проверка при удалении ролей в команде upravlyator\_deprive\_roles. RULES-724.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-30 16:43:04

0.17.51
---

  * Настройки поправлены таким образом, чтобы Управлятор не пятисотил. RULES-720.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-29 20:14:09

0.17.50
---

  * Поправлен скрипт, обновляющий lego при сборке пакета.
  * Дан доступ пользователю caspermdmuser к API управлятора. RULES-719.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-29 16:05:39

0.17.49
---

  * Исправлен алгоритм работы с данными, поступающими из Splunk. Вновь включены блокировки по этим данным. RULES-713.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-29 15:29:57

0.17.48
---

  * В процесс сборки пакета добавлен профайлер, чтобы отслеживать сколько занимает каждый этап. RULES-710.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-21 21:36:08

0.17.47
---

  * Поправлена проверка клиентских сертификатов в nginx конфиге. В рамках RULES-670.
  * Исправлена работа выбиралки роли. Пришлось перейти с jquery-ui 1.8.11 на 1.10.4. RULES-711.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-21 18:11:51

0.17.46
---

  * Еще раз обновлены зависимости. RULES-703.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-21 16:39:06

0.17.45
---

  * Обновлены зависимости, так что теперь должна быть решена проблема выдачи доступов в сам Управлятор. RULES-703.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-21 12:46:39

0.17.44
---

  * Поправил пути к статике и добавил немного логгинга для профайлинга шаблонов. RULES-697, RULES-709.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-16 19:15:04

0.17.43
---

  * Доработана проверка сертификатов ручек /system/handles/. RULES-704.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-16 12:19:19

0.17.42
---

  * Исправлена опечатка в конфиге nginx, из-за которой Управлятор не принимал свой собственный сертификат. RULES-701.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-13 14:02:41

0.17.41
---

  * Обновлен модуль djblets, чтобы не зависеть от PIL. RULES-699

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-13 13:13:40

0.17.40
---

  * Update.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-13 12:47:13

0.17.39
---

  * Обновлены библиотеки в virtualenv. RULES-699.
  * Исправлен конфиг Nginx, чтобы снова пускало helpdesk. RULES-698.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-13 12:13:19

0.17.38
---

  * Включена валидация серверных сертификатов систем. RULES-692, RULES-670.
  * Исправлена ошибка в subject клиентского сертификата, который может принимать Управлятор. RULES-670

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-10 12:08:33

0.17.37
---

  * Поправлены настройки requests и nginx, чтобы проверять новые сертификаты. RULES-670.
  * Добавлен указатель с каким сертификатом, старым или новым, ходить в ситему. RULES-670.
  * Исправлены ошибки от xscript-proc, связанные с отсутствущим lego:locale. RULES-691.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-27 12:41:17

0.17.36
---

  * Теперь agranat.yandex-team.ru редиректит на idm.yandex-team.ru. RULES-672.
  * Теперь на странице /changelog/ все номера тикетов ведут на соответствующие страницы трекера. RULES-680.
  * Исправлено поведение механизма пересмотра доступов. Теперь в качестве точки отсчета используется отдельное поле granted\_at. RULES-689.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-25 15:44:49

0.17.35
---

  * Поправлены тесты и debian/changelog.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 18:11:39

0.17.34
---

  * Добавлена функция, для проверки работы splunk. RULES-685.
  * Исправлена работае debugtoolbar. RULES-690.
  * Встроена защита от большого числа неактивных пользователей, получаемых из SPLUNK. RULES-685.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 17:55:00

0.17.33
---

  * Временно отключена блокировка по данным спланка. RULES-688.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-20 18:03:52

0.17.32
---

  * GenericPlugin пробрасывают исключение при получении пустого ответа от системы. RULES-678.
  * Убран лишний отладочный принт.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-16 11:11:57

0.17.31
---

  * Еще одна правка теста для RULES-677.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-11 18:29:47

0.17.30
---

  * Поправлен тест, проверяющий RULES-677.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-11 18:18:00

0.17.29
---

  * Теперь при синхронизации не учитываются отозванные доступы. RULES-677.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-11 18:07:23

0.17.28
---

  * Исправлена остановка механизма регулярного пересмотра при первой же ошибке. RULES-663.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-11 09:29:29

0.17.27
---

  * Добавлено отображение текущего статуса редактируемого workflow и оповещение автора о принятии его правок. RULES-561.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-05 14:49:57

0.17.26
---

  * Исправлена ошибка при формировании CSV отчетов. RULES-668.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-05 01:16:16

0.17.25
---

  * Поправлено автоматическое обновление дерева ролей целиком. RULES-661.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-26 17:46:24

0.17.24
---

  * Исправлена ошибка в процессинге данных от ОЕБС. RULES-655.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-25 16:33:22

0.17.23
---

  * Поправлен шаблон письма о блокировках по данным ОЕБС, чтобы логины были о одному на строчку. RULES-655.
  * block users only if their number is not deviate from the middle. RULES-655.
  * Исправлена ошибка, связанная с логгером в команде drop\_virtual\_machines. RULES-658.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-25 14:27:57

0.17.22
---

  * OU=TechUsers,DC=ld,DC=yandex,DC=ru добавлен в список DN, где следует искать активных пользователей. RULES-656.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-18 21:34:02

0.17.21
---

  * Обновлена команда взаимодействия с OEBS. RULES-643. RULES-655.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-18 21:03:53

0.17.20
---

  * Исправлена ошибка при попытке отзыва доступа в системе, которая более не подключена к Управлятору. RULES-647.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-15 21:34:05

0.17.19
---

  * В уведомления о блокировке из-за долгой неактивности в сети, добавлено примечание о том, что для разблокировки нужно писать на help@. RULES-653.
  * Из крона удалена команда, блокирующая сотрудников по данным от 1c. RULES-654.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-14 17:48:36

0.17.18
---

  * В письме о действиях по данным OEBS, говорим что ничего не было, если никаких действий не было произведено. RULES-652.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-13 20:29:36

0.17.17
---

  * Ссылки в письмах исправлены с agranat.yandex-team.ru на idm.yandex-team.ru. RULES-651.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-13 19:15:57

0.17.16
---

  * Временно отключена часть теста, так как интеграция с OEBS будет работать до 22 в тестовом режиме.
  * В список получателей данных о взаимодействии с OEBS включена Лида Свистельник.
  * Прикручиваем OEBS в качестве источника данных о сотрудниках с истекшим NDA. RULES-643.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-13 18:51:21

0.17.15
---

  * Исправлено обновление даты найма сотрудника при синхронизации со стаффом. RULES-650.
  * Исправлена ошибка при длинной цепочке заместителей в workflow. RULES-649.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-12 21:12:31

0.17.14
---

  * Исправлена работа на хосте api.idm.yandex-team.ru
  * В репозиторий добавлены скрипты, которые я использовал для апгрейда базы в продакшене.
  * Исправлена работа админки.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 14:56:41

0.17.13
---

  * Еще раз исправлена сборка virtualenv. На этот раз явно указано, что надо использовать /usr/bin/python.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-07 16:06:05

0.17.12
---

  * Исправлена работа на домене agranat.yandex-team.ru

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-07 14:51:37

0.17.11
---

  * Исправлены инкрементальные синхронизации с Центром.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-07 12:02:56

0.17.10
---

  * Исправлена настройка ALLOWED\_HOSTS.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-07 01:39:37

0.17.9
---

  * Поправлены скрипты, создающие виртуальное окружение, чтобы уж наверняка устанавливать все нужные пакеты в virtualenv.
  * django-yauth убран из списка зависимостей.
  * В файле настроек урлы для доступа к Center перемещены ближе к концу файла.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-07 01:02:54

0.17.8
---

  * Снова исправлен импорт настроек intranet\_auth, ибо иначе ломаются тесты.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-06 21:11:42

0.17.7
---

  * Поправлен импорт настроек django\_intranet\_auth для перехода на новую модель User.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-06 21:09:11

0.17.6
---

  * DJANGO\_INTRANET\_USER\_MODEL = "upravlyator.User"

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-06 20:53:36

0.17.5
---

  * В проект добавлены миграции django\_intranet\_auth.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-06 16:30:02

0.17.4
---

  * Испарвлены тесты, выполнение которых зависело от таймзоны и ломалось после полуночи.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-06 00:47:31

0.17.3
---

  * Добавлен скрипт, исправляющий сборку virtualenv для продакшена.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-06 00:26:39

0.17.2
---

  * Поправлен debian/rules скрипт, в надежде, что virtualenv будет собираться правильно.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-01 21:04:28

0.17.1
---

  * Поправлен manage.py скрипт, который не запускался из за отсутствующего импорта модуля os.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-01 20:36:46

0.17.0
---

  * Большой рефакторинг с обновлением Django до 1.5, переходом на пользовательскую модель User и переходом на более новые версии остальных библиотек. RULES-642.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-01 16:39:38

0.16.83
---

  * Позволяем использовать в workflow в качестве подтверждающих не только объекты типа Approver, но и объекты типа User, UserWrapper и даже обычные строки. RULES-640.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-17 17:09:40

0.16.82
---

  * fix report generation.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-09 18:23:29

0.16.81
---

  * Добавлен упущенный импорт в команде process\_hovering\_roles.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-26 14:43:39

0.16.80
---

  * Исправлен тест.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-25 19:14:41

0.16.79
---

  * В вывод API ручки отдающей доступы сотрудника добавлен slug системы.
  * Теперь дергаем ручку паспорта admsubscribe на хосту passport-internal.yandex.ru. RULES-637.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-25 19:04:10

0.16.78
---

  * Исправлены тесты.
  * Команда deprive\_hovering переименована в process\_hovering и теперь она обрабатывает так же роли, зависшие в состоянии approved. DOSTUP-29418.
  * Пускаем руководителя сотрудника на страницу /user/<login>/expire/. RULES-601.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-23 22:03:14

0.16.77
---

  * Исправлен resource\_uri.
  * Исправлена фильтрация API ручки, выдающей роли пользователя.
  * Девелоперский Nginx теперь будет валидировать нормальные пользовательские сертификаты, выданные через YandexExternalCA.
  * Явно задана глубина проверки цепочки сертификатов в nginx.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-23 17:57:46

0.16.76
---

  * Исправлен production конфиг nginx.
  * Опциональный флаг no\_email в workflow, если не надо отправлять уведомления. RULES-633.
  * Поправлено отображение неконсистентностей. RULES-636.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-18 17:56:12

0.16.75
---

  * Добавлена ручка API для отзыва доступов. RULES-632.
  * Добавлена возможность помечать роли как невидимые в интерфейсе. RULES-628.
  * Добавлена ручка для получения ролей пользователя. RULES-631.
  * доступы в различных таблицах снова кликабельны. RULES-621.
  * Добавлен крон для просчета резкого увеличения аппрувов в системе. Из теста удалено хождение на staff.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-13 14:15:52

0.16.74
---

  * Исправлена ветка для сборки пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-09 20:52:54

0.16.73
---

  * Временно отключен один из тестов.
  * Добавлены методы get\_head\_of и get\_head\_of\_or\_zam. RULES-627.
  * Добавлен метод пользователя для определения неотсутствующих руководителей. RULES-626.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-09 20:45:42

0.16.72
---

  * Поправлен fabfile, чтобы ставить пакетики из secdist.
  * Поправлены имена хостов в девелоперском nginx конфиге.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-03 16:34:00

0.16.71
---

  * Еще одна пересборка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-03 15:23:24

0.16.70
---

  * Пересборка пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-02 22:16:57

0.16.69
---

  * Исправлена опечатка в номере версии six.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-02 20:20:57

0.16.68
---

  * Поправлены данные одного теста.
  * В зависимости добавлен six.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-02 20:11:47

0.16.67
---

  * Синхронизируемся со стафом чаще, раз в пять минут. RULES-622.
  * Password for mysql was removed.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-02 17:37:33

0.16.66
---

  * Теперь доступы будут отзываться не только раз в час, но и по выходным.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-17 12:52:35

0.16.65
---

  * Не запускаем тесты в fabfile, так как они и так стартуют из debian/release.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-17 11:44:23

0.16.64
---

  * Небольшое исправление одного теста.
  * Изменил на отзыв ролей у уволенных раз в час, пока не разберемся с тем, как оно должно быть правильно.
  * Дошикшены последние тесты, которые не было видно из-за склонятора. RULES-615.
  * В уведомления об ошибке при выдаче доступа добавлен паспортный логин и пароль. RULES-595.
  * Заменяем подчеркивания дефисами в паспортных логинах и приводим их к нижнему регистру. RULES-620.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-17 08:36:32

0.16.63
---

  * Архитектура изменена с all на amd64.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-12 21:27:52

0.16.62
---

  * Теперь загружаем пакетик в secdist.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-12 21:13:34

0.16.61
---

  * Еще раз поправлены пути к медиафайлам.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-12 20:51:11

0.16.60
---

  * Еще чуть чуть исправлен конфиг nginx.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-12 20:35:31

0.16.59
---

  * Добавлен кэш для dev\_version.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-12 15:48:35

0.16.58
---

  * Поправлены названия хостов в девелоперском nginx конфиге.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-12 15:10:03

0.16.57
---

  * Исправлен запуск тестов при debuild.
  * Исправлен двойной запуск тестов при fab do\_release.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-09 22:40:06

0.16.56
---

  * Исправлен баг, из-за которого в получался relocatable virtualenv с неработающим djblets.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-09 22:15:58

0.16.55
---

  * Игнорируем файл состояния tdaemon.
  * Собираем только из ветки precise.
  * Исправлен кусок мерджа.
  * Дошикшены последние тесты, которые не было видно из-за склонятора. RULES-615.
  * В уведомления об ошибке при выдаче доступа добавлен паспортный логин и пароль. RULES-595.
  * Перевод сборки пакета и разработческой среды на precise. RULES-615.
      * Обновлены версии пакетов.
      * Проставлены корректные настройки для новых пакетов.
      * AnyApprover переведен на list.

  * Подключаем приложения для работы djblets. RULES-615.
  * Корректная версия djblets. RULES-615.
  * Новый механизм склонения по падежам. RULES-619.
  * Заменяем подчеркивания дефисами в паспортных логинах и приводим их к нижнему регистру. RULES-620.
  * Перевод сборки пакета и разработческой среды на precise. RULES-615.
  * Убрал из зависимостей importlib.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-09 20:29:42

0.16.54
---

  * Показываем даты принятия в штат и увольнения, без времени.
  * Запускаем некоторые кроны только на продакшене. RULES-526.
  * Выводим название отдела в карточке сотрудника. RULES-611.
  * Добавлена кроновая задача для обновления списка паспортных логинов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-29 22:04:59

0.16.53
---

  * Запрет отправки формы запроса доступа при недоступном паспортном логине. RULES-605.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-09 17:31:00

0.16.52
---

  * Исправлен скрипт run-celery.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-09 16:37:33

0.16.51
---

  * Переименован css класс для списка систем. RULES-612.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-02 17:39:57

0.16.50
---

  * Большинство ежечасных кроновых задач теперь будут запускаться с 8 до 20, чтобы не пересекаться с ночными задачами.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-27 18:36:26

0.16.49
---

  * Исправлена небольшая ошибка, допущенная во время предыдущего фикса.
  * Больше Урпавлятор не будет блокировать сотрудников Денег, на основании 1С и Splunk. RULES-609.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-26 15:38:56

0.16.48
---

  * Обновлен список хостов LDAP серверов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-25 19:03:13

0.16.47
---

  * Переменные fields\_data и system\_specific добавлены в код тестирования workflow.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-25 17:49:22

0.16.46
---

  * Исправлена форма тестирования workflow.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-21 15:32:39

0.16.45
---

  * Добавлена команда, удаляющая people виртуалки уволенных сотрудников. RULES-527.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-17 16:47:03

0.16.44
---

  * Убираем SECRET\_KEY из settings.
  * Избавляемся от try\_files в конфигах nginx.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-13 18:37:00

0.16.43
---

  * Теперь записи RevokeControl будут удаляться при блокировки пользователя вследствии его увольнения. Благодаря этому, Управлятор перестанет доставать руководителей уволенных сотрудников, уведомлениями о том, что скоро их сотрудник будет заблокирован в домене. RULES-599.
  * Конфиг Nginx поправлен, чтобы работать и на алиасах. RULES-602.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-05 20:08:23

0.16.42
---

  * Добавлен случайно удаленный файл tasks.py.
  * Исправлена ошибка в client-api, связанная с кривой версией django-api. RULES-60.
  * Теперь роль, добавленная у Управлятор в результате неконсистентности, должна быть подтверждена в течении 7 дней. Если этого не сделать, она будет отозвана.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-24 17:55:40

0.16.41
---

  * Теперь Управлятор передает правильный User-Agent, содержащий Upravlyator/номер-версии. RULES-432.
  * Используем upravlyator-django-api==0.16.39.
  * Перевод комментариев на странице очереди запросов. RULES-596.
  * Добавлена возможность комментировать отказ и аппрув выдачи доступа, отображение комментариев в actions. RULES-459.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-21 16:00:25

0.16.40
---

  * Исправлена сигнатура функции update\_model.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-21 11:29:38

0.16.39
---

  * Убран запуск createinitialrevisions в postinst, так как он очень долго отрабатывает для всех профилей.
  * Убрано старое удаление кронов из posinst.
  * Снова запускаем тесты при сборке пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-20 23:57:43

0.16.38
---

  * Добавлено поле updated в Profile, проверяем изменения профиля перед сохранением. RULES-592.
  * Сохраняем в профиль пользователя первый из отданных центром телефонов. RULES-593.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-20 23:41:22

0.16.37
---

  * Исправлено неправильное использование datetime.strptime(). RULES-fix.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-17 19:55:04

0.16.36
---

  * Фикс обновления профилей пользователей. RULES-fix.
  * В конфиг Nginx добавлен Strict-Transport-Security заголовок.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-17 13:08:32

0.16.35
---

  * Добавлено правило, чтобы Nginx раздавал правила файрвола.
  * Теперь правила файрвола будут содержать и те системы, которые is\_broken.
  * Окончательно выпилен django-api.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-16 19:40:30

0.16.34
---

  * Выпилил django api в отдельный проект.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-16 13:32:59

0.16.33
---

  * Гриф "Конфиденциально". RULES-584.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-26 17:17:44

0.16.32
---

  * Не отображаем закрытые неконсистентности на их странице. RULES-582.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-17 20:08:27

0.16.31
---

  * Закомментирован тест nose.
  * Правильное форматирование причины действий в AD. RULES-581.
  * Страница блокировок подчиненных сотрудников и рассылка уведомлений о скорой блокировке таковых. RULES-528.
  * Добавлен тест вывода русского текста плагином noseprogressive.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-17 18:47:35

0.16.30
---

  * На главных страницах суперюзера и аудитора добавлены ссылки на страницу неконсистентностей. RULES-576.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-10 20:47:06

0.16.29
---

  * Мониторинг появления выданных доступов с неотработанными запросами. RULES-542.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-10 18:56:19

0.16.28
---

  * Нотификация о текущих подтверждениях переведена на обобщенные запросы доступа. RULES-580.
  * В письмо об отзыве доступа добавлена ссылка для его повторного запроса. RULES-570.
  * Отображение списка автокомплита по клику на поле. RULES-461.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-10 17:21:05

0.16.27
---

  * Поправлен баг с неправильным запросом доступа для другого сотрудника. RULES-562.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-04 19:54:55

0.16.26
---

  * Добавлен параметр fired=1 в запрос удаления доступа, если пользователь уволен. RULES-524.
  * Изменен дизайн формы запроса доступа - теперь роль раскрывается сверху вниз. RULES-563.
  * Отображение данных о аппруверах на этапе выбора роли. RULES-562.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-04 17:21:13

0.16.25
---

  * Восстанавливаем удаленные департаменты во время синхронизации с центром. RULES-579.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-02 20:06:07

0.16.24
---

  * Метод run\_workflow отрефакторен, чтобы принимать только роль и реквестера. RULES-574.
    Кроме того, теперь он передает в workflow fields\_data и system\_specific.


 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-22 17:24:44

0.16.23
---

  * Добавлена возможность передать dynamic значение для дополнительных полей. Добавлена ручка GET /fields-info/ в django\_api. RULES-568.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-21 17:59:50

0.16.22
---

  * Добавлен прототип команды для вычистки истории изменения дерева ролей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-20 18:53:20

0.16.21
---

  * Добавлена страница суперпользователя для обращения по системным ручкам /info/ и /get-all-roles/. RULES-539.
  * Добавлена возможность осуществления http-запросов из workflow. RULES-569.
  * Добавлен выбор веток для сравнения в дереве ролей. RULES-555.
  * При заведении неконсистентности об отсутствующем доступе в управляторе отправляем уведомление пользователю о необходимости аппрувов. RULES-567.
  * Страница для дергания системных ручек /get-all-roles/ и /info/. RULES-539.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-18 17:06:31

0.16.20
---

  * Добавлен выбор веток для сравнения в дереве ролей. RULES-555.
  * При заведении неконсистентности об отсутствующем доступе в управляторе отправляем уведомление пользователю о необходимости аппрувов. RULES-567.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-13 17:49:41

0.16.19
---

  * Удаление доступа проверяет его состояние и не переводит в недопустимое. RULES-547.
  * Поправлено форматирование в debian/changelog.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-04 14:47:49

0.16.18
---

  * Обновляем debian changelog только если изменения действительно были.
  * Добавлена обработка наложенных аппрувов или отзывов доступов аппруверами. RULES-547.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-01 15:44:06

0.16.17
---

  * Улучшено форматирование кода в команде upravlyator\_review\_roles.
  * Команда для рассылки оповещений о потенциальных угрозах, определенных по увеличению количества потенциальных подтверждений. RULES-559.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-28 19:37:05

0.16.16
---

  * Базовый класс менеджмент команд, принудительно устанавливающий ru-локаль. RULES-537.
  * Добавлена кнопка восстановления системы, доступная только суперюзеру. RULES-541.
  * Добавлена возможность переводить систему в состояние поломки из админки. RULES-543.
  * Отчеты по выходам из строя и восстановлениям систем. RULES-549.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-13 12:58:06

0.16.15
---

  * Теперь команда generate\_firewall\_rules возвращает 1 при любой ошибке.
  * При изменении системы, если не было изменено workflow, не создается Action. RULES-540.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-12 17:43:18

0.16.14
---

  * Исправлена опечатка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-07 20:11:27

0.16.13
---

  * Добавлена возможность указания в дереве ролей наименований правил firewall. Выгрузка макросов для firewall с учетом указанных в дереве ролей правил. RULES-524.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-07 19:51:46

0.16.12
---

  * Исправлена ошибка из-за которой на главной странице всегда показывалась плашка '39 запросов'. RULES-556.
  * Не включаем в debian/changelog записи git о мерджах.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-07 17:15:51

0.16.11
---



 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-05 14:30:07

0.16.10
---

  * Merge branch 'master' of github.yandex-team.ru:art/yandex-upravlyator
  * Тепреь команда do\_release выводит номер собранной и выкаченной версии.
  * Merge pull request #105 from fantom/hotfix/report\_553
  * Добавлено поле system\_specific в отчеты по ролям. RULES-553. Поправлен баг с 500 ошибкой при попытке сортировать записи в отчете по ролям. RULES-548.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-05 13:24:13

0.16.9
---

  * Исправлена опечатка в fabfile.py.
  * Merge branch 'master' of github.yandex-team.ru:art/yandex-upravlyator
  * Таймаут для Splunk увеличен до 5 минут. RULES-551.
  * Исправлена команда, формирующая debian/changelog.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-01 16:02:09

0.16.8
---

  * Добавлена команда для git pull.
  * Исправлено имя пользователя в уведомлении о добавленном Splunk исключении. RULES-546.
  * Увеличен defaulttimeout при работе со Splunk. RULES-550.
  * Поправлена команда для деплоя.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-31 16:32:57

0.16.7
---

  * Исправлены переводы со множеством форм. Фиксит RULES-533.
    Как оказалось, там где используются ungettext,
    надо указывать одинаковые строки и для единственного,
    и для множественного числа. Иначе, gettext при мердже
    переводов с танкера и из python файлов, создает fuzzy
    переводы, которые не компилируются в *.mo.


 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-22 13:24:38

0.16.6
---

  * Фикс в fabfile.py

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-21 15:00:13

0.16.5
---

  * Еще один фикс в миграции.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-18 22:34:46

0.16.4
---

  * Исправлена 90 миграция, которая дропает таблицу и фейлится на продакшене.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-18 22:21:14

0.16.3
---

  * Исправлен учет неконсистентностей логинов, которые уже есть в нашей базе. RULES-545.
  * Закрываем неконсистентности логина, если система перестала отдавать эти неправильные логины. RULES-544.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-18 18:12:24

0.16.2
---

  * Исправлена ошибка, возникшая из за удаления поля systems.
  * Исправлен стиль плашки, предупреждающей о сломанных системах.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-18 15:55:12

0.16.1
---

  * Удалено поле admins модели System, так как оно давно не используется.
  * В письмо о поломке системы добавлена информация о неконсистентностях. RULES-538.
  * Добавлен \_\_repr\_\_ для RoleRequest. RULES-536.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-17 19:25:35

0.16.0
---

  * Читаемый цвет для rerequested доступов. RULES-460.
  * Добавлен фильтр по типу action. RULES-500.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-16 13:17:40

0.15.71
---

  * Встроена защита от большого количества неконсистентностей.
    Теперь система может быть переведена в состояние "поломана" и никакие
    изменения ролей к ней не будут применяться. RULES-505.
  * Поправлен автокомплит редактора workflow. RULES-513.
  * При заведении доступов вследствие разрешения неконсистентности добавляются AD-группы . RULES-522.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-15 15:57:27

0.15.70
---

  * Исправлен подсчет количества запросов на доступ. Теперь он учитывает
    назакрытые RoleRequest.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-15 15:49:34

0.15.69
---

  * Некоторые кроны теперь будут запускаться только на продакшене.
  * Раскоменнтированы кроны, отключенные на новогодние праздники.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-10 17:34:37

0.15.68
---

  * Некоторые кроны отключены до конца новогодних праздников.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-28 18:37:20

0.15.67
---

  * Исправлен ошибочный перевод доступа из состояния rerequested в approved. RULES-523.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-24 18:17:23

0.15.66
---

  * Добавлена миграция для поля department\_from.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-17 12:47:16

0.15.65
---

  * Теперь Управлятор регистрирует факт первоначального присвоения отдела
    пользователю. RULES-521.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-14 17:30:28

0.15.64
---

  * Сборка с новыми переводами.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-14 15:45:15

0.15.63
---

  * Поправлена обработка ошибки при preview воркфлоу.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-14 14:57:49

0.15.62
---

  * Возможность передавать в is\_head\_of и works\_in\_dep нескольких департаментов. RULES-512.
  * Привязка запросов роли к соответствующим action при создании. RULES-507.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-13 18:59:47

0.15.61
---

  * Исправлена ошибка AttributeError при отправке письма из management команды
    check\_roles. RULES-518.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-13 18:24:19

0.15.60
---

  * Исправлены тесты.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-12 17:58:52

0.15.59
---

  * Исправлены шаблоны писем, так что теперь мобильные пароли будут снова
    доступны.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-07 17:58:09

0.15.58
---

  * Поправлен путь для запуска celeryd.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-07 15:53:09

0.15.57
---

  * Переход на virtualenv.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-07 11:32:32

0.15.56
---

  * Шаблоны писем приведины к единообразному виду и в них улучшенна поддержка
    переводов. RULES-517.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-06 20:05:36

0.15.55
---

  * Отрефакторены view для управления исключениями.
  * Добавлено пояснение к письму о блокировке по спланку.
  * Добавлен INNODB engine для базы, подключаемый по умолчанию.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-04 13:11:35

0.15.54
---

  * Реализован механизм исключений из блокировок по данным Splunk. RULES-506.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-03 17:46:54

0.15.53
---

  * Более верная обработка запросов роли в случае совпадения запрашивающего и
    подтверждающего. RULES-507.
  * Для ускорения обработки дерева ролей на странице управления ролями
    разделяем её на полную и легкую версии.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-26 19:43:47

0.15.52
---

  * Теперь все запросы на доступ имеют один корневой объект, к которому уже
    привязываются отдельные запросы к конкретным подтверждающим. RULES-507.
  * Ошибка 'inactive external user' при обработке данных от спланка, превращена в warning.
  * Удален лишний логгинг из send\_log\_digest.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-23 17:05:24

0.15.51
---

  * Не логируем попусту, чтобы не приходило письмо с ложными ошибками.
    RULES-504.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-16 17:46:14

0.15.50
---

  * При аудите приводим регистр полученных логинов к lowercase. RULES-503.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-16 17:30:00

0.15.49
---

  * Исправлена логика протухания кэша дерева ролей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-15 20:56:12

0.15.48
---

  * Большое дерево ролей помещаем в память, а не в memcached.
    Это нужно для того, чтобы команда обновления дерева ролей работала быстро,
    а не по 40 минут. RULES-492.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-15 19:50:12

0.15.47
---

  * Ссылка на страницу с отчетами, добавлена на главную страницу
    суперпользователя. RULES-501.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-14 19:53:05

0.15.46
---

  * Исправлен алгоритм блокировки сотрудников по данным от 1С. RULES-498.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-13 20:29:39

0.15.45
---

  * Блокировка в домене по данным из Splunk включена в боевом режиме. RULES-490.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-13 19:11:18

0.15.44
---

  * Теперь начальник может не только видеть, но и отзывать доступы своих
    подчиненных. ANGDVA-8866.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-13 16:10:15

0.15.43
---

  * Добавлена проверка даты выхода сотрудника на работу при обработке данных от
    спланка. RULES-490.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-13 12:41:51

0.15.42
---

  * Убран лишний set\_trace из команды, достающей данные из splunk.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-09 19:56:57

0.15.41
---

  * Исправлена команда, выбирающая из Спланка неактивных сотрудников.
    RULES-490.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-09 17:40:20

0.15.40
---

  * Добавлена интеграция со спланком, пока в тестовом режиме. RULES-490.
  * Переименована команда контроля неактивных внешних подрядчиков. RULES-456.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-09 15:57:29

0.15.39
---

  * Исправлен текст письма про взаимодействие с 1С. RULES-497.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-09 14:48:47

0.15.38
---

  * Напоминалка о ролях, нуждающихся в перезапросе. RULES-494.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-07 18:34:22

0.15.37
---

  * Добавлено логирование отправки и результата отправки СМС. RULES-SMS.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-07 18:19:01

0.15.36
---

  * Дополнительное логирование в команде автоматического обновления дерева
    ролей. RULES-492.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-01 18:08:15

0.15.35
---

  * Улучшение логирования и обработки ошибок от паспорта, в процессе
    простановки sid=67. RULES-486.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-01 16:31:19

0.15.34
---

  * Проставляем sid=67 всем паспортным логинам, используемым в админках. RULES-486.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-31 14:31:17

0.15.33
---

  * Исправлена ошибка при обновлении динамических переводов. RULES-488.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-31 14:31:17

0.15.32
---

  * Включен боевой режим интеграции с 1С.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-26 18:08:10

0.15.31
---

  * Теперь отчет об интеграции с 1С отсылается каждый раз, независимо от
    данных. Так же, в него включены данные о пользователях, не найденных в
    Управляторе.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-25 17:14:49

0.15.30
---

  * Крон поправилен, чтобы делать несколько попыток хождения в 1С.
  * Исправлена обработка исключения в команде, обрабатывающей данные от 1С.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-25 16:03:46

0.15.29
---

  * Добавлен контекстный менеджер catch\_templates полезный для тестов.
  * Проверяем поле phones на не None. RULES-487.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-25 13:04:23

0.15.28
---

  * Обновлены переводы.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-25 11:45:23

0.15.27
---

  * Исправлен URL ручки sendsms.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-24 20:41:15

0.15.26
---

  * Поправлены уведомления о принятии доступа на рассмотрение при наличии или
    отсутствии подтверждающих. RULES-485.
  * Добавлена возможность отправки СМС после выдачи роли. Для этого требуется
    в воркфлоу установить параметр send\_sms=True. RULES-484.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-24 19:07:03

0.15.25
---

  * Проверяем синтаксис workflow и сообщаем пользователю о синтаксических
    ошибках. RULES-483.
  * Подчищаем доступы, запрошенные уволенными сотрудниками, но так и не
    подтвержденные. RULES-482.
  * Автоматически подтверждаем доступ, если подтверждать должен тот, кто
    запросил. RULES-410.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-22 13:07:49

0.15.24
---

  * Исправлены кракозябры в предупреждениях пользователя, возникающих в результате использования AccessDenied в workflow. RULES-477.
  * Исправлена обработка AccessDenied в команде check\_ttl\_days. RULES-480.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-11 12:38:22

0.15.23
---

  * Дополнительная информация о данных из 1С.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-10 20:30:26

0.15.22
---

  * Исправлен текст действия по удалению сотрудника из AD группы. RULES-475.
  * Интеграция с 1С переведена в тестовый режим, когда аккаунты не блокируются
    и сотрудники не удаляются из AD групп, а только приходят письма о том,
    какие действия должны быть совершены. RULES-479.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-09 20:21:54

0.15.21
---

  * Теперь, если workflow устанавливает атрибут ttl\_days, то выданный доступ будет
    ограничен по времени и отзовется через указанное количество дней. RULES-474.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-08 16:54:40

0.15.20
---

  * Храним логи бэкенда за 90 дней, а не за 7, как было ранее.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-05 15:56:59

0.15.19
---

  * Исправлен тест upravlyator\_control\_dismissed, в management командах всегда
    используется английский перевод.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-05 15:36:26

0.15.18
---

  * Поправлена возможноть листать страницы отчетов. RULES-475.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-05 13:36:21

0.15.17
---

  * Исправлена и ускорена обработка переводов. RULES-458.
  * Исправлена пятисотка на странице /reports/ad\_actions. RULES.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-03 18:27:52

0.15.16
---

  * Исправлена опечатка в кронтабе.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-03 14:59:56

0.15.15
---

  * Вновь включен аудит для AWAPS.
  * Комментарий в функции \_create\_approve\_requests теперь необязателен. RULES-475.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-02 16:48:50

0.15.14
---

  * Отрываем доступы у уволенных не раз в час, в раз в сутки, в 6:30 утра.
    PAYTASK-270.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-01 17:34:31

0.15.13
---

  * Логирование в базу фактов изменения аккаунта сотрудника в АД, а так же,
    генерация отчетов по этим данным. RULES-475.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-10-01 16:00:48

0.15.12
---

  * Исправлена ошибка из за которой не отзывался доступ у тех, у кого в
    ldap\_active None.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-28 16:37:48

0.15.11
---

  * Появился удобный редактор кода воркфлоу, позволяющий нормально писать код
    прямо в браузере. RULES-449.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-27 18:27:18

0.15.10
---

  * Исправлено логирование ошибок доступа к AD.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-27 18:27:16

0.15.9
---

  * Исправлена установка опций для LDAP.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-24 16:47:13

0.15.8
---

  * Все процедуры для доступа к LDAP перенесены в один класс.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-24 16:18:01

0.15.7
---

  * Теперь при переводе сотрудника из отдела в отдел, Управлятор запоминает
    это и показывает эту информацию вместе с запросом о пересмотре доступа. RULES-465.
  * Возможность для админа задавать в урле /login-as/логин-сотрудника/ под кем залогиниться.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-20 16:38:26

0.15.6
---

  * Переходим на passport-internal в местах, где обращаемся к админским ручкам. RULES-381.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-20 15:27:23

0.15.5
---

  * Меняем проверку неактивности аккаунта чтобы не подключаться к LDAP на
    каждый чих. RULES-456.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-12 20:27:49

0.15.4
---

  * Зависимость от python-suds>=0.4.1svn710-yandex3.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-12 18:43:57

0.15.3
---

  * Больше не читаем конфиг adpass.py.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-12 18:07:52

0.15.2
---

  * Правильный URL для 1C в продакшене и чтение секурных настроек из secure\_settings.py.
  * Добавляем отметку импорта списков неактивных и снова активных пользователей из 1С. RULES-456.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-12 17:48:21

0.15.1
---

  * Добавлено новое is\_homeworker в профиле сотрудника. RULES-467.
  * Включена обратно нотивикация о запросах в связи с пересмотрами и неконсистентностями. RULES-466.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-11 20:36:34

0.15.0
---

  * Блокировка учетных записей в AD на основе списков, выгруженных из 1С. RULES-456.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-06 15:24:53

0.14.41
---

  * Включаем для doctest внутри workflow опцию ELLIPSIS.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-05 17:34:10

0.14.40
---

  * Поправлена обработка AccessDenied при проверке doctest тестов в workflow.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-05 16:54:18

0.14.39
---

  * И еще один фикс угловой скобки на странице /queue/. RULES-463.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-04 15:13:10

0.14.38
---

  * Сделаны ссылки на систему и сотрудника, со страницы неконсистентности. RULES-433.
  * Удалена лишняя угловая скобка, и названия элементов роли теперь начинаются с большой буквы. RULES-436.


 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-04 14:50:21

0.14.37
---

  * Добавлено отображение system\_specific на странице /queue/. RULES-463.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-09-04 13:46:49

0.14.36
---

  * Исправлено отображение ChangeLog. RULES-462.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-31 09:48:11

0.14.35
---

  * Теперь в workflow можно указать email\_cc, строку или список.
    В результате, уведомление о выдаче доступа будет отправлено
    не только на емейл тому, кто его получил, но и указанным лицам.
    RULES-452.
  * Также, отныне, в workflow можно кидать исключение AccessDenied,
    уведомляя сотрудника о том, что у он не имеет права даже просить
    такую роль. RULES-451.
  * Кроме этого, реализовано асинхронное формирование CSV отчетов
    с уведомлением на почту. RULES-413.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-30 20:36:10

0.14.34
---

  * Появился новый корневой департамент virtual.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-22 18:02:50

0.14.33
---

  * Добавлена опция для танкера TANKER\_KEY\_NOT\_LANGUAGE = True.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-17 16:51:19

0.14.32
---

  * Пробуем добавить третью форму перевода.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-17 15:57:14

0.14.31
---

  * Правильный комментарий к перезапросам в связи с регулярным пересмотром, на странице /queue/.
  * Поправлен перевод предупреждения о количестве оставшихся дней, на странице /queue/.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-17 15:33:34

0.14.30
---

  * Автоматический перенос новых сертификатов из /tmp/agranat-certs в /etc/yandex/upravlyator/certs.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-13 11:01:31

0.14.29
---

  * Удаляем старый крон от yandex-firewall-admin. RULES-446.
  * Исправлен XSS в djblets.datagrid. RULES-455.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-09 19:26:04

0.14.28
---

  * Переносим сертификаты в /etc/yandex/upravlyator.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-09 17:13:57

0.14.27
---

  * Переключились на новый клиентский сертификат.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-09 16:54:53

0.14.26
---

  * Исправлена ошибка, возникающая при сбросе описания ролей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-09 16:01:28

0.14.25
---

  * Исправлена верстка страницы /queue/ для Internet Explorer. RULES-428.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-09 14:33:07

0.14.24
---

  * Исправлена ошибка, в случае если help к роли — пустая строка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-09 14:12:25

0.14.23
---

  * Исправлен баг, когда Управлятор не находит роль для deprive при разрешении неконсистентности. RULES-426.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-08 13:29:02

0.14.22
---

  * Более наглядная страница последних запросов доступов. RULES-442.
  * Удаляем старые описания ролей при обновлении дерева ролей. RULES-453.
  * Поправлен комментарий для роли, которую необходимо перезапросить при смене отдела. RULES-425.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-08 09:38:27

0.14.21
---

  * Добавлена страница /blocks/ на которой будем собирать разные визуальные элементы.
  * Добавили страницу последних запросов ролей системы, например /system/balance/latest-requests/. RULES-442.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-07 16:37:42

0.14.20
---

  * Исправлен переход из rerequested переходим в granted. RULES-450.
  * Каждые 10 минут добавляем или удаляем сотрудников в/из AD группы, если это требуется по workflow.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-08-07 15:32:36

0.14.19
---

  * Исправлено поведение Django API - при удалении неизвестной роли всегда возвращается OK. RULES-443.
  * Исправлена выдача /get-all-roles/ самого Управлятора. RULES-444.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-31 18:14:04

0.14.18
---

  * Исправлена ошибка обработки ошибок в upravlyator\_review\_approvers.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-30 19:17:50

0.14.17
---

  * Добавлен трейс в обработчик ошибок upravlyator\_review\_approvers.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-30 19:02:14

0.14.16
---

  * Попытка исправить UnicodeDecodeError в upravlyator\_review\_approvers.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-30 18:47:46

0.14.15
---

  * Исправлена команда upravlyator\_review\_approvers.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-30 18:32:32

0.14.14
---

  * Добавлена команда upravlyator\_review\_approvers которая по умолчанию,
    перезапускает workflow для всех ролей, которые еще не подтверждены,
    если с момента запроса изменялось workflow системы.

    Кроме того, у её есть опции --force и --system чтобы можно было
    избирательно запустить этот процесс для отдельной системы. RULES-439.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-30 17:03:21

0.14.13
---

  * Добавлена вспомогательная функция restore\_role. RULES-445.
  * Закомментирована сверка ролей для AWAPS. RULES-445.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-30 15:51:58

0.14.12
---

  * Еще одна поправка для /queue/. RULES-441.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-27 18:28:01

0.14.11
---

  * Для ролей, создаваемых в результате неконсистентности, проставляем expire в 3 месяца. RULES-441
  * Отключил отображение ролей с expire\_at в дайжестах и на странице /queue/. Мера временная, дол нормализации разбора неконсистентностей. RULES-441

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-27 17:49:50

0.14.10
---

  * Исправлена проверка неконсистентностей при аудите на наличие части their\_side. RULES-440.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-27 13:42:30

0.14.9
---

  * Закрытие неконсистентностей по доступам, которые были только в системе, а позже пропали и в ней. RULES-438.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-26 17:48:08

0.14.8
---

  * Теперь в дайжест попадают все запросы, а не только те, что старее суток. RULES-434.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-25 21:17:02

0.14.7
---

  * Просмотр отдельных неконсистентностей доступен для всех.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-25 19:11:12

0.14.6
---

  * Добавлен дополнительный логгинг и мониторинг при заведении неконсистентностей. RULES-431.
  * Сделана нормальная страница неконсистентности. Теперь на нее пускаем всех. RULES-430.
  * Сделан правильный repr для Inconsistency. RULES-429.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-25 18:54:03

0.14.5
---

  * Для уволенных сотрудников отзываем неконсистентные роли из системы, не добавляя их в Управлятор. RULES-424.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-24 18:07:22

0.14.4
---

  * Исправлена ошибка при попытке синхронизировать роли, если есть доступ в состоянии rerequested.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-24 12:59:28

0.14.3
---

  * Пагинация там, где нужна. RULES-419.
  * Поправлены ошибки рендеринга действий. RULES-415.
  * Поправлен текст письма для отправки уведомления об оставшихся подтверждениях. RULES-411.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-23 21:34:30

0.14.2
---

  * Отсекаем перезапрос неактивных ролей при смене отдела, перезапрашиваем только роли в состоянии granted. RULES-421.
  * Поправлена ошибка логирования при разрешении неконсистентностей. RULES-418.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-20 15:52:02

0.14.1
---

  * И опять попытка исправить строки в танкеровых переводах.
  * Экранируем комментарий пользователя из запроса роли для предупреждения xss. RULES-417.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-19 18:40:01

0.14.0
---

  * Добавлена возможность указывать в workflow AD группы, в которые нужно добавить сотрудника
    после того, как доступ будет подтвержден. Например так:

        if role == {'role': 'superuser'}:
              ad\_groups = ['OU=какая-то-группа']

    RULES-403

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-19 15:47:11

0.13.13
---

  * Еще один фикс переводов строк для танкера.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-19 14:20:08

0.13.12
---

  * Исправлена обработка многострочных динамических данных в dynamic\_upload. RULES-407.
  * Теперь From в письмах - upravlyator@yandex-team.ru. RULES-416.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-19 12:00:16

0.13.11
---

  * Улучшения отображения таблицы неконсистентностей, в том числе поправлена ошибка отображения ролей неконсистентности. RULES-412.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-18 16:54:09

0.13.10
---

  * Попытка исправить проблему кривыми переносами строк при django\_upload.
  * Передача all\_heads\_of в review\_roles. RULES-405.
  * Доработка механизма разрешения неконсистентностей - чтобы не мешали старые роли.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-17 14:33:00

0.13.9
---

  * Исправлена ошибка выдаваемая xgettext на многострочных значениях. RULES-407.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-16 16:56:39

0.13.8
---

  * Сохранение переводов в случае ошибки. RULES-407.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-16 11:21:03

0.13.7
---

  * HTML в комментариях на /queue/.
  * Раскомментирован код, отвечающий за пересмотр роли при смене отдела.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-12 19:27:23

0.13.6
---

  * Еще раз исправлена отправка уведомлений.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-09 19:20:23

0.13.5
---

  * Исправлена отправка уведомлений, теперь их снова можно отправлять на конкретные емейлы, а не только объектам типа User.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-09 18:59:35

0.13.4
---

  * Не отправляем писем уволенным сотрудникам. RULES-404.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-09 15:30:24

0.13.3
---

  * Закрываем неконсистентности пользователя при увольнении. RULES-402.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-09 15:21:41

0.13.2
---

  * Исправлена ошибка при попытке заресолвить неконситентность отозванной роли.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-09 11:56:11

0.13.1
---

  * Отключен queue.js.
  * Исправлена ссылка на queue из письма с просьбой подтвердить доступ.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-06 19:18:59

0.13.0
---

  * Finished feature request\_queue\_397.
  * Большинство кроновых команд, например те, что отвечают за автоматический отзыв и пересмотр ролей,
    теперь работают только по будням.
  * Теперь есть единая страница подтверждения доступов, на которой показаны все запросы на
    доступ и их можно подтверждать без дополнительных переходов куда либо. RULES-397.
  * Кроме того, теперь отдельными пиьсмами приходят только обынчые запросы на доступ,
    неконсистентности и регулярные пересмотры своливаются раз в сутки, в виде дайжеста.
  * Не прописываем при dynamic\_upload дату в po файл, чтобы не создавать лишних ревизий в танкере.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-07-05 16:29:38

0.12.6
---

  * Страница для отображения различных данных об одиночной роли. RULES-401.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-26 16:25:17

0.12.5
---

  * Исправлены повторные уведомления о необходимости подтверждения роли при регулярном пересмотре. RULES-400.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-25 16:19:08

0.12.4
---

  * Убираем ненужную ссылку отзыва роли, если она еще не подтверждена. RULES-391.
  * Добавлена ссылка на несоответствия со страницы системы.
  * Исправлено отображение одиночной неконсистентности.
  * Показываем только последние запросы на аппрув роли. RULES-394.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-18 13:23:27

0.12.3
---

  * Исправлен баг, когда роль мог подтвердить любой, кто знает "секретную" ссылку.
    Теперь подтвердить может только тот, кому ссылка адресована, либо суперпользователь
    Управлятора. Так же теперь нельзя указывать произвольный email в качестве
    аппрувера. RULES-392.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-14 19:16:35

0.12.2
---

  * При определении оставшихся подтверждений, теперь учитывается только последний запрос. RULES-393.
  * При формировании списка аппруверов в workflow удаляем повторяющихся подтверждающих. RULES-390.
  * В описании workflow теперь допускаются только объекты типа Approver (а не User). RULES-390.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-14 17:36:16

0.12.1
---

  * Испрвлено отображение неконсистентностей системы для суперпользователя. RULES-388.
  * Добавлена management команда upravlyator\_drop\_role\_descriptions. RULES-389.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-09 17:56:15

0.12.0
---

  * Выпилен плагин к Oracle, теперь он поставляется в отдельном пакете. RULES-386.
  * Поправлены цвета лога. RULES-387.
  * Поправлен шаблон одиночной неконсистентности. RULES-385.
  * Отображаем неконсистентности логинов на страницах неконсистентностей. RULES-385.
  * Добавлен учет неконсистентностей логинов, когда Система сообщает нам логин, который не привязан к сотруднику. RULES-384.
  * Поправлены человеческие названия ролей Управлятора.
  * Добавлена Sphinx документация по API самого Управлятора.
  * Теперь в hash RoleDescription замешан slug и человеческие названия ролей разных систем не должны пересекаться.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-09 16:35:21

0.11.7
---

  * Учет неконсистентностей логинов в при генерации email отчета. RULES-384.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-09 16:07:42

0.11.6
---

  * Поправлены человеческие названия ролей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-07 17:17:31

0.11.5
---

  * Закомментирован DROP TABLE в одной из миграций.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-06 13:08:57

0.11.4
---

  * Теперь в hash RoleDescription замешан slug.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-06 12:36:17

0.11.3
---

  * Поле user в неконсистентностях теперь необязательно, и если в системе есть
    несуществующие, с точки зрения Управлятора, пользователи, то на это будет
    заведена неконсистентность. RULES-384.
  * Паспортный логин может быть необязательным полем. RULES-383.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-06-05 17:27:14

0.11.2
---

  * Теперь в yandex-notification собираются и шаблоны тоже.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-05-16 14:30:21

0.11.1
---

  * Поправлена сборка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-05-16 12:24:18

0.11.0
---

  * Реализовано сохранение уведомлений на стороне Управлятора с тем, чтобы они не терялись в общем потоке писем. RULES-374.
  * Теперь супер-пользователь может применять измения воркфлоу без необходимости отправлятор запрос на подтверждение изменений самому себе. RULES-377.
  * Исправлена ошибка вывода в лог PluginFatalError. RULES-372.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-05-15 15:12:40

0.10.1
---

  * Теперь upravlyator\_django\_api умеет отдавать по ручке /info ограниченное количество ролей плюс ссылку на остальные. RULES-364.
  * Generic плагин умеете выкачивать строить дерево ролей по ссылкам 'next-url'. RULES-364.
  * Исправлено сравнение ролей, имеющих подсказки. RULES-370.
  * Исправлена расстановки флагов на автоматическое обновление дерева ролей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-27 16:27:19

0.10.0
---

  * Сообщения об ошибках, теперь переводятся через Танкер. RULES-342.
  * Появился способ показывать дополнительные подсказки к ролям. http://wiki.yandex-team.ru/Upravljator/api#opisanijarolejj RULES-241.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-19 14:01:46

0.9.1
---

  * Дополнительные правила для создания юзеров в базах Oracle. RULES-368.
  * Добавлен сайдбар с действий над ролями пользователя. RULES-361.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-18 13:41:19

0.9.0
---

  * Добавлен блок Запросы, на главной странице обычного сотрудника. RULES-360.
  * Если был использован login-as, теперь на каждой странице выводится плашечка с логином пользователя. RULES-354.
  * Для аппрувера показваем плашечку с количеством запросов на аппрув, и ссылкой на /me/approve-requests/. RULES-357.
  * В форме запроса роли, текст кнопки изменен с Добавить на Запросить. RULES-352.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-16 12:41:32

0.8.16
---

  * Поправлена десериализация названия роли из базы. RULES-349.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-11 18:28:34

0.8.15
---

  * Теперь отправляем письма, если при добавлении роли возникла ошибка. RULES-350.
  * Увеличено окно просмотра workflow. RULES-356.
  * Теперь все сотрудники могут искать других сотрудников и смотреть их профили. Однако
    список ролей сотрудника виден только ему самому и его начальникам. RULES-344.
  * Так же, начальник может запрашивать доступ для своих подчиненных. RULES-344.
  * Человеческие названия ролей теперь хранятся в базе, и при удалении роли из системы,
    у нас все равно будет оставаться знание о том, что это была за роль. RULES-349.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-11 18:11:33

0.8.14
---

  * Команда upravlyator\_stats approved\_roles\_total изменена на granted\_roles\_total. RULES-355.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-10 17:37:15

0.8.13
---

  * Исправлена ошибка с уже существующим в нашей базе паспортным логином. RULES-348.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-10 15:33:48

0.8.12
---

  * Добавлена опция ignore\_stoplist=1 при вызове admreg. RULES-348.
  * Начальник может запрашивать роль для подчиненного в любой системе. RULES-344.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-10 14:40:39

0.8.11
---

  * Исправлена ошибка с двойным переводом в deprived. RULES-346.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-09 19:34:20

0.8.10
---

  * Еще один фикс в миграции.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-09 18:11:05

0.8.9
---

  * Исправлена миграция 62.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-09 17:54:59

0.8.8
---

  * Исправлен путь до описания коннекторов Oracle.
  * Поправлена обработка ошибок, при отправке финального уведомления о добавлении роли. RULES-341.
  * Мидльварь PassportLoginRedirectMiddleware удалена, теперь декоратор requre\_login редиректит на паспорт. Нужно использовать его, или staff\_member\_requred.
  * Новая процедура редактирования Workflow теперь позволяет сотрудникам вносить правки, с ИБ подтверждать их. RULES-324.
  * Управлятор теперь нормализует паспортные логины и заменяет точки на дефисы.
  * Назалогиненные пользователи редиректятся на паспорт. RULES-333.
  * Поправлена выгрузка с CSV, а то там встречались куски HTML.
  * На странице запроса роли, имена запросивших отображаются в виде ссылки. RULES-340.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-09 17:13:37

0.8.7
---

  * Передаем в письме о выдаче роли паспортный логин и пароль к нему. RULES-337.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-05 20:25:59

0.8.6
---

  * Еще немного логгинга в login\_as.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-05 20:05:15

0.8.5
---

  * Дополнительный логгинг в мидльваре аутентификации.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-05 19:42:54

0.8.4
---

  * Добавлена страница /login-as/, чтобы superuser мог посмотреть на сервис с точки зрения любого пользователя. RULES-334.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-05 18:11:17

0.8.3
---

  * Исправлена ошибка 'global name 'logging' is not defined'. RULES-338.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-04 15:24:26

0.8.2
---

  * Роль "Управление ролями" теперь позволяет запросить роль в системе для другого сотрудника. RULES-335.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-04 14:42:54

0.8.1
---

  * Устранен баг с None вместо словаря при рендеринге action. ROLES-336.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-04 13:14:41

0.8.0
---

  * Переименование пакета в yandex-upravlyator. RULES-135.
  * Роли Управлятора теперь древовидные. RULES-322.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-03 17:53:25

0.8.0-pre4
---

  * Исправлено отображение номера версии в футере.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-28 18:10:09

0.8.0-pre3
---

  * Поправлены пути в scripts.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-28 18:03:48

0.8.0-pre2
---

  * Замена пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-28 17:49:53

0.8.0-pre1
---

  * Переименование пакета в yandex-upravlyator.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-27 15:53:20

0.7.11
---

  * Теперь работает с IE 9. RULES-332.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-04-03 12:46:45

0.7.10
---

  * Не предлагать завести логин длиннее 30 символов. RULES-329.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-30 21:11:10

0.7.9
---

  * Еще один фикс кодировки сообщений от паспорта.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-30 20:56:16

0.7.8
---

  * Перекодировка в Unicode сообщений от паспорта.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-30 20:43:20

0.7.7
---

  * Исправлена обработка 500 ошибок от паспорта. RULES-330.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-30 20:25:42

0.7.6
---

  * Исправлены тесты.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-30 19:33:39

0.7.5
---

  * Теперь дерево департаментов строится на center\_id. Нужна миграция. RULES-327.
  * Нормальное отображение департаментов в админке.
  * Дополнительный логгинг при добавлении паспортного логина.
  * Исправлен URL до admreg.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-30 19:07:45

0.7.4
---

  * Сделано сохранение плохого ответа от паспорта.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-29 20:22:57

0.7.3
---

  * Исправлен хост паспорта для добавления логина.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-29 19:34:05

0.7.2
---

  * Исправлен урл до внешнего blackbox.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-29 18:40:30

0.7.1
---

  * Исправлена ошибка в GenericPlugin. Для логгинга нужно использовать self.log, а не self.\_log.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-28 18:47:56

0.7.0
---

  * Реализован регулярный пересмотр ролей. RULES-321.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-27 14:02:35

0.6.17-1
---

  * Убираем system-specific из отчета о ролях. RULES-325.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-27 12:38:10

0.6.16-2
---

  * Игнорируем CN=NoLogonUsers,OU=Partners,OU=Groups,DC=ld,DC=yandex,DC=ru.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-26 12:46:50

0.6.16-1
---

  * Пробуем собирать через Jenkins.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-22 16:17:24

0.6.16
---

  * Разрешаем Jenkins собирать пакеты.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-20 16:39:08

0.6.15
---

  * Отправляем все отчеты на security-alerts@yandex-team.ru.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-20 13:34:31

0.6.14
---

  * Исправлен еще один баг внутри smtp логгера.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-06 17:55:02

0.6.13
---

  * Исправлена ошибка в кастомном Smtp бэкенде (проявлялась на неюникодных email адресах).
  * Исправлен  BCC в settings.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-06 15:39:38

0.6.12
---

  * Отправляем ошибки отрывания AD аккаунтов, на art@ и ursus@. RULES-319.
  * Добавлен список AD групп, которые не надо отрывать. Улучшено логгирование. RULES-320.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-06 14:24:52

0.6.11
---

  * Страница для отображения паспортных логинов любого пользователя.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-05 19:46:54

0.6.10
---

  * Исправлена проверка существования паспортного логина, при импорте из system-specific.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-05 18:32:46

0.6.9
---

  * Команда для переноса всех существующих паспортных логинов из ролей в модель UserPassportLogin. RULES-318.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-05 18:08:22

0.6.8
---

  * Исправлен вывод в лог инфы о том, что невозможно задисейблить аккаунт.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-05 12:55:42

0.6.7
---

  * Отмечаем, как деактивированных, только тех, у кого действительно всё оторвали.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-05 12:44:49

0.6.6
---

  * Еще один фикс debian/rules.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-02 19:41:29

0.6.5
---

  * В debian/rules добавлено ограничение, позволяющее собирать только из мастера.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-02 19:24:45

0.6.4
---

  * Добавлено поле added в модель и миграция для него. RULES-305.
  * Теперь вне заисимости от наличия паспортных логинов не будет мерцания при выборе роли. RULES-305.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-02 18:38:39

0.6.3
---

  * Переносим товарища в Old Users, только если он еще не там.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-02 18:30:26

0.6.2
---

  * При отзыве учетной записи, ищем так же и в Old Users.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-02 17:16:42

0.6.1
---

  * Считаем запись в AD деактивированной только в том случае, если оторваны все группы.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-02 15:20:57

0.6.0
---

  * Возможность использовать существующий паспортный логин, и не только. RULES-197.
  * Управлятор теперь хранит привязки паспортных логинов к доменным. RULES-305.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-02 12:31:56

0.5.22
---

  * Пробуем отобрать все LDAP группы, и если не получилось, считаем, что аккаунт не деактивирован.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-02 11:13:48

0.5.21
---

  * Поправлен логгинг в disable\_user.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-01 17:26:50

0.5.20
---

  * Еще один фикс AD кода.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-01 17:00:13

0.5.19
---

  * Еще один фикс AD кода.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-01 16:18:21

0.5.18
---

  * Поправлена процедура деактивации AD, чтобы так же обновлялась информация в профиле пользователя.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-01 15:22:18

0.5.17
---

  * Еще раз поправлен вывод ChangeLog.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-01 14:11:01

0.5.16
---

  * OU=Users исправлен на CN=Users.
  * Исправлены ошибки при humanize роли, пропавшей из /info/. RULES-316.
  * Исправлен вывод Changelog в продакшн. RULES-315.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-03-01 13:46:45

0.5.15
---

  * Выводим ChangeLog в интерфейсе. RULES-315.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-29 19:16:15

0.5.14
---

  * Дополнительное логирование оракловых ошибок.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-29 16:51:36

0.5.13
---

  * Таймаут по умолчанию в GenericPlugin теперь 10, а не 3 секунды.
  * Проверка логина и роли на корректность (чтоб sql инъекция не прорвалась). RULES-284.
  * Откат создания пользоваетля, профиль dba\_users -> db\_users, логирование.RULES-284.
  * Исправлены тесты, валившиеся из за использования memcache.
  * Исправлены тесты, валившиеся из за измененного таймаута.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-29 15:10:30

0.5.12
---

  * Оракловый коннектор для CRM вытянут в строку.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-27 18:02:35

0.5.11
---

  * Возможность игнорировать строчки логов, при рассылке дайджеста.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-27 13:04:58

0.5.10
---

  * Разделены настройки клиента Oracle для продакшена и тестинга. RULES-284.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-27 12:40:01

0.5.9
---

  * Проставление активности ldap профиля нового сотрудника. RULES-313.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-24 18:43:06

0.5.8-oracle4
---

  * Продакшен логин и коннект-дескриптор для Oracle. RULES-284.
  * Создаем пользователей в Oracle в верхнем регистре. RULES-284.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-24 17:03:49

0.5.8-oracle3
---

  * Перемещение каталога настроек Oracle и путей. RULES-284.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-16 19:03:13

0.5.8-oracle2
---

  * Замена кавычек на одинарные и наоборот для корректного взаимодействия с Oracle. RULES-284.
  * ORACLE\_HOME и дефолтный конфиг для сборки пакета. RULES-284.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-16 18:19:16

0.5.8-oracle1
---

  * Не присылаем WARNING на почту. RULES-308.
  * Плагин для работы с Oracle.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-16 15:05:19

0.5.8
---

  * Декодируем строки лога, прежде чем посылать их на почту. И понятные имена переменных. RULES-312.
  * Команды парсинга логов посылает только последние 1000 записей. RULES-312.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-24 13:06:42

0.5.7
---

  * Управлятор теперь отрывает учетные записи в AD. RULES-261.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-22 15:50:33

0.5.6-ldap4
---

  * Исправлена ошибка поиска уволенного пользователя в AD.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-21 15:33:10

0.5.6-ldap3
---

  * Исправлены имена LDAP хостов, чтобы совпадали с теми, что в сертификате.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-21 13:18:09

0.5.6-ldap2
---

  * Собираем статистику по деактивации пользователей в AD. Ключ: firewall.user.ad.deactivated

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-20 17:40:46

0.5.6-ldap1
---

  * Настройки AD LDAP для продакшена.
  * Миграция 53: в профиль добавлено поле активности пользователя в LDAP.
  * Добавлена задача отзыва учетки пользователя из LDAP. RULES-261.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-20 16:43:01

0.5.6
---

  * Title для писем с грепами лога.
  * Не присылаем WARNING на почту. RULES-308.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-17 17:44:10

0.5.5
---

  * При особой отметке в workflow, письма о подтверждении роли рассылаются всем аппруверам. RULES-300.
  * Исправлено попытка автообновления ролей для отключенных плагинов.
  * Добавлен пропавший шаблон reports.html.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-13 13:16:52

0.5.4
---

  * Запуск автоматического обновления ролей по крону. RULES-299.
  * Возможность получения параметра context при добавлении роли в систему. RULES-297.
  * Изменение теста синхронизации с учетом lang\_ui.
  * Фильтр по системам и датам изменения ролей. RULES-294.
  * Фильтр лога для формирования отчетов по действиям пользователей, системам и датам. RULES-236.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-02-09 14:49:47

0.5.3
---

  * Добавлен автокомплит для all\_heads\_of функции workflow. RULES-292.
  * Автокомплит по пользователям теперь срабатывает только после набора трех букв.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-23 20:18:09

0.5.2
---

  * Пересборка с обновленными переводами.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-19 17:58:38

0.5.1
---

  * Исправлена \_add\_log\_entry на случай, если плагин не найден.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-19 16:11:25

0.5.0
---

  * Забираем lang\_ui из центра. Теперь у интернациональных сотрудников будет английский язык.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-19 15:30:16

0.4.30
---

  * Поправлены все косяки с забором ролей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-19 14:24:03

0.4.29-3
---

  * Исправлен сброс кэша при обновлении ролей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-19 14:14:46

0.4.29-2
---

  * Исправлена ошибка при установке. RULES-277.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-19 13:52:58

0.4.29-1
---

  * Логирование для отладки кэша. RULES-277.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-19 13:29:06

0.4.29
---

  * Отзыв выданных ролей при их удалении из системы. RULES-293.
  * Команда автоматического обновления дерева ролей отзывает удаленные роли. RULES-293.
  * В JSONField обертки заменены на JSONDict и JSONList.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-18 19:48:46

0.4.28
---

  * Более удобное приведение типов в JSON, поле JSON не переворачивает кавычки
    когда не надо.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-18 13:17:58

0.4.27
---

  * Функция получения списка начальников подразделений all\_heads\_of. RULES-292.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-18 12:57:09

0.4.26
---

  * Добавлена поддержка tmux в тестах, и tdaemon.
  * Команда для рассылки дайджестов логов с ошибками ответственным за системы. RULES-279.
  * Отправление письма уполномоченным сотрудникам о невозможности удаления ролей выданных ранее. RULES-277.
  * Команда для автоматического обновления дерева ролей. RULES-277.
  * Добавлена страница отображения дерева ролей. RULES-277.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-01-16 17:22:45

0.4.25
---

  * Расширенное сообщение об ошибке при аудите. RULES-281.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-26 16:53:13

0.4.24
---

  * Отправление письма с просьбой подтвердить роль с параметром Reply-To. RULES-278.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-23 12:25:55

0.4.23
---

  * Группируем сообщения перевода и передаем в качестве контекста список систем. RULES-275.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-21 17:18:56

0.4.22
---

  * Шаблон письма для Директа перенесен в базу.
  * Удалены шаблоны emails/role\_approved\_*.txt
  * Шаблон письма о выдаче роли теперь с именем role\_granted.txt. RULES-276.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-20 14:44:43

0.4.21
---

  * Выводим имя и фамилию пользователя в зависимости от текущей локали. RULES-274.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-19 18:33:56

0.4.20
---

  * Пересборка с новыми переводами.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-19 14:23:44

0.4.19
---

  * При сборке пакета, берем данные из продакшн танкера.
  * Интернационализация данных, запрашиваемых чрез api. RULES-163.
  * Сделана проверка существования роли, при добавлении ее через API. RULES-235.
  * Изменено отображение ролей (при их наличии) на странице пользователя. RULES-270.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-19 13:35:51

0.4.18
---

  * Пересборка с новыми переводами.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-16 18:01:02

0.4.17
---

  * Используем исправленный django-kombu==0.9.4.art0.dev.
  * Отображаем ошибку, если не выполнился аяксовый запрос. RULES-271.
  * Фикс для прекращения логирования огромных записей, приходящих от систем.
  * Если указан только Accept-Language, используем его для выбора языка. RULES-163.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-16 12:23:30

0.4.16
---

  * Умный поиск + opensearch. RULES-244, RULES-267.
  * При отображение действия, учитываем пол сотрудника.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-14 16:46:15

0.4.15
---

  * Исправлено обнаружение неполадок в структуре департаментов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-13 16:55:00

0.4.14
---

  * Исправлена проверка структуры департаментов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-13 14:58:52

0.4.13
---

  * В урлы писем добавлены UTM метки. RULES-269.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-13 14:46:21

0.4.12
---

  * Исправлена синхронизация с центером. RULES-265.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-13 13:01:31

0.4.11
---

  * Переключаемся на db-new.art.dev.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-12 17:44:30

0.4.10
---

  * Management команды обернуты в try except. RULES-266.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-09 17:22:08

0.4.9
---

  * Изменен формат макросов пользователей систем. RULES-262.
  * Добавлен крон для сабмита файрвольных правил в svn.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-09 15:38:54

0.4.8
---

  * Отправка писем только одному подтверждающему из присутствующих на работе (если логика ИЛИ). RULES-254.
  * Сообщение при запросе роли, когда аппруверы отсутствуют. RULES-263.
  * Исправлена ошибка в Generic плагине. RULES-264.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-09 11:25:52

0.4.7
---

  * Исправлена команда dynamic\_download.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-08 16:32:19

0.4.6
---

  * Удален лишний set\_trace.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-07 16:39:33

0.4.5
---

  * Вывод дополнительных сообщений в скрипте генерации правил фаервола -
    только при --verbose. RULES-252.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-07 16:12:01

0.4.4
---

  * При запуске команд в dev окружении используем тестовый танкер.
  * Merge режим при работе с Танкером.
  * Исправлена ошибка при попытке залогировать все роли, приехавшие от Статистики.
  * Ограничение на предельно допустимое количество заливаемых в танкер записей (чтобы не заливать туда все роли, какие есть в Статистике).

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-07 15:24:05

0.4.3
---

  * Скрипт, генерерующий правила для фаервола. RULES-252.
  * Поправлен фильтр запроса пользователей через API. RULES-259.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-07 13:17:04

0.4.2
---

  * Всегда сохраняем роль после создания Action. RULES-256.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-01 19:46:01

0.4.1
---

  * Исправлена ошибка на странице подтверждения доступа. RULES-258.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-01 17:57:31

0.4.0
---

  * Большой рефакторинг состояний роли. RULES-255.
  * Исправлена ошибка авторизации SSL сертификатом, когда subject есть, но он пустой.
  * Исправлена ошибка отображения действия 'запустил синхронизацию'.
  * Комментарий события во всплывающей подсказке о ролии. RULES-255.
  * На странице пользователя добавлена возможность выбора активных/неактивных ролей. RULES-255.
  * update-translation теперь загружает данные в танкер.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-30 17:58:41

0.3.16
---

  * Исправлена ошибка при добавлении роли, когда уже есть такая, но была отклонена. RULES-253.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-25 14:20:22

0.3.15
---

  * Добавлен robots.txt. RULES-248.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-24 15:02:55

0.3.14
---

  * Зависимость от нового python-django-tanker 0.8.2.
  * Исправлено получение логина текущего пользователя в файле настроек.
  * Переводы статических данных на английский.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-23 20:00:08

0.3.13
---

  * Переезд на django=1.3-20110926.svn16904-yandex1. Исправлена админка на dev виртуалке. RULES-247.
  * В dev версии используем Django, установленный в систему из пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-22 17:52:38

0.3.12
---

  * Исправление, чтобы db-templates нормально работал с Django >= 1.4.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-22 15:51:58

0.3.11
---

  * Переход на django-dbtemplates = 1.2.1.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-22 15:17:56

0.3.10
---

  * Теперь можно включить на продакшене код метрики. RULES-246.
  * Добавлен редирект с короткого имени agranat. RULES-245.
  * Исправлены тесты, сломавшиеся из-за включения обязательной авторизации в API.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-22 14:50:04

0.3.9
---

  * Исправлен показ ролей Аудитору. RULES-243.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-17 16:22:27

0.3.8
---

  * Исправлена 500ка у Аудитора. RULES-242.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-17 12:35:08

0.3.7
---

  * Выгрузка ролей системы в формате CSV. RULES-217.
  * Временно отключен механизм протухания ролей при смене отдела.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-16 19:45:32

0.3.6
---

  * Поправлена ошибка из за которой оставался expire\_at у проаппрувленных ролей. DOSTUP-17722, DOSTUP-17755.
  * Конфиг Nginx для резработческого сервера, с проверкой SSL сертификата и отдельными хостами для API.
  * Требуем авторизации SSL сертификатом у тех, кто дёргает API ручки. RULES-190.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-15 15:47:05

0.3.5
---

  * Отправка писем при изменении workflow. RULES-223.
  * Исправлена отправка формы запроса роли по нажатию Enter в поле комментария. RULES-206.
  * Исправлена ошибка при открытии формы редактирования workflow. RULES-234.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-14 16:41:19

0.3.4
---

  * Исправлена ошибка с юникодом, при рендеринге RoleColumn.
  * Не дергаем add-role, при повторном подтверждении роли. RULES-232.
  * Исправлены редиректы на HTTPS. RULES-233.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-11 15:13:13

0.3.3
---

  * Исправлена отправка писем.
  * Логирование для команд динамической загрузки, выгрузки переводов. RULES-110.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-11 13:51:04

0.3.2
---

  * Пишем в лог про каждую отправку письма.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-11 12:29:18

0.3.1
---

  * Добавлена потерянная зависимость от gettext.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-11 11:29:13

0.3.0
---

  * ИНТЕРНАЦИОНАЛИЗАЦИЯ. RULES-110.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-10 18:47:46

0.2.98
---

  * Кастомный email backend, для сбора статистики. RULES-222.
  * Отправка уведомлений о зависших аппрувах. Уведомляем только о запросах, которые "висят" более суток. RULES-230.
  * Конфиг для Nginx, требующий правильного сертификата на api.agranat.yandex-team.ru. RULES-195.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-10 14:44:51

0.2.97
---

  * Фильтр по пользователю на странице неконсистентностей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-08 13:12:14

0.2.96
---

  * Фильтр по системам и is\_resolved на странице Неконсистентностей. RULES-224.
  * Карточки сотрудников на странице подтверждения роли.
  * Исправлена ошибка при просмотре реквеста на роль которая сфейлилась.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-08 12:47:34

0.2.95
---

  * Исправлены контролы на странице подтверждения роли с истекшим сроком.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-07 19:16:57

0.2.94
---

  * Исправлен баг отображения запросов на аппрув.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-07 19:05:33

0.2.93
---

  * Суперпользователь может смотреть зависшие запросы на аппрув других сотрудников.
  * Не включаем дату в subject письма об ошибках.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-07 18:55:32

0.2.92
---

  * Добавлена страница 'зависших аппрувов' /me/approve-requests/. RULES-169.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-07 17:35:47

0.2.91
---

  * Ничего нового. Фейк для apt-get.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-03 18:08:00

0.2.90
---

  * Добавлена команда, отдающая статистику по зависшим аппрувам.
  * Добавлена management команда firewall\_stats.
  * Анализатор неконсистентностей научился понимать, что неконсистентность пропала, и помечать ее, как is\_resolved. RULES-227
  * Исправлены выдача всех ролей в самом Управляторе. RULES-226.
  * Теперь действия привязываются к запросам на аппрув.
  * Отправка писем пользователю при отказе в подтверждении роли. RULES-192.
  * Теперь repr у объектов типа Approve показывает кто подтвердил, а кто нет.
  * Крон поправлен, чтобы грепать ошибки только на продакшене.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-11-03 17:40:21

0.2.89
---

  * Поправлено письмо, отсылающее ошибки.
  * Изменена иконка, добавлены реврайты для favicon.ico.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-26 18:24:08

0.2.88
---

  * Правильный путь до sendmail.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-26 16:29:09

0.2.87
---

  * Новый UserParameter для Zabbix. RULES-215.
  * Теперь ошибки грепаются и отправляются на почту раз в 15 минут.
  * Консистентные названия для логгеров.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-26 14:42:08

0.2.86
---

  * Корректная обработка ситуации, когда у сотрудника не назначен отдел и get\_boss возвращает None. В этом случае просто показываем ошибку и не даем запросить роль.
  * Исправлена ошибка запуска синхронизации с центром из под крона.
  * Пишем warning, если при синхронизации встречен сотрудник без департамента.
  * Больше не стопим lighttpd при выкладке пакета.
  * Присылаем на почту не только ERROR,  но и WARNING с CRITICAL.
  * Скрипт send-errors исправлен. И теперь он будет посылать отчеты так же и на fantom@yandex-team.ru
  * Более информативные сообщения о невозможности загрузить settings.py или local\_settings.py.
  * Новый тип действия — 'отказать' (пока не используется).

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-25 19:00:27

0.2.85
---

  * Дополнительная страница для протухших ролей пользователя. ROLES-209.
  * Открытие страницы с ролями пользователя и уже заполненными полями запроса роли. Данные для выбора передаются в url. RULES-200.
  * Добавлена проверка для словаря в remove\_password. Поправлены тесты.
    RULES-212.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-24 16:42:32

0.2.84
---

  * Поправлен скрипт send-errors.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-24 13:51:29

0.2.83
---

  * Еще раз поправлен путь к логам.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-21 23:13:14

0.2.82
---

  * Добавлен скрипт, чтобы оповещать меня об ошибках в бэкенде.
  * Поправлен путь к логу и logrotate.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-21 20:48:29

0.2.81
---

  * Окончательный переход на Nginx.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-21 19:55:37

0.2.80
---

  * Поправлен продакшн конфиг nginx.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-21 19:29:42

0.2.79
---

  * Зависимость от syslog-ng.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-21 18:16:59

0.2.78
---

  * Зависимость от nginx.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-21 18:04:07

0.2.77
---

  * Конфиги для NGINX.
  * Теперь все логирование идет через syslog-ng.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-21 17:48:54

0.2.76
---

  * Выводим в /me/expire/ все роли у которых есть дата протухания, даже если
    дата уже в прошлом.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-19 14:52:42

0.2.75
---

  * Отключена проверка клиентского сертификата в lighttpd.
  * Добавлен в зависимости python-mimeparse (для tastypie).

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-14 11:54:26

0.2.74
---

  * Возможность авторизации SSL сертификатом. RULES-195.
  * Конфиг для запуске dev сервера, как FastCGI.
  * Ручка для запроса роли и проверки ее статуса. RULES-162.
  * Ручки API, отдающие список систем, систему и пользователей в ней.
  * Исправлена функция remove\_password. RULES-204.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-13 19:05:58

0.2.73
---

  * Расширенное логгирование в humanize\_using\_slug. RULES-201.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-12 12:22:10

0.2.72
---

  * Список корневых департаментов вынесен в settings.py.
  * Переход на coverage==3.5.1
  * Исправлена ошибка препятствующая обработке смены отдела!
  * Исправлено создание System для GenericPlugin.
  * Переименован services в sync.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-10-10 18:26:56

0.2.71
---

  * Логируем перевод из отдела в отдел.
  * Включил себя в список получающих алерты о поломанном дереве департаментов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-30 18:27:53

0.2.70
---

  * Уведомляем thasonic, если структура департаментов поломалась. RULES-196.
  * Признак is\_active перенесен в Систему. RULES-193.
  * Зависимость от python-django-russian (>=0.18)

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-30 14:59:31

0.2.69
---

  * Исправлены запросы с пустым system к /get-roles/. RULES-189.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-27 16:13:24

0.2.68
---

  * Теперь пакет yandex-firewall-admin должен зависеть от конкретной версии yandex-firewall-django-api. RULES-188.
  * Корректный перенос параметров в тело POST запроса. RULES-185.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-27 13:12:06

0.2.67
---

  * Страница подтверждения теперь не требует прав доступа в админку, а только
    проверяет залогиновость.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-22 11:34:12

0.2.66
---

  * Исправлено отображение сообщение об ожибке при выполнении действия.
  * Опциональный комментарий в форме запроса роли. RULES-180.
  * Нормальные имена в уведомлениях и карточки сотрудников на сайте. RULES-180.
  * Страница подтверждения роли теперь требует логина. RULES-179.
  * Передаем request в контекст страниц с ошибкой, когда доступ запрещен.
  * Компиляция CSS для IE.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-21 15:52:02

0.2.65
---

  * Схеманезависимые урлы для JS статики.
  * HTTPS в урлах в письме.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-20 17:52:08

0.2.64
---

  * Таймаут 60 секунд на запросу ролей.
  * Исправлена ошибка редактирования Workflow у новой системы. RULES-171.
  * Исправлен игнор уволенных сотрудников в процессе аудита. RULES-175.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-18 10:45:19

0.2.63
---

  * Исправлена ошибка в скрипте, выполняющем аудит.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-07 14:48:11

0.2.62
---

  * Больше не рассылаем писем с тестинга.
  * Дополнительные тесты на смену департамента.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-07 14:05:31

0.2.61
---

  * Механизм повторного запроса ролей при переводе в другой департамент или отдел. RULES-133.
  * Сообщение, что у сотрудника пока нет ролей (/me/).
  * \_\_repr\_\_  для Approve и ApproveRequest.
  * Исправлена ссылка на сотрудника (в логе).

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-06 16:08:14

0.2.60
---

  * Исправлена ошибка на дашборде администратора системы. RULES-164.
  * Исправлена страница c 500 ошибкой.
  * Вью, добавляющая роль, сделана с поддержкой транзакций. Нужно
    сконвертировать таблички в InnoDB.
  * Исправлена ошибка, когда в workflow в approver передавался UserWrapper вместо строки. RULES 166.
  * Вывод номера версии суперпользователю.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-09-02 12:29:32

0.2.59
---

  * Экспорт лога действий с CSV формате. RULES-129.
  * Исправлен заголовок на странице пользовательских ролей. RULES-156.
  * Исправлен путь до SSL сертификата. RULES-155.
  * Уменьшен интервал кэширования статистики по ролям.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-31 15:07:17

0.2.58
---

  * Уведомление сотрудника о том, что требуются подтверждения.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-30 16:42:13

0.2.57
---

  * Крон для очистки очереди задач от старых задач. RULES-158.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-30 15:05:23

0.2.56
---

  * Celery больше не будет сохранять результаты задач. RULES-158.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-30 14:27:56

0.2.55
---

  * Исправлена ошибка отзыва роли, которая не подтверждена. RULES-160.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-29 20:31:46

0.2.54
---

  * Исправлена ошибка в обертывании user и requester при передаче в workflow.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-29 18:37:55

0.2.53-8
---

  * Всё, установка и удаление работают как надо.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-11 17:48:13

0.2.53-7
---

  * Еще одно исправление для правильного удаление и установки

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-11 17:37:13

0.2.53-6
---

  * Еще одно исправление для правильного удаление и установки

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-11 17:22:10

0.2.53-5
---

  * Еще одно исправление для dh\_environment

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-11 17:05:29

0.2.53-4
---

  * Еще одно исправление для dh\_environment

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-11 16:21:09

0.2.53-3
---

  * Еще одно исправление для dh\_environment

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-11 15:54:49

0.2.53-2
---

  * Еще одно исправление для dh\_environment

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-11 14:40:00

0.2.53-1
---

  * Добавлен конфиг для dh\_environment.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-11 13:51:43

0.2.53
---

  * Используем dh\_environment вместо dh\_django\_init.
  * Автокомплит для выбора департамента в is\_head\_of.
  * Код автокомплита поправлен в соответствии с http://jshint.com/

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-11 12:51:56

0.2.52
---

  * Метод is\_head\_of добавлен в автокомплит.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-09 17:41:07

0.2.51
---

  * Добавлен метод is\_head\_of. RULES-153
  * Исправлена 500 ошибка на превью воркфлоу. RULES-152.
  * Поправлены пути до сертификатов в продакшене.
  * Исправлен автокомплит роли. ROLES-151.
  * Нормальная обработка TAB в автокомплите.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-09 16:56:27

0.2.50
---

  * Автокомплит ролей при редактировании workflow.
  * Имя сотрудника или департамента в комментах после срабатывания автокомплита.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-05 18:45:36

0.2.49
---

  * При сверке, игнорируем отсутствующий пароль. RULES-149.
  * Метод is\_boss\_of поддерживает текстовые логины. RULES-148.
  * Теперь слаг департамента полный и может быть использован, как id в методе works\_in\_dep. RULES-136.
  * Автокомплит при редактировании Workflow. RULES-147.
  * Можно прописать в local\_settings.py пути до сертификатов которые будут использованы для HTTPS.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-05 13:23:23

0.2.48-1
---

  * Исправлена миграция фейлившаяся на Duplicate Error.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-01 17:59:05

0.2.48
---

  * Берем сертификат для подписи из конфига. RULES-143.
  * Записываем в лог факт запуска синхронизации с Системой.
  * Исправлена синхронизация с системой если уже есть сфейлившиеся роли. RULES-145.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-08-01 15:45:24

0.2.47
---

  * Отдельные доступы для редактирования workflow и шаблонов. RULES-144.
  * Автоматическая сверка списка ролей в системах с базой Управлятора. RULES-132.
  * works\_in\_dep проходит вверх по иерархии. RULES-136.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-26 16:08:37

0.2.46
---

  * Привязка подсетей к токену. RULES-137.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-21 12:30:22

0.2.45
---

  * Исправлен декоратор json.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-20 11:30:42

0.2.44
---

  * Поддержка JSONP. RULES-138.
  * В логе выводим логины, если нет нормального имени.
  * Чистим buildout перед тем, как делать девелоперский bootstrap.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-19 18:21:42

0.2.43
---

  * Отображение действий в логе, со склонятором.
  * Рисуем диффы изменений workflow в логе. RULES-130.
  * Фильтр по статусу роли на странице пользователя. RULES-131
  * Фильтр ролей системы. RULES-131
  * Статистика по статусу ролей в системе.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-19 16:30:25

0.2.42-1
---

  * Чистим buildout перед сборкой пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-14 19:10:08

0.2.42
---

  * Редактирование шаблона письма. RULES-128.
  * Исправлена загрузка плагинов так, что теперь они не десериализуются каждый раз из кэша.
  * Добавлена поддержка dbtemplates.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-14 18:41:46

0.2.41
---

  * Вывод версии пакета в HTML.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-07 16:23:40

0.2.40
---

  * Подключен django-reversion для Workflow.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-07 15:50:29

0.2.39
---

  * Поддержка авторизации с использованием SSL сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-06 17:04:02

0.2.38
---

  * Параметр requester в ручке /add-user-role/.
  * Правильная обработка ошибок в RoleRemoved.failed.
  * Добавлена возможность авторизации по токену.
  * URL репозитория перемещен в главный buildout
  * Ручка, отдающая список систем. RULES-114.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-05 18:12:13

0.2.37
---

  * Пересборка с Djblets.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-07-01 16:54:57

0.2.36
---

  * Генерация отчетов о неконсистентности ролей.
  * Исправлен формат времени. RULES-117
  * Функции get\_boss и is\_boss\_of. RULES-121.
  * Работающие примеры поиска.
  * Исправлена ссылка на главную страницу с логотипа.
  * Импорт данных из Center.y-t.ru. RULES-101
  * Возвращаем 404 если пользователь не найден.
  * Поддержка Django 1.3.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-06-30 15:41:43

0.2.35
---

  * Автокомплит по сотрудника при проверке workflow. RULES-42.
  * Выбиралка роли с автокомплитом. RULES-38.
  * Сотрудник может отзывать свои роли. RULES-109
  * Теперь можно отозвать неподтвержденную роль.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-06-17 14:42:30

0.2.34
---

  * Удален рестарт celery, он и так делается.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-06-14 17:21:23

0.2.33
---

  * Теперь действия пользователей и ошибки по ним, логируются в UserActionInfo.
  * Вывод в лог таймаутов при обращении к системе.
  * Исправлена сортировка ролей по сотруднику.
  * Исправлено сохранение сортировки при листании страниц.
  * Исправлено дублирование ролей при импорте.
  * Исправлена пометка уволенных сотрудников при синхронизации.
  * Исправлено логирование ответов от сервисов.
  * Рестарт celery в postinst.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-06-14 16:47:02

0.2.32
---

  * Исправлен отзыв ролей у уволенных. RULES-105.
  * Конфиг для заббикса.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-06-08 11:00:12

0.2.31
---

  * Django API может принимать token и в GET и в POST.
  * Исправлен отзыв суперпользователя Управлятора.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-06-03 17:23:25

0.2.30
---

  * Исправлен перевод роли в failed при ошибке отзыва.
  * Авторизация в Django API по токену. RULES-98.
  * Не генерируем кучу тасков про увольнения.
  * Не посылаем уведомления при импорте ролей из системы. RULES-97.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-06-03 12:24:59

0.2.29
---

  * Конфиг для logrotate.
  * "From" исправлен на security@yandex-team.ru
  * Исправлена работа в IE. IE6 не поддерживается.
  * Поправлены README, лайти конфиг и local\_settings.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-05-31 11:11:15

0.2.28
---

  * Поправлено имя лога celeryd.
  * Исправлена ручка выдающая права на сам Управлятор.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-05-11 13:00:23

0.2.27
---

  * Кастомное письмо от Директа, с логином/паролем.
  * Rename ajax/user-role-details.html
  * Показываем паспортный логин в попапе. RULES-92.
  * Поправлен порядок UserRoleActions.
  * Информативные сообщения об ошибках добавления роли
  * Поправлен CSS и настрочки для поддержки потухших ролей.
  * Generic плагин правильно обрабатывает токен Директа.
  * Исправлена обработка превышения кол-ва ретраев.
  * Перезапускаем сервис после установки пакета.
  * Обработка старых запросов роли. RULES-72.
  * Уведомление об аппруве роли. RULES-54.
  * Исправлено создание уволенных сотрудников. RULES-90.
  * Исправлена обработка system\_specific при импорте.
  * Base url может иметь название ручки в любом месте.
  * Тест на обработку UnrecoverableError. RULES-89.
  * Одинаковые роли с разным system\_specific.
  * API вызовы возвращают code=XXX.
  * Забираем system\_specific при начальной синхронизации.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-05-06 16:06:51

0.2.26
---

  * Передача доп информации из ручки /add-role/ и а ручку /remove-role/.
    RULES-84.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-04-29 16:12:15

0.2.25
---

  * Добавлены примеры workflow и ссылка на описание. RULES-82.
  * Зависимость от stratostat >= 0.1.8

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-04-27 17:15:53

0.2.24
---

  * Исправлена ошибка у анонимуса.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-04-26 12:25:31

0.2.23
---

  * Исправлена загрузка плагинов при старте Celery.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-04-25 17:37:13

0.2.22
---

  * Исправлена сериализация GenericPlugin.
  * Динамическое добавление систем, использующих API.
  * Отображение комментария о роли.
  * Создание действий при автоимпорте. RULES-81.
  * Исправлен тест доступа к логу событий.
  * Popup с расшифровкой статуса роли.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-04-25 16:16:32

0.2.21
---

  * Тесты django API исправлены для python2.5
  * Использовать джанговский кэш для ролей. RULES-76.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-04-11 14:01:04

0.2.20
---

  * Новое отображение списка ролей в системе.
  * Аватарки сотрудников. RULES-69.
  * Ссылка на систему из списка ролей пользователя.
  * Первичная синхронизация ролей. RULES-71.
  * Добавлена view для первичного забора данных из системы.
  * Описание переопределенных хуков.
  * Упрощены хуки Django API.
  * Хуки в виде класса. RULES-70.
  * Сортировка систем по имени. RULES-64.
  * Исправлена строка поиска на странице сервиса.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-04-07 17:22:51

0.2.19
---

  * Создание Django пользователя при присвоении роли.
  * Подключен тестовый Досталятор.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-03-28 17:02:47

0.2.18
---

  * Исправлена зависимость от самого нового python-central.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-03-25 16:55:35

0.2.17
---

  * Тестируем использование джанговского API.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-03-25 16:44:23

0.2.16
---

  * Исправлен postinst.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-03-25 15:37:59

0.2.15
---

  * Апгред базы после установки пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-03-25 15:21:06

0.2.14
---

  * Игнорировать django\_guts если не установлен.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-03-25 15:12:27

0.2.13
---

  * Исправлено отображение строки поиска для админа.
  * Только доступные системы на странице ролей.
  * Фильтры ролей в админке + DebugToolbar.
  * BaseTask перенесен в отдельный модуль.
  * Добавлена фавиконка. RULES-59.
  * Исправлено отображение времени. RULES-61.
  * Подсчет кол-ва уволенных, для мониторинга.
  * Обработка увольнения сотрудника. RULES-56.
  * Расширение профиля пользователя. Нужна миграция.
  * Миграция исправляющая apporoved=None (RULES-60).
  * Workflow редактируют только админы и суперы.
  * Dependency from yandex-stratostat-server
  * Сбор статистик через stratostat сервер (RULES-55).
  * Используем devserver и guts в разработке.
  * Уменьшено количество процессов Django и Celery.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-03-25 15:02:26

0.2.12
---

  * Исправлено копирование содержимого "яиц" билдаута.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-03-11 17:36:30

0.2.11
---

  * Шаблоны 500 и 404 страниц. RULES-57.
  * Логируем 500 ошибки с использованием jogging.
  * Не кладем в buildout все яйца.
  * Зависимость от yandex-python-yutil>=1.6.3.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-03-11 16:28:24

0.2.10
---

  * Крон для продакшена. RULES-48.
  * Для обычных пользователей скрываем форму поиска. RULES-50.
  * Ручка /get-roles/ не требует is\_staff. RULES-49.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-25 16:25:57

0.2.9
---

  * Из buildout убраны лишние два пакета.
  * Исправлены DepricationWarnings.
  * Зависимость от пакета python-lxml.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-25 13:12:23

0.2.8
---

  * Lighttpd и Django конфиги для продакшена.
  * Отключен xscript модуль development.
  * Зависимость от simplejson.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-25 12:35:08

0.2.7
---

  * Конфиг для продакшена.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-18 15:29:08

0.2.6
---

  * Правильный урл до тестового Центра.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-18 15:10:41

0.2.5
---

  * Правильный путь к логам для xscript.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-18 12:55:30

0.2.4
---

  * Поправлен скрипт, собирающий buildout в debian пакет.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-18 11:24:12

0.2.3
---

  * Поправлен скрипт для запуска и деплоя в разработке.
  * Модуль py включен в стандартный buildout.
  * Зависимость от нужных lighttpd конфигов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-18 11:09:35

0.2.2
---

  * Зависимость админки от пакета с API.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-17 18:34:05

0.2.1
---

  * Пересборка пакета с нормальным buildout.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-17 18:22:26

0.2.0
---

  * Страница со списком ролей обычного пользователя.
  * Допилен процесс workflow.
  * Запуск Workflow по добавлению роли.
  * Выбор главного паспортного логина для Директа. RULES-36.
  * Добавлены хуки для управления ролями самого Управлятора.
  * В клиентское Django API добавлены хуки для управления ролями.
  * Ограничение прав только на редактирование ролей своих систем, для простых администраторов. RULES-34.
  * Починен декоратор render.
  * Добавлена специальная страница для запрещения доступа и проверка, имеет ли пользователь доступ к системе. RULES-33
  * Теперь администратор систем может смотреть их лог. RULES-32.
  * Дашборд для администратора систем. RULES-29, RULES-30.
  * Добавлен лог последний действий на дашборде аудитора. RULES-28.
  * Список всех доступных систем в dashboard суперюзера. RULES-27.
  * Лог действий на дашборде суперпользователя. RULES-26.
  * Исправлен баг с кнопкой добавления роли. RULES-23.
  * Запоминание паспортного логина для директа.
  * Добавлено поле system\_specific.
  * Базовый класс Task. Пометка ролей, как сфейлившихся.
  * Добавлен generic плагин, который будет работать с любой системой, поддерживающей http://wiki.yandex-team.ru/Upravljator/API.
  * Новый deb пакет с API.
  * Добавлена ручка для получени ролей пользователя.
  * Добавлена ручка отдающая все роли пользователей в системе.
  * Добавлена ручка для удаления роли.
  * Добавление групп пользователю.
  * Реализовано добавление суперпользователей.
  * Добавлено приложение, реализующее API системы для django проектов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-02-17 16:04:14

0.1.11
---

  * Добавлены south миграции.
  * Исправлена работа подсказок в поиске.
  * Утащил к себе процедуру синхронизации с center.yandex-team.ru.
  * На странице ролей пользователя исправлен конфликт имен переменных в контексте.
  * Сделано отображение бывших сотрудников.
  * Добавлены проверки прав на добваление/удаление ролей во вьюхах.
  * Добавлена связь между пользователями и системами и ограничение для
  * несуперпользователей на доступные системы.
  * Исправлены тесты.
  * Добавлен лог всех действий и permission чтобы его просматривать.
  * Добавлена проверка, что такая роль уже есть. RULES-20.
  * Работающий лог действий по добавлению/подтверждению/отзыву роли.
  * Атрибут 'active' заменен на 'status' с тремя различными состояниями.
  * Добавлен тест на авто аппрув роли и то что запись об этом попадает в лог.
  * Теперь используется User из contrib.auth. Добавлена модель для действий по
  * добавлению роли.
  * Тесты исправлены.
  * Добавлено обновление русских имен пользователя из staff. RULES-15.
  * Удобные переходы на результаты live-search с помощью клавиатуры.
  * Добавлен live-search по пользователям и системам.
  * На страницу ролей в системе, добавлен пейджер.
  * Теперь все view требуют логина и прав пользования админкой. RULES-18.
  * Добавлена страница ролей пользователей на конкретном сервисе. RULES-12.
  * В базе хранится транслитерированное имя пользователя. RULES-15.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-11-01 18:08:23

0.1.10
---

  * Добавлен init скрипт для запуска celery.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-09-28 17:19:27

0.1.9
---

  * Добавлена опция FORCE\_SCRIPT\_NAME.
  * Исправлен скрипт импорта стаффа.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-09-27 18:36:52

0.1.8
---

  * Добавлены скрипты для простого запуска shell, dbshell и других команд.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-09-27 18:10:35

0.1.7
---

  * Добавлено сжатие js/css.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-09-27 17:50:09

0.1.6
---

  * Добавлен конфиг lighttpd.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-09-27 17:42:06

0.1.5
---

  * Удалены debug\_toolbar и django\_extensions из APPS.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-09-27 17:06:18

0.1.4
---

  * Исправлены настройки в devel конфиге.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-09-27 16:48:07

0.1.3
---

  * Поправлены настройки логгера.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-09-27 15:42:32

0.1.2
---

  * Добавлены уведомления о действиях.
  * Указание роли при ее удалении.
  * Отлажена система ретраев для задач и удаление роли в директе.
  * Кастомная валидация заменена на формочки.
  * Простой тест удаления роли.
  * Добавлен тест view добавления новой роли.
  * Обработка ошибок от директа.
  * Для ролей, сортировка по дате обновления.
  * Добавлено заведение Директового логина в паспорте.
  * Сделано человеческое отображение ролей. RULES-8.
  * Исправлены тесты.
  * Мелкие поправки.
  * Форма поиска перенесена в Lego шапку.
  * Move to LEGO 2.4
  * Добавлена леговаская верстка для шапки и футера.
  * Добавлен плагин для взаимодействия с Директом.
  * Добавлен buildout конфиг для разработки, с дополнительными библиотечками.
  * Настроено логирование, исправлен тестовый плагин, так что он теперь исправно
  * активирует роли.
  * Добавлена команда для иморта из LDAP. RULES-5.
  * Загрузка данных стаффа из файлов. RULES-3.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-09-27 15:14:43

0.1.1
---

  * Множество изменений.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2010-09-07 12:46:57
