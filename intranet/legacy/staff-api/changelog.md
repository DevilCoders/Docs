3.2.4
-----

[denis-p](http://staff/denis-p) 2020-10-06 12:50:36+03:00

3.2.3
-----

* [denis-p](http://staff/denis-p)

 * Use roles on high level fields                                             [ https://a.yandex-team.ru/arc_vcs/commit/7ee334081dbce4b7da0bc7d7175a9ba6ad642c0c ]
 * Formatting                                                                 [ https://a.yandex-team.ru/arc_vcs/commit/4433729e15dd67ca50ed83bed459a254cb70b23f ]
 * Fixes                                                                      [ https://a.yandex-team.ru/arc_vcs/commit/040cab2f02eb0cd7f2926f579a381640e0965588 ]
 * Added schemas with roles, generate patched again to build inside arcadia,  [ https://a.yandex-team.ru/arc_vcs/commit/0833d3daf626e40db891e4e5da794429d75a4f8c ]
 * Bring back file                                                            [ https://a.yandex-team.ru/arc_vcs/commit/7849ee4593d9945c79dcc7338a1300f72dece3e9 ]
 * Fix for idm, compile tests                                                 [ https://a.yandex-team.ru/arc_vcs/commit/a4c993389757182bcaa7e4b07d282a332776408d ]

* [gzuykov](http://staff/gzuykov)

 * vendor: bump github.com/go-chi/chi to v4.1.2  [ https://a.yandex-team.ru/arc/commit/7353513 ]

[denis-p](http://staff/denis-p) 2020-10-06 12:49:09+03:00

3.2.2
-----
 * STAFF-13824: [back] Формировать дерево ролей для IDM из jsonschema                               [ https://a.yandex-team.ru/arc/commit/7313938 ]

[aksenovma](http://staff/aksenovma) 2020-09-09 11:54:59+03:00

3.2.1
-----

[cracker](http://staff/cracker) 2020-08-26 11:10:27+03:00

3.2.0
-----
 * STAFF-13704: [back] Начать отдавать positions через новый стафф-апи  [ https://a.yandex-team.ru/arc/commit/7255537 ]

[cracker](http://staff/cracker) 2020-08-26 11:05:56+03:00

3.1.1
-----
 * STAFF-13774: [back] Запустить интеграцию с IDM  [ https://a.yandex-team.ru/arc/commit/7217098 ]

[aksenovma](http://staff/aksenovma) 2020-08-13 10:09:45+03:00

3.1.0
-----

* [aksenovma](http://staff/aksenovma)

 * STAFF-13449: Опечатка                                                        [ https://a.yandex-team.ru/arc_vcs/commit/4820f7cdf921e71b7326acf1881c3cbeadab94e0 ]
 * STAFF-13449: Закомментил TVM                                                 [ https://a.yandex-team.ru/arc_vcs/commit/234290985383b4761f05cf445f883dfa2b0e2be7 ]
 * STAFF-13449: Порядок импортов                                                [ https://a.yandex-team.ru/arc_vcs/commit/e0e6b1c87aeb370e7844923094e750b7131e4cb0 ]
 * STAFF-13449: Доработки по ревью                                              [ https://a.yandex-team.ru/arc_vcs/commit/a19b181844c50a711b1bde438533fee32b4ddd8b ]
 * STAFF-13449: Переделал обработку ошибок                                      [ https://a.yandex-team.ru/arc_vcs/commit/7f98f61e035850dc8a04d024c908e2fffddee3ab ]
 * STAFF-13449: Убрал настройки сертификата                                     [ https://a.yandex-team.ru/arc_vcs/commit/cbae7c24a1f1d21b3e5786821c6855265549779e ]
 * STAFF-13449: Улучшенная обработка ошибок, правильный логгер                  [ https://a.yandex-team.ru/arc_vcs/commit/8c434d009b2226714e8d79bc01457ea466714721 ]
 * STAFF-13449: InitDB методом, явная передача контекста, принимать только uid  [ https://a.yandex-team.ru/arc_vcs/commit/7624d9bca8d30edcc8753bdc056ee14a08f630f8 ]
 * STAFF-13449: Все креденшелы БД в секретнице + вытащить БД из конфига         [ https://a.yandex-team.ru/arc_vcs/commit/1a0ec53c3c4f5d6dd207ecfce60330924c765202 ]
 * STAFF-13449: Секреты из секретницы + небольшие доработки                     [ https://a.yandex-team.ru/arc_vcs/commit/391dbae86400bbf3eb95d52269e7cc5196130b20 ]
 * STAFF-13449: Доработки нейминга                                              [ https://a.yandex-team.ru/arc_vcs/commit/902a99e23c1fcc83ff8a07c5a27f369c00d6af1b ]
 * STAFF-13449: Убрал Монгу за интерфейс + различные доработки                  [ https://a.yandex-team.ru/arc_vcs/commit/9c0c189dc51db8eeaa3e60de8f544730f7cf7d76 ]
 * STAFF-13449: Fix                                                             [ https://a.yandex-team.ru/arc_vcs/commit/107f462bc357e59cdcf9f05c0abc9b6d303bf86b ]
 * STAFF-13449: Запросы в Монгу отдельными методами                             [ https://a.yandex-team.ru/arc_vcs/commit/d8b806ba11ca9aa5cd5c9ae538ac4accc3de61a2 ]
 * STAFF-13449: Валидация query-параметров                                      [ https://a.yandex-team.ru/arc_vcs/commit/3ed3740384d2b248eca7cc3ee39b3218e44da3c5 ]
 * STAFF-13449: Доработал ручки /add-role и /remove-role                        [ https://a.yandex-team.ru/arc_vcs/commit/9004f92b48edd1028e01c60cf8ad3ad96eb52b55 ]
 * STAFF-13449: Передалал ручку /get-all-roles                                  [ https://a.yandex-team.ru/arc_vcs/commit/f3e6d2512e96673590e348e02b9c11d0c47a285c ]
 * STAFF-13449: Всё остальное                                                   [ https://a.yandex-team.ru/arc_vcs/commit/384840f7bb96fe99662caa0257282074107c34d4 ]
 * STAFF-13449: Первая итерация                                                 [ https://a.yandex-team.ru/arc_vcs/commit/fc7f878510ad9a99143863f377708f3496031ee5 ]

* [cracker](http://staff/cracker)

 * STAFF-13444: [back] Настроить интеграцию с Паспортом  [ https://a.yandex-team.ru/arc/commit/7066872 ]

[aksenovma](http://staff/aksenovma) 2020-08-10 12:15:00+03:00

3.0.0
-----

* [cracker](http://staff/cracker)

 * Add releaser support                                              [ https://a.yandex-team.ru/arc/commit/6920957 ]

* [aksenovma](http://staff/aksenovma)

 * STAFF-13441: Add Dockerfile & related                                             [ https://a.yandex-team.ru/arc/commit/6920246 ]
 * DEVTOOLSUP-13685: Подключил проект к автосборке                                   [ https://a.yandex-team.ru/arc/commit/6917185 ]
 * PR from branch users/aksenovma/staff_api_initial

Заготовка для нового Staff-API  [ https://a.yandex-team.ru/arc/commit/6912211 ]

[cracker](http://staff/cracker) 2020-06-11 00:16:54+03:00

