2.369
-----
 * Revert "DISKBACK-252: correct change password"

This reverts commit dc768c6061d7cb5376478ae35f89e8c96633029b, reversing
changes made to 00794b48cd7ed7ee6b5185a6a43d53c71f359320.  [ https://a.yandex-team.ru/arc/commit/9791038 ]

[trushkin](http://staff/trushkin) 2022-07-29 13:52:51+03:00

2.368
-----

[trushkin](http://staff/trushkin) 2022-07-28 15:47:02+03:00

2.367
-----

* [trushkin](http://staff/trushkin)

 * DISKBACK-278: Force syncing organization if SSO become enabled

DISKBACK-278: Force syncing organization if SSO become enabled          [ https://a.yandex-team.ru/arc/commit/9785698 ]
 * DISKBACK-24: Exclude expired invites while limiting invite issuing

DISKBACK-24: Exclude expired invites while limiting invite issuing  [ https://a.yandex-team.ru/arc/commit/9783767 ]
 * Fix TestDomainList__get_6::test_wrong_fields_returned_by_list_view

Fix TestDomainList__get_6::test_wrong_fields_returned_by_list_view  [ https://a.yandex-team.ru/arc/commit/9783761 ]

* [sanya2013](http://staff/sanya2013)

 * DISKBACK-533: fix cloud graphics       [ https://a.yandex-team.ru/arc/commit/9784077 ]
 * DISKBACK-252: correct change password  [ https://a.yandex-team.ru/arc/commit/9783577 ]

* [smosker](http://staff/smosker)

 * CHEMODAN-85054 Использование локальных сертификатов при синке с облаком  [ https://a.yandex-team.ru/arc/commit/9783633 ]

[trushkin](http://staff/trushkin) 2022-07-28 15:22:12+03:00

2.366
-----

* [sanya2013](http://staff/sanya2013)

 * DISKBACK-533: cloud timeouts  [ https://a.yandex-team.ru/arc/commit/9766122 ]

[kozharin](http://staff/kozharin) 2022-07-25 13:56:30+03:00

2.365
-----

* [trushkin](http://staff/trushkin)

 * DISKBACK-65: Retry SyncSsoOrgTask

DISKBACK-65: Retry SyncSsoOrgTask  [ https://a.yandex-team.ru/arc/commit/9765730 ]

* [kozharin](http://staff/kozharin)

 * DISKBACK-99 Обновлять по диффам

fix(DISKBACK-99): обновлять по диффам, а не с нуля
Раньше сносилась вся табла, затем заново заполнялась данными. Теперь же высчитывается diff (на добавление и на удаление) и применяются операции из него
CLOSES: DISKBACK-99

test(DISKBACK-99): support for pydevd debug server

build(DISKBACK-99): скрипт по переносу пользователей  [ https://a.yandex-team.ru/arc/commit/9765626 ]

* [sanya2013](http://staff/sanya2013)

 * DISKBACK-289: fix locks logbroker  [ https://a.yandex-team.ru/arc/commit/9749317 ]

[kozharin](http://staff/kozharin) 2022-07-25 12:44:06+03:00

2.364
-----

[kozharin](http://staff/kozharin) 2022-07-12 18:02:40+03:00

2.363
-----
 * DISKBACK-140 Отключить крон джобу на check_organizations_balance_and_debt

chore(DISKBACK-140): stop `check_organizations_balance_and_debt` cron job  [ https://a.yandex-team.ru/arc/commit/9710263 ]

[kozharin](http://staff/kozharin) 2022-07-12 17:54:41+03:00

2.362
-----
 * DISKBACK-261: remove create all maillist auto  [ https://a.yandex-team.ru/arc/commit/9697811 ]

[sanya2013](http://staff/sanya2013) 2022-07-09 11:59:30+03:00

2.361
-----
 * CHEMODAN-84737: lb fixes  [ https://a.yandex-team.ru/arc/commit/9660169 ]

[sanya2013](http://staff/sanya2013) 2022-07-01 11:36:17+03:00

2.360
-----
 * CHEMODAN-84737: fixes  [ https://a.yandex-team.ru/arc/commit/9657426 ]

[sanya2013](http://staff/sanya2013) 2022-06-30 17:31:03+03:00

2.359
-----

* [sanya2013](http://staff/sanya2013)

 * CHEMODAN-84737: lb fixes  [ https://a.yandex-team.ru/arc/commit/9656203 ]

* [saku](http://staff/saku)

 * possible fix case when uid not in bb  [ https://a.yandex-team.ru/arc/commit/9644501 ]

[sanya2013](http://staff/sanya2013) 2022-06-30 15:18:53+03:00

2.358
-----

* [sanya2013](http://staff/sanya2013)

 * CHEMODAN-84631: fix get main connection  [ https://a.yandex-team.ru/arc/commit/9638999 ]
 * fix read lb                              [ https://a.yandex-team.ru/arc/commit/9572018 ]

* [saku](http://staff/saku)

 * full sync process CHEMODAN-83404  [ https://a.yandex-team.ru/arc/commit/9559901 ]

[sanya2013](http://staff/sanya2013) 2022-06-27 15:30:45+03:00

2.357
-----
 * CHEMODAN-84044: partner organizations  [ https://a.yandex-team.ru/arc/commit/9542889 ]

[sanya2013](http://staff/sanya2013) 2022-06-03 12:33:42+03:00

2.356
-----

[sanya2013](http://staff/sanya2013) 2022-06-02 15:19:41+03:00

2.355
-----

* [kis8ya](http://staff/kis8ya)

 * CHEMODAN-84150: updated test                            [ https://a.yandex-team.ru/arc/commit/9532181 ]
 * CHEMODAN-84150: increased MAX_LABEL_LENGTH (30 -> 100)  [ https://a.yandex-team.ru/arc/commit/9531736 ]

* [sanya2013](http://staff/sanya2013)

 * fix lb reader             [ https://a.yandex-team.ru/arc/commit/9524849 ]
 * New logic read logbroker  [ https://a.yandex-team.ru/arc/commit/9517350 ]

* [saku](http://staff/saku)

 * read data from logbroker endpoint with same DC               [ https://a.yandex-team.ru/arc/commit/9509566 ]
 * fix incorrect handling, separate users to domain and portal  [ https://a.yandex-team.ru/arc/commit/9509495 ]

[kis8ya](http://staff/kis8ya) 2022-06-01 16:15:37+03:00

2.354
-----

* [sanya2013](http://staff/sanya2013)

 * PR from branch users/sanya2013/CHEMODAN-83874-remove-sas-replica

CHEMODAN-83874: remove sas replica

CHEMODAN-83886: no old abook  [ https://a.yandex-team.ru/arc/commit/9504112 ]
 * CHEMODAN-83886: no old abook                                                                                                        [ https://a.yandex-team.ru/arc/commit/9504110 ]
 * CHEMODAN-83998: clean failed tasks                                                                                                  [ https://a.yandex-team.ru/arc/commit/9493200 ]
 * CHEMODAN-83815: fix sync user data                                                                                                  [ https://a.yandex-team.ru/arc/commit/9459003 ]

* [saku](http://staff/saku)

 * CHEMODAN-82654 unify logging, fix missing files in ya.make, fix exception problem, releaser.sh changes  [ https://a.yandex-team.ru/arc/commit/9474649 ]

[sanya2013](http://staff/sanya2013) 2022-05-26 12:11:26+03:00

2.353
-----
 * CHEMODAN-83815: fix sso for big org  [ https://a.yandex-team.ru/arc/commit/9458107 ]
 * CHEMODAN-83816: ignore enters sso    [ https://a.yandex-team.ru/arc/commit/9458098 ]
 * fix sso                              [ https://a.yandex-team.ru/arc/commit/9452878 ]

[sanya2013](http://staff/sanya2013) 2022-05-16 14:01:00+03:00

2.352
-----
 * CHEMODAN-83758

CHEMODAN-83465  [ https://a.yandex-team.ru/arc/commit/9450792 ]

[sanya2013](http://staff/sanya2013) 2022-05-13 13:14:50+03:00

2.351
-----

* [sanya2013](http://staff/sanya2013)

 * CHEMODAN-83313: fix analytic upload  [ https://a.yandex-team.ru/arc/commit/9415690 ]

* [saku](http://staff/saku)

 * CHEMODAN-82654 integrated logbroker concept  [ https://a.yandex-team.ru/arc/commit/9407178 ]

* [ivaninva](http://staff/ivaninva)

 * CHEMODAN-82696: Добавление ограничений на удаление последнего портального админа в SSO организации

add path and dissmis tests  [ https://a.yandex-team.ru/arc/commit/9406047 ]

[sanya2013](http://staff/sanya2013) 2022-04-29 16:03:02+03:00

2.350
-----
 * CHEMODAN-83491: fix sso email field  [ https://a.yandex-team.ru/arc/commit/9375781 ]

[sanya2013](http://staff/sanya2013) 2022-04-20 16:50:23+03:00

2.349
-----
 * CHEMODAN-83476: fix roles idm  [ https://a.yandex-team.ru/arc/commit/9371237 ]

[sanya2013](http://staff/sanya2013) 2022-04-20 13:26:45+03:00

2.348
-----

* [ivaninva](http://staff/ivaninva)

 * Добавление SSO запретов

add alias creation restriction  [ https://a.yandex-team.ru/arc/commit/9367651 ]

[sanya2013](http://staff/sanya2013) 2022-04-19 19:34:46+03:00

2.347
-----

[sanya2013](http://staff/sanya2013) 2022-04-14 16:13:55+03:00

2.346
-----

[sanya2013](http://staff/sanya2013) 2022-04-13 14:19:49+03:00

2.345
-----

* [sanya2013](http://staff/sanya2013)

 * CHEMODAN-82919: sync sso userinfo  [ https://a.yandex-team.ru/arc/commit/9345334 ]

* [ivaninva](http://staff/ivaninva)

 * CHEMODAN-82656: Добавление верификации изменений SSO пользователей

add sso validation in patch user  [ https://a.yandex-team.ru/arc/commit/9323957 ]

[sanya2013](http://staff/sanya2013) 2022-04-13 14:13:47+03:00

2.344
-----
 * CHEMODAN-83132: fix multiorg access  [ https://a.yandex-team.ru/arc/commit/9308979 ]
 * CHEMODAN-82440: remove billing       [ https://a.yandex-team.ru/arc/commit/9308161 ]

[sanya2013](http://staff/sanya2013) 2022-04-04 17:34:32+03:00

2.343
-----
 * CHEMODAN-82963: fix                      [ https://a.yandex-team.ru/arc/commit/9292934 ]
 * CHEMODAN-83063: fix                      [ https://a.yandex-team.ru/arc/commit/9292930 ]
 * CHEMODAN-82963: fix                      [ https://a.yandex-team.ru/arc/commit/9287991 ]
 * CHEMODAN-83063: domain id                [ https://a.yandex-team.ru/arc/commit/9287989 ]
 * CHEMODAN-83025: fix many dismiss users   [ https://a.yandex-team.ru/arc/commit/9287653 ]
 * CHEMODAN-82963: sso config conflict fix  [ https://a.yandex-team.ru/arc/commit/9287334 ]

[sanya2013](http://staff/sanya2013) 2022-03-30 22:35:56+03:00

2.342
-----

* [smosker](http://staff/smosker)

 * CHEMODAN-82731 Разбиваем постановку тасок синхронизации организаций на батчи  [ https://a.yandex-team.ru/arc/commit/9272952 ]

[sanya2013](http://staff/sanya2013) 2022-03-25 12:09:59+03:00

2.341
-----
 * CHEMODAN-82784: fix nickname save  [ https://a.yandex-team.ru/arc/commit/9272739 ]

[sanya2013](http://staff/sanya2013) 2022-03-25 11:28:56+03:00

2.340
-----

* [sanya2013](http://staff/sanya2013)

 * CHEMODAN-82888: disable create user on enable sso                 [ https://a.yandex-team.ru/arc/commit/9264761 ]
 * PR from branch users/sanya2013/CHEMODAN-82823-fix-enable-feature  [ https://a.yandex-team.ru/arc/commit/9261170 ]
 * CHEMODAN-82807                                                    [ https://a.yandex-team.ru/arc/commit/9261167 ]
 * CHEMODAN-82790                                                    [ https://a.yandex-team.ru/arc/commit/9261159 ]

* [dsamuylov](http://staff/dsamuylov)

 * ARCANUM-5510 prepare migration from .devexp.json to a.yaml (intranet)  [ https://a.yandex-team.ru/arc/commit/9231012 ]

[sanya2013](http://staff/sanya2013) 2022-03-23 16:56:00+03:00

2.339
-----

* [smosker](http://staff/smosker)

 * CHEMODAN-82540 Синхронизируем только облачные организации с вики/трекером + оптимизация  [ https://a.yandex-team.ru/arc/commit/9230146 ]

* [sanya2013](http://staff/sanya2013)

 * fix                                              [ https://a.yandex-team.ru/arc/commit/9224733 ]
 * CHEMODAN-82698: fix testing tasks                [ https://a.yandex-team.ru/arc/commit/9224401 ]
 * PSBTBSUP-1283: fix verify domain for cloud orgs  [ https://a.yandex-team.ru/arc/commit/9224397 ]
 * CHEMODAN-82658: users type field                 [ https://a.yandex-team.ru/arc/commit/9219683 ]

[sanya2013](http://staff/sanya2013) 2022-03-14 15:12:04+03:00

2.338
-----

[sanya2013](http://staff/sanya2013) 2022-03-09 18:17:52+03:00

2.337
-----
 * CHEMODAN-82520: fix dashboard tasks  [ https://a.yandex-team.ru/arc/commit/9215973 ]

[sanya2013](http://staff/sanya2013) 2022-03-09 18:04:08+03:00

2.336
-----

* [sanya2013](http://staff/sanya2013)

 * fix client_id field optional                    [ https://a.yandex-team.ru/arc/commit/9215219 ]
 * CHEMODAN-82327: disable sso on disable feature  [ https://a.yandex-team.ru/arc/commit/9191702 ]
 * CHEMODAN-82341: timeout balance                 [ https://a.yandex-team.ru/arc/commit/9191500 ]
 * CHEMODAN-82340

CHEMODAN-82325
CHEMODAN-82329   [ https://a.yandex-team.ru/arc/commit/9189130 ]
 * fix monitoring                                  [ https://a.yandex-team.ru/arc/commit/9170839 ]

* [shadchin](http://staff/shadchin)

 * IGNIETFERRO-1816 Switch on collections.abc  [ https://a.yandex-team.ru/arc/commit/9166143 ]

[sanya2013](http://staff/sanya2013) 2022-03-09 15:38:39+03:00

2.335
-----

[sanya2013](http://staff/sanya2013) 2022-02-18 10:15:44+03:00

2.334
-----

* [sanya2013](http://staff/sanya2013)

 * CHEMODAN-82051: sso sync monitoring                           [ https://a.yandex-team.ru/arc/commit/9157356 ]
 * CHEMODAN-82047

CHEMODAN-82048
CHEMODAN-82049
CHEMODAN-82050  [ https://a.yandex-team.ru/arc/commit/9154903 ]
 * CHEMODAN-82052: event delay monitoring                        [ https://a.yandex-team.ru/arc/commit/9153444 ]

* [maratik](http://staff/maratik)

 * feat: startrek integration for DIR ARCANUM-5357

feat: startrek integration  [ https://a.yandex-team.ru/arc/commit/9150865 ]

[sanya2013](http://staff/sanya2013) 2022-02-17 18:02:53+03:00

2.333
-----
 * CHEMODAN-82047

CHEMODAN-82048
CHEMODAN-82049
CHEMODAN-82050  [ https://a.yandex-team.ru/arc/commit/9146148 ]

[sanya2013](http://staff/sanya2013) 2022-02-15 14:11:50+03:00

2.332
-----

* [sanya2013](http://staff/sanya2013)

 * PR from branch users/sanya2013/CHEMODAN-82024-fix-event-notification-task  [ https://a.yandex-team.ru/arc/commit/9106977 ]
 * CHEMODAN-82011: remove sensetive logger                                    [ https://a.yandex-team.ru/arc/commit/9104990 ]

* [maratik](http://staff/maratik)

 * Revert commit r9099804                                                       [ https://a.yandex-team.ru/arc/commit/9100100 ]
 * feat: startrek integration for DIR ARCANUM-5357

feat: startrek integration  [ https://a.yandex-team.ru/arc/commit/9099804 ]

* [shadchin](http://staff/shadchin)

 * Switch requests on charset-normalizer  [ https://a.yandex-team.ru/arc/commit/9064108 ]

[sanya2013](http://staff/sanya2013) 2022-02-04 11:01:07+03:00

2.331
-----

* [sanya2013](http://staff/sanya2013)

 * CHEMODAN-81584: fix maillists check many   [ https://a.yandex-team.ru/arc/commit/9029805 ]
 * CHEMODAN-81563: disable trial on all orgs  [ https://a.yandex-team.ru/arc/commit/9029798 ]

* [thegeorg](http://staff/thegeorg)

 * protobuf: Move python runtime to contrib/python

Split  protobuf runtime into py2 and py3.

Make svn hook happy: DTCC-661  [ https://a.yandex-team.ru/arc/commit/9022477 ]

[sanya2013](http://staff/sanya2013) 2022-01-14 00:25:59+03:00

2.330
-----

[sanya2013](http://staff/sanya2013) 2021-12-06 16:19:16+03:00

2.329
-----
 * Change "user_inconsistencies.py"  [ https://a.yandex-team.ru/arc/commit/8903921 ]

[friendlyevil](http://staff/friendlyevil) 2021-12-04 15:15:41+03:00

2.328
-----
 * CHEMODAN-80752: fix equals password bug  [ https://a.yandex-team.ru/arc/commit/8900845 ]
 * CHEMODAN-80960: save meta info           [ https://a.yandex-team.ru/arc/commit/8900551 ]

[sanya2013](http://staff/sanya2013) 2021-12-03 14:25:45+03:00

2.327
-----
 * CHEMODAN-80952: fix sync cloud orgs task  [ https://a.yandex-team.ru/arc/commit/8889061 ]

[sanya2013](http://staff/sanya2013) 2021-11-30 19:21:21+03:00

2.326
-----
 * CHEMODAN-80814: fix yt upload disable tracker  [ https://a.yandex-team.ru/arc/commit/8862697 ]

[sanya2013](http://staff/sanya2013) 2021-11-23 13:39:03+03:00

2.325
-----
 * CHEMODAN-79650: fix security bug invite tld  [ https://a.yandex-team.ru/arc/commit/8829869 ]

[sanya2013](http://staff/sanya2013) 2021-11-16 12:03:31+03:00

2.324
-----

[sanya2013](http://staff/sanya2013) 2021-11-15 13:48:15+03:00

2.323
-----
 * CHEMODAN-80122: fix sync passport userdata  [ https://a.yandex-team.ru/arc/commit/8771448 ]
 * CHEMODAN-79964: flag billing tracker        [ https://a.yandex-team.ru/arc/commit/8769394 ]

[sanya2013](http://staff/sanya2013) 2021-10-26 17:06:51+03:00

2.322
-----
 * CHEMODAN-80407: return sync passport users  [ https://a.yandex-team.ru/arc/commit/8760021 ]

[sanya2013](http://staff/sanya2013) 2021-10-22 14:46:56+03:00

2.321
-----
 * CHEMODAN-79928 fixup logrotate  [ https://a.yandex-team.ru/arc/commit/8752692 ]

[vadzay](http://staff/vadzay) 2021-10-20 18:38:30+03:00

2.320
-----

[sanya2013](http://staff/sanya2013) 2021-10-19 15:19:28+03:00

2.319
-----

[sanya2013](http://staff/sanya2013) 2021-10-19 13:26:52+03:00

2.318
-----

[sanya2013](http://staff/sanya2013) 2021-10-19 12:23:36+03:00

2.317
-----

[sanya2013](http://staff/sanya2013) 2021-10-19 12:19:18+03:00

2.316
-----
 * CHEMODAN-80346: rps graphics                                                 [ https://a.yandex-team.ru/arc/commit/8746436 ]
 * PR from branch users/sanya2013/CHEMODAN-80353-fix-sync-cloud-orgs-scheduler  [ https://a.yandex-team.ru/arc/commit/8744556 ]

[sanya2013](http://staff/sanya2013) 2021-10-19 10:58:08+03:00

2.315
-----
 * CHEMODAN-80274: add nginx logrotate  [ https://a.yandex-team.ru/arc/commit/8734658 ]

[zero-ger](http://staff/zero-ger) 2021-10-14 15:49:04+03:00

2.314
-----
 * CHEMODAN-80274: logrotate run every hour  [ https://a.yandex-team.ru/arc/commit/8727708 ]

[zero-ger](http://staff/zero-ger) 2021-10-14 13:59:28+03:00

2.313
-----
 * CHEMODAN-79928 yet another fix...  [ https://a.yandex-team.ru/arc/commit/8707671 ]

[vadzay](http://staff/vadzay) 2021-10-06 16:58:03+03:00

2.312
-----
 * CHEMODAN-79928 fix nginx error log parser perl script  [ https://a.yandex-team.ru/arc/commit/8707439 ]

[vadzay](http://staff/vadzay) 2021-10-06 16:17:28+03:00

2.311
-----

* [vadzay](http://staff/vadzay)

 * PR from branch users/vadzay/CHEMODAN-79928

CHEMODAN-79928 LF and LSh configs

CHEMODAN-79928 - use Bionic instead of Debian 10 for directory + fix push-client config

CHEMODAN-79928 - add tskv log for nginx, add puch-client config, install correct nginx version  [ https://a.yandex-team.ru/arc/commit/8699142 ]

[zero-ger](http://staff/zero-ger) 2021-10-06 12:49:04+03:00

2.310
-----
 * CHEMODAN-79983: bulk search domains          [ https://a.yandex-team.ru/arc/commit/8687521 ]
 * CHEMODAN-80066: fix checkmaillists tasks     [ https://a.yandex-team.ru/arc/commit/8686973 ]
 * CHEMODAN-8003: nginx max-client-body is 8mb  [ https://a.yandex-team.ru/arc/commit/8686972 ]

[sanya2013](http://staff/sanya2013) 2021-09-30 15:18:21+03:00

2.309
-----

[sanya2013](http://staff/sanya2013) 2021-09-24 16:16:06+03:00

2.308
-----

[sanya2013](http://staff/sanya2013) 2021-09-24 15:18:59+03:00

2.307
-----

[sanya2013](http://staff/sanya2013) 2021-09-24 15:10:51+03:00

2.306
-----
 * PSBTBSUP-936: fix cloud organization change admin  [ https://a.yandex-team.ru/arc/commit/8665453 ]
 * CHEMODAN-78716: fix bugs                           [ https://a.yandex-team.ru/arc/commit/8665447 ]

[sanya2013](http://staff/sanya2013) 2021-09-24 12:12:05+03:00

2.305
-----

[sanya2013](http://staff/sanya2013) 2021-09-23 18:58:26+03:00

2.304
-----
 * CHEMODAN-79716: new graphics by shards            [ https://a.yandex-team.ru/arc/commit/8660510 ]
 * CHEMODAN-79645: kill scheduler wait finish tasks  [ https://a.yandex-team.ru/arc/commit/8660507 ]

[sanya2013](http://staff/sanya2013) 2021-09-23 12:01:18+03:00

2.303
-----

[sanya2013](http://staff/sanya2013) 2021-09-22 13:02:14+03:00

2.302
-----
 * CHEMODAN-79493: get userinfo from blackbox  [ https://a.yandex-team.ru/arc/commit/8655966 ]

[sanya2013](http://staff/sanya2013) 2021-09-22 12:41:07+03:00

2.301
-----

[sanya2013](http://staff/sanya2013) 2021-09-21 13:09:06+03:00

2.300
-----
 * CHEMODAN-79911: fail event notification chunk duplicated task  [ https://a.yandex-team.ru/arc/commit/8650925 ]

[sanya2013](http://staff/sanya2013) 2021-09-21 11:41:02+03:00

2.299
-----
 * CHEMODAN-79721: up scheduled workers  [ https://a.yandex-team.ru/arc/commit/8614936 ]

[sanya2013](http://staff/sanya2013) 2021-09-10 14:58:09+03:00

2.298
-----

[sanya2013](http://staff/sanya2013) 2021-09-08 15:42:05+03:00

2.297
-----

[sanya2013](http://staff/sanya2013) 2021-09-08 13:05:12+03:00

2.296
-----

[sanya2013](http://staff/sanya2013) 2021-09-07 20:31:14+03:00

2.295
-----
 * CHEMODAN-79498: new deploy script  [ https://a.yandex-team.ru/arc/commit/8603200 ]

[sanya2013](http://staff/sanya2013) 2021-09-07 20:23:34+03:00

2.294
-----

[sanya2013](http://staff/sanya2013) 2021-09-06 14:06:37+03:00

2.293
-----
 * CHEMODAN-79492: fix check maillists scheduler  [ https://a.yandex-team.ru/arc/commit/8595906 ]

[sanya2013](http://staff/sanya2013) 2021-09-06 12:29:00+03:00

2.292
-----

[sanya2013](http://staff/sanya2013) 2021-08-31 15:41:21+03:00

2.291
-----

* [sanya2013](http://staff/sanya2013)

 * CHEMODAN-79501: fix test disk address'  [ https://a.yandex-team.ru/arc/commit/8572227 ]

* [vadzay](http://staff/vadzay)

 * CHEMODAN-78913 setup logshatter and add push-client to docker image  [ https://a.yandex-team.ru/arc/commit/8566170 ]

[sanya2013](http://staff/sanya2013) 2021-08-30 16:26:55+03:00

2.290
-----

[sanya2013](http://staff/sanya2013) 2021-08-27 14:59:57+03:00

2.289
-----

[sanya2013](http://staff/sanya2013) 2021-08-27 13:16:08+03:00

2.288
-----
 * CHEMODAN-78906: fix failed tasks part 3  [ https://a.yandex-team.ru/arc/commit/8561724 ]

[sanya2013](http://staff/sanya2013) 2021-08-26 15:52:15+03:00

2.287
-----

[sanya2013](http://staff/sanya2013) 2021-08-26 12:24:16+03:00

2.286
-----

[sanya2013](http://staff/sanya2013) 2021-08-26 12:18:19+03:00

2.285
-----

[sanya2013](http://staff/sanya2013) 2021-08-25 19:20:59+03:00

2.284
-----
 * CHEMODAN-79367: scheduler lock fix       [ https://a.yandex-team.ru/arc/commit/8556939 ]
 * CHEMODAN-78906: fix                      [ https://a.yandex-team.ru/arc/commit/8556935 ]
 * CHEMODAN-78906: fix failed tasks part 1  [ https://a.yandex-team.ru/arc/commit/8554753 ]

[sanya2013](http://staff/sanya2013) 2021-08-25 14:25:47+03:00

2.283
-----
 * DIR-9892: Не требуем org_id и user-a в ручке обработки события  [ https://a.yandex-team.ru/arc/commit/8549829 ]

[uruz](http://staff/uruz) 2021-08-23 18:05:51+03:00

2.282
-----
 * CHEMODAN-79160: event notification subtasks  [ https://a.yandex-team.ru/arc/commit/8548367 ]
 * CHEMODAN-78697: cron tasks monitoring        [ https://a.yandex-team.ru/arc/commit/8548366 ]

[sanya2013](http://staff/sanya2013) 2021-08-23 13:25:26+03:00

2.281
-----

[sanya2013](http://staff/sanya2013) 2021-08-19 12:25:03+03:00

2.280
-----

* [sanya2013](http://staff/sanya2013)

 * CHEMODAN-78697: cron tasks monitoring  [ https://a.yandex-team.ru/arc/commit/8535602 ]

* [uruz](http://staff/uruz)

 * DIR-9892: Правки 3 по отказу от bbemu  [ https://a.yandex-team.ru/arc/commit/8534495 ]

[sanya2013](http://staff/sanya2013) 2021-08-18 19:07:32+03:00

2.279
-----

* [uruz](http://staff/uruz)

 * DIR-9892: Правки по отказу от bbemu  [ https://a.yandex-team.ru/arc/commit/8533228 ]

[sanya2013](http://staff/sanya2013) 2021-08-18 12:08:52+03:00

2.278
-----

* [uruz](http://staff/uruz)

 * DIR-9892: Отказаться от bbemu  [ https://a.yandex-team.ru/arc/commit/8530168 ]

* [sanya2013](http://staff/sanya2013)

 * CHEMODAN-78842: sync tracker bug  [ https://a.yandex-team.ru/arc/commit/8529767 ]

[sanya2013](http://staff/sanya2013) 2021-08-17 15:38:21+03:00

2.277
-----

[sanya2013](http://staff/sanya2013) 2021-08-10 19:26:57+03:00

2.276
-----

[sanya2013](http://staff/sanya2013) 2021-08-10 19:25:19+03:00

2.275
-----
 * CHEMODAN-79805: nginx underscores headers  [ https://a.yandex-team.ru/arc/commit/8508242 ]

[sanya2013](http://staff/sanya2013) 2021-08-10 19:06:52+03:00

2.274
-----

[sanya2013](http://staff/sanya2013) 2021-08-06 15:22:30+03:00

2.273
-----

[sanya2013](http://staff/sanya2013) 2021-08-06 15:20:51+03:00

2.272
-----
 * CHEMODAN-78905: service statistic  [ https://a.yandex-team.ru/arc/commit/8494826 ]

[sanya2013](http://staff/sanya2013) 2021-08-06 14:57:44+03:00

2.271
-----

[sanya2013](http://staff/sanya2013) 2021-08-04 15:13:19+03:00

2.270
-----

[sanya2013](http://staff/sanya2013) 2021-08-04 13:44:13+03:00

2.269
-----

[sanya2013](http://staff/sanya2013) 2021-08-03 20:20:17+03:00

2.268
-----

[sanya2013](http://staff/sanya2013) 2021-08-03 20:18:35+03:00

2.267
-----

[sanya2013](http://staff/sanya2013) 2021-08-03 20:07:52+03:00

2.266
-----

[sanya2013](http://staff/sanya2013) 2021-08-03 20:05:11+03:00

2.265
-----
 * CHEMODAN-78903: fix build  [ https://a.yandex-team.ru/arc/commit/8484272 ]

[sanya2013](http://staff/sanya2013) 2021-08-03 19:39:33+03:00

2.264
-----

[sanya2013](http://staff/sanya2013) 2021-08-03 14:27:02+03:00

2.263
-----

[sanya2013](http://staff/sanya2013) 2021-07-30 17:53:54+03:00

2.262
-----

[sanya2013](http://staff/sanya2013) 2021-07-30 17:46:54+03:00

2.261
-----

[sanya2013](http://staff/sanya2013) 2021-07-30 17:19:19+03:00

2.260
-----

[sanya2013](http://staff/sanya2013) 2021-07-30 16:46:56+03:00

2.259
-----

[sanya2013](http://staff/sanya2013) 2021-07-30 16:45:34+03:00

2.258
-----
 * CHEMODAN-78696: correct logging  [ https://a.yandex-team.ru/arc/commit/8473087 ]

[sanya2013](http://staff/sanya2013) 2021-07-30 16:22:43+03:00

2.257
-----
 * CHEMODAN-78696: fix ycrid task  [ https://a.yandex-team.ru/arc/commit/8472619 ]

[sanya2013](http://staff/sanya2013) 2021-07-30 15:01:47+03:00

2.256
-----

[sanya2013](http://staff/sanya2013) 2021-07-30 13:25:59+03:00

2.255
-----

[sanya2013](http://staff/sanya2013) 2021-07-30 13:08:22+03:00

2.254
-----
 * PR from branch users/sanya2013/CHEMODAN-78696-correct-logging

CHEMODAN-78696: correct logging  [ https://a.yandex-team.ru/arc/commit/8471706 ]
 * CHEMODAN-78852: standalone connect release                                                      [ https://a.yandex-team.ru/arc/commit/8463155 ]

[sanya2013](http://staff/sanya2013) 2021-07-30 12:22:03+03:00

2.253
-----

[sanya2013](http://staff/sanya2013) 2021-07-27 22:32:15+03:00

2.252
-----

[sanya2013](http://staff/sanya2013) 2021-07-27 22:08:59+03:00

2.251
-----

* [shadchin](http://staff/shadchin)

 * Update pgcli from 3.0.0 to 3.1.0  [ https://a.yandex-team.ru/arc/commit/8442122 ]

[sanya2013](http://staff/sanya2013) 2021-07-26 15:38:38+03:00

2.250
-----
 * DIR-10376: Правка условия  [ https://a.yandex-team.ru/arc/commit/8437438 ]

[uruz](http://staff/uruz) 2021-07-20 20:46:20+03:00

2.249
-----
 * DIR-10376: [Вики, Трекер] отключить подключение при создании организации  [ https://a.yandex-team.ru/arc/commit/8437069 ]

[uruz](http://staff/uruz) 2021-07-20 19:00:07+03:00

2.248
-----

[uruz](http://staff/uruz) 2021-07-13 14:09:09+03:00

2.247
-----
 * DIR-10335: Добавил зависимость от claimservice  [ https://a.yandex-team.ru/arc/commit/8403807 ]

[uruz](http://staff/uruz) 2021-07-09 19:47:22+03:00

2.246
-----
 * DIR-10333: Ручка для проставления cloud_org_id в организации Коннекта  [ https://a.yandex-team.ru/arc_vcs/commit/cd2ecc468dc30f7140200ebd128cb817cae78c3a ]

[uruz](http://staff/uruz) 2021-07-09 15:39:54+03:00

2.245
-----
 * DIR-10364: Снять ограничение на дублирующиеся почты для облачных пользователей облачных огранизаций  [ https://a.yandex-team.ru/arc/commit/8385834 ]

[uruz](http://staff/uruz) 2021-07-07 19:07:51+03:00

2.244
-----
 * DIR-10326: Ошибки получения tvm2 тикета  [ https://a.yandex-team.ru/arc/commit/8384979 ]

[uruz](http://staff/uruz) 2021-07-07 16:18:13+03:00

2.243
-----
 * Убираем из сборки screen                                                                                                 [ https://a.yandex-team.ru/arc/commit/8361843 ]
 * DIR-10123: Исправляю генерацию документации

Перенес файлы документации в проект, в том числе и автогенерируемые файлы.  [ https://a.yandex-team.ru/arc/commit/8361826 ]

[kdunaev](http://staff/kdunaev) 2021-07-02 17:04:30+03:00

2.242
-----
 * DIR-10346: Отключить отправку писем после создания доменных пользователей  [ https://a.yandex-team.ru/arc/commit/8361326 ]
 * DIR-10351: Падает синхронизация в организации Яндекс                       [ https://a.yandex-team.ru/arc/commit/8361323 ]

[uruz](http://staff/uruz) 2021-07-02 15:25:32+03:00

2.241
-----

* [uruz](http://staff/uruz)

 * DIR-10348: Выгрузили в yt запись с пустым client_id  [ https://a.yandex-team.ru/arc/commit/8355772 ]

[kdunaev](http://staff/kdunaev) 2021-07-01 13:53:35+03:00

2.240
-----

* [uruz](http://staff/uruz)

 * DIR-10326: Ошибки получения tvm2 тикета  [ https://a.yandex-team.ru/arc/commit/8350009 ]

* [shadchin](http://staff/shadchin)

 * IGNIETFERRO-1154 Rename contrib/python/apscheduler to contrib/python/APScheduler  [ https://a.yandex-team.ru/arc/commit/8344932 ]
 * IGNIETFERRO-1154 Rename contrib/python/twiggy to contrib/python/Twiggy            [ https://a.yandex-team.ru/arc/commit/8344818 ]

[kdunaev](http://staff/kdunaev) 2021-06-29 14:42:56+03:00

2.239
-----
 * DIR-10123: Копируем bashrc в /root  [ https://a.yandex-team.ru/arc/commit/8331823 ]

[kdunaev](http://staff/kdunaev) 2021-06-25 14:58:23+03:00

2.238
-----
 * DIR-10123: Удаляем таску read_from_domenator_logbroker

Решили удалить таску, не исправляя ее.  [ https://a.yandex-team.ru/arc/commit/8331071 ]

[kdunaev](http://staff/kdunaev) 2021-06-25 12:11:52+03:00

2.237
-----

* [kdunaev](http://staff/kdunaev)

 * DIR-10123: Меняем iva на man в шардах бд тестинга  [ https://a.yandex-team.ru/arc/commit/8327322 ]
 * DIR-10123: Скрипты для выкатки в деплой            [ https://a.yandex-team.ru/arc/commit/8327014 ]

* [uruz](http://staff/uruz)

 * DIR-10334: Попытка починить тесты  [ https://a.yandex-team.ru/arc/commit/8326087 ]
 * DIR-10324: Скрипты выгрузок        [ https://a.yandex-team.ru/arc/commit/8322117 ]

[kdunaev](http://staff/kdunaev) 2021-06-24 12:33:50+03:00

2.236
-----

* [kdunaev](http://staff/kdunaev)

 * DIR-10123: Перевезти directory

Заменил кулаудные переменные окружения на деплойные.  [ https://a.yandex-team.ru/arc/commit/8318557 ]

[uruz](http://staff/uruz) 2021-06-21 18:04:42+03:00

2.235
-----
 * DIR-10325: В org_ids пользователя должны быть все организации, если он пришёл с двумя заголовками  [ https://a.yandex-team.ru/arc/commit/8277714 ]

[uruz](http://staff/uruz) 2021-06-18 17:22:36+03:00

2.234
-----
 * DIR-10325: Сохраняем cloud_uid для необлачного режима                            [ https://a.yandex-team.ru/arc/commit/8277028 ]
 * DIR-10324: Выгрузить контактные данные по списку ушедших из Трекера организаций  [ https://a.yandex-team.ru/arc/commit/8276995 ]

[uruz](http://staff/uruz) 2021-06-18 15:25:10+03:00

2.233
-----
 * DIR-10325: Ещё один фикс для двух заголовков  [ https://a.yandex-team.ru/arc/commit/8275065 ]

[uruz](http://staff/uruz) 2021-06-17 22:48:04+03:00

2.232
-----
 * DIR-10325: Ещё один фикс для двух заголовков  [ https://a.yandex-team.ru/arc/commit/8274077 ]

[uruz](http://staff/uruz) 2021-06-17 18:42:14+03:00

2.231
-----
 * DIR-10086: Переезд в redis из consul/memcache  [ https://a.yandex-team.ru/arc/commit/8267508 ]

[uruz](http://staff/uruz) 2021-06-15 19:19:46+03:00

2.230
-----
 * DIR-10228: [Облако] Синк лицензий Трекера  [ https://a.yandex-team.ru/arc/commit/8267451 ]

[uruz](http://staff/uruz) 2021-06-15 18:47:56+03:00

2.229
-----
 * DIR-10259: [ЯОрг] не удалять доменных пользователей сразу  [ https://a.yandex-team.ru/arc/commit/8261373 ]

[uruz](http://staff/uruz) 2021-06-11 20:35:06+03:00

2.228
-----
 * DIR-10304: Упрощаю работу с коннекшенами  [ https://a.yandex-team.ru/arc/commit/8260901 ]

[uruz](http://staff/uruz) 2021-06-11 18:19:56+03:00

2.227
-----
 * DIR-10304: Обновляем cloud_uid в метабазе  [ https://a.yandex-team.ru/arc/commit/8260309 ]

[uruz](http://staff/uruz) 2021-06-11 16:02:00+03:00

2.226
-----
 * DIR-10304: Починить создание пользователя на лету с двумя заголовками  [ https://a.yandex-team.ru/arc/commit/8257103 ]

[uruz](http://staff/uruz) 2021-06-10 17:30:10+03:00

2.225
-----
 * DIR-10117: [GoZora] connect переезд на GoZoRa        [ https://a.yandex-team.ru/arc/commit/8252777 ]
 * DIR-10316: Сделать скрипт выгрузки uid-ов по org_id  [ https://a.yandex-team.ru/arc/commit/8252307 ]

[uruz](http://staff/uruz) 2021-06-09 15:56:54+03:00

2.224
-----
 * DIR-10298: Добавить логов при ошибке создания пользователя на лету  [ https://a.yandex-team.ru/arc/commit/8228729 ]

[uruz](http://staff/uruz) 2021-06-01 16:02:47+03:00

2.223
-----
 * DIR-10279: Убираю begin_nested в delay  [ https://a.yandex-team.ru/arc/commit/8204022 ]

[uruz](http://staff/uruz) 2021-05-27 17:14:21+03:00

2.222
-----
 * DIR-10279: Делаю ручку идемпотентной по умолчанию  [ https://a.yandex-team.ru/arc/commit/8201455 ]

[uruz](http://staff/uruz) 2021-05-26 19:47:16+03:00

2.221
-----
 * DIR-10280: Поменять 500 на 400 в ручке organizations-by-uids  [ https://a.yandex-team.ru/arc/commit/8199757 ]

[uruz](http://staff/uruz) 2021-05-26 14:05:37+03:00

2.220
-----

[uruz](http://staff/uruz) 2021-05-25 14:56:33+03:00

2.219
-----

[uruz](http://staff/uruz) 2021-05-24 20:16:47+03:00

2.218
-----

[uruz](http://staff/uruz) 2021-05-21 15:49:12+03:00

2.217
-----

[uruz](http://staff/uruz) 2021-05-21 14:47:40+03:00

2.216
-----

* [uruz](http://staff/uruz)

 * DIR-10130: Фикс для x-cloud-uid  [ https://a.yandex-team.ru/arc/commit/8187078 ]

* [thegeorg](http://staff/thegeorg)

 * Fix typo  [ https://a.yandex-team.ru/arc/commit/8186788 ]

[uruz](http://staff/uruz) 2021-05-21 13:58:19+03:00

2.215
-----

[uruz](http://staff/uruz) 2021-05-19 17:32:43+03:00

2.214
-----

[uruz](http://staff/uruz) 2021-05-19 17:18:32+03:00

2.213
-----
 * DIR-10130: Фикс тестов  [ https://a.yandex-team.ru/arc/commit/8178025 ]

[uruz](http://staff/uruz) 2021-05-18 19:26:08+03:00

2.212
-----
 * DIR-10130: Правка забытого места для создания паспортных пользователей на лету  [ https://a.yandex-team.ru/arc/commit/8174864 ]

[uruz](http://staff/uruz) 2021-05-17 20:13:23+03:00

2.211
-----
 * DIR-10130: Создание паспортных пользователей на лету  [ https://a.yandex-team.ru/arc/commit/8173147 ]

[uruz](http://staff/uruz) 2021-05-17 14:00:59+03:00

2.210
-----

[uruz](http://staff/uruz) 2021-04-29 20:27:52+03:00

2.209
-----
 * DIR-10236: Замедление работы коннекта  [ https://a.yandex-team.ru/arc/commit/8121382 ]

[uruz](http://staff/uruz) 2021-04-29 20:24:51+03:00

2.208
-----

* [smosker](http://staff/smosker)

 * DIR-10236 Снижение количества запросов в ручке domains/  [ https://a.yandex-team.ru/arc/commit/8110754 ]

[uruz](http://staff/uruz) 2021-04-26 20:00:42+03:00

2.207
-----

* [smosker](http://staff/smosker)

 * DIR-10233 ускорение ручки v6/groups  [ https://a.yandex-team.ru/arc/commit/8110050 ]

* [exprmntr](http://staff/exprmntr)

 * DEVTOOLS-7781 - remove NO_LINT()

DEVTOOLS-7781

<!-- DEVEXP BEGIN -->
\****
![review](https://codereview.in.yandex-team.ru/badges/review-in_progress-yellow.svg) [![rinatous](https://codereview.in.yandex-team.ru/badges/rinatous-...-yellow.svg)](https://staff.yandex-team.ru/rinatous)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/8107744 ]
 * DEVTOOLS-7781 - remove NO_LINT()

DEVTOOLS-7781                                                                                                                                                                                                                                                                 [ https://a.yandex-team.ru/arc/commit/8097952 ]

[uruz](http://staff/uruz) 2021-04-26 17:14:57+03:00

2.206
-----
 * DIR-10214 Запрет балкового обновления групп для nur.kz  [ https://a.yandex-team.ru/arc/commit/8082121 ]

[smosker](http://staff/smosker) 2021-04-16 12:27:38+03:00

2.205
-----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-10199: Поправить синк имени облачных пользователей(2)  [ https://a.yandex-team.ru/arc/commit/8075246 ]

* [shadchin](http://staff/shadchin)

 * Fix tests yandex_directory with new cachetools  [ https://a.yandex-team.ru/arc/commit/8075141 ]

[oleglarionov](http://staff/oleglarionov) 2021-04-14 13:11:58+03:00

2.204
-----

* [uruz](http://staff/uruz)

 * DIR-10138: Перейти на новую протоспеку Я.Орга  [ https://a.yandex-team.ru/arc/commit/8075061 ]

[oleglarionov](http://staff/oleglarionov) 2021-04-14 12:28:13+03:00

2.203
-----
 * DIR-10199: Поправить синк имени облачных пользователей  [ https://a.yandex-team.ru/arc/commit/8071653 ]

[oleglarionov](http://staff/oleglarionov) 2021-04-13 12:32:30+03:00

2.202
-----
 * DIR-10192: Снять ограничения по длине логина для федеративных пользователей  [ https://a.yandex-team.ru/arc/commit/8064804 ]

[uruz](http://staff/uruz) 2021-04-09 18:49:30+03:00

2.201
-----
 * PR from branch users/uruz/feature/DIR-100086-revert

Revert "DIR-10086: Переезд в redis из consul/memcache"
This reverts commit ca731113e7ce595df3d2c7ebb7dec2aa09b6a7a3, reversing
changes made to 1c2592fb7217d52505494fd088264a95d423c044.

Revert "releasing version 2.201"
This reverts commit d587854aee5b4a75ddd0fb4f22e8c2a638a0787b, reversing
changes made to 4e873f43b3d2481d9ac4726011eb9f068676ec3c.  [ https://a.yandex-team.ru/arc/commit/8064782 ]
 * releasing version 2.201                                                                                                                                                                                                                                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/8064081 ]
 * DIR-10086: Переезд в redis из consul/memcache                                                                                                                                                                                                                                                                                                                                                                      [ https://a.yandex-team.ru/arc/commit/8063795 ]

[uruz](http://staff/uruz) 2021-04-09 18:43:38+03:00

2.200
-----
 * DIR-10166: Создавать пользователя на лету всегда сразу с cloud_uid  [ https://a.yandex-team.ru/arc/commit/8040934 ]

[uruz](http://staff/uruz) 2021-04-01 15:37:14+03:00

2.199
-----
 * DIR-10097: Не падать в таске SaveBillingInfoToYTTask при отсутствии биллинговой инфы у одной из организаций  [ https://a.yandex-team.ru/arc/commit/8039568 ]

[oleglarionov](http://staff/oleglarionov) 2021-04-01 10:24:29+03:00

2.198
-----
 * DIR-10154: Ускоряю build_email  [ https://a.yandex-team.ru/arc/commit/8038534 ]

[uruz](http://staff/uruz) 2021-03-31 20:38:28+03:00

2.197
-----
 * DIR-10042: Убрать триал для облачных организаций  [ https://a.yandex-team.ru/arc/commit/8032794 ]

[oleglarionov](http://staff/oleglarionov) 2021-03-30 13:18:52+03:00

2.196
-----
 * DIR-9924: Поднять новое окружение Доменатроа для препрода ( integration-qa )  [ https://a.yandex-team.ru/arc/commit/8028635 ]
 * DIR-9924: Поднять новое окружение Доменатроа для препрода ( integration-qa )  [ https://a.yandex-team.ru/arc/commit/7997435 ]

[oleglarionov](http://staff/oleglarionov) 2021-03-29 14:41:24+03:00

2.195
-----
 * DIR-10055: [Трекер] перевести на cloud_notify ещё 3 рассылки  [ https://a.yandex-team.ru/arc/commit/7993915 ]

[uruz](http://staff/uruz) 2021-03-25 13:38:16+03:00

2.194
-----
 * PR from branch users/uruz/feature/DIR-9800

DIR-9800: Читаем из LB

DIR-9800: Комментарий

DIR-9800: Убираю лишние импорты

DIR-9800: линкуемся с lb

DIR-9800: Настройки для логброкера

DIR-9800: Вытаскиваю методо is_tech в функцию  [ https://a.yandex-team.ru/arc/commit/7982963 ]

[uruz](http://staff/uruz) 2021-03-22 18:17:08+03:00

2.193
-----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9949: [Проксирование] Проксировать создание доменных пользователей Я.Орг  [ https://a.yandex-team.ru/arc/commit/7954180 ]

* [smosker](http://staff/smosker)

 * PASSP-31314 Использование tvmauth под капотом

Убираем использование ticket_parser2 из library/tvm2 library/python-django-yauth 
Подробности в https://st.yandex-team.ru/PASSP-31314  [ https://a.yandex-team.ru/arc/commit/7948299 ]

[oleglarionov](http://staff/oleglarionov) 2021-03-16 20:09:12+03:00

2.192
-----
 * DIR-9854: межсервисная аутентификация коннект и баланс  [ https://a.yandex-team.ru/arc/commit/7933811 ]

[oleglarionov](http://staff/oleglarionov) 2021-03-10 12:54:56+03:00

2.191
-----
 * DIR-10082: Для федеративных пользователей не проставлен email  [ https://a.yandex-team.ru/arc/commit/7917292 ]

[oleglarionov](http://staff/oleglarionov) 2021-03-03 19:07:18+03:00

2.190
-----
 * DIR-9841: Пятисотит ручка calculate price  [ https://a.yandex-team.ru/arc/commit/7915766 ]

[uruz](http://staff/uruz) 2021-03-03 14:18:00+03:00

2.189
-----
 * DIR-10096: Таска вместо прямого вызова  [ https://a.yandex-team.ru/arc/commit/7913541 ]

[uruz](http://staff/uruz) 2021-03-02 19:39:07+03:00

2.188
-----
 * DIR-10096: Починить первый синк: пробрасываем коннекшен во все функции синка  [ https://a.yandex-team.ru/arc/commit/7910317 ]

[uruz](http://staff/uruz) 2021-03-01 22:24:18+03:00

2.187
-----
 * DIR-10094: Увеличиваю количество ретраев, чтобы укладываться в интервал синка  [ https://a.yandex-team.ru/arc/commit/7909362 ]

[uruz](http://staff/uruz) 2021-03-01 17:56:15+03:00

2.186
-----
 * DIR-10094: Падаем и ретраимся, если cloud_uid ещё не посинкан + логи  [ https://a.yandex-team.ru/arc/commit/7908457 ]

[uruz](http://staff/uruz) 2021-03-01 14:45:49+03:00

2.185
-----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-10074: добавил organization_name в параметры письма о включении трекера  [ https://a.yandex-team.ru/arc/commit/7904323 ]

[uruz](http://staff/uruz) 2021-02-26 19:26:44+03:00

2.184
-----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-10074: заменил id рассылки включения трекера для рассылятора  [ https://a.yandex-team.ru/arc/commit/7904013 ]

[uruz](http://staff/uruz) 2021-02-26 18:07:37+03:00

2.183
-----

[uruz](http://staff/uruz) 2021-02-26 15:54:40+03:00

2.182
-----

[uruz](http://staff/uruz) 2021-02-26 13:19:10+03:00

2.181
-----
 * DIR-10076: camelCase для ключей и формат ответа  [ https://a.yandex-team.ru/arc/commit/7900688 ]

[uruz](http://staff/uruz) 2021-02-25 19:17:36+03:00

2.180
-----
 * DIR-10076: Фикс пятисотки при пустом списке организаций  [ https://a.yandex-team.ru/arc/commit/7899470 ]

[uruz](http://staff/uruz) 2021-02-25 14:32:30+03:00

2.179
-----
 * PR from branch users/uruz/feature/DIR-10076

DIR-10076: Фиксы

DIR-10076: Ручка со списком облачных организаций пользователя  [ https://a.yandex-team.ru/arc/commit/7899206 ]

[uruz](http://staff/uruz) 2021-02-25 13:31:06+03:00

2.178
-----
 * DIR-10046: Переключить балансер Webmaster Internal API  [ https://a.yandex-team.ru/arc/commit/7853457 ]

[uruz](http://staff/uruz) 2021-02-12 16:05:42+03:00

2.177
-----
 * DIR-9925: No json for 202  [ https://a.yandex-team.ru/arc/commit/7851098 ]

[uruz](http://staff/uruz) 2021-02-11 21:08:30+03:00

2.176
-----
 * DIR-9762: Существуют пользователи с uid из облачного диапазона, но без cloud_uid  [ https://a.yandex-team.ru/arc/commit/7850278 ]

[uruz](http://staff/uruz) 2021-02-11 17:12:24+03:00

2.175
-----
 * DIR-10048: Добавить фильтр по нескольким типам организаций  [ https://a.yandex-team.ru/arc/commit/7845640 ]

[uruz](http://staff/uruz) 2021-02-10 14:25:55+03:00

2.174
-----
 * DIR-9925: Правка настроек                               [ https://a.yandex-team.ru/arc/commit/7842131 ]
 * DIR-9916: Включать мультиорг для облачных организаций.  [ https://a.yandex-team.ru/arc/commit/7841558 ]

[uruz](http://staff/uruz) 2021-02-09 14:15:41+03:00

2.173
-----
 * PR from branch users/uruz/DIR-9925

fix tests

DIR-9925: fixes

DIR-9925: Перейти с рассылятора на cloud_notify  [ https://a.yandex-team.ru/arc/commit/7833434 ]

[uruz](http://staff/uruz) 2021-02-05 16:08:05+03:00

2.172
-----
 * releasing version 2.172                      [ https://a.yandex-team.ru/arc/commit/7826669 ]
 * DIR-10006: Поправил изменение типа на cloud  [ https://a.yandex-team.ru/arc/commit/7826643 ]

[uruz](http://staff/uruz) 2021-02-03 17:02:03+03:00

2.171
-----
 * DIR-10006: Ошибка при изменении типа организации в Каталоге  [ https://a.yandex-team.ru/arc/commit/7824262 ]

[uruz](http://staff/uruz) 2021-02-02 21:46:02+03:00

2.170
-----
 * DIR-10004: Добавить cloud_org_id в админскую ручку  [ https://a.yandex-team.ru/arc/commit/7823624 ]

[uruz](http://staff/uruz) 2021-02-02 18:40:49+03:00

2.169
-----
 * PR from branch users/uruz/feature/DIR-10000  [ https://a.yandex-team.ru/arc/commit/7820407 ]

[uruz](http://staff/uruz) 2021-02-01 21:58:34+03:00

2.168
-----
 * DIR-9843: Пытаемся засинхронизировать мастер-домен в рид-онли транзакции  [ https://a.yandex-team.ru/arc/commit/7787386 ]

[oleglarionov](http://staff/oleglarionov) 2021-01-28 13:24:24+03:00

2.167
-----
 * DIR-9920: Трекер: добавить тип организаций cloud_partner  [ https://a.yandex-team.ru/arc/commit/7784031 ]

[oleglarionov](http://staff/oleglarionov) 2021-01-27 13:29:08+03:00

2.166
-----
 * DIR-9919: Флаг отключения контроля наличия платёжных данных  [ https://a.yandex-team.ru/arc/commit/7758302 ]

[oleglarionov](http://staff/oleglarionov) 2021-01-18 16:48:17+03:00

2.165
-----
 * DIR-9932: Добавить в params 400-ой ошибки при создании организации org_id  [ https://a.yandex-team.ru/arc/commit/7754139 ]

[uruz](http://staff/uruz) 2021-01-15 19:11:33+03:00

2.164
-----
 * DIR-9792: Удаляю пресет cloud-tracker, изменяю состав сервисов у пресета cloud  [ https://a.yandex-team.ru/arc/commit/7744289 ]
 * DIR-9885: Проверка на случай пустого ответа                                     [ https://a.yandex-team.ru/arc/commit/7724677 ]

[uruz](http://staff/uruz) 2021-01-12 16:49:26+03:00

2.163
-----
 * DIR-9885: Создание пользователя на лету падает с ошибкой

DIR-9885: Проверяем, что поле organizations существует в grpc-ответе. Открываем meta-коннекшен на запись, если нужно записать. Ловим  UserAlreadyInThisOrganization - если пользователь посинкался пока мы делали select/insert

DIR-9885: Пытаемся создать пользователя для всех случаев, а не только для облачных (т.к. для паспортных сервисы будут продолжать приходить к нам с X-UID, а не X-Cloud-UID)  [ https://a.yandex-team.ru/arc/commit/7724104 ]
 * DIR-9792: Я.Орг: пресет по-умолчанию                                                                                                                                                                                                                                                                                                                                                                                                                                    [ https://a.yandex-team.ru/arc/commit/7718898 ]

[uruz](http://staff/uruz) 2020-12-28 18:06:09+03:00

2.162
-----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9814: ходим в доменатор в ручке для спамобороны                               [ https://a.yandex-team.ru/arc/commit/7710089 ]
 * DIR-9722: при создании орг-ции с доменом по фиче создаем этот домен в доменаторе  [ https://a.yandex-team.ru/arc/commit/7710087 ]
 * DIR-9862: Добавил тип education в список типов организаций, которые не биллятся   [ https://a.yandex-team.ru/arc/commit/7710086 ]
 * DIR-9721: Админская ручка получения списка доменов организации из доменатора      [ https://a.yandex-team.ru/arc/commit/7710085 ]

[uruz](http://staff/uruz) 2020-12-22 20:10:13+03:00

2.161
-----
 * DIR-9766: Удаляю код походов за токенами в IAM, переходим на TS  [ https://a.yandex-team.ru/arc/commit/7663255 ]

[uruz](http://staff/uruz) 2020-12-11 14:40:27+03:00

2.160
-----
 * DIR-9766: Фикс имени поля  [ https://a.yandex-team.ru/arc/commit/7660748 ]

[uruz](http://staff/uruz) 2020-12-10 18:19:43+03:00

2.159
-----
 * DIR-9766: add new dep  [ https://a.yandex-team.ru/arc/commit/7660495 ]

[uruz](http://staff/uruz) 2020-12-10 17:43:28+03:00

2.158
-----
 * DIR-9709: fixed proto spec field name  [ https://a.yandex-team.ru/arc/commit/7653003 ]

[uruz](http://staff/uruz) 2020-12-08 15:58:57+03:00

2.157
-----
 * DIR-9723: Поправить расчет цены  [ https://a.yandex-team.ru/arc/commit/7652832 ]

[oleglarionov](http://staff/oleglarionov) 2020-12-08 15:22:22+03:00

2.156
-----
 * DIR-9709: Я.Орг: создание пользователя на лету  [ https://a.yandex-team.ru/arc/commit/7652771 ]

[uruz](http://staff/uruz) 2020-12-08 15:12:43+03:00

2.155
-----
 * DIR-9765: Я.Орг: ФИО федеративных пользователей в Коннекте  [ https://a.yandex-team.ru/arc/commit/7652220 ]

[oleglarionov](http://staff/oleglarionov) 2020-12-08 13:04:35+03:00

2.154
-----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9638: fixes  [ https://a.yandex-team.ru/arc/commit/7643434 ]

* [hhell](http://staff/hhell)

 * CONTRIB-2042: contrib/python/sqlalchemy -> contrib/python/sqlalchemy/sqlalchemy-1.2

<!-- DEVEXP BEGIN -->
![review](https://codereview.in.yandex-team.ru/badges/review-in_progress-yellow.svg) [![inngonch](https://codereview.in.yandex-team.ru/badges/inngonch-...-yellow.svg)](https://staff.yandex-team.ru/inngonch)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/7633357 ]

[oleglarionov](http://staff/oleglarionov) 2020-12-04 15:37:52+03:00

2.153
-----
 * DIR-9638: fixed iam host for integration-qa/preprod  [ https://a.yandex-team.ru/arc/commit/7623619 ]

[uruz](http://staff/uruz) 2020-11-26 18:51:54+03:00

2.152
-----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9638: fix host  [ https://a.yandex-team.ru/arc/commit/7622893 ]

[uruz](http://staff/uruz) 2020-11-26 15:50:21+03:00

2.151
-----

[uruz](http://staff/uruz) 2020-11-26 14:28:53+03:00

2.150
-----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9638: Синхронизация облачных пользователей через другую ручку  [ https://a.yandex-team.ru/arc/commit/7622392 ]

[uruz](http://staff/uruz) 2020-11-26 14:15:21+03:00

2.149
-----
 * DIR-9745: Заменить в скриптах releaser на ya tool releaser                                [ https://a.yandex-team.ru/arc/commit/7619494 ]
 * DIR-9742: Добавить в ошибку создания организации информацию о конфликтующих организациях  [ https://a.yandex-team.ru/arc/commit/7619468 ]

[uruz](http://staff/uruz) 2020-11-26 14:02:20+03:00

2.148
-----
 * PR from branch users/oleglarionov/DIR-9750  [ https://a.yandex-team.ru/arc/commit/7617303 ]

[oleglarionov](http://staff/oleglarionov) 2020-11-24 20:27:11+03:00

2.147
-----
 * DIR-9537: Везде где в коде есть обращение к domainmodel - ходить в доменатор  [ https://a.yandex-team.ru/arc/commit/7615792 ]

[oleglarionov](http://staff/oleglarionov) 2020-11-24 14:26:30+03:00

2.146
-----

* [uruz](http://staff/uruz)

 * DIR-9637: Поддержать сохранение cloud_org_id / clouds при создании организации  [ https://a.yandex-team.ru/arc/commit/7612705 ]

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9537: Написал проксирующие функции  [ https://a.yandex-team.ru/arc/commit/7540134 ]

[uruz](http://staff/uruz) 2020-11-23 16:32:02+03:00

2.145
-----
 * DIR-9650 Возвращаем имя для tr пользователей  [ https://a.yandex-team.ru/arc/commit/7527214 ]

[smosker](http://staff/smosker) 2020-10-29 11:53:20+03:00

2.144
-----

* [smosker](http://staff/smosker)

 * DIR-9556 Правка отправки данных в YT  [ https://a.yandex-team.ru/arc/commit/7489731 ]

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9537: ручки в доменаторе + методы в клиенте  [ https://a.yandex-team.ru/arc/commit/7489465 ]

[smosker](http://staff/smosker) 2020-10-23 14:37:37+03:00

2.143
-----
 * DIR-9641 дергаем ручку доменатора при включении фичи  [ https://a.yandex-team.ru/arc/commit/7484736 ]

[smosker](http://staff/smosker) 2020-10-21 22:51:55+03:00

2.142
-----
 * fix domains  [ https://a.yandex-team.ru/arc/commit/7477732 ]

[oleglarionov](http://staff/oleglarionov) 2020-10-19 19:16:31+03:00

2.141
-----
 * DIR-9622 Умножаем количество лицензий для биллинга  [ https://a.yandex-team.ru/arc/commit/7476069 ]

[smosker](http://staff/smosker) 2020-10-19 12:43:00+03:00

2.140
-----
 * DIR-9371: fix ручки списка доменов  [ https://a.yandex-team.ru/arc/commit/7472260 ]

[oleglarionov](http://staff/oleglarionov) 2020-10-16 16:38:50+03:00

2.139
-----
 * DIR-9371: Получать и добавлять и удалять домены и в коннекте и в доменатор

<!-- DEVEXP BEGIN -->
![review](https://codereview.yandex-team.ru/badges/review-complete-green.svg) [![smosker](https://codereview.yandex-team.ru/badges/smosker-ok-green.svg)](https://staff.yandex-team.ru/smosker) [![elisei](https://codereview.yandex-team.ru/badges/elisei-ok-green.svg)](https://staff.yandex-team.ru/elisei)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/7469084 ]

[oleglarionov](http://staff/oleglarionov) 2020-10-15 16:56:34+03:00

2.138
-----
 * DIR-9620 ручка для синхронизации доменов

[smosker](http://staff/smosker) 2020-10-15 13:49:36+03:00

2.137
-----
 * DIR-9617 Правка количества лицензий для проверки  [ https://a.yandex-team.ru/arc/commit/7457361 ]

[smosker](http://staff/smosker) 2020-10-12 21:07:40+03:00

2.136
-----
 * DIR-9588 Прокси в ручке изменения организации                         [ https://a.yandex-team.ru/arc/commit/7444201 ]
 * DIR-9586 Возможность получать только доменные учетки в ручке suggest  [ https://a.yandex-team.ru/arc/commit/7444200 ]

[smosker](http://staff/smosker) 2020-10-07 15:03:33+03:00

2.135
-----
 * DIR-9516 Правка фильтрации по id                        [ https://a.yandex-team.ru/arc/commit/7437271 ]
 * DIR-9584 Поддержка возможности отключить проксирование  [ https://a.yandex-team.ru/arc/commit/7437227 ]
 * DIR-9521 Поддержка фильтрации по organization_type      [ https://a.yandex-team.ru/arc/commit/7437226 ]

[smosker](http://staff/smosker) 2020-10-05 14:59:26+03:00

2.134
-----
 * DIR-9595 не удаляем пользователя в диске  [ https://a.yandex-team.ru/arc/commit/7437097 ]

[smosker](http://staff/smosker) 2020-10-05 14:25:09+03:00

2.133
-----
 * DIR-9587 Не проверяем есть ли данные в таблицах  [ https://a.yandex-team.ru/arc/commit/7423330 ]

[smosker](http://staff/smosker) 2020-10-02 18:16:08+03:00

2.132
-----
 * DIR-9587 Правка таски сохранения данных  [ https://a.yandex-team.ru/arc/commit/7421840 ]

[smosker](http://staff/smosker) 2020-10-02 13:02:39+03:00

2.131
-----
 * DIR-9538 Правка расчета долга  [ https://a.yandex-team.ru/arc/commit/7419603 ]

[smosker](http://staff/smosker) 2020-10-01 17:54:59+03:00

2.130
-----
 * DIR-9532 прокси в ручке /v6/organizations/<id>                [ https://a.yandex-team.ru/arc/commit/7418671 ]
 * DIR-9557 Создаем алиасы в паспорте при создании пользователя  [ https://a.yandex-team.ru/arc/commit/7418668 ]

[smosker](http://staff/smosker) 2020-10-01 15:18:10+03:00

2.129
-----
 * DIR-9456 Новая политика ценообразования для трекера     [ https://a.yandex-team.ru/arc/commit/7410740 ]
 * DIR-9531 Прокси в ручке organizations + use_proxy фича  [ https://a.yandex-team.ru/arc/commit/7410676 ]
 * DIR-9563 Не ломаемся при отсутствии pdd сида            [ https://a.yandex-team.ru/arc/commit/7407515 ]
 * DIR-9530 Прокси в я.орг + поддержка x-user-iam-token    [ https://a.yandex-team.ru/arc/commit/7364222 ]

[smosker](http://staff/smosker) 2020-09-29 14:39:48+03:00

2.128
-----
 * DIR-9548: Реализовать ручку на событие подтверждение домена  [ https://a.yandex-team.ru/arc/commit/7360538 ]

[oleglarionov](http://staff/oleglarionov) 2020-09-23 13:12:23+03:00

2.127
-----
 * DIR-9488 Не отключаем трекер за долги  [ https://a.yandex-team.ru/arc/commit/7336650 ]

[smosker](http://staff/smosker) 2020-09-17 11:11:10+03:00

2.126
-----
 * DIR-9509 Сохраняем дату биллинга при включении трекера  [ https://a.yandex-team.ru/arc/commit/7323548 ]
 * DIR-9487 Функция для расчета количества лицензий        [ https://a.yandex-team.ru/arc/commit/7322936 ]

[smosker](http://staff/smosker) 2020-09-11 17:06:11+03:00

2.125
-----
 * DIR-9486 Сохраняем лог лицензий  [ https://a.yandex-team.ru/arc/commit/7314201 ]

[smosker](http://staff/smosker) 2020-09-09 12:06:55+03:00

2.124
-----
 * DIR-9504: Поправил типы в схеме данных YT для аналитической выгрузки  [ https://a.yandex-team.ru/arc/commit/7313736 ]

[oleglarionov](http://staff/oleglarionov) 2020-09-09 10:04:25+03:00

2.123
-----
 * DIR-9420 Правка проверки консистентности рассылок  [ https://a.yandex-team.ru/arc/commit/7300190 ]

[smosker](http://staff/smosker) 2020-09-04 12:17:37+03:00

2.122
-----
 * DIR-9489: Заменить BILLING_MANAGER_UID  [ https://a.yandex-team.ru/arc/commit/7285393 ]

[oleglarionov](http://staff/oleglarionov) 2020-09-03 15:15:55+03:00

2.121
-----
 * DIR-9454 Добавление черного списка доменов  [ https://a.yandex-team.ru/arc/commit/7285137 ]
 * DIR-9469 Обновляем владельцам is_pdd_admin  [ https://a.yandex-team.ru/arc/commit/7285131 ]

[smosker](http://staff/smosker) 2020-09-03 14:22:58+03:00

2.120
-----
 * DIR-9299: Везде где в коде есть обращение к registrar_id ходить в доменатор  [ https://a.yandex-team.ru/arc/commit/7269532 ]

[oleglarionov](http://staff/oleglarionov) 2020-08-31 13:48:19+03:00

2.119
-----
 * DIR-9416 ручка изменения лимита во внутреннем апи  [ https://a.yandex-team.ru/arc/commit/7264940 ]

[smosker](http://staff/smosker) 2020-08-28 17:28:53+03:00

2.118
-----
 * FORMS-5866 Правка авторизации облачного пользователя  [ https://a.yandex-team.ru/arc/commit/7255771 ]

[smosker](http://staff/smosker) 2020-08-26 12:13:40+03:00

2.117
-----
 * DIR-9376 Устраняем рассинхрон в случае несуществующего департамента  [ https://a.yandex-team.ru/arc/commit/7252058 ]
 * DIR-9375 Не 500тим при удалении несуществующего алиаса               [ https://a.yandex-team.ru/arc/commit/7252042 ]

[smosker](http://staff/smosker) 2020-08-25 12:00:58+03:00

2.116
-----
 * DIR-9296: Начать в ручках регистраторов ходить и к нам и в новый сервис  [ https://a.yandex-team.ru/arc/commit/7250024 ]

[oleglarionov](http://staff/oleglarionov) 2020-08-24 17:34:39+03:00

2.115
-----
 * DIR-9269: валидация email'а организации  [ https://a.yandex-team.ru/arc/commit/7236357 ]

[oleglarionov](http://staff/oleglarionov) 2020-08-19 14:59:20+03:00

2.114
-----
 * DIR-9385 Проставляем признак админа не только доменным пользователям  [ https://a.yandex-team.ru/arc/commit/7219741 ]

[smosker](http://staff/smosker) 2020-08-13 21:24:02+03:00

2.113
-----
 * DIR-6831: Переезд на аркадийную реализацию tvm2  [ https://a.yandex-team.ru/arc/commit/7209902 ]

[oleglarionov](http://staff/oleglarionov) 2020-08-11 12:13:43+03:00

2.112
-----
 * DIR-9400: Поддержка возможности перехода фронта на новый tvm client id  [ https://a.yandex-team.ru/arc/commit/7177485 ]

[oleglarionov](http://staff/oleglarionov) 2020-08-05 14:00:04+03:00

2.111
-----
 * DIR-9328 Проверка заполненности платежной информации для трекера  [ https://a.yandex-team.ru/arc/commit/7162932 ]
 * DIR-9327 Правка поиска suggest                                    [ https://a.yandex-team.ru/arc/commit/7162931 ]

[smosker](http://staff/smosker) 2020-07-31 11:44:46+03:00

2.110
-----
 * DIR-9300 Прокси в who-is  [ https://a.yandex-team.ru/arc/commit/7157976 ]

[smosker](http://staff/smosker) 2020-07-29 22:39:09+03:00

2.109
-----
 * DIR-9365 Ручка добавления/удаления лицензии  [ https://a.yandex-team.ru/arc/commit/7150707 ]
 * DIR-9329 Показываем цену в триале            [ https://a.yandex-team.ru/arc/commit/7150705 ]
 * DIR-9180 Fix logging for domenator           [ https://a.yandex-team.ru/arc/commit/7136394 ]

[smosker](http://staff/smosker) 2020-07-27 20:27:39+03:00

2.108
-----
 * DIR-9335 Валидация имени/фамилии при изменении  [ https://a.yandex-team.ru/arc/commit/7129779 ]

[smosker](http://staff/smosker) 2020-07-20 12:32:30+03:00

2.107
-----
 * DIR-9184 Прокси в ручках доменных токенов  [ https://a.yandex-team.ru/arc/commit/7121637 ]

[smosker](http://staff/smosker) 2020-07-17 14:58:56+03:00

2.106
-----

* [smosker](http://staff/smosker)

 * DIR-9339 Добавил billing_info в выдачу  [ https://a.yandex-team.ru/arc/commit/7116963 ]

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9253: Запуск перепроверки в вебмастере при автоотрыве домена.  [ https://a.yandex-team.ru/arc/commit/7116720 ]

[smosker](http://staff/smosker) 2020-07-16 19:56:09+03:00

2.105
-----
 * DIR-9239: fix  [ https://a.yandex-team.ru/arc/commit/7095709 ]

[oleglarionov](http://staff/oleglarionov) 2020-07-09 14:04:46+03:00

2.104
-----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9239: Ручка с детальной информацией по лицензиям трекера для каталога  [ https://a.yandex-team.ru/arc/commit/7086040 ]

* [smosker](http://staff/smosker)

 * DIR-9306 Добавляю фильтрацию по саджесту  [ https://a.yandex-team.ru/arc/commit/7086038 ]

* [shadchin](http://staff/shadchin)

 * Fix tests yandex_directory with Python 3.8  [ https://a.yandex-team.ru/arc/commit/7077827 ]

[smosker](http://staff/smosker) 2020-07-07 14:48:55+03:00

2.103
-----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9221: фикс долгого запроса  [ https://a.yandex-team.ru/arc/commit/7073305 ]

* [smosker](http://staff/smosker)

 * DIR-9283 Поддержка возможности указать слаг письма    [ https://a.yandex-team.ru/arc/commit/7073304 ]
 * DIR-9301 Поддержка organization_type в v6 версии апи  [ https://a.yandex-team.ru/arc/commit/7073285 ]

[smosker](http://staff/smosker) 2020-07-02 16:08:20+03:00

2.102
-----

* [smosker](http://staff/smosker)

 * DIR-9232 Выдача лицензии при принятии инвайта  [ https://a.yandex-team.ru/arc/commit/7072242 ]

* [comradeandrew](http://staff/comradeandrew)

 * Contrib: separate tornado from gunicorn GEOINFRA-2117

В gunicorn использование tornado веркера является опциональным. Прямо сейчас по пирдиру на gunicorn всегда приходит tornado, причем версии 4, что делает пирдир на gunicorn не совместимым с contrib/python/motor под PY3, потому что motor пирдирит себе tornado-6.
Так как в gunicorn использовать tornado - опционально, вынес пирдир на tornado всем кто пирдирит gunicorn. Такое изменение никак не меняет поведение и никаких функциональных изменений здесь не ожидается. Все кому нужен tornado вместе с gunicorn могут делать пирдир на него отдельно.

UPD: Вынес пирдир на торнадо явно  [ https://a.yandex-team.ru/arc/commit/7068479 ]

[smosker](http://staff/smosker) 2020-07-02 12:34:58+03:00

2.101
-----
 * DIR-9284 Включаю отключение трекера  [ https://a.yandex-team.ru/arc/commit/7036394 ]

[smosker](http://staff/smosker) 2020-06-25 16:57:54+03:00

2.100
-----
 * DIR-9230: Поправил выдачу  [ https://a.yandex-team.ru/arc/commit/7036026 ]

[oleglarionov](http://staff/oleglarionov) 2020-06-25 16:45:50+03:00

2.99
----
 * DIR-9278 отключаем отлючение трекера  [ https://a.yandex-team.ru/arc/commit/7013115 ]

[smosker](http://staff/smosker) 2020-06-23 20:43:35+03:00

2.98
----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9263: Добавить инкремент ревизии организаций в ручке PATCH /organization  [ https://a.yandex-team.ru/arc/commit/7004569 ]
 * DIR-9230: Добавить данные в ручку v6/users для трекера                        [ https://a.yandex-team.ru/arc/commit/7004568 ]

* [smosker](http://staff/smosker)

 * DIR-9151 правка ошибки при создании организации  [ https://a.yandex-team.ru/arc/commit/7004567 ]

[smosker](http://staff/smosker) 2020-06-22 14:33:02+03:00

2.97
----

* [smosker](http://staff/smosker)

 * DIR-9248 обрезаем пробелы из логина при смене владельца          [ https://a.yandex-team.ru/arc/commit/6988539 ]
 * DIR-9237 Ручка с данными лицензий для трекера                    [ https://a.yandex-team.ru/arc/commit/6988537 ]
 * DIR-9231 добавить в ручки groups/departments данные для трекера  [ https://a.yandex-team.ru/arc/commit/6988533 ]

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9078: Новый тип организации charity  [ https://a.yandex-team.ru/arc/commit/6988528 ]

[smosker](http://staff/smosker) 2020-06-19 15:14:54+03:00

2.96
----

* [smosker](http://staff/smosker)

 * DIR-9215 Поддержка авторизации облачных пользователей  [ https://a.yandex-team.ru/arc/commit/6921520 ]

* [oleglarionov](http://staff/oleglarionov)

 * DIR-8841: Передавать person_id в ручке об организации в Каталоге  [ https://a.yandex-team.ru/arc/commit/6921515 ]

[smosker](http://staff/smosker) 2020-06-10 15:46:06+03:00

2.95
----

* [smosker](http://staff/smosker)

 * DIR-9216 Правка 500 при создании пользователя   [ https://a.yandex-team.ru/arc/commit/6913977 ]
 * DIR-8990 Добавлена ручка для просмотра лимитов  [ https://a.yandex-team.ru/arc/commit/6913970 ]
 * DIR-9169 Сохраняем облачный uid в базе          [ https://a.yandex-team.ru/arc/commit/6913968 ]

* [oleglarionov](http://staff/oleglarionov)

 * Docstring fix  [ https://a.yandex-team.ru/arc/commit/6913128 ]

[smosker](http://staff/smosker) 2020-06-08 16:23:11+03:00

2.94
----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-8577: Ускорение ручки создания пользователя  [ https://a.yandex-team.ru/arc/commit/6906808 ]

[smosker](http://staff/smosker) 2020-06-05 12:04:22+03:00

2.93
----
 * DIR-9213 Правка синхронизации пользователей  [ https://a.yandex-team.ru/arc/commit/6905660 ]
 * fix syncexternalids for robots               [ https://a.yandex-team.ru/arc/commit/6905643 ]

[smosker](http://staff/smosker) 2020-06-04 22:58:07+03:00

2.92
----

* [smosker](http://staff/smosker)

 * DIR-9185 Синхронизация данных пользователей из паспорта  [ https://a.yandex-team.ru/arc/commit/6900980 ]
 * DIR-8872 Правка ручки сервисов                           [ https://a.yandex-team.ru/arc/commit/6900979 ]

* [ignat](http://staff/ignat)

 * Remove yt/python/yt_yson_bindings dependency  [ https://a.yandex-team.ru/arc/commit/6888976 ]

[smosker](http://staff/smosker) 2020-06-03 18:04:26+03:00

2.91
----

* [smosker](http://staff/smosker)

 * DIR-9126 Не создаем внешнего админа в таске на смену владельца  [ https://a.yandex-team.ru/arc/commit/6879914 ]
 * DIR-9124 Правка дублирования групп                              [ https://a.yandex-team.ru/arc/commit/6879908 ]

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9014: Перейти в тестах на pytest  [ https://a.yandex-team.ru/arc/commit/6875463 ]

[smosker](http://staff/smosker) 2020-05-28 12:46:51+03:00

2.90
----
 * DIR-9056 Ручка для добавления/удаления внешнего админа  [ https://a.yandex-team.ru/arc/commit/6861541 ]

[smosker](http://staff/smosker) 2020-05-25 14:30:30+03:00

2.89
----
 * DIR-9052 правка хостов метрики                                   [ https://a.yandex-team.ru/arc/commit/6848715 ]
 * DIR-9138 Правка удаления пользователей при удалении организации  [ https://a.yandex-team.ru/arc/commit/6848713 ]

[smosker](http://staff/smosker) 2020-05-20 16:49:59+03:00

2.88
----

* [smosker](http://staff/smosker)

 * DIR-9093 Правка работы ручки сервисов для зама админа        [ https://a.yandex-team.ru/arc/commit/6844517 ]
 * DIR-9114 Правка получения емейла для облачных пользователей  [ https://a.yandex-team.ru/arc/commit/6844509 ]
 * DIR-9080 правка хоста рассылок + правка логики запуска       [ https://a.yandex-team.ru/arc/commit/6844507 ]
 * DIR-9010 Игнорируем ответственность за формы при увольнении  [ https://a.yandex-team.ru/arc/commit/6844503 ]
 * DIR-9046 Правка обработки существования пользователя         [ https://a.yandex-team.ru/arc/commit/6844502 ]

* [oleglarionov](http://staff/oleglarionov)

 * DIR-8046: Рассылать письма и отключать трекер если долго не было активности  [ https://a.yandex-team.ru/arc/commit/6840342 ]

[smosker](http://staff/smosker) 2020-05-19 14:06:41+03:00

2.87
----
 * DIR-8961 удаление организаций с долгом            [ https://a.yandex-team.ru/arc/commit/6785145 ]
 * DIR-9048 Фикс лимита пользователей в организации  [ https://a.yandex-team.ru/arc/commit/6785144 ]

[smosker](http://staff/smosker) 2020-05-14 14:48:56+03:00

2.86
----
 * DIR-8888 Поддержка возможности указать срок действия промокода       [ https://a.yandex-team.ru/arc/commit/6781298 ]
 * Change .devexp.json

Note: mandatory check (NEED_CHECK) was skipped  [ https://a.yandex-team.ru/arc/commit/6755271 ]

[smosker](http://staff/smosker) 2020-05-13 13:46:02+03:00

2.85
----
 * DIR-8924 правка создания тасок  [ https://a.yandex-team.ru/arc/commit/6755152 ]

[smosker](http://staff/smosker) 2020-04-30 16:19:39+03:00

2.84
----
 * DIR-9055 Правка запуска  check_maillista  [ https://a.yandex-team.ru/arc/commit/6754262 ]

[smosker](http://staff/smosker) 2020-04-30 13:02:40+03:00

2.83
----
 * DIR-8924 Синхронизация данных облачных пользователей  [ https://a.yandex-team.ru/arc/commit/6754203 ]

[smosker](http://staff/smosker) 2020-04-30 12:48:49+03:00

2.82
----
 * Change docker_package.json

Note: mandatory check (NEED_CHECK) was skipped  [ https://a.yandex-team.ru/arc/commit/6752390 ]
 * DIR-8901 Удаление организации с ресурсами и учетками                        [ https://a.yandex-team.ru/arc/commit/6752298 ]
 * DIR-8874 Уборка кода                                                        [ https://a.yandex-team.ru/arc/commit/6752144 ]

[smosker](http://staff/smosker) 2020-04-29 20:49:43+03:00

2.81
----
 * DIR-9038 Не ставим таски на синк с паспортом для облачных пользователей                                                           [ https://a.yandex-team.ru/arc/commit/6747296 ]
 * DIR-8955 Добавил полезные импорты в шел                                                                                           [ https://a.yandex-team.ru/arc/commit/6747295 ]
 * DIR-8925 Поправлено вычисление свойства enabled в выдаче ручки с сервисами. Добавлено поле settings_url в таблицу services_links  [ https://a.yandex-team.ru/arc/commit/6747291 ]

[smosker](http://staff/smosker) 2020-04-28 13:00:05+03:00

2.80
----

[oleglarionov](http://staff/oleglarionov) 2020-04-24 14:47:18+03:00

2.80
----

* [smosker](http://staff/smosker)

 * DIR-8997 Правим количество в выдаче ручке организаций по куки  [ https://a.yandex-team.ru/arc/commit/6695582 ]

* [oleglarionov](http://staff/oleglarionov)

 * DIR-9025: Поднятие ревизии в организациях пользователя при удалении одной из организациий  [ https://a.yandex-team.ru/arc/commit/6695578 ]

* [shadchin](http://staff/shadchin)

 * IGNIETFERRO-1154 Rename contrib/python/jwt to contrib/python/PyJWT  [ https://a.yandex-team.ru/arc/commit/6691758 ]

[oleglarionov](http://staff/oleglarionov) 2020-04-24 14:16:50+03:00

2.79
----

* [marianastrix](http://staff/marianastrix)

 * DIR-8915: Не прокидывается org_id и uid в карточке сотрудника Коннекта  [ https://a.yandex-team.ru/arc/commit/6687429 ]

* [smosker](http://staff/smosker)

 * DIR-9000 Убираю лишние логи                              [ https://a.yandex-team.ru/arc/commit/6687423 ]
 * DIR-9004 Правка проверки уволености при выдаче лицензий  [ https://a.yandex-team.ru/arc/commit/6687422 ]

* [oleglarionov](http://staff/oleglarionov)

 * DIR-8779: Возвращаем пустой список вместо пятисотки  [ https://a.yandex-team.ru/arc/commit/6687420 ]

[smosker](http://staff/smosker) 2020-04-22 13:12:16+03:00

2.78
----
 * DIR-8979 Не учитываем org_id в ручке поиска доменов если он явно не задан  [ https://a.yandex-team.ru/arc/commit/6679199 ]

[smosker](http://staff/smosker) 2020-04-20 12:52:02+03:00

2.77
----
 * DIR-8966 fix tr sms problem  [ https://a.yandex-team.ru/arc/commit/6667331 ]

[smosker](http://staff/smosker) 2020-04-15 17:04:33+03:00

2.76
----
 * DIR-8879 Настройка работы с pgcli                 [ https://a.yandex-team.ru/arc/commit/6666986 ]
 * DIR-8958 Не отправляем письмо при включении вики  [ https://a.yandex-team.ru/arc/commit/6666911 ]
 * DIR-8878 Настроена работа с миграциями            [ https://a.yandex-team.ru/arc/commit/6664992 ]

[smosker](http://staff/smosker) 2020-04-15 15:35:46+03:00

2.75
----
 * SUBBOTNIK-4723 fix style tests                      [ https://a.yandex-team.ru/arc/commit/6660985 ]
 * DIR-8930 Включаем multiorg всем новым организациям  [ https://a.yandex-team.ru/arc/commit/6660982 ]

[smosker](http://staff/smosker) 2020-04-13 20:27:15+03:00

2.74
----

* [smosker](http://staff/smosker)

 * DIR-8895 Возможность самовыпила из организации                                                                                                                                                                                                                                                                                                                                                                                                                  [ https://a.yandex-team.ru/arc/commit/6605152 ]
 * DIR-8418 Не выводим лимит в каталоге если его нет

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-complete-green.svg) [![oleglarionov](https://codereview.common-int.yandex-team.ru/badges/oleglarionov-ok-green.svg)](https://staff.yandex-team.ru/oleglarionov) [![kdunaev](https://codereview.common-int.yandex-team.ru/badges/kdunaev-ok-green.svg)](https://staff.yandex-team.ru/kdunaev)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6605128 ]
 * DIR-8927 Запуск тестов через pycharm

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-complete-green.svg) [![marianastrix](https://codereview.common-int.yandex-team.ru/badges/marianastrix-ok-green.svg)](https://staff.yandex-team.ru/marianastrix) [![kdunaev](https://codereview.common-int.yandex-team.ru/badges/kdunaev-ok-green.svg)](https://staff.yandex-team.ru/kdunaev)
<!-- DEVEXP END -->               [ https://a.yandex-team.ru/arc/commit/6603982 ]

* [marianastrix](http://staff/marianastrix)

 * DIR-8833: Проверять существование пользователя при его добавлении  [ https://a.yandex-team.ru/arc/commit/6605132 ]

* [feakuru](http://staff/feakuru)

 * PR from branch users/feakuru/DIR-8817-logs-cleanup

DIR-8817 disabled TVM tickets logger

DIR-8817 not logging shard selection

DIR-8817 remove unneeded logs

DIR-8817 bump tools-structured-logs  [ https://a.yandex-team.ru/arc/commit/6605131 ]

[smosker](http://staff/smosker) 2020-04-10 18:09:42+03:00

2.73
----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-8923: убрал ограничение на количество инвайтов для организаций в белом списке

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![marianastrix](https://codereview.common-int.yandex-team.ru/badges/marianastrix-...-yellow.svg)](https://staff.yandex-team.ru/marianastrix) [![neofelis](https://codereview.common-int.yandex-team.ru/badges/neofelis-...-yellow.svg)](https://staff.yandex-team.ru/neofelis)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6597847 ]

* [jsus](http://staff/jsus)

 * Change .devexp.json

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-complete-green.svg) [![marianastrix](https://codereview.common-int.yandex-team.ru/badges/marianastrix-...-yellow.svg)](https://staff.yandex-team.ru/marianastrix) [![neofelis](https://codereview.common-int.yandex-team.ru/badges/neofelis-ok-green.svg)](https://staff.yandex-team.ru/neofelis) [![smosker](https://codereview.common-int.yandex-team.ru/badges/smosker-ok-green.svg)](https://staff.yandex-team.ru/smosker)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6597355 ]

[oleglarionov](http://staff/oleglarionov) 2020-04-08 17:25:49+03:00

2.72
----

* [smosker](http://staff/smosker)

 * DIR-8857 Удаление неактивных договров при оплате

<!-- DEVEXP BEGIN -->
\****
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![marianastrix](https://codereview.common-int.yandex-team.ru/badges/marianastrix-ok-green.svg)](https://staff.yandex-team.ru/marianastrix) [![poegva](https://codereview.common-int.yandex-team.ru/badges/poegva-...-yellow.svg)](https://staff.yandex-team.ru/poegva)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6596548 ]
 * Change .arcignore

Note: mandatory check (NEED_CHECK) was skipped                                                                                                                                                                                                                                                                                                                                                                                                      [ https://a.yandex-team.ru/arc/commit/6583527 ]
 * Add ignore                                                                                                                                                                                                                                                                                                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/6583502 ]
 * Правка конфига ревьюшницы                                                                                                                                                                                                                                                                                                                                                                                                                                              [ https://a.yandex-team.ru/arc/commit/6583293 ]

* [oleglarionov](http://staff/oleglarionov)

 * DIR-8918: изменил миграцию - добавляем новый столбец fake_id и pk(fake_id, org_id)

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-complete-green.svg) [![feakuru](https://codereview.common-int.yandex-team.ru/badges/feakuru-ok-green.svg)](https://staff.yandex-team.ru/feakuru) [![kdunaev](https://codereview.common-int.yandex-team.ru/badges/kdunaev-ok-green.svg)](https://staff.yandex-team.ru/kdunaev) [![smosker](https://codereview.common-int.yandex-team.ru/badges/smosker-...-yellow.svg)](https://staff.yandex-team.ru/smosker)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6595972 ]
 * DIR-8902: фикс доставки событий

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![marianastrix](https://codereview.common-int.yandex-team.ru/badges/marianastrix-ok-green.svg)](https://staff.yandex-team.ru/marianastrix) [![denis--p](https://codereview.common-int.yandex-team.ru/badges/denis--p-...-yellow.svg)](https://staff.yandex-team.ru/denis-p)
<!-- DEVEXP END -->                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/6590747 ]
 * DIR-8427: тесты на синхронизацию с облаком

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-changes_needed-yellow.svg) [![smosker](https://codereview.common-int.yandex-team.ru/badges/smosker-ok-green.svg)](https://staff.yandex-team.ru/smosker) [![ksticks](https://codereview.common-int.yandex-team.ru/badges/ksticks-...-yellow.svg)](https://staff.yandex-team.ru/ksticks)
<!-- DEVEXP END -->                                                                                                                                                                [ https://a.yandex-team.ru/arc/commit/6589494 ]

[smosker](http://staff/smosker) 2020-04-08 12:25:24+03:00

2.71
----

* [oleglarionov](http://staff/oleglarionov)

 * DIR-8427: Потреблять list_users (#3072)

\* DIR-8427: Потреблять list_users

\* DIR-8427: small fixes

\* DIR-8427: правки

\* DIR-8427: Берем имя и фамилию для облачных пользователей из атрибутов

\* DIR-8427: Заполняем email пустой строкой, если он не передан

\* DIR-8427: правки

\* DIR-8427: ограничение окружений, в которых запускается синк


Former-commit-id: b93384359e3950355bf6323530b2394b0356c81c  [ https://a.yandex-team.ru/arc/commit/6570973 ]

* [smosker](http://staff/smosker)

 * add docker package

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![marianastrix](https://codereview.common-int.yandex-team.ru/badges/marianastrix-...-yellow.svg)](https://staff.yandex-team.ru/marianastrix) [![poegva](https://codereview.common-int.yandex-team.ru/badges/poegva-...-yellow.svg)](https://staff.yandex-team.ru/poegva)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6577663 ]
 * fix stand

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-not_started-lightgrey.svg) [![marianastrix](https://codereview.common-int.yandex-team.ru/badges/marianastrix-...-yellow.svg)](https://staff.yandex-team.ru/marianastrix) [![neofelis](https://codereview.common-int.yandex-team.ru/badges/neofelis-...-yellow.svg)](https://staff.yandex-team.ru/neofelis)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6576708 ]
 * DIR-6134 правки после переноса проекта в аркадию                                                                                                                                                                                                                                                                                                                                                                                      [ https://a.yandex-team.ru/arc/commit/6576484 ]
 * DIR-6134 Переезд в аркадию (#3074)

\*  первый подход к переезду

\*  работа над аркадией

\*  Правка для работы сборки и тестов

\*  правка create_stand

\*  правка кода

\*  правка импорта


Former-commit-id: 6387f9b2911c6315f8357d52a0f063e50ef12607                                                                                                                                                                                 [ https://a.yandex-team.ru/arc/commit/6570974 ]
 * Правка получения емейла для облачных пользователей (#3075)



Former-commit-id: d0a74618b21ace1b76053df84d3805bcd34a4e6e                                                                                                                                                                                                                                                                                                              [ https://a.yandex-team.ru/arc/commit/6570972 ]

* [nslus](http://staff/nslus)

 * ARCADIA-958 [migration] github/yandex-directory/yandex-directory  [ https://a.yandex-team.ru/arc/commit/6576150 ]

[smosker](http://staff/smosker) 2020-04-06 12:13:42+03:00

2.70
----
 * DIR-8884 Разблокируем домен если нужно при удалении организации (#3067)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2141214f5 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-04-02 13:34:40+03:00

2.69
----
 * DIR-8898 не падаем на отправке событий облачных пользователей (#3073)             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0e30de586 ]
 * DIR-8856 Проверка на существование организации при создании пользователя (#3070)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eee4f219c ]
 * DIR-8629 Не 500 тим при ошибках вебмастера (#3069)                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d3f898524 ]
 * DIR-8564 Не 500 на кривой дате от мониторинга (#3066)                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6935fb474 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-04-02 13:11:06+03:00

2.68
----

* [Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru)

 * DIR-8778: Не отдавать в ручке Директории счётчик Метрики после его удаления в Метрике (#3064)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/91cfadedb ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * У старого домена для тестов истек срок годности, добавил новый (#3065)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/19b0e0da4 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-30 19:37:14+03:00

2.67
----

[Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru) 2020-03-26 18:05:59+03:00

2.66
----
 * DIR-8478: Редиректить в Почту по инвайт-ссылкам из Почты для Бизнеса (поддержать параметр service_slug) (#3062)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0121bcc4e ]

[Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru) 2020-03-26 18:05:23+03:00

2.65
----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8863 Правка отрезка облачных уидов + поддержка выдачи типа организации в ручке users (#3063)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2cd362e4d ]

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * DIR-8837 проверяем на BillingUnknownError (#3057)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7d9ef481d ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2020-03-26 12:30:12+03:00

2.64
----

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * DIR-8333 BB Emu (#3037)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d601b13a3 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8634 Не создаем новых внешних админов (#3054)                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ae7c03b19 ]
 * DIR-7469 Отдаем в ручке /ownership-info/ preferred_host (#3061)         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8b4f7e26e ]
 * DIR-8835 Добавление права на использование интерфейса коннекта (#3060)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3858c1e54 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-8847: Возвращаем в ответе в поле links объект (#3058)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/20c98f37e ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-25 15:21:00+03:00

2.63
----
 * DIR-8844 Не билим трекер для организаций до 100 людей, до конца сентября (#3059)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6917f315b ]
 * DIR-8825 Правка проверки на ответственного при увольнении пользователя (#3055)    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/364dde4be ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-24 12:36:38+03:00

2.62
----

[Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru) 2020-03-23 16:59:12+03:00

2.61
----
 * DIR-7075: [Directory] Ручка, возвращающая данные о сервисах (#3035)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/326c85e72 ]

[Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru) 2020-03-23 16:26:43+03:00

2.60
----
 * DIR-8848: Если передана пустая строка в label отдела/команды приводим ее к None (#3056)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a67b5a963 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2020-03-20 18:51:01+03:00

2.59
----

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-8574: Поддержать ручку с метаданными alice4business (#3053)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9db6577b2 ]

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * Remove unused imports  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dc918dc60 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2020-03-20 13:03:29+03:00

2.58
----
 * DIR-8104 Ручка создания облачной организации и статуса включения сервиса (#3051)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/49090b1be ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-19 12:08:34+03:00

2.57
----

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-8560: Переезд в облачную zora-online (#3050)                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9154813c1 ]
 * DIR-8599: Поддержать сортировку по дате присоединения к организации (#3046)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/67a99804c ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8586 Не даем пользователям расширенного коннекта состоять в нескольких организациях (#3044)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/916e391eb ]
 * DIR-8596 Обновляем ревизии всех организаций пользователя при добавлении в новую (#3045)          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2eb0cf9e7 ]
 * DIR-8598 Ограничение на количество организаций (#3043)                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/10b1abae0 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-17 16:52:13+03:00

2.56
----
 * DIR-8793 add int-qa to envs (#3049)                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bc768c5ff ]
 * DIR-8813 SMS texts for domain confirmation (#3052)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2ec053057 ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2020-03-17 15:03:49+03:00

2.55
----
 * DIR-8808 Правка выдачи avatar_id (#3048)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/25b00e63d ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-13 19:41:33+03:00

2.54
----
 * DIR-8802 Не пытаемся отправить смски с переводами которых нет (#3047)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2e834f568 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-13 13:46:42+03:00

2.53
----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8410 Клиент для работы с облаком (#3028)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5aef216f2 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-6450: поиск по nickname в логах организации в каталоге (#3036)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6749f58df ]

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * DIR-8630 Правка удаления организации с доменом (#3041)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b7511c42e ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-11 12:38:58+03:00

2.52
----
 * DIR-8541 Убираем лишние трейсы part 2 (#3042)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/98a5e77bc ]
 * DIR-8482 Переходим на pytest (#3038)           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/90b21a477 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-05 20:16:10+03:00

2.51
----
 * DIR-8639 правка для привязки ресурсов алисы (#3039)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b7ec223d8 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-04 18:45:55+03:00

2.50
----
 * DIR-8113 fix field inconsistency  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/92548df4a ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2020-03-03 14:10:43+03:00

2.49
----
 * DIR-8595 фиск ошибки синка организаций (#3034)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9b8b039e2 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-03-03 12:59:56+03:00

2.48
----
 * DIR-8113 json bb (#3005)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5f4474cdd ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2020-03-02 12:15:41+03:00

2.47
----
 * DIR-8565 Не билим все кроме трекера (#3031)                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0ad42b59f ]
 * DIR-8592 Правка выбора организации для внешних админов (#3033)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1ff94e4eb ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-26 14:48:10+03:00

2.46
----
 * DIR-8368: Убрать ограничение на несколько организаций (#3029)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2b3887750 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2020-02-25 17:41:02+03:00

2.45
----
 * DIR-8397: Поддержка обратной совместимости апи для пользователя в нес… (#3027)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/15b1dd380 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2020-02-25 15:18:30+03:00

2.44
----
 * DIR-8284: Поправить проверку уникальности никнейма (#3026)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0a13428c2 ]

[Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru) 2020-02-25 14:06:50+03:00

2.43
----
 * DIR-8571 Все время ходим в биллинг онлайн для показа баланса (#3032)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f85a6ca0e ]
 * DIR-8534 Правка ролей для алисы (#3030)                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9b733c49f ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-20 16:42:51+03:00

2.42
----
 * DIR-8540 Убираю ошибку при запуске таски (#3025)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a1035fda2 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-17 17:37:21+03:00

2.41
----

* [Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru)

 * DIR-8353: Добавила поля фильтрации и тесты (#3021)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d5a706575 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-13 13:54:05+03:00

2.40
----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8187 pdf из биллинга (#2980)                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/716a71bbc ]
 * DIR-8451 Добавил переводы в проект + разблокируем домен сразу в отдельной транзакции (#3023)        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4f9f9b9c4 ]
 * DIR-8459 Смена хостов у прод базы (#3024)                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/162fecd88 ]
 * DIR-8531 Не 500 при повторной постановке задачи вебмастера в очередь (#3020)                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/31cfb5702 ]
 * DIR-8532 Не выводим организации где пользователь внешний админ в ручке /bind/organizations (#3022)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/44f9ddfa7 ]

* [Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru)

 * DIR-8188 Избавиться от has_owned_domains в мета базе (#3012)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/665a46194 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-13 13:13:24+03:00

2.39
----

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-11 17:11:34+03:00

2.38
----
 * DIR-8459 меняем хосты базы  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9e82c8a38 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-11 17:10:37+03:00

2.37
----
 * Понижаю уровень лога  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/77b9c89f3 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-11 16:30:26+03:00

2.36
----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8484 Делаем тех домен мастером при его создании через domain/connect (#3019)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/431143e73 ]

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * DIR-8300 Анализ трейсов (#3013)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4eb299cc7 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-11 15:36:49+03:00

2.35
----
 * DIR-8459 Меняем хост в первого шарда                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/192a111a8 ]
 * DIR-8222 Учитываем отсутствие полей в ответе жандарма (#3015)                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/faee6dfc7 ]
 * DIR-8052 Добавил обработку yarm rate error + пишу в логи урл по которому ходили (#3014)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9241e7bc4 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-11 15:05:53+03:00

2.34
----

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2020-02-11 13:50:28+03:00

2.33
----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8480 Не выдаем 10гб на диске (#3018)                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d3ec8f497 ]
 * DIR-8270 не 500 тим при повторном сохранении биллинговой информации (#3016)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c40f8e882 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-8262: переписал команду отключения сервисов по триалу (#3017)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/44299d3cd ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2020-02-11 13:48:58+03:00

2.32
----
 * DIR-8459 убираю лишний хост  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4114ed9f5 ]
 * Удаляю ненужный тест         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d67074d59 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-10 18:13:31+03:00

2.31.1
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8095 не отправляем события об облачных организациях без явной подписки (#3011)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f6a81fa69 ]

* [Dmitrii Sergeev](http://staff/9913+d1568@users.noreply.github.yandex-team.ru)

 * DIR-6528 Перенести build_docs в сборку докер-образа (#3010)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4b964ca4a ]

[Dmitrii Sergeev](http://staff/d1568@yandex-team.ru) 2020-02-10 14:10:49+03:00

2.31.0
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 2.30.0 → 2.31.0                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/64b45422c ]
 * DIR-8182 Ручка для получения формы оплаты через траст (#2977)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ba90c29c7 ]
 * DIR-8334 выбираем шард рандомно (#3009)                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fd99d4f08 ]

* [Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru)

 * DIR-8405: Сделать ручку для получения списка организаций с которыми можно связать ресурс (#3008)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b63f5db2d ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-02-04 12:01:58+03:00

2.30.0
------

* [Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru)

 * Bump version: 2.29.0 → 2.30.0                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d51b16234 ]
 * DIR-8170: Пятисотим на плохих токенах (#3004)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/067504718 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8441 Правка удаление ресурса в случае отсутствия ответственного за сервис (#3007)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d14f6bf8a ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7544: Исправление удаления организации с внутренним админом (#3006)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8c24a88cf ]

[Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru) 2020-01-30 18:14:01+03:00

2.29.0
------
 * Bump version: 2.28.0 → 2.29.0                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/51bb693cb ]
 * DIR-8385: В ручке применения инвайта запускать проставления атрибута … (#3003)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e4b8e20fb ]

[Mariia Ibragimova](http://staff/marianastrix@yandex-team.ru) 2020-01-28 13:09:38+03:00

2.28.0
------
 * Bump version: 2.27.0 → 2.28.0                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9b6f71384 ]
 * hotfix: правка ручки получения организаций пользователей  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f51fbdd46 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2020-01-27 15:36:34+03:00

2.27.0
------
 * Bump version: 2.26.0 → 2.27.0                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c092f1c71 ]
 * DIR-8100 dirty hack for wrong encodings (#2997)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/557b43b31 ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2020-01-24 14:04:52+03:00

2.26.0
------
 * Bump version: 2.25.0 → 2.26.0                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/836e06968 ]
 * DIR-8366: Фикс ошибки 'Service None not found' в ручке получения прав (#3001)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a7e35df12 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2020-01-22 12:50:32+03:00

2.25.0
------
 * Bump version: 2.24.0 → 2.25.0                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/69b894796 ]
 * DIR-8371 Правка работы параметра для внешнего админа (#3000)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/aef26001b ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-01-21 11:38:04+03:00

2.24.0
------
 * Bump version: 2.23.0 → 2.24.0                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d275ff4b2 ]
 * DIR-8253 Правка добавления пользователя при рассинхроне мастер/алиас с паспортом (#2996)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2b2f7253c ]
 * DIR-8156 Правка инвайт линков (#2998)                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4142f649d ]
 * правка определения облачного пользователя (#2999)                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2eb4f1e26 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-01-20 12:26:53+03:00

2.23.0
------
 * Bump version: 2.22.0 → 2.23.0                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f317871a9 ]
 * DIR-8311: Добавил обработку ошибки от биллинга при заполнении биллинговой инфы (#2989)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/287cdabc0 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2020-01-16 15:15:36+03:00

2.22.0
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 2.21.0 → 2.22.0                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/500e5897c ]
 * DIR-8246 Добавил выдачу организаций где пользователь админ (#2988)                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1b8759ec7 ]
 * DIR-8321 Не отгружаем данные облачных пользователей (#2992)                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/249958a07 ]
 * DIR-8194 Не ломаемся при попытке добавить алиас который уже есть в паспорте (#2994)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2c91a85e2 ]
 * DIR-8296 Ходим из int-qa в тестовый билинг (#2995)                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bbbfd7b48 ]
 * DIR-8107 Не ходим в паспорт для облачных пользователей (#2991)                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3a4bdd5f3 ]
 * DIR-8320 Работа с облачными uid'ами (#2990)                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/630a0834c ]

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * DIR-8290 подмешиваем org_id внутри SyncExternalIDs (#2993)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/801eb3997 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2020-01-14 16:52:15+03:00

2.21.0
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8280 Добавляю роли для алисы (#2986)                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/079aef113 ]
 * DIR-8090 Устраняем No master domain in Passport (#2982)                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0c5742eaf ]
 * DIR-8082 Делаем таску обновления лицензий при выдаче синхронной (#2984)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c727dda0c ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-8121: При инвайте портального пользователя брать email из бб (#2985)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b028ae2b2 ]

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * Bump version: 2.20.0 → 2.21.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0505da9bf ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2019-12-30 12:59:23+03:00

2.20.0
------
 * Bump version: 2.19.0 → 2.20.0                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a0a066e91 ]
 * DIR-8210 поднимаем приоритет у таски (#2987)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7d5b6280c ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-12-27 18:38:22+03:00

2.19.0
------
 * Bump version: 2.18.0 → 2.19.0                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d1a6d8ac1 ]
 * Добавил поддержку заголовка Access-Control-Allow-Credentials  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b416772fc ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-12-26 14:43:25+03:00

2.18.0
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8089 правка проверки прав на удаление отношения (#2981)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5f80010b4 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 2.17.0 → 2.18.0                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/684754a37 ]
 * DIR-8085: Попытка автоматического разрешения ситуации, когда домен ес… (#2979)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1ea12472f ]
 * DIR-8257: Поддержать CORS в апи (#2983)                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1d6054b69 ]

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * Updated README for python3  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e64f86bca ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-12-26 11:14:13+03:00

2.17.0
------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 2.16.0 → 2.17.0              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1bfb5d7a7 ]
 * DIR-7238: Выпилить лишние метрики (#2978)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a33317ec4 ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-8243 правки по переиспользованию плательщика (#2976)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f93b8efed ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-12-23 12:26:08+03:00

2.16.0
------
 * Bump version: 2.15.0 → 2.16.0                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7f0d74a64 ]
 * DIR-8192 added secret key to InviteUseView.post (#2970)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/61619d448 ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2019-12-20 15:43:01+03:00

2.15.0
------
 * Bump version: 2.14.0 → 2.15.0                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/00c9c39e3 ]
 * DIR-8185: Добавить тип плательщика в OrganizationSubscriptionInfoView (#2975)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e4620054 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-12-20 11:57:45+03:00

2.14.0
------
 * Bump version: 2.13.0 → 2.14.0                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ec2370f53 ]
 * DIR-8181: В ручке баланса добавить параметр для обновления данных онлайн (#2973)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/60c799e13 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-12-19 12:12:57+03:00

2.13.0
------
 * Bump version: 2.12.0 → 2.13.0                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dad52753c ]
 * DIR-8199 Добавил в зависимости pyOpenSSL (#2974)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6a960e088 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-12-17 11:30:33+03:00

2.12.0
------

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * удалены метрики build_users_count_for_dashboard и build_organizations_count_for_dashboard, запросы очень грузят базу (#2972)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dfbcaa53a ]

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * Bump version: 2.11.0 → 2.12.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9e923c9bf ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2019-12-16 16:49:30+03:00

2.11.0
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8172 Возвращаем 422 при удалении организации с сотрудниками (#2967)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fe7124944 ]
 * DIR-8199 Добавил requests[security] (#2971)                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eea06f231 ]

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * Bump version: 2.10.0 → 2.11.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cae96e591 ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2019-12-16 16:00:06+03:00

2.10.0
------
 * Bump version: 2.9.0 → 2.10.0                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/de20a77be ]
 * DIR-8203 разрешил порталам управлять почтой (#2969)      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1b797213e ]
 * DIR-8105 fix for org deletion with blocked bots (#2968)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/36bc2a878 ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2019-12-16 15:31:29+03:00

2.9.0
-----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8006 Выводим source/created в выдаче ручек (#2966)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a147bead4 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 2.8.0 → 2.9.0                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8439d632e ]
 * releasing version 2.8.0                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d72bb022e ]
 * DIR-8007: Запрет на выключение календаря/почты/диска (#2960)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/db4e03ee6 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-12-12 14:32:35+03:00

2.8.0
-----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-8006 Выводим source/created в выдаче ручек (#2966)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a147bead4 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-8007: Запрет на выключение календаря/почты/диска (#2960)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/db4e03ee6 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-12-12 14:26:12+03:00

2.8.0
-----

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-8165 новый продукт айди для диска (#2965)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0b77a80ab ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 2.7.0 → 2.8.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e495cb3d ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-12-11 12:56:20+03:00

2.7.0
-----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 2.6.0 → 2.7.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/af3dfa5d6 ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-8114 в функции create_user_from_bb_info добавлена проверка, что пользователь имеет отношение к организации (#2959)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/711d030ba ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-12-10 15:37:20+03:00

2.6.0
-----

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * hotfix: правка сеттингов                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/be190b9b1 ]
 * Dir 8159 (#2964)                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5250d7940 ]
 * DIR-8159: фикс генерации токенов (#2963)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e755cf530 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 2.5.0 → 2.6.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/05519fb6c ]
 * Bump version: 2.4.0 → 2.5.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b7e5aed99 ]
 * Bump version: 2.3.0 → 2.4.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0a9d08a48 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-12-10 14:10:34+03:00

2.3.0
-----

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7984 теперь всегда используем существующий client_id пользователя… (#2957)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e5e966ec0 ]
 * уровень логирования настраивается через перменную LOG_LEVEL (#2962)             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/67a1a67e5 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 2.2.0 → 2.3.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9cd4142a8 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-12-10 11:44:22+03:00

2.2.0
-----
 * Bump version: 2.1.0 → 2.2.0                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/36316f670 ]
 * DIR-7989 fix https://jing.yandex-team.ru/files/smosker/2019-12-09_14-38-16.png  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7c6c3ecfb ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-12-09 14:39:52+03:00

2.1.0
-----
 * Bump version: 2.0.0 → 2.1.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b69d80245 ]
 * DIR-7989 fix sms             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7257f1c78 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-12-09 14:26:31+03:00

2.0.0
-----

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * fix: изменил имя поля в ручке для лего  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/968997469 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 1.23.0 → 2.0.0                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a2a770b42 ]
 * DIR-7868 DIR-7869 DIR-7989 Python 3 (#2936)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d280924b6 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-12-09 12:50:55+03:00

1.23.0
------

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-8115 защита от спама в ручке /invites/emails/ (#2961)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ca76452d5 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 1.22.0 → 1.23.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1bebac5ae ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-8031: Добавил ручку получения организаций по списку пользователей (#2958)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dd2c96d6c ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-12-06 12:31:29+03:00

1.22.0
------
 * Bump version: 1.21.0 → 1.22.0                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/10832ccf2 ]
 * DIR-8009: Добавил проверку на наличие пользователя в метабазе, чтобы … (#2956)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b9986e94f ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-12-04 14:47:44+03:00

1.21.0
------
 * Bump version: 1.20.0 → 1.21.0                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/664135581 ]
 * DIR-7921 remove update of ChangeLog.rst via bumpversion  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f489aba7e ]
 * DIR-7921 выпилил changelog и api-changelog (#2954)       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b787b3b96 ]

[Dmitry Orlov](http://staff/feakuru@yandex-team.ru) 2019-12-02 13:20:39+03:00

1.20.0
------

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * Added personal config  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bfe3124dd ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 1.19.0 → 1.20.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c4df6895e ]
 * Обновлён ChangeLog.rst.        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3b36293ca ]
 * правка хоста idm (#2955)       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/66dd5cfa5 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-11-28 16:57:06+03:00

1.19.0
------

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7747 Удален таск UnsubscribeAllMaillistsTask (#2952)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f802b4ae7 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 1.18.0 → 1.19.0                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0d3244f5c ]
 * Обновлён ChangeLog.rst.                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/51dea0a33 ]
 * Bump version: 1.17.0 → 1.18.0                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0b4f393d3 ]
 * Обновлён ChangeLog.rst.                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d34ac7972 ]
 * DIR-8055 Добавлена проверка на то, что только chief может привязывать ресурс директа (#2953)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2a5fa3e09 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-11-28 14:49:32+03:00

1.17.0
------
 * Bump version: 1.16.0 → 1.17.0                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/00875456c ]
 * Обновлён ChangeLog.rst.                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8f7c22884 ]
 * DIR-7992 Правка повторной выдачи прав и передачи кампании от агенства (#2951)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/994af2ed3 ]
 * DIR-7972 Правка проверки прав для управления ролями директа (#2949)            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/34b9afb8c ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-11-26 18:22:03+03:00

1.16.0
------
 * Bump version: 1.15.0 → 1.16.0                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/97027937f ]
 * Обновлён ChangeLog.rst.                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/efe9098cb ]
 * DIR-7861: Правки интеграции с idm и direct (#2926)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/13303915c ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-11-26 11:43:53+03:00

1.15.0
------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 1.14.0 → 1.15.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/72fc2ba48 ]
 * Обновлён ChangeLog.rst.        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/187f8b840 ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-6916 Учитываем существование внешних роботов в create-robots (#2950)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e5b6304e5 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-11-25 16:33:17+03:00

1.14.0
------

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * удален ticket_age_checker_thread (#2948)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e706d9834 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 1.13.0 → 1.14.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cccb63a86 ]
 * Обновлён ChangeLog.rst.        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/647ca3e81 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-11-21 12:50:30+03:00

1.13.0
------

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-8013 тех оптимизация (#2947)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/13e4c330e ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 1.12.0 → 1.13.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cd12317aa ]
 * Обновлён ChangeLog.rst.        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a048db5fa ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-11-21 12:22:41+03:00

1.12.0
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 1.11.0 → 1.12.0                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1a1895662 ]
 * Обновлён ChangeLog.rst.                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a21d6d051 ]
 * DIR-7654 Поправили способ получения ip адреса при восстановлении доступа к организации (#2944)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f0779dd0c ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7945: Ручка для лего со списком организаций. (#2943)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/59831dc60 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-11-15 12:29:16+03:00

1.11.0
------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7859 Проверяем наличие client_id в организации и при dryrun=1 (#2938)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f5146e030 ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7958 новые индексы (#2941)                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7584f61f9 ]
 * DIR-7953 исправлен подсчет vip признака для платных сервисов (#2942)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/17f337f0f ]
 * DIR-7936 разрешаем редактировать label у рассылок (#2937)             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/61b63c078 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 1.10.0 → 1.11.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/453fbb2af ]
 * Обновлён ChangeLog.rst.        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d184d3682 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-11-13 12:39:37+03:00

1.10.0
------
 * Bump version: 1.9.0 → 1.10.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e9b452f6e ]
 * Обновлён ChangeLog.rst.       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/158e15f95 ]
 * changelog                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/abcacf95c ]
 * fixes DIR-6242                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/37f562636 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-11-12 16:44:10+03:00

1.9.0
-----
 * changelog                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ee0f14eab ]
 * Bump version: 1.8.0 → 1.9.0                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/091dcd098 ]
 * Обновлён ChangeLog.rst.                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5cefd7fed ]
 * DIR-6242 структурированные логи (#2940)           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c9cb4d5ab ]
 * Revert "DIR-6242 структурированные логи (#2928)"  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0f0ae93ed ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-11-12 11:38:40+03:00

1.8.0
-----

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * changelog                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d9d573a14 ]
 * Bump version: 1.7.0 → 1.8.0              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9c9f031d1 ]
 * Обновлён ChangeLog.rst.                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/00e74957c ]
 * DIR-6242 структурированные логи (#2928)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/38502dd06 ]

* [Dmitry Orlov](http://staff/feakuru@yandex-team.ru)

 * Gitignored .vscode service folder  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/46ce1cca0 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-11-11 12:28:23+03:00

1.7.0
-----
 * Bump version: 1.6.0 → 1.7.0                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b79af3f02 ]
 * Обновлён ChangeLog.rst.                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e8d04dd3a ]
 * DIR-7641: Оповещение при отвязывании счетчика (#2935)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/55a516959 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-11-07 13:35:16+03:00

1.6.0
-----
 * Bump version: 1.5.0 → 1.6.0                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dd056c873 ]
 * Обновлён ChangeLog.rst.                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7b82bb70d ]
 * DIR-7942 Добавляем avatar_id в недостающие ручки (#2933)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fd93f1ed3 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-10-31 12:34:13+03:00

1.5.0
-----

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7941 доработки по диску (#2932)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b2bef4339 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 1.4.0 → 1.5.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0755b9b1f ]
 * Обновлён ChangeLog.rst.      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/23d3b6d4c ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-10-29 18:10:13+03:00

1.4.0
-----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7931 Выдаем avatar_id во всех нужных ручках (#2930)          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/00b27d70c ]
 * DIR-7767 начинаем сохранять историю действий с ресурсом (#2925)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/27e394da2 ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7900 запоминать service_id от диска (#2929)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2e94d9779 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 1.3.0 → 1.4.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/115911695 ]
 * Обновлён ChangeLog.rst.      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e990919fa ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-10-28 16:10:29+03:00

1.3.0
-----

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7661 Не 500тим при создании пользователя с некорректным id департамента  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/05d6016ab ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 1.2.0 → 1.3.0                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/620ca538e ]
 * Обновлён ChangeLog.rst.                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6b1e65db7 ]
 * DIR-7785 правильный продукт в балансе                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d5561c42c ]
 * DIR-7815 При увольнении пользователя отбирать место на диске  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/242682eec ]
 * DIR-7785 доделки2                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/27d7fcc88 ]
 * DIR-7785 доделки                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5177d64dd ]
 * DIR-7785 не даем выдать место больше, чем 1 раз               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e0b6374e2 ]
 * DIR-7785 справлена проверка словаря с ценами                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a9c449c10 ]
 * DIR-7785 правки                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2baea6dda ]
 * DIR-7785 платный диск                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/97cc21f22 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-10-24 15:51:06+05:00

1.2.0
-----
 * Bump version: 1.1.0 → 1.2.0                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cd5eefcea ]
 * Обновлён ChangeLog.rst.                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/49484b3f1 ]
 * DIR-7600 Отдаем avatar_id если он запрошен в fields (#2917)                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/21c755fa1 ]
 * DIR-7842 Ограничение на 1000 пользователей в организации по умолчанию (#2923)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5c489acfe ]
 * DIR-6780 Обновление версий библиотек (#2918)                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7f041023e ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-10-23 13:52:26+03:00

1.1.0
-----
 * Bump version: 1.0.0 → 1.1.0                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9726c44d6 ]
 * Обновлён ChangeLog.rst.                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a267bcd5f ]
 * Удалены старые коблеки CORP_MAILLIST_CALLBACK для org_id 34          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6e770cb62 ]
 * Bump version: 0.397.0 → 1.0.0                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8830da126 ]
 * Обновлён ChangeLog.rst.                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/113291797 ]
 * DIR-7675 правильные колбеки                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/177abe61e ]
 * DIR-7675 изменила тест                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/833aee843 ]
 * DIR-7675 вернула колбек диска                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5ab2123a5 ]
 * DIR-7675 директория без пдд                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d67bbfc18 ]
 * DIR-7922 При восстановлении пользователя апдейтим 1017 атрибут в бб  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7711d2b9e ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-10-23 13:52:31+05:00

0.397.0
-------
 * Bump version: 0.396.0 → 0.397.0                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/14125d093 ]
 * Обновлён ChangeLog.rst.                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a09087613 ]
 * DIR-1638 Правка получения данных от справочника  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c3b5b3d15 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-10-15 17:48:38+03:00

0.396.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7800 Логирование работы с ресурсами (#2912)                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e31910f7a ]
 * DIR-7904 Даем возможность создавать организации с tr локалью (#2920)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3da8e901e ]
 * DIR-7350 Правка работы функции lang_for_notification (#2916)          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9d3ae9b3d ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 0.395.0 → 0.396.0                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b27a75d0b ]
 * Обновлён ChangeLog.rst.                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a61b84d7e ]
 * DIR-7885: Поправил тесты                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/060478713 ]
 * DIR-7885: Починка получения статуса делегированности из жандарма  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/49a101b34 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-10-15 14:00:15+03:00

0.395.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7897 Не 500тим в случае ошибок от сервисов в ручке полученния данных о ресурсах (#2915)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/67356570c ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 0.394.0 → 0.395.0                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c28f12ac7 ]
 * Обновлён ChangeLog.rst.                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9f1c9e0cc ]
 * DIR-7453: Реализация связывания ресурса директа (#2910)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/465af36cc ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-10-14 11:42:17+03:00

0.394.0
-------
 * Bump version: 0.393.0 → 0.394.0                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8a6f7d06c ]
 * Обновлён ChangeLog.rst.                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c76be9f8b ]
 * DIR-7874 Разрешаем can_users_change_password в каталожной ручке actions (#2911)      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1d88666a8 ]
 * DIR-7725 Выводим поясняющую информацию при ошибке UserIsAlreadyInAnotherOrg (#2903)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7b12409d7 ]
 * DIR-7669 Ходим в IDM при отвязывании ресурса (#2908)                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7fb3a872e ]
 * DIR-7244 отображение данных по ресурсу справочника (#2909)                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/89a85ecf8 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-10-10 13:04:50+03:00

0.393.0
-------
 * Bump version: 0.392.0 → 0.393.0                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c201c3ba2 ]
 * Обновлён ChangeLog.rst.                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a4d4ddd96 ]
 * Добавил changelog                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/594bca4f8 ]
 * DIR-7384: При смене ответственного за директ, новый ответственный становится владельцем ресурсов Директа (#2901) (#2906)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f1f1d71f1 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-10-03 15:45:36+03:00

0.392.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7810 Выгружаем timezone для call центра в формате +03:00 (#2898)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f94d3577f ]
 * DIR-7639 Доработки b2b клиента idm                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5cc23c630 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7640: Сделал обязательным передачу заголовка X-UID           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ae64b2cf9 ]
 * DIR-7640: Вернул возможность не передавать пользователя в ручку  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ee23a4f0d ]
 * DIR-7640: Доработка просмотра списка выданных ролей              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/da539664f ]
 * DIR-7625: добавил логирование                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/69eaa5aa9 ]
 * DIR-7625: Реализовал выдачу ролей через idm                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b9625e804 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.391.0 → 0.392.0                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1f8a36bea ]
 * Обновлён ChangeLog.rst.                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b661ae0cb ]
 * DIR-7783 Выводим информацию о количестве ресурсов и ответственном (#2904)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/109066d51 ]
 * DIR-7841 Правка порядка вызова проверок при привязывании ресурса (#2905)   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/39e305a73 ]
 * Правка тестов (#2902)                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c7f5d06f9 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * DIR-7658: Исправлено логгирование unhangled exception в случае, когда в описании ошибки есть юникодные символы. (#2897)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0255b1d3d ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-10-03 12:22:43+03:00

0.391.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Описание ошибок в unicode  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/82d9f739a ]
 * Фикс тестов                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/de613a8ca ]
 * Фикс тестов                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/10d92c1a3 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.390.0 → 0.391.0                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2fdfb18b1 ]
 * Обновлён ChangeLog.rst.                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ca9a48ddb ]
 * Поправлена опечатка.                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/276a79376 ]
 * DIR-7683 Поправлена 500 ошибка в ручке who-is.                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/373c0350c ]
 * DIR-7708: Исправлена 500 ошибка в случае, когда нам вместо ПДД токена передают какой-то мусор.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/66a234075 ]
 * DIR-6534: Во внутренней админке Коннекта - Каталоге, теперь можно выдавать групповые доступы.   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/283fb9f65 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-09-30 13:49:10+03:00

0.390.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.389.0 → 0.390.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f3871b6f8 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fda2ff358 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7625: Реализовал выдачу ролей через idm (#2887)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fbf8f525b ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-09-27 18:14:59+03:00

0.389.0
-------

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * DIR-7752: Добавлен скрипт fix-duplicate-maillists, которым я исправлял рассинхроны в таске DIR-7752.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/01171c974 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.388.0 → 0.389.0                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dbb0e262f ]
 * Обновлён ChangeLog.rst.                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/29b360faa ]
 * DIR-7651 Проверка связи пользователя с client_id  при запросе прав (#2889)               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b1b1a5b99 ]
 * DIR-7818 Не задваиваем права для ответственного (#2892)                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f290a202d ]
 * DIR-7498 Запрещать удаление организации с ресурсами метрики/директа/справочника (#2891)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7d4548f96 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-09-27 13:43:41+03:00

0.388.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.387.0 → 0.388.0                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/730bd6533 ]
 * Обновлён ChangeLog.rst.                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2057a72c3 ]
 * DIR-7804 Правка таски check_resource_existence (#2888)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/598d9be41 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7639 Доработки b2b клиента idm (#2884)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/09ed18542 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-09-26 12:40:59+03:00

0.387.0
-------
 * Bump version: 0.386.0 → 0.387.0                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f3ab96f35 ]
 * Обновлён ChangeLog.rst.                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5da72400e ]
 * Добавлен Changelog.                                                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2dac8844a ]
 * Поправлена опечатка.                                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f75b89a5d ]
 * Откладываем таск создания рассылки all на 15 секунд.                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/791f74bc6 ]
 * DIR-7755: Исправлена ошибка из-за которой пользователь терял некоторые права после добавления в организацию домена yandex.ru.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d902fe71a ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-09-25 16:47:12+03:00

0.386.0
-------
 * Bump version: 0.385.0 → 0.386.0                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1ac226f73 ]
 * Обновлён ChangeLog.rst.                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ee0683755 ]
 * DIR-7763: Теперь при включении сервиса рассылок мы не будем вычищать правила фуриты для организаций принадлежащих Яндексу.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e54c9a158 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-09-19 16:42:45+03:00

0.385.0
-------
 * Bump version: 0.384.0 → 0.385.0                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/77118e538 ]
 * Обновлён ChangeLog.rst.                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8de8269e0 ]
 * DIR-7761: Исправлена ошибка TypeError: 'type' object has no attribute '__getitem__' из-за которой пятисотила ручка who-is.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dbc333343 ]
 * DIR-7692: Исправлена 500 в ручке /subscription/services/<service_slug>/licenses/request/<confirm|deny>/.                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d81efe680 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-09-19 09:55:37+03:00

0.384.0
-------
 * Bump version: 0.383.0 → 0.384.0                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0033c5a64 ]
 * Обновлён ChangeLog.rst.                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7b749f7f1 ]
 * Поправлен падавший тест.                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/330af930a ]
 * Разблокировка домена переделана на асинхронный таск, на случай если в процессе подтверждения были ошибки.             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1262f7c53 ]
 * DIR-7320: Теперь в случае ошибки при подтверждении домена, должны откатываться изменения и в основной базе и в мета.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e9623ee39 ]
 * Исключение ExternalServiceError переименовано в IDMError.                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ca9ea4d3c ]
 * Исправил ошибку в тексте сообщения об ошибке.                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6cc058759 ]
 * Убран лишний set_trace.                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/41fcf012c ]
 * Поправлены ошибки в тестах.                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3a12f9f00 ]
 * Добавлена возможность генерировать файл с описанием ошибок для танкера.                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/88f0f0a19 ]
 * В команду api_errors добавлена возможность сохранить описания ошибок в tjson формате, годном для заливки в Танкер.    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/158bca877 ]
 * Добавлены описания ошибкам Fouras, Gendarme и MDS.                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/26f1d3fe2 ]
 * Теперь больше нельзя инстанциировать исключения унаследованные от APIError, если у них не указан description.         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2a9372123 ]
 * Добавлена команда api-errors, для вывода описания исключений.                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/97e7a69fc ]
 * Исключение APIError разделено на кучку мелких.                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e52bfb335 ]
 * DIR-6694: Добавлены описания исключений, унаследованных от APIError.                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/23ce8dd28 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-09-18 08:59:31+03:00

0.383.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7510 правка кода                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6b827b35a ]
 * DIR-7510 Проверяем что пользователь состоит в организации при привязке ресурса  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1eebff454 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7732: changelog        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ae997a520 ]
 * DIR-7732: Фикс пагинатора  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7be7dbaad ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7697 Добавлен список ролей для сервиса Директ  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1d77dccb3 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.382.0 → 0.383.0                                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a3fc837bf ]
 * Обновлён ChangeLog.rst.                                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2124a5941 ]
 * DIR-7751 Исправлен баг из-за которого нельзя было удалить организацию в которой из-за ошибки DIR-7752 uid рассыки all@ был из другого домена.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ae64ce070 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-09-17 15:50:07+03:00

0.382.0
-------
 * Bump version: 0.381.0 → 0.382.0                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/63bbd6f48 ]
 * Обновлён ChangeLog.rst.                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9e7d61872 ]
 * DIR-7009 исправлен тест                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3fa9d6c25 ]
 * DIR-7009 выгрузка контактов админов только для трекера  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/836dc2018 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-09-17 17:35:17+05:00

0.381.0
-------
 * Bump version: 0.380.0 → 0.381.0                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a578bcf0e ]
 * Обновлён ChangeLog.rst.                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b363e8ca2 ]
 * DIR-7009 правки                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/02971f3c3 ]
 * DIR-7009 правки                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/578f05066 ]
 * DIR-7009 сохраняем номера телефонов админов в таблицу с аналитикой  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1d415611d ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-09-16 15:02:11+05:00

0.380.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7687: changelog                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bbaa84f36 ]
 * DIR-7687: правки                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/70a3f74a1 ]
 * DIR-7687: Реализация метода get_roles в IDMB2BApiClient  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9477c8da1 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.379.0 → 0.380.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/096acef7b ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/43df5c1f2 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-09-12 17:19:16+03:00

0.379.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7707 не даем выдавать права на счетчик метрики если у пользователя уже есть другое право на счетчик  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/67d99874d ]
 * DIR-7642 правка орфографии                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b699a4f21 ]
 * DIR-7642 правка по замечаниям                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b1e79d800 ]
 * DIR-7642 добавил логирование                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2cfd7fef4 ]
 * DIR-7642 Выдаем права ответственному при привязке ресурса                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7ce766a5e ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7679 Поправлены настройки                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7c316a870 ]
 * DIR-7679 fix typo                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2340ed496 ]
 * DIR-7679 Поиск портальных учеток в GET who-is  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/434d79c49 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.378.1 → 0.379.0                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/64a42c90a ]
 * Обновлён ChangeLog.rst.                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cb7b568a5 ]
 * Добавлен ченьджлог, забытый Вовой.                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9373ce66a ]
 * Исправил тесты, падающие из-за неопределенного порядка отправки sms и емейлов.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a876b47f1 ]
 * Убрал лишнюю функцию get_state.                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6278307a3 ]
 * DIR-7431: Таск AccessRestoreTask отрефакторен так, чтобы логику было проще проследить.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/619e4acf6 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * review          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4ccc40d29 ]
 * DIR-7707 ревью  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/453614ff0 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-09-12 16:32:01+03:00

0.378.1
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7696 правка кода                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4295da554 ]
 * DIR-7696 Уменьшаем время нотификации об удалении организации       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ba8928dd9 ]
 * DIR-7693 Добавил описание                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6a4fd9939 ]
 * DIR-7693 убрал лишнее                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dc9bf8243 ]
 * DIR-7693 Не даем запрашивать права на ресурс в другой организации  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/32f44a032 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7590: Добавил фтльтрацию по external_id                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c12df7d01 ]
 * DIR-7590: Добавил генерацию событие при выдаче доступа к ресурсу метрики  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/609b064ae ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.378.0 → 0.378.1                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/21bc9b400 ]
 * Обновлён ChangeLog.rst.                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1baf17d71 ]
 * DIR-7736: Восстановление доступа теперь будет запускаться только в том окружении, в котором была создана организация.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f0847368a ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-09-11 13:23:41+03:00

0.378.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Правка команды для релиза  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b9fb11365 ]
 * Обновлён ChangeLog.rst.    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e084dbfd5 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-7446 чейнджлог                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/196a80c06 ]
 * DIR-7446 поправила тесты                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7cf644d4c ]
 * DIR-7446 Скрываем копирование аналитики в yt за настройкой COPY_ANALYTICS_TO_YT  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8abc34085 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.377.0 → 0.378.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6935cecfb ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/200ecf45a ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-09-10 12:00:20+03:00

0.377.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7573: При добавлении домена в проверке на дубликат учитываются то… (#2860)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8a05598ef ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.376.0 → 0.377.0        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/48581c520 ]
 * Добавил код для релиза одной командой  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0c6a3ddfe ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7461 Починили фильтр updated_at__gt в ручке GET /users/ (#2857)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/edaecdb18 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-09-04 19:17:55+03:00

0.376.0
-------
 * Bump version: 0.375.0 → 0.376.0                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a0cfe4ec5 ]
 * Обновлён ChangeLog.rst.                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1049c30a6 ]
 * DIR-7668 Не выводим право own для счетчиков метрики (#2864)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/78ecd57e7 ]
 * DIR-7587 Список запросов ролей для метрики (#2851)           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6ed18a89d ]
 * DIR-7628 убрал metrika-test из кода (#2854)                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f16c7d8ab ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-09-04 11:38:15+03:00

0.375.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.374.0 → 0.375.0                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5679cbf8b ]
 * Обновлён ChangeLog.rst.                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/aad4bf71c ]
 * DIR-7665 Убрал ограниченное редактирование (#2862)             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8b22dbcb8 ]
 * DIR-7512 Не даем добавить два client_id в организацию (#2861)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/477011f62 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7590: Ручка управления запрошенными ролями (#2853)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b8607cb2f ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-09-03 18:31:46+03:00

0.374.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7560 Оповещаем регистраторов только о удалении подтвержденных дом… (#2845)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/227cbc55e ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.373.0 → 0.374.0                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6d296bc49 ]
 * Обновлён ChangeLog.rst.                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0b07323fb ]
 * DIR-7650 Добавлен поиск ресурса во всех организациях на всех шардах при привязывании (#2856)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5b291ba43 ]
 * DIR-7556 Возврат более специфической 403 ошибки (#2848)                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1a9acec1e ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7662 Добавлены записи в историю домена при удалении организации и отрыве. (#2859)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ac1f460fc ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-09-02 17:05:03+03:00

0.373.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7239 Учитываем то что в ответе может не быть uids_with_modify_permission (#2855)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/645b1cda9 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 0.372.0 → 0.373.0                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a223b7f14 ]
 * Обновлён ChangeLog.rst.                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5001773bf ]
 * Убрал из вывода команды create-stand ссылки на стенд                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1d0b84a64 ]
 * DIR-7588: Ручка создания запроса на доступ к счетчику метрики (#2839)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/240a47b1f ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7524 Обрабатывать ответ с не xml содержимым от колбеков регистраторов (#2850)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d73d732d6 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * DIR-7617: Больше не запускаем таск SyncDomainsWithPDDTask при просмотре списка доменов. (#2852)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3a26b7f28 ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7503 Сохраняем дату рождения у портального сотрудника во время инвайта (#2846)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a2bf6206b ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-09-02 12:25:27+03:00

0.372.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * hotfix: поправил тест ResourceHistoryViewTest  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/55351cb00 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7551 Включаем фичи при создании организаций без домена  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8da2d548f ]
 * DIR-7551 Починил тесты                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f9156e4c9 ]
 * DIR-7551 Всем новым организациям включаем фичу no-more-pdd  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/377f69f85 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.371.0 → 0.372.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/38d3360d1 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/facf655bb ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-08-28 14:37:57+03:00

0.371.0
-------
 * Bump version: 0.370.0 → 0.371.0                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/49d93a86d ]
 * Обновлён ChangeLog.rst.                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fa3168125 ]
 * DIR-7593 Правка работы ручки /proxy/organizations для организаций с лого (#2838)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/643a9d9c5 ]
 * DIR-7542 дедупликация хуков (#2835)                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/15d7c16a9 ]
 * DIR-7629 базовые классы для работы с IDM (#2847)                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/82f698817 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-27 16:47:26+03:00

0.370.0
-------
 * Bump version: 0.369.0 → 0.370.0                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/330b3033a ]
 * Обновлён ChangeLog.rst.                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/448ee0a4f ]
 * DIR-7239 правка хостов справочника для int-qa  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/046963c71 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-26 18:03:06+03:00

v0.368.0
--------

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-08-26 17:37:59+03:00

0.369.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 0.367.0 → 0.368.0                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ba1c0ba6f ]
 * Обновлён ChangeLog.rst.                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2b8dbcab9 ]
 * DIR-7394: Админская ручка для отображении истории домена (#2825)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1fbf63025 ]
 * DIR-7392: сохранение истории действий с доменом (#2809)           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/db972b240 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.368.0 → 0.369.0                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/17ce54951 ]
 * Обновлён ChangeLog.rst.                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/715d69c71 ]
 * DIR-7601 Правка создания пользователя в create_user_from_bb_info (#2836)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6112c4fec ]
 * DIR-7415 Обрабатывать удаление ресурса из сервиса (#2842)                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/79fc9155d ]
 * DIR-7239 проверка прав для справочника при привязывании ресурса (#2844)   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3c4c77bbb ]
 * DIR-7326 Добавил описание вьюхи (#2841)                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/96dfc0ea4 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-26 17:11:04+03:00

0.367.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.366.0 → 0.367.0                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1799869fe ]
 * Обновлён ChangeLog.rst.                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2faf7af8a ]
 * DIR-7616 Не проверяем возможность связывания для метрики в тестинге (#2837)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0956434e4 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Поправлена ветка pgmigrate так, чтобы не использовать новых коммитов pgmigrate, где требуются более свежие зависимости.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a91f63b9e ]
 * Добавлен changelog.                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/68b6b63e9 ]
 * Исправлена установка pgmigrate.                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d7d191fc5 ]
 * Переключаемся на pgmigrate в котором я поправил убивалку блокирующих запросов.                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/53cadaf42 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-23 14:11:17+03:00

0.366.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7400 Базовые вьюхи для IDM (#2832)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/09b7ce0ac ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.365.0 → 0.366.0                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e7d2978f ]
 * Обновлён ChangeLog.rst.                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9cfac0f3b ]
 * Поправлено условие, при котором таск SyncSingleDomain засыпает и пытается дождаться подтверждения.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5f85bba5e ]
 * Поля karma и ip добавлены в список непубличных полей.                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a341b679d ]
 * Запрещаем запрашивать карму и ip в ручках про организацию.                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/19c5e91bf ]
 * Исправлены тесты, которые падали из-за того, что теперь значения в заголовках, это строки.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/87b501026 ]
 * Поправлены падающие тесты.                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/887c891b7 ]
 * Поменял тип колонки для IP на INET.                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/46aeeeaa6 ]
 * Поправлено форматирование согласно рекомендациям в ревью.                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9efa65b51 ]
 * Поправлено логгирование с текстом "Unable to find shard for organization".                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d12a5b9fe ]
 * Поправлено число скоупов в тесте.                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9d9954c45 ]
 * Поправлено "мигание" заголовка X-User-IP в тестах.                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dd48df735 ]
 * Поправлена опечатка в тесте.                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/160ab7804 ]
 * Поправлен один падающий тест.                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/60d1e6ac9 ]
 * Поправлено использование переменной в Makefile.                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/53e75bf5c ]
 * Поправлена ошибка при отдаче поля country для домена.                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/150369994 ]
 * Поправлена опечатка.                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c158cadd3 ]
 * DIR-7506: Добавлены поля karma и ip для организаций.                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/94b0ed28c ]
 * Добавлена новая проверка на наличие записи для ChangeLog.                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/714fe5815 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * typo fix  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/04413f8b3 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-08-21 16:36:27+03:00

0.365.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.364.0 → 0.365.0                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d606494ac ]
 * Обновлён ChangeLog.rst.                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5bda23a1e ]
 * DIR-7596 Правка ошибки нотификации при удалении организации (#2833)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9de11ef50 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * when stand - move ticket to readyForTest (#2834)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/042fb7fef ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-20 11:58:11+03:00

0.364.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7076 правка проверки прав         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ce734bc52 ]
 * DIR-7076 Переименовал права           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a4dad3d25 ]
 * DIR-7076 Правка теста                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/222771024 ]
 * DIR-7076 добавил описание             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/048d8de9a ]
 * DIR-7076 Ручка для удаления ресурсов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/802f17450 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-7581 Пуникодим домены от регистраторов при отправке колбеков.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/802e93e8b ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.363.0 → 0.364.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/16c1f8c89 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/aa24ba617 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-08-19 15:33:03+03:00

0.363.0
-------

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * releasing version 0.362.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ef3b855a1 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.362.0 → 0.363.0                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/01b384dc8 ]
 * Обновлён ChangeLog.rst.                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a8057cf9a ]
 * DIR-7591 Правка проверки прав на realtions (#2830)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fac78ed84 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-19 13:15:35+03:00

0.362.0
-------

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-08-19 11:13:00+03:00

0.362.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7514 правка описания                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f5c2a41ad ]
 * DIR-7569 правка changelog                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6bdf1be9a ]
 * DIR-7569 merge master                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dcbada590 ]
 * DIR-7569 Правка кода                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e5dc91b7 ]
 * DIR-7569 Добавил генерацию события при удалении организации          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/28c3b8f17 ]
 * DIR-7514 добавил описание                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/578162da7 ]
 * DIR-7514 правка теста                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3879bee46 ]
 * DIR-7514 Правка получения пользователя в /users/nickname/<nickname>  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1c490f193 ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7247: Поправил swagger описание            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e9246f666 ]
 * DIR-7247: Поменял роуты и добавил новый скоуп  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8211f5bf3 ]
 * DIR-7247: правки по ревью                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/499e137cf ]
 * DIR-7247: Ручки для доменных токенов           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/14447ab2d ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.361.0 → 0.362.0                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/70fcc4c66 ]
 * Обновлён ChangeLog.rst.                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2489f1110 ]
 * DIR-7582: Добавлено логгирование чтобы поймать причину того, почему иногда не прописывается organization_name.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5d9ca3e77 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-08-19 11:11:27+03:00

0.361.0
-------
 * Bump version: 0.360.2 → 0.361.0             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0551082ba ]
 * Обновлён ChangeLog.rst.                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/15c44c58c ]
 * DIR-7586 Добавил описание                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d4654501a ]
 * DIR-7586 Правка запроса за правами (#2827)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4d1924a30 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-16 17:38:19+03:00

0.360.2
-------
 * Bump version: 0.360.1 → 0.360.2                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/30004380d ]
 * Обновлён ChangeLog.rst.                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b95043d47 ]
 * Исправлена ошибка в функции get_last_verification_type из-за которой сломалось подтверждение доменов.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7dec9286a ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-08-15 17:17:58+03:00

0.360.1
-------
 * Bump version: 0.360.0 → 0.360.1                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9dd2e1adb ]
 * Обновлён ChangeLog.rst.                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b8d156c5f ]
 * Поправлен код который определяет, надо ли послать событие в setter.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eb01c62a8 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-08-15 15:57:13+03:00

0.360.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7523: перенес вызов таски CheckDomainInGendarmeAndGenDkimTask в функцию create_domain_in_passport_and_pdd  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/465a97633 ]
 * DIR-7523: правки по ревью                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/55ca2cb56 ]
 * DIR-7523: Запуск проверки в жандарме при подтверждении домена                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/aee047bd8 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-7520 правки                                                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9df1d8fa1 ]
 * DIR-7520 Откладываем выполнение таска SyncSingleDomainTask только для способа подтверждения PDD_EMU или None DIR-7572 Не дрегаем колбеки, если их нет  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4fb9a1791 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.359.0 → 0.360.0                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c0c4985fb ]
 * Обновлён ChangeLog.rst.                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bc3565dfb ]
 * Добавлена запись для changelog.                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/81639d33d ]
 * Поправлена отправка событий в EventNotificationTask                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9b3a61024 ]
 * DIR-7570: Добавлен "workaround" для того, чтобы отправлять в сервис setter только события по организациям с фичей no-more-pdd.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/63c7c056a ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-08-15 14:34:10+03:00

0.359.0
-------
 * Bump version: 0.358.0 → 0.359.0                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8f319e2ad ]
 * Обновлён ChangeLog.rst.                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/354dbc22f ]
 * DIR-7559 правки                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/250a636f9 ]
 * DIR-7559 При удалении организации дергаем колбек регистратора.                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7b1ab9bb6 ]
 * DIR-7564 Для 2 регистраторов передавать в callback параметр sign независимо от HTTP/HTTPS  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/265645ef8 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-08-13 20:04:12+03:00

0.358.0
-------
 * Bump version: 0.357.0 → 0.358.0                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/450f630f3 ]
 * Обновлён ChangeLog.rst.                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/51cdb558d ]
 * DIR-7497 пуникодим домены при выдаче                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f5fa9b731 ]
 * DIR-7497 ручка для спамообороны                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/099ed320a ]
 * DIR-7449 При отрыве домена включаем фичу NO_MORE_PDD в новой организации, если она была включена в старой.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1fbfdab5a ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-08-13 14:59:55+03:00

0.357.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.356.0 → 0.357.0                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9f16c24a3 ]
 * Обновлён ChangeLog.rst.                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9f0f8d491 ]
 * DIR-7502 Добавил описание                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eae80c8ca ]
 * DIR-7502 Обновляем кеш лицензий при включении трекера (#2811)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6a7b150d4 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Исправлена путаница с колбекамми в скрипте import_registrars.py  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/80a86e2d6 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-12 16:19:02+03:00

0.356.0
-------
 * Bump version: 0.355.0 → 0.356.0                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/df89a951e ]
 * Обновлён ChangeLog.rst.                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/999aaabfc ]
 * DIR-7472 Добавил описание                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/34bc0fa00 ]
 * DIR-7472 Возвращаем данные счетчиков метрики (#2807)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3432da590 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-12 12:53:59+03:00

0.355.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.354.0 → 0.355.0                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ec183b1a6 ]
 * Обновлён ChangeLog.rst.                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/906563411 ]
 * DIR-7519 ждем реплик паспорта, когда принимаем за поьлзователя ПС                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a3fedff58 ]
 * DIR-7519 удаляем за пользователя все рассылки и владельца домена                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d5c880022 ]
 * DIR-7519 При удалении организации удаляем из паспорта только роботов и рассылку all  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/181fdb927 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7368 Скрипт миграции регистраторов               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6f42c56fc ]
 * DIR-7475 При отрыве домена ожидаем реплики паспорта  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b859e6732 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Поправлен TVM client id для Fouras в проде.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e07d07adc ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-08-08 18:01:25+03:00

0.354.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7501: правки по ревью                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b9e144017 ]
 * DIR-7501: Поправлена ручка /proxy/domains/  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a2158d9c7 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.353.2 → 0.354.0                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ffa2eaf2e ]
 * Обновлён ChangeLog.rst.                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fe5214bea ]
 * DIR-7490 Добавлена ручка GET /registrar/uid/v2/<int:uid>/  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/65cafd0c4 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-08-08 14:23:51+03:00

0.353.2
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 0.353.1 → 0.353.2                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3769a8f6e ]
 * Обновлён ChangeLog.rst.                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/81832c0fe ]
 * DIR-7484: Фикс передачи параметров в метрику (#2804)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0fc7199a5 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-08-07 15:16:30+03:00

0.353.1
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 0.353.0 → 0.353.1                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/debe284c7 ]
 * Обновлён ChangeLog.rst.                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2bbebf9b4 ]
 * DIR-7484: Убрал обязательную передачу заголовков X-UID и X-ORG-ID в ручке получения ролей (#2803)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8c9455d8b ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-08-07 13:25:05+03:00

0.353.0
-------
 * Bump version: 0.352.0 → 0.353.0                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6598127fe ]
 * Обновлён ChangeLog.rst.                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8dd522d5b ]
 * DIR-7484: Разные права для разных счетчиков метрики (#2791)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/04e0198e3 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-08-06 17:40:26+03:00

0.352.0
-------
 * Bump version: 0.351.1 → 0.352.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bbb0ff075 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2729e5f39 ]
 * DIR-7326 добавил описание        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5578567f0 ]
 * DIR-7326 убрал лишнюю проверку   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b57ad3af6 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-06 15:12:17+03:00

0.351.1
-------
 * Bump version: 0.351.0 → 0.351.1  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/be789938b ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/49a0e8d20 ]
 * DIR-7509 Логируем ответ Zora     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cda119a2b ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-08-06 14:37:19+03:00

0.351.0
-------
 * Bump version: 0.350.1 → 0.351.0                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e2887a0ad ]
 * Обновлён ChangeLog.rst.                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/700260778 ]
 * DIR-7326 Управление правами на ресурсы (#2790)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c3abd42c1 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-06 13:56:08+03:00

0.350.1
-------
 * Bump version: 0.350.0 → 0.350.1                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e82421569 ]
 * Bump version: 0.349.1 → 0.350.0                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9e7273d16 ]
 * DIR-7509 Поправлена ошибка парсинга xml колбеков регистратора  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8fed1b100 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-08-06 13:29:19+03:00

0.349.1
-------
 * Bump version: 0.349.0 → 0.349.1                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d004c0bd2 ]
 * Обновлён ChangeLog.rst.                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/69959d953 ]
 * DIR-7509 Поправлена ошибка парсинга xml колбеков регистратора  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/16989a9c1 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-08-06 11:21:33+03:00

0.349.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.348.0 → 0.349.0                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1180847bf ]
 * Обновлён ChangeLog.rst.                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3910ec467 ]
 * DIR-7508 Переименовал право owner на own (#2799)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8fc09d9f3 ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7471 рефакторинг секретных токенов регистраторов (#2789)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/20ea18180 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-05 19:28:38+03:00

0.348.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7429: Удалил принт                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/78dc7487b ]
 * DIR-7429: Добавил параметр в исключение DuplicateDomain и дополнил тест  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7be7a17d1 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.347.0 → 0.348.0                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dc5406e66 ]
 * Обновлён ChangeLog.rst.                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/500ef2395 ]
 * игнорируем USER__HOST_NOT_ADDED от вебмастера  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/92f0c1e98 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-08-05 16:58:40+03:00

0.347.0
-------
 * Bump version: 0.346.0 → 0.347.0               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/53925ac37 ]
 * Обновлён ChangeLog.rst.                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1d1c5769c ]
 * DIR-7504 Добавил описание                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3455db8c9 ]
 * DIR-7504 Правка смены ответственного (#2797)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a2062c5b0 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-05 15:18:51+03:00

0.346.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.345.0 → 0.346.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dee193393 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6f79c9e4f ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7318 Разрешаем сотруднику быть уволенным в нескольких организациях (#2782)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ae1d670da ]
 * DIR-7439 Отключаем платные сервисы при блокировке организации (#2793)           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8670bfd1d ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-05 13:35:36+03:00

0.345.0
-------
 * Bump version: 0.344.0 → 0.345.0                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/899dccb66 ]
 * Обновлён ChangeLog.rst.                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0b277d990 ]
 * конфиг для выкатки на integration-qa                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f28206457 ]
 * DIR-7499 Добавил описание изменений                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9e9be8b9d ]
 * DIR-7499 добавил генерацию события при изменении ресурса (#2795)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4bbb9244a ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-02 16:56:42+03:00

0.344.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7493: Добавил добавление DomainDeleteCallbackTask на событие doma… (#2792)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0c2cb66e1 ]

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.343.0 → 0.344.0                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c52fbeba1 ]
 * Обновлён ChangeLog.rst.                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e1e52a524 ]
 * DIR-7383 Обработка смены ответственного для метрики (#2786)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a9178be92 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-08-01 13:46:15+03:00

0.343.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.342.1 → 0.343.0                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5ff9b2710 ]
 * Обновлён ChangeLog.rst.                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bd5fbb0ae ]
 * DIR-7377 Возвращаем ошибку при проверке прав заблокированных организаций (#2785)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e6ce1e23f ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7432 генерим DKIM при подтверждении домена, если ПДД выключено (#2774)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4208f9498 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-07-31 13:17:15+03:00

0.342.1
-------
 * Bump version: 0.342.0 → 0.342.1                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5d6da79fa ]
 * Обновлён ChangeLog.rst.                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/01d54a497 ]
 * DIR-7174: Добавил обработку http ошибок взаимодействия с регистратором (#2787)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/069533963 ]
 * hotfix: Поправил юнит тест для ZoraClient                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bcee97fbf ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-07-30 17:41:50+03:00

0.342.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7404 Добавлены базовые классы для работы с idm (#2784)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3b6a4a3ec ]

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 0.341.0 → 0.342.0                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e3ac9641 ]
 * Обновлён ChangeLog.rst.                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3a94e9c34 ]
 * DIR-7174: Реализация процедуры подтверждения домена через регистратора (#2781)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6e70aeb52 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-07-30 12:56:04+03:00

0.341.0
-------
 * Bump version: 0.340.0 → 0.341.0                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0c466c7b7 ]
 * Обновлён ChangeLog.rst.                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1d4beb2fc ]
 * DIR-7375: Админская ручка на беке для разблокировки/блокировки органи… (#2767)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1995a1b97 ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-07-29 19:55:18+03:00

0.340.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.339.0 → 0.340.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fce3a1aef ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/78b1257fb ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Убрал лишний ретурн                                                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6047a88f2 ]
 * DIR-7424: Добавлена функция add_registrar_domain и таск SyncSingleDomain теперь будет перезапускать проверку в Вебмастере для доменов от регистраторов.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0edd744b8 ]
 * Поправлена опечатка.                                                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/712dca80e ]
 * DIR-7423: Таск SyncSingleDomainTask теперь будет периодически проверять статус добавленного домена в течении 7 дней.                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f6a639c93 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7447 Скрываем в выдаче ручек приватные способы подтверждения домена (#2780)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eb383dfd1 ]

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-7452 ленивая миграция в ручке who-is (#2779)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2dd2a775a ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-07-29 17:25:30+03:00

0.339.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-7325: Актуализировал список ролей                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/93780a3da ]
 * DIR-7325: Унаследовал ошибку UnknownService от APIError  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c4bb42608 ]
 * DIR-7325: Добавил swagger описание                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3d61f063e ]
 * DIR-7325: Ручка со списком прав доступа                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7b1238953 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.338.0 → 0.339.0                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/75de14aa7 ]
 * Обновлён ChangeLog.rst.                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/84e0d9d24 ]
 * DIR-6700 асессоры и саппорты могут могут видеть Фоновые задачи в каталоге  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5a90b9aa0 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Отключили автоматический старт ревью пулл-реквеста.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3099c506b ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-07-25 13:17:57+03:00

0.338.0
-------
 * Bump version: 0.337.0 → 0.338.0                                                                                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a36517bc7 ]
 * Обновлён ChangeLog.rst.                                                                                                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/330f5062a ]
 * Убрал костыль который блокировал удаление доменов.                                                                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8690097d0 ]
 * Временно запретил удаление доменов.                                                                                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8580bc28b ]
 * Исправлена ошибка из-за которой мог случиться отрыв домена в той же организации куда он только что был добавлен.                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/40057e144 ]
 * Исправлена ошибка "NameError: global name 'to_punycode' is not defined" появлявшаяся при смене владельца.                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/139457712 ]
 * Снова переименова миграцию, так как этот пулл скорее всего будет мерджиться после пулла https://github.yandex-team.ru/yandex-directory/yandex-directory/pull/2769 в котором тоже есть миграция.   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2db016486 ]
 * Добавил обработку ошибок с кодом >= 400.                                                                                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f7546ff46 ]
 * Переименовал конфликтующую миграцию базы.                                                                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/471142233 ]
 * Поправил ошибку в тестах.                                                                                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/441a1e068 ]
 * Поправлена обработка ошибок от Жандарма. В случае если домен не найден, отправляем задание на его проверку.                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1f7e34b6e ]
 * Удалены тесты, проверяющие синк алиасов с ПДД.                                                                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f74f86261 ]
 * Поправлен циклический импорт.                                                                                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/525a532cf ]
 * Поправил опечаточку.                                                                                                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6617dbca2 ]
 * DIR-7341: Для организаций с отключенным ПДД берём поля mx и delegated из сервиса Жандарм.                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b9f01397c ]
 * DIR-7343: В ручке GET /v[1-5]/domains/ больше не ходим в ПДД, если у организации фича no-more-pdd.                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a6125c745 ]
 * DIR-7347: Теперь при добавлении нового подтверждённого домена, мы не будем ходить в ПДД, если у организации фича no-more-pdd.                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4bc79b039 ]
 * DIR-7346: Больше не ходим в ПДД при смене мастер-домена, если у организации фича no-more-pdd.                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b6baade9e ]
 * Поправил опечатку.                                                                                                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7a0946c54 ]
 * DIR-7345: Если создавать организацию старым способом, через паспорт, и указать в домене ключевое слово no-pdd, то для организации включится фича no-more-pdd и мы отключим все походы в API ПДД.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/821af1895 ]
 * DIR-7340: При смене владельца домена, если в организации ПДД отключен, то будем менять владельца напрямую в Паспорте, а ПДД трогать не будем.                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fd0c57145 ]
 * DIR-7339: Больше не будем ходить в ПДД при удалении домена, если для организации ПДД отключён.                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/83fbc17b5 ]
 * DIR-7338: Удалена функция sync_aliases, синхронизирующая алиасы с ПДД.                                                                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ae726913b ]
 * DIR-7337: В функции sync_domain_with_pdd больше не ходим в ПДД если он для организации отключён.                                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9ad59d938 ]
 * DIR-7336: Добавлена фича no-more-pdd, позволяющая запрещать походы в ПДД для определённых организаций.                                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/95d8630e1 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-23 13:23:47+03:00

0.337.0
-------
 * Bump version: 0.336.0 → 0.337.0                                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/16067338f ]
 * Обновлён ChangeLog.rst.                                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/01ced4cdf ]
 * DIR-7197: Исправлен баг, из-за которого при определённых обстоятельствах домен пропадал из организации, и оставался в Паспорте.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dc5bf2ade ]
 * Исправлена ошибка из-за которой мог случиться отрыв домена в той же организации куда он только что был добавлен.                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ebe3201bd ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-23 10:57:56+03:00

0.336.0
-------
 * Bump version: 0.335.0 → 0.336.0                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6c0dda6a6 ]
 * Обновлён ChangeLog.rst.                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2e759c6d2 ]
 * DIR-7444: Убрали снихронизацию доменов с ПДД из крона.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e7d663ea0 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-22 17:55:56+03:00

0.335.0
-------
 * Bump version: 0.334.0 → 0.335.0                                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a6e6f6aed ]
 * Обновлён ChangeLog.rst.                                                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1a84a30a3 ]
 * DIR-7410: Теперь можно проставить организации фичу no-doregistration, и мы не будем требовать от её сотрудников принятия пользовательского соглашения.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/080a14443 ]
 * Поправлена опечатка.                                                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d0b3306d9 ]
 * DIR-7175: Исправлен баг из-за которого новый владелец не становился админом организации.                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e2cc47383 ]
 * Добавлен тест, проверяющий, что будет если владелец организации без домена сменится дважды.                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6380d4705 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-22 15:58:26+03:00

0.334.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-6636 Добавил новый кейсет  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/97d98bb89 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.333.0 → 0.334.0                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4a5284f92 ]
 * Обновлён ChangeLog.rst.                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a8d9a87a1 ]
 * DIR-7434 Исправлено условие в prefetch_related модели Organization  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/146baa41f ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-5738 Правки по ревью                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d16dc0d30 ]
 * DIR-5738 Дергаем колбеки регистраторов при подтверждении/удалении домена  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/20cefb65c ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-07-22 13:48:09+03:00

0.333.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-7362 инвалидируем кэш                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/86fe15848 ]
 * DIR-7362 правки                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e5a833e9b ]
 * DIR-7362 в организации можно менять default_uid и can_user_change_password  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8c8eb5c17 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.332.0 → 0.333.0                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1a514d531 ]
 * Обновлён ChangeLog.rst.                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/150819584 ]
 * Поправил один из тестов так, чтобы проверялась работа maillist чекера на вложенных отделах.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8f66b7f51 ]
 * Поправлены тесты.                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f8d3e5e8f ]
 * Добавлены утилиты для проверки рассылок из manage shell.                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7a39b29bb ]
 * Убрал лишний код.                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f59dded24 ]
 * DIR-7370: Поправлена сверка состава рассылки между Коннектом и BigML.                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fb001610c ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-18 10:50:05+03:00

0.332.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * DIR-6174: Сделал обязательным передачу пользователя  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ba1e8cf53 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.331.0 → 0.332.0                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8179248bc ]
 * Обновлён ChangeLog.rst.                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f3422a37a ]
 * Поправлены импорты.                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/730929228 ]
 * Исправлена опечатка из-за которой случались пятисотки.                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d944f86ef ]
 * Кидаем APIError.                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/580afb0bb ]
 * DIR-6979: Исправлена 500 ошибка в случае, если через API пытались завести пользователя с external_id, который занят.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/76af7e233 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-16 15:45:24+03:00

0.331.0
-------
 * Bump version: 0.330.0 → 0.331.0                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ce629b476 ]
 * Обновлён ChangeLog.rst.                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/92922751b ]
 * DIR-7414 улучшения для складывания аналитики           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b93bea3a9 ]
 * DIR-7413 удалены вики и формы из пресета для порталов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1c6e0b02e ]
 * удалены вики и формы из пресета для порталов           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6564e3896 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-07-15 18:37:30+03:00

0.330.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.329.0 → 0.330.0                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a34cd194c ]
 * Обновлён ChangeLog.rst.                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/136979993 ]
 * Увеличили приоритет тасков SaveAnalyticsLocal и SaveAnalyticsToYTTask  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/65c54eff4 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-07-12 17:04:13+03:00

0.329.0
-------

* [Oleg Larionov](http://staff/oleglarionov@yandex-team.ru)

 * Bump version: 0.328.0 → 0.329.0                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/040fd46df ]
 * Обновлён ChangeLog.rst.                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/781c4d9ee ]
 * fix: Фикс версии                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/627105482 ]
 * Bump version: 0.327.1 → 0.328.0                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eb0ab8553 ]
 * Обновлён ChangeLog.rst.                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b6a008fa0 ]
 * DIR-6174: Ручка для добавления домена как подтвержденного (#2746)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/df26bfe05 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Поправил работу с транзакциями в migrate-portal и сделал так, чтобы было удобно использовать функции в REPL.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fb566a4cf ]
 * Небольшой фиксик :)                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3ea7f8262 ]
 * DIR-7366: Исправлены проблемы в команде migrate-domains.                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f7e9f053d ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-07-12 12:44:37+03:00

0.327.1
-------
 * Bump version: 0.327.0 → 0.327.1                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f35d527a3 ]
 * Обновлён ChangeLog.rst.                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3c60c104f ]
 * Используем правильный токен для паролей регистраторов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3f04c7311 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-07-11 17:10:01+03:00

0.327.0
-------
 * Bump version: 0.326.1 → 0.327.0                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/095146796 ]
 * Обновлён ChangeLog.rst.                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c6730a201 ]
 * DIR-7371 В выдачу GET /v10/registrar/{id}/ добавлен admin_id  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f58274211 ]
 * DIR-7255 Поправлена схема для токенов доменов                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2713167ba ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-07-09 17:43:35+03:00

0.326.1
-------
 * Bump version: 0.326.0 → 0.326.1  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4d0e437af ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2faf19aef ]
 * fix changelog                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7b3d8fdbf ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-07-09 11:48:44+03:00

0.326.0
-------

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-07-09 11:27:24+03:00

0.326.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7305 отключаю кеширование в integration qa  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d034b9cdf ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * fix changelog                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3118acd05 ]
 * fix changelog                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c189c4762 ]
 * Bump version: 0.325.0 → 0.326.0                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bd7d0b03b ]
 * Обновлён ChangeLog.rst.                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b1630a148 ]
 * DIR-7255 Удален лишний код                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/952ad740e ]
 * DIR-7255 Добавлена поддержка шифрования паролей для новых регистраторов    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f56ad9932 ]
 * DIR-7255 Доработка команды import-registrars для переноса токенов доменов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7988d59ea ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-07-09 11:26:27+03:00

0.325.0
-------
 * Bump version: 0.324.1 → 0.325.0                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fbdbe7d58 ]
 * Обновлён ChangeLog.rst.                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d216ea1c9 ]
 * DIR-6778: Добавлен changelog                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2cd56f464 ]
 * DIR-6778: Заменил вызов json_error (где нет логгирования) на выбрасыв… (#2733)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3b29922ac ]

[Oleg Larionov](http://staff/oleglarionov@yandex-team.ru) 2019-07-08 12:45:02+03:00

0.324.1
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7305 Конфиг для integration-qa (#2738)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/744e4c01f ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Починен фильтр registrar_id в GET /domains/  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c46f95a9a ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.324.0 → 0.324.1                                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4992a5622 ]
 * Обновлён ChangeLog.rst.                                                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5971c84f2 ]
 * Исправлена ошибка из-за которой ручка поиска организаций по registrar_id не работала, когда в неё приходили без X-Org-ID или без X-UID.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/26ff8f798 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-05 19:41:05+03:00

0.324.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-6939 Правка по замечаниям  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/87655126a ]
 * DIR-6939 работа с тестами      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2c1037670 ]
 * DIR-6939 Клиент для Zora       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/68240dcb9 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7351 Явно указываем какие поля с "чувствительными" параметрами отдаем разрешаем в выдаче  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d12b6032f ]
 * DIR-7302 пересоздаем базу в тестах                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f8ba63c5e ]
 * DIR-7302 ttl задачи SaveAnalyticsToYTTask увеличен до часа                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ec0e9219c ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.323.0 → 0.324.0                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/99dcd5705 ]
 * Обновлён ChangeLog.rst.                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d6dc41f31 ]
 * Bump version: 0.322.0 → 0.323.0                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c9b79986f ]
 * Обновлён ChangeLog.rst.                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3c09bc02d ]
 * Удалены лишние вызовы метода trace() в тех местах где не перехватывается исключение.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b9eaea767 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-04 17:07:44+03:00

0.322.0
-------
 * Bump version: 0.321.1 → 0.322.0                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b3329265b ]
 * Обновлён ChangeLog.rst.                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d9a06d536 ]
 * DIR-7182 Проверка прав на счетчик метрики (#2726)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/666c686dc ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-07-04 12:51:38+03:00

0.321.1
-------
 * Bump version: 0.321.0 → 0.321.1                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0c45b0553 ]
 * Обновлён ChangeLog.rst.                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bcc154a7a ]
 * DIR-7352: Поправлена ошибка с типом аргумента во вьюшке /proxy/organizations/.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/01c5c5753 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-04 12:35:20+03:00

0.321.0
-------
 * Bump version: 0.320.0 → 0.321.0                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1496a6f4d ]
 * Обновлён ChangeLog.rst.                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ff7e4039c ]
 * Добавлена обработка случая, когда домена у организации нет.                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/78ec8db0e ]
 * Берем урл из MDS_READ_API.                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dbe4811a4 ]
 * DIR-7331: Добавлена ручка /proxy/organizations/ для ПДД API прокси.                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/16e7329b6 ]
 * В тест добавлена проверка, что при автоподтверждении домена проставляется призгнак has_owned_domains.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e253f2115 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-03 18:32:18+03:00

0.320.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Проверка на наличие msgfmt                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a30bc34c9 ]
 * DIR-7294 правка readme                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1cba3985e ]
 * DIR-7294 Выдача данных регистратора по ПДД id  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3bed01ca1 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6844 Правки по ревью                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/de2abb3c7 ]
 * DIR-6844 АПИ для токенов регистраторов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6fb3100db ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.319.0 → 0.320.0                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/31f81dc59 ]
 * Обновлён ChangeLog.rst.                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/099aa6c5a ]
 * DIR-7295: Добавлена возможность запрашивать данные о доменах по registrar_id.        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9b689edd8 ]
 * Отключил кэширование для вьюшки которая отдаёт данные о регистраторе по токену.      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5a2a39c71 ]
 * Улучшил ChangeLog.                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2b6626589 ]
 * Добавлена инфа про нужные секреты и более внятное сообщение об ошибке, если их нет.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4bc841095 ]
 * Добавлен ChangeLog.                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2368ddc0e ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-7300 приложение metrika-test в ручке связывания (#2729)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6f7583ecf ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-07-01 13:13:10+03:00

0.319.0
-------
 * Bump version: 0.318.0 → 0.319.0                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/aee1ae466 ]
 * Обновлён ChangeLog.rst.                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ea328b7ba ]
 * DIR-7311 Ищем пользователя по емейлу а не никнейму (#2727)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/85086791c ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-06-28 12:58:59+03:00

0.318.0
-------
 * Bump version: 0.317.0 → 0.318.0                                                                                                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/76f0046d3 ]
 * Обновлён ChangeLog.rst.                                                                                                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9cbdd77b1 ]
 * Пробуем postgres 10.8                                                                                                                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/942fe9013 ]
 * Пустой коммит чтобы стриггерить билд!                                                                                                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3259c0780 ]
 * DIR-6391: Теперь все домены заканчивающиеся на .auto.connect-test.tk будут автоматически подтверждаться и тестировщики-ассесоры возрадуются, потому что смогут проходить сценарии в которых нужно добавлять домен.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/60dba24ef ]
 * Код deferred поправлен так, чтобы не падать, когда внутри теста случается ошибка.                                                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fc995485e ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-06-27 18:21:16+03:00

0.317.0
-------
 * Bump version: 0.316.0 → 0.317.0                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a5c737e45 ]
 * Обновлён ChangeLog.rst.                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2a2647202 ]
 * DIR-7310 yandexsprav можно временно связывать любые ресурсы (#2725)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d878ccd42 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-06-27 16:54:04+03:00

0.316.0
-------
 * Bump version: 0.315.0 → 0.316.0                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/67fb5605e ]
 * Обновлён ChangeLog.rst.                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f2af659e7 ]
 * DIR-7049 Убираем user_limit из required (#2719)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d22747ca6 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-06-27 15:25:11+03:00

0.315.0
-------
 * Bump version: 0.314.0 → 0.315.0            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d26d0e383 ]
 * Обновлён ChangeLog.rst.                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b97069568 ]
 * DIR-7303 Правка счетчика ресурсов (#2720)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6103e0cce ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-06-27 12:22:22+03:00

0.314.0
-------

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * Revert "DIR-6844 АПИ для токенов регистраторов"  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b247dcc3f ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.313.0 → 0.314.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c00316b6c ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/186006267 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6844 Правки по ревью                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d770c8ba1 ]
 * DIR-6844 АПИ для токенов регистраторов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c0cb04c6b ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Исправлено так, чтобы в событие про создание ресурса попадали его внешний id и название сервиса.                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d35045e13 ]
 * DIR-7163: Исправлен баг из-за которого при "сбросе" дня рождения сотрудника изменение в паспорте ДР не сбрасывался.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e2b16c248 ]
 * DIR-7157: Теперь при добавлении ресурса будет генериться событие resource_added.                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/65574fc62 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-06-25 11:34:25+03:00

0.313.0
-------
 * Bump version: 0.312.0 → 0.313.0                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3242a3aab ]
 * Обновлён ChangeLog.rst.                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/064fad9d0 ]
 * DIR-7074 Апи для изменения ответственного (#2703)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c69304346 ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-06-21 19:31:01+03:00

0.312.0
-------

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.311.0 → 0.312.0                                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fa943bba7 ]
 * Обновлён ChangeLog.rst.                                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8443b4c37 ]
 * Поправил ./create-stand.sh, чтобы он обновлял Playground доку.                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a10339b28 ]
 * Eщё раз поправлены докстринги.                                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/84a989244 ]
 * Исправлен докстринг, так чтобы playground правильно работал с ручками про регистраторов.                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fb0a1ea50 ]
 * Поправил опечатку.                                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/21636827b ]
 * DIR-7231: Добавлена вьюшка /resources/count/?service=<слаг-сервиса>                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/550c1a034 ]
 * DIR-7210: Теперь мы после принятия инвайта будем отправлять пользователя в сервис через ручку /portal/context для правильной смены контекста.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/32a1ad115 ]
 * Поправил докстринг ручки PATCH registrar.                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b9feb97ba ]
 * Поправлено так, чтобы регистраторское API принимало разные поля, в зависимости от версии.                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/076e9bc6e ]
 * Добавлено примечание на счёт необходимости миграции.                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1b87e32c6 ]
 * Добавлен кусочек changelog.                                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/81cd2ad3f ]
 * Переименовал модули, которые относились к API регистраторов.                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/58cadb50e ]
 * Добавлен кусочек Emacs конфига, для подключения Python Language Server. Не обращайте на него внимания :)                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a82b86b27 ]
 * DIR-7127: Ручка для редактирования callback регистьратора переименована в /registrar/<int:id>/ и теперь позволяет обновлять и другие поля.     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/74176e552 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Update README.md  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f02dc1d73 ]
 * Update README.md  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/009590a87 ]
 * Update README.md  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/94f465848 ]
 * Update README.md  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/05a6a3e2e ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-06-20 18:24:07+03:00

0.311.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * Bump version: 0.310.0 → 0.311.0                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/130821843 ]
 * Обновлён ChangeLog.rst.                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/96e061339 ]
 * DIR-7233 Выдача ресурсов по переданному сервису (#2711)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a91d6fe74 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Поправлены тесты, поломанные изменениями в update_maillist_uids.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/639e89b0c ]

[Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru) 2019-06-19 18:16:57+03:00

0.310.0
-------
 * Bump version: 0.309.0 → 0.310.0                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2e201edba ]
 * Обновлён ChangeLog.rst.                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/39fc7076d ]
 * Поправлен скрипт, который создаёт аккаунты рассылок.                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2f972548d ]
 * DIR-7253: Исправлен рассчёт графиков про скорость включения трекера.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4f6ef7e8e ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-06-18 16:01:05+03:00

0.309.0
-------
 * Bump version: 0.308.0 → 0.309.0                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bde291475 ]
 * Обновлён ChangeLog.rst.                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c91bfde14 ]
 * DIR-7176: События стараемся разослать в первую очередь, чтобы задержка была минимальной.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/af6be9734 ]
 * Поправил косячок. Как хорошо, что у нас есть тесты!!!                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dff29a913 ]
 * DIR-7234: Добавлено логгирование popid после создания сборщика почты.                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0cbaa62d6 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-06-17 15:52:30+03:00

0.308.0
-------

* [Vladimir Koljasinskij](http://staff/smosker@yandex-team.ru)

 * DIR-7093 правка кодов ошибок                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1827dfacd ]
 * DIR-7093 правка тестов                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/58dd3e5bb ]
 * DIR-7093 Правки по замечаниям                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4ce780d93 ]
 * DIR-7093 Убрал лишнее                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d776af02a ]
 * DIR-7093 Убрал vcrpy                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/472457253 ]
 * DIR-7093 для перезапуска                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b7ec89b0a ]
 * DIR-7093 правки                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8e8c68a36 ]
 * DIR-7093 правка кода                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/411f0fe3c ]
 * DIR-7093 правка кода                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/18a514aa9 ]
 * DIR-7093 отказ от trendocker                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/106bfecb6 ]
 * DIR-7093 правка тестов                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/718ca0c70 ]
 * DIR-7093 правка тестов                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3e480a5a4 ]
 * DIR-7093 DIR-7093 Проверка прав на ресурс при привязывании к организации в формах  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c548d6142 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-5737 привязываем организацию к регистратору        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6d890d4bd ]
 * DIR-5737 привязываем организацию к регистратору        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f2d65122a ]
 * DIR-5737 ручка создания организации для регистраторов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/10ab7434b ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.307.0 → 0.308.0                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1ed02e0e7 ]
 * Обновлён ChangeLog.rst.                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0b9f43edb ]
 * DIR-7226: Исправлена ошибка, из-за которой мы не отдавали в API (и на фронте) домены, подтверждённые через ПДД.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5d25ef794 ]
 * DIR-7223: Ручка POST /invites/emails/ теперь тоже может принимать слаг компании из рассылятора.                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0ed033f89 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-06-14 10:30:05+03:00

0.307.0
-------
 * Bump version: 0.306.0 → 0.307.0                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/262afdf4f ]
 * Обновлён ChangeLog.rst.                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fc8b37e58 ]
 * DIR-7196 В ручке GET /domains/ не ходим в ПДД, если не запрошены поля из ПДД  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2c6494bdf ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-06-11 12:15:26+03:00

0.306.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7201 Подправлены имена метрик request_count_by_ для более консистеного состояния  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b2e037445 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.305.0 → 0.306.0                                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e711a5525 ]
 * Обновлён ChangeLog.rst.                                                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/18b3e0f12 ]
 * Переименовал функции так чтобы было более понятно.                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6296b6eef ]
 * Поправлен ChangeLog.                                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/74df14621 ]
 * Поправлен host на котором работает команда invoke serve-docs.                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/66e213fd0 ]
 * Фикс опечатки.                                                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0787827dd ]
 * Поправлены тесты.                                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cbe1272c4 ]
 * Удалён тестовый прототип.                                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b2fdb80d7 ]
 * DIR-7091: Ускорено сохранение данных про организации для аналитических отчётов.                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/03528862a ]
 * Move prepare                                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/48ba82ec9 ]
 * Поправил ошибку в докстринге.                                                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/071589db7 ]
 * DIR-7063: Добавлена ручка /ui/organizations/, которая отдаёт названия организаций, в которых пользователь является сотрудником.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/27f54c488 ]
 * Поправлено несколько тестов.                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/33987134b ]
 * DIR-7144: Исправлено включение ЯОрг режима для тех, кто приходит с ПДД промки.                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/475634b3e ]
 * Добавлен тестовый скрипт scripts/test_analytics_saving.py, который использует временные таблицы для складывания данных по организациям.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/724aa350e ]
 * Улучшена функция show_analytics_saving_status, чтобы можно было запрашивать данные по конкретному таску.                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/964f42452 ]
 * Поправлены разные штуки про складывание аналитики.                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b35b74fcd ]
 * Поправил команду normalize-org-names, чтобы корректно обрабатывать ошибки AccountDisabled и PassportUnavailable.                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d8deabc71 ]
 * Починил пару опечаток.                                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0e31d5de3 ]
 * DIR-7091: Увеличен таймаут до 4 часов на таск который складывает данные для аналитики.                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4ee23c54b ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-06-10 17:19:25+03:00

0.305.0
-------
 * Bump version: 0.304.1 → 0.305.0                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/018e622bc ]
 * Обновлён ChangeLog.rst.                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2e8ee7bc7 ]
 * DIR-7014: В не (прод, QA) окружениях по умолчанию отправлять все письма на рассылку connect-test-mail (#2687)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/31d167ff4 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-06-07 11:57:53+03:00

0.304.1
-------
 * Bump version: 0.304.0 → 0.304.1                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/02566cd82 ]
 * Обновлён ChangeLog.rst.                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bee01290f ]
 * Добавлен changelog.                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e8639676 ]
 * DIR-6975: Исправлено принятие инвайта, когда в body есть дополнительные ключи.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e9177e853 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-06-06 18:25:34+03:00

0.304.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6973 По умолчанию коды принадлежат сервису portal                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d420a393c ]
 * DIR-6973 В ручку POST /invites/ добавлены параметры wait и mail_campaign_slug  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cd4aa3b55 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.303.0 → 0.304.0                                                                                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f149982f2 ]
 * Обновлён ChangeLog.rst.                                                                                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d8a69498a ]
 * Добавлен скрипт enable_forms.py                                                                                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/88021b8b2 ]
 * Небольшие изменения в enable_maillists.py                                                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2370b778f ]
 * Поправлены тесты.                                                                                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9756e1f5a ]
 * Удалены лишние тесты.                                                                                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/371e5c0bd ]
 * Теперь при валидации по JSON схеме мы во всех ручках будем считать, что на вход поступил пустой словарь, даже если body не было вовсе или если был указан неправильный Content-Type.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/788130822 ]
 * DIR-6537: Исправлена ошибка, из-за которой не удавалось установить правильный organization_name для организаций, в которых default_uid заблокирован.                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fd2db8b38 ]
 * DIR-6975: Теперь ручка для "использования" инвайта, всегда отдаёт поля "redirect_to" и "wait".                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/661997b39 ]
 * Добавлен импорт логгера.                                                                                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f69b569df ]
 * Переложил скриптик для включения рассылок в папку scripts/                                                                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/85e119485 ]
 * Скрипт для включения листов рассылок переписан на итераторы, чтобы включать параллельно во всех шардах.                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ab11eceb5 ]
 * Добавлен код для подсчёта на какой процент включены рассылки.                                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ff5393349 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-06-06 16:20:04+03:00

0.303.0
-------

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.302.0 → 0.303.0                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a10996584 ]
 * Обновлён ChangeLog.rst.                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9a2b73b06 ]
 * DIR-7034: Исправлена ошибка из-за которой падал таск при попытке заблокировать "портального" робота.                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8d297e6c3 ]
 * DIR-7145: Скрипт, включающий yaorg режим, теперь включает его и для организацией у которых подключен Трекер.                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/725dc6841 ]
 * DIR-7160: Раньше из-за ошибки, статус триала не "протухал", если пользователь сам выключил сервис до даты окончания триала.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/61c798556 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Update .devexp.json  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/91ca3bf96 ]
 * Update README.md     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/015b705da ]
 * Update README.md     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/69ae2f98b ]
 * Update README.md     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ae2b7f631 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-06-06 15:31:13+03:00

0.302.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6999 новый тариф для трекера  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/102a91bff ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.301.0 → 0.302.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/854e91bb1 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/477092335 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-05-31 12:24:11+03:00

0.301.0
-------
 * Bump version: 0.300.0 → 0.301.0                                                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2210d8d5b ]
 * Обновлён ChangeLog.rst.                                                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/be02ecdee ]
 * Поправлено обновление max_department_id в случае, если отдел создаётся с заданным id.                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a8cd5a4c1 ]
 * Поправлены тесты и обработка ситуаций, когда отдел создаётся с указанием ID.                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cb2fd02a8 ]
 * Поправлена логика выбора id для нового отдела.                                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/964b98010 ]
 * Переименована конфликтующая миграция.                                                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/191928d19 ]
 * DIR-7128: Исправлена ошибка, из за которой при удалении последней созданной команды, её id освобождался и мог быть переиспользован при создании следующей команды.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/379457d91 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-05-29 16:37:35+03:00

0.300.0
-------
 * Bump version: 0.299.0 → 0.300.0                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/abab3d95b ]
 * Обновлён ChangeLog.rst.                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fb829c29b ]
 * Поправлен падавший тест.                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/47de5a0c0 ]
 * Добавлено подробное описание того, как работает SQL запрос для рассчёта скорости включения сервисов.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/24864bc1f ]
 * DIR-5974: Заменил memoize на нашу новую функцию cached_in_memory_with_ttl.                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/72422bf7f ]
 * Правки по ревью.                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bf2c19ed6 ]
 * DIR-6808: Исправлен рассчёт графика количества учёток для которых разъехался 1017 атрибут.            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e742c7195 ]
 * Добавлен коммент на будущее, про конфиг external_prod.                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9bd647746 ]
 * Поправлено ещё одно место, в котором мы теперь должны отдавать логотип организации для всех.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/45abb386d ]
 * Теперь в API отдаём логотим для всех организаций, вне зависимости от тарифного плана.                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/813fcb735 ]
 * Поправлены тесты.                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1a7f283d4 ]
 * DIR-6468: Добавлены метрики для мониторинга скорости включения сервисов.                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/52c792be3 ]
 * Добавлена миграция с индексами для сбора метрик по скорости включения сервисов.                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b815093c0 ]
 * Добавлен класс для сбора метрик в корзины для гистограммы.                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e79e035f2 ]
 * Правка по ревью.                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/092b8eb1c ]
 * DIR-7069: Исправлена проверка того, что подзадача таска на миграцию, создающая аккаунты, не найдена.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4f1b9dd57 ]
 * Считаем этап переноса почты accounts-creating успешным даже в том случае, если таска нет.             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/65eac5d63 ]
 * DIR-7069: Исправлена проверка того, что одна из главных подзадач таска на миграцию не найдена.        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3b3ba15aa ]
 * DIR-6943: Включаем возможность установить лого для всех организаций.                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/de9d41a04 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-05-27 15:49:29+03:00

0.299.0
-------
 * Bump version: 0.298.0 → 0.299.0                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cb42b309d ]
 * Обновлён ChangeLog.rst.                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c7e26e0f9 ]
 * DIR-6845 Правки по ревью                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6eb1dd633 ]
 * DIR-7071  Исправлен баг с удалением команд для организаций с сервисом рассылок  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/62b15c0cd ]
 * DIR-6845 Правки по ревью                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/595a2470f ]
 * DIR-6845 CRUD для управления callback регистраторов                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/62c1c644b ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-05-23 18:40:36+03:00

0.298.0
-------
 * Bump version: 0.297.1 → 0.298.0            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d83930534 ]
 * Обновлён ChangeLog.rst.                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8f8a95434 ]
 * DIR-7107 исправлен конфиг базы в тестинге  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e84bc9cb6 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-05-22 17:45:54+03:00

0.297.1
-------
 * Bump version: 0.297.0 → 0.297.1               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/da33c716f ]
 * Обновлён ChangeLog.rst.                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/793a896a5 ]
 * Added fake.txt                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/617ac00b0 ]
 * Бампаем версию, потому что релизер сломался.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3ac3e25e5 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-05-22 14:41:25+03:00

0.297.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-7010  фолбечимся на логин для ФИО, если ФИО нет в паспорте  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/391ed20f3 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.296.0 → 0.297.0                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6b6891a9e ]
 * Обновлён ChangeLog.rst.                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8229065e0 ]
 * DIR-7105: Исправлена 500 ошибка при смене дефолтного uid на домене.                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eb3a8591d ]
 * DIR-7088 Исправлен баг из-за которого мы не обновляли список org_id в паспорте при удалении организации.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e877c1608 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-05-22 14:00:31+03:00

0.296.0
-------
 * Bump version: 0.295.0 → 0.296.0                                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/358d13900 ]
 * Обновлён ChangeLog.rst.                                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4ef4de160 ]
 * DIR-6983: Исправлена отправка писем администраторам организаций в которых нет подтверждённого домена.                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/035481032 ]
 * DIR-7016: Исправлен баг из-за которого, при редиректе на версию урла заканчивающуюся на слэш, не отдавался HTTP заголовок Location.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/66bebf155 ]
 * DIR-7002: Исправлена ошибка, из-за которой не работала миграция доменов из ПДД в Коннект у админов, которые завели себе Яндекс Организацию.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f84026d2e ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-05-20 09:55:21+03:00

0.295.0
-------
 * Bump version: 0.294.0 → 0.295.0                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1227ebb9c ]
 * Обновлён ChangeLog.rst.                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6127605e5 ]
 * Поправил номер тикета.                                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6861c77d3 ]
 * DIR-6677: В manage команде enable-yaorg снято ограничение на домены.                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6522a97f9 ]
 * Поправлен возврат ошибок, который оказался поломан в результате рефакторинга.                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/244cdf4a2 ]
 * Вынес код для смены default_uid в отдельный метод вьюхи.                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e18442608 ]
 * DIR-6617: Теперь в метод PATCH /organization/1234/ можно передать поле default_uid чтобы установить ящик по-умолчанию.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3e227b1b4 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-05-16 15:07:19+03:00

0.294.0
-------
 * Bump version: 0.293.0 → 0.294.0                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a5da3141a ]
 * Обновлён ChangeLog.rst.                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/639b14dad ]
 * DIR-7065: Раньше только обычные саппорты это могли делать, но пока временно пришлось дать этот пермишшен и ассесорам.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2f9ba1766 ]
 * DIR-6954: Добавлено описание того, как передать source в ручку POST /bind/.                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a9e09987a ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-05-15 15:42:56+03:00

0.293.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * исправлен номер миграции  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/62c9cadf2 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.292.0 → 0.293.0                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f28929880 ]
 * Обновлён ChangeLog.rst.                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1b080a1a9 ]
 * Команда create-stand поправлена так, чтобы фронтенд нормально работал.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/28d332344 ]
 * DIR-7028: Исправлено обновление логотипа в организации.                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c359dc5c4 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-05-14 14:52:48+03:00

0.292.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.291.0 → 0.292.0                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/58f2d7802 ]
 * Обновлён ChangeLog.rst.                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1b384708d ]
 * DIR-6769 дополнила changelog                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bd577c61e ]
 * DIR-6769 Избавились от ветки подтверждения домена через ПДД, настроек NEW_DOMAIN_VALIDATION и WEBMASTER_PROBABILITY.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0abf9952d ]

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * DIR-5735 Дополнил декортатор appcontext_cached возможностью использовать в качесте части ключа кэширования аргументы функции  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/28c8abc91 ]
 * DIR-5735 Перенес команду импорта регистраторов в пакет meta                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/53fe49fde ]
 * DIR-5735 Каменты к коду                                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2871dd8fa ]
 * DIR-5735 Добавлены таблицы и SQLA-модели для регистраторов + команда для импорта регистраторов.                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6683f750d ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-05-13 13:56:33+03:00

0.291.0
-------
 * Bump version: 0.290.0 → 0.291.0                                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/153f6484f ]
 * Обновлён ChangeLog.rst.                                                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/81dcd48d6 ]
 * Теперь команда ./create-stand.sh выводит ссылки на окружения с картинками                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e450d1070 ]
 * DIR-6911: Поправлена обработка отсутствующей фамилии, а так же случай, когда имя и фамилия в событии присутствуют в виде простых строк.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fa9d55446 ]
 * DIR-7020: Исправлена ошибка с недостающим position в событии из-за которого ломалась доставка событий в организации.                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a68cb7336 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-05-07 18:08:24+03:00

0.290.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6942 при деактивации диска проверяем, что пользователь есть в паспорте и b2b  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b40b59619 ]
 * DIR-6840 404 вместо 500 для org_id=0 в ручках                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/82cf762b1 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.289.0 → 0.290.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/09ea3d193 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a7a3e8ced ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-29 16:27:40+03:00

0.289.0-fix-queue
-----------------

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-29 10:31:18+03:00

0.289.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6345 Поменяли код ошибки  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/80f2eaa4d ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.288.0 → 0.289.0                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/272bd3e29 ]
 * Обновлён ChangeLog.rst.                                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d7848a40e ]
 * DIR-7006: Больше не логгируем WARNING 'Data is invalid for given schema", если ошибок на самом деле не было.                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f9eac606f ]
 * DIR-7007: Добавлено больше логгирования в местах, где мы возвращаем ошибки при создании организаций.                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e11deef11 ]
 * Убрал лишний ресурс.                                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8f073a971 ]
 * DIR-6827: Отныне можно в ручку связывания передавать сколь угодно много одинаковых уидов, и лишние будут просто проигнорированы.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d4ac61b60 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-25 16:02:44+03:00

0.288.0
-------
 * Bump version: 0.287.1 → 0.288.0                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2fb9cce11 ]
 * Обновлён ChangeLog.rst.                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d772b7c82 ]
 * DIR-6345 fix тестов                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/08907853d ]
 * DIR-6345 Правки по ревью                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8f7e0ec5f ]
 * DIR-6345 Отдельный код ошибки при попытке отнять админские права у владельца организации  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4bd17e75c ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-04-24 17:27:48+03:00

0.287.1
-------
 * Bump version: 0.287.0 → 0.287.1                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/62730ecfc ]
 * Обновлён ChangeLog.rst.                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3bd1f157f ]
 * DIR-6938: Добавлено побольше логгирования в ручку смены владельца организации.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5803d8608 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-24 13:26:30+03:00

0.287.0
-------
 * Bump version: 0.286.1 → 0.287.0                                                                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4c92e8128 ]
 * Обновлён ChangeLog.rst.                                                                                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a495f94b5 ]
 * Добавлено нормальное описание для теста.                                                                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3e4db891e ]
 * Исправлен запуск миграций в юнит-тестах.                                                                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0f2a20e8f ]
 * DIR-6986: Больше мы не будем отправлять роботам приветственные письма.                                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a99139f59 ]
 * DIR-6829: Теперь при создании команды в Яндекс Организации, портальная учётка создающего становится "создателем" команды и добавляется в участники и админы (если админы не указаны явно).  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a7ee7dba4 ]
 * Поправил неудачно названный параметр.                                                                                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dbbca548c ]
 * DIR-6815: Таск UnsubscribeAllMaillistsTask больше не будет завершаться ошибкой, если у организации ещё нет ни одного неподтверждённого домена.                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/59b572ddd ]
 * Убрал лишние моки, мы ведь и так в базовом setUp клиент ПДД моккируем.                                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e088c345a ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-24 12:20:36+03:00

0.286.1
-------
 * Bump version: 0.286.0 → 0.286.1                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ed55bb689 ]
 * Обновлён ChangeLog.rst.                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ea5a96202 ]
 * DIR-6987 небольшие правки                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c278b83e9 ]
 * DIR-6987 берем отдельный конэкшен внутри функции set_domain_as_owned, разблокируем домены по крону  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d47e17029 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-04-23 19:29:01+03:00

0.286.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.285.1 → 0.286.0                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ba4babfad ]
 * Обновлён ChangeLog.rst.                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4ef3d3119 ]
 * DIR-6967 правки                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c57c6d603 ]
 * DIR-6967 не учитываем sensitive поля при поиске duplicated тасков  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2943f93ac ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6686 поправила meta_connecction              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6d547a235 ]
 * DIR-6686 Правки после ревью                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/96d6148af ]
 * DIR-6686 Пустой коммит, чтобы поддолкнуть тесты  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4999e833a ]
 * DIR-6686 Метрика для Яорганизаций                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4c67f8098 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-04-23 15:43:09+03:00

0.285.1
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.285.0 → 0.285.1                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b9081a4c0 ]
 * Обновлён ChangeLog.rst.                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e86d3232 ]
 * DIR-6982 исправлена ошибка в фукнции set_domain_as_owned, из-за которой не подтрвеждался домен.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4a4f98919 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * DIR-6958: Поправлена команда manage migrate так что она теперь автоматически будет выбирать master базу.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7dea6c95f ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-04-23 14:48:17+03:00

0.285.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6417 вынесла удаление доменов из паспорта и пдд в отдельную функцию  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9d4ddde ]
 * DIR-6417 удаляем домены сначала из паспорта, потом из пдд                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4f16ae1 ]
 * DIR-6417 разрешаем удалять тех домены - алиасы                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/002030b ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * Bump version: 0.284.0 → 0.285.0                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/41e886d ]
 * Обновлён ChangeLog.rst.                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/77a7c50 ]
 * DIR-6843 Добавить алерты на количество ошибок в тасках на миграцию почты  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7879ca5 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * DIR-6542: Теперь можно создавать организации с названиями типа blah.ru:8080.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b834750 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-04-22 13:18:25+03:00

0.284.0
-------

* [Ivan Babintsev](http://staff/ibabintsev@yandex-team.ru)

 * DIR-4745 Исправлена проблема с отсутсвием контактов руководтеля отдела (#2642)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7b4d835bd ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6806 Не удаляются отделы в организациях с включенным сервисом рассылок, у которых нет uid  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2dfe9dcbd ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Bump version: 0.283.0 → 0.284.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e8f8546d0 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2b0a064e9 ]
 * DIR-6936 bug fixes (#2646)       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/40597c825 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-04-16 11:29:56+03:00

0.283.0
-------

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Bump version: 0.282.0 → 0.283.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4336ac3ec ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/168b464f6 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * DIR-6906: Исправлена ошибка, из-за которой при наличии ошибок во время подтверждения домена мог не проставляться признак has_owned_domains в метабазе. (#2641)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/af6ed5ab9 ]
 * DIR-6884: Исправлена ошибка в команде enable-yaorg - мы брали read коннект к метабазе.                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c794dcdf5 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-04-15 13:04:48+03:00

0.282.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6786 Проверка на наличие алиасов домена                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8200e8da1 ]
 * DIR-6786 Позволяем добавить "голый" домен если он есть только в паспорте у того-же админа  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/450a0f9aa ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.281.0 → 0.282.0                                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0a21e527a ]
 * Обновлён ChangeLog.rst.                                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6ca410ea3 ]
 * Исправлена опечатка в названии колонки таблички.                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7e3986482 ]
 * Раскомментировал фильтр по сервису Трекер.                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/21dcd44ad ]
 * DIR-6884: Команда enable-yaorg теперь правильно учитывает лимит, и пишет данные админов в YT табличку.                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f7d6625c3 ]
 * Добавлено примечание про то, почему мы удаляем внешних админом из метабазы.                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b4b67b530 ]
 * Исправлена ошибка, случавшаяся при попытке сделать владельцем организации портального пользователя, являющегося сотрудником организации.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/267b9a893 ]
 * DIR-6478: Поправлена ошибка из-за которой не работала смена владельца в организации, когда нет ни одного подтверждённого домена.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2ac0a9bca ]
 * DIR-6478: Исправлена ошибка, из-за которой было невозможно сменить владельца в Яндекс Организации.                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c2dc65118 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-11 17:28:44+03:00

0.281.0
-------

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * DIR-6903 не проставляем org_id в паспорте для внешних роботов (#2639)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f4490b36d ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * fix changelog                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/392754284 ]
 * Bump version: 0.280.0 → 0.281.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/de6a4778d ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ec387d6da ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-04-09 14:57:27+03:00

0.280.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6757 Обрабатываем uid в ответе паспорта как строку                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f0e554d0d ]
 * DIR-6757 Фикс использования bulk похода в BB                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b6db0560d ]
 * DIR-6757 Правки по ревью                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/48d3b5d2a ]
 * DIR-6757 В выдачу ручки GET /admin/organizations/<int:org_id>/staff/ добавлена карма пользователя.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bb890343d ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.279.0 → 0.280.0                                                                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d4e5b78ef ]
 * Обновлён ChangeLog.rst.                                                                                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cd132fcb9 ]
 * Исправлен конфликт, из-за которого попадали тесты.                                                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c8577411f ]
 * Исправлена команда check-permissions.                                                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c47bb0c87 ]
 * Добавлен дополнительный тест на то, что длинное название организации с нормальными словами и без домена - допустимо.                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/13e013d10 ]
 * DIR-6875: Теперь в каждой модифицирующей ручке, записи лога с текстом "Request was authenticated" будут содержать значение его кармы из Паспорта в поле @fields.auth.user.karma.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/14472c09d ]
 * COMPUTERPROBLEM-161: Закрыта дыра через которую спамеры могли создавать домены у которых TLD в верхнем регистре.                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/56d4dfc60 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6693 Разрешить внешнему админу состоять в одной организации как сотрудник/админ  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/07fe5e158 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-09 13:59:48+03:00

0.279.0
-------
 * Bump version: 0.278.0 → 0.279.0                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/befb18527 ]
 * Обновлён ChangeLog.rst.                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ed5c52582 ]
 * DIR-5574 Енкодим имя сингнала                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9ea99e290 ]
 * DIR-5574 Правки по ревью                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/784b2d887 ]
 * DIR-6897 Changelog                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8b514ee3d ]
 * DIR-5574 Отдельные графики по числу запросов от каждого из потребителей API                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b2376d918 ]
 * DIR-6897 Для подмены ссылок на сервисы используем заголовок X-<SLUG>-SERVICE-HOST вместо X-<SLUG>-HOST  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/05754ece8 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-04-08 19:01:43+03:00

0.278.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.277.0 → 0.278.0                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/aa72618e9 ]
 * Обновлён ChangeLog.rst.                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1a1dacdd6 ]
 * DIR-6886 Для всех организаций создаем внешнего робота, если такой есть у сервиса  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/70a8fba3e ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-6598 fix tests  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/698e8abd4 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-04-05 18:04:11+03:00

0.277.0
-------

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * quick fix                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/27967fabf ]
 * quick fix                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bb8fa5bf3 ]
 * Bump version: 0.276.9 → 0.277.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6e28db46b ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/72cfa7580 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * DIR-6685: Отныне для организаций, заведённых из админки или через ПДДшную промку, будет включаться фича can-work-without-owned-domains. (#2616)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c2c25ac3f ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-04-04 10:33:43+03:00

0.276.9
-------
 * Bump version: 0.276.8 → 0.276.9                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ceb0d69af ]
 * Обновлён ChangeLog.rst.                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/84ea32284 ]
 * COMPUTERPROBLEM-161: Теперь проверяем названия организаций на спамность ещё и по словарю.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/86e658de6 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-03 21:24:50+03:00

0.276.8
-------
 * Bump version: 0.276.7 → 0.276.8                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a63e9d595 ]
 * Обновлён ChangeLog.rst.                                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/286c31b7e ]
 * COMPUTERPROBLEM-161: Закрыта дыра через которую можно было создавать организации с названиями типа: ВыПобедилиВашПризНаСайтеwww.vk.com  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a158eeed9 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-03 18:16:42+03:00

0.276.7
-------
 * Bump version: 0.276.6 → 0.276.7                                                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/42296d3c5 ]
 * Обновлён ChangeLog.rst.                                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/686ce36bc ]
 * COMPUTERPROBLEM-161: Добавлена проверка на punicode кодированные зоны доменов, так что теперь мы тоже их считаем невалидными в именах организаций.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d994e1271 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-03 16:57:15+03:00

0.276.6
-------
 * Bump version: 0.276.5 → 0.276.6                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/617da00d6 ]
 * Обновлён ChangeLog.rst.                                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8bf35630a ]
 * COMPUTERPROBLEM-161: Поправлена эвристика, так что теперь даже домены взятые в кавычки - считаются невалидными названиями организации.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0df366235 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-03 10:22:31+03:00

0.276.5
-------
 * Bump version: 0.276.4 → 0.276.5                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4ec73a4f1 ]
 * Обновлён ChangeLog.rst.                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/41fa22725 ]
 * Ещё небольшие правки эвристик.                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1b783bd6b ]
 * COMPUTERPROBLEM-161: Добавлены новые эвристики в правила антиспама.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6189b0927 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-03 08:29:24+03:00

0.276.4
-------
 * Bump version: 0.276.3 → 0.276.4                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1197fce9c ]
 * Обновлён ChangeLog.rst.                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a5502ce92 ]
 * COMPUTERPROBLEM-161: Добавил проверку на спамность в ручку /organization/without-domain/.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e9eba83bc ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-02 23:53:25+03:00

0.276.3
-------
 * Bump version: 0.276.2 → 0.276.3                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f5212a1af ]
 * Обновлён ChangeLog.rst.                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8361e4133 ]
 * COMPUTERPROBLEM-161: Добавлена проверка, что название организации не похоже на спамерское.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3d3fca3a7 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-02 23:02:27+03:00

0.276.2
-------

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * DIR-6782 Исправил версию миграции  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/94b73bb4d ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.276.1 → 0.276.2                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/868efdc46 ]
 * Обновлён ChangeLog.rst.                                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8859ae846 ]
 * DIR-6863: Введено ограничение в 200 символов на длинну названия организации, чтобы спамеры не записывали туда всякую чепуху.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ea1315820 ]
 * DIR-6863: Сделано ограничение в 100 инвайтов на организацию, чтобы "осадить" спамеров.                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/81c993b87 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-02 14:42:55+03:00

0.276.1
-------

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * Bump version: 0.276.0 → 0.276.1  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/76192e71f ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6ca6ce6a0 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * DIR-6779: Библиотека для получения и проверки TVM тикетов перенесена в код Директории.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/778f118e5 ]

[ibabintsev](http://staff/ibabintsev@yandex-team.ru) 2019-04-02 12:28:40+03:00

0.276.0-rc1
-----------

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Поправлено название external-prod.                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a561ebc10 ]
 * Улучшены наши команды по выкатыванию релизов.                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f4a7061fc ]
 * releasing version 0.271.1                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d87df1524 ]
 * Bump version: 0.271.0 → 0.271.1                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/19df484e9 ]
 * Обновлён ChangeLog.rst.                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d8d31584e ]
 * DIR-6792: Поправлен запуск тасков, сохраняющих данные для биллинга и аналитики.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8e02c795f ]
 * releasing version 0.271.0-rc1                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/66eb65ab1 ]
 * releasing version 0.268.0-rc2                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/75d1bd532 ]
 * releasing version 0.268.0-rc1                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e374145d6 ]
 * Исправлено определение текущего датацентра.                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cc18dd9f8 ]
 * releasing version 0.250.0-rc1                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d6482cb86 ]

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * Bump version: 0.275.0 → 0.276.0                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7352bf14f ]
 * Обновлён ChangeLog.rst.                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4691e9d67 ]
 * Добавлена опция --no-tty для apt-key                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8d8e8bd80 ]
 * DIR-6849 Подправил обработку ImmediateReturn                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8f8de3c58 ]
 * DIR-6849 Подправил обработку дефолтных HTTP-ошибок                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f305f99a6 ]
 * DIR-6849 Починили сборку докер образа                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/708387cbc ]
 * DIR-6782 Пофиксил коды ошибок                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9e4777051 ]
 * DIR-6782 Добавил побольше каментов                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7d506a0f0 ]
 * DIR-6782 Решили что назовем контейнер component_registry                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3e89de0be ]
 * DIR-6782 Вызываем expunge_all вместо close, чтобы случайно не закрыть транзакцию на запись                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ec070440c ]
 * DIR-6783 Тест для 404                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c710c37d2 ]
 * DIR-6783 Привел сообщения об ошибках к формату из DIR-6394                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c3f11068a ]
 * DIR-6782 Контекстный менеджер session_compat для обратной совместимости с main_connection, main_connection  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/66b46397b ]
 * DIR-6782 Добавил коментов по запросу от @art                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9b2a0021b ]
 * DIR-6782 пофиксил changelog'и                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/99eafe718 ]
 * DIR-6783 Тесты для поля comment для patch-ручки                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cba2df8b1 ]
 * DIR-6783 Добавлено поле comment для patch-ручки                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/10c08487e ]
 * DIR-6782 Фиксы по замечаниям от khunafin@                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a62a0bb34 ]
 * DIR-6782 Добавил записи в changelog                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9e2470a69 ]
 * DIR-6782 Добавил тесты для patch'а                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9af52a634 ]
 * DIR-6782 Добавил тест для get-ручки                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/44bf1bb90 ]
 * DIR-6782 Ограничиваем права доступа к лимитным ручкам                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ccb38d28a ]
 * DIR-6782 Лимитируем кол-во алиасов для пользователя                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3cb2f4d74 ]
 * DIR-6782 Читаем лимиты по умолчанию из настроек                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/db77c6baa ]
 * DIR-6782 Подготовил механизм лимитов                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8401d3842 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6462 Поправил регулярку                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/61d054eb8 ]
 * DIR-6462 Доработки для /services + инвалидация кэша  по заголовкам                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2da8a83a2 ]
 * WIP                                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e9797fe7e ]
 * DIR-6462 Changelog                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6f89b4c04 ]
 * releasing version 0.273.0                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a2a444514 ]
 * Bump version: 0.272.0 → 0.273.0                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0a258fa3d ]
 * Обновлён ChangeLog.rst.                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/715dae26e ]
 * DIR-6654 Не берем деньги с образовательных организаций Максимальный размер x-request-id увеличен до 100 символов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/40bb51e7a ]
 * DIR-6695 Больше не считаем 0 не валидным значением при валидации через json схему                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/10ca90a1e ]
 * DIR-6695 Больше не считаем 0 и пустую строку не валидным значением при валидации через json схему                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/36dc05bd4 ]
 * DIR-6774 Тесты                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e3181438c ]
 * DIR-6774 Changelog                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/edf795923 ]
 * DIR-6774 golovan-stats-aggregator==2.0.0                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5f58a2405 ]
 * DIR-6462 Ручка GET /ui/headers тепереь принимает загловок X-<SLUG>-HOST для подмены хоста сервиса                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c671aceaf ]
 * releasing version 0.271.0-rc1                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/42d10aaa3 ]
 * releasing version 0.271.0-rc1                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5b99ee911 ]
 * releasing version 0.271.0-rc1                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4778349d9 ]
 * releasing version 0.261.0-rc1                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cc93a530e ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-6598 удалил дубликат       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e588f6baa ]
 * releasing version 0.272.0-rc1  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f626b7155 ]
 * releasing version 0.265.0-rc1  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/53464dd46 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * releasing version 0.272.0                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/87e32c789 ]
 * Bump version: 0.271.1 → 0.272.0                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/38154216a ]
 * Обновлён ChangeLog.rst.                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9f715e602 ]
 * DIR-6570 правильная обработка минимального порога для больших организаций                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7b9bd048e ]
 * DIR-6570 доработала тесты                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6dd4666c1 ]
 * DIR-6570 проверяем снова nickname вместо uid                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ad4f86e6b ]
 * DIR-6570 исправила фильтр, добавила тест                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/446241f49 ]
 * DIR-6670 новая версия функции проверки ответов                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/592587d6f ]
 * DIR-6555 добавила описание тестов + ребейз с мастером                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/433b259c5 ]
 * DIR-6555 удаляем домен из паспорта при удалении организации с has_owned_domains == False  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8e0f171ff ]
 * releasing version 0.250.1-rc1                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c04cb91bf ]

[ibabintsev](http://staff/ibabintsev@yandex-team.ru) 2019-04-01 20:17:52+03:00

0.275.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6652 при создании ящика в миграторе почты приводим nickname к нижнему регистру  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/06b81b55b ]
 * DIR-6671 поправила changelog                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2b9961841 ]
 * DIR-6671 в выдаче v10/organizations/ для пользователя добавлено поле total          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2fdd19883 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6688 Убрала коммент                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cfc534248 ]
 * DIR-6688 Добавлено условие про социальные и light аккаунты  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9255f684e ]
 * DIR-6632 Переименована миграция                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0a87a7807 ]
 * DIR-6688 Правки в форматировании                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4907f51c8 ]
 * DIR-6632 Добавить forms и wiki во все пресеты               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/50d5e7d30 ]
 * DIR-6688 Включить ЯОрг у существующих организаций 70 тыс    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ce4c98e10 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.274.1 → 0.275.0                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d9f60c7fd ]
 * Обновлён ChangeLog.rst.                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fc03a3df6 ]
 * DIR-6362: Устранена 500 ошибка, возникавшая, когда пытаешься через ручку POST /resources/ создать ресурс с одним и тем же id.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a5b47920f ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-04-01 14:11:39+03:00

0.274.1
-------
 * Bump version: 0.274.0 → 0.274.1                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/71d40cf6a ]
 * Обновлён ChangeLog.rst.                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/10c3417af ]
 * Bump version: 0.273.0 → 0.274.0                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/042a83b25 ]
 * Обновлён ChangeLog.rst.                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/97c816642 ]
 * DIR-6598 changelog                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dd030c690 ]
 * DIR-6598 признак уволенности часть 1 (#2612)                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3ce59157b ]
 * Revert "DIR-6598 признак уволенности в meta базе (Часть 2) (#2596)" (#2626)               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bba251030 ]
 * DIR-6598 признак уволенности в meta базе (Часть 2) (#2596)                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/19299096c ]
 * DIR-6598 wrong naming                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4eb36e61f ]
 * DIR-6598 wrong naming                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c84c5c976 ]
 * DIR-6598 fixes                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b6486713f ]
 * Revert "DIR-6598 ревертни меня во второй части задачи"                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7619c842e ]
 * DIR-6676 багфикс                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/078e592bd ]
 * DIR-6676 багфикс                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/071491f41 ]
 * DIR-6598 багфикс                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3af8d1ce7 ]
 * DIR-6598 ревертни меня во второй части задачи                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e5ed06721 ]
 * Revert "DIR-6598 комит который надо revert после того как закончится миграция и команда"  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4138abdc5 ]
 * DIR-6598 признак уволенности часть 1                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ed13c4115 ]
 * DIR-6598 команда для миграции должна работать                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7fb85aa85 ]
 * DIR-6598 migration number                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b44c403ef ]
 * DIR-6598 фиксы без которых не запускается менеджмент команда                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7cfae9fe2 ]
 * DIR-6598 некорректный импорт                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e6c1a3c4c ]
 * DIR-6598 убрал ненужный тест                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ea8b882b5 ]
 * DIR-6598 комит который надо revert после того как закончится миграция и команда           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4b5830069 ]
 * DIR-6598 review                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4df34eea8 ]
 * DIR-6598 review                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7e84f8187 ]
 * форматирование                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f5b28bfd4 ]
 * DIR-6598 тесты, -2 запроса начало и конец транзакции                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8410396a8 ]
 * DIR-6598 не печатать в тестах ничего                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f8613b768 ]
 * DIR-6598 тесты, -2 начала и конца транзакции                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fe4691954 ]
 * DIR-6598 тесты                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e97e3edfa ]
 * DIR-6598 переделал remove_orgs_with_deleted_portal_user                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6a81098b4 ]
 * DIR-6598 пользователь создается с is_dismissed False                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9c9b58ce5 ]
 * DIR-6598 review                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7a9eacb95 ]
 * DIR-6598 changelog                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e31cf3a5c ]
 * DIR-6598 команда для обновления                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a16e57b23 ]
 * DIR-6598 UserMetaModel создается с is_dismissed=False                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/82cf874dd ]
 * DIR-6598 review                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/47cae7d7e ]
 * DIR-6598 changelog                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/aa5806783 ]
 * DIR-6598 признак уволенности в main базе                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f834d20f0 ]
 * DIR-6598 рефакторинг, проходит тесты                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d49297072 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-03-28 16:21:34+03:00

0.273.0
-------
 * Bump version: 0.272.0 → 0.273.0           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a03080d72 ]
 * Обновлён ChangeLog.rst.                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e8f0dbe02 ]
 * DIR-6774 Тесты                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7f07e1e94 ]
 * DIR-6774 Changelog                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4449ed3e0 ]
 * DIR-6774 golovan-stats-aggregator==2.0.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/049804ac6 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-03-25 18:10:09+03:00

0.272.0-rc1
-----------

* [itjune](http://staff/itjune@yandex-team.ru)

 * releasing version 0.250.1-rc1  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c04cb91bf ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * releasing version 0.271.0-rc1             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/42d10aaa3 ]
 * releasing version 0.271.0-rc1             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5b99ee911 ]
 * releasing version 0.271.0-rc1             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4778349d9 ]
 * DIR-6774 golovan-stats-aggregator==2.0.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/049804ac6 ]
 * releasing version 0.261.0-rc1             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cc93a530e ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-6598 wrong naming                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4eb36e61f ]
 * DIR-6598 wrong naming                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c84c5c976 ]
 * DIR-6598 fixes                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b6486713f ]
 * Revert "DIR-6598 ревертни меня во второй части задачи"                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7619c842e ]
 * DIR-6676 багфикс                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/078e592bd ]
 * DIR-6676 багфикс                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/071491f41 ]
 * DIR-6598 багфикс                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3af8d1ce7 ]
 * DIR-6598 ревертни меня во второй части задачи                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e5ed06721 ]
 * Revert "DIR-6598 комит который надо revert после того как закончится миграция и команда"  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4138abdc5 ]
 * DIR-6598 признак уволенности часть 1                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ed13c4115 ]
 * DIR-6598 команда для миграции должна работать                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7fb85aa85 ]
 * DIR-6598 migration number                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b44c403ef ]
 * DIR-6598 фиксы без которых не запускается менеджмент команда                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7cfae9fe2 ]
 * DIR-6598 некорректный импорт                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e6c1a3c4c ]
 * DIR-6598 убрал ненужный тест                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ea8b882b5 ]
 * DIR-6598 комит который надо revert после того как закончится миграция и команда           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4b5830069 ]
 * DIR-6598 review                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4df34eea8 ]
 * DIR-6598 review                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7e84f8187 ]
 * форматирование                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f5b28bfd4 ]
 * DIR-6598 тесты, -2 запроса начало и конец транзакции                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8410396a8 ]
 * DIR-6598 не печатать в тестах ничего                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f8613b768 ]
 * DIR-6598 тесты, -2 начала и конца транзакции                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fe4691954 ]
 * DIR-6598 тесты                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e97e3edfa ]
 * DIR-6598 переделал remove_orgs_with_deleted_portal_user                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6a81098b4 ]
 * DIR-6598 пользователь создается с is_dismissed False                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9c9b58ce5 ]
 * DIR-6598 review                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7a9eacb95 ]
 * DIR-6598 changelog                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e31cf3a5c ]
 * DIR-6598 команда для обновления                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a16e57b23 ]
 * DIR-6598 UserMetaModel создается с is_dismissed=False                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/82cf874dd ]
 * DIR-6598 review                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/47cae7d7e ]
 * DIR-6598 changelog                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/aa5806783 ]
 * DIR-6598 признак уволенности в main базе                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f834d20f0 ]
 * DIR-6598 рефакторинг, проходит тесты                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d49297072 ]
 * releasing version 0.265.0-rc1                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/53464dd46 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * releasing version 0.271.0-rc1                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/66eb65ab1 ]
 * releasing version 0.268.0-rc2                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/75d1bd532 ]
 * releasing version 0.268.0-rc1                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e374145d6 ]
 * Исправлено определение текущего датацентра.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cc18dd9f8 ]
 * releasing version 0.250.0-rc1                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d6482cb86 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-03-25 18:00:19+03:00

0.272.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.271.1 → 0.272.0                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/768802337 ]
 * Обновлён ChangeLog.rst.                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/035c6c7d7 ]
 * DIR-6570 правильная обработка минимального порога для больших организаций                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/be23ad770 ]
 * DIR-6570 доработала тесты                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/db382df27 ]
 * DIR-6570 проверяем снова nickname вместо uid                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/73a081c6b ]
 * DIR-6570 исправила фильтр, добавила тест                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4e029b044 ]
 * DIR-6670 новая версия функции проверки ответов                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/63885e9b9 ]
 * DIR-6555 добавила описание тестов + ребейз с мастером                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6b7bc301f ]
 * DIR-6555 удаляем домен из паспорта при удалении организации с has_owned_domains == False  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/be599509b ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6695 Больше не считаем 0 не валидным значением при валидации через json схему                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/48d62b37b ]
 * DIR-6695 Больше не считаем 0 и пустую строку не валидным значением при валидации через json схему                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9cb3a619d ]
 * DIR-6654 Не берем деньги с образовательных организаций Максимальный размер x-request-id увеличен до 100 символов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4fd18cbb9 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Поправлено название external-prod.             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/473b7b594 ]
 * Улучшены наши команды по выкатыванию релизов.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/60ab7e2e4 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-03-25 11:30:37+03:00

0.271.1
-------
 * Bump version: 0.271.0 → 0.271.1                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1ebc736d6 ]
 * Обновлён ChangeLog.rst.                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1f8335877 ]
 * DIR-6792: Поправлен запуск тасков, сохраняющих данные для биллинга и аналитики.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4b8364974 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-03-22 16:17:45+03:00

0.271.0-rc1
-----------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * releasing version 0.271.0-rc1                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5b99ee911 ]
 * releasing version 0.271.0-rc1                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4778349d9 ]
 * DIR-6774 golovan-stats-aggregator==2.0.0                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/049804ac6 ]
 * DIR-6695 Больше не считаем 0 не валидным значением при валидации через json схему                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/48d62b37b ]
 * DIR-6695 Больше не считаем 0 и пустую строку не валидным значением при валидации через json схему  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9cb3a619d ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * releasing version 0.271.0                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7d8448e98 ]
 * Bump version: 0.270.2 → 0.271.0                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/97a089a29 ]
 * Обновлён ChangeLog.rst.                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e248d4e5 ]
 * DIR-6776 Поправлена ошибка в команде manage migrate, так чтобы она могла напрямую в базы ходить.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ab8123c4b ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-03-21 18:44:37+03:00

0.271.0-rc1
-----------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * releasing version 0.271.0-rc1                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4778349d9 ]
 * DIR-6774 golovan-stats-aggregator==2.0.0                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/049804ac6 ]
 * DIR-6695 Больше не считаем 0 не валидным значением при валидации через json схему                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/48d62b37b ]
 * DIR-6695 Больше не считаем 0 и пустую строку не валидным значением при валидации через json схему  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9cb3a619d ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * releasing version 0.271.0                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7d8448e98 ]
 * Bump version: 0.270.2 → 0.271.0                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/97a089a29 ]
 * Обновлён ChangeLog.rst.                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e248d4e5 ]
 * DIR-6776 Поправлена ошибка в команде manage migrate, так чтобы она могла напрямую в базы ходить.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ab8123c4b ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-03-21 18:43:14+03:00

0.271.0-rc1
-----------

* [itjune](http://staff/itjune@yandex-team.ru)

 * releasing version 0.250.1-rc1  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c04cb91bf ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6774 golovan-stats-aggregator==2.0.0                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/049804ac6 ]
 * DIR-6695 Больше не считаем 0 не валидным значением при валидации через json схему                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/48d62b37b ]
 * DIR-6695 Больше не считаем 0 и пустую строку не валидным значением при валидации через json схему  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9cb3a619d ]
 * releasing version 0.261.0-rc1                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cc93a530e ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * releasing version 0.271.0-rc1                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/66eb65ab1 ]
 * releasing version 0.268.0-rc2                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/75d1bd532 ]
 * releasing version 0.268.0-rc1                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e374145d6 ]
 * Исправлено определение текущего датацентра.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cc18dd9f8 ]
 * releasing version 0.250.0-rc1                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d6482cb86 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * releasing version 0.265.0-rc1  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/53464dd46 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-03-21 18:42:36+03:00

0.271.0
-------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * Bump version: 0.270.1 → 0.270.2                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3ce300c1b ]
 * Обновлён ChangeLog.rst.                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d204a4cec ]
 * Bump version: 0.270.0 → 0.270.1                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bb57a5b8e ]
 * Обновлён ChangeLog.rst.                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4d58dd2f3 ]
 * DIR-6672 Если у сервиса в организации уже есть аналогичный ресурс - возвращаем корректную ошибку  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/914d3b57a ]
 * DIR-6635 Логгировать в dispatch_request все ошибки с трейсбэком                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0bef14b08 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.270.2 → 0.271.0                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/97a089a29 ]
 * Обновлён ChangeLog.rst.                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e248d4e5 ]
 * DIR-6776 Поправлена ошибка в команде manage migrate, так чтобы она могла напрямую в базы ходить.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ab8123c4b ]
 * Перенёс вызов app_context в метод process.                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/99da84956 ]
 * Просто подопнём теств в Sandbox.                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/76836c7ad ]
 * Убрано лишнее логгирование из асинхронных тасков.                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/125125bc6 ]
 * Убрал лишнюю строчку логгирования.                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f29975e03 ]
 * DIR-6676: Теперь почти все асинхронные таски требуют параметр org_id.                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0541c1dfd ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-03-20 14:52:08+03:00

0.270.0
-------
 * Bump version: 0.269.1 → 0.270.0          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d300712 ]
 * Обновлён ChangeLog.rst.                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9c03dbb ]
 * DIR-6675 Создавать рассылку all в таске  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8e0eb87 ]
 * DIR-6675 Создавать рассылку all в таске  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6278417 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-03-19 09:15:56+03:00

0.269.1
-------
 * Bump version: 0.269.0 → 0.269.1                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a26a3a7a8 ]
 * Обновлён ChangeLog.rst.                                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b020af7c5 ]
 * Откатили назад golovan_stats_aggregator до 1.2.3 и futures до 3.0.4, потому что у нас сломалась отгрузка графика с количеством ошибок.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/df0c22ece ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-03-14 20:32:56+03:00

0.269.0
-------

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * DIR-6699: Добавлена поддержка target_session_attrs для команды dbshell  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2cf1392ec ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Исправлено определение текущего датацентра.                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b2e885cd0 ]
 * Bump version: 0.268.0 → 0.269.0                                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6a038c14a ]
 * Обновлён ChangeLog.rst.                                                                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a69b38a92 ]
 * Исправлена ошибка, из-за которой неправильно выбирался master.                                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2d4755d20 ]
 * Добавлен ChangeLog.                                                                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/53eabd416 ]
 * Исправлена "плавающая" ошибка про JSON валидацию сваггер спеки.                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/40006f520 ]
 * DIR-6629: Изменены пресеты tracker и forms.                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fb89d76b5 ]
 * Добавлены настройки, позволяющие ходить с тестинга и прода напрямую в хосты баз.                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c6f06a08d ]
 * Возвращена библиотека environs.                                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/597885044 ]
 * Дополнительно некоторые зависимости зафиксированы на версиях, которые используют соседние команды или Аркадия.                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a370df73f ]
 * Скомпилированы *.txt зависимости.                                                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6ad6d9a72 ]
 * Зафиксированы версии golovan_stats_aggregator==1.3.0 и yandex-yt-yson-bindings==0.3.26.post0.                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1a9b5f1d3 ]
 * DIR-6382: Зафиксированы версии в *.in файлах.                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/91caf7d0b ]
 * Поправлен досадный косяк, выявленный Сэром в Очках в рамках обзирательства кода :)                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9f52a9822 ]
 * DIR-6327: В организацию добавлено поле root_departments, и теперь в ручках, которые отдают информацию про организации можно запрашивать это поле.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a847df7be ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-03-14 19:12:14+03:00

0.268.0
-------
 * Bump version: 0.267.0 → 0.268.0                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8d13ad307 ]
 * Обновлён ChangeLog.rst.                                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/628693cb0 ]
 * Поправлен падавший тест.                                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/18444cabf ]
 * Исправлена ошибка в _create_subtasks, из-за которой миграторы почты ломались на втором этапе.                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a3b9925b8 ]
 * Поправлен тест, который начал падать из-за того, что в параметры таска был добавлен org_id.                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6c0f4aa32 ]
 * DIR-6674: Добавлен org_id в класс, чтобы уникальность тасков считалась для каждой организации.                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/57df19137 ]
 * Миграция 155 поправлена так, чтобы был пример того, как надо добавлять NOT NULL колонку без блокировки базы на длительное время.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c57b4df09 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-03-14 13:22:03+03:00

0.267.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6623 ручка для получения маскированного логина владельца  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a666e7fc9 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.266.0 → 0.267.0                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e6277f0c3 ]
 * Обновлён ChangeLog.rst.                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d3257578d ]
 * DIR-6596 Понизили приоритет у задачи MaillistsCheckTask  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/240bf47c5 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-03-13 14:42:15+03:00

0.266.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6420 поправила тест                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a6ce11b82 ]
 * DIR-6420 пеменяла дефолтное значение для page                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ee06d4fe2 ]
 * DIR-6420 добавила 10 версию апи                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/23bc79735 ]
 * DIR-6420 поправила фильтр                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/488fe8ac2 ]
 * DIR-6420 пагинированный список организаций для пользователя в /organizations/  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/876ad928e ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.265.0 → 0.266.0                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7aef0d5bd ]
 * Обновлён ChangeLog.rst.                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0c1ead1cc ]
 * DIR-6596 Поправлен скрипт проверки рассинхрона подписок с BigMl              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/65aae48e9 ]
 * DIR-6622 Добавлена ручка GET /admin/organizations/<org_id>/access-restores/  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a304b39ff ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-6340 changelog                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/05d602e3c ]
 * DIR-6340 фикс тестов                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/57f780872 ]
 * DIR-6340 review                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/afb719678 ]
 * DIR-6340 review                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0b18eff84 ]
 * DIR-6340 review                                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2c9bf7939 ]
 * DIR-6340 комментарии                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8388acdcb ]
 * DIR-6340 фиксы теста                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c36a91d40 ]
 * DIR-6340 фиксы рефакторинга                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/467125528 ]
 * DIR-6340 фиксы рефакторинга                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ba40197c6 ]
 * DIR-6340 фиксы рефакторинга                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4d664fa66 ]
 * DIR-6340 фиксы рефакторинга                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fab7ed66e ]
 * DIR-6340 явно бросаю FieldsMustComeTogether                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/620317357 ]
 * DIR-6340 фильтровать можно только по resource и resource_service одновременно                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/646b738bb ]
 * DIR-6340: [Directory] Сделать так, чтобы ручка /users/?resource=12345 учитывала service_slug.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f12e04f63 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-03-13 11:06:09+03:00

0.265.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6556 удален clint  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/390b280e4 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.264.0 → 0.265.0                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c460bec7b ]
 * Обновлён ChangeLog.rst.                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ae6ce1a2b ]
 * DIR-6611 NONTRANSACTIONAL migration                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b436c04db ]
 * DIR-6611 Конфликт номера миграции                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8c6896562 ]
 * DIR-6647 Добавлен индекс i_users_id_dismissed                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/084c3fc7b ]
 * DIR-6611 В аналитическую выгрузку для доменов добавлено поле master  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8f8d2ced5 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-03-12 14:50:59+03:00

0.264.0
-------

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * Номер миграции уже заняли, поправил                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ba1030a ]
 * Запускаем миграцию создающую индекс вне транзакции                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e526af1 ]
 * Добавил предупреждение о необходимости миграции                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b6025f0 ]
 * Добавлен индекс на поля org_id, revision, timestamp для таблицы actions  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/46a8fcd ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * Fix changelog                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3ff3415 ]
 * Bump version: 0.263.0 → 0.264.0                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cd95d09 ]
 * Обновлён ChangeLog.rst.                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3a15150 ]
 * DIR-6467 Исправила запрос                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7555a37 ]
 * DIR-6467 Добавила запятую                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3119dba ]
 * DIR-6467 Запрещаем связывать рессурсы с внешними админами ручкой /bind/  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/21791a4 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-03-11 12:22:57+03:00

0.263.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6557 удалена команда get-stats вместе с либами  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/724f936 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * Bump version: 0.262.0 → 0.263.0                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/93917a6 ]
 * Обновлён ChangeLog.rst.                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d23e7ae ]
 * DIR-6645 Не разрешаем пользователям заводить больше 10 алиасов. По мотивам ISEARCH-5855  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b8a61c0 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-03-07 20:48:34+03:00

0.262.0
-------
 * Bump version: 0.261.0 → 0.262.0                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8fce4ced7 ]
 * Обновлён ChangeLog.rst.                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a1e9f5974 ]
 * Добавлена заметка про необходимость миграции.                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d7300a442 ]
 * Переименован файл и функции в нём.                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/16191336d ]
 * Удалена лишняя миграция базы.                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6a96100b1 ]
 * Поправил докстринг функции                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b35d8a755 ]
 * Ещё одно исправление опечатки.                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a1a0ebbe3 ]
 * Поправлена опечатка в имени сигнала.                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/16947d2a4 ]
 * DIR-6140: Добавлена отгрузка в Yasm сигнала org_ids_inconsitencies_axxx.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9cc5a6f48 ]
 * Mogration fixed.                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3cf91fadf ]
 * Починил загрузку bash алиасов в шелле запущенном под tmux.                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7415e9269 ]
 * Добавлен метод batch_userinfo для blackbox.                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/12174be31 ]
 * Добавил пользователю поле updated_at и табличку для сбора статистики.     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fd4220ee2 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-03-06 10:17:49+03:00

0.261.0
-------
 * Bump version: 0.260.0 → 0.261.0                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/186b2d655 ]
 * Обновлён ChangeLog.rst.                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ef50496cd ]
 * DIR-6516 Сбрасываем признак VIP если для него нет больше причин  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dd57a738b ]
 * DIR-6516 Сбрасываем признак VIP если для него нет больше причин  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/524355289 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-03-05 12:16:38+03:00

0.260.0
-------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * Bump version: 0.259.0 → 0.260.0                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ecd87ad ]
 * Обновлён ChangeLog.rst.                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cda74b4 ]
 * DIR-6416 убрала ненужные импорты                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ce8d7a4 ]
 * DIR-6416 Ускорить выбор шарда для новой организации  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d2097ac ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-6439 fix tests  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/98e60e8 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6544 Фиксы тестов                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cfa3a4e ]
 * DIR-6544 Отключили логирование в файл  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1c13781 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Добавлена защита, чтобы команда clear-merged-branches запускалась только на master ветке.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dc283c2 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-03-05 10:23:36+03:00

0.259.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.257.0 → 0.258.0                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7ff32f881 ]
 * Обновлён ChangeLog.rst.                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/356541ea0 ]
 * DIR-6551 менять статус на expired только у попыток восстановления доступа в in_progress  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/56d979d51 ]
 * DIR-6514 каталожные ручки для добавления/удаления whitelist                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/14e6277bc ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Bump version: 0.258.0 → 0.259.0                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1d389a2b7 ]
 * Обновлён ChangeLog.rst.                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9db48148e ]
 * DIR-6314: [Directory] Запретить удаление и блокировку ответственного (#2552)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/19f14ec06 ]
 * DIR-6439: [Directory] Сделать ручку связывания синхронной  (#2553)            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/21c19b62d ]
 * Убрал возможность собирать релиз без свежих тегов                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e4a40f343 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-02-27 18:05:39+03:00

0.257.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.256.0 → 0.257.0                                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1d4f36ca9 ]
 * Обновлён ChangeLog.rst.                                                                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bcdfd359b ]
 * DIR-6248 В выгрузку в YT для orgnizations добавлены поля  name, vip                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/507a7738f ]
 * DIR-6516 Правки по ревью DIR-6517 Правки по ревью                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1c47e5838 ]
 * DIR-6516 Добавлена функция для определения признака VIP для организаций DIR-6517 Добавлен cron и manage.py команда для пересчета признакак VIP  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/52ead8803 ]
 * DIR-6513 Всегда уникальный label пока не возможен                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a9d0e2ac5 ]
 * DIR-6513 Правки по ревью                                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4329f3f7b ]
 * DIR-6424 Починили баг при создании организации с не уникальным лейблом                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/17a98a5c2 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Ещё фиксик к ChangeLog.                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e17dbccd ]
 * Добавил для ChangeLog описание того, что такое штатный отдел и что такое внештатный.                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5a6508c04 ]
 * Добавил логгирование warning на случай, если пытаются получить permission и указывают неправильный id пользователя.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a5ff651ff ]
 * DIR-6506: Добавлен пермишшен move_to_staff для сотрудников которые являются внешними сотрудниками.                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ea11be55c ]
 * DIR-6521: Для отделов теперь можно запрашивать поле is_outstaff.                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b083039ca ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-02-26 17:26:30+03:00

0.256.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6525 использовать get_login  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/97ff8aedf ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.255.0 → 0.256.0                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/aa47be6f6 ]
 * Обновлён ChangeLog.rst.                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d231f7c31 ]
 * DIR-6513 Правки по ревью                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7cbeb829f ]
 * DIR-6407 Расширены права для роли асессор во внутренней админке  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3afbddc2a ]
 * DIR-6513 Для организаций добавлен признак vip                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c69c5ccde ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-02-25 10:57:24+03:00

0.255.0
-------
 * Bump version: 0.254.0 → 0.255.0                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ff96eb743 ]
 * Обновлён ChangeLog.rst.                                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/553da8241 ]
 * Добавил описание команды в README.                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bf795803d ]
 * Добавил команду invoke clear-merged-branches, которая удаляет те ветки, которые смерджены, как из локального гита, так и из GitHub.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/706fdae47 ]
 * Поправлен тест.                                                                                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5dfd22093 ]
 * Добавил кусок changelog.                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7c1c9abfd ]
 * Исправлена версия pyyaml, потому что 4.1 почему-то не находилась в pypi.                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8de25c4cb ]
 * Сделал так, чтобы сборка докер-образа падала если pip не смог поставить зависимости.                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b8a58e187 ]
 * Раскомментил логин в докер в трендбоксовых тасках.                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/838851f8c ]
 * DIR-6264: Исправлена ошибка из-за которой мы не давали админу попытаться удалить самого себя.                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/afae59002 ]
 * Поправил некоторые упавшие тесты.                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/174b9cc28 ]
 * Отключил логин в registry.                                                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2b9a10486 ]
 * DIR-6374: Теперь ручки которые отдают информацию про пользователей, могу отдавать поле is_outstaff.                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d1ae1e7cb ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-02-21 22:16:06+03:00

0.254.0
-------

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Bump version: 0.253.0 → 0.254.0                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bc66c780a ]
 * Обновлён ChangeLog.rst.                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/96b1b07e4 ]
 * Bump version: 0.252.0 → 0.253.0                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e64b2905e ]
 * Обновлён ChangeLog.rst.                                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a697823cb ]
 * changelog DIR-6354                                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5bc3e5855 ]
 * DIR-6354: По инвайтам может добавиться в несколько организаций одновременно (а это мы пока должны запрещать)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/de57d40e6 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Исправлен тест сделанный в рамках задачи DIR-6454.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0e3e4f8e6 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-02-21 12:36:53+03:00

0.252.0
-------

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * DIR-6454 Расширил набор полей для подстановки в _fill_domain_defaults  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/63dc291f3 ]
 * DIR-6454 При редактировании org_name использовать метод domain_edit    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7bbce5f9d ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Поправлено форматирование в ChangeLog.                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/24944b4da ]
 * Bump version: 0.251.0 → 0.252.0                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/21dfd1390 ]
 * Обновлён ChangeLog.rst.                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1f79dbc9f ]
 * Исправил тесты упавшие из-за отсутствия поддержки __in и импорта from yandex_directory.core.events import event  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/00f26ba53 ]
 * Отключил логин в docker registry, так как он поломался и стал отдавать 503.                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/215192e7f ]
 * Поправил ссылку на тикет в ChangeLog.                                                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/41683e772 ]
 * DIR-6459: Отныне мы не позволяем внешним админам принимать инвайты в организации.                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5a47bc425 ]
 * Раньше модель безропотно принимала разные операции по сравнению полей, а теперь на это будет ошибка.             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3b6d9fb07 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-02-19 15:40:11+03:00

0.251.0
-------

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6328 Little fix  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1861a39f1 ]
 * DIR-6328 Outstaff    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/13da6becc ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.250.3 → 0.251.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7a751d824 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a5a2a76dc ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-02-19 11:46:21+03:00

0.250.3
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.250.2 → 0.250.3  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0495df693 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3f93c8139 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6425 Корректно генерируем технические домены для кириллических мастер доменов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b895df951 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-02-18 16:20:14+03:00

0.250.2
-------

* [Alexander Artemenko](http://staff/svetlyak.40wt@gmail.com)

 * DIR-6320: Теперь в событии service_enabled object и content содержат поле responsible_id, которое может быть уидом пользователя или None.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2cbed966b ]
 * Добавлена обработка ответственного в ручке /organizations/<org-id>/.                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/77e6f33bf ]
 * DIR-6313: Теперь можно получить ответственного за сервис в ручке /organizations/.                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3db7d26eb ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.250.1 → 0.250.2  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/53f0b6773 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9bf52d17f ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Явно перечисляем вложенные поля у service, вместо **.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b0d58f5bf ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-6430 deps  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7b6aa3e26 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-02-18 14:52:57+03:00

0.250.1
-------

* [Alexander Artemenko](http://staff/svetlyak.40wt@gmail.com)

 * Откатил изменения из DIR-6320 и DIR-6313                                                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8d8854ba7 ]
 * DIR-6320: Теперь в событии service_enabled object и content содержат поле responsible_id, которое может быть уидом пользователя или None.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6e9f79810 ]
 * Добавлена обработка ответственного в ручке /organizations/<org-id>/.                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/856d33534 ]
 * DIR-6313: Теперь можно получить ответственного за сервис в ручке /organizations/.                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/563b046c7 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.250.0 → 0.250.1                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/62d3974f5 ]
 * Обновлён ChangeLog.rst.                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f95b4fe1c ]
 * DIR-6428 проверка владения раз в 15 минут                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e0f1566a5 ]
 * DIR-6428 поправила тесты                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/09ea984b6 ]
 * DIR-6428 поправила тесты                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5efa89243 ]
 * DIR-6428 добавлена проверка при передаче владения доменом в ПДД  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d1bd4b41f ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6297 Для оправки писем берем коннект к мастер базе                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/783e4ee78 ]
 * DIR-6297 Передаем во все письма про восстановление доступа дату попытки и ip  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a2640d2c7 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Фиксирую версию pip==18.0                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/03ddaabfa ]
 * DIR-6315 review                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c1f6cac14 ]
 * DIR-6315 review                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5112426a3 ]
 * DIR-6315 review                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d400e64cf ]
 * DIR-6315 review                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1ec5a729c ]
 * DIR-6315 review                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ca36211f7 ]
 * DIR-6315 review                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b24bf89e2 ]
 * DIR-6315 review                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/50e12be13 ]
 * DIR-6315 тесты                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/72fc36be5 ]
 * DIR-6315: [Директория] сохранять ответственного в таблицу organization_services  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/94990c545 ]
 * DIR-6355 docstring                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7dff04220 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6269 Fix KeyError                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1b0edcbf4 ]
 * DIR-6356 Fix connection                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8efa8e134 ]
 * DIR-6269 Fix connection                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/601c53210 ]
 * DIR-6356 Fix connection                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f13a9f356 ]
 * DIR-6356 Fix connection                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c06dab312 ]
 * DIR-6269 API для связывания существующей организации с ресурсом              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/44c61014f ]
 * DIR-6269 API для связывания существующей организации с ресурсом              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1b791f149 ]
 * DIR-6356 Даём внешнему админу завести ЯОрганизацию и привязать к ней ресурс  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c5c5268b7 ]

[itjune](http://staff/itjune@yandex-team.ru) 2019-02-14 19:48:41+03:00

0.250.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6304 Отправляем письма о передаче владения в отдельной задаче                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/94007358c ]
 * DIR-6310 Добавлен cron по проверке передачи владения                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dd96aa34a ]
 * DIR-6304 Запускаем передачу владения если домен подтвержден в вебмастере                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/17b00623b ]
 * DIR-6304 Мелкие правки                                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/35e182174 ]
 * DIR-6304 Добавлена задача для передачи владения организацией. DIR-6297 Отправляем письмо о попытке передачи владения.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7263b7fc6 ]

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * DIR-3909 Считаем, что пользователь без информации о сервисе по умолчанию внешний.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3426ded69 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Update README.md  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8da3a9c30 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6358 Связывание ресурса с организацией пятисотит  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/192931c8e ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6384 доработки                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6674d9b2d ]
 * DIR-6309 починила тест             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a0bb68523 ]
 * DIR-6309 правки                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/852a5d856 ]
 * DIR-6309 функция проверки ответов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f70d7f495 ]
 * DIR-6384 правки                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fa679a2e9 ]
 * DIR-6384 source = yt               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/719dfb411 ]
 * DIR-6384 +ченджлог                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eb8134a42 ]
 * DIR-6384 скрипт миграции доменов   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8963695e9 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.249.0 → 0.250.0                                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b4f7d5431 ]
 * Обновлён ChangeLog.rst.                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9f910d4fc ]
 * DIR-6412: Исправлена обработка исключений в потоках, которые обрабатывают таски в очереди задач.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e4407c65d ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2019-02-12 11:00:26+03:00

0.249.0
-------

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * Bump version: 0.248.0 → 0.249.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f6a7a5278 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/479749b3a ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6305 Добавлена обработка ошибки VERIFY_HOST__VERIFICATION_IS_IN_PROGRESS                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eeb034342 ]
 * delete legacy                                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3aad9d649 ]
 * DIR-6302 Правки по ревью                                                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2909860e3 ]
 * DIR-6305 Добавлена ручка POST /restore/<restore_id>/ownership/verify/ DIR-6302 Добавлена ручка GET /restore/<restore_id>/ownership/  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c67e8b06e ]

[ibabintsev](http://staff/ibabintsev@yandex-team.ru) 2019-02-05 14:12:46+03:00

0.248.0
-------

* [Alexander Artemenko](http://staff/svetlyak.40wt@gmail.com)

 * Поправил trendbox образ на версию, в которой исправлена ошибка.                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cc4121085 ]
 * Переместил таск CreateExistingAccountTask в правильное место.                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/298c6eb07 ]
 * Добавлен тест, проверяющий что ручка связывания работает в нормальном режиме.                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5353d034b ]
 * DIR-6312: Добавил для 9 версии ручки GET /users/ докстринг, чтобы она снова появилась в Плейграунде.                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ec5edb59f ]
 * DIR-6266: Добавлена возможность через ручку /bind/ включить сервис, создать ресурс и связать его с указанными сотрудниками.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d1d2d197e ]
 * Код, создающий организацию без домена, вынесен в отдельную функцию create_organization_without_domain.                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6df0796dd ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6170 Fix Не отдается список способов подтверждения домена  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7093f4599 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Bump version: 0.247.1 → 0.248.0                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8cd291e64 ]
 * Обновлён ChangeLog.rst.                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fa05a2a18 ]
 * DIR-6288 review                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/92af4a91a ]
 * DIR-6330 тесты                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/63fa5874e ]
 * DIR-6330 changelog                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bb239ec67 ]
 * DIR-6288 changelog                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7c597f4f2 ]
 * DIR-6288 ревью                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ddd456f01 ]
 * DIR-6330: Ошибка при создании отдела в яорг                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/de0ada9bb ]
 * DIR-6288: Ручка проверки возможности показать виджет связывания  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3718c61fb ]
 * review                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eb50d908f ]
 * Update user.py                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bed9d0903 ]
 * DIR-6274 Исправления                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/54f8a6090 ]
 * Update DIR-6274.rst                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/48c6384a0 ]
 * DIR-6274 review                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f5cebb086 ]
 * DIR-6274 первичный ключ удален, не нужен                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5a856c6ff ]
 * Update DIR-6274.rst                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b0063a6c8 ]
 * DIR-6274 ревью                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fc8691e7a ]
 * DIR-6274 использование инвайтов                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0e157ba6f ]
 * DIR-6274 использование инвайтов                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9b5203e88 ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-02-04 21:01:58+03:00

0.247.1
-------
 * Bump version: 0.247.0 → 0.247.1                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/84b8fe8ef ]
 * Пофиксил неверный класс исключения DomainNotFound  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f7d8ff53e ]

[ibabintsev](http://staff/ibabintsev@yandex-team.ru) 2019-02-04 18:07:13+03:00

0.247.0
-------

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * Bump version: 0.246.1 → 0.247.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/28933a07a ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bc1003370 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6106 Проверка по user_type, а не по is_robot                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/45ca2d470 ]
 * DIR-6106 Правки после ревью                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a2f7a59e0 ]
 * DIR-6106 Исправлена ошибка, из-за которой для робота активировался Диск  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/04632fe7d ]

[ibabintsev](http://staff/ibabintsev@yandex-team.ru) 2019-02-04 14:50:45+03:00

0.246.1
-------

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * Bump version: 0.246.0 → 0.246.1  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0769742be ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b04741b6d ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6166 поменяла схему для POST           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a6cb08424 ]
 * DIR-6166 правки                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/89ecba16a ]
 * DIR-6166 добавила тесты                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ecceda781 ]
 * DIR-6166 ручки для восстановления доступа  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9e6c2ae9a ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Сделал развёрнутое описание исправленной проблемы для ChangeLog  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8f72b2c98 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-6333: Не выполняется асинхронная задача  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/afdcba5ab ]
 * DIR-6333: Не выполняются асинхронные задачи  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8c1436848 ]

[ibabintsev](http://staff/ibabintsev@yandex-team.ru) 2019-02-01 18:21:33+03:00

0.246.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6233 Поправил упавший тест                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e9d0490ff ]
 * DIR-6233 Если мастер домен сменён в ПДД второй раз туда не ходим       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/74673e483 ]
 * DIR-6233 Если мастер домен сменён в паспорте второй раз туда не ходим  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2a35412fb ]

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * Bump version: 0.245.0 → 0.246.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7ddb834cc ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f4ff71c5d ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-6235 review                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/21bd9aa6a ]
 * DIR-6235 review                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/20b7cb374 ]
 * DIR-6235 review                                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6399e425e ]
 * DIR-6235: changelog                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6ee863529 ]
 * DIR-6235: 500 ошибка на старой Яорг без домена с включенными Рассылками в тестинге  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/97a6e89cb ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6270 Проверим, что при добавлении уволенного пользователя по инвайту генерится событие  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6d38d7459 ]
 * DIR-6270 Таск для заведения пользователя существующего в паспорте                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1ee81587f ]
 * DIR-6095 ДОбавлен код, который исправит уже созданных роботов                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a72f91685 ]
 * DIR-6095 BUG: Роботы Вики и Трекера являются внешними админами                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f6ca63efc ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6308 исправила номер мирграции, добавила новое поле  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/10ca82ea9 ]
 * DIR-6308 добавила еще одно поле                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4c3549ea1 ]
 * DIR-6308 таблица для записи попыток восстановления       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/367f9fb94 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * DIR-6272: Добавлен таск CreateResourceTask, который умеет создавать ресурс и связывать его с объектами.                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7654b74d9 ]
 * DIR-6181: В ответ с кодом duplicate_domain добавлен параметр conflicting_org_id, чтобы мы могли средиректить пользователя на организацию, в которой уже есть такой домен.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e92eca085 ]

[ibabintsev](http://staff/ibabintsev@yandex-team.ru) 2019-01-30 16:17:52+03:00

0.245.0
-------

* [Evgenia Fedoseyeva](http://staff/itjune@yandex-team.ru)

 * Обновление зависимостей (#2514)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/98953d975 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6195 затираем external_id при увольнении пользователя  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8b76a7726 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * DIR-6252 Обновляем количество пользоватлей в отделе и в организации при приглашении пользователя  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/260d3d79b ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Bump version: 0.244.0 → 0.245.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6aaf2711d ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f7c370e2f ]
 * Обновление ревьюшницы (#2507)    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7c772f94c ]

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2019-01-25 20:14:27+03:00

0.244.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.243.0 → 0.244.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ddbd29e39 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ce41e1fe9 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-6230 review                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e18f51bd5 ]
 * DIR-6230 восстанавливаем уволенных пользователей по инвайту  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ce74b9769 ]
 * DIR-6230 восстанавливаем уволенных пользователей по инвайту  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/04952fa7d ]
 * DIR-6230 восстанавливаем уволенных пользователей по инвайту  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b31c355c6 ]
 * DIR-6230 небольшой рефакторинг                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b176a622a ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-01-22 19:13:27+03:00

0.243.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.242.0 → 0.243.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/562426f7a ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/eb2344ead ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * DIR-6080: Добавлена manage команда для проверки external_org_ids домена: get-external-org-ids.                                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fcabc9750 ]
 * DIR-6080: Добавлена manage команда set-external-org-ids.                                                                                                                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d1d2453a4 ]
 * DIR-6080: Теперь при добавлении сотрудника в организацию и при увольнении из неё, мы обновляем свойство аккаунта external_organization_ids в паспорте, что приводит к обновлению атрибута 1017 в blackbox.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/023dd310f ]
 * Добавлено прописывание external_organization_ids в случае, когда учётка добавляется.                                                                                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/50e780b19 ]
 * DIR-6080: Добавлен метод set_organization_ids в паспортный клиент.                                                                                                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0ab49811d ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-01-22 14:21:30+03:00

0.242.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.241.0 → 0.242.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/34fd926d2 ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/76f0581e8 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * ревью                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fd64b9097 ]
 * DIR-5903 вырезаем организации в которых пользователь уволен  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/70641804f ]
 * DIR-5903 вырезаем организации в которых пользователь уволен  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ce728a01f ]
 * DIR-5903 вырезаем организации в которых пользователь уволен  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1faae3d91 ]
 * DIR-5903 исправления для удаленных сотрудников               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6983e89d2 ]
 * DIR-5903 удаление из организации                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/85c2bcec3 ]
 * DIR-5903 fixes                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/69ba787b1 ]
 * DIUR-5903 ревью                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c26e19c5f ]
 * DIR-5903 changelog                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f6c46797d ]
 * DIR-5903 исправил ревью                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7a1a5f4cb ]
 * Update chapson.py                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6cf69f1f8 ]
 * DIR-5903 тест                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0c6ebc3fb ]
 * DIR-5903 тесты                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/92d2b364a ]
 * DIR-5903 не удаляю из паспорта yandex учетку                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5684fd682 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Теперь нормализуются имена organization_name только тех master доменов, которые подтверждены, то есть имеют в базе owned=True.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a002bf9e6 ]
 * DIR-5968: Добавлено логгирование и возможность включать progress-bar для команды normalize-org-names.                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ec6c94c37 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-01-22 11:48:11+03:00

0.241.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-5808 Проверяем наличие организации в таске создания роботов.   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b88051ef6 ]
 * DIR-6007 нельзя блокировать и менять роль у владельца организации  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d9a5ed599 ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.240.0 → 0.241.0  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1f9b61d3d ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/df8dcce9d ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Дополнил changelog разъяснениями, что именно было поправлено.                                                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7ca660683 ]
 * Теперь в after_first_domain_became_confirmed мы создаём асинхронную таску для прописывания домену organization_name в паспорте.                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/35d01282b ]
 * Улучшил логгирование и обработку ошибок в таске SetOrganizationNameInPassportTask.                                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5e3b77597 ]
 * DIR-6079: Теперь при дорегистрации домену в Паспорте проставляется organization_name в правильном формате.                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/db453ea3f ]
 * Добавлен расширенный вывод. Так, чтобы можно было посмотреть с какими доменами есть проблемы.                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/479a5a943 ]
 * DIR-5650: Исправлена ошибка, из за которой мы позволяли пользователю попробовать настроить сборку почты из одного ящика в несколько учётных записей Коннекта.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/30d0fef61 ]
 * Добавлена manage команда normalize-org-names, которая проставляет в паспорте всем master доменам правильный organization_name вида: "org_id:12345"             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/676baee9c ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * Bump version: 0.239.0 → 0.240.0                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6cf807286 ]
 * Обновлён ChangeLog.rst.                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/90b76d427 ]
 * Bump version: 0.238.0 → 0.239.0                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/63c65e25d ]
 * Обновлён ChangeLog.rst.                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/83e506cbe ]
 * DIR-6184 При запросе ролей из idm сделать limit=1000  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/35cd28224 ]
 * DIR-5995 Добавлены actions                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/347290e11 ]
 * DIR-5995 Добавлены actions                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3dd096298 ]
 * DIR-5997 Удаление инвайт-кода для отдела              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4e336a5a7 ]
 * Правки после ревью                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0d09b3406 ]
 * DIR-5995 Правки после ревью                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2c7ad1d86 ]
 * DIR-5996 Правки после ревью                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c41dbee1c ]
 * DIR-5996 Ручка создания кода приглашения в отдел      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/42c0ead77 ]
 * DIR-5995 Ручка получения кода приглашения для отдела  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4df80087e ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-5969 changelog                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/462892995 ]
 * DIR-5969: Отсутствие возможности редактирования в разделе "Команды"  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ecde396b8 ]
 * Дополнение к документации (#2498)                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cf0cee16e ]
 * ревью                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c97813a97 ]
 * ревью                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bdb65cfef ]
 * 5989 rst                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e5aeffa7 ]
 * DIR-5989: Добавить permission на добавление/редактирования алиаса    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5bf35da38 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2019-01-18 14:51:37+03:00

0.238.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-6152 контекстный менеджер не работает, если в нем явно брать конекшен к базе, вернула как было  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e9bbc6d6e ]
 * DIR-6152 починила использование конекшенов                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/130d1e0fb ]
 * DIR-6152 запрещаем отрыв доменов у порталов                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8db3e279e ]
 * DIR-6152 убрала разблокировку в контекстный менеджер                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b1af3e4b0 ]
 * DIR-6152 разблокируем домены при отрыве                                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d760ac8ff ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.237.0 → 0.238.0                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/86db0aa8e ]
 * Обновлён ChangeLog.rst.                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c1686dcd3 ]
 * DIR-6172 Не мигрируем домены для yndx.maillists  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a48a555e8 ]

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * DIR-6150 При миграции ящика из ПДД подписываем его на общую рассылку, если у пользователя есть sid 2  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4c111f2be ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * Bump version: 0.236.0 → 0.237.0                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/37e88dcbb ]
 * Обновлён ChangeLog.rst.                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/dc26fe2da ]
 * Обновлён ChangeLog.rst.                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b57b6f074 ]
 * DIR-5964 Правки после ревью                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4009e4f98 ]
 * DIR-5964 Для яорг в ручке /ui/header/ показывать все подключенные сервисы  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2d51edf91 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2018-12-28 14:12:14+03:00

0.236.0
-------
 * Bump version: 0.235.6 → 0.236.0                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2c577a566 ]
 * Обновлён ChangeLog.rst.                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3bd079a95 ]
 * DIR-6142 Поправлен баг в ручке /v6/domains/ во внешнем API  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4afea1e0d ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2018-12-26 19:28:53+03:00

0.235.6
-------

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * releasing version 0.235.6                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fb9712685 ]
 * Bump version: 0.235.5 → 0.235.6                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3c9e13cfd ]
 * Обновлён ChangeLog.rst.                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2361a8b88 ]
 * DIR-6150 При миграции ящика ПДД передаем uid пользователя в create_user  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2aec40a06 ]
 * DIR-6150 При миграции ящика ПДД передаем uid пользователя в create_user  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9d5f796c6 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * Bump version: 0.235.4 → 0.235.5                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0a2bfb67b ]
 * Обновлён ChangeLog.rst.                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f6f869a46 ]
 * DIR-6151 При добавлении портального аккаунта не валидиреум логин в паспорте  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e27fb6a01 ]
 * Bump version: 0.235.3 → 0.235.4                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cbd6d2a27 ]
 * Обновлён ChangeLog.rst.                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/86a16888b ]
 * DIR-6013 Права на управления Почтой                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ffa997749 ]
 * DIR-5907 Порталам нельзя управлять трекером                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/02d5392db ]
 * DIR-5907 Права для управления трекером                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/04e5efc9b ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Поправил запись в ChangeLog.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f1284a19c ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * DIR-6141 Поправили логгирование так, чтобы Qloud подкрашивал ошибки и ворнинги.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2d835c7fc ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * releaser docs  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/52f1f3e47 ]

[ibabintsev](http://staff/ibabintsev@yandex-team.ru) 2018-12-25 19:47:34+03:00

0.235.3
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.235.2 → 0.235.3                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ab7e72d47 ]
 * Обновлён ChangeLog.rst.                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e7bcb3ac1 ]
 * DIR-5888 добавила разблокировку доменов в любом случае              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/04737bbc5 ]
 * DIR-5888 перенесла блокировку в set_domain_as_owned                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8075068f0 ]
 * DIR-5888 блокировка домена                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c8b8deee6 ]
 * DIR-6100 явно берем конекшен в ручках                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a71629638 ]
 * DIR-6100 поменяла параметр id на task_id в выдаче ручек             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cd754b46a ]
 * DIR-6100 убраны пермишены из ручки GET смены владельца организации  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/18c669357 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * Bump version: 0.235.1 → 0.235.2  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c09b352fe ]
 * Обновлён ChangeLog.rst.          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ef46ee1bb ]
 * не накатываем миграцию main 152  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/68064b5f3 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.235.0 → 0.235.1                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3b413ae7f ]
 * Обновлён ChangeLog.rst.                                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/abaa2fbf0 ]
 * Changelog в отдельно файлике.                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3831bb02c ]
 * Вызываем compile-translations даже при сборке просто через invoke docker-build.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6b8c790ed ]

[itjune](http://staff/itjune@yandex-team.ru) 2018-12-24 19:44:43+05:00

0.235.0
-------

[Anton Chaporgin](http://staff/chapson@yandex-team.ru) 2018-12-21 20:54:06+03:00

0.232.3
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.232.2 → 0.232.3                 [ https://github.yandex-team.ru/itjune/yandex-directory/commit/9b36cad4c ]
 * Обновлён ChangeLog.rst.                         [ https://github.yandex-team.ru/itjune/yandex-directory/commit/420761d87 ]
 * DIR-5938 админские ручки для управления фичами  [ https://github.yandex-team.ru/itjune/yandex-directory/commit/1d841e1f9 ]
 * DIR-5805 доработки для сохранения аналитики     [ https://github.yandex-team.ru/itjune/yandex-directory/commit/0674e05b1 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Поправлена загрузка конфига.                                                       [ https://github.yandex-team.ru/itjune/yandex-directory/commit/b6413e62b ]
 * DIR-6021: Сделано ещё более полное разделение окружений для стендов.               [ https://github.yandex-team.ru/itjune/yandex-directory/commit/1a4c69112 ]
 * Bump version: 0.232.1 → 0.232.2                                                    [ https://github.yandex-team.ru/itjune/yandex-directory/commit/28c19c4a8 ]
 * Обновлён ChangeLog.rst.                                                            [ https://github.yandex-team.ru/itjune/yandex-directory/commit/adc808ccd ]
 * DIR-6048: Исправлен выбор шарда в случае, если все шарды пустые.                   [ https://github.yandex-team.ru/itjune/yandex-directory/commit/d24f72498 ]
 * Игнорим файлы с базами, создающимися для юниттестов запущеных в docker-compose.    [ https://github.yandex-team.ru/itjune/yandex-directory/commit/6bb0b08a0 ]
 * Bump version: 0.232.0 → 0.232.1                                                    [ https://github.yandex-team.ru/itjune/yandex-directory/commit/9ac28619d ]
 * Обновлён ChangeLog.rst.                                                            [ https://github.yandex-team.ru/itjune/yandex-directory/commit/e842fe9c9 ]
 * Исправил настройки баз на тестинге так, чтобы они смотрели в новые (пустые) базы.  [ https://github.yandex-team.ru/itjune/yandex-directory/commit/8163d29b8 ]
 * releasing version 0.232.0                                                          [ https://github.yandex-team.ru/itjune/yandex-directory/commit/bfb23581c ]
 * Исправлена manage shell функция get_uid.                                           [ https://github.yandex-team.ru/itjune/yandex-directory/commit/a88f95d12 ]

* [ibabintsev](http://staff/ibabintsev@yandex-team.ru)

 * Настроена покладка данных на arnold вместо banach  [ https://github.yandex-team.ru/itjune/yandex-directory/commit/83db9ca65 ]

* [Andrei Terekhov](http://staff/tserakhau@yandex-team.ru)

 * DIR-5793: Добавил ченджлог                   [ https://github.yandex-team.ru/itjune/yandex-directory/commit/82d400bba ]
 * DIR-5793: Добавить контактное поле telegram  [ https://github.yandex-team.ru/itjune/yandex-directory/commit/d8fe12af8 ]

[itjune](http://staff/itjune@yandex-team.ru) 2018-12-17 12:54:39+03:00

0.232.0
-------

* [Alexander Artemenko](http://staff/svetlyak.40wt@gmail.com)

 * Устанавливаем DEFAULT_QUEUE_NAME для тестовых стендов в название тикета, чтобы разделить очереди тасков.        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/69be9ace8 ]
 * Тест и код поправлен так, чтобы "внешние" роботы могли добавляться и в организациях без домена.                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a29891e00 ]
 * Поправлено название переменной из-за которой падал один тест.                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9f5ba5aef ]
 * Внешние роботы закрыты фичёй CAN_WORK_WITHOUT_OWNED_DOMAIN.                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/508b196de ]
 * Расширено описание в ChangeLog.                                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b875013c9 ]
 * Добавлен коммент в миграцию и ссылка на тикет про то, что надо будет сделать ещё одну миграцию.                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c1ea8e625 ]
 * В ChangeLog добавлена заметка про необходимость миграции.                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/76d4fc522 ]
 * Теперь модель RobotService имеет поле org_id и ограничение уникальности накладывается на (org_id, uid).         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/061fa69c7 ]
 * DIR-5915: Теперь если у сервиса указан robot_uid, то для этого робота будет использоватся существующая учётка.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a7e272408 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Bump version: 0.231.1 → 0.232.0                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5706f6be3 ]
 * Обновлён ChangeLog.rst.                                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d21faf696 ]
 * Поправлен один из тестов.                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c378bd764 ]
 * Отключил SENTRY_DSN для всех окружений, так как Sentry всё равно не работает.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/7373dcbfc ]
 * Исправлена ошибка, из-за которой не получалось накатить миграцию.              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a55cea619 ]
 * Поправлено форматирование ChangeLog.                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bcb9f7753 ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * DIR-5914 migration renamed                                          [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a131a24f1 ]
 * Update users.py                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/5cb690c7f ]
 * DIR-5916 review                                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c63b2e169 ]
 * deps                                                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/6a7ede81f ]
 * зависимости                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/752796b77 ]
 * DIR-5916 тесты, вызовы                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b9acf6e8f ]
 * optimization fix                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/62ce87450 ]
 * DIR-5916 update requirements                                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e4e589c56 ]
 * DIR-5916: Не выдавать oauth токен для внешних роботов               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d1dba4cf8 ]
 * DIR-5914 ревью                                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a70fa3a57 ]
 * review                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/822680b78 ]
 * review                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a95a710cd ]
 * review                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/86283af15 ]
 * review                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/03c1c0e7c ]
 * DIR-5914: В модель сервиса добавить поле robot_uid и заполнить его  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ea00d5b35 ]
 * DIR-5914: В модель сервиса добавить поле robot_uid и заполнить его  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a8420c0e8 ]

[Alexander Artemenko](http://staff/art@yandex-team.ru) 2018-12-10 18:51:06+03:00


0.231.1
-------

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2018-12-10 16:52:55+03:00

0.231.0
-------

* [itjune](http://staff/itjune@yandex-team.ru)

 * DIR-5947 поменяла код ошибки в каталоге        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0d71f9ef7 ]
 * DIR-5947 добавила обработку DuplicatedTask     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/29baa0e92 ]
 * DIR-5947 починила тесты                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0d75f2b04 ]
 * DIR-5993 починила тест                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c6c213707 ]
 * DIR-5993 при увольнении админа возвращаем 422  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a5d68b51a ]
 * DIR-5947 правки + ребейз с мастером            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9245a415c ]
 * DIR-5947 добавила экшон                        [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a659f626c ]
 * DIR-5947 тесты                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bf8bbeea8 ]
 * DIR-5947 ручка смены владельца                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/addd94d4f ]

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.230.0 → 0.231.0                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/86133c0dd ]
 * Обновлён ChangeLog.rst.                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/56f5c7bc8 ]
 * DIR-6001 Правки по ревью                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/22a4328e8 ]
 * DIR-6001 Для внутреннего админа не отнимаем права при передаче владения.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c57e181e4 ]

[Nail Khunafin](http://staff/khunafin@yandex-team.ru) 2018-12-10 15:22:09+03:00

0.230.0
-------

* [Nail Khunafin](http://staff/khunafin@yandex-team.ru)

 * Bump version: 0.229.0 → 0.230.0               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fe37093 ]
 * Обновлён ChangeLog.rst.                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e188d99 ]
 * DIR-5939 Лениво создаем пользователей         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/444f6c6 ]
 * DIR-5939 Правки по ревью                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d295013 ]
 * DIR-5939 Доработка скрипта миграции порталов  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d0f682a ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2018-12-07 11:51:34+03:00

0.229.0
-------

* [Alexander Artemenko](http://staff/svetlyak.40wt@gmail.com)

 * Поправлены тесты.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/a14f677 ]

* [itjune](http://staff/itjune@yandex-team.ru)

 * Bump version: 0.228.1 → 0.228.2                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/077379b ]
 * Обновлён ChangeLog.rst.                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3be79eb ]
 * DIR-5805 правки после тестирования                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e27338c ]
 * DIR-5805 правки                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/f6c41bd ]
 * DIR-5965 починила тест                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4df5daa ]
 * DIR-5805 починила тесты                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/e8de7f2 ]
 * DIR-5965 добавлена фича передачи владения организацией  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/df9a1c1 ]
 * DIR-5805 рефакторинг сохранения аналитики               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1e33aa9 ]

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * Bump version: 0.228.2 → 0.229.0                                     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/fd928d7 ]
 * Обновлён ChangeLog.rst.                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/cf5d08d ]
 * DIR-5937 Яндекс организациям с доменом добавлены недостающие права  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/91672a8 ]
 * DIR-5904 Исправлен тест                                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/3e57420 ]
 * DIR-5904 Удаление яндекс организации                                [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/961f8d5 ]
 * DIR-5937 Правки после ревью                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/317b967 ]
 * DIR-5937 Правки после ревью                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ab71636 ]
 * DIR-5937 Поправлены импорты                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8ee0f2e ]
 * DIR-5937 Рефакторинг прав доступа                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/71ef192 ]
 * DIR-5906 Добавлен тест                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bde28f4 ]
 * DIR-5906 Ручка для проверки является ли пользователь внутренним     [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/8b245d2 ]

* [Alexander Artemenko](http://staff/art@yandex-team.ru)

 * Добавил допольнительно логгирование с текстом "Deleting organization"                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/4424cc3 ]
 * Поправлена опечатка.                                                                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/74b7759 ]
 * Поправлено время запуска в Changelog.                                                                                                                              [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/70342b8 ]
 * Поправлено форматирование Changelog.                                                                                                                               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ff5f20f ]
 * DIR-5883: При запросе ручек Вебмастера мы больше не будем логгировать как ошибки, те ответы, коды которых перечислены как "нормальные" в параметре ignore_errors.  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bc1895a ]

* [Anton Chaporgin](http://staff/chapson@yandex-team.ru)

 * Update README.md                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0fc6cec ]
 * TOOLS-2248 Правильный конфиг для кросс-ревью (#2437)  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2c20518 ]
 * Update README.md                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/084c4ce ]
 * TOOLS-2248                                            [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/734845a ]
 * Update README.md                                      [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/341a5b7 ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2018-12-05 18:05:52+03:00

0.228.1
-------
 * Bump version: 0.228.0 → 0.228.1                                                   [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/d14363919 ]
 * Обновлён ChangeLog.rst.                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/38f3938c4 ]
 * DIR-5954: SyncDomainsWithPDDTask выполняется в read-only транзакции               [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/edf8ee01e ]
 * DIR-5941: Фиксы + тесты                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/2fec75133 ]
 * DIR-5941: При редактировании мастер домена в паспорте всегда передавать org_name  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/1539082e0 ]

[ibabintsev](http://staff/ibabintsev@yandex-team.ru) 2018-11-29 17:08:00+03:00

0.228.0
-------
 * releasing version 0.228.0                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/bd21f37 ]
 * releasing version 0.228.0                                                                       [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/0bbe20a ]
 * Bump version: 0.227.2 → 0.228.0                                                                 [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/803d9d1 ]
 * Обновлён ChangeLog.rst.                                                                         [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ef12b53 ]
 * DIR-5857 merge commit                                                                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/ada5e4a ]
 * DIR-5857 format_date_for_test -> format_date                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/9288b10 ]
 * DIR-5857 format_date -> format_date_for_test                                                    [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/c08df43 ]
 * DIR-5855 Исправлено форматирование в changelog                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/490b80f ]
 * DIR-5857 API для списка ссылок                                                                  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/01536f2 ]
 * DIR-5855 В код использования инвайта добавлены дополнительные условия                           [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/931f66f ]
 * DIR-5855 Переименована таблица yandexuid_invites -> used_invites, небольшие правки после ревью  [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/67f75eb ]
 * DIR-5855 По одному инвайт-коду можно приглашать несколько аккаунтов                             [ https://github.yandex-team.ru/yandex-directory/yandex-directory/commit/b19405f ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2018-11-29 15:07:57+03:00

0.227.2
-------

[ibabintsev](http://staff/ibabintsev@yandex-team.ru) 2018-11-28 16:51:47+03:00

