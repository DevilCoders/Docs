3.4.48
------
 * CERTOR-2187: update linuxoid email template  [ https://a.yandex-team.ru/arc/commit/9683003 ]

[lithium](http://staff/lithium) 2022-07-06 16:29:17+03:00

3.4.47
------
 * CERTOR-2168: update linuxoid email template  [ https://a.yandex-team.ru/arc/commit/9671432 ]

[lithium](http://staff/lithium) 2022-07-04 18:30:31+03:00

3.4.46
------
 * feat(db): forgotten migration  [ https://a.yandex-team.ru/arc/commit/9649001 ]

[rocco66](http://staff/rocco66) 2022-06-29 13:15:00+03:00

3.4.45
------
 * feat(host-to-approve): optional globalsign domain  [ https://a.yandex-team.ru/arc/commit/9648326 ]

[rocco66](http://staff/rocco66) 2022-06-29 11:52:51+03:00

3.4.44
------
 * fix(globalsign): fix validation code regex again  [ https://a.yandex-team.ru/arc/commit/9642107 ]

[rocco66](http://staff/rocco66) 2022-06-28 10:02:30+03:00

3.4.43
------
 * CERTOR-2160 fix(globalsign): validation code regex  [ https://a.yandex-team.ru/arc/commit/9609102 ]

[rocco66](http://staff/rocco66) 2022-06-20 14:34:17+03:00

3.4.42
------
 * CERTOR-2160 feat(globalsign): autovalidation  [ https://a.yandex-team.ru/arc/commit/9607935 ]

[rocco66](http://staff/rocco66) 2022-06-20 12:03:32+03:00

3.4.41
------
 * CERTOR-2160: fix broken globalsign issue cert  [ https://a.yandex-team.ru/arc/commit/9569150 ]

[rocco66](http://staff/rocco66) 2022-06-09 11:28:59+03:00

3.4.40
------

* [rocco66](http://staff/rocco66)

 * CERTOR-2160: save globalsign domain verification info  [ https://a.yandex-team.ru/arc/commit/9564557 ]

* [zivot](http://staff/zivot)

 * Change ".monitorado.yml"  [ https://a.yandex-team.ru/arc/commit/9531534 ]

[rocco66](http://staff/rocco66) 2022-06-08 15:29:23+03:00

3.4.39
------

* [zivot](http://staff/zivot)

 * CERTOR-2143: revert импорта admin-smartcard                                       [ https://a.yandex-team.ru/arc/commit/9347079 ]
 * CERTOR-2144: Отзыв VPN-токенов после выдачи новых или оборудования                [ https://a.yandex-team.ru/arc/commit/9345135 ]

[zivot](http://staff/zivot) 2022-04-13 18:12:00+03:00

3.4.38
------
 * CERTOR-2143: Импорт admin-smartcard  [ https://a.yandex-team.ru/arc/commit/9326218 ]

[zivot](http://staff/zivot) 2022-04-08 11:26:21+03:00

3.4.37
------
 * CERTOR-2137: Приклеить кросс-сертификаты к intermediate'ам GS  [ https://a.yandex-team.ru/arc/commit/9266513 ]

[zivot](http://staff/zivot) 2022-03-23 23:07:58+03:00

3.4.36
------
 * CERTOR-2132: sync env type override  [ https://a.yandex-team.ru/arc/commit/9249200 ]

[zivot](http://staff/zivot) 2022-03-18 15:15:33+03:00

3.4.35
------
 * CERTOR-2132: Поменять в тестинге url staff на прод  [ https://a.yandex-team.ru/arc/commit/9246760 ]

[zivot](http://staff/zivot) 2022-03-17 23:44:13+03:00

3.4.34
------
 * CERTOR 2126 Use existing certificate template for bank-client-server certificates  [ https://a.yandex-team.ru/arc/commit/9244329 ]

[squirrel](http://staff/squirrel) 2022-03-17 15:16:46+03:00

3.4.33
------
 * CERTOR-2126 Bank client-server certificate support  [ https://a.yandex-team.ru/arc/commit/9240239 ]

[squirrel](http://staff/squirrel) 2022-03-16 16:50:20+03:00

3.4.32
------

* [poletansky](http://staff/poletansky)

 * CERTOR-2125: skip groups without parents  [ https://a.yandex-team.ru/arc/commit/9234544 ]

* [dsamuylov](http://staff/dsamuylov)

 * ARCANUM-5510 prepare migration from .devexp.json to a.yaml (intranet)  [ https://a.yandex-team.ru/arc/commit/9231012 ]

[poletansky](http://staff/poletansky) 2022-03-15 13:40:04+03:00

3.4.31
------
 * CERTOR-2116: Убираем common_name 'www.' из SANs для globalsign  [ https://a.yandex-team.ru/arc/commit/9216761 ]
 * CERTOR-2116: globalsign 6 месяцев, поддержка .рф в common_name  [ https://a.yandex-team.ru/arc/commit/9205655 ]
 * CERTOR-2116: Очистка \r в PEM сертификате                       [ https://a.yandex-team.ru/arc/commit/9205035 ]

[zivot](http://staff/zivot) 2022-03-09 20:38:41+03:00

3.4.28
------
 * CERTOR-2116: Цепочка для ECC globalsign, отключение yandex.ua, yandex.com.ua  [ https://a.yandex-team.ru/arc/commit/9204166 ]
 * CERTOR-2116: Убираем SANs из заявки GS, если в SAN только CN                  [ https://a.yandex-team.ru/arc/commit/9203689 ]
 * CERTOR-2116: Делаем common_name wildcard для globalsign                       [ https://a.yandex-team.ru/arc/commit/9203181 ]
 * CERTOR-2116: Несколько wildcard для GlobalSign                                [ https://a.yandex-team.ru/arc/commit/9201956 ]

[zivot](http://staff/zivot) 2022-03-04 16:21:18+03:00

3.4.24
------
 * CERTOR-2116: Переход с Certum на GlobalSign  [ https://a.yandex-team.ru/arc/commit/9201811 ]

[zivot](http://staff/zivot) 2022-03-03 23:29:34+03:00

3.4.23
------
 * sync-crl task is enabled in testing  [ https://a.yandex-team.ru/arc/commit/9172200 ]
 * CERTOR-2070: juggler-configs         [ https://a.yandex-team.ru/arc/commit/9172022 ]

[zivot](http://staff/zivot) 2022-02-28 20:02:24+03:00

3.4.22
------

* [poletansky](http://staff/poletansky)

 * CERTOR-2090-1: Remove inconsistent offers

skip and monitor staff inconsistencies  [ https://a.yandex-team.ru/arc/commit/9150848 ]

* [artanis](http://staff/artanis)

 * CERTOR-2100 Change error message to more verbose  [ https://a.yandex-team.ru/arc/commit/9150849 ]

* [maratik](http://staff/maratik)

 * feat: startrek integration for CERTOR ARCANUM-5357

feat: startrek integration  [ https://a.yandex-team.ru/arc/commit/9150338 ]
 * Revert commit r9099792                                                          [ https://a.yandex-team.ru/arc/commit/9100103 ]
 * feat: startrek integration for CERTOR ARCANUM-5357

feat: startrek integration  [ https://a.yandex-team.ru/arc/commit/9099792 ]

* [shadchin](http://staff/shadchin)

 * Update django-extensions from 2.2.9 to 3.1.5                                                         [ https://a.yandex-team.ru/arc/commit/9139388 ]
 * CONTRIB-2153 Update amqp from 2.6.1 to 5.0.9, kombu from 4.6.3 to 5.2.3, celery from 4.3.0 to 5.2.3  [ https://a.yandex-team.ru/arc/commit/9091829 ]

* [rocco66](http://staff/rocco66)

 * Change "test_host_formatting.py"	[ https://a.yandex-team.ru/arc/commit/9134605 ]

* [danila-eremin](http://staff/danila-eremin)

 * IGNIETFERRO-1976 Fix logging in intranet	[ https://a.yandex-team.ru/arc/commit/9117978 ]

* [zivot](http://staff/zivot)

 * CERTOR-2067: убрал мониторинг 4хх   [ https://a.yandex-team.ru/arc/commit/9090117 ]
 * CERTOR-2067: CRT AWACS monitorings  [ https://a.yandex-team.ru/arc/commit/9088909 ]

[poletansky](http://staff/poletansky) 2022-02-16 17:33:46+03:00

3.4.21
------

* [zivot](http://staff/zivot)

 * CERTOR-2084: Исправить фильтр по username                    [ https://a.yandex-team.ru/arc/commit/9077046 ]
 * CERTOR-2078: Добавить в шаблон sdc Subject Alternative Name  [ https://a.yandex-team.ru/arc/commit/9076898 ]
 * CERTOR-1896: Добавить helpdesk_ticket в ручку reissue        [ https://a.yandex-team.ru/arc/commit/9076678 ]

* [danila-eremin](http://staff/danila-eremin)

 * Fix flaky test #2  [ https://a.yandex-team.ru/arc/commit/9060773 ]
 * Fix flaky test #1  [ https://a.yandex-team.ru/arc/commit/9060772 ]

[zivot](http://staff/zivot) 2022-01-27 12:26:26+03:00

3.4.20
------
 * CERTOR-2073: Affilation for hired  [ https://a.yandex-team.ru/arc/commit/9052077 ]

[poletansky](http://staff/poletansky) 2022-01-20 12:53:40+03:00

3.4.19
------

* [poletansky](http://staff/poletansky)

 * CERTOR-1819: Validate type validity in ca_name before saving cert to db [ https://a.yandex-team.ru/arc/commit/9047600 ]
 * fix-ussr-misspelling: Fix misspelling in test [ https://a.yandex-team.ru/arc/commit/9033327 ]

* [zivot](http://staff/zivot)

 * Change "README.md"  [ https://a.yandex-team.ru/arc/commit/9028308 ]

[poletansky](http://staff/poletansky) 2022-01-19 12:57:10+03:00

3.4.18
------
 * CERTOR-1902: Update /hosts/auto-managed route [ https://a.yandex-team.ru/arc/commit/9027666 ]

[poletansky](http://staff/poletansky) 2022-01-13 15:18:25+03:00

3.4.17
------
 * CERTOR-2076: Добавить rtc-oc.yandex.net в whitelist YandexRCCA  [ https://a.yandex-team.ru/arc/commit/9019985 ]

[zivot](http://staff/zivot) 2022-01-11 17:08:51+03:00

3.4.16
------
 * CERTOR-2017: Сертификаты bank-pc  [ https://a.yandex-team.ru/arc/commit/9014780 ]

[zivot](http://staff/zivot) 2022-01-10 13:29:31+03:00

3.4.15
------
 * CERTOR-2072: Log CaError instead of saving to temporary file  [ https://a.yandex-team.ru/arc/commit/9014323 ]

[poletansky](http://staff/poletansky) 2022-01-10 12:04:34+03:00

3.4.14
------
 * CERTOR-2063-fix: Add thresholds, update task monitoring Revert "PR from branch users/rocco66/feature/revert-some-crt-prs" [ https://a.yandex-team.ru/arc/commit/8999485 ]

[poletansky](http://staff/poletansky) 2021-12-29 17:08:08+03:00

3.4.13
------

* [rocco66](http://staff/rocco66)

 * PR from branch users/rocco66/feature/revert-some-crt-prs

Revert "CERTOR-2063: Add certificates limit overriding" and his fixes  [ https://a.yandex-team.ru/arc/commit/8995231 ]

[zivot](http://staff/zivot) 2021-12-28 15:05:33+03:00

3.4.12
------

 * fix-file-formats: Fix tags in file formats & setial->setial_number [ https://a.yandex-team.ru/arc/commit/8994407 ]

 * fix-cvs-upload-tags-file-format: Fix file format in sync_cvs_tags task [ https://a.yandex-team.ru/arc/commit/8992000 ]

[poletansky](http://staff/poletansky) 2021-12-28 12:39:32+03:00

3.4.11
------

* [poletansky](http://staff/poletansky)

 * CERTOR-2063: Add certificates limit overriding

* [zivot](http://staff/zivot)

 * tests fix                             [ https://a.yandex-team.ru/arc/commit/8984816 ]
 * CERTOR-2065: Фикс get_reissue_user()  [ https://a.yandex-team.ru/arc/commit/8960778 ]

* [shadchin](http://staff/shadchin)

 * Update django-constance from 2.5.0 to 2.6.0                [ https://a.yandex-team.ru/arc/commit/8966771 ]
 * FEMIDA-6893 Update django-model-utils from 3.1.2 to 4.2.0  [ https://a.yandex-team.ru/arc/commit/8964104 ]

[poletansky](http://staff/poletansky) 2021-12-24 15:15:20+03:00

3.4.10
------

* [poletansky](http://staff/poletansky)

 * CERTOR-1965: Отключение мониторинга на sync сертификаты в HungCertificatesView. [ https://a.yandex-team.ru/arc/commit/8956710 ]

* [zivot](http://staff/zivot)

 * get_addition_fields optimization  [ https://a.yandex-team.ru/arc/commit/8944280 ]

[poletansky](http://staff/poletansky) 2021-12-16 14:17:12+03:00

3.4.9
-----
 * CERTOR-2055: Пермишен на выписывание vpn-token для себя  [ https://a.yandex-team.ru/arc/commit/8913013 ]

[zivot](http://staff/zivot) 2021-12-07 17:42:27+03:00

3.4.8
-----
 * CERTOR-2054: Улучшенный текст письма, фидбэк на st/CERTOR  [ https://a.yandex-team.ru/arc/commit/8857799 ]

[zivot](http://staff/zivot) 2021-11-22 12:28:06+03:00

3.4.7
-----
 * CERTOR-1915: Улучшить логирование изменений в тегфильтрах  [ https://a.yandex-team.ru/arc/commit/8837479 ]

[zivot](http://staff/zivot) 2021-11-17 12:23:26+03:00

3.4.6
-----
 * CERTOR-1869: Запретить vpn-token для allstaff || has_hw  [ https://a.yandex-team.ru/arc/commit/8822787 ]

[zivot](http://staff/zivot) 2021-11-12 11:52:52+03:00

3.4.5
-----
 * CERTOR-2042: Win-wh-shared new OID  [ https://a.yandex-team.ru/arc/commit/8770690 ]
 * crt sandbox build changes           [ https://a.yandex-team.ru/arc/commit/8757700 ]

[zivot](http://staff/zivot) 2021-10-26 15:10:00+03:00

3.4.4
-----
 * CERTOR-2040: exclude_from_monitoring для validation  [ https://a.yandex-team.ru/arc/commit/8757500 ]

[zivot](http://staff/zivot) 2021-10-21 19:34:59+03:00

3.4.3
-----
 * CERTOR-2023: import_internal_ca_certs tz fix  [ https://a.yandex-team.ru/arc/commit/8714008 ]
 * CERTOR-2023: sync_tags каждые 5 минут         [ https://a.yandex-team.ru/arc/commit/8712250 ]

[zivot](http://staff/zivot) 2021-10-08 11:36:35+03:00

3.4.2
-----

* [zivot](http://staff/zivot)

 * CERTOR-2024: Тормозит /approverequest/                [ https://a.yandex-team.ru/arc/commit/8711967 ]
 * CERTOR-2023: import_internal_ca_certs каждые 5 минут  [ https://a.yandex-team.ru/arc/commit/8710170 ]

* [shadchin](http://staff/shadchin)

 * DEVTOOLSSUPPORT-12493 Drop ResourceFinder

Текущая реализация `library.python.django.contrib.staticfiles.finders.ResourceFinder` эквивалентна `django.contrib.staticfiles.finders.FileSystemFinder`  [ https://a.yandex-team.ru/arc/commit/8711107 ]

[zivot](http://staff/zivot) 2021-10-07 17:41:08+03:00

3.4.1
-----
 * CERTOR-2021: approverEmail admin@yandex.ru  [ https://a.yandex-team.ru/arc/commit/8708519 ]
 * DEVTOOLSUP-16881: Подключение к автосборке  [ https://a.yandex-team.ru/arc/commit/8695549 ]

[zivot](http://staff/zivot) 2021-10-06 19:40:16+03:00

3.4.0
------
 * CERTOR-1784: CRT в Y.Deploy  [ https://a.yandex-team.ru/arc/commit/8690509 ]

[zivot](http://staff/zivot) 2021-10-01 12:25:27+03:00

3.3.65
------

* [zivot](http://staff/zivot)

 * CERTOR-2006: Поправить CertumCA в соответствии с изменениями API  [ https://a.yandex-team.ru/arc/commit/8680086 ]

* [ezaitov](http://staff/ezaitov)

 * Allow to filter requests by requester  [ https://a.yandex-team.ru/arc/commit/8672275 ]

[zivot](http://staff/zivot) 2021-09-28 20:32:26+03:00

3.3.64
------

* [zivot](http://staff/zivot)

 * CERTOR-2011: Старая ручка BOT для RequestLinuxCertificate  [ https://a.yandex-team.ru/arc/commit/8663951 ]

* [rocco66](http://staff/rocco66)

 * feat(arcadia): strong mode for crt  [ https://a.yandex-team.ru/arc/commit/8630271 ]

[zivot](http://staff/zivot) 2021-09-23 21:47:27+03:00

3.3.63
------
 * CERTOR-2004: Доп поля в сертификаты zombie  [ https://a.yandex-team.ru/arc/commit/8628342 ]
 * CERTOR-1987: Сертификаты vpn-1d             [ https://a.yandex-team.ru/arc/commit/8625400 ]

[zivot](http://staff/zivot) 2021-09-14 20:18:48+03:00

3.3.62
------
 * CERTOR-1946: Выгружать в yav сконкатинированный crt+key  [ https://a.yandex-team.ru/arc/commit/8609386 ]
 * CERTOR-2001: Исключаем IDM-тегфильтры из синка           [ https://a.yandex-team.ru/arc/commit/8609364 ]

[zivot](http://staff/zivot) 2021-09-09 12:08:28+03:00

3.3.61
------
 * CERTOR-1958: Складываем zombie-сертификаты Маркета в yav    [ https://a.yandex-team.ru/arc/commit/8589073 ]
 * CERTOR-1979: Разрешаем /reissue/ если юзер не найден в BOT  [ https://a.yandex-team.ru/arc/commit/8587002 ]

[zivot](http://staff/zivot) 2021-09-03 12:52:40+03:00

3.3.60
------
 * CERTOR-1976: Фикс синхронизации неактивного тега  [ https://a.yandex-team.ru/arc/commit/8541401 ]

[zivot](http://staff/zivot) 2021-08-20 10:43:06+03:00

3.3.59
------
 * CERTOR-1972: timestamp finish index added  [ https://a.yandex-team.ru/arc/commit/8539099 ]

[zivot](http://staff/zivot) 2021-08-19 16:46:27+03:00

3.3.58
------
 * CERTOR-1972: pc_inum, pc_serial_number indexes added  [ https://a.yandex-team.ru/arc/commit/8530863 ]

[zivot](http://staff/zivot) 2021-08-17 17:29:11+03:00

3.3.57
------
 * CERTOR-1972: common_name index added  [ https://a.yandex-team.ru/arc/commit/8529002 ]

[zivot](http://staff/zivot) 2021-08-17 11:50:04+03:00

3.3.56
------
 * CERTOR-1963: Увеличить лимит new,removed для cvs_upload  [ https://a.yandex-team.ru/arc/commit/8497132 ]

[zivot](http://staff/zivot) 2021-08-06 18:32:17+03:00

3.3.55
------
 * CERTOR-1957: Разные таймауты мониторинга для разных тасок  [ https://a.yandex-team.ru/arc/commit/8496097 ]
 * CERTOR-1955: Увеличить время холда при /reissue/           [ https://a.yandex-team.ru/arc/commit/8495961 ]

[zivot](http://staff/zivot) 2021-08-06 15:56:49+03:00

3.3.54
------
 * CERTOR-1960: Новые ручки BOT  [ https://a.yandex-team.ru/arc/commit/8488644 ]

[zivot](http://staff/zivot) 2021-08-04 19:24:51+03:00

3.3.53
------
 * CERTOR-1938: Белый список логинов для PDAS                 [ https://a.yandex-team.ru/arc/commit/8486156 ]
 * CERTOR-1954: Валидировать pc_inum в /reissue/              [ https://a.yandex-team.ru/arc/commit/8486148 ]
 * CERTOR-1952: Выгружать в NOC сертификаты без пользователя  [ https://a.yandex-team.ru/arc/commit/8486142 ]

[zivot](http://staff/zivot) 2021-08-04 12:22:00+03:00

3.3.52
------
 * CERTOR-1900: Возможность навесить тег по SN  [ https://a.yandex-team.ru/arc/commit/8420908 ]

[zivot](http://staff/zivot) 2021-07-15 13:36:27+03:00

3.3.51
------

* [zivot](http://staff/zivot)

 * CERTOR-1941: Поле pc_inum для сертификатов zombie  [ https://a.yandex-team.ru/arc/commit/8416725 ]

* [rocco66](http://staff/rocco66)

 * Change "ya.make"  [ https://a.yandex-team.ru/arc/commit/8402876 ]

[zivot](http://staff/zivot) 2021-07-14 18:17:07+03:00

3.3.50
------
 * CERTOR-1879: Certificates updated__gt filter  [ https://a.yandex-team.ru/arc/commit/8402790 ]

[zivot](http://staff/zivot) 2021-07-09 16:14:20+03:00

3.3.49
------
 * CERTOR-1933: Запретить выдачу сертификатов на robot-*  [ https://a.yandex-team.ru/arc/commit/8389484 ]

[zivot](http://staff/zivot) 2021-07-08 18:01:25+03:00

3.3.48
------

* [zivot](http://staff/zivot)

 * CERTOR-1900: unique_id для узлов IDM  [ https://a.yandex-team.ru/arc/commit/8388558 ]

* [ezaitov](http://staff/ezaitov)

 * CERTOR-1933  [ https://a.yandex-team.ru/arc/commit/8385808 ]

[zivot](http://staff/zivot) 2021-07-08 15:22:55+03:00

3.3.47
------

* [zivot](http://staff/zivot)

 * CERTOR-1922: /reissue/: Возможность обновить поля pc_*                   [ https://a.yandex-team.ru/arc/commit/8354558 ]
 * CERTOR-1912: /reissue/: Отзываем сертификаты с тем же pc_inum            [ https://a.yandex-team.ru/arc/commit/8354515 ]
 * CERTOR-1916: /reissue/: Записываем в requester пользователя сертификата  [ https://a.yandex-team.ru/arc/commit/8354387 ]

* [shadchin](http://staff/shadchin)

 * IGNIETFERRO-1154 Rename contrib/python/zero_downtime_migrations to contrib/python/zero-downtime-migrations  [ https://a.yandex-team.ru/arc/commit/8344699 ]

[zivot](http://staff/zivot) 2021-06-30 17:12:05+03:00

3.3.46
------
 * CERTOR-1917: Роль "HelpDesk для внешних"  [ https://a.yandex-team.ru/arc/commit/8328614 ]

[zivot](http://staff/zivot) 2021-06-24 16:26:01+03:00

3.3.45
------

* [zivot](http://staff/zivot)

 * CERTOR-1876: Запретить выпуск PDAS без активного @ld.yandex.ru  [ https://a.yandex-team.ru/arc/commit/8324278 ]

* [squirrel](http://staff/squirrel)

 * HDRFS-822329 Change "expire-linuxoids.html"  [ https://a.yandex-team.ru/arc/commit/8316754 ]

[zivot](http://staff/zivot) 2021-06-23 13:59:04+03:00

3.3.44
------
 * CERTOR-1909: Выгружать в NOC все сертификаты (+без тегов)  [ https://a.yandex-team.ru/arc/commit/8273275 ]

[zivot](http://staff/zivot) 2021-06-17 15:20:33+03:00

3.3.43
------
 * CERTOR-1907: Снять проверку пермишена oid с /reissue/  [ https://a.yandex-team.ru/arc/commit/8248534 ]
 * Change ".devexp.json"                                  [ https://a.yandex-team.ru/arc/commit/8246923 ]

[zivot](http://staff/zivot) 2021-06-08 17:52:52+03:00

3.3.42
------
 * CERTOR-1881: Пермишен на сертификаты для зомби Маркета  [ https://a.yandex-team.ru/arc/commit/8201571 ]

[zivot](http://staff/zivot) 2021-05-26 20:27:00+03:00

3.3.41
------
 * Bump due releaser/arcanum problems DEVTOOLSSUPPORT-8604

[zivot](http://staff/zivot) 2021-05-25 17:40:15+03:00

3.3.40
------
 * CERTOR-1829: Новый тип фильтра по владельцам ролей в IDM  [ https://a.yandex-team.ru/arc/commit/8195449 ]

[zivot](http://staff/zivot) 2021-05-25 12:01:16+03:00

3.3.39
------
 * Revert "CERTOR-1829: Новый тип фильтра как система в IDM"

This reverts commit bc12ae95b8a6ef6e83f3fcf888877a544e66549b, reversing
changes made to 652bd7607d8d8136082394fbed3182b427495734.  [ https://a.yandex-team.ru/arc/commit/8193718 ]

[dmitrypro](http://staff/dmitrypro) 2021-05-24 18:17:44+03:00

3.3.38
------
CERTOR-1894: Min length of pc_serial_number in imdm certs 

[dmitrypro](http://staff/dmitrypro) 2021-05-24 16:43:13+03:00

3.3.37
------

* [zivot](http://staff/zivot)

 * CERTOR-1829: Новый тип фильтра как система в IDM  [ https://a.yandex-team.ru/arc/commit/8185501 ]

* [exprmntr](http://staff/exprmntr)

 * DEVTOOLS-7781 - remove NO_LINT()

DEVTOOLS-7781  [ https://a.yandex-team.ru/arc/commit/8097952 ]

[zivot](http://staff/zivot) 2021-05-20 21:26:45+03:00

3.3.36
------
 * CERTOR-1816: Шаблон для win_pc_shared  [ https://a.yandex-team.ru/arc/commit/8080200 ]

[dmitrypro](http://staff/dmitrypro) 2021-04-15 18:07:50+03:00

3.3.35
------
 * CERTOR-1874: import CertificateType  [ https://a.yandex-team.ru/arc/commit/8078501 ]

[zivot](http://staff/zivot) 2021-04-15 11:59:50+03:00

3.3.34
------
 * CERTOR-1874: Оптимизация get_expiring_certificates  [ https://a.yandex-team.ru/arc_vcs/commit/eec5c6724c061f924e381328d438e0c0d50b03f4 ]

[zivot](http://staff/zivot) 2021-04-14 21:16:47+03:00

3.3.33
------
 * CERTOR-1862: Принимаем idna хосты  [ https://a.yandex-team.ru/arc/commit/8043660 ]

[zivot](http://staff/zivot) 2021-04-02 12:09:49+03:00

3.3.32
------
 * CERTOR-1863: Не отзывается заявка certum  [ https://a.yandex-team.ru/arc/commit/8035978 ]

[zivot](http://staff/zivot) 2021-03-31 11:15:47+03:00

3.3.31
------
 * CERTOR-1834: принимаем поле с тикетом fix  [ https://a.yandex-team.ru/arc/commit/8034680 ]

[dmitrypro](http://staff/dmitrypro) 2021-03-30 19:53:58+03:00

3.3.30
------
 * CERTOR-1834: add helpdesk ticket field  [ https://a.yandex-team.ru/arc/commit/8032792 ]

[dmitrypro](http://staff/dmitrypro) 2021-03-30 13:22:35+03:00

3.3.29
------
 * CERTOR-1843: conn timeout fix  [ https://a.yandex-team.ru/arc/commit/8028575 ]

[dmitrypro](http://staff/dmitrypro) 2021-03-29 11:22:34+03:00

3.3.28
------
 * CERTOR-1860: sync_svc_tags в meta-таску sync_tags  [ https://a.yandex-team.ru/arc/commit/7995501 ]

[zivot](http://staff/zivot) 2021-03-25 18:44:59+03:00

3.3.27
------
 * CERTOR-1851: Отфильтровывать TLD из валидации  [ https://a.yandex-team.ru/arc/commit/7982644 ]

[zivot](http://staff/zivot) 2021-03-22 17:10:18+03:00

3.3.26
------
 * CERTOR-1815: Прописать YAUTH_MECHANISMS  [ https://a.yandex-team.ru/arc/commit/7922183 ]

[zivot](http://staff/zivot) 2021-03-05 02:45:00+03:00

3.3.25
------
 * CERTOR-1813: reversion revert, get username by distinguishedName  [ https://a.yandex-team.ru/arc/commit/7822338 ]

[zivot](http://staff/zivot) 2021-02-02 13:56:09+03:00

3.3.24
------
 * CERTOR-1813: revert  [ https://a.yandex-team.ru/arc_vcs/commit/95c83aa32c37a3206dc9a0ae2712874c45624c5f ]

[zivot](http://staff/zivot) 2021-01-28 17:48:07+03:00

3.3.23
------
 * CERTOR-1813: tests fix  [ https://a.yandex-team.ru/arc_vcs/commit/043de1d6f045f60b27176118d16835c35288d2f6 ]

[zivot](http://staff/zivot) 2021-01-28 11:03:10+03:00

3.3.22
------

* [idtv](http://staff/idtv)

 * CERTOR-1813: Fix `common_name` property  [ https://a.yandex-team.ru/arc/commit/7778947 ]

[zivot](http://staff/zivot) 2021-01-25 20:45:39+03:00

3.3.21
------

* [idtv](http://staff/idtv)

 * CERTOR-1785: Сделать лимит 10 сертификатов ninja для зомбиков [ https://a.yandex-team.ru/arc/commit/7778849 ]

[zivot](http://staff/zivot) 2021-01-25 19:49:22+03:00

3.3.20
------

* [idtv](http://staff/idtv)

 * CERTOR-1813: Check canonical name from CSR in LDAP (instead of requesting user name)  [ https://a.yandex-team.ru/arc/commit/7771869 ]

[zivot](http://staff/zivot) 2021-01-22 10:50:33+03:00

3.3.19
------

* [idtv](http://staff/idtv)

 * CERTOR-1690: Fix wrong boolean value in api for `notify_on_expiration` flag
   Remove `notify_on_expiration` from frontend,  fix tests  [ https://a.yandex-team.ru/arc/commit/7767238 ]

[zivot](http://staff/zivot) 2021-01-20 20:08:25+03:00

3.3.18
------

* [idtv](http://staff/idtv)

 * CERTOR-1690: Add `notify_on_expiration` flag to Certificate  [ https://a.yandex-team.ru/arc/commit/7750883 ]

[zivot](http://staff/zivot) 2021-01-19 00:42:02+03:00

3.3.17
------
 * CERTOR-1807: CN=login для внешних  [ https://a.yandex-team.ru/arc_vcs/commit/f529bda2782ee2b5b2fe7800473bad6a6db325a8 ]

[zivot](http://staff/zivot) 2021-01-12 12:50:00+03:00

3.3.16
------
 * CERTOR-1807: Сертификатор не выдаёт 1C сертификат для ForeignUsers  [ https://a.yandex-team.ru/arc/commit/7743110 ]

[zivot](http://staff/zivot) 2021-01-12 11:30:10+03:00

3.3.15
------
 * CERTOR-1793: crt sync_tags не удаляет теги, выданные по типу сертификата  [ https://a.yandex-team.ru/arc/commit/7657299 ]
 * CERTOR-1794: Выпилить raven                                               [ https://a.yandex-team.ru/arc/commit/7654263 ]

[zivot](http://staff/zivot) 2020-12-09 18:31:32+03:00

3.3.14
------
 * CERTOR-1789: Выпилить sentry  [ https://a.yandex-team.ru/arc/commit/7635931 ]

[zivot](http://staff/zivot) 2020-12-01 22:30:29+03:00

3.3.13
------
 * CERTOR-1723 serial_number lookup upper  [ https://a.yandex-team.ru/arc/commit/7616967 ]

[zivot](http://staff/zivot) 2020-11-24 18:48:44+03:00

3.3.12
------

* [mvel](http://staff/mvel)

 * [crt] Convert certificate serial to uppercase to fix case-sensitive match noticed in CERTOR-1723

* [zivot](http://staff/zivot)

 * CERTOR-1723: serial upper case query test added  [ https://a.yandex-team.ru/arc/commit/7611412 ]


[zivot](http://staff/zivot) 2020-11-23 03:17:23+03:00

3.3.11
------
 * CERTOR-1780: Переименование чекбокса iOS Exchange  [ https://a.yandex-team.ru/arc/commit/7571527 ]

[zivot](http://staff/zivot) 2020-11-10 13:32:23+03:00

3.3.10
------
 * CERTOR-1778: Уменьшить cooldown ninja до 2 минут  [ https://a.yandex-team.ru/arc/commit/7568232 ]

[zivot](http://staff/zivot) 2020-11-09 13:40:09+03:00

3.3.9
-----
 * CERTOR-1775: drf fix  [ https://a.yandex-team.ru/arc/commit/7547828 ]

[shigarus](http://staff/shigarus) 2020-11-05 15:57:24+03:00

3.3.8
-----
 * CERTOR-1525: фикс галки "Выбрать все"  [ https://a.yandex-team.ru/arc/commit/7540681 ]

[zivot](http://staff/zivot) 2020-11-02 17:27:53+03:00

3.3.7
-----
 * CERTOR-1616: Сертификаты для временных ноутбуков  [ https://a.yandex-team.ru/arc/commit/7535168 ]

[zivot](http://staff/zivot) 2020-10-30 17:17:56+03:00

3.3.6
-----
 * CERTOR-1525: Фикс ограничения при отзыве (ninja)  [ https://a.yandex-team.ru/arc/commit/7522864 ]
 * CERTOR-1525: Сертификаты для зомби на ninja       [ https://a.yandex-team.ru/arc/commit/7520616 ]

[zivot](http://staff/zivot) 2020-10-27 23:42:33+03:00

3.3.5
-----
 * CERTOR-1525: revert ninja  [ https://a.yandex-team.ru/arc/commit/7520355 ]

[zivot](http://staff/zivot) 2020-10-27 11:59:12+03:00

3.3.4
-----
 * CERTOR-1742: Фикс проверки desired_ttl_days  [ https://a.yandex-team.ru/arc/commit/7519230 ]

[zivot](http://staff/zivot) 2020-10-26 20:55:08+03:00

3.3.3
-----
 * CERTOR-1525: фикс ограничения в 5 минут (ninja)  [ https://a.yandex-team.ru/arc/commit/7518099 ]

[zivot](http://staff/zivot) 2020-10-26 14:57:59+03:00

3.3.2
-----
 * CERTOR-1742: Краткосрочные сертификаты host в отдельный шаблон  [ https://a.yandex-team.ru/arc/commit/7490799 ]

[zivot](http://staff/zivot) 2020-10-23 19:04:38+03:00

3.3.1
-----
 * CERTOR-1525: Галка "Выбрать все" на ninja  [ https://a.yandex-team.ru/arc/commit/7487819 ]

[zivot](http://staff/zivot) 2020-10-22 20:38:05+03:00

3.3.0
-----
 * CERTOR-1525 возвращаем функциональность про ninja

PR from branch users/zivot/ninja_revert

ninja revert

Revert "PR from branch users/ndtretyak/feature/CERTOR-1525"
This reverts commit 4a6b9a7b89d710c5346c7c737b45d4bf3248e0cd, reversing
changes made to 2755b00eb601a3c11c99b3d8ab3483e3412f8bfd.

Revert "Change ninja.html"
This reverts commit d0f46270d8bb71b3743db55cbf751296a81b5d70.

Revert "CERTOR-1525: одинаковый порядок пользователей"
This reverts commit 248d3eae6d5e01f169d1cb95ffb81a3ac14cf934, reversing
changes made to 26eb97147c2f4a4c7d98a5c220acaab21b974959.

<!-- DEVEXP BEGIN -->
\****
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![chirkinvf](https://codereview.common-int.yandex-team.ru/badges/chirkinvf-...-yellow.svg)](https://staff.yandex-team.ru/chirkinvf) [![terrmit](https://codereview.common-int.yandex-team.ru/badges/terrmit-...-yellow.svg)](https://staff.yandex-team.ru/terrmit)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/7479650 ]

[tmalikova](http://staff/tmalikova) 2020-10-20 13:33:10+03:00

3.2.3
-----
 * CERTOR-1693 не ридонли common_name  [ https://a.yandex-team.ru/arc/commit/7469463 ]

[tmalikova](http://staff/tmalikova) 2020-10-15 18:15:19+03:00

3.2.2
-----
 * CERTOR-1669 обработка исключений от сертума  [ https://a.yandex-team.ru/arc/commit/7458950 ]

[tmalikova](http://staff/tmalikova) 2020-10-13 12:33:46+03:00

3.2.1
-----
 * Revert "CERTOR-1664 фикс валидации облачных сертов"

This reverts commit 24c0e6a9df48401a4bfb4be1ca11b55e9d479602, reversing
changes made to 300552ae21810c5da391878fdbc4f5f494ab4d0b.

Revert "CERTOR-1664 фикс валидации облачных сертов"
This reverts commit 24c0e6a9df48401a4bfb4be1ca11b55e9d479602, reversing
changes made to 300552ae21810c5da391878fdbc4f5f494ab4d0b.  [ https://a.yandex-team.ru/arc/commit/7456032 ]

[tmalikova](http://staff/tmalikova) 2020-10-12 14:24:11+03:00

3.2.0
------
 * CERTOR-1664 фикс валидации облачных сертов  [ https://a.yandex-team.ru/arc/commit/7455766 ]

[tmalikova](http://staff/tmalikova) 2020-10-12 12:57:59+03:00

3.1.23
------
 * CERTOR-1758 фикс \r\n в сертификате  [ https://a.yandex-team.ru/arc/commit/7440573 ]

[tmalikova](http://staff/tmalikova) 2020-10-06 14:22:27+03:00

3.1.22
------
 * CERTOR-1635: TPM Smartcard Certificates  [ https://a.yandex-team.ru/arc/commit/7436648 ]

[zivot](http://staff/zivot) 2020-10-05 12:27:05+03:00

3.1.21
------
 * CERTOR-1646: tvm for idm  [ https://a.yandex-team.ru/arc/commit/7422412 ]

[shigarus](http://staff/shigarus) 2020-10-02 15:41:47+03:00

3.1.20
------
 * CERTOR-1745: Выпилил костыль yandex.ua  [ https://a.yandex-team.ru/arc_vcs/commit/622c47d7c3e8a6f17d9a66ce9850a028194dc18f ]

[zivot](http://staff/zivot) 2020-10-01 22:09:59+03:00

3.1.19
------
 * CERTOR-1745: code expire_at fix  [ https://a.yandex-team.ru/arc/commit/7419126 ]

[zivot](http://staff/zivot) 2020-10-01 16:28:07+03:00

3.1.18
------
 * CERTOR-1745: Параллельная валидация кодов  [ https://a.yandex-team.ru/arc/commit/7418186 ]

[zivot](http://staff/zivot) 2020-10-01 13:02:25+03:00

3.1.17
------
 * CERTOR-1750: fix com.ua  [ https://a.yandex-team.ru/arc/commit/7417016 ]

[shigarus](http://staff/shigarus) 2020-10-01 00:35:53+03:00

3.1.16
------
 * CERTOR-1749: fix ua  [ https://a.yandex-team.ru/arc/commit/7416883 ]

[shigarus](http://staff/shigarus) 2020-09-30 23:21:30+03:00

3.1.15
------
 * CERTOR-1724: fix verification hosts choose  [ https://a.yandex-team.ru/arc/commit/7416753 ]

[shigarus](http://staff/shigarus) 2020-09-30 22:18:33+03:00

3.1.14
------
 * CERTOR-1724: host-to-approve fix  [ https://a.yandex-team.ru/arc/commit/7412972 ]

[zivot](http://staff/zivot) 2020-09-30 00:14:33+03:00

3.1.13
------
 * CERTOR-1724: Убрал ненужные поля  [ https://a.yandex-team.ru/arc_vcs/commit/22f5b4bb45610119553fa3ad99aa0156a3ade96a ]

[zivot](http://staff/zivot) 2020-09-29 21:10:28+03:00

3.1.12
------
 * CERTOR-1635: TPM revert 2  [ https://a.yandex-team.ru/arc/commit/7412467 ]

[zivot](http://staff/zivot) 2020-09-29 20:18:33+03:00

3.1.11
------

* [zivot](http://staff/zivot)

 * CERTOR-1724: misstype fix                             [ https://a.yandex-team.ru/arc/commit/7411916 ]
 * CERTOR-1635: Изменение валидации TPM Smartcard Logon  [ https://a.yandex-team.ru/arc/commit/7409884 ]
 * CERTOR-1635: revert revert tpm certificates           [ https://a.yandex-team.ru/arc/commit/7408829 ]

* [tmalikova](http://staff/tmalikova)

 * CERTOR-1724 новая модель для кодов валидации  [ https://a.yandex-team.ru/arc/commit/7411819 ]

[zivot](http://staff/zivot) 2020-09-29 18:16:14+03:00

3.1.10
------
 * CERTOR-1741: fix certum call  [ https://a.yandex-team.ru/arc/commit/7407631 ]

[shigarus](http://staff/shigarus) 2020-09-28 16:53:03+03:00

3.1.9
-----
 * CERTOR-1635: Сертификаты TPM Smartcard Logon (1C)  [ https://a.yandex-team.ru/arc/commit/7356829 ]

[zivot](http://staff/zivot) 2020-09-22 13:16:10+03:00

3.1.8
-----
 * CERTOR-1717 заменяем verifyDomain на новый performSanVerification  [ https://a.yandex-team.ru/arc/commit/7306967 ]

[tmalikova](http://staff/tmalikova) 2020-09-07 15:17:22+03:00

3.1.7
-----
 * CERTOR-1517: is_delete key fix  [ https://a.yandex-team.ru/arc/commit/7302527 ]

[zivot](http://staff/zivot) 2020-09-04 19:36:57+03:00

3.1.6
-----
 * CERTOR-1715: Не получаем удаленные группы из staff-api  [ https://a.yandex-team.ru/arc/commit/7302359 ]

[zivot](http://staff/zivot) 2020-09-04 19:02:01+03:00

3.1.5
-----
 * CERTOR-1651 обновление версии abc                                [ https://a.yandex-team.ru/arc/commit/7285648 ]
 * CERTOR-1665 замена groups на groupmembership при походе в staff  [ https://a.yandex-team.ru/arc/commit/7285646 ]

[tmalikova](http://staff/tmalikova) 2020-09-03 16:08:32+03:00

3.1.4
-----
 * CERTOR-1551 ограничение на год для хостовых сертов и полгода для сертумовских  [ https://a.yandex-team.ru/arc/commit/7264643 ]

[tmalikova](http://staff/tmalikova) 2020-08-28 17:13:55+03:00

3.1.3
-----
 * CERTOR-1681: Задублированные письма об истечении срока  [ https://a.yandex-team.ru/arc/commit/7217900 ]

[zivot](http://staff/zivot) 2020-08-13 13:55:45+03:00

3.1.2
-----
 * CERTOR-1647: Отдаем код на валидацию сразу  [ https://a.yandex-team.ru/arc/commit/7215375 ]

[zivot](http://staff/zivot) 2020-08-12 18:18:30+03:00

3.1.1
-----
 * CERTOR-1653 фикс выписывания ecc сертификатов  [ https://a.yandex-team.ru/arc/commit/7214614 ]

[tmalikova](http://staff/tmalikova) 2020-08-12 15:45:29+03:00

3.1.0
------

* [tmalikova](http://staff/tmalikova)

 * CERTOR-1653 changes for certum api 4.10.1        [ https://a.yandex-team.ru/arc/commit/7211702 ]
 * CERTOR-1653 подстраиваемся под новое api certum  [ https://a.yandex-team.ru/arc/commit/7152554 ]

* [zivot](http://staff/zivot)

 * CERTOR-1675: ro.admin.y-t.ru connect timeout     [ https://a.yandex-team.ru/arc/commit/7210592 ]
 * CERTOR-1673: Исправить экшн private_key_deleted  [ https://a.yandex-team.ru/arc/commit/7184807 ]

[tmalikova](http://staff/tmalikova) 2020-08-11 18:26:22+03:00

3.0.47
------
 * CERTOR-1489: resolver в nginx с небольшим временем кеширования  [ https://a.yandex-team.ru/arc/commit/7135441 ]

[zivot](http://staff/zivot) 2020-07-21 21:38:30+03:00

3.0.46
------
 * CERTOR-1647 команда для поставновки очередных кодов на валидацию  [ https://a.yandex-team.ru/arc/commit/7131553 ]

[tmalikova](http://staff/tmalikova) 2020-07-20 16:55:55+03:00

3.0.45
------
 * CERTOR-1609: return CA errors to user  [ https://a.yandex-team.ru/arc/commit/7104491 ]

[shigarus](http://staff/shigarus) 2020-07-14 11:18:51+03:00

3.0.44
------
 * CERTOR-1648: Разрешить хостовые (rtc) сертификаты для хостов в домене core-c.yandex.net  [ https://a.yandex-team.ru/arc/commit/7090664 ]

[tmalikova](http://staff/tmalikova) 2020-07-08 17:44:07+03:00

3.0.43
------
 * CERTOR-1626: Замораживать linux-pc не сразу, уточнить о заморозке в уводомлении  [ https://a.yandex-team.ru/arc/commit/6972965 ]
 * CERTOR-1624: Попробовать собираться в sandbox                                    [ https://a.yandex-team.ru/arc/commit/6914452 ]

[zivot](http://staff/zivot) 2020-06-15 13:24:21+03:00

3.0.42
------
 * CERTOR-1623: FQDN  [ https://a.yandex-team.ru/arc/commit/6909113 ]

[zivot](http://staff/zivot) 2020-06-05 21:44:26+03:00

3.0.41
------
 * PR from branch users/shigarus/certor-1549__need_aprrove_has_no_end_date  [ https://a.yandex-team.ru/arc/commit/6881940 ]

[shigarus](http://staff/shigarus) 2020-05-28 20:32:19+03:00

3.0.40
------
 * CERTOR-1549: need_approve has no end date  [ https://a.yandex-team.ru/arc/commit/6881608 ]

[shigarus](http://staff/shigarus) 2020-05-28 19:04:54+03:00

3.0.39
------
 * CERTOR-1549: dont send exceed emails  [ https://a.yandex-team.ru/arc/commit/6872088 ]

[shigarus](http://staff/shigarus) 2020-05-26 13:50:34+03:00

3.0.38
------
 * CERTOR-1597: revert  [ https://a.yandex-team.ru/arc/commit/6851955 ]

[shigarus](http://staff/shigarus) 2020-05-21 15:19:41+03:00

3.0.37
------
 * CERTOR-1603: Флапает cvs_upload  [ https://a.yandex-team.ru/arc/commit/6842981 ]
 * Change README.md                 [ https://a.yandex-team.ru/arc/commit/6842866 ]

[zivot](http://staff/zivot) 2020-05-19 13:04:35+03:00

3.0.36
------
 * CERTOR-1599: Падаем при попытке записать ошибку от CA  [ https://a.yandex-team.ru/arc/commit/6791546 ]

[zivot](http://staff/zivot) 2020-05-15 22:39:06+03:00

3.0.35
------

* [shigarus](http://staff/shigarus)

 * CERTOR-1597: add walle as host cert  [ https://a.yandex-team.ru/arc/commit/6782596 ]

* [zivot](http://staff/zivot)

 * Change README.md  [ https://a.yandex-team.ru/arc/commit/6779085 ]

[shigarus](http://staff/shigarus) 2020-05-14 18:08:12+03:00

3.0.34
------
 * CERTOR-1593: Форма запроса сертификата через CSR поломалась

[zivot](http://staff/zivot) 2020-05-07 12:35:59+03:00

3.0.33
------
 * Фикс валидации  [ https://a.yandex-team.ru/arc/commit/6746934 ]

[ndtretyak](http://staff/ndtretyak) 2020-04-28 11:15:28+03:00

3.0.32
------

 * CERTOR-1576: str  [ https://a.yandex-team.ru/arc/commit/6690474 ]

[zivot](http://staff/zivot) 2020-04-24 01:04:49+03:00

3.0.31
------
 * CERTOR-1434: [MDB] сделать аналог сертификатов yc-server для внутреннего CA

[zivot](http://staff/zivot) 2020-04-22 20:38:27+03:00

3.0.30
------

* [ndtretyak](http://staff/ndtretyak)

 * Python3 fix  [ https://a.yandex-team.ru/arc/commit/6583075 ]

* [zivot](http://staff/zivot)

 * Change .devexp.json

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![chirkinvf](https://codereview.common-int.yandex-team.ru/badges/chirkinvf-...-yellow.svg)](https://staff.yandex-team.ru/chirkinvf) [![kdunaev](https://codereview.common-int.yandex-team.ru/badges/kdunaev-ok-green.svg)](https://staff.yandex-team.ru/kdunaev)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6583070 ]

[ndtretyak](http://staff/ndtretyak) 2020-04-06 12:19:47+03:00

3.0.29
------
 * Фикс сборки python3

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![zivot](https://codereview.common-int.yandex-team.ru/badges/zivot-ok-green.svg)](https://staff.yandex-team.ru/zivot) [![neofelis](https://codereview.common-int.yandex-team.ru/badges/neofelis-...-yellow.svg)](https://staff.yandex-team.ru/neofelis)
<!-- DEVEXP END -->                                                                                                                 [ https://a.yandex-team.ru/arc/commit/6577347 ]
 * PR from branch users/ndtretyak/python3

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![poegva](https://codereview.common-int.yandex-team.ru/badges/poegva-...-yellow.svg)](https://staff.yandex-team.ru/poegva) [![d1568](https://codereview.common-int.yandex-team.ru/badges/d1568-ok-green.svg)](https://staff.yandex-team.ru/d1568)
<!-- DEVEXP END -->                                                                                                    [ https://a.yandex-team.ru/arc/commit/6576197 ]
 * Фикс тестов

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) [![uruz](https://codereview.common-int.yandex-team.ru/badges/uruz-ok-green.svg)](https://staff.yandex-team.ru/uruz) [![swetlanka](https://codereview.common-int.yandex-team.ru/badges/swetlanka-...-yellow.svg)](https://staff.yandex-team.ru/swetlanka) [![zivot](https://codereview.common-int.yandex-team.ru/badges/zivot-ok-green.svg)](https://staff.yandex-team.ru/zivot)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6557629 ]

[ndtretyak](http://staff/ndtretyak) 2020-04-03 15:09:52+03:00

3.0.28
------
 * CERTOR-1548: Empty certificate fix

[zivot](http://staff/zivot) 2020-03-31 22:04:10+03:00

3.0.27
------
 * PR from branch users/zivot/ninja_revert

ninja revert

 * .devexp.json (Ревьюшница)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  [ https://a.yandex-team.ru/arc/commit/6542010 ]
 * CERTOR-1548: Выводить информацию о тегах, записанных в сертификат                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          [ https://a.yandex-team.ru/arc/commit/6540910 ]

[zivot](http://staff/zivot) 2020-03-30 20:13:35+03:00

3.0.26
------

* [ndtretyak](http://staff/ndtretyak)

 * CERTOR-1525: одинаковый порядок пользователей  [ https://a.yandex-team.ru/arc/commit/6523688 ]

* [zovcharov](http://staff/zovcharov)

 * Change ninja.html  [ https://a.yandex-team.ru/arc/commit/6516285 ]

[ndtretyak](http://staff/ndtretyak) 2020-03-24 13:18:00+03:00

3.0.25
------
 * CERTOR-1319: убирать пустые значения из запроса                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              [ https://a.yandex-team.ru/arc/commit/6506565 ]
 * PR from branch users/ndtretyak/feature/CERTOR-1525

CERTOR-1525: запрос сертификата для роботоа

Откат фичи про запрос ninja-сертификатов
Revert "PR from branch users/v-sopov/feature/CERTOR-1477"
This reverts commit 3a3605d5e96af948adfb50a42d83d55c310f8675, reversing
changes made to a06edeb87b6e78b7b7e41e178341773d43592aea.
CERTOR-1477: теперь отзываются только выбранные сертификаты, лимит можно выставлять через админку
REVIEW: 1051655
CERTOR-1477: убрано упоминание повышения лимита, уменьшены чекбоксы в шаблоне ninja
REVIEW: 1055495
REVIEW: 1074845  [ https://a.yandex-team.ru/arc/commit/6505877 ]

[ndtretyak](http://staff/ndtretyak) 2020-03-19 14:52:26+03:00

3.0.24
------
 * CERTOR-1319: разрешить пустой common_name  [ https://a.yandex-team.ru/arc/commit/6495808 ]

[ndtretyak](http://staff/ndtretyak) 2020-03-17 10:09:26+03:00

3.0.23
------
 * CERTOR-1565: CourtecyVPN  [ https://a.yandex-team.ru/arc/commit/6490626 ]

[ndtretyak](http://staff/ndtretyak) 2020-03-16 15:03:57+03:00

3.0.22
------

* [ndtretyak](http://staff/ndtretyak)

 * Фикс миграции                                                                                                                           [ https://a.yandex-team.ru/arc/commit/6474168 ]
 * PR from branch users/ndtretyak/feature/CERTOR-1369

ca_name

CERTOR-1369: Сделать мониторинг на количество Certum-сертификатов в ERROR  [ https://a.yandex-team.ru/arc/commit/6473231 ]

* [zivot](http://staff/zivot)

 * CERTOR-1560: Привязывать сертификаты hypercube к пользователям  [ https://a.yandex-team.ru/arc/commit/6473004 ]

[ndtretyak](http://staff/ndtretyak) 2020-03-11 16:55:48+03:00

3.0.21
------

* [danielzhe](http://staff/danielzhe)

 * SUBBOTNIK-3370 Move yenv, python-blackboxer to arcadia common library  [ https://a.yandex-team.ru/arc/commit/6394727 ]

* [zivot](http://staff/zivot)

 * CERTOR-1552: Не выгружать в NOC cvs сертификаты уволенных пользователей  [ https://a.yandex-team.ru/arc/commit/6453758 ]
 * CERTOR-1553: Сделать сертификаты гиперкуба тегируемыми                   [ https://a.yandex-team.ru/arc/commit/6453743 ]

* [ezaitov](http://staff/ezaitov)

 * Change ssl-certificate-was-issued.html  [ https://a.yandex-team.ru/arc/commit/6437978 ]

[zivot](http://staff/zivot) 2020-03-04 12:59:02+03:00

3.0.20
------
 * Hypercube 3d permission added  [ https://a.yandex-team.ru/arc/commit/6379755 ]

[zivot](http://staff/zivot) 2020-02-17 14:38:17+03:00

3.0.19
------

  * CERTOR-1449: Не работает админка для constance

[zivot](http://staff/zivot) 2020-02-17 12:22:38+03:00

3.0.18
------
 * CERTOR-1538: новая роль для Гиперкуба  [ https://a.yandex-team.ru/arc/commit/6374159 ]

[ndtretyak](http://staff/ndtretyak) 2020-02-14 18:15:57+03:00

3.0.17
------

 * Фикс подсчета изменений

[zivot](http://staff/zivot) 2020-02-14 17:34:55+03:00

3.0.16
------

 * Расширил описание тикета

[zivot](http://staff/zivot) 2020-02-14 14:53:44+03:00

3.0.15
------

 * CERTOR-1524: Синхронизировать ответственность за роботов

[zivot](http://staff/zivot) 2020-02-14 12:45:36+03:00

3.0.14
------
 * CERTOR-689: Поле is_broken в админке  [ https://a.yandex-team.ru/arc/commit/6369988 ]

[zivot](http://staff/zivot) 2020-02-13 16:55:16+03:00

3.0.13
------

 * CERTOR-689: Фикс менеджмент команды, фикс сообщения

[zivot](http://staff/zivot) 2020-02-13 14:38:58+03:00

3.0.12
------

 * CERTOR-1532: Сделать таски CRT celery-тасками  [ https://a.yandex-team.ru/arc/commit/6365067 ]
 * CERTOR-689: Научиться ломать фильтры           [ https://a.yandex-team.ru/arc/commit/6356898 ]

[zivot](http://staff/zivot) 2020-02-12 21:17:49+03:00

3.0.11
------
 * Change permissions.py  [ https://a.yandex-team.ru/arc/commit/6321062 ]

[ndtretyak](http://staff/ndtretyak) 2020-02-04 12:17:20+03:00

3.0.10
------
 * CERTOR-1526: сертификаты для постаматов  [ https://a.yandex-team.ru/arc/commit/6316624 ]

[ndtretyak](http://staff/ndtretyak) 2020-02-04 10:36:27+03:00

3.0.9
-----

* [sidorovaa](http://staff/sidorovaa)

 * Remove duplicate PY_SRCS/TEST_SRCS (DEVTOOLS-5213)  [ https://a.yandex-team.ru/arc/commit/6304974 ]

* [ndtretyak](http://staff/ndtretyak)

 * Правка импортов  [ https://a.yandex-team.ru/arc/commit/6309509 ]

* [v-sopov](http://staff/v-sopov)

 * Обработка отсутствия юзера у сертификата при проверке прав  [ https://a.yandex-team.ru/arc/commit/6309176 ]

[zivot](http://staff/zivot) 2020-01-31 18:45:42+03:00

3.0.8
-----
 * tag_query optimization  [ https://a.yandex-team.ru/arc/commit/6304680 ]

[zivot](http://staff/zivot) 2020-01-30 12:48:13+03:00

3.0.7
-----
 * CERTOR-1517: Фикс синхронизации тегов  [ https://a.yandex-team.ru/arc/commit/6263317 ]

[zivot](http://staff/zivot) 2020-01-28 15:00:55+03:00

3.0.6
-----
 * CERTOR-1517: Возможность вешать фильтры на все типы сертификатов  [ https://a.yandex-team.ru/arc/commit/6250955 ]

[zivot](http://staff/zivot) 2020-01-24 18:08:35+03:00

3.0.5
-----
 * CERTOR-1519: Поправить отображение abc_service в админке approverequest  [ https://a.yandex-team.ru/arc/commit/6241709 ]

[zivot](http://staff/zivot) 2020-01-22 19:03:52+03:00

3.0.4
-----

* [ezaitov](http://staff/ezaitov)

 * Add abc_service to certrequest admin  [ https://a.yandex-team.ru/arc/commit/6238319 ]

[zivot](http://staff/zivot) 2020-01-21 19:55:40+03:00

3.0.3
-----

* [ndtretyak](http://staff/ndtretyak)

 * CERTOR-929: ускорить команду  [ https://a.yandex-team.ru/arc/commit/6227827 ]

* [zivot](http://staff/zivot)

 * CERTOR-1513: Старт базы в тестах не укладывается в таймаут  [ https://a.yandex-team.ru/arc/commit/6227020 ]

[ndtretyak](http://staff/ndtretyak) 2020-01-20 14:31:06+03:00

3.0.2
-----
 * CERTOR-1482: Фикс дефолтного тега  [ https://a.yandex-team.ru/arc/commit/6223854 ]

[zivot](http://staff/zivot) 2020-01-17 19:39:13+03:00

3.0.1
-----

* [zivot](http://staff/zivot)

 * CERTOR-1504: Добавить проверку прав на выписывание CSR с тегами  [ https://a.yandex-team.ru/arc/commit/6222882 ]

* [ndtretyak](http://staff/ndtretyak)

 * Конфиг релизера  [ https://a.yandex-team.ru/arc/commit/6218762 ]

[zivot](http://staff/zivot) 2020-01-17 16:22:02+03:00

3.0.0
------

* [ndtretyak](http://staff/ndtretyak)

 * CERTOR-929: сохранять отозвавшего серт                                                           [ https://a.yandex-team.ru/arc/commit/6218496 ]
 * CERTOR-1491: выбирать меньше из staff-api                                                        [ https://a.yandex-team.ru/arc/commit/6040203 ]
 * Убрать трешолд из синка групп                                                                    [ https://a.yandex-team.ru/arc/commit/5986386 ]
 * Releasing version 2.6.15                                                                         [ https://a.yandex-team.ru/arc/commit/5985516 ]
 * CERTOR-1479: Разрешить создание сертификатов для cloud-testing.yandex.net доменов Яндекс.Облака  [ https://a.yandex-team.ru/arc/commit/5985441 ]
 * Releasing version 2.6.14                                                                         [ https://a.yandex-team.ru/arc/commit/5984656 ]
 * PR from branch users/ndtretyak/CERTOR-1473                                                       [ https://a.yandex-team.ru/arc/commit/5984568 ]
 * Change pkg.json                                                                                  [ https://a.yandex-team.ru/arc/commit/5824238 ]
 * Change 090-crt.conf                                                                              [ https://a.yandex-team.ru/arc/commit/5824231 ]
 * Change pkg.json                                                                                  [ https://a.yandex-team.ru/arc/commit/5818530 ]

* [zivot](http://staff/zivot)

 * tests forking                                                          [ https://a.yandex-team.ru/arc/commit/6210209 ]
 * releasing version 2.8.1                                                [ https://a.yandex-team.ru/arc/commit/6209968 ]
 * CERTOR-1482: Записываем теги в поля OID                                [ https://a.yandex-team.ru/arc/commit/6206050 ]
 * Change README.md                                                       [ https://a.yandex-team.ru/arc/commit/6130191 ]
 * Добавил описание makemigrations                                        [ https://a.yandex-team.ru/arc/commit/6046388 ]
 * releasing version 2.6.17                                               [ https://a.yandex-team.ru/arc/commit/6045238 ]
 * CERTOR-1476: Белый список доменов для InternalCA                       [ https://a.yandex-team.ru/arc/commit/6045201 ]
 * releasing version 2.6.16                                               [ https://a.yandex-team.ru/arc/commit/6040349 ]
 * Releasing CRT 2.6.11                                                   [ https://a.yandex-team.ru/arc/commit/5882464 ]
 * CERTOR-1469: Нули в пароле от сертификата                              [ https://a.yandex-team.ru/arc/commit/5882298 ]
 * CERTOR-1462: Иногда падает тест на создании каталога CRT_CVS_REPO_DIR  [ https://a.yandex-team.ru/arc/commit/5837701 ]
 * releasing version 2.6.9                                                [ https://a.yandex-team.ru/arc/commit/5828754 ]
 * CERTOR-1458: Потюнить таймаут похода в CA (connect timeout)            [ https://a.yandex-team.ru/arc/commit/5828506 ]
 * CERTOR-1459: Добавить воркеров CRT                                     [ https://a.yandex-team.ru/arc/commit/5826540 ]
 * TOOLSUP-60221: http->https                                             [ https://a.yandex-team.ru/arc/commit/5826538 ]

* [v-sopov](http://staff/v-sopov)

 * Откат фичи про запрос ninja-сертификатов

Revert "PR from branch users/v-sopov/feature/CERTOR-1477"
This reverts commit 3a3605d5e96af948adfb50a42d83d55c310f8675, reversing
changes made to a06edeb87b6e78b7b7e41e178341773d43592aea.

CERTOR-1477: теперь отзываются только выбранные сертификаты, лимит можно выставлять через админку
REVIEW: 1051655

CERTOR-1477: убрано упоминание повышения лимита, уменьшены чекбоксы в шаблоне ninja
REVIEW: 1055495  [ https://a.yandex-team.ru/arc/commit/6147850 ]
 * CERTOR-1483: в prefetch_tags возвращён distinct(), который, как оказалось, в некоторых местах всё же нужен                                                                                                                                                                                                                                                                                                                                                     [ https://a.yandex-team.ru/arc/commit/6136620 ]
 * releasing version 2.7                                                                                                                                                                                                                                                                                                                                                                                                                                          [ https://a.yandex-team.ru/arc/commit/6132103 ]
 * CERTOR-1483: динамическое управление тегами

CERTOR-1483: добавлены миграции

CERTOR-1483: добавлено редактирование тегов в API, переработано отображение тегов в API

CERTOR-1483: редактирование сертификатов и связей с тегами в админке                                                                                                                                                                                                                    [ https://a.yandex-team.ru/arc/commit/6132055 ]
 * CERTOR-1477: убрано упоминание повышения лимита, уменьшены чекбоксы в шаблоне ninja                                                                                                                                                                                                                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/6082359 ]
 * CERTOR-1477: теперь отзываются только выбранные сертификаты, лимит можно выставлять через админку                                                                                                                                                                                                                                                                                                                                                              [ https://a.yandex-team.ru/arc/commit/6052303 ]
 * Release version 2.16.18                                                                                                                                                                                                                                                                                                                                                                                                                                        [ https://a.yandex-team.ru/arc/commit/6047211 ]
 * PR from branch users/v-sopov/feature/CERTOR-1477

CERTOR-1477: тесты и небольшие правки

CERTOR-1477: ограничение на ninja-сертификаты и предложение их отзыва

CERTOR-1477: исправлен редирект на ninja

CERTOR-1477: страница ninja теперь не требует логин/пароль

CERTOR-1477: миддлварь аутентификации теперь умеет редиректить на Паспорт

CERTOR-1477: походы в ldap теперь используют логин-пароль нашего робота                                       [ https://a.yandex-team.ru/arc/commit/6047134 ]

* [aduryagin](http://staff/aduryagin)

 * CERTOR-1499 - Extend acceptable common names for botik certificates

Pull-request for branch users/aduryagin/extend-acceptable-common-names-for-botik  [ https://a.yandex-team.ru/arc/commit/6126542 ]

* [stampi](http://staff/stampi)

 * Releasing version 2.6.13                            [ https://a.yandex-team.ru/arc/commit/5984263 ]
 * CERTOR-1393 Фикс миграции                           [ https://a.yandex-team.ru/arc/commit/5984126 ]
 * Releasing version 2.6.12                            [ https://a.yandex-team.ru/arc/commit/5981554 ]
 * PR from branch users/stampi/feature/CERTOR-1393     [ https://a.yandex-team.ru/arc/commit/5981506 ]
 * Release 2.6.10                                      [ https://a.yandex-team.ru/arc/commit/5850609 ]
 * CERTOR-1450 Ускорить выгрузку сертификатов для СИБ  [ https://a.yandex-team.ru/arc/commit/5849809 ]

[ndtretyak](http://staff/ndtretyak) 2020-01-16 12:04:47+03:00

1.70.2
------

* [rudskoy](http://staff/rudskoy)

 * migrate github.yandex-team.ru/idm/yandex-crt ARCADIA-1059  [ https://a.yandex-team.ru/arc/commit/5456967 ]

* [orivej](http://staff/orivej)

 * Rename contrib/python/django-rest-framework to djangorestframework according to PyPI. CONTRIB-608 IGNIETFERRO-1154  [ https://a.yandex-team.ru/arc/commit/5644288 ]

* [shubinv](http://staff/shubinv)

 * CERTOR-1213 Изменена логика отправки писем                                                                                     [ https://a.yandex-team.ru/arc/commit/5634216 ]
 * CERTOR-1210 Изменен фильтр по умолчанию (видит не только свои сертификаты, но и всех сервисов, в которых у него соотв. скоуп)  [ https://a.yandex-team.ru/arc/commit/5558993 ]
 * CERTOR-1211 Изменены права на просмотр и редактирование                                                                        [ https://a.yandex-team.ru/arc/commit/5536374 ]

* [stupidhobbit](http://staff/stupidhobbit)

 * CERTOR-1441: Новый шаблон client-серверных сертификатов для машин и зомбиков                                                                                                                                                                                       [ https://a.yandex-team.ru/arc/commit/5786843 ]
 * Поднял версию                                                                                                                                                                                                                                                      [ https://a.yandex-team.ru/arc/commit/5783537 ]
 * PR from branch users/stupidhobbit/feature/CERTOR-1194-3                                                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/5783320 ]
 * Поднял версию                                                                                                                                                                                                                                                      [ https://a.yandex-team.ru/arc/commit/5763500 ]
 * Добавил крон                                                                                                                                                                                                                                                       [ https://a.yandex-team.ru/arc/commit/5763277 ]
 * Поднял версию                                                                                                                                                                                                                                                      [ https://a.yandex-team.ru/arc/commit/5758168 ]
 * CERTOR-1213: Добавил скоуп, которому отправляется письмо                                                                                                                                                                                                           [ https://a.yandex-team.ru/arc/commit/5757597 ]
 * CERTOR-1256: Добавил команду для удаления ключей                                                                                                                                                                                                                   [ https://a.yandex-team.ru/arc/commit/5664465 ]
 * CERTOR-1155: Поднял версию                                                                                                                                                                                                                                         [ https://a.yandex-team.ru/arc/commit/5622778 ]
 * Поменял длину ecc ключа в тестинге                                                                                                                                                                                                                                 [ https://a.yandex-team.ru/arc/commit/5622776 ]
 * WINADMINREQ-8029: Поднял версию                                                                                                                                                                                                                                    [ https://a.yandex-team.ru/arc/commit/5603775 ]
 * Поднял версию                                                                                                                                                                                                                                                      [ https://a.yandex-team.ru/arc/commit/5603469 ]
 * WINADMINREQ-8029: Добавил новый шаблон                                                                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/5603171 ]
 * CERTOR-1115: Научиться выдавать ECC сертификаты через API                                                                                                                                                                                                          [ https://a.yandex-team.ru/arc/commit/5535492 ]
 * Поправил версию                                                                                                                                                                                                                                                    [ https://a.yandex-team.ru/arc/commit/5515032 ]
 * PR from branch users/stupidhobbit/CERTOR-1196-1

CERTOR-1196: Доработать функцию, создающую тикет

CERTOR-1194 Добавить тип сертификатов client-server в метод issue-certificates

CERTOR-1194 Добавить тип сертификатов client-server в метод issue-certificates  [ https://a.yandex-team.ru/arc/commit/5514810 ]

* [stampi](http://staff/stampi)

 * CERTOR-1445 Добавить новый паттерн                      [ https://a.yandex-team.ru/arc/commit/5742574 ]
 * CERTOR-1426 Сделать пагинацию по ID в синке со Стаффом  [ https://a.yandex-team.ru/arc/commit/5506313 ]

* [shadchin](http://staff/shadchin)

 * Drop library/python/django/patch for Django 1.11 CONTRIB-643  [ https://a.yandex-team.ru/arc/commit/5664147 ]

* [ndtretyak](http://staff/ndtretyak)

 * CERTOR-1441: убрал ZOMB_PC из DEVICES                                            [ https://a.yandex-team.ru/arc/commit/5808258 ]
 * Change pkg.json                                                                  [ https://a.yandex-team.ru/arc/commit/5790467 ]
 * CERTOR-1454: Проверять, что сервис заполнен перед поиском ответственных          [ https://a.yandex-team.ru/arc/commit/5790431 ]
 * Change pkg.json                                                                  [ https://a.yandex-team.ru/arc/commit/5786883 ]
 * Change pkg.json                                                                  [ https://a.yandex-team.ru/arc/commit/5786685 ]
 * CERTOR-1210: ускорение запроса                                                   [ https://a.yandex-team.ru/arc/commit/5786678 ]
 * Change pkg.json                                                                  [ https://a.yandex-team.ru/arc/commit/5780663 ]
 * CERTOR-1194: Добавить тип сертификатов client-server в метод issue-certificates  [ https://a.yandex-team.ru/arc/commit/5780524 ]
 * CERTOR-1256: проверять WHITE_LIST в ручке

CRT-1256: rename

Release 2.5         [ https://a.yandex-team.ru/arc/commit/5757890 ]
 * Release 2.5                                                                      [ https://a.yandex-team.ru/arc/commit/5686722 ]
 * Releasing version 2.0                                                            [ https://a.yandex-team.ru/arc/commit/5506720 ]

* [zivot](http://staff/zivot)

 * PR from branch users/zivot/CERTOR-1456

Поле ECC всегда

CERTOR-1456: Добавить признак ECC в интерфейсы и тикет st  [ https://a.yandex-team.ru/arc/commit/5799743 ]
 * COMPUTERPROBLEM-281: CRT (Сертификатор): Сломана выгрузка тегов                                                     [ https://a.yandex-team.ru/arc/commit/5796962 ]
 * readme updated                                                                                                      [ https://a.yandex-team.ru/arc/commit/5524028 ]
 * migrations fix                                                                                                      [ https://a.yandex-team.ru/arc/commit/5519074 ]
 * CERTOR-1409: os.makedirs(CRT_CVS_REPO_DIR) fix                                                                      [ https://a.yandex-team.ru/arc/commit/5458886 ]
 * CERTOR-1409: Дополнительные пакеты debian                                                                           [ https://a.yandex-team.ru/arc/commit/5457542 ]
 * CETROR-1409: default CERTUM_TEST_USERNAME changed                                                                   [ https://a.yandex-team.ru/arc/commit/5457538 ]

[ndtretyak](http://staff/ndtretyak) 2019-10-11 11:55:47+03:00

1.70.1
----
 * CERTOR-1356 добавление шаблона для ttl_days=365 в rc-server  [ https://github.yandex-team.ru/idm/yandex-crt/commit/0ffbbd1 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-07-31 17:31:49+03:00

1.70
----
 * CERTOR-1360 Считать total_errors (#363)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/4b36b50c ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-19 22:34:27+03:00

1.69
----
 * CERTOR-1360 Считать количество ошибок без InternalCA (#362)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/3c1bc2b2 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-19 18:51:17+03:00

1.68
----
 * CERTOR-1360 Nginx для мониторинга InternalCA (#359)                               [ https://github.yandex-team.ru/idm/yandex-crt/commit/a959d2c7 ]
 * CERTOR-1360 Мониторинги отдают 412, а не 500. Ручка проверки живости базы (#358)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/deea908a ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-07-16 13:23:57+03:00

1.67
----
 * CERTOR-1395: Проверить выписывание сертификата в тестовом Certum (#360)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/9f44f937 ]
 * Переделал пароли certum на переменную окружения (#361)                   [ https://github.yandex-team.ru/idm/yandex-crt/commit/b0667adb ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-07-16 12:49:36+03:00

1.66
----
 * CERTOR-1376: поправлен список разрешённых CA  [ https://github.yandex-team.ru/idm/yandex-crt/commit/e86192de ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-03 19:14:03+03:00

1.65
----
 * CERTOR-1376: Подключить новый УЦ YandexCBCA (#357)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/7597ed2b ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-07-03 13:07:08+03:00

1.64
----

* [Eldar Zaitov](http://staff/ezaitov@yandex-team.ru)

 * CERTOR-1036  [ https://github.yandex-team.ru/idm/yandex-crt/commit/ba51b473 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-07-02 10:29:27+03:00

1.63
----
 * CERTOR-1386 Привести имена аккаунта в locke к lowercase (#355)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/004207b4 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-06-24 19:28:07+03:00

1.62
----
 * CERTOR-1305: никогда не сохранять серты из блеклиста  [ https://github.yandex-team.ru/idm/yandex-crt/commit/6340130b ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-24 18:28:46+03:00

1.61
----

* [Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru)

 * CERTOR-1365 Правки после ревью + небольшая доработка клиента       [ https://github.yandex-team.ru/idm/yandex-crt/commit/e3056b5 ]
 * CERTOR-1365 Перейти на использование zeep в качестве SOAP-клиента  [ https://github.yandex-team.ru/idm/yandex-crt/commit/0a255d0 ]


1.59
----
 * CERTOR-1305: Не сохранять сертификат и изготовленный закрытый ключ в Секретницу для отдельных потребителей  [ https://github.yandex-team.ru/idm/yandex-crt/commit/88635468 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-06-19 15:57:20+03:00

1.58
----

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * CERTOR-1351: быстрофикс определения запрашивающего сертификат (#351)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/42d46d56 ]

* [Eldar Zaitov](http://staff/ezaitov@yandex-team.ru)

 * CERTOR-1318: Добавить признак EV в админку и письма о заказе сертификатов  [ https://github.yandex-team.ru/idm/yandex-crt/commit/a2d9279e ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-05-21 14:13:10+03:00

1.57
----
 * CERTOR-1316 Бросаем инстанс исключения             [ https://github.yandex-team.ru/idm/yandex-crt/commit/880bfea ]
 * CERTOR-1316 Add polosate to reviewers              [ https://github.yandex-team.ru/idm/yandex-crt/commit/da86395 ]
 * CERTOR-1316 Валидация csr при заказе сертификатов  [ https://github.yandex-team.ru/idm/yandex-crt/commit/609b47a ]

[Anastasiya Shaposhnikova](http://staff/polosate@yandex-team.ru) 2019-05-15 15:45:11+03:00

1.56
----
 * Исправление админки  [ https://github.yandex-team.ru/idm/yandex-crt/commit/1fd15f14 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-05-14 16:04:29+03:00

1.55
----

* [Eldar Zaitov](http://staff/ezaitov@yandex-team.ru)

 * Add more fields to admin list  [ https://github.yandex-team.ru/idm/yandex-crt/commit/59b6a06c ]

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * CERTOR-1343: валидировать, что CN входит в список SAN (#346)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/73a19198 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-05-08 09:51:14+03:00

1.54
----
 * CERTOR-1247: поправлен поброс юзернейма в закрытие тикета (#345)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/40f7d061 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-04-26 14:51:02+03:00

1.53
----

* [Eldar Zaitov](http://staff/ezaitov@yandex-team.ru)

 * CERTOR-1247 (#344)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/508bad15 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-04-26 14:25:13+03:00

1.52
----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * Update .devexp.json  [ https://github.yandex-team.ru/idm/yandex-crt/commit/388c5260 ]

* [ndtretyak](http://staff/ndtretyak@yandex-team.ru)

 * CERTOR-724: 400 вместо 500 при ошибке валидации  [ https://github.yandex-team.ru/idm/yandex-crt/commit/cea1e67a ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-04-23 12:02:12+03:00

1.51
----

* [Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru)

 * CERTOR-724: принимать desired_ttl_days в ручке reissue (#341)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/9ba26991 ]

[ndtretyak](http://staff/ndtretyak@yandex-team.ru) 2019-04-18 16:47:38+03:00

1.50
----
 * CERTOR-1249: поправлена миграция                                                              [ https://github.yandex-team.ru/idm/yandex-crt/commit/179e0eaf ]
 * CERTOR-1249: новый шаблон для нового типа                                                     [ https://github.yandex-team.ru/idm/yandex-crt/commit/f4278361 ]
 * CERTOR-1249: добавлен новый тип сертификатов и обвязки к нему, поправлены существующие тесты  [ https://github.yandex-team.ru/idm/yandex-crt/commit/6a5f5b44 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-04-15 11:58:49+03:00

1.49
----
 * Добавлена возможность запуска crt_sync_groups без учета threshold (#340)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/a737b27d ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-11 20:13:17+03:00

1.48
----
 * CERTOR-1304 Исправлен баг с удалением пользователя из фильтра (#339)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/4f542d23 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-11 13:31:19+03:00

1.47
----
 * Добавлена middleware для проверки сертификата при походе в idm-ные ручки  [ https://github.yandex-team.ru/idm/yandex-crt/commit/a6817de8 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-04-10 14:58:18+03:00

1.46
----
 * CERTOR-1314 поле request видно как charfield, должно быть textarea (#337)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/eff78e0e ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-04-08 19:40:39+03:00

1.45
----

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * CERTOR-1306: поправлено обнаружение wildcard-ов  [ https://github.yandex-team.ru/idm/yandex-crt/commit/65e0b74d ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * CERTOR-1313 Валидация email при запросе LinuxPC по csr (#336)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/a989c0ed ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-04-08 15:07:49+03:00

1.44
----

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * CERTOR-1306: добавлена валидация на несколько wildcard-хостов, тесты на это  [ https://github.yandex-team.ru/idm/yandex-crt/commit/ad0b2f84 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * CERTOR-1306: Wildcard сертификаты для УЦ Яндекс.Облака  [ https://github.yandex-team.ru/idm/yandex-crt/commit/f4511286 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2019-04-08 14:42:51+03:00

1.43
----
 * CERTOR-1302: Разрешить создание сертификатов для testing доменов Яндекс.Облака  [ https://github.yandex-team.ru/idm/yandex-crt/commit/1246568 ]

[chirkinvf](http://staff/chirkinvf@yandex-team.ru) 2019-03-25 14:13:22+03:00

1.42
----
 * CERTOR-1278 Добавлен робот в исключения в тестовом окружении (#331)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/0e321f76 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-03-21 14:22:26+03:00

1.41
----

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * CERTOR-1278: Не выдаём доступ к приватным ключам сертификатов, запрошенных роботами (#326)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/7c413e77 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-03-20 15:55:50+03:00

1.40
----

* [vladimir](http://staff/chirkinvf@yandex-team.ru)

 * CERTOR-1158 Обновил версию ylock  [ https://github.yandex-team.ru/idm/yandex-crt/commit/7ec6543 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * CERTOR-1286: Поправить тексты  [ https://github.yandex-team.ru/idm/yandex-crt/commit/21654c1 ]

[vladimir](http://staff/chirkinvf@yandex-team.ru) 2019-03-13 11:12:12+03:00

1.39
----
 * CERTOR-1158: Съехать с коммунального Zookeeper  [ https://github.yandex-team.ru/idm/yandex-crt/commit/61369d4 ]

[vladimir](http://staff/chirkinvf@yandex-team.ru) 2019-03-11 15:49:31+03:00

1.38
----
 * Обновлен DSN для Sentry (#325)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/908a0081 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-26 16:54:21+03:00

1.37
----
 * CERTOR-1261 Убрать ссылку на скачивание сертификата через API (#324)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/129b51dd ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-19 20:53:17+03:00

1.36
----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * Вернул pytest-sugar (#321)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/2b8c767a ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * CERTOR-1183: Домен .com.am не считается top-level доменом (#323)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/61b64870 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-15 14:04:16+03:00

1.35
----
 * CERTOR-1236 Записываем сертификат и приватный ключ в секретницу (#322)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/9bc56a5f ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-14 15:55:26+03:00

1.34
----
 * CERTOR-1236 Выдавать доступ к секрету скоупу из ABC (#319)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/c1d1ab88 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-13 12:07:43+03:00

1.33
----

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * CERTOR-1230: Поменять правила выдачи сертификатов для YcInternalCA (#318)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/59a0e66b ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-02-11 16:13:45+03:00

1.32
----
 * CERTOR-1222 Записываем ключи только хостовых сертификатов (#317)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/f12b3729 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-05 20:10:49+03:00

1.31
----
 * CERTOR-1222 Исправлено имя нового секрета (#316)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/4b0cedee ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-05 13:31:14+03:00

1.30
----
 * CERTOR-1222 Не используем итератор по queryset (#315)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/e74408a6 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-05 12:59:25+03:00

1.29
----
 * CERTOR-1222 Изменено название ключа секрета (#314)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/88600b5c ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-05 12:44:30+03:00

1.28
----
 * CERTOR-1222 Записывать приватный ключ в секретницу (#311)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/c4df9807 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-05 11:37:26+03:00

1.27
----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * CERTOR-1234: Зафиксировать версии пакетов в CRT (#313)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/ba3de4ca ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * CERTOR-1223 Исправление ошибок при тестировании (#312)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/b4bca841 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-02-04 17:34:26+03:00

1.26
----

* [vladimir](http://staff/chirkinvf@yandex-team.ru)

 * CERTOR-1206: Поменял равно на is в тесте              [ https://github.yandex-team.ru/idm/yandex-crt/commit/e9fafd3 ]
 * CERTOR-1206: Принимать csr для LinuxPcCertSerializer  [ https://github.yandex-team.ru/idm/yandex-crt/commit/de5ae7e ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * CERTOR-1224 Синхронизировать состав scope (#305)                      [ https://github.yandex-team.ru/idm/yandex-crt/commit/dc17ad1 ]
 * CERTOR-1223 Позволить пользователю передавать в api secret_id (#308)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/d8b8236 ]

[vladimir](http://staff/chirkinvf@yandex-team.ru) 2019-02-04 14:34:41+03:00

1.25
----
 * CERTOR-1055: Не работает фильтр по владельцу  [ https://github.yandex-team.ru/idm/yandex-crt/commit/5548e62 ]

[vladimir](http://staff/chirkinvf@yandex-team.ru) 2019-01-31 18:50:53+03:00

1.24
----
 * CERTOR-1231: Обновить библиотеки CRT до аркадийных версий (#306)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/c7fe7ce8 ]

[Vladimir Kutyavin](http://staff/zivot@yandex-team.ru) 2019-01-31 18:15:07+03:00

1.23
----
 * CERTOR-1220 Отдавать в api параметр 'requested_by_csr' (#304)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/347d1339 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-01-30 13:52:13+03:00

1.22
----
 * CERTOR-1220 Добавить дополнительные поля в модель (#303)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/f8045dc2 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-01-29 15:23:57+03:00

1.21
----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * Добавил dev-зависимости в образ (#301)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/313b7351 ]
 * Добавил ревьюеров, tmux (#300)          [ https://github.yandex-team.ru/idm/yandex-crt/commit/86e03612 ]

* [Arsenii Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * CERTOR-1226: 504 при выгрузке информации по сертификатам через API (#302)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/8813de56 ]

[Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru) 2019-01-25 19:58:21+03:00

1.20
----

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * CERTOR-1005 Убрать из саджеста YC и RC intrenalCA (#298)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/c05f2bc5 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * CERTOR-1205: Письмо про сертификаты асессорам -- поправить адресат внутри письма  [ https://github.yandex-team.ru/idm/yandex-crt/commit/42db41f6 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2019-01-11 14:36:20+03:00

1.19
----
 * CERTOR-1193: Поправить regexp для сертификатов NOC  [ https://github.yandex-team.ru/idm/yandex-crt/commit/d2efb4c9 ]
 * Обновил конфиг ревьюшницы                           [ https://github.yandex-team.ru/idm/yandex-crt/commit/d7107f7e ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-12-28 21:24:41+03:00

1.18
----

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * releasing version 1.7.1  [ https://github.yandex-team.ru/idm/yandex-crt/commit/1ef75bb ]

* [zivot](http://staff/zivot@yandex-team.ru)

 * CERTOR-1134 Долгие селекты с WHERE end_date (#276)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/aeda138 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * CERTOR-1185: ращрешены дополнительные домены для YC  [ https://github.yandex-team.ru/idm/yandex-crt/commit/8476e09 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-12-11 17:51:56+03:00

1.17
----

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * CERTOR-1163: Поправил конфиг  [ https://github.yandex-team.ru/idm/yandex-crt/commit/fa5aaea5 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * CERTOR-1137 Все запросы из админки переводим на master  [ https://github.yandex-team.ru/idm/yandex-crt/commit/130712de ]

[Alexey Boriskin](http://staff/uruz@yandex-team.ru) 2018-11-29 16:12:24+03:00

1.16
----

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * CERTOR-1137-4 Добавлена возможность оперативного выхода из ручного readonly (#292)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/0c4e7a66 ]
 * CERTOR-1137-3 Исправлен флаг проверки живости базы данных                           [ https://github.yandex-team.ru/idm/yandex-crt/commit/0ac5bc5b ]
 * CERTOR-1137-2 Исправлена работа флага ручного перехода в readonly                   [ https://github.yandex-team.ru/idm/yandex-crt/commit/8c3d61e3 ]

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * CERTOR-1163: Сквозное ревью + уведомления в почту                   [ https://github.yandex-team.ru/idm/yandex-crt/commit/e79e29b7 ]
 * CERTOR-1140: поправил команду my2pg и обновил ссылку на либу my2pg  [ https://github.yandex-team.ru/idm/yandex-crt/commit/65e61f2b ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-11-26 19:13:35+03:00

1.15
----
 * CERTOR-1137-3 Исправлен флаг проверки живости базы данных  [ https://github.yandex-team.ru/idm/yandex-crt/commit/16ef0e73 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-11-22 18:49:02+03:00

1.14
----
 * CERTOR-1137-2 Исправлена работа флага ручного перехода в readonly  [ https://github.yandex-team.ru/idm/yandex-crt/commit/f1aa780d ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-11-22 16:47:38+03:00

1.13
----
 * CERTOR-1140: поправил команду my2pg и обновил ссылку на либу my2pg  [ https://github.yandex-team.ru/idm/yandex-crt/commit/65e61f2b ]

[Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru) 2018-11-20 17:27:00+03:00

1.12
----

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * 1140: pg_password в переменной  [ https://github.yandex-team.ru/idm/yandex-crt/commit/6058ff2 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-19 19:29:28+03:00

1.11
----
 * CERTOR-1140: pg_password в переменной окружения  [ https://github.yandex-team.ru/idm/yandex-crt/commit/c0e6dcba ]

[Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru) 2018-11-19 18:24:42+03:00

1.10
----

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * CERTOR-1156: Поправлена зависимость от pymongo; В отдельный файл вынесены зависимости добавляемые руками  [ https://github.yandex-team.ru/idm/yandex-crt/commit/e40d7c0 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * CERTOR-1153: Получаем клиент явно, чтобы не ходить в Certum когда не нужно  [ https://github.yandex-team.ru/idm/yandex-crt/commit/72d45de ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * CERTOR-1155: в фильтрах проставлены distinct=False  [ https://github.yandex-team.ru/idm/yandex-crt/commit/5e7efbd ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-19 17:45:31+03:00

1.9
---

* [Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru)

 * CERTOR-1140: увеличен размер поля unit в crtusers                                                [ https://github.yandex-team.ru/idm/yandex-crt/commit/3ae29c3 ]
 * CERTOR-1140: +Пакет для переливки в зависимостях и команда для его запуска в managment/commands  [ https://github.yandex-team.ru/idm/yandex-crt/commit/3df3d4d ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * Правки по ревью, добавил if-блок  [ https://github.yandex-team.ru/idm/yandex-crt/commit/6401e71 ]
 * Добавить pytest-html              [ https://github.yandex-team.ru/idm/yandex-crt/commit/a08e805 ]
 * Исправил тест для postgresql      [ https://github.yandex-team.ru/idm/yandex-crt/commit/e54bafd ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * CERTOR-1154: разрешили запуск Celery от рута  [ https://github.yandex-team.ru/idm/yandex-crt/commit/7fc9c51 ]
 * Конфиг Ревьюшницы                             [ https://github.yandex-team.ru/idm/yandex-crt/commit/55ebbfb ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-11-19 15:59:33+03:00

1.8
---


* [zivot](http://staff/zivot@yandex-team.ru)

 * CERTOR-1134 Долгие селекты с WHERE end_date (#276)                                          [ https://github.yandex-team.ru/idm/yandex-crt/commit/c1a1e217 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * CERTOR-1136: Улучшил регулярку, из-за которой падали тесты                     [ https://github.yandex-team.ru/idm/yandex-crt/commit/d5afaa2c ]
 * CERTOR-1136: Убрал проброс портов                                              [ https://github.yandex-team.ru/idm/yandex-crt/commit/79028cc1 ]
 * CERTOR-1136: Поправил ворнинги                                                 [ https://github.yandex-team.ru/idm/yandex-crt/commit/1a7825bb ]
 * CERTOR-1136: Поправил падавший из-за захардкоженного айдишника тест            [ https://github.yandex-team.ru/idm/yandex-crt/commit/975f3ed5 ]
 * CERTOR-1136: Тесты на postgresql                                               [ https://github.yandex-team.ru/idm/yandex-crt/commit/8d9ae13e ]
 * CERTOR-1136: Новые дебиан и python зависимости для postgresql                  [ https://github.yandex-team.ru/idm/yandex-crt/commit/b7d17ec8 ]

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * Исправил тесты                                                                                                                 [ https://github.yandex-team.ru/idm/yandex-crt/commit/4c62d3f2 ]
 * Добавил возможность переключения между mysql и psql при установке переменной Поправил 2 теста для корректой работы на postgre  [ https://github.yandex-team.ru/idm/yandex-crt/commit/733171cc ]
 * CERTOR-1137 Добавлена возможность ручного перехода в read_only                                                                 [ https://github.yandex-team.ru/idm/yandex-crt/commit/a115b698 ]

[Arseny Vitchenko](http://staff/forestdeer@yandex-team.ru) 2018-11-12 20:46:19+03:00

1.7.1
---

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)
 * CERTOR-1134 Долгие селекты с WHERE end_date (#276)                                          [ https://github.yandex-team.ru/idm/yandex-crt/commit/aeda138a ]

1.7
---
 * CRT-1108-4 Изменения для CRT-1108 скорректирована cron команда пересчета метрик  [ https://github.yandex-team.ru/idm/yandex-crt/commit/9dfefd76 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-10-26 18:28:14+03:00

1.6
---
 * CRT-1108-3 Корректировки для CRT-1108 поддержка выкатки celery  [ https://github.yandex-team.ru/idm/yandex-crt/commit/378abac2 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-10-26 17:22:57+03:00

1.5
---

* [Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru)

 * CRT-1108-2 Исправления для CRT-1108  [ https://github.yandex-team.ru/idm/yandex-crt/commit/cb978377 ]

* [Alexey Boriskin](http://staff/uruz@yandex-team.ru)

 * Add trendbox  [ https://github.yandex-team.ru/idm/yandex-crt/commit/77b62e78 ]

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * CERTOR-1089 Добавить db.yandex.net в список доменов хостов Яндекс-облака (yc-server)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/2789d5b7 ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-10-26 17:04:08+03:00

1.4
---
 * CERTOR-1108 Мониторинг истекающих сертификатов для RcInternalCA, YcInternalCA и InternalCA (#269)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/6c31063c ]

[Stanislav Prokopchuk](http://staff/stampi@yandex-team.ru) 2018-10-22 17:20:01+03:00

1.3.3
---

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * CERTOR-1089 Добавить db.yandex.net в список доменов хостов Яндекс-облака (yc-server)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/bf195319 ]

1.3
---
 * CERTOR-1128: Уменьшить размер батча при синке пользователей  [ https://github.yandex-team.ru/idm/yandex-crt/commit/81e0de4 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-10-18 17:25:59+03:00

1.2
---
 * CERTOR-1124: обрабатывать пользователей батчами  [ https://github.yandex-team.ru/idm/yandex-crt/commit/ef444bd5 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-16 17:05:35+03:00

1.1
---
 * CERTOR-1091: поправлено добавление common_name в SANы, если нам присылают только common_name (без csr)                             [ https://github.yandex-team.ru/idm/yandex-crt/commit/1d858fb ]
 * CERTOR-1091: снова используем новое поведение для записи CN в список SANов                                                         [ https://github.yandex-team.ru/idm/yandex-crt/commit/08d4668 ]
 * CERTOR-1091: добавлен тест на указание хостов для yc-server, поправлена запись первого SANа в CN                                   [ https://github.yandex-team.ru/idm/yandex-crt/commit/d4a90dd ]
 * CERTOR-1091: возвращено старое поведение с добавлением CN в список SANов                                                           [ https://github.yandex-team.ru/idm/yandex-crt/commit/755ef7c ]
 * CERTOR-1091: поправлен тест на хостовые сертификаты                                                                                [ https://github.yandex-team.ru/idm/yandex-crt/commit/d69e267 ]
 * CERTOR-1091: поправлен csr-конфиг                                                                                                  [ https://github.yandex-team.ru/idm/yandex-crt/commit/5bec717 ]
 * CERTOR-1091: поправлен баг, когда при заказе через CSR common_name добавлялся в список хостов (даже если хосты были явно указаны)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/46cb671 ]
 * CERTOR-1091: небольшие правки по багам                                                                                             [ https://github.yandex-team.ru/idm/yandex-crt/commit/85e2055 ]
 * CERTOR-1091: list -> tuple в описании полей                                                                                        [ https://github.yandex-team.ru/idm/yandex-crt/commit/a1c9790 ]
 * CERTOR-1091: добавлена команда для миграции старых сертификатов yc-server                                                          [ https://github.yandex-team.ru/idm/yandex-crt/commit/d9658dd ]
 * CERTOR-1091: сериализатор yс-server теперь корректно обрабатывает поле hosts                                                       [ https://github.yandex-team.ru/idm/yandex-crt/commit/853b842 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-10-11 17:02:44+03:00

1.0
-------
 * CERTOR-1112: увеличить длину поля validation_code  [ https://github.yandex-team.ru/idm/yandex-crt/commit/464022ff ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-05 16:29:41+03:00

0.66.22
-------
 * CERTOR-1083: Запрет слэша и знака равно в email  [ https://github.yandex-team.ru/idm/yandex-crt/commit/6f76abb5 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-10-04 15:43:53+03:00

0.66.21
-------
 * CERTOR-1111: добавить параметр hashAlgorithm для ECC-сертификатов  [ https://github.yandex-team.ru/idm/yandex-crt/commit/6f3e0d63 ]

[Nikolay Tretyak](http://staff/ndtretyak@yandex-team.ru) 2018-10-03 17:28:53+03:00

0.66.20
-------

* [Pavel Kondratiev](http://staff/kaloprominat@yandex.ru)

 * CERTOR-1095: выносим сертификат в профиле iphone exchange в отдельный пейлоад  [ https://github.yandex-team.ru/idm/yandex-crt/commit/6668aed ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-28 15:33:23+03:00

0.66.19
-------
 * CERTOR-1099: поправлено преобразование к строке при логировании                       [ https://github.yandex-team.ru/idm/yandex-crt/commit/2960473 ]
 * CERTOR-1099: теперь при фейле уведомления об одном сертификате вся команда не падает  [ https://github.yandex-team.ru/idm/yandex-crt/commit/989b845 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-27 17:10:21+03:00

0.66.18
-------
 * feature/CERTOR-931: Убрал параметр gentle_reminder_days. Добавил ссылку на предзаполненный шаблон  [ https://github.yandex-team.ru/idm/yandex-crt/commit/2e147919 ]
 * Убрал ненужный метод                                                                               [ https://github.yandex-team.ru/idm/yandex-crt/commit/96ac51d7 ]
 * feature/CERTOR-931: Перенес настройки в модель                                                     [ https://github.yandex-team.ru/idm/yandex-crt/commit/3754002a ]
 * feature/CERTOR-931: убрал print                                                                    [ https://github.yandex-team.ru/idm/yandex-crt/commit/c861a900 ]
 * feature/CERTOR-931: Поправил шаблон. Вынес проверку ca_name в constants                            [ https://github.yandex-team.ru/idm/yandex-crt/commit/98757b37 ]
 * feature/CERTOR-931: доработка оповещений о протухающих сертификатах                                [ https://github.yandex-team.ru/idm/yandex-crt/commit/8a9e6cb2 ]
 * feature/CRT-1072: Игнорировать ручку ping                                                          [ https://github.yandex-team.ru/idm/yandex-crt/commit/159c6dfb ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-09-27 15:00:00+03:00

0.66.17
-------
 * feature/CRT-1072: Переименовал настройку              [ https://github.yandex-team.ru/idm/yandex-crt/commit/949ece42 ]
 * feature/CRT-1072: Middleware для QLOUD_SECRET_HEADER  [ https://github.yandex-team.ru/idm/yandex-crt/commit/91edba34 ]

[Tamirlan Omarov](http://staff/tamirok@yandex-team.ru) 2018-09-21 21:47:17+03:00

0.66.16
-------
 * CERTOR-1090: добавлены тесты на ответ с ошибками                                                     [ https://github.yandex-team.ru/idm/yandex-crt/commit/d62b943 ]
 * CERTOR-1090: теперь мы благосклонно принимаем Цертумовскую ошибку о том, что сертификат уже отозван  [ https://github.yandex-team.ru/idm/yandex-crt/commit/92411c4 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-21 15:14:08+03:00

0.66.15
-------
 * CERTOR-1090: более подробная ошибка при получении неизвестного сертификата  [ https://github.yandex-team.ru/idm/yandex-crt/commit/3978072 ]
 * CERTOR-1090: поправлены тесты для yc-server                                 [ https://github.yandex-team.ru/idm/yandex-crt/commit/1e1cc9f ]
 * CERTOR-1090: поправлены тесты для ручки reissue                             [ https://github.yandex-team.ru/idm/yandex-crt/commit/481f44c ]
 * CERTOR-1090: добавлен новый шаблон для common_name                          [ https://github.yandex-team.ru/idm/yandex-crt/commit/807309c ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-20 20:27:54+03:00

0.66.14
-------
 * Таймаут до внутренних CA увеличен до 30 секунд  [ https://github.yandex-team.ru/idm/yandex-crt/commit/3ab0cc6 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-19 16:37:22+03:00

0.66.13
-------

* [Vladimir Kutyavin](http://staff/zivot@yandex-team.ru)

 * CERTOR-1066: Таймаутится отзыв сертификата RCInternalCA  [ https://github.yandex-team.ru/idm/yandex-crt/commit/7449f51 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * CERTOR-1082: увеличен timeout при хождении в uatraits.qloud.yandex.ru  [ https://github.yandex-team.ru/idm/yandex-crt/commit/ec63d1d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-19 13:38:35+03:00

0.66.12
-------
 * Поправлено раскладывание ssh в докерфайле  [ https://github.yandex-team.ru/idm/yandex-crt/commit/d56d4c2 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-17 20:20:35+03:00

0.66.11
-------

* [zivot](http://staff/zivot@yandex-team.ru)

 * CERTOR-1079 Конфиг openvpn без опции "link-mtu 1492" (Android) (#254)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/217d29b ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * Поправлен конфиг ssh  [ https://github.yandex-team.ru/idm/yandex-crt/commit/510958d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-17 20:05:55+03:00

0.66.10
-------
 * Перехать с www-data на root  [ https://github.yandex-team.ru/idm/yandex-crt/commit/ce7db91 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-17 18:12:21+03:00

0.66.9
------
 * Апнут django_tools_log_context до поправленной версии  [ https://github.yandex-team.ru/idm/yandex-crt/commit/bb20a69 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-17 17:30:34+03:00

0.66.8
------
 * Обновлены зависимости  [ https://github.yandex-team.ru/idm/yandex-crt/commit/3e52866 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-17 14:12:05+03:00

0.66.7
------
 * CERTOR-1077: прописан почтовый релей Почты                                  [ https://github.yandex-team.ru/idm/yandex-crt/commit/98e4e91 ]
 * CERTOR-1075: поправлена (и упрощена) интеграция с django_tools_log_context  [ https://github.yandex-team.ru/idm/yandex-crt/commit/b85d3e4 ]
 * CERTOR-1074: поправлен IOError                                              [ https://github.yandex-team.ru/idm/yandex-crt/commit/43c8087 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-17 13:50:14+03:00

0.66.6
------

* [zivot](http://staff/zivot@yandex-team.ru)

 * CERTOR-1060: Обновить сертификат YandexInternalCA в конфиге для мобильного Exchange (#251)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/c7bb431 ]
 * CERTOR-1062: Замороженные сертификаты у новых сотрудников (#252)                            [ https://github.yandex-team.ru/idm/yandex-crt/commit/0f774b1 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * CERTOR-1028: обнуляем не подходящий нам сертификат            [ https://github.yandex-team.ru/idm/yandex-crt/commit/319a628 ]
 * CERTOR-1028: поправлен формат ssl-заголовков в ручке reissue  [ https://github.yandex-team.ru/idm/yandex-crt/commit/a045f57 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-13 19:08:07+03:00

0.66.5
------
 * Поправлен комментарий в настройках  [ https://github.yandex-team.ru/idm/yandex-crt/commit/5265469 ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-11 20:19:36+03:00

0.66.3
------
 * Поправлен список разрешённых доменов в ALLOWED_HOSTS  [ https://github.yandex-team.ru/idm/yandex-crt/commit/4f6e54f ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-11 19:28:25+03:00

0.66.2
------

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * releasing version 1.12        [ https://github.yandex-team.ru/idm/yandex-crt/commit/f65b657 ]
 * CERTOR-915 Docker             [ https://github.yandex-team.ru/idm/yandex-crt/commit/554c342 ]
 * CERTOR-915 token log removed  [ https://github.yandex-team.ru/idm/yandex-crt/commit/93b0a5d ]

* [zivot](http://staff/zivot@yandex-team.ru)

 * CERTOR-1021: Подключить django_tools_log_context (#242)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/e2150ba ]
 * CERTOR-1020: Подключить Sentry (#241)                    [ https://github.yandex-team.ru/idm/yandex-crt/commit/28b1431 ]

* [Vitaly Sopov](http://staff/v-sopov@yandex-team.ru)

 * CERTOR-1028: поправлены заголовки информации о клиентском сертификате (#250)  [ https://github.yandex-team.ru/idm/yandex-crt/commit/5832c1f ]
 * CERTOR-915: поправлен конфиг releaser'а                                       [ https://github.yandex-team.ru/idm/yandex-crt/commit/6a4ee25 ]
 * CERTOR-915: сконвертирован changelog                                          [ https://github.yandex-team.ru/idm/yandex-crt/commit/cf3502d ]

[Vitaly Sopov](http://staff/v-sopov@yandex-team.ru) 2018-09-11 16:19:53+03:00

0.66.1.1
---

  * CERTOR-1062: Замороженные сертификаты у новых сотрудников (#252)
  * CERTOR-1060: Обновить сертификат YandexInternalCA в конфиге для мобильного Exchange (#251)

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2018-09-12 15:15:18

0.66.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-1051: Фикс для новой ручки Наниматора

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-09-10 15:47:11

0.66.0
---

 * [Nikolay Tretyak](https://staff.yandex-team.ru/Nikolay%20Tretyak)

  * CERTOR-1051: новая ручка newhire

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-09-07 13:42:18

0.65.1
---

  * CERTOR-1053: Поменять домены хостов Яндекс-облака (yc-server) (#249)

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2018-09-05 19:49:51

0.65.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-869: Расширил ALLOWED\_HOSTS

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-08-29 19:56:23

0.64.0
---

 * [Nikolay Tretyak](https://staff.yandex-team.ru/Nikolay%20Tretyak)

  * CERTOR 1034: улучшена обработка исключений
  * CERTOR-1034: тест
  * CERTOR-1047: обновить mobvpn-ca

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-869: Не снимается in\_hiring у просроченных заявок

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-08-29 15:39:32

0.63.1
---

 * [Nikolay Tretyak](https://staff.yandex-team.ru/Nikolay%20Tretyak)

  * CERTOR-1047: обновить mobvpn-ca

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-09-03 16:29:22

0.63.0
---

 * [Nikolay Tretyak](https://staff.yandex-team.ru/Nikolay%20Tretyak)

  * CERTOR-1037: отзывать импортированные серты
  * CERTOR-1037: логирование

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-08-28 17:37:42

0.62.1
---

  *  CERTOR-627: Добавил авторизацию по client-server сертификатам (#245)

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2018-08-24 17:03:06

0.62.0
---

  * СERTOR-627: Возможность перезаказывать client-server сертификаты (#243)

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2018-08-23 12:35:22

0.61.1
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-1017: Добавить домены crypta.yandex.net и rtcrypta.yandex.net к разрешенным для запроса rc-server (#238)

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * CERTOR-1008: Добавил возможность авторизоваться с vpn-token (#239)


 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2018-08-13 18:16:53

0.61.0
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * CERTOR-1008: Ручка для перевыпуска сертификата для надомников (#237)

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2018-08-11 13:16:23

0.60.2
---

  * CERTOR-992: вытаскивать пользователя vpntoken-сертификата из common\_name (#235)
  * CERTOR-1001: теперь пользователь имеет аналогичные права, что и запрашивающий, для всех типов сертификатов (#234)

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-08-09 13:30:20

0.60.1.1
---

  * CERTOR-992: вытаскивать пользователя vpntoken-сертификата из common\_name (#235)
  * CERTOR-1001: теперь пользователь имеет аналогичные права, что и запрашивающий, для всех типов сертификатов (#234)
  * CERTOR-1017: Добавить домены crypta.yandex.net и rtcrypta.yandex.net к разрешенным для запроса rc-server (#238)

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-08-13 15:28:21

0.60.1
---

  * CERTOR-1010: при наличии сертификата проверка через yauth не выполняется
  * CERTOR-1010: поправлено вытаскивание пользователя в миддлвари
  * CERTOR-1010: небольшие правки по проверке ssl-аутентифицированности клиента
  * CERTOR-1010: упрощено получение пользователя в ssl-миддлвари

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-08-06 15:54:11

0.60.0
---

 * [Nikolay Tretyak](https://staff.yandex-team.ru/Nikolay%20Tretyak)

  * CERTOR-999: не холдить сертификат, если новый не выписан

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-07-24 15:17:35

0.59.3
---

  * CERTOR-996: Изменить отдаваемый конфиг для vpn

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-07-18 16:35:50

0.59.2
---

  * Поправлена кодировка цепочки тестового сертификата

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-07-10 18:09:52

0.59.1
---

  * Обновлена цепочка для InternalTestCA

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-07-10 16:51:41

0.59
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-982: Временно выключить InternalCA
  * CERTOR-982: Поддержать новый сертификат InternalCA
  * Revert "CERTOR-982: Временно выключить InternalCA"
  * CERTOR-985: Поднять лимит перевыпуска pc-сертификатов с 45 до 120 дней (#230)
  * CERTOR-983: Поднять лимиты на мониторинги cvs-upload

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-07-10 15:37:41

0.56.2
---

  * CERTOR-971: поправить ссылку на аппрув с crt.y-t.ru на crt-api.y-t.ru
  * CERTOR-909: поправить проверку на тип сертификата в пермишне
  * CERTOR-909: поправить проверку на тип сертификата в пермишне
  * CERTOR-909: поправлены тесты

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-06-28 16:55:06

0.56.1
---

  * CERTOR-966: из наниматора теперь синкаются сотрудники со статусами 30 и 40
  * CERTOR-966: допустимая дельта для Наниматора увеличена с 14 до 60 дней
  * CERTOR-475: Нет проверки скоупов oauth токенов в Сертификаторе (#222)

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-06-28 15:17:21

0.56.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-909: Владелец, не совпадающий с запросившим, не может скачать сертификат

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-06-13 19:17:55

0.55.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-919: Поднял threshold до 150
  * CERTOR-941: log.info should not use format(). Added some clarifications
  * CERTOR-941: Log verification code first, do checking later
  * CERTOR-941: Падающий тест
  * CERTOR-941: Move function around
  * CERTOR-941: Не отгружается ydata.co.il в ручку валидационных доменов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-06-08 17:32:43

0.54.2
---

  * CERTOR-768 remove backup private key
  * CERTOR-768 remove private keys
  * CERTOR-768 encrypt private key

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-06-08 15:03:43

0.54.1
---

  * CERTOR-894: поправлена отдача полей в форме, поправлен ввод хостов, неправильный CSR теперь не кидает пятисотку, пустое поле хостов теперь не кидает эксепшн, в поле отдаются только валидные CA
  * CERTOR-894: CertumProductionCA заменён на CertumTestCA в тестах на Цертум
  * CERTOR-894: апнута версия DRF
  * CERTOR-894: хосты в апишной форме теперь отдаются через запятую, а не питонячим списком

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-06-05 12:53:10

0.54.0
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-894: поправлена html-форма, разрешён заказ хостовых сертификатов через CSR
  * CERTOR-894: виджет для csr в форме заменён на textarea
  * CERTOR-894: виджет для abc\_service в форме заменён на текстовый
  * CERTOR-894: поправлен тест на фронтовую ручку /fields

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-31 16:22:02

0.53.1
---

  * CERTOR-859: унифицирована обработка строкоподобных полей
  * CERTOR-859: проверка на тип поля теперь выполняется через isinstance
  * CERTOR-889: в ручке userdata пользователю с NEED\_RESET-куками возвращается редирект на Паспорт
  * CERTOR-889: подновление кук на урлах из белого списка теперь не происходит
  * CERTOR-889: отсутствие sessionid2 теперь тоже отлавливается
  * CERTOR-889: игнорируем все редиректы на Паспорт
  * CERTOR-889: not\_authenticated -> authenticated
  * CERTOR-889: поправлена проверка протухших кук
  * CERTOR-889: поправлены другие middleware и вьюхи
  * CERTOR-889: perform\_authentication вынесена в миксин
  * CERTOR-885: [API V2] Отображать только доступные действия в ручке certificate (#211)
  * CERTOR-888: длина хоста и common\_name увеличена до 255 символов
  * CERTOR-887: в v1 хосты теперь сплитятся и по whitespace
  * CERTOR-887: валидация хостов перенесена в хостовый сериализатор
  * CERTOR-888: сериализаторы хостов разделены для v1 и v2

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-05-17 12:37:39

0.53.0
---

  * CERTOR-870 user names max len up
  * CERTOR-876 add revoke action on certificate detail post
  * CERTOR-881 hosts parsing bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-05-08 16:50:13

0.52.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-873: Не удается получить сертификат скриптом

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2018-05-02 22:43:58

0.51.0
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-861: отдавать поле used\_template в api
  * CERTOR-860: Передавать на фронт локализованные названия действий (#203)
  * CERTOR-868: from\_db перенесён из спискового сериализатора в обычный

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Фикс синхронизации с наниматором

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)


 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-04-28 20:23:13

0.50.20
---

  * CERTOR-864: idm/ добавлен в белый список

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-28 14:24:11

0.50.19
---

  * CERTOR-848: убрана кастомная спецификация поля is\_waiting\_for\_validation
  * CERTOR-848: для hosttoapprove все базовые поля помечены readonly
  * CERTOR-841: во все фронтовые ручки (кроме userdata) добавлена проверка пермишна IsAuthenticated
  * CERTOR-841: проверка аутентификации сделана через подправленную yauth-middleware
  * CERTOR-841: теперь мы корректно определяем пользователя
  * CERTOR-841: теперь мы не редиректим на паспорт, а кидаем 401
  * CERTOR-841: добавлены ручки без аутентификации, удалена ручка с получением случайного пароля
  * CERTOR-841: возврат ответа от дефолтной миддлвари (если есть), переименована функция

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-27 18:37:59

0.50.18
---

  * CERTOR-858: Для полей с датами всегда присылать строку

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-27 15:00:47

0.50.17
---

  * CERTOR-842: теперь мы возвращаем пустую строку только во фронтенд
  * CERTOR-842: теперь сериализаторы для v2 параметризуются через класс опций

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-26 16:26:40

0.50.16
---

  * CERTOR-842: отсутствующий serial\_number теперь отдаётся в виде пустой строки
  * CERTOR-846: добавлена отрисовка дефолтного описания для неизвестных т… (#196)
  * CERTOR-847: Очеловечить названия типов/статусов/т.д. (#198)
  * CERTOR-851: из выдачи ручки fields удалён CSR (до лучших времён)
  * CERTOR-855: теперь в /api/frontend/ проксируется v2 целиком

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-26 13:29:09

0.50.15
---

  * CERTOR-804: все действия, кроме обновления сервиса, выделены в отдельные вьюхи
  * CERTOR-804: поправлена проверка пермишнов, добавлена ручка download
  * CERTOR-804: поправлены ссылки на страницу сертификата и на скачивание
  * CERTOR-804: теперь поле status необязательно, поправлен параметр \_fields
  * CERTOR-804: тесты теперь проверяют и v2
  * CERTOR-804: теперь мы возвращаем допустимые действия. Переделаны пермишны для v2
  * CERTOR-804: из красивой апишной морды выпилена html-форма
  * CERTOR-804: формат при скачивании сертификата теперь задаётся через параметры запроса
  * CERTOR-804: поправлен тест на certum
  * CERTOR-804: поле abc\_service сделано обязательным
  * CERTOR-804: hold-unhold-revoke вынесены в единую ручку operations
  * CERTOR-804: убрана грязь с \_\_class\_\_ и неактуальные TODO-шки
  * CERTOR-804: переделаны пермишны для v2, обновление сертификата теперь происходит через PATCH, все действия возвращают описание сертификата

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-23 16:07:07

0.50.14
---

  * CERTOR-843: в мета-информацию добавлен номер текущей страницы

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-23 15:28:56

0.50.13
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Добавил /certificates/ в нейспейс frontend по просьбе remnev@

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2018-04-20 14:21:00

0.50.12
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-823: Подключить YandexCLCA
  * CERTOR-823: Fix username for YcInternalCA
  * CERTOR-807: Поправил тесты и константы
  * Certum full test

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * Правки по ручке полей из CERTOR-808 (#191)
  * Запинена версия pip==9.0.3

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-19 14:16:07

0.50.11
---

  * CERTOR-808: [API V2] Сделать ручку fields (#184)

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-12 17:30:21

0.50.10
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-807: реорганизована структура url, добавлен простая suggest-вьюха для пользователей
  * CERTOR-807: обработан случай с пустым именем, поправлена обработка параметров запроса
  * CERTOR-807: добавлена интернационализация, сортировка выдачи
  * CERTOR-807: добавлен саджест для ca\_name
  * CERTOR-807: саджест для пользователей теперь ходит в intrasearch
  * CERTOR-807: теперь мы корректно прописываем имена на двух языках в пользовательском саджесте
  * CERTOR-807: рефакторинг вьюх
  * CERTOR-807: саджест для статусов
  * CERTOR-807: добавлен саджест для типов сертификатов, хуманизированные имена для типов и статусов
  * CERTOR-807: добавлена регистронезависимость для параметра search
  * CERTOR-807: саджест для хостов
  * CERTOR-807: теперь пагинация пагинирует правильно
  * CERTOR-807: саджест для сервисов
  * CERTOR-807: добавлены тесты на саджест
  * CERTOR-825: фильтр abc\_service\_\_isnull для новой версии DRF (#185)
  * CERTOR-765: теперь мы не пропускаем дефис в конце и в начале блока (#188)

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-807: Проставил везде слеши и переименовал вьюху
  * CERTOR-807: Убрал копипасту, добавил фильтрацию типов сертификатов по названию CA
  * CERTOR-807: Поправил настройки для разработки

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-09 14:42:17

0.50.9
---

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-765: добавлена регулярка для проверки хостов, поправлены тесты
  * CERTOR-765: убран warning на кириллические хосты

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-765: Удалил старую неиспользуемую регулярку
  * CERTOR-765: Поправил падающий тест

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-03 14:25:05

0.50.8
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-806: Поперемещал тесты
  * CERTOR-806: Добавлены поля в синхронизации пользователей, добавлена первая версия ручки /userdata и тесты для неё

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-806: добавлена синхронизация русских имён и fullname, переделана ручка /userdata и тесты под это всё
  * CERTOR-806: добавлена джанговая миграция на поля
  * CERTOR-806: добавлен индекс для полного имени

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-02 16:08:41

0.50.7
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * use cryptography
  * add custom shell\_plus imports

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-607: render\_to\_response заменён на render
  * CERTOR-607: попытка поправить GET на detail сертификата
  * CERTOR-607: правки по пагинации
  * CERTOR-607: у hosttoapprove обработана ситуация, когда нам не приходит data
  * CERTOR-607: правки по соответствию объявленных полей и fields, небольшие правки по фильтрации сертификатов

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-02 14:09:38

0.50.6
---
 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-720: Распилил API на кусочки
  * CERTOR-607: правки по отсутствующему полю request
  * Up to current BrowserableAPIRenderer

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-03-28 14:15:46

0.50.5
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-792 up uwsgi buffer size

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-607: добавлено приложение django.contrib.sites, переименована настройка миддлварей, миддлвари унаследованы от deprecation-миксина
  * CERTOR-607: попытка исправить AlmostBrowsableAPI
  * CERTOR-607: теперь yauth не пытается найти хост через Site
  * CERTOR-607: правки по отсутствующему полю request
  * CERTOR-607: middleware переделаны на современный лад

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-03-27 20:41:23

0.50.4
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * update requirements.txt
  * lavrukov fab test

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-607: Обновить django rest framework (#160)

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-03-27 15:27:39

0.50.3.2
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-823: Fix username for YcInternalCA

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2018-04-06 20:07:46

0.50.3.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-823: Подключить YandexCLCA

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-825: добавлен фильтр по наличию abc-сервиса и тесты на него
  * CERTOR-825: в тестах параметры передаются отдельным аргументом

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-04-05 13:25:09

0.50.3
---

  * Revert "use cryptography"

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-26 15:39:52

0.50.2
---

  * CrtSession bugfix + internal CA test
  * update\_fields added

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-23 18:34:23

0.50.1
---

  * exception moved
  * use localze
  * use cryptography
  * ca chain refactoring
  * use CrtSession

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-23 13:02:47

0.50.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-798: Не выписываются сертификаты после релиза

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)


 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-23 10:00:34

0.49.7
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * test crl generate bugfix
  * CERTOR-795 default template bugfix

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-796: Добавить новую m2m certificate-host связь
  * CERTOR-796: добавлено копирование старой связи в новую
  * CERTOR-796: теперь миграция состоит в переименовании таблицы и в создании уникального индекса
  * CERTOR-796: убраны упоминания CertificateHost
  * CERTOR-796: поправлена команда создания индекса
  * CERTOR-796: миграция удаляет дублирующиеся пары сертификат-хост
  * CERTOR-796: добавлена проверка в сериализаторе
  * CERTOR-796: добавлена фейковая миграция с удалением джанговых данных

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)


 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-22 14:25:53

0.49.6
---

  * CERTOR-783 Фикс анхолда захолдженых сертов, не успевших доехать в crl

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-20 12:50:36

0.49.5
---

  * CERTOR-783 hold queue bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-19 17:11:51

0.49.4
---

  * CERTOR-783 status changes bugfixes

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-18 10:26:27

0.49.3
---

  * CERTOR-783 hold -> hold bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-17 21:04:10

0.49.2
---

  * CERTOR-783 no revoke expired

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-17 20:27:20

0.49.1
---

  * CERTOR-783 add update\_fields

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-17 19:49:07

0.49.0
---

  * add assert serial\_number test
  * CERTOR-783 update\_status remove + revoke refacktoring

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-17 19:31:58

0.48.5
---

  * CERTOR-755 force up false

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-15 20:59:43

0.48.4
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-755 cvs auth by ssh key

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-785: апнута версия django\_abc\_data, которая по умолчанию не удаляет abc-сервисы
  * CERTOR-785: поправлены старые тесты, падающие из-за Сашиных проверок на serial\_number
  * CERTOR-785: обновлены зависимости

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-781 tests fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-15 20:50:12

0.48.3
---

  * CERTOR-775 diff cmp bugfix
  * CERTOR-770 migrations + revoke dismissed chrontab change
  * CERTOR-781 unique index + serial\_number to upper

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-15 14:51:23

0.48.2
---

  * CERTOR-775 diff bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-14 21:07:06

0.48.1
---

  * CERTOR-766 filter imported vpn-token certs
  * CERTOR-775 save diff to cvs

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-14 20:28:28

0.48.0
---

  * CERTOR-766 vpn-token type added

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-14 19:10:44

0.47.2
---

  * remove old command

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-14 18:07:03

0.47.1
---

  * CERTOR-764 revoke duplicate imdm certificates

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-14 17:56:57

0.47.0
---

  * CERTOR-770 sync -> tasks + revoke task

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-14 16:26:12

0.46.1
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * zombie test fix

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-538: Лучше сохраняю трейсбеки

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * CERTOR-475: Добавил логирование client\_id

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * Правки по админке в CERTOR-719 (#141)

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * reraise и логгирование
  * CERTOR-773: Не выдаётся сертификат для терминаторов
  * CERTOR-773: Переписал цикл покрасивее
  * CERTOR-773: Забытый import

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)


 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-14 15:29:41

0.46.0
---

  * CERTOR-638: Уведомления о протухающих хостовых сертификатах: "умная" логика (#130)

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-03-07 15:30:47

0.45.2
---

  * CERTOR-744 error message in download2
  * CERTOR-767 add new DN format to VALID\_SSL\_DN

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-03-06 15:10:59

0.45.1
---

  * CERTOR-763 check unit in csr with zombie request

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-28 17:33:20

0.45.0
---

  * CERTOR-763 add zombie type

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-28 16:47:52

0.44.4
---

  * CERTOR-762 correct save user for api imdm certificates

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-27 21:51:41

0.44.3
---

  * CERTOR-742 cert type tagging

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-27 17:24:18

0.44.2
---

  * CERTOR-733 tag ordering fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-27 16:35:27

0.44.1
---

  * CERTOR-731 захардкодил country, city и unit

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-21 21:41:21

0.44.0
---

  * CERTOR-733 new cert tag relation

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-21 18:02:22

0.43.0
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-584 InternalTestCA url fix
  * CERTOR-584 remove freezegun from prod req

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-746: разрешить хостовые (rtc) сертификаты для хостов в домене yp.yandex.net

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-16 17:42:51

0.42.2
---

  * CERTOR-584 monitoring fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-13 16:44:40

0.42.1
---

  * CERTOR-584 encoding fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-13 14:58:18

0.42.0
---

  * CERTOR-584 add base synchronizer and http session
  * CERTOR-584 zanzibar synchronizer

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-12 18:17:31

0.41.4
---

  * Revert "CERTOR-718: отображение ссылки на abc-сервис в консоли"
  * CERTOR-718: захардкожен продовый хост ABC

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-02-08 20:23:52

0.41.3
---

  * CERTOR-718: отображение ссылки на abc-сервис в консоли

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-02-08 19:06:11

0.41.2
---

  * CERTOR-718: добавлен проброс abc-сервиса в html-шаблон консоли

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-02-08 18:46:20

0.41.1
---

  * CERTOR-718: команда синхронизации с ABC переименована

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-02-08 17:40:33

0.41.0
---

  * CERTOR-718: Добавить поле "ABC-сервис" для хостовых сертификатов (#122)

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2018-02-08 14:48:46

0.40.2
---

  * CERTOR-728: add is\_active field for tags and filters
  * CERTOR-728 is\_active check in querysets
  * CERTOR-610 add actions
  * CERTOR-610 remove deploy/undeploy actions

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-05 15:03:16

0.40.1
---

  * CERTOR-727 small test fix
  * update cryptography

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-05 14:21:41

0.40.0
---

  * CERTOR-727 add IMDM type

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-01 18:14:08

0.39.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-729: Обновить шаблон client-server
  * CERTOR-731: Перестать забирать старые офферы

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)


 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-02-01 18:08:54

0.38.14
---

  * CERTOR-726: raise if user is not www-data

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-01-26 18:27:26

0.38.13
---

  * CERTOR-717 return invalid ca chain for RC
  * CERTOR-726 cvs up -> checkout && new timestamp error without message

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-01-25 21:32:19

0.38.12
---

  * CERTOR-717 ssl refactoring
  * CERTOR-717 add CA\_NAME constant
  * CERTOR-717 test ca refactoring
  * CERTOR-717 add rc internal ca chain

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-01-22 14:59:27

0.38.11
---

  * CERTOR-715 new allowed host

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2018-01-16 20:25:14

0.38.10
---

  * CERTOR-394: Добавил в текст письма дату истечения сертификата

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2018-01-10 18:47:10

0.38.9
---

  * CERTOR-394: Убрал лишнюю строку из шаблона уведомлений

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2018-01-09 23:17:31

0.38.8
---

  * CERTOR-710: Отправлять копию письма-уведомления о протухающем сертификате на рассылку

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2017-12-29 16:51:34

0.38.7
---

  * CERTOR-394: Поменял шаблон письма

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2017-12-21 17:25:22

0.38.6
---

  * CERTOR-394: Формат уведомлений переделан на html

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2017-12-21 15:11:35

0.38.5
---

  * CERTOR-394: Оповещение о протухающих сертификатах (cron edit)

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2017-12-21 12:59:02

0.38.4
---

  * CERTOR-394: Оповещение о протухающих сертификатах

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2017-12-21 11:58:59

0.38.3
---

  * remove old assessors commands
  * CERTOR-697 priv\_key bugfix
  * CERTOR-701 add new check to client\_server CN
  * CERTOR-701 check common name small fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-12-19 15:57:03

0.38.2
---

  * CERTOR-697: reverse private key relation

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-12-19 00:09:28

0.38.1
---

  * CERTOR-699 decode utf-8 added to BOT response

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-12-15 14:44:10

0.38.0
---

  * CERTOR-629 add migration with permission

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-12-15 12:35:28

0.37.7
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-695 requests error handle (#101)
  * add freezegun to deps
  * CERTOR-695 add test
  * CERTOR-696 hung in requested certs monitoring
  * CERTOR-695 verify fix

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-629: теперь асессорские сертификаты фильтруются ещё и в статус… (#103)

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-11 18:02:42

0.37.6
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-692: Ходить с правильным verify (#99)

 * [Vitaly Sopov](https://staff.yandex-team.ru/Vitaly%20Sopov)

  * CERTOR-629: добавлены локи для синхронизации асессоров с IDM

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-08 16:10:13

0.37.5
---

  * CERTOR-629: сертификаты дополнительно фильтруются по значению ca\_name

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-06 16:57:21

0.37.4
---

  * CERTOR-629: поправлены настройки и взаимодействие с django-idm-api

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-06 14:50:28

0.37.3
---

  * CERTOR-629: поправлены сигнатуры обработчиков сигнала

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-06 13:13:32

0.37.2
---

  * CERTOR-629: мануал по установке сертификата теперь лежит в static, правки по разрешениям на файлы

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-05 17:10:37

0.37.1
---

  * CERTOR-629: мануал по установке сертификата теперь складывается в /var/lib/

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-05 16:46:38

0.37.0
---

  * CERTOR-629: Возможность получать ассессорские сертификаты через IDM (#94)

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-05 16:05:09

0.36.4
---

  * Добавлен скрипт для добавления асессорских ролей в IDM

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-05 15:40:47

0.36.3
---

  * Resubmit

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-04 18:45:46

0.36.2
---

  * CERTOR-629: добавлен необходимый пермишн
  * Поправлена конфигурация логгеров в development-окружении

 [Vitaly Sopov](https://staff.yandex-team.ru/v-sopov@yandex-team.ru) 2017-12-04 17:48:29

0.36.1
---

  * CERTOR-658 admin log user relation fixes (#95)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-12-01 13:14:42

0.36.0
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-674 up just\_updated max age

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-685: Уменьшить стандартный срок действия сертификатов до года
  * Downgrade suds-jurko, release was deleted from pypi

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-30 15:53:55

0.35.0
---

  * CERTOR-614 поправил last-tags ручку (#93)
  * CERTOR-614 bugfix
  * CERTOR-605 fix sync tags flaps (#92)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-11-13 16:07:58

0.34.2
---

  * CERTOR-610 add simple tag sync logging (#91)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-11-09 14:54:28

0.34.1
---

  * CERTOR-644 add users <-> filter relation (#83)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-11-03 19:13:56

0.34.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-668: Перенёс тесты про рендеринг pfx в отдельный файл
  * CERTOR-668: Добавил новый тестовый самоподписывающий CA, который позволяет тестировать асинхронность и подтверждение запросов
  * CERTOR-668: Проверять статус в ручке скачивания
  * Поправил падающий без сети тест
  * Локи на тредах для тестов

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-11-02 11:48:23

0.33.0
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * CERTOR-475: Добавил проверку атрибута, отключил лог-хендлер

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CAUTH-669 qloud monitorings (#90)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-10-27 22:05:13

0.31.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * Починить форму для безопасников
  * Перенёс renderer в отдельный файл

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-20 19:01:33

0.30.0
---

 * [Vladimir Kutyavin](https://staff.yandex-team.ru/Vladimir%20Kutyavin)

  * CERTOR-475: Добавил логирование скоупов

 [Vladimir Kutyavin](https://staff.yandex-team.ru/zivot@yandex-team.ru) 2017-10-20 14:24:35

0.29.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-650: Запретить слеши в мейлах при запросе через CSR и Common Name

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-12 23:10:27

0.28.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-600: Добавил приложение raven в список установленных
  * CERTOR-654: Unhandled exception: The label * is not a valid A-label

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-04 19:05:10

0.27.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-600: Подключить sentry (#81)
  * CERTOR-657: Не удается выставить галку "Managed DNS" для некоторых доменов (#82)

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-655 вывожу количество дней в 400 ручки reissue
  * CERTOR-625 вывожу доступные CA в 400 на /api/certificate/
  * CERTOR-394 get\_aliases
  * CERTOR-656: Сменить ограничение на перевыпуск pc сертификатов на 45 дней

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-10-03 18:28:20

0.26.11
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-652: Падает выписывание сертификата на проверке яндекс.рф (#79)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-09-30 12:21:34

0.26.10
---

  * CERTOR-647: 400 при слишком частом заказе ninja сертов (#78)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-28 15:01:56

0.26.9
---

  * CERTOR-635: fix host\_to\_approve save (#77)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-27 16:26:22

0.26.8
---

  * CERTOR-648 typo fix
  * CERTOR-635: Обновлять name\_servers при обновлении HostToApprove (#76)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-27 15:03:47

0.26.7
---

  * CERTOR-648 check common\_name in validation

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-25 17:25:02

0.26.6
---

  * CERTOR-648 check length of CN (#75)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-25 16:21:22

0.26.5
---

  * CERTOR-614: фиксы для Бориса (#74)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-14 21:52:14

0.26.4
---

  * CERTOR-615: приоритет тегов (#73)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-14 17:59:19

0.26.3
---

  * CERTOR-614 сонсоле фикс

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-14 16:37:33

0.26.2
---

  * Избавился от проблем в CRT (#72)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-14 16:16:42

0.26.1
---

  * CERTOR-614 cvs upload fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-14 13:01:13

0.26.0
---

  * CERTOR-614: ручка выгрузки (#67)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-14 12:16:49

0.25.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-642: Сломали валидацию для Ботика (#71)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-09-12 16:47:54

0.24.0
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-640: Вернуть возможность запроса через globalsign (#69)

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * TOOLSUP-22338: Обновление словаря валидных CN (#70)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-09-11 15:07:06

0.23.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-637: Временно разрешил всем запрос хостовых сертификатов через CSR (#68)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-09-10 12:45:53

0.22.1
---

  * private key generation fix
  * download urls tests

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-08 19:23:49

0.22.0
---

  * CERTOR-630: Тамстампы действий (#65)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-08 14:46:48

0.21.1
---

  * Поправил автогенерацию тестового CA
  * CERTOR-624: Доработки ручки перевыпуска клиентских похостовых сертификатов (#63)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-09-05 17:27:03

0.21.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-580: raise вместо return, чтобы ретраить попытку выписать сертификат на Certum
  * CERTOR-603: Вернул возможность заказать PC-сертификат через CSR, запретил заказ через Common Name
  * CERTOR-620: Проверил, что ручка /api/reissue сохранила старую логику работы. Ручка может принимать как принимать CSR, так и не принимать его

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-18 17:52:37

0.20.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-603: Генерирую csr с помощью cryptography, теперь все тесты проходят
  * CERTOR-603: Поправил ворнинг, время должно быть timezone-aware
  * CERTOR-603: Добавил django-extensions, чтобы получить shell\_plus
  * CERTOR-603: Никаких True по умолчанию. Сделал список и безопасные умолчания
  * CERTOR-603: Удалил код про mobile сертификаты, перенёс mobile сертификат в inactive
  * CERTOR-603: Поправил небезопасный код
  * CERTOR-603: Закрыл возможность заказа через CSR кроме четырёх типов: LINUX\_TOKEN, CLIENT\_SERVER, ETOKEN, MOBVPN
  * CERTOR-603: Валидирую common\_name для всех типов сертификатов, которые пользователь может заказать сам
  * CERTOR-603: Переименовал SELF\_REQUEST\_TYPES в PUBLIC\_REQUEST\_TYPES
  * CERTOR-603: Вынес константы на уровень модуля, стал передавать в create\_raw\_csr словарь
  * CERTOR-603: Документировал mixin
  * CERTOR-603: Обновил список доступных полей
  * CERTOR-603: Завернул свойства в property, чтобы тесты проходили в любом порядке

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-16 20:25:39

0.19.1
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-596: Поправил ошибку в SSLAuthMiddleware

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-14 23:40:43

0.19.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-603: Расширил доступтимый pc common name regexp подчёрком, потому что он бывает, а без него падают тесты
  * CERTOR-603: Перенёс TestCA и поменял gitignore
  * CERTOR-596: Отдаю те же данные при перевыпуске, что и при выпуске
  * CERTOR-596: Починил subject
  * CERTOR-596: Отдаю больше деталей при ошибке
  * CERTOR-596: Убрал проверку OAuth-токенов при походе с клиентским сертификатом

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-14 20:09:58

0.18.0
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-596: Ручка перевыпуска снова пятисотит (#60)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-10 23:49:31

0.17.3
---

  * CERTOR-612: filename  fix + no start commit in no changes (#57)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-08-08 18:38:10

0.17.2
---

  * CERTOR-613: fetching is\_robot flag (#56)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-08-08 17:08:33

0.17.1
---

  * CERTOR-612: Добавить сверку по максимальному количеству изменений (#55)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-08-08 15:43:23

0.17
---

  * CERTOR-605: Поправил пару мини багов в выгрузке (#54)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-08-07 14:16:18

0.16
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-604: Плохая настройка CORS (#53)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-08-03 19:01:07

0.15
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-596: Ручка перевыпуска, тестинг (#52)
  * CERTOR-596: Поправил fabfile

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-27 14:14:17

0.14
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * CERTOR-596: Ручка перевыпуска пятисотит (#51)

 [Alexey Boriskin (uruz)](https://staff.yandex-team.ru/uruz@yandex-team.ru) 2017-07-26 10:28:55

0.13
---

  * CERTOR-581: Ещё один фикс (#50)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-07-17 17:25:34

0.12
---

  * CERTOR-581: Фикс SyntaxError (#49)
  * fab release не обнуляет минорные версии (#48)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-07-17 16:57:05

0.11.28
---

  * CERTOR-548: Фикс для GlobalSign (#46)
  * CERTOR-581: Возможность перевыпуска rc-сертификатов (#37)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-07-17 14:15:10

0.10.28
---

 * [Alexey Boriskin](https://staff.yandex-team.ru/Alexey%20Boriskin)

  * TOOLS-2113: Доступы: Унести пользовательские обращения в tools@ (#44)

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * Команда fab release (#43)
  * CERTOR-548: Уменьшить срок жизни сертификатов получаемых qloud через api до 6 месяцев (#36)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-07-13 15:14:42

0.9.28
---

  * CERTOR-591: Сделать код 201 в NinjaView (#45)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-07-11 18:42:11

0.9.27
---

  * CERTOR-590 Убрана дублирующаяся база slave2, connect\_timeout default->15, CONN\_MAX\_AGE 1800->300 (#42)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-07-06 17:01:45

0.9.26
---

  * CERTOR-590 204 вместо 200 в REPLICATED\_FORCE\_MASTER\_COOKIE\_STATUS\_CODES (#41)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-07-04 20:57:36

0.9.25
---

  * CERTOR-590 Закрытие соединений на postfork, uwsgitop в requierments (#40)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-07-04 20:00:12

0.9.24
---

  * CERTOR-590 stats, harakiri, max-requests в uwsgi.ini (#39)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-07-04 18:37:51

0.9.23
---

  * CERTOR-470 Отображать в Сертификаторе сертификаты на e-токенах (#35)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-06-19 19:00:00

0.9.22
---

  * CERTOR-578 Вернуть логику для трафик-тима (#34)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-06-01 19:06:45

0.9.21
---

  * very small fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-31 18:03:31

0.9.20
---

  * CERTOR-572 Фикс ошибки, ссылка на тестинг стартрека с тестовой админки (#33)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-05-31 16:20:43

0.9.19
---

  * CERTOR-572 Пятисотит админка ApproveRequest (#32)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-05-31 14:48:47

0.9.18
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-574 проставляю куки после post запросов

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * CERTOR-552 Починил тестинг GlobalSign (#31)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-05-31 14:13:29

0.9.17
---

  * CERTOR-570 Поправил выдачу сертификатов с не активным типом

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-22 23:10:27

0.9.16
---

  * CERTOR-568 Добавить домен qloud-vm.yandex.net к разрешенным для запроса rc-server (#30)

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-05-22 16:55:27

0.9.15
---

  * Refactoring (#29)

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-18 20:01:09

0.9.14
---

  * ninja fix 5

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-18 16:02:39

0.9.13
---

  * ninja fix
  * ninja fix 2
  * ninja fix 3
  * ninja fix 4

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-18 15:51:28

0.9.12
---

  * ninja fix
  * ninja fix 2

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-17 21:02:10

0.9.11
---

  * ninja fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-17 18:35:24

0.9.10
---

  * uatraits bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-12 19:22:31

0.9.9
---

  * Перешел с самосборного uatraits на ids

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-12 19:10:00

0.9.8
---

  * CERTOR-562 Поправил письмо асессорам

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-12 16:50:30

0.9.7
---

  * CERTOR-565 Сделал возможность фильтрации нескольких type

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-12 15:56:14

0.9.6
---

  * Удалил django-vanilla-views
  * Добавил логгирование user\_agent

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-12 15:14:59

0.9.5
---

  * CERTOR-564 Починил хелп консоли

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-05-03 14:32:52

0.9.4
---

  * Фикс ошибки при approve/reject запроса

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-04-26 19:03:44

0.9.3
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * Не инстанцирую ca при запросе серта

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * CERTOR-561 Закрывать тикеты при подтверждении сертификата через админку

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-04-25 20:21:54

0.9.2
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * Удалил сабмодуль и gulp файлы

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * CERTOR-559 Проставлять компоненту при создании тикета

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-04-25 16:29:20

0.9.1
---

  * unicode error fix + 500 page fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-04-20 12:10:15

0.9.0
---

  * Вынес использование uatraits в утилс
  * Перенес def views в начало

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-04-19 21:07:12

0.8.30
---

  * CAUTH-560 Поправил логику удаления приватных ключей

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-04-17 17:01:01

0.8.29
---

  * CERTOR-558 Вернул возможность фильтрации по нескольким юзерам

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-04-13 16:15:17

0.8.28
---

  * CERTOR-557 Добавил хост для rc-server

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-04-12 21:06:53

0.8.27
---

  * CERTOR-515 lower serial name in noc json

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-04-12 13:53:57

0.8.26
---

  * CERTOR-553 поправил разбор кодов из dns

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-04-07 18:12:48

0.8.25
---

  * CERTOR-553 Поправил длину кода

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-04-05 13:04:25

0.8.24
---

  * CERTOR-551 assessor management command fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-04-04 14:25:13

0.8.23
---

  * small fixes
  * admin fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-31 23:47:14

0.8.22
---

  * small bugfixes

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-31 23:12:30

0.8.21
---

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * permission fix

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * Фикс ошибки про CRT\_NOTIFICATIONS\_TEST\_BCC

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-03-31 13:22:32

0.8.20
---

  * notification fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-30 20:55:15

0.8.19
---

 * [Ilya Peterov](https://staff.yandex-team.ru/Ilya%20Peterov)

  * CERTOR-537 Небольшой фикс в админке

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * CERTOR-537 issue\_key -> st\_issue\_key

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-30 18:14:52

0.8.18
---

  * Хранится issue.key вместо issue.id, ссылки в админке, запросивший в наблюдателях

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-03-30 15:39:29

0.8.17
---

  * Добавлены test\_ca и .cache в .gitignore
  * Команды fab test (SQLite) и fab fulltest (MySQL)
  * При заказе сертификата возвращать ID тикета в ST

 [Ilya Peterov](https://staff.yandex-team.ru/ipeterov@yandex-team.ru) 2017-03-29 21:46:13

0.8.16
---

 * [Eldar T. Zaitov](https://staff.yandex-team.ru/Eldar%20T.%20Zaitov)

  * Reject/Approve requests via admin panel

 * [Alexander Lavrukov](https://staff.yandex-team.ru/Alexander%20Lavrukov)

  * approve request admin refuctor + up requirements

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-22 17:37:12

0.8.15
---

  * CERTOR-546 transaction bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-14 18:35:53

0.8.14
---

  * CERTOR-546 Поправил баг с unhold

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-13 16:39:01

0.8.13
---

  * CERTOR-545 typo fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-09 23:54:57

0.8.12
---

  * add update to update\_fields and show hold in console

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-07 15:51:05

0.8.11
---

  * CERTOR-542 Исправил баг с терминаторами

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-07 14:08:23

0.8.10
---

  * certum revoke bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-06 15:47:23

0.8.9
---

  * CERTOR-541 Изменил правила выдачи асессорам

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-03 21:27:39

0.8.8
---

  * CERTOR-538 exception refactoring

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-03 19:10:20

0.8.7
---

  * CERTOR-538 order parameters refactoring
  * CERTOR-538 request header refactoring
  * CERTOR-538 requestor info refactoring
  * CERTOR-538 san entries refactoring
  * CERTOR-538 order option refactoring
  * CERTOR-538 verify domains refactoring
  * CERTOR-538 approvers refactoring
  * CERTOR-538 suds client refactoring
  * CERTOR-538 create certum suds client
  * CERTOR-538 request header refactoring
  * CERTOR-538 creating suds arguments refactoring
  * CERTOR-538 suds calls refactoring
  * CERTOR-538 global sign suds client
  * CERTOR-538 подтянул зависимости
  * CERTOR-538 order refactoring
  * CERTOR-538 bugfixes
  * CERTOR-538 remove with statement

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-02 23:27:06

0.8.4
---

  * CERTOR-535 asesssor command fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-03-02 16:55:35

0.8.3
---

  * mini bugfixes
  * CERTOR-535 Поправил письмо асессорам

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-02-28 19:51:00

0.8.2
---

  * crt -> crt

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-02-27 21:06:14

0.8.1
---

  * small fix
  * CERTOR-464 add hold capability
  * CERTOR-464 mini model fix
  * CERTOR-464 permission fix 500 -> 403

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-02-27 15:31:36

0.7.11
---

  * small bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-02-16 14:36:01

0.7.10
---

  * CERTOR-534 переписал ninja

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-02-15 18:56:48

0.7.9
---

  * Add new top level domain yandex.co.il

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-02-01 14:21:23

0.7.8
---

  * check txt bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-27 19:17:32

0.7.7
---

  * добавил com.am + вернул check\_txt

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-27 16:47:20

0.7.6
---

  * fix check\_txt bug

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-27 15:35:45

0.7.5
---

  * send\_notifications bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-26 21:23:30

0.7.4
---

  * can\_autovalidate\_fqdn for InternalCA + small fixes

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-26 19:14:29

0.7.3
---

  * Поправил логи
  * удалил check\_if\_certs\_deployed с разрешения ursus

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-26 17:33:08

0.7.2
---

  * CERTOR-416 убрал логи пингов, поправил логи проверки на деплой, починил бэкап приватных ключей

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-26 15:40:49

0.7.1
---

  * CERTOR-416 validation host bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-26 13:46:05

0.7.0
---

  * CERTOR-416 Прикрутил ylog

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-26 00:01:13

0.6.12
---

  * Вернул обратно случайно удаленные зависимости
  * CERTOR-416 Изменил и отсортировал зависимости
  * CERTOR-416 Рефакторинги, что бы коммит с логами был легче
  * CERTOR-416 Рефакторинги: перенес ca\_chains в etc

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-24 23:45:05

0.6.11
---

  * certum errors handling bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-23 23:57:17

0.6.10
---

  * CERTOR-528 response bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-23 22:59:53

0.6.9
---

  * CERTOR-368 удалил точку
  * CERTOR-531 Временно вернул vanilla

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-20 23:46:55

0.6.7
---

  * CERTOR-528 remove vanilla views
  * CERTOR-528 Убрал "секретный уровень Яндекса"
  * CERTOR-528 Удалил оставшиеся упоминания Сертификатора
  * CERTOR-528 validation ca\_name

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-20 18:53:02

0.6.5
---

  * CERTOR-528 Удалил smailik
  * CERTOR-528 module crt -> crt

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-19 15:58:31

0.6.4
---

  * CERTOR-527 Запускаю коммит в cvs сразу после синхронизации
  * CERTOR-528 remove migrations
  * CERTOR-528 up django to 1.7
  * CERTOR-528 up to django 1.8
  * CERTOR-528 удалил ненужные зависимости
  * CERTOR-528 small fixes

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-18 23:03:41

0.5.1
---

  * CERTOR-522 Поднял таймаут cvs + remove mptt

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-16 20:21:38

0.5
---

  * Поправил отправку писем на pki-test и поправил темплейт письма о ошибке
  * CERTOR-521 base command refactoring
  * CERTOR-519 Добавил тэги
  * CERTOR-521 Добавил синхронизацию с staff-api
  * CERTOR-524 Отображаю типы в консоли
  * CERTOR-522 Выгружаю тэги в cvs

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2017-01-16 15:01:52

0.4.27
---

  * CERTOR-520 small fix
  * CERTOR-520 Вернул ninja в get\_serializer

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-23 14:41:19

0.4.26
---

  * CERTOR-520 Certum CA bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-22 19:08:20

0.4.25
---

  * CERTOR-520 Добавил тесты, запретил запросы на неактивные типы, добавил админку для типов
  * CERTOR-520 host certificate request bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-22 18:33:37

0.4.24
---

  * CERTOR-520 Вынес тип сертификата в отдельную таблицу

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-22 03:57:16

0.4.23
---

  * CERTOR-520 Вынес имена типов в enum

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-21 19:53:16

0.4.22
---

  * CERTOR-518 newhire request bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-21 04:06:04

0.4.21
---

  * CERTOR-518 User as custom model

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-21 02:33:25

0.4.20
---

  * datasources renaming

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-21 02:33:25

0.4.19
---

  * CERTOR-518 Окончательно разнес все по сериалайзерам
  * add tests

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-20 18:17:44

0.4.18
---

  * CERTOR-518 Поправил requester в писмах от host сертов

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-19 15:57:03

0.4.17
---

  * CERTOR-518 Поправил 500 в /api/user/ на 404

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-19 15:26:57

0.4.16
---

  * CERTOR-518 user field is not required

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-16 13:38:54

0.4.15
---

  * CERTOR-518 action table User in model

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-16 03:49:38

0.4.14
---

  * CERTOR-518 user now is User model

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-15 19:02:59

0.4.13
---

  * CERTOR-518 requester console bugfix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-15 14:36:45

0.4.12
---

  * CERTOR-518 requester is foreign key

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-15 00:53:21

0.4.11
---

  * CERTOR-518 Переименовал поле requester для более простой миграции

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-14 18:45:53

0.4.10
---

  * CERTOR-488 small refactoring
  * remove invalid tests
  * CERTOR-518 Удалил модуль staff
  * CERTOR-518 remove UserFields model

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-14 17:36:49

0.4.9
---

  * CERTOR-505 Поправил проверку cn в запросе rc-server
  * CERTOR-488 Добавил тип сертификата client-server

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-09 19:30:43

0.4.8-3
---

  * CERTOR-505 Увеличил длину serial\_number до 64

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-07 18:26:54

0.4.8-2
---

  * CERTOR-505 Генерирую csr на своей стороне

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-07 13:46:04

0.4.8-1
---

  * CERTOT-505 add ninja certs to supported

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-06 13:50:10

0.4.8
---

  * CERTOR-505 Новый внутренний УЦ для нужд rc

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-06 13:05:00

0.4.7-2
---

  * CERTOR-453 временно вернул поле hash\_algorithm

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-02 15:11:07

0.4.7-1
---

  * CERTOR-496 Добавил недостающих типов в internal CA

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-01 20:14:51

0.4.7
---

  * SIGNER-496 Удалил smime
  * CERTOR-453 Удалил hash\_algorithm (всегда sha2)
  * CERTOR-496 Удалил code-sign
  * CERTOR-511 Команда для выдачи ассессорских сертификатов
  * CERTOR-510 Отправляю письма на спец рассылки
  * CERTOR-513 Поменял урл для idm

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-12-01 18:03:39

0.4.6-4
---

  * SIGNER-39 Отдаю новый серт в ответе

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-11-16 16:38:09

0.4.6-3
---

  * CERTOR-506 Проверяем только CNы

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-11-15 21:51:30

0.4.6-2
---

  * CERTOR-508 CERTOR-509 Поправил пятисотку и страницу пятисоток

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-11-15 15:34:01

0.4.6-1
---

  * CERTOR-506 Для удобства тестирования сделал исключение для bombastic@

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-11-14 16:03:00

0.4.6
---

  * CERTOR-506 Ручка для обновления pc сертов

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-11-14 14:58:45

0.4.5-2
---

  * CERTOR-486 new maillist

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-11-10 16:00:54

0.4.5-1
---

  * CERTOR-486 fix hosts to native

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-11-02 18:10:29

0.4.4
---

  * CERTOR-486 ещё фиксы по изменившимся требованиям

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-11-02 17:14:50

0.4.0
---

  * CERTOR-486 Добавил подтверждение СИБ для host-сертов

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-10-30 19:07:37

0.3.60
---

  * CERTOR-504 Добавил таймауты в обращениях к staff-api

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-10-19 16:05:40

0.3.58
---

  * CERTOR-490 Добавил валидацию домена yandex.com.ge

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-09-05 16:17:14

0.3.57
---

  * CERTOR-482: Добавил новый тип assessor и ручку для него

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-07-26 19:11:09

0.3.56
---

  * CERTOR-478 Вместо MySQLdb.OperationError прилетает джанговый

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-07-05 12:10:08

0.3.55
---

  * CERTOR-474 validate fix

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-06-24 21:18:55

0.3.54
---

  * CERTOR-472 Добавил сервера в config.ovpn
  * CERTOR-473 Поправил баг с проверкой username/password
  * CERTOR-474 Добавил сравнение cn и username

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-06-24 19:28:40

0.3.53
---

  * CERTOR-467 Удалил одноразовую команду
  * CERTOR-464 Ручка revoke от Internal CA возвращает описание ошибки в reason
  * CERTOR-471 Поправил баг с невозможностью выдачи серта без pc\_serial\_number

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-06-20 18:34:26

0.3.52
---

  * CERTOR-463 Добавил таск для отзыва старых сертификатов устройств
  * CERTOR-468 Добавил отзыв smime сертификатов
  * Рефакторинг: вынес общее из issue() в BaseCA + убрал класс http
  * CERTOR-463 Временно отключил таску с отзывом перевыпущенных

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-06-16 23:38:38

0.3.51
---

  * Поправил проблему с выводом

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-06-15 18:14:30

0.3.50
---

  * CERTOR-467 Поправил логику определения инвентарника
  * CERTOR-464 Добавил вывод таблицы случайных сертов в режиме ярости

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-06-15 16:25:30

0.3.49
---

  * Апнул версии cryptography и uwsgi для сборки
  * Поправил баг с неактивностью второго слейва
  * CERTOR-464 Добавил периодическую команду для отзыва сертификатов уволенных сотрудников
  * CERTOR-464 Добавил режим полной ярости в команду для отзыва сертов уволенных

 [Alexander Lavrukov](https://staff.yandex-team.ru/lavrukov@yandex-team.ru) 2016-06-09 21:47:06

0.3.48
---

  * CERTOR-460 Ходим в балансер LDAP

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-05-24 12:24:46

0.3.47
---

  * CERTOR-459 Вырезаем символ CR из сертификатов

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-05-24 11:52:40

0.3.46
---

  * CERTOR-447 Link to config.ovpn

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-05-23 15:58:13

0.3.45
---

  * CERTOR-447 config.ovpn

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-05-23 15:45:32

0.3.44
---

  * CERTOR-457 IDN-кодирование при создании CSR

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-04-18 11:07:22

0.3.43
---

  * CERTOR-455 Увеличиваем backlog uwsgi до 1024

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-30 15:01:35

0.3.42
---

  * CERTOR-447 Возможность скачать ca.pem и tls.key

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-29 16:40:11

0.3.41
---

  * CERTOR-452 Принимаем OAuth-токены в новом формате

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-23 13:16:42

0.3.40
---

  * Отзыв сертификата из InternalTesrtCA понарошку

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-17 15:56:59

0.3.39
---

  * CERTOR-447 Пофикшено падение при отображении mobvpn-сертификата

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-17 14:35:32

0.3.38
---

  * Логируем необработанные исключения

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-17 14:22:37

0.3.37
---

  * CERTOR-450 Починены мониторинги (на самом деле)

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-15 16:56:42

0.3.36
---

  * CERTOR-450 Починены мониторинги

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-15 16:24:41

0.3.35
---

  * CERTOR-450 Активация-деактивация конфига nginx

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-15 11:56:50

0.3.34
---

  * CERTOR-450 Конфиги nginx уехали в админский пакет

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-14 15:04:23

0.3.33
---

  * CERTOR-451 Тестовый конфиг поправлен для /ping

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-14 14:29:26

0.3.32
---

  * CERTOR-450 Обновлён конфиг nginx для нового продакшна
  * CERTOR-451 Ручка /ping для балансера
  * CERTOR-441 Мониторинги monrun

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-14 14:20:37

0.3.31
---

  * CERTOR-447 Сертификаты mobvpn

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-03 18:12:52

0.3.30
---

  * Избавляемся от зависимости от python-apt

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-02 16:37:47

0.3.29
---

  * TOOLSADMIN-2895 Синхронизируемся со стаффом в тестинге тоже

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-02 14:28:16

0.3.28
---

  * TOOLSADMIN-2895 Синхронизируемся со стаффом в тестинге тоже

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-02 14:28:06

0.3.27
---

  * TOOLSADMIN-2895 Добавил smailik в зависимости

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-02 14:18:16

0.3.26
---

  * TOOLSADMIN-2895 SUPPRESS\_DATASOURCES\_WARNING

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-02 14:02:51

0.3.25
---

  * TOOLSADMIN-2895 Активируем логирование раньше импорта датасорсов

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-02 13:45:05

0.3.24
---

  * CERTOR-439 Исправлена ручка /api/user/<login>.json, пишущая в базу на get

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-01 19:02:53

0.3.23
---

  * CERTOR-439 Более удачная проверка datasources

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-01 16:32:36

0.3.22
---

  * CERTOR-446 Выпилил динамические группы, потому что Управлятор
  * CERTOR-435 winadmin@ -> @cert-update
  * CERTOR-439 Django replicated

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-03-01 16:22:40

0.3.21
---

  * CERTOR-445 Исправлен тупейший фильтр по хостам

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-02-19 17:09:17

0.3.20
---

  * TOOLSADMIN-2895 Переменные database\_host и database\_port в datasources

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-02-18 15:39:05

0.3.19
---

  * Version bump

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-02-18 14:11:50

0.3.18
---

  * Version bump

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-02-18 13:34:53

0.3.17
---

  * CERTOR-438 Лочим фоновые таски с помощью zookeeper
  * CERTOR-438 Дополнительные хосты zookeeper для девелопмента

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-02-16 12:08:09

0.3.16
---

  * $ssl\_client\_s\_dn в логе nginx

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-26 13:39:04

0.3.15
---

  * CERTOR-440 Приватные ключи в отдельной таблице

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-26 13:28:19

0.3.14
---

  * CERTOR-437 Выпиливание \_get\_username\_and\_requester()
  * CERTOR-434 Django permissions вместо захардкоженных проверок прав

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-25 16:00:57

0.3.13
---

  * Выбор тестового внутреннего CA в тестинге

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-21 12:23:33

0.3.12
---

  * username в ninja-форме конвертируем в lowercase

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-20 18:48:39

0.3.11
---

  * Обновление django-yauth для включения OAuth

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-20 17:03:12

0.3.10
---

  * CERTOR-412 Переименован файл monrun-конфига

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-20 16:14:54

0.3.9
---

  * CERTOR-406 Заказ сертификатов для токенов
  * SECTASK-246 Починка сертификатов PDAS

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-20 15:47:01

0.3.8
---

  * CERTOR-412 Переходим на staff-api и больше не закладываемся на изменяемые урлы подразделений

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-19 18:47:21

0.3.7
---

  * CERTOR-432 Разрешаем  ответственным за хосты отзывать сертификаты во всех УЦ

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-15 14:42:46

0.3.6
---

  * CERTOR-431 Отзывать сертификаты ходим в тот же порт, что и заказывать #2

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-14 19:18:32

0.3.5
---

  * CERTOR-431 Отзывать сертификаты ходим в тот же порт, что и заказывать

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-14 19:09:35

0.3.4
---

  * CERTOR-431 Разные CRL урлы внутреннего CA для тестинга и продакшна

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-14 18:42:00

0.3.3
---

  * test

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-14 17:21:21

0.3.2
---

  * CERTOR-431 Тестовый сертификатор смотрит в тестовый внутренний zanzibar

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-14 17:05:04

0.3.1
---

  * CERTOR-422 Выпилен rq, django-rq, redis и весь оставшийся от них мёртвый код
  * CERTOR-423 suds-jurko с локального pypi
  * CERTOR-421 Перешел на django-idm-api, оптимизировал конфиг nginx
  * CERTOR-420 Выпилил logster и graphitesend
  * CERTOR-426 Код api/views.py разнесён по модулям
  * CERTOR-427 Выпилен django-debug-toolbar
  * CERTOR-426 Разумный выбор рендерера по заголовку Accept
  * CERTOR-419 Дефолтные фильтры без патчинга внешних либ
  * CERTOR-415 Избавился от lego, старых шаблонов и compressor'а
  * CERTOR-410 Нормальная сборка, почти нет debian-зависимостей, запуск через uwsgi
  * CERTOR-411 Переезд настроек на granular\_settings
  * CERTOR-411 Конфиг nginx для девелопмент и секретики в datasources
  * CERTOR-417 Рефакторинг жирных модулей
  * CERTOR-431 С тестинга и девелопмента ходим в dev.bot.yandex-team.ru

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2016-01-12 15:41:22

0.2.151
---

  * CERTOR-428 В crt-allowed-cas.pem должна быть вся цепочка

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-24 19:24:16

0.2.150
---

  * Bump

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-24 19:03:17

0.2.149
---

  * CERTOR-428 Subject нового сертификата Управлятора в конфиге nginx

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-24 18:59:38

0.2.146
---

  * CERTOR-429 Отдельный nginx-локейшн для /dostup/, оптимизация конфига

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-24 17:32:45

0.2.145
---

  * CERTOR-394 Отправляем уведомления только по задеплоенным хостовым сертификатам

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-22 13:28:12

0.2.144
---

  * CERTOR-418 Передаём в Certum GMT-дату при запросе сертификата

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-21 19:39:31

0.2.143
---

  * CERTOR-312 Исправлена кривая логика проверки установленности сертификата
  * CERTOR-394 Интервал в 2 дня между нотификациями о протухающем сертификате

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-17 16:36:54

0.2.142
---

  * Обновление DN у клиентского сертификата cacique.yandex.net
  * CERTOR-405 yandextrafik.com.tr

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-15 17:13:03

0.2.141
---

  * CERTOR-394 Уведомляем о протухающих botik-сертификатах

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-14 12:55:10

0.2.140
---

  * Всегда разрешаем скачать сертификат тому, кто его заказал

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-11 15:28:13

0.2.139
---

  * CERTOR-387 Retry on database errors in issue\_certificate.py

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-10 12:24:33

0.2.138
---

  * CERTOR-380 Починил отзыв сертификатов GlobalSign

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-04 15:01:38

0.2.137
---

  * CERTOR-380 Используем MSSL API для заказа сертификатов в GlobalSign

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-03 18:43:33

0.2.136
---

  * Хватит заниматься в postinst всякой фигнёй

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-02 17:49:57

0.2.135
---

  * CERTOR-388 Правильный код продукта для EV-cертификата SHA256

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-02 17:45:09

0.2.134
---

  * CERTOR-389 Ссылка на вики-форму в каждом уведомлении

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-02 16:01:50

0.2.133
---

  * CERTOR-389 Отсылка к вики-форме, а не к рассылке pki@

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-02 15:00:59

0.2.132
---

  * CERTOR-392 Cross-сертификат Certum Trusted Network

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-02 13:08:42

0.2.131
---

  * CERTOR-391 Разрешать SHA1-сертификаты в CERTUM до декабря 2016

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-12-02 12:28:00

0.2.130
---

  * CERTOR-380 Всё-таки syncdb --migrate

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-11-13 23:40:18

0.2.129
---

  * CERTOR-380 Длина поля ca\_name=30

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-11-13 23:01:04

0.2.128
---

  * CERTOR-380 Пофикшена обратная несовместимость

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-11-12 22:29:46

0.2.127
---

  * CERTOR-383 Разрешаем линуксоидам перевыпускать сертификат за 90 дней до истечения

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-11-12 19:24:47

0.2.126
---

  * CERTOR-380 Поддержка УЦ GlobalSign для хостовых сертификатов

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-11-12 14:29:14

0.2.125
---

  * CERTOR-381 Серийный номер в админской консольке

 [Andrey Bulgakov](https://staff.yandex-team.ru/abulgakov@yandex-team.ru) 2015-11-12 12:03:18

0.2.124
---

  * Забыл, что subject сертификата надо ещё и в nginx конфиге прописать.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-09-25 13:09:25

0.2.123
---

  * Добавил доступ по сертификату для пользователя zomb-watching-dead, по просьбе anton-k. CERTOR-378.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-09-24 15:29:42

0.2.122
---

  * Переключились на LDAP хост steady.yandex.ru и теперь это можно переопределить в настройках /etc/yandex/yandex-directory/secure\_settings.py, указав LDAP\_HOST.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-09-18 15:55:33

0.2.121
---

  * Заменил \r\n на \n в яндексовых цепочках сертификатов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-08-31 11:52:57

0.2.120
---

  * Добавил дополнительный логгинг, чтобы разобраться с CERTOR-371.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-08-25 18:31:55

0.2.119
---

  * Используем для SHA256 правильную цепочку сертификатов. CERTOR-370.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-08-25 15:13:20

0.2.118
---

  * Снова разрешаем перезапрашивать linux сертификаты только если они истекают меньше чем через 31 день.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-08-19 17:03:32

0.2.117
---

  * Теперь человек может перевыпустить любой сертификат для своего устройства, независимо от того, когда у него истекает срок действия текущего сертификата. Все старые сертификаты на это устройство, тут же отзываются. CERTOR-363
  * Исправлено сравнение логинов, когда решаем есть у человека доступ к сертификату или нет. Теперь при сравнении не учитывается регистр логина.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-08-08 07:24:34

0.2.116
---

  * Теперь emailAddress не обязательно должен присутствовать в CSR. CERTOR-360.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-07-21 18:03:09

0.2.115
---

  * Исправлена проблема с заказом certum сертификатов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-07-15 23:54:32

0.2.114
---

  * SHA2 сертификаты выдаются сроком на два года.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-07-15 11:44:23

0.2.113
---

  * Теперь сертификаты с SHA2 используют код 972 и выдаются на два года.
  * Добавлен логгинг проблем с аутентификацией в ldap.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-07-14 19:10:05

0.2.112
---

  * Поправлено еще одно место, где мы ходим в LDAP.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-06-04 18:51:09

0.2.111
---

  * Используем TLS при обращении к LDAP.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-06-04 16:08:14

0.2.110
---

  * Добавил Тараса Иващенко (oxdef) в список супер-пользователей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-06-01 14:53:06

0.2.109
---

  * Ограничиваем SHA1 сертификаты сроком до 2015-12-25. CERTOR-355.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-05-15 12:48:34

0.2.108
---

  * Поменялись Allowed Origin разработческих машинок голема. CERTOR-346.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-04-16 17:47:04

0.2.107
---

  * Сделал для сертификатов типа botik поле hash\_algorithm опциональным.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-03-27 13:43:30

0.2.106
---

  * Лишние поля в CertificateSerializer были помечены, как readonly и больше не показываются в форме запроса, которую генерит django rest framework.
  * Добавлено поле hash\_algorithm и соответствующая опция в API. CERTOR-348.
  * Добавлен HSTS заголовок. CERTOR-337.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-03-20 15:24:43

0.2.105
---

  * Фильтры по pc\_xxx полям. CERTOR-344

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-03-11 18:38:31

0.2.104
---

  * Добавлено ограничение — не более одного ninja сертификата за 5 минут.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-02-06 17:49:35

0.2.103
---

  * Включаем email уведомления от Certum для code sign сертификатов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-01-16 15:19:43

0.2.102
---

  * И еще один фикс.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-01-14 18:48:28

0.2.101
---

  * Еще один фикс.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-01-14 18:11:53

0.2.100
---

  * Разрешаем поле request для code sign сертификатов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-01-14 18:02:04

0.2.99
---

  * Еще одна правка Meta.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-01-14 17:52:54

0.2.98
---

  * Небольшие доработки Meta в классе CodeSignCertSerializer.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-01-14 17:42:50

0.2.97
---

  * Добавил забытую строчку в models.py.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-01-14 17:26:22

0.2.96
---

  * Возможность запрашивать сертификаты для code sign.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-01-14 17:17:08

0.2.95
---

  * Не обрабатываем запросы внутренних сертификатов асинхронно. CERTOR-339.
  * Дополнительно логгируем ошибки от виндового CA при отзыве сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-01-12 15:20:25

0.2.94
---

  * Добавил Германию и Берлин в определялку полей для сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2015-01-06 20:31:46

0.2.93
---

  * Отправляем уведомление о том, что хостовый сертификат готов, только тогда, когда он действительно готов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-24 20:18:32

0.2.92
---

  * Небольшой фикс BCC.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-22 13:52:46

0.2.91
---

  * Когда делаем BCC мне, то добавляем к subject оригинальный email.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-22 12:50:28

0.2.90
---

  * Включаем уведомления о протухающих linux сертификатах.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-22 12:12:37

0.2.89
---

  * Небольшой фикс bcc.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-22 11:46:34

0.2.88
---

  * Добавляем меня в BCC для всех исходящих email уведомлений.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-22 11:28:04

0.2.87
---

  * Еще один фикс нотифаек.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-19 16:53:47

0.2.86
---

  * Исправлена ошибка в send\_notfications\_to\_people.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-19 16:11:04

0.2.85
---

  * Исправлена команда send\_notifications\_to\_people.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-19 15:48:51

0.2.84
---

  * Реализован прототип уведомлялки линукс-пользователей о протухающих сертификатах.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-17 18:17:22

0.2.83
---

  * Реализована обработка ошибок в форме отзыва сертификата через консольку. CERTOR-332.
  * Сразу после сабмита ninja формы, кнопка дисейблится, исключая повторные попытки запросить сертификат. CERTOR-329.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-12 16:29:40

0.2.82
---

  * Оказывается restframework не позволяет использовать знак '-' в названии формата сериализации. Исправили iphone-exchange на iphoneexchange.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-12 13:00:08

0.2.81
---

  * Убрали зависимость от внешнего jquery на странице запроса сертификатов для линуксоидов.
  * Исправляем определение smime полей для сотрудников в Хельсинки.
  * Для всех ninja сертификатов subject теперь содержит только CommonName. А если включен Exchange, то еще OU=mobile.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-12 12:45:31

0.2.80
---

  * Добавил забытый CA темплейт для эксперимернта с Subj.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-11 19:02:56

0.2.79
---

  * Включил pe4kin в эксперимент с простым Subject.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-11 17:59:47

0.2.78
---

  * Костылик, чтобы для меня генерился Subject с одним только CN.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-11 17:37:39

0.2.77
---

  * Исправлена генерация Exchange профиля для iOS. CERTOR-330.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-11 16:36:22

0.2.76
---

  * Откатил назад зависимость от tablib.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-11 12:27:44

0.2.75
---

  * Включаем в цепочку для внутренних сертификатов YandexInternalRootCA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-11 12:19:42

0.2.74
---

  * Autofocus на поле 'логин' в морде Ninja. CERTOR-321.
  * Responsive дизайн для Ninja интерфейса. CERTOR-321.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-10 17:25:38

0.2.73
---

  * Для сертификатов, заказанных через Ninja, показываем в консоли поля с описанием платформы. CERTOR-324.
  * Исправлена 400 ошибка при обращении к домену ninja.yandex-team.ru. CERTOR-325.
  * Исправлена ошибка, когда в CSR указан закодированный в punicode домен. CERTOR-327.
  * Исправлена ошибка связанная с запросом EV сертификатов. CERTOR-326.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-12-10 15:50:58

0.2.72
---

  * Забыл добавить common-name ботика в конфиг самого сертификатора.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-11-25 16:24:28

0.2.71
---

  * Позволяем proxy-real00.yandex.net ходить в API с SSL сертификатом (по просьбе thebits).

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-11-20 17:06:31

0.2.70
---

  * Исправлена генерация PDAS сертификатов для работы с Exchange.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-11-13 13:56:06

0.2.69
---

  * Исправлено определение платформы в новой Ninja.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-11-12 14:57:47

0.2.68
---

  * Загружаем пакетики в unstable.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-11-06 15:57:16

0.2.67
---

  * Исправлена ошибка когда Golem возвращает не 200 при проверки ответственности за хосты.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-11-05 18:57:17

0.2.66
---

  * Rebuild

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-11-05 16:40:59

0.2.65
---

  * Отключено ограничение на количество wildcard в серитфикате.
  * Для всех польских сертификатов кроме EV теперь используем код продукта 973. По их словам он теперь позволяет и milti-wildcard и скоро будет до 200 хостов в SAN разрешать.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-11-05 10:59:24

0.2.64
---

  * Теперь ninja-интерфейс будет работать на доменах mobcert.yandex.net, mobcert.yandex-team.ru и ninja.yandex-team.ru.
  * Теперь в ninja view используется uatraits вместо устаревшего phonedetect.
  * Исправлено определение момента, когда сертификат был удален с хостов. CERTOR-312.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-16 12:55:39

0.2.63
---

  * Передаем HTTP\_HOST при скачиваении ninja сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-10 17:40:55

0.2.62
---

  * Исправлена аутентификация на странице /ninja/.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-10 17:25:22

0.2.61
---

  * Добавлена возможность аутентифицироваться доменными логином и паролем, передав их в заголовках запроса. Исправлено скачивание сертификата после логина на странице /ninja/.
  * Добавлен логгинг в код определения мобильной платформы.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-10 17:15:06

0.2.60
---

  * Исправлена ошибка, связанная с попыткой выписывать нинзевые сертификаты через тестовый CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-10 14:20:40

0.2.59
---

  * Улучшана форма запроса PDAS сертификатов. CERTOR-308, CERTOR-309, CERTOR-310.
    Кроме того, теперь эта страница отдается на другом IP адресе, в который резолвится mobcert.yandex.net. CERTOR-311.


 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-10 12:16:53

0.2.58
---

  * Исправлена ошибка, из-за которой не валидировались русскоязычные домены. Надо было кодировать их в punicode прежде чем обращаться к dig. CERTOR-305.
  * Записываем в истории действий над сертификатом момент, когда тот был отозван из-за того, что не удалось подтвердить домен.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-10 10:51:25

0.2.57
---

  * Все обращения к times.now испралены на timezone.now.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-02 16:17:13

0.2.56
---

  * Теперь Django будет сохранять все даты в UTC, и API отображать тоже в UTC.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-02 11:54:57

0.2.55
---

  * Добавлена проверка HTTP кода ошибки в ответе голема при проверке прав владения хостом. CERTOR-299

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-01 19:12:04

0.2.54
---

  * Поправлена ручка API, выдающая информацию по нескольким пользователям.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-01 17:05:33

0.2.53
---

  * Теперь API поддерживает запрос сертификатов для перечисленных через запятую логинов. CERTOR-230.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-10-01 16:20:43

0.2.52
---

  * Исправлена команда, проверяющая установлен ли сертификат на хостах. Кроме того, она теперь умеет показывать, удалось ли вообще проверить какой там на хостах сертификат.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-09-26 19:25:37

0.2.51
---

  * Используем более новый twiggy goodies.
  * И снова изменена логика работы костыля для валидации украинских доменов.
  * Исправлено использование голема в дев среде.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-09-23 13:44:29

0.2.50
---

  * Небольшие дополнения для mobcert.yandex.net.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-09-19 19:20:13

0.2.49
---

  * В Nginx конфиг добавлена секция для того, чтобы обслуживать mobcert.yandex.net.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-09-19 19:03:38

0.2.48
---

  * Добавлено пояснение что к чему, в ninja-форму.
  * Добавлена генерация профилей для iphone и запоминение типа устройства при запросе сертификата через ninja-интерфейс.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-09-19 17:44:24

0.2.47
---

  * Исправлена ошибка в Download view PFX.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-09-19 14:04:49

0.2.46
---

  * Исправлена логика подтверждения украинских доменов. CERTOR-292.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-09-18 15:45:43

0.2.45
---

  * Теперь API возвращает 403 вместо 400, при попытке скачать сертификат, если ты не ответственный за хосты или не являешься его владельцем.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-09-18 13:20:41

0.2.44
---

  * Исправлена логика выставления кодов валидации для yandex.ua домена.
  * Исправлена логика сохранения объектов Certificate, из за которой при сохранении давно выданных сертификатов с update\_fields='has\_problems', все хосты с которыми сертификат связан, помечались как провалидированные.
  * All logic from ninja was transferred. Now API handle /dowload/ accepts optional 'filename' and 'with\_chain=0' arguments.
  * Добавлен шаблон для ninja и зависимость от lxml.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-09-18 05:00:40

0.2.43
---

  * Теперь все сертификаты запрашиваемые через Certum, должны протухнуть к 2016 году.
  * Добавлена вьюшка, которая будет заменять Ninja, но пока она только девайс определять умеет.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-09-11 17:11:46

0.2.42
---

  * Исправлено отображение дат. Теперь все даты, приходящие из API, считаются в UTC, а отображаются в локальной таймзоне. CERTOR-290.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-26 18:16:57

0.2.41
---

  * Теперь все проблемы с сертификатами, которые были разрешены, помечаются автоматически, как исчезнувшие.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-25 16:53:04

0.2.40
---

  * Добавлена проверка сертификатов на возможные проблемы. Описания проблем можно смотреть в админской консольке. CERTOR-270.
  * Django обновлена до 1.6.6, а так же некоторые другие зависимости.
  * Добавлена новая модель для фиксации проблем с сертификатами.
  * В девелоперском CA выписываем smime с возможностью clientAuth.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-22 16:22:17

0.2.39
---

  * Реализован костыль для последовательной валидации доменов yandex.com.ua и yandex.ua. CERTOR-286.
  * Исправлены тесты.
  * Исправлен шаблон карточки сертификата.
  * В API и на карточке сертификата в консоли, теперь показывается поле issued. CERTOR-288.
  * Переехали на jisp 0.3.2

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-19 17:07:44

0.2.38
---

  * Исправлена ошибка из-за которой не отрабатывала команда check\_txt.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-14 15:19:20

0.2.37
---

  * Исправлена проблема с пустым действием в истории валидации. Кроме того, теперь к действию validated-because-cert-issued, привязан сертификат, который был выписан.
  * В команде check\_txt\_records отныне проверяем только те хосты, для которых были выставлены коды валидации.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-14 13:15:19

0.2.36
---

  * Помечаем все домены, относящиеся к выданному сертификату, как провалидированные.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-13 19:40:49

0.2.35
---

  * Сохраняем в лог все коды валидации, которые находили на домене. CERTOR-258.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-13 19:07:37

0.2.34
---

  * Исправлена процедура бэкапа приватных ключей. А удаление теперь происходит через 10 дней, а не через 9. CERTOR-282.
  * Логгируем имя пользователя, который совершает каждый веб-запрос. CERTOR-283.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-13 13:00:11

0.2.33
---

  * Теперь в консоли, в списке доменов видно, какой в настоящий момент ожидает валидации. Логика по определению необходимости валидации перенесена из view в модель HostToApprove.
  * Добавлено поле, в котором будет фиксироваться дата выдачи сертификата. CERTOR-260.
  * Теперь сертификатор уведомляет о том, что хостовый сертификат готов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-08 14:37:01

0.2.32
---

  * Добавлен логгинг в функцию отсылки уведомлений, чтобы отследить их в рамках тикета CERTOR-275.
  * Теперь мы раз в день проверяем, какие сертификаты висят в validation больше 2 суток, и отзываем их. CERTOR-247.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-07 16:23:56

0.2.31
---

  * Переход на исправленную twiggy-goodies 0.3.1

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-06 12:59:18

0.2.30
---

  * Обновил версию twiggy goodies. Теперь записи лога должны быть в UTC.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-06 12:41:02

0.2.29
---

  * Появилось магическое разворачивание некоторых запросов в консоли. CERTOR-276.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-08-01 15:46:33

0.2.28
---

  * Исправлена ошибка, из-за которой урлы на скачивание сертификата были относительные, и скачивание не работало в големе. CERTOR-272.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-30 09:56:33

0.2.27
---

  * Больше логгинга в логике проверки владения сертификатом. CERTOR-272.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-29 17:42:38

0.2.26
---

  * Добавлен дополнительный логгинг при скачивании сертификата. CERTOR-272.
  * Поправлен конфиг логгинга, чтобы в лог попадали 500 ошибки.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-29 17:18:00

0.2.25
---

  * Поправлены права суперпользователя в /console/.
  * Добавлено общее поле status.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-28 19:16:19

0.2.24
---

  * Поправлены 500 ошибки.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-28 18:59:19

0.2.23
---

  * Исправлены поля, которые сериализуются в JSON.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-28 18:42:57

0.2.22
---

  * Теперь для разных типов сертификатов API отдает разный набор полей. Возможная обратная несовместимость!

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-28 17:36:15

0.2.21
---

  * Добавлен тест на разные сериализаторы для разных типов сертификатов.
  * Теперь API отдает список хостов одного сертификата. CERTOR-264.
  * Теперь в консоль позволяет фильтровать сертификаты по названию CA. CERTOR-259.
  * Обновлен .gitignore.
  * Добавлен конфиг для gulp.
  * Добавлен package.json.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-25 17:36:00

0.2.20
---

  * Теперь порядок хостов в SAN должен быть такой, какой задавался изначально. CERTOR-263.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-23 15:10:26

0.2.19
---

  * Добавлены миграции базы, чтобы переключиться на CertificateHost.
  * Исправлен тест test\_host\_with\_csr\_if\_admin.
  * Добавлена модель CertificateHost и проведена подготовка к переключению на нее.
  * Добавлена команда upload\_release, для повторной загрузки пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-23 14:07:37

0.2.18
---

  * Добавлена документация по компиляции jisp исходников. Реализована сборка JS кода через gulp.
  * Поправлена неверная подсказка про валидирущиеся домены, когда сертификат больше не находится в стадии валидации. CERTOR-257.
  * Angular.js контролы переписаны на jisp.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-22 17:37:04

0.2.17
---

  * Еще более правильные таблички.
  * Красивые таблички везде и всюду.
  * Изменен порядок данных в истории валидации домена. Теперь сначала идут более свежие данные.
  * Теперь в истории валидации хоста, common\_name является ссылкой на описание сертификата. CERTOR-253.
  * Добавлена страница админки, на которой можно проследить когда и какие коды добавлялись и валидировались. А так же даты теперь отображаются по-человечески. CERTOR-252.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-03 20:32:29

0.2.16
---

  * Добавлены страницы админки в которых можно смотреть статус валидации доменов. CERTOR-248.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-02 18:24:01

0.2.15
---

  * Добавлена обработка ошибок при создании клиентского соединения с Certum. CERTOR-249.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-02 13:12:39

0.2.14
---

  * Теперь API отдает информацию по доменам, которые требуют подтверждения для получения сертификата. И эта информация отображается в админской консоли. CERTOR-248.
  * Проверяем, что код есть в DNS только если код действительно есть.
  * Убран лишний return, из-за которого в случае ошибки с одним доменом не происходило подтверждение других доменов командой check\_txt\_records.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-07-01 15:42:37

0.2.13
---

  * Теперь для заказа внутренних хостовых сертификатов не нужно быть владельцем хостов. CERTOR-246.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-06-20 13:49:47

0.2.12
---

  * Подключаем debug\_toolbar опционально, только если такой пакет установлен.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-06-18 15:23:03

0.2.11
---

  * Теперь CSR проверяется на обязательное наличие Common Name и Email. CERTOR-243.
  * Теперь на 500 странице показываем человеческое сообщение об ошибке с кодом по которому можно отследить произошедшее в логах. CERTOR-244.
  * Подключен django-debug-toolbar.
  * Обновлены версии зависимостей, в деве добавлен debug-toolbar.
  * Отзыв внутренних сертификатов включен.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-06-18 14:27:31

0.2.10
---

  * Теперь сертификатор показывает текст последней ошибки, случившейся с сертификатом и показывает его в консоли. CERTOR-225.
  * Откачен назад реальный отзыв внутренних сертификатов. CERTOR-241.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-06-09 14:09:13

0.2.9
---

  * Отслеживаем время, когда был удален приватный ключ, и отдаем его в API в поле priv\_key\_deleted\_at. CERTOR-238.
  * Добавлена страница /changelog/, поправлены шаблоны консоли и консольного help.
  * Сделана поддержка удаления внутренних сертификатов. CERTOR-193.
  * Исправлено отображение ошибок в API, связанных с обязательными полями.
  * Выдаем человечесоке сообщение об ошибке в случае, когда запрашивают pfx, а приватного ключа уже нет в базе. CERTOR-93.
  * Логгируем ошибки от get\_smime\_fields только если это не HTTP 404. CERTOR-237.
  * Переключился на дефолтный pip-tools.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-06-05 09:37:00

0.2.8
---

  * Для mobile сертификатов теперь всегда OU=MOBILE. CERTOR-123.
  * Добавлена команда send\_notifications, рассылающая уведомлялки про истекающие сертификаты. CERTOR-96.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-05-23 16:43:32

0.2.7
---

  * Фильтруем по хостам только если они были заданы.
  * Используем специальный индекс, чтобы искать по нескольким хостам и учитывать wildcard. CERTOR-169.
  * Показываем сообщение линуксоидам, у которых сертификат истекает еще не скоро. CERTOR-231.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-05-21 15:13:47

0.2.6
---

  * Исправлена ошибка, из-за которой данные о сертификате не показывались в консоли.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-05-14 16:36:32

0.2.5
---

  * Добавлена справка по языку запросов в консоли. CERTOR-234.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-05-13 12:53:23

0.2.4
---

  * Используем django\_extensions во всех окружениях.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-05-12 17:29:16

0.2.3
---

  * Обновлены некоторые зависимости.
  * Теперь любой, у кого есть can\_revoke\_any\_certificate, может отзывать сертификаты. CERTOR-228.
  * Исправлен тест, который давно фейлился при валидации полей при запросе сертификата.
  * Добавлена кнопка отзыва сертификата из консоли. CERTOR-228.
  * Доступ к консоли ограничен кругом тех, кто имеет право 'core.can\_use\_console'. CERTOR-233.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-05-12 17:09:56

0.2.2
---

  * Исправлена версия в debian/changelog.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-24 15:12:49

0.2.1
---

  * Конфиг nginx поправлен, чтобы пускать в API Управлятор.
  * Добавлена настройка ALLOWED\_HOSTS.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-24 12:37:16

0.2.0
---

  * Переключился на Django 1.6.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-23 18:08:08

0.1.297
---

  * Обновил версию upravlyator-django-api, на работающую с Django 1.6.
  * Подключен upravlyator-django-api.
  * Убрал pip-tools из зависимостей.
  * Удален лишний djangorestframework из зависимостей.
  * Из файлов с зависимостями убраны куски wheels.
  * Один тест исправлен.
  * Полное обновление файлов с зависимостями.
  * Переключился на Django 1.6 и более новый nosedjango из GitHub.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-23 18:08:08

0.1.296
---

  * Обновлены и зафиксированы зависимости.
  * Исправлена 500 на /request/. CERTOR-229.
  * Подчищены все места, где использовался logging.py.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-15 20:03:32

0.1.295
---

  * Добавлена возможность получить новый linux-pc сертификат взамен истекающего старого. CERTOR-209.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-09 12:49:52

0.1.294
---

  * Убрал сертификаты из debian/install.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-03 21:25:11

0.1.293
---

  * Заменены l2, l4 и evca. CERTOR-227.
  * Произведен рефакторинг того, как определяются пути к промежуточным сертификатам и цепочкам. Удалены лишние сертификаты.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-03 18:23:54

0.1.292
---

  * Добавлена команда revoke\_lost\_certificates.
  * Добавлена команда fab coverage и конфиг nginx, чтобы смотреть coverage в деве.
  * В девелоперские зависимости добавлен coverage.
  * Добавлены хелперы для fabric.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-04-02 17:06:00

0.1.291
---

  * Приводим логин сотрудника в lowercase при формировании common\_name. CERTOR-224.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-17 11:24:05

0.1.290
---

  * Добавил пару дополнительных колонок в отчет о подвисших сертификатах. CERTOR-124.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-13 15:21:39

0.1.289
---

  * Поправлена проверка деплоймента сертификата в команде show\_lost\_certum\_certificates.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-11 17:41:35

0.1.288
---

  * Команда show\_lost\_certum\_certificates теперь выдает csv и проверяет, задеплоен ли сертификат на какие-нибудь хосты.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-11 17:23:25

0.1.287
---

  * Поправлено имя используемого show\_lost\_certum\_... CA для продакшена.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-07 15:46:04

0.1.286
---

  * Обновлены зависимости, там новый suds, который должен более правильно работать с кодировками.
  * Не показываем сертификат, если знаем такой order\_id.
  * Добавлена команда для отображения 'потерянных' запросов на сертификат. CERTOR-124.
  * В консоли добавлена новая колонка ca\_name. CERTOR-218.
  * Бэкапим только приватные ключи SMIME сертификатов, а удаляем все через 9 дней. CERTOR-186.
  * Теперь дни и месяцы в бэкапе приватных ключей дополняются нулем. CERTOR-186.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-03-07 15:36:50

0.1.285
---

  * Поправил доку по фильтрации результатов API.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-20 13:26:48

0.1.284
---

  * Снова делаем статику ссылками для разработки.
  * Добавлены колонки username, requester.
  * Улучшено отображение результатов поиска.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-20 12:52:06

0.1.283
---

  * Исправлено раздражающее мигание результатов поиска в консоли.
  * Показываем в консоли 50 результатов за раз.
  * Теперь API выдает первыми наиболее свежие сертификаты.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-20 12:18:01

0.1.282
---

  * Удалено правило, удаляющее статику при сборке пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-20 12:02:20

0.1.281
---

  * Исправлена компрессия статики для консоли.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-20 11:20:21

0.1.280
---

  * Исправлена опечатка в шаблоне cool-console.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-20 10:45:33

0.1.279
---

  * Добавил django-compressor в зависимости.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-20 00:22:41

0.1.278
---

  * Обновил зависимости, добавив django-filter со своими патчами.
  * Добавлены стили для консольки.
  * Добавлено сохранение запроса в URL.
  * Подключен rest\_framework\_chain и крутые фильтры по common\_name.
  * Показываем все поля сертификата в консольке.
  * Страница для просмотра данных о сертификате WIP.
  * Консоль без стилей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-19 20:50:53

0.1.277
---

  * Добавлены команды backup\_priv\_keys и delete\_priv\_keys. Запускаются по крону в 7 утра. CERTOR-186.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-17 16:50:27

0.1.276
---

  * Временно убрал сборку с использованием wheels.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-13 16:01:16

0.1.275
---

  * Теперь все внутренние сертификаты выдаются синхронно. CERTOR-210.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-13 13:23:24

0.1.274
---

  * Исправлена ошибка, из-за которой нельзя было получить сертификат на *.multiship.ru. CERTOR-215.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-11 18:22:30

0.1.273
---

  * Теперь используем шаблон yaUser-iMDM для сертификатов типа mobile.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-02-04 10:40:10

0.1.272
---

  * Добавлена обработка для специального типа сертификатов — mobile. CERTOR-210.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-31 16:54:48

0.1.271
---

  * Исправлена ошибка, при которой дублируется записи в /hosts/to-approve/, если несколько сертификатов с одним TLD висят в состоянии validation. CERTOR-212.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-30 13:57:13

0.1.270
---

  * Добавлен тест test\_dont\_show\_duplicate\_codes, чтобы проверять CERTOR-212. Но он пока почему-то не работает.
  * Добавлена возможность игнорировать некоторые коды ошибок от certum. Пока только 'Domain Has already been verified'. CERTOR-211.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-30 01:13:11

0.1.269
---

  * Отключено автоматическое вычисление статуса, когда сертификат переведен в revoking.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-23 21:52:55

0.1.268
---

  * Забыл еще про один статус - requested.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-23 11:05:19

0.1.267
---

  * Добавлена проверка того, что сертификат находится в состоянии validation на момент открытия страницы /request/smime/. CERTOR-208.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-23 10:30:54

0.1.266
---

  * JS код поправлен так, чтобы работать после минификации.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-23 01:37:21

0.1.265
---

  * Поправлен путь к \_smime.js.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-23 01:20:58

0.1.264
---

  * Восстановлена проверка бранча при сборке пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-23 00:46:32

0.1.263
---

  * Пересборка с нормальной статикой.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-23 00:10:06

0.1.262
---

  * Используем ca\_name по-умолчанию при запросе SMIME.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-22 23:54:15

0.1.261
---

  * Добавлена view для получения smime сертификата. Попутно исправлено расширение скачиваемых pfx файлов. CERTOR-208.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-22 23:49:56

0.1.260
---

  * Исправлена работа страницы для запроса сертификатов линуксоидами. CERTOR-198.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-22 13:37:29

0.1.259
---

  * Собираем продакшн env с использованием wheels.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-21 15:15:19

0.1.258
---

  * Исправлена 500 при запросе доступа, и ошибка с логгингом в check\_txt\_record. CERTOR-207.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-21 15:10:08

0.1.257
---

  * Test build.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-21 14:36:02

0.1.256
---

  * Ограничение на один единственный wildcard теперь работает только для Certum. CERTOR-206.
  * Теперь внутренние сертификаты могут переходить в состояние 'revoking' и ожидать отзыва.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-21 12:04:06

0.1.255
---

  * Для pc и linux-pc сертификатов достаем имя настоящего сотрудника из common\_name. CERTOR-199.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-20 15:56:56

0.1.254
---

  * Исправлена ошибка с отсутствующим логгером. CERTOR-205.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-17 17:36:59

0.1.253
---

  * Исправлены ошибки в логгинге, из за которых в записях оставались данные предыдущих запросов. CERTOR-143.
  * С наступающим Новым Годом!
  * Теперь, при запросе сертификата, можно разделять хосты пробелами. CERTOR-195.
  * Правки Nginx конфига, чтобы загонять недоменщиков в счастье. CERTOR-196.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2014-01-15 15:56:16

0.1.252
---

  * Добавлен текст на страницу /migration/. CERTOR-188.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 16:38:19

0.1.251
---

  * Исправлена валидация common\_name для linux-pc. CERTOR-192.
  * Теперь при запросе host сертификата проверяем, что все его хосты входят в домены, для которых поддерживается автоматическое подтверждение. CERTOR-159.
  * Больше не выдаем в TestCA синхронно, так как это ломает тесты.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 16:21:18

0.1.250
---

  * Исправлена 500 ошибка при попытке отзыва внутреннего сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 12:32:33

0.1.249
---

  * Исправлена выдача хостовых сертификатов во внутреннем CA. CERTOR-189.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 12:02:51

0.1.248
---

  * Добавил common\_name в список полей LinuxPC.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 01:40:43

0.1.247
---

  * Ликвидировано еще несколько косяков с linux-pc.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 01:28:37

0.1.246
---

  * Используем шаблон WebServer-auto для выдачи внутренних host сертификатов без подтверждения. CERTOR-189.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 01:25:03

0.1.245
---

  * Исправлена внесенная предыдущим релизом ошибка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 01:14:04

0.1.244
---

  * В шапку /request/ добавлено отображение логина. CERTOR-190.
  * Позволяем избранным запрашивать linux-pc сертификаты через API. CERTOR-185.
  * Исправлен конфиг nginx. CERTOR-188.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-24 01:02:43

0.1.243
---

  * Добавлена страница /migration/ и редирект на нее.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-23 20:55:07

0.1.242
---

  * Поправлено скачивание последнего выданного сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-20 20:37:18

0.1.241
---

  * Не показываем в списке устройства, для которых есть валидный сертификат, выданный хелпдеском.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-20 20:23:23

0.1.240
---

  * Теперь сертификат для linux пользователей не выпускается заново, а мы даем скачать заказанный прежде.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-20 19:57:00

0.1.239
---

  * Исправлен косяк с отображением ворнинга для нелинуксоидов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-20 16:47:46

0.1.238
---

  * Теперь линуксоиды могут перезапрашивать сертификаты. CERTOR-183.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-20 15:54:19

0.1.237
---

  * Таймаут соединения с  Certum увеличен с 90 секунд до 300.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-20 15:04:26

0.1.236
---

  * Исправлена обработка ошибок от голема. CERTOR-182.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-20 13:29:31

0.1.235
---

  * Показываем код валидации лишь спустя пять минут после того, как он был получен. CERTOR-180.
  * Исправлена ошибка, из-за которой мы могли слишком быстро убирать коды валидации из DNS. CERTOR-179.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-19 01:03:46

0.1.234
---

  * Больше не считаем ошибку номер 1 от цертума критической. CERTOR-178.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-18 22:45:14

0.1.233
---

  * Команда resurrect\_certs поправлена, чтобы работать с сертами сфейлившимися в процессе валидации.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-18 21:24:00

0.1.232
---

  * Исправлен DN сервера sachem.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-18 21:19:16

0.1.231
---

  * Исправлена ошибка, когда хостовый сертификат заказывается с использованием CSR в котором нет SAN. CERTOR-177.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-18 18:18:41

0.1.230
---

  * Исправлен вывод списка хостов в API. CERTOR-176.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-18 16:23:46

0.1.229
---

  * Добавлена команда resurrect\_certs. CERTOR-175.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-18 16:15:39

0.1.228
---

  * Теперь для SMIME и HOST сертификатов используются отдельные
    сериализаторы. Команда issue\_cetificates запущенная из под дебага
    выдает traceback. CERTOR-170.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-18 14:48:10

0.1.227
---

  * Поправлена битая ссыла. CERTOR-173

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-17 17:59:21

0.1.226
---

  * На страницу /request/ добавлены ссылы на недавние сертификаты. CERTOR-173.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-17 17:28:52

0.1.225
---

  * Теперь считаем все ошибки типа SSLError, некритическими. CERTOR-148.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-16 20:41:53

0.1.224
---

  * Расширен список сложных доменов, что должно решить проблему выдачи сертификата для yandex-team.com.tr.
  * Поправлен скрипт для сборки production virtualenv.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-13 15:49:00

0.1.223
---

  * Requirements were updated.
  * RedirectLogger исправлен, чтобы корректно записывать сообщения, содержащие фигурные скобки.
  * Добавлена настройка логгера suds чтобы он использовал twiggy.
  * Добавлена fabric команда для компиляции зависимостей.
  * Исправлена команда bootstrap.sh.
  * correct intermediateCA bundles processing

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-13 11:58:50

0.1.222
---

  * Поправлен импорт.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-11 18:02:07

0.1.221
---

  * Исправлена опечатка в команде check\_txt\_records.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-11 17:07:22

0.1.220
---

  * Теперь верификация домена происходит не хождением по HTTP, а вызовом метода verifyDomain. CERTOR-167.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-11 16:57:18

0.1.219
---

  * Исправлена ошибка в логике подачи кодов для валидации в машинку Олега Горохова.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-10 16:48:03

0.1.218
---

  * В имени файла для ответа цертума используем дату и время. CERTOR-167.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-10 16:01:03

0.1.217
---

  * При сохранении ответа от цертум о валидации домена, сохраняем валидированный код.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-10 15:51:32

0.1.216
---

  * Если не смогли определить страну или город, используем RU и Moscow. CERTOR-166.
  * Убрана установка npm install.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-10 15:36:52

0.1.215
---

  * Исправлена опечатка в check\_txt\_record.
  * Добавлено автоматическое создание тикета в кондукторе, после сборки пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-10 14:38:23

0.1.214
---

  * Изменена ссылка на рассылку pki@yandex-team.ru, на странице заказа для линуксоидов. CERTOR-153.
  * В уведомление об ошибке добавлена ссыла на рассылку pki@yandex-team.ru, а так же заголовок Reply-To для всех уведомлений. CERTOR-150.
  * На входе, все хосты перекодировать из punicode в unicode. CERTOR-161.
  * Update install
    copy EVCA bundle to cert dir.

  * specific CA bundle for EV certs

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-10 10:48:58

0.1.213
---

  * Исправлена отправка данных в graphite. CERTOR-163.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-06 23:13:28

0.1.212
---

  * Улучшен процесс подтверждения доменов. CERTOR-162.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-06 22:46:31

0.1.211
---

  * Добавлен production-bootstrap.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-06 21:24:10

0.1.210
---

  * Добавлена команда show\_host\_history.
  * Исправлена команда check\_txt\_records, чтобы не было ошибки для HostToApprove, к которому не привязано сертификата.
  * Девелоперский reloader теперь выводит дату и время.
  * Обновлены зависимости, rest\_framework теперь берется из моей ветке на гитхабе.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-06 20:30:02

0.1.209
---

  * Исправлена опечатка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-05 18:14:48

0.1.208
---

  * Поправлены сабжекты сертификатов для animals.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-05 18:08:25

0.1.207
---

  * Добавлено сообщение об ошибке, при попытка запросить хостовый сертификат через внутренний CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-05 16:54:39

0.1.206
---

  * Данные о сотруднике теперь кэшируются на 30 минут, а не на сутки. CERTOR-158.
  * Не кэшируем неполную информацию о сотрудники, когда он еще не заведен на staff. CERTOR-158.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-05 14:13:18

0.1.205
---

  * Длинна поля pc\_mac увеличена до 1000 символов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-04 16:56:13

0.1.204
---

  * Теперь ручка /api/user/login.json отдает 404 и сообщение об ошибке, если сотрудник с указанным логином не найден. CERTOR-155.
  * Исправлен парсинг common\_name из сертификата и CSR. CERTOR-154.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-04 16:40:38

0.1.203
---

  * Исправлена последствия добавления XML рендерера.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-04 14:44:01

0.1.202
---

  * Добавлена ручка, выдающая список хостов, для которых настроена автоматическая валидация. Кроме того, теперь все API ручки по-умолчанию, поддерживают и XML и JSON. CERTOR-140
  * Добавлено сохранения кода продукта в отдельном поле лога. CERTOR-142.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-04 12:43:20

0.1.201
---

  * Разрешаем запрашивать pc сертификаты всем хелпдескам. CERTOR-149.
  * Исправлен шаблон виндового CA для хостовых сертификатов.
  * Добавлена функция для определения ответственных за хост.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-03 16:33:05

0.1.200
---

  * Добавлен продакшн subject от винадминов. CERTOR-146.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-12-02 20:53:05

0.1.199
---

  * Функции get\_name\_servers и get\_aliases поправлены так, чтобы работать с кириллическими доменами. CERTOR-138.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-27 16:51:24

0.1.198
---

  * Исправлены ошибки, связанные с кодировками кириллических доменов. CERTOR-136.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-27 14:44:23

0.1.197
---

  * Исправлена команда check\_if\_certs\_deployed, чтобы обновлять данные сертификатов с помощью update. CERTOR-137.
  * Добавлена процедура пометки сертификатов, как протухших. CERTOR-127.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-26 17:42:57

0.1.196
---

  * Для botik сертификатов поле 'type' убрано из prohibited.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-25 14:33:45

0.1.195
---

  * Исправлена выдача SMIME сертификатов. Во всех обращениях к Certum, позиционные параметры заменены на именованые. CERTOR-126.
  * Улучшено логирование ошибок от Certum. Теперь логгируется и оригинальный traceback. CERTUM-128.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-23 00:20:39

0.1.194
---

  * Сделаны настройки, чтобы пускать робота-ботика в сертификатор по 444 порту.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-22 16:04:17

0.1.193
---

  * В модель UserFields добавлено поле city.
  * Показываем инвентарный номер устройств на странице запроса линукс-сертификатов. CERTOR-132.
  * Из VALID\_SSL\_DN убран golem. CERTOR-133.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-22 15:46:34

0.1.192
---

  * Исправлена ошибка при отзыве сертификата в certum. CERTOR-135.
  * Теперь для сертификатов типа botik common\_name обязателен, а остальные поля запрещены.
  * Добавлен еще один тип сертификатов botik. CERTOR-129.
  * В локальные настройки добавлен URL CRL тестового CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-22 10:49:46

0.1.191
---

  * Добавлена цепочка тестового InternalCA.
  * Добавлено профилирование http запросов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-21 18:07:04

0.1.190
---

  * Отдельные цепочки для проверки сертификатов польского и нашего CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-21 14:34:21

0.1.189
---

  * Исправлена опечатка в имени пользователя winadmin.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-21 14:01:59

0.1.188
---

  * Указана кодировка для settings.production.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-21 07:22:59

0.1.187
---

  * Исправлена функция определения подразделения. Теперь она работает и для Воложа.
  * Теперь pc сертфикаты могут быть созданы без использования внешнего CSR, а лишь указанием common\_name. CERTOR-131.
  * Исаправлен subject сертификата винадминов.
  * В тестовый конфиг добавил свой сертификат.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-21 00:14:55

0.1.186
---

  * Убран излишне подробный логгинг смены значения атрибутов сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-20 18:48:30

0.1.185
---

  * В тестовый конфиг добавлен subject тестового сертификата винадминов.
  * Тестовый nginx конфиг настроен, чтобы требовать аутентификации сертификатом только на 444 порту.
  * Добавлен комментарий по поводу common\_name голема.
  * Количество джанговских воркеров увеличено до 20.
  * В конфиг добавлен сабжект сертификата helpdesk.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-20 18:35:43

0.1.184
---

  * Показываем десктопы в списке устройств на которые можно запрашивать linux-сертификаты. CERTOR-130.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-20 00:39:38

0.1.183
---

  * Исправлена проблема eukho, из-за которой протухший сертификат не давал запросить новый. CERTOR-125.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-20 00:26:51

0.1.182
---

  * Отключил генерацию lego при сборке пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-12 18:51:12

0.1.181
---

  * Добавлена возможность задавать пароль при скачивании pfx. Теперь для линуксовых пользователей генерится случайный пароль. CERTOR-122.
  * Разрешаем запрашивать сертификаты вручную пользователям BSD. CERTOR-122.
  * Показываем линуксоидам только те устройства, на которые у них еще нет сертификатов. CERTOR-122.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-12 17:13:59

0.1.180
---

  * Сделал used\_template поле read-only.
  * Не репортим багу через email, для mobile сертификатов. CERTOR-123

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-11 21:38:45

0.1.179
---

  * Добавлен openssl шаблон mobile. CERTOR-123

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-11 21:32:28

0.1.178
---

  * Добавлен новый тип сертификата mobile. CERTOR-123.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-11 21:03:10

0.1.177
---

  * Понавставлял flock для всех кроновых задач.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-09 00:52:11

0.1.176
---

  * Задача по проверке факта установки сертификатов на сервера убрана из крона, до лучших времен.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-09 00:05:52

0.1.175
---

  * Еще более продвинутый логгинг изменения атрибутов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 21:34:32

0.1.174
---

  * Сохраняем stack trace в поле stack.
  * Логируем плохие ответы от Certum, когда в них есть error коды.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 21:21:49

0.1.173
---

  * Логируем traceback и id сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 20:54:15

0.1.172
---

  * И снова исправлена еще одна тупая опечатка. Всё таки надо постараться покрыть всё это уг тестами.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 20:27:21

0.1.171
---

  * Добавлен код для логирования изменения атрибутов status и request\_id.
  * Исправлена еще одна опечатка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 20:07:18

0.1.170
---

  * Исправлена опечатка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 18:26:55

0.1.169
---

  * Исправлена еще одна ошибка в обращении к suds клиенту.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 17:54:06

0.1.168
---

  * Добавлены упущенные импорты.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 17:34:30

0.1.167
---

  * Исправлены ошибки использования suds клиента. CERTOR-91.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 17:18:12

0.1.166
---

  * Проверка на единственный wildcard включена обратно.
  * Улучшена обработка ошибок от Certum. CERTOR-91.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-08 16:44:02

0.1.165
---

  * Отключена проверка количества wildcard сертификатов. CERTOR-120.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-11-05 20:33:57

0.1.164
---

  * Исправлена ошибка в формировании выгрузки для NOC. CERTOR-116.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-30 21:58:09

0.1.163
---

  * В админку добавлена возможность редактировать привязку доступов к отделам. CERTOR-116

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-30 19:49:22

0.1.162
---

  * В выгрузку для NOC добавлена информация о доступах на основе принадлежности к отделу. CERTOR-119.
  * Добавлен забор данных о департаментах из центра.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-30 19:37:51

0.1.161
---

  * Теперь поле pc\_unum не обязательное. CERTOR-118.
  * Игнорируем любые ошибки в команде after\_release, чтобы не ломалась установка пакета, когда graphite сервер недоступен. CERTOR-100.
  * Исправлена опечатка в nginx файле.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-30 17:13:38

0.1.160
---

  * Конфиг nginx модифицирован таким образом, чтобы на 444 порту принимать только хелпового пользователя с определенным сертификатом. CERTOR-116.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-28 15:33:46

0.1.159
---

  * Разделитель выгрузки для NOC изменен на просто пробел. CERTOR-115.
  * Для сертификатов, которые запрашиваются путем передачи внешнего CSR, заполняем поле common\_name сначала беря данные из CSR, а потом из самого сертификата. CERTOR-114.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-24 21:41:16

0.1.158
---

  * Не посылаем сообщения о том, что сертификат не был выдан, если это был 'pc' сертификат.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-22 17:03:01

0.1.157
---

  * Добавлена проверка crl внутреннего CA, так что теперь Сертификатор сможет узнавать о сертифткатах, отозванных через оснастку. CERTOR-105.
  * Добавлен newline в конец кронтаба.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-21 18:01:44

0.1.156
---

  * Отключены дефолтные authentication classes restframework, так как они пытаются требовать csrf токен.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-17 17:05:38

0.1.155
---

  * Исправлена 500-ка для неизвестных yauth пользователей. CERTOR-113.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-17 15:43:09

0.1.154
---

  * Обязательно требуем логина на странице /request/. CERTOR-112.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-16 20:24:33

0.1.153
---

  * Исправлены шаблоны для запроса pc сертификатов во внутрненнем CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-16 20:02:10

0.1.152
---

  * Выгрузка данных для NOC, через запятую.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-16 19:03:59

0.1.151
---

  * Исправлена ошибка выгрузки, когда для шаблона CA не задана ни одна сеть. CERTOR-111.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-16 18:46:11

0.1.150
---

  * Позволяем не задать пустой список доступных сетей для шаблона CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-16 18:33:06

0.1.149
---

  * Исправлено отображение статики админки на продакшене. CERTOR-111.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-16 18:17:06

0.1.148
---

  * Добавлена возможность устанавливать соответствия между шаблонами CA и сетями в которые надо пускать сотрудника. CERTOR-111.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-16 18:02:29

0.1.147
---

  * Исправлено отсутствующее расширение файла, если сертификат скачивался без явного указания формата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-16 13:08:03

0.1.146
---

  * Вернул обратно used\_template в выгрузку для NOC. По просьбе Саши Болотова.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-16 13:02:35

0.1.145
---

  * Теперь ручка, отдающая сертификат, устанавливает правильный заголовок Content-Disposition, что приводит к тому, что файл сохраняется не как download.pfx, а состоит из common\_name + расширение. CERTOR-110.
  * Прячем форму запроса сертификата от всех, кроме линуксоидов. CERTOR-108.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-15 17:48:31

0.1.144
---

  * Исправлена ошибка выдачи сертификата через Certum. CERTOR-109.
  * Исправлена ошибка подгрузки скрипта для определения браузера. CERTOR-107.
  * Реализована первая версия plain/text выгрузки для NOC. CERTOR-106.
  * XML renderer for PCCertificatesList.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-15 16:53:43

0.1.143
---

  * Добавлено поле Certificate.end\_date.
  * Добавлено получение даты окончания действия сертификата, а так же его серийника, из самого сертификата. CERTOR-104.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-15 01:10:47

0.1.142
---

  * Пересборка пакета в связи с лишним файлом от emacs.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-15 00:20:28

0.1.141
---

  * Добавлена вьюшка для выдачи pc-сертификатов, как линуксовых, так и обычных.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-15 00:04:08

0.1.140
---

  * Исправлен common\_name для linux-pc сертификатов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-14 18:49:38

0.1.139
---

  * С список шаблонов внутреннего CA добавлен шаблон для linux-pc.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-14 18:28:12

0.1.138
---

  * Убран забытые set\_trace.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-14 18:02:00

0.1.137
---

  * Сертификаты линуксоидам выдаем через виндовый CA, а не через тестовый.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-14 10:12:58

0.1.136
---

  * Добавлена страница запроса сертификата линукс пользователем.
  * Обновлены зависимости.
  * Дополнительный логгинг факта постановки домена в очередь на валидацию.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-10-14 09:41:19

0.1.135
---

  * Добавлен динамический выбор шаблона для внутреннего CA.
  * Используем cachain, при получении готового сертификата от внутреннего CA.
  * Исправлено имя шаблона сертифката во внутреннем CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-30 18:25:36

0.1.134
---

  * Добавлено сохранение ошибочного ответа от InternalCA в файл.
  * Добавлен скрипт обновления зависимостей.
  * В цепочку добавлены два сертификата YandexInternalRootCA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-27 18:07:17

0.1.133
---

  * Исправлена проверка сертификата внутреннего CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-27 15:49:33

0.1.132
---

  * Перешли на продакшн внутренний CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-27 11:01:51

0.1.131
---

  * Исправлена отсылалка статистики из логов django в graphite.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-26 18:00:36

0.1.130
---

  * Дополнительный отладочный логгинг в команде issue\_certificates.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-25 17:25:10

0.1.129
---

  * Исправлена ошибка, возникающая когда верификация доменов не требуется.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-25 17:04:54

0.1.128
---

  * Дополнительный логгинг для отслеживания плохих данных от Certum.
  * Исправлена запятая в перечислении хостов письма-уведомления об ошибке выдачи сертификата.
  * Используем реальный yandexCAs в конфиге тестового Nginx.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-24 21:49:05

0.1.127
---

  * Исправлена ошибка в check\_txt\_records.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-20 15:11:52

0.1.126
---

  * Customer заменен с tokza@yandex-team.ru на просто pki-customer.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-20 01:21:51

0.1.125
---

  * Вернул в зависимости Markdown.
  * Исправлены дублирующиеся зависимости.
  * Исправлена ошибка c fields\_to\_native.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-20 00:37:44

0.1.124
---

  * Поправлены зависимости.
  * Добавлены компилированные requirements.
  * Добавлен requirements/development.in.
  * Новые requirements, для обработки pip-compile.
  * Новая Django 1.4.8.
  * Плашка в письмах, предупреждающая о том, из какого окружения было отправлено это письмо.
  * Более подробная история валидации домена.
  * Добавлен функционал для рассылки HTML писем с уведомлениями.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-19 22:51:20

0.1.123
---

  * Кодируем хосты в IDNA, перед отправкой в certum.
  * Поле deployed\_at теперь не редактируемое.
  * Исправлена проверка ssl сертификата для русских доменов.
  * Добавлена забытая миграция.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-05 12:05:46

0.1.122
---

  * Записываем в лог факт того, что сертификат стал использоваться в продакшене.
  * Собираем статистику по установкам протухших сертификатов.
  * Добавлен сбор статистики по задеплоеным сертификатам.
  * Добавлена проверка того, что SSL сертификат установлен на указанные хосты. CERTOR-76.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-04 16:58:23

0.1.121
---

  * Не делаем lowercase при получении серифника с вебсервера.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-04 14:50:45

0.1.120
---

  * Еще раз поправлена настройка shell\_plus.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-04 14:16:25

0.1.119
---

  * Конфигурация shell\_plus перенесена в development.py.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-03 21:51:16

0.1.118
---

  * Добавлены утилиты для проверки установлен сертификат на хосте или нет. CERTOR-76.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-09-03 21:44:40

0.1.117
---

  * Pdb++ добавлен в зависимости.
  * В разработческий requrement добавлен pip-tools из правильной ветки.
  * Команде issue\_certificates добавлена опция pdb.
  * Убран старый отладочный код.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-26 21:40:32

0.1.116
---

  * Отключаем рассылку кодов валидации по email.
  * Собираем virtualenv с distribute.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-22 17:47:47

0.1.115
---

  * Добавлен repr для HostToApproveHistory.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-22 16:58:43

0.1.114
---

  * Поправлена миграция 0031.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-22 16:39:04

0.1.113
---

  * Поле in\_dns переименовано в validated и его обновление теперь вызывает добавление действия  'validated' к HostToApprove.
  * Выкинут этап чтения кодов для валидации из Imap папки. Теперь все должно происходить еще быстрее.
  * Больше не делаем chown на все логи подряд.
  * Теперь для EV сертификата используем лишь один product id: 982.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-22 13:51:19

0.1.112
---

  * Добавлена ссылка download2, для которой можно указывать Accept заголовок. И переход на restframework 2.2.7 -> 2.3.7.
  * При формировании pem файла, указываем вплотную приватный ключ, сертификат и промежуточный сертификат.
  * Теперь позволяем запрашивать pc сертификат через тестовый виндовый CA.
  * Исправлена ошибка в документации, поле называется не csr, а request.
  * Исправлен хост тестового внутреннего сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-19 22:18:21

0.1.111
---

  * Исправлено сохранение лишних данных в логгере при профайлинге поляцкого CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-16 18:28:04

0.1.110
---

  * Убрал ylog из зависимостей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-15 00:26:13

0.1.109
---

  * Поправлено логирование ошибок.
  * Теперь логи ведутся в JSON формате, чтобы было проще разбирать из в logstash.
  * Исправлена ошибка при скачивании pem из TestCA.
  * Поправлен скрипт для локальной установки пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-15 00:20:45

0.1.108
---

  * Пользователь slash теперь может выписывать pc сертификаты. IS-864.
  * Добавлена команда, чтобы обновлять сертификатор на тестинге сразу после сборки.
  * Исправлен конфиг для Nginx на тестинге.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-08 21:16:00

0.1.107
---

  * Убрал django-alive из списка зависимостей.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-08 15:25:46

0.1.106
---

  * Добавлен флаг для запроса EV сертификатов. Пока запрашивать могу только я или tokza. CERTOR-92.
  * Исправлена ошибка логирование ошибок в командах, когда в трейсбэке есть русские символы.
  * Исправлена ошибка в readmail, из-за которой чтение кодов ломалось, когда в папку попадало письмо с только plain/text частью.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-08-05 15:05:43

0.1.105
---

  * Вьюшка, отдающая пользователей поправлена так, чтобы кэшировать данные при первом запросе и использовать xml или json по выбору.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-12 20:52:02

0.1.104
---

  * Добавлена вьюшка, отдающая информацию про пользователя.
  * Добавлен класс для запроса сертификатов в виндовом CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-12 20:20:58

0.1.103
---

  * Исправлена ошибка в hosts-to-approve, и добавлен тест на это.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-05 22:21:41

0.1.102
---

  * Теперь вынимаем коду из писем более правильными регекспами и поддерживаем любые домены.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-05 21:25:53

0.1.101
---

  * Еще больше логгинга.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-05 20:20:20

0.1.100
---

  * Расширен логгинг.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-05 19:58:37

0.1.99
---

  * Исправлена ошибка в read\_mail.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-05 19:22:56

0.1.98
---

  * Поправил код так, чтобы новые коды подтверждения хоста перетирали старые и не возникало дубликатов. CERTOR-89.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-05 17:47:56

0.1.97
---

  * Тестовая сборка, пробую катить через conductor.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-01 18:10:04

0.1.96
---

  * Отключена опция 'ssl\_verify\_client optional'.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-01 14:07:54

0.1.95
---

  * Добавлена миддльварь, устанавливающая allow-origin для голема. GOLEM-946.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-07-01 13:08:18

0.1.94
---

  * Еще одно исправление предыдущей ошибки.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-27 16:26:25

0.1.93
---

  * Исправлена ошибка в проерке ответственности за хосты. CERTOR-85.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-27 15:25:48

0.1.92
---

  * Исправлена обработка сетевых ошибок при попытках выписать сертификат. CERTOR-84.
  * Скрипт сборки исправлен, чтобы использовать общую библиотеку.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-25 16:38:36

0.1.91
---

  * Включаем в пакет favicon.ico и robots.txt. CERTOR-82.
  * Добавлен newline в Cron.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-24 20:15:05

0.1.90
---

  * Добавлена обработка неправильного статус-кода от Центра.
  * Добавлено логирование попыток скачать или отозвать сертификат. CERTOR-77.
  * Теперь для хостовых сертификатов, при операциях Download и Delete, производится проверка владения хостами в Големе. CERTOR-81.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-24 17:54:21

0.1.89
---

  * Исправлена функция проверки прав в големе.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-11 20:47:24

0.1.88
---

  * Поправлен урл для устновки logster.
  * Исправлена ошибка, связанная с проверкой хостов через голем.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-11 18:44:24

0.1.87
---

  * Добавлен пропущенный импорт check\_if\_user\_responsible\_for\_hosts.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-11 17:52:50

0.1.86
---

  * Исправлена опечатка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-11 17:20:10

0.1.85
---

  * Исправлен requirements файл для продакшена.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-11 17:11:23

0.1.84
---

  * Берем патченный logster с моего гитхаба.
  * Tokza убран из списка суперпользователей.
  * Добавлен парсер ошибок для Django логов.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-11 15:25:12

0.1.83
---

  * Переключился на logster из апстрима.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-10 20:36:02

0.1.82
---

  * Добавлены конфиги для генерации графиков посредством logster.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-10 19:52:29

0.1.81
---

  * Добавлена команда, сохраняющая в Graphite файкт выкладки релиза.
  * Добавлена проверка того, что запрашивающий владеет хостами на големе. CERTOR-79.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-07 21:03:33

0.1.80
---

  * Добавлена возможность указывать размер страницы в API.
  * В статистику добавлено поле latest\_issue\_time.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-05 14:05:44

0.1.79
---

  * Добавлена команда, отсылающая данные в Graphite.
  * Улучшено логгирование ответов от Certum.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-06-05 13:01:27

0.1.78
---

  * Исправлена опечатка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-27 15:23:42

0.1.77
---

  * Исправлена ошибка из-за которой не выписывался сертификат через Certum.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-27 14:50:21

0.1.76
---

  * Исправлена HTML форма запроса сертификата через API. CERTOR-74.
  * Добавлен заголовок Access-Control-Allow-Origin *. CERTOR-68.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-23 21:30:58

0.1.75
---

  * Исправлена ошибка при скачивании pfx, CERTOR-72. Теперь в PEM так же включается промежуточный сертификат L2 или L4, CERTOR-73.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-23 20:38:00

0.1.74
---

  * Исправлена ошибка, связанная с забытой переменной limit.
  * Исправлена уязвимость, ползволяющая через Nginx читать файлы проекта. CERTOR-71.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-23 19:46:56

0.1.73
---

  * Добавлена модель Host и возможность фильтрации по хостам. CERTOR-70.
  * Раскомментирован запрет запроса PC сертификата для всех проме helpdesk и меня.
  * Расширенный фильтр по логину, позволяющий получать полный список сертификатов. CERTOR-70.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-23 18:50:07

0.1.72
---

  * Сделано определение инвентарного номера по серийнику. CERTOR-47.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-20 17:29:11

0.1.71
---

  * Исправлена опечатка, приводившая к SyntaxError.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-14 10:52:47

0.1.70
---

  * Выпилил старые вьюшки, которые работали с сертификатами напрямую. CERTOR-65.
  * Исправлен возможный shell injection при вызове команд через envoy. CERTOR-67.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-14 10:40:08

0.1.69
---

  * Исправлен миксин IsOwner, чтобы соответствовать новому API django rest framework. CERTOR-65.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-05-13 18:33:52

0.1.68
---

  * Исправлен срок действия сертификата. Теперь он до трех лет.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-26 16:17:37

0.1.67
---

  * Еще одна попытка исправить рендеринг download на продакшене.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-26 16:13:49

0.1.66
---

  * Еще один фикс рендеринга DownloadField.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-26 14:48:24

0.1.65
---

  * Исправлены суффиксы для ссылки скачивания сертификатов. CERTOR-64.
  * Кэшируем результат вычисления A записи для hosts-to-approve.xml. CERTOR-53.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-25 15:24:32

0.1.64
---

  * Теперь любой может выбрать ca\_name, а так же исправлена выборка сертификатов по-умолчанию.
  * Исправлена невозможность выписать SMIME. CERTOR-63.
  * Добавлена обработка ошибки Bad Gateway.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-24 14:19:42

0.1.63
---

  * Добавлена обработка ошибок BadStatusLine.
  * Переезд на новые версии библиотек.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-22 19:13:23

0.1.62
---

  * Исправлена ошибка, возникающая при запросе хостового сертификата.
  * SSL настроен так, чтобы пускать тестовый голем.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-22 14:25:00

0.1.61
---

  * Логгинг поправлен, чтобы работать в 2.6 питоне.
  * Теперь management команды выдают ошибку, а не выходят молча, как будто ничего не было.
  * Позволяем избранным пользователям выбирать CA при запросе сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-17 21:07:11

0.1.60
---

  * Теперь в CommonName хостового сертификата попадает либо wildcard, либо первый из указанных хостов. CERTOR-56.
  * Введены ограничения на хостовые сертификаты. Common name задавать нельзя, email тоже. Более одного wildcard домена быть не может.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-16 17:51:18

0.1.59
---

  * Исправлен подсчет wildcard сертификатов. CERTOR-61.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-12 20:32:08

0.1.58
---

  * Добавлена фавиконка с замочком и пустой robots.txt. CERTOR-57.
  * Исправлено вычисление статуса при преждевременном отзыве сертификата. CERTOR-60.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-12 17:23:54

0.1.57
---

  * Исправлено логирование ошибок от Certum, при отзыве сертификата.
  * Исправлена выборка hosts-to-approve. Теперь выдаются только хосты для сертификатов в востоянии validation.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-12 16:50:07

0.1.56
---

  * Исправлена опечатка в коде.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-12 16:05:10

0.1.55
---

  * Разрешить 'art' просматривать и отзывать любые сертификаты. CERTOR-58.
  * Команда issue\_certificates теперь смотрит на статус сертификата, и в случае ошибки переводит его в error. CERTOR-59.
  * Создаем HostToApprove только для доменов верхнего уровня.
  * Исправлена ошибка в профайлере, из-за которой логгинг ломался.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-12 15:55:52

0.1.54
---

  * Добавлено логирование окончания обработки HTTP запроса.
  * Включил yandex.com.tr в список toplevel доменов для валидации.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-11 18:13:50

0.1.53
---

  * Добавлено поле status и вьюха для отображения статистики.
  * Добавлены дополнительные поля для подсчета количества сертификатов. CERTOR-24.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-11 14:59:27

0.1.52
---

  * Rebuild as amd64.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-10 18:06:23

0.1.51
---

  * Rebuild.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-10 17:58:34

0.1.50
---

  * Аппрувим только домены второго уровня. CERTOR-55.
  * Выбираем направление в качестве Organization Unit. CERTOR-54.
  * Теперь логи содержат информацию о контексте, благодаря twiggy.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-10 17:04:34

0.1.49
---

  * Исправлена обработка кодов подтверждения. CERTOR-52.
  * Исправлен токен к Center, в деве.
  * Настроен HTTPS в продакшене.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-03 16:26:24

0.1.48
---

  * Добавлена опция ssl\_verify\_client optional в продакшн nginx.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-03 14:19:43

0.1.47
---

  * В продакшене читаем imap папку INBOX. CERTOR-43.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-02 21:41:39

0.1.46
---

  * Прописан CN сертификата голема для продакшена.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-04-02 19:44:55

0.1.45
---

  * Исправлен токен для доступа к Center. CERTOR-25.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-22 14:41:45

0.1.44
---

  * Вернул назад organizationalUnitName так как Certum требует наличия этого
    поля. Но у нас оно содержит значение NONE.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-15 21:04:15

0.1.43
---

  * Берем поля для SMIME сертификата со Staff. CERTOR-25.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-15 20:51:27

0.1.42
---

  * Теперь сертификат типа 'pc' выписывается синхронно, сразу при запросе через API. CERTOR-42.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-14 12:59:08

0.1.41
---

  * Добавлена авторизация для helpdesk, по доступу к определенному порту. CERTOR-36.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-13 14:35:54

0.1.40
---

  * Добавлен новый тип сертификата PC. CERTOR-35.
  * Не позволяем вручную задавать поля для smime сертификата. CERTOR-37.
  * Теперь хосты можно перечислять построчно. CERTOR-36.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-13 18:44:37

0.1.39
---

  * Теперь ручка hosts-to-approve возвращает A записи вместо алиасов. CERTOR-40.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-07 16:16:26

0.1.38
---

  * Исправлена ошибка вывода хостов, требующих подтверждения.
  * Исправлены ошибки в read\_mail.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-05 17:56:47

0.1.37
---

  * Еще одно исправление логики обработки wildcard. CERTUM-39.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-05 16:58:41

0.1.36
---

  * Исправлено определение wildcard сертификатов. CERTOR-39.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-05 16:46:16

0.1.35
---

  * Исправлена обработка ошибок в issue\_certificates. CERTOR-38.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-03-05 16:29:24

0.1.34
---

  * Добавлено поле expire\_at для HostToApprove.
  * В цепочку сертификатов Certum добавлены Level 1-4.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-25 18:44:20

0.1.33
---

  * Исправлена опечатка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-22 19:06:26

0.1.32
---

  * Улучшена обработка ошибок в команде check\_txt.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-22 18:00:29

0.1.31
---

  * Исправлена директория, в которую устанавливается certum-chain.pem.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-22 17:30:12

0.1.30
---

  * Исправлена команда check\_txt\_records.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-22 15:45:19

0.1.29
---

  * Команды read\_mail и check\_txt\_records по крону.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-21 19:27:05

0.1.28
---

  * Исправлена ошибка в CertumCA.
  * Включаем ssl на продакшене.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-21 17:55:51

0.1.27
---

  * Добавлена возможность подгружать secure\_settings.py из
    /etc/yandex/yandex-crt.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-21 17:13:02

0.1.26
---

  * Поправлен Nginx конфиг для продакшена.
  * В зависимости добавлен django-russian.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-21 16:29:51

0.1.25
---

  * Произведен рефакторинг кода, выполняющего запросы к Certum.
  * Убрана селективная выдача конкретного сертификата.
  * Убран set\_trace из virtualenv.py.
  * Теперь для однодоменного сертификата испольуется Trusted Multidomain 10 domains вместо EV.
  * Поправлен read-mail, чтобы работать с yandex-team доменами.
  * Валидируем сертификат certum по цепочке, при отправке запроса на валидацию домена.
  * Показываем в hosts-to-approve.xml только те хосты, для которых можем менять DNS автоматически.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-20 17:54:28

0.1.24
---

  * Django\_rq закомментирован в settings.py.
  * Virtualenv 1.8.4

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-12 19:12:31

0.1.23
---

  * Добавлен fabfile.py
  * Поправлена dev зависимость от ipython.
  * Исправлен postinst файл.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-12 17:50:28

0.1.22
---

  * Добавлена команда check\_txt\_records.
  * Добавлена миграция и команда для проверки DNS серверов, отвечающих за хост.
  * Теперь при запросе сертификата в Certum, создается соответствующее количество HostToApprove записей в базе.
  * Реализован отзыв заказанного сертификат, в случае, если он еще не выписан.
  * Поправлено поле orderParameters.customer.
  * Добавлены две миграции БД.
  * Отлажена работа скрипта read\_mail.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-02-12 16:23:10

0.1.21
---

  * Сделан экстрактор кодов из писем от Certum.
  * Исправлен формат выдачи hosts-to-approve. Теперь там XML.
  * Исправлен скрипт сборки. Теперь он берет Легу из Git.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-29 18:06:46

0.1.20
---

  * Начата работа над подтверждением доменов через DNS.
  * Мелкие правки в работе с Certum.
  * Поле serial\_number сделано нередактируемым. CERTOR-28.
  * Добавлен отзыв сертификатов из Certum.
  * Закомментированы продакшн настройки в local\_settings.
  * ID всех продуктов прописаны в settings.py.
  * Allow python-django or python-django-1.4, but use custom in viritualenv.
  * Поправлена сборка под precise.
  * Прописал в requestorInfo Антона Карпова.
  * Подготовка к выкладке в продакшн.
  * Отдельная настройка SMIME\_PRODUCT\_ID.
  * Рестарт после установки.


 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2013-01-29 11:34:59

0.1.19
---

  * Добавлены фильтры и возможность отзыва тестового сертификата.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-21 16:21:42

0.1.18
---

  * Снова накатываем миграции в postinst.
  * Поправлена авторизация по SSL.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-20 18:41:17

0.1.17
---

  * Убраны лишние set\_trace, удален migrate при установке пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-20 17:20:36

0.1.16
---

  * Добавлено поле requester и соответствующее заполнение для пользователя
    golem.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-20 16:55:28

0.1.15
---

  * Исправлен manage.py.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 19:13:44

0.1.14
---

  * Еще одно исправление debian/rules.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 18:56:42

0.1.13
---

  * Исправлен путь до manage.py.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 18:36:04

0.1.12
---

  * Зависимость от requests==1.0.3.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 18:17:18

0.1.11
---

  * Выпилена связка с Управлятором.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 17:54:58

0.1.10
---

  * Кладем virtualenv в общее место. CERTOR-19.
  * Добавлена документация к ручкам API.
  * Добавлен auth бэкенд для авторизации по SSL. CERTOR-15.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 17:41:39

0.1.9
---

  * Исправлено выписывание тестовых сертификатов. Теперь для этого создается
    отдельная директория.
  * Поправлены конфиги Nginx для девелопмента.
  * Добавлена команда для запуска девелоперского fastcgi.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-18 13:36:38

0.1.8
---

  * Правильный путь до тестового CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 18:11:31

0.1.7
---

  * Added cron.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 17:40:14

0.1.6
---

  * More fixes.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 16:48:28

0.1.5
---

  * Fixed lego.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 16:30:49

0.1.4
---

  * Фиксим Lego.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 15:49:49

0.1.3
---

  * Еще один фикс rest\_framework.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 15:20:58

0.1.2
---

  * Не удаляем статику rest\_framework.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 14:53:17

0.1.1
---

  * Убрана лишняя отладка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 13:21:02

0.1.0
---

  * Initial release

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-30 13:13:13

новке пакета.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-20 17:20:36

0.1.16
---

  * Добавлено поле requester и соответствующее заполнение для пользователя
    golem.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-20 16:55:28

0.1.15
---

  * Исправлен manage.py.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 19:13:44

0.1.14
---

  * Еще одно исправление debian/rules.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 18:56:42

0.1.13
---

  * Исправлен путь до manage.py.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 18:36:04

0.1.12
---

  * Зависимость от requests==1.0.3.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 18:17:18

0.1.11
---

  * Выпилена связка с Управлятором.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 17:54:58

0.1.10
---

  * Кладем virtualenv в общее место. CERTOR-19.
  * Добавлена документация к ручкам API.
  * Добавлен auth бэкенд для авторизации по SSL. CERTOR-15.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-19 17:41:39

0.1.9
---

  * Исправлено выписывание тестовых сертификатов. Теперь для этого создается
    отдельная директория.
  * Поправлены конфиги Nginx для девелопмента.
  * Добавлена команда для запуска девелоперского fastcgi.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-12-18 13:36:38

0.1.8
---

  * Правильный путь до тестового CA.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 18:11:31

0.1.7
---

  * Added cron.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 17:40:14

0.1.6
---

  * More fixes.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 16:48:28

0.1.5
---

  * Fixed lego.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 16:30:49

0.1.4
---

  * Фиксим Lego.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 15:49:49

0.1.3
---

  * Еще один фикс rest\_framework.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 15:20:58

0.1.2
---

  * Не удаляем статику rest\_framework.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 14:53:17

0.1.1
---

  * Убрана лишняя отладка.

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2012-11-27 13:21:02

0.1.0
---

  * Initial release

 [Alexander Artemenko](https://staff.yandex-team.ru/art@yandex-team.ru) 2011-12-30 13:13:13

