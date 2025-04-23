# Unbound в Аркадии

## Код

Код в Аркадии лежит в contrib/tools: [contrib/tools/unbound](http://a.yandex-team.ru/arc/trunk/arcadia/contrib/tools/unbound)

Импортируется код из [github](https://github.com/NLnetLabs/unbound) через утилиту для импорта внешних репозиториев в Аркадию [yamaker](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/yamaker/). Конфиг импорта и патчи расположены [тут](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/yamaker/projects/unbound).

## Философия

Так как мы много меняем код в Unbound, важно сохранить оригинальное поведение ванильной версии.
То есть если есть конфиг A и поведение Unbound с ним было одним, то и после наложения всех наших патчей Unbound с конфигом A должен иметь то же поведение, что и до патчей.
Таким образом, все изменения, которые вносятся патчами, должны находиться под опцией, которая в дефолтном значении выключает использование нового кода, или не должны значительно влиять на поведение Unbound.

## Сборка

Помимио самого бинаря с сервером к Unbound прилагаются разные утилиты (unbound-control, unbound-checkconf и другие).
Собрать все сразу можно через [Ya Package](https://docs.yandex-team.ru/ya-make/usage/ya_package/).
Конфиг пакета находится в [infra/yp_dns/deploy/unbound/package.json](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns/deploy/unbound/package.json).

Ресурсы можно собрать как локально (для тестов и разработки), так и через Sandbox (для выкладки в продакшен).
Как собрать правильно:

{% list tabs %}

- Сборка в Sandbox

  1. Идем в последний тикет в очереди [UNBOUNDREL](https://st.yandex-team.ru/UNBOUNDREL) и находим ссылку на ресурс со сборкой Unbound.
     У ресурса тип `UNBOUND_WITH_YP_BUNDLE`. Пример: <https://sandbox.yandex-team.ru/resource/3318337142/view>.
  2. Переходим в Sandbox Task, которая создала этот ресурс (пример задачи для ресурса выше: [UNBOUND_WITH_YP_BUNDLE](https://sandbox.yandex-team.ru/task/1375680647/view)). И клонируем ее.
  3. Дальше важно указать нужную версию Ubuntu, под которую будет собираться релиз.
     Для этого раскрываем вкладку `Advanced`. Дальше `Host` устанавливаем в `linux_ubuntu_18.04_bionic` (именно такая версия сейчас используется в продакшене).
  4. Остальные параметры должны быть уже заполнены правильно.
  5. Запускаем задачу `Run`. Ждем завершения.
  6. Устанавливаем время жизни ресурса в бесконечность: кнопка `Important` на странице ресурса.

- Локальная сборка

  ```sh
  ya package --raw-package patch/to/arcadia/infra/yp_dns/deploy/unbound/package.json
  ```

{% endlist %}

## Тестирование

При каждом внесении правок в код Unbound **крайне рекомендуется** фискировать изменение тестом.
Тесты пишутся на Python через pytest в [infra/unbound/tests](https://a.yandex-team.ru/arc/trunk/arcadia/infra/unbound/tests).
Эти тесты запускаются в автосборке в прекоммитных и посткоммитных проверках.
Также их рекомендуется запускать перед сборкой релиза.

## Внутренние релизы

Версии Unbound, которые мы используем в Яндексе, принимаются в ST-очереди [UNBOUNDREL](https://st.yandex-team.ru/UNBOUNDREL).

## Инструкция: приложение конкретного коммита из Гитхаба {#apply-github-patch}

На примере коммита <https://github.com/NLnetLabs/unbound/commit/ff6b527184b33ffe1e2b643db8a32fae8061fc5a>.

1. Качаем файл с патчем:

   ```sh
   wget https://github.com/NLnetLabs/unbound/commit/ff6b527184b33ffe1e2b643db8a32fae8061fc5a.patch
   ```

1. Перемещаем патч к остальным в [arcadia/devtools/yamaker/projects/unbound/patches](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/yamaker/projects/unbound/patches). Именуем файл, добавляя порядковое число патча в начало (тут это 24-й патч, поэтому пишем `0024`):

   ```sh
   mv ff6b527184b33ffe1e2b643db8a32fae8061fc5a.patch devtools/yamaker/projects/unbound/patches/0024-reset-the-dns-message-id-when-moving-queries.patch
   ```

1. Собираем `yamaker` и запускаем `import`:

   ```sh
   ya make -r devtools/yamaker
   ./devtools/yamaker/yamaker import contrib/tools/unbound
   ```

   {% note tip %}

   После первого `import` можно добавлять `-nb` к параметрам запуска, чтобы не пересобирать проект каждый раз.

   {% endnote %}

1. Исправляем проблемы/конфликты. На этом примере мы получаем такую ошибку применения патча:

   {% cut "Текст ошибки" %}

   ```text
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0024-reset-the-dns-message-id-when-moving-queries.patch
   can't find file to patch at input line 19
   Perhaps you used the wrong -p or --strip option?
   The text leading up to this was:
   --------------------------
   |From ff6b527184b33ffe1e2b643db8a32fae8061fc5a Mon Sep 17 00:00:00 2001
   |From: George Thessalonikefs <george@nlnetlabs.nl>
   |Date: Wed, 19 May 2021 14:59:33 +0200
   |Subject: [PATCH] - Fix for #411, #439, #469: Reset the DNS message ID when
   | moving queries   between TCP streams. - Refactor for uniform way to produce
   | random DNS message IDs.
   |
   |---
   | doc/Changelog              |  5 +++++
   | services/authzone.c        |  4 ++--
   | services/outside_network.c | 45 ++++++++++++++++++++++++++++++++------
   | util/net_help.h            |  4 ++++
   | 4 files changed, 49 insertions(+), 9 deletions(-)
   |
   |diff --git a/doc/Changelog b/doc/Changelog
   |index 6fd42f92d..c410c1880 100644
   |--- a/doc/Changelog
   |+++ b/doc/Changelog
   --------------------------
   File to patch:
   ```

   {% endcut %}

   По тексту ошибки ясно, что в патче есть изменения в файле, которого у нас нет – `doc/Changelog`.
   Поэтому идем и вырезаем из файла с патчем соответствующие строчки.

1. Перезапускаем `yamaker` с ключом `-la` (чтобы обновились файлы с лицензиями) и наблюдаем успех:

   {% cut "Подробнее" %}

   ```sh
   $ ya make -r devtools/yamaker && ./devtools/yamaker/yamaker import contrib/tools/unbound -nb -la
   Warn: checkout option is unnecessary for Arc vcs
   Ok
   + ./devtools/yamaker/yamaker run -s /place/vartmp/yamaker/unbound/unbound-1.13.1/ -b /place/vartmp/yamaker/unbound/unbound-1.13.1/ -o /place/vartmp/yamaker/unbound/destdir -d /place/vartmp/yamaker/unbound/deps.json --arc /home/dima-zakharov/arc/arcadia --out-rel contrib/tools/unbound -u /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/provides.pbtxt --owner g:yp-dns --owner dima-zakharov --put 'Library unbound=.' --put 'Program unbound=unbound' --put unbound-anchor=unbound-anchor --put unbound-checkconf=unbound-checkconf --put unbound-control=unbound-control --put unbound-host=unbound-host -t unbound -t unbound-anchor -t unbound-checkconf -t unbound-control -t unbound-host --ignore-command libtool --version 1.13.1 --license BSD-3-Clause --add-defines --nixpkgs-revision c00959877fb06b09468562518b408acda886c79e
   ...
   Library  unbound               .
   Program  unbound            +  unbound
   Program  unbound-anchor     +  unbound-anchor
   Program  unbound-checkconf  +  unbound-checkconf
   Program  unbound-control    +  unbound-control
   Program  unbound-host       +  unbound-host
   unaccounted include dependency: /nix/store/9r9fd0b2i91wh4s4qcilrdklla549vpq-protobuf-c-1.3.3/include
   + rsync -L -0 --exclude=CMakeLists.txt '--exclude=*.vcxproj.filters' '--exclude=*.vcproj' '--exclude=*.sln' '--exclude=*.o' '--exclude=*.in' '--exclude=*.la' '--exclude=*.lo' '--exclude=*.vcxproj' '--exclude=*.am' /place/vartmp/yamaker/unbound/unbound-1.13.1/ /place/vartmp/yamaker/unbound/destdir --files-from /var/tmp/subcopyfd8i0vg9
   + rsync -L -0 --exclude=BUILD.bazel --exclude=BUCK --exclude=NWGNUmakefile --exclude=MANIFEST --exclude=LLVMBuild.txt '--exclude=*.vcproj' --exclude=GNUmakefile '--exclude=*.in' --exclude=OWNERS '--exclude=*.la' '--exclude=*.lo' '--exclude=*.vcxproj' '--exclude=*.am' --exclude=BUILD '--exclude=*.vcxproj.filters' --exclude=WORKSPACE '--exclude=*.sln' --exclude=PKG-INFO '--exclude=*.o' /place/vartmp/yamaker/unbound/unbound-1.13.1 /place/vartmp/yamaker/unbound/destdir --files-from /var/tmp/subcopy0xjbk1aj
   + rsync -L -0 --exclude=BUILD.bazel --exclude=BUCK --exclude=NWGNUmakefile --exclude=MANIFEST --exclude=LLVMBuild.txt '--exclude=*.vcproj' --exclude=GNUmakefile '--exclude=*.in' --exclude=OWNERS '--exclude=*.la' '--exclude=*.lo' '--exclude=*.vcxproj' '--exclude=*.am' --exclude=BUILD '--exclude=*.vcxproj.filters' --exclude=WORKSPACE '--exclude=*.sln' --exclude=PKG-INFO '--exclude=*.o' /place/vartmp/yamaker/unbound/unbound-1.13.1/ /place/vartmp/yamaker/unbound/destdir --files-from /var/tmp/subcopy1wo_phpt
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0001-fix_build.patch
   patching file config.h
   Hunk #6 succeeded at 1117 (offset 1 line).
   patching file services/listen_dnsport.c
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0002-Adding-affinity-for-unbound-configuration-switch-sho.patch
   patching file daemon/worker.c
   Hunk #2 succeeded at 1944 (offset 8 lines).
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0003-Adding-response-force-aa-feature-for-external-intern.patch
   patching file daemon/worker.c
   Hunk #1 succeeded at 557 (offset 2 lines).
   Hunk #2 succeeded at 762 (offset 5 lines).
   patching file iterator/iterator.c
   patching file services/authzone.c
   Hunk #1 succeeded at 3295 (offset 3 lines).
   patching file services/localzone.c
   Hunk #1 succeeded at 1262 (offset 44 lines).
   patching file services/mesh.c
   Hunk #1 succeeded at 1162 (offset 2 lines).
   Hunk #2 succeeded at 1288 (offset 2 lines).
   patching file util/config_file.c
   Hunk #2 succeeded at 560 (offset 9 lines).
   Hunk #3 succeeded at 982 (offset 28 lines).
   patching file util/config_file.h
   patching file util/configlexer.lex
   patching file util/configparser.y
   Hunk #2 succeeded at 238 (offset 2 lines).
   Hunk #3 succeeded at 1373 (offset 22 lines).
   patching file util/data/msgencode.c
   Hunk #1 succeeded at 879 (offset 37 lines).
   patching file util/data/msgencode.h
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0004-Adding-response-ttl-aglorithm-selection.patch
   patching file daemon/worker.c
   Hunk #1 succeeded at 552 (offset 2 lines).
   Hunk #2 succeeded at 767 (offset 5 lines).
   Hunk #3 succeeded at 1953 (offset 8 lines).
   patching file services/authzone.c
   Hunk #1 succeeded at 3294 (offset 3 lines).
   patching file services/localzone.c
   Hunk #1 succeeded at 1261 (offset 44 lines).
   patching file services/mesh.c
   Hunk #1 succeeded at 1162 (offset 2 lines).
   Hunk #2 succeeded at 1289 (offset 2 lines).
   patching file util/config_file.c
   Hunk #2 succeeded at 562 (offset 9 lines).
   Hunk #3 succeeded at 985 (offset 28 lines).
   Hunk #4 succeeded at 1493 (offset 34 lines).
   patching file util/config_file.h
   patching file util/configlexer.lex
   patching file util/configparser.y
   Hunk #3 succeeded at 239 (offset 2 lines).
   Hunk #4 succeeded at 1397 (offset 22 lines).
   patching file util/data/msgencode.c
   Hunk #3 succeeded at 475 (offset 4 lines).
   Hunk #4 succeeded at 509 (offset 4 lines).
   Hunk #5 succeeded at 557 (offset 3 lines).
   Hunk #6 succeeded at 588 (offset 2 lines).
   Hunk #7 succeeded at 605 (offset 2 lines).
   Hunk #8 succeeded at 619 (offset 2 lines).
   Hunk #9 succeeded at 631 (offset 2 lines).
   Hunk #10 succeeded at 719 (offset 2 lines).
   Hunk #11 succeeded at 772 (offset 2 lines).
   Hunk #12 succeeded at 788 (offset 2 lines).
   Hunk #13 succeeded at 806 (offset 2 lines).
   Hunk #14 succeeded at 823 (offset 2 lines).
   Hunk #15 succeeded at 928 (offset 37 lines).
   Hunk #16 succeeded at 970 (offset 37 lines).
   patching file util/data/msgencode.h
   patching file util/data/msgparse.h
   Hunk #1 succeeded at 209 (offset 2 lines).
   patching file util/data/msgreply.c
   Hunk #1 succeeded at 516 (offset 2 lines).
   Hunk #2 succeeded at 831 (offset 3 lines).
   patching file util/data/msgreply.h
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0005-Adding-hard-limit-for-modified-TTL.patch
   patching file util/data/msgencode.c
   Hunk #1 succeeded at 496 (offset 4 lines).
   patching file util/data/msgparse.h
   patching file util/data/msgreply.c
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0006-Fixing-cases-for-reply-structure-created-from-scratc.patch
   patching file services/mesh.c
   Hunk #1 succeeded at 1398 (offset 5 lines).
   patching file util/data/msgencode.c
   Hunk #1 succeeded at 775 (offset 4 lines).
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0007-Adding-config-switch-for-thread-affinity-could-be-ye.patch
   patching file daemon/worker.c
   Hunk #1 succeeded at 1957 (offset 8 lines).
   patching file util/config_file.c
   Hunk #2 succeeded at 564 (offset 9 lines).
   Hunk #3 succeeded at 988 (offset 28 lines).
   patching file util/config_file.h
   patching file util/configlexer.lex
   patching file util/configparser.y
   Hunk #2 succeeded at 241 (offset 2 lines).
   Hunk #3 succeeded at 1398 (offset 22 lines).
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0008-Adding-dns64-strict-mode.-This-mode-is-enabled-with-.patch
   patching file daemon/worker.c
   Hunk #1 succeeded at 562 (offset 2 lines).
   Hunk #2 succeeded at 770 (offset 5 lines).
   Hunk #3 succeeded at 1957 (offset 8 lines).
   patching file services/authzone.c
   Hunk #1 succeeded at 3297 (offset 3 lines).
   patching file services/localzone.c
   Hunk #1 succeeded at 1263 (offset 44 lines).
   patching file services/mesh.c
   Hunk #1 succeeded at 1165 (offset 2 lines).
   Hunk #2 succeeded at 1292 (offset 2 lines).
   patching file util/config_file.c
   Hunk #2 succeeded at 566 (offset 9 lines).
   Hunk #3 succeeded at 991 (offset 28 lines).
   patching file util/config_file.h
   patching file util/configlexer.lex
   patching file util/configparser.y
   Hunk #2 succeeded at 250 (offset 2 lines).
   Hunk #3 succeeded at 1408 (offset 22 lines).
   patching file util/data/msgencode.c
   Hunk #2 succeeded at 466 (offset 1 line).
   Hunk #3 succeeded at 599 (offset 4 lines).
   Hunk #4 succeeded at 616 (offset 4 lines).
   Hunk #5 succeeded at 631 (offset 4 lines).
   Hunk #6 succeeded at 644 (offset 4 lines).
   Hunk #7 succeeded at 733 (offset 4 lines).
   Hunk #8 succeeded at 790 (offset 4 lines).
   Hunk #9 succeeded at 805 (offset 4 lines).
   Hunk #10 succeeded at 817 (offset 4 lines).
   Hunk #11 succeeded at 865 (offset 4 lines).
   Hunk #12 succeeded at 883 (offset 4 lines).
   Hunk #13 succeeded at 896 (offset 4 lines).
   Hunk #14 succeeded at 991 (offset 39 lines).
   Hunk #15 succeeded at 1040 (offset 39 lines).
   patching file util/data/msgencode.h
   patching file util/data/msgreply.c
   Hunk #1 succeeded at 834 (offset 3 lines).
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0009-Skipping-out-authority-section-creation-for-A-respon.patch
   patching file util/data/msgencode.c
   Hunk #1 succeeded at 816 (offset 9 lines).
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0010-Adding-more-details-for-zone-auth-transfers-and-oper.patch
   patching file daemon/worker.c
   Hunk #1 succeeded at 1024 (offset 19 lines).
   Hunk #2 succeeded at 1041 (offset 19 lines).
   patching file services/authzone.c
   Hunk #1 succeeded at 1572 (offset 11 lines).
   Hunk #2 succeeded at 4934 (offset 61 lines).
   Hunk #3 succeeded at 5038 (offset 64 lines).
   Hunk #4 succeeded at 5099 (offset 64 lines).
   Hunk #5 succeeded at 5230 (offset 65 lines).
   Hunk #6 succeeded at 6107 (offset 69 lines).
   Hunk #7 succeeded at 6186 (offset 69 lines).
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0011-Adding-one-more-corner-case-for-ttl-randomization.patch
   patching file util/data/msgencode.c
   Hunk #1 succeeded at 525 (offset 13 lines).
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0012-yp_dns_support.patch
   patching file config.h
   Hunk #1 succeeded at 771 (offset 1 line).
   patching file daemon/daemon.c
   patching file services/authzone.c
   Hunk #11 succeeded at 2387 (offset 1 line).
   Hunk #12 succeeded at 2430 (offset 3 lines).
   Hunk #13 succeeded at 3247 (offset 3 lines).
   Hunk #14 succeeded at 3277 (offset 3 lines).
   Hunk #15 succeeded at 3316 (offset 3 lines).
   patching file services/authzone.h
   patching file services/listen_dnsport.h
   patching file util/config_file.c
   Hunk #3 succeeded at 374 (offset 8 lines).
   Hunk #4 succeeded at 600 (offset 9 lines).
   Hunk #5 succeeded at 863 (offset 28 lines).
   Hunk #6 succeeded at 1068 (offset 28 lines).
   Hunk #7 succeeded at 1487 (offset 34 lines).
   Hunk #8 succeeded at 1546 (offset 34 lines).
   Hunk #9 succeeded at 1590 (offset 36 lines).
   patching file util/config_file.h
   Hunk #3 succeeded at 710 (offset 17 lines).
   Hunk #4 succeeded at 726 (offset 17 lines).
   Hunk #5 succeeded at 921 (offset 17 lines).
   Hunk #6 succeeded at 1086 (offset 17 lines).
   patching file util/configlexer.lex
   patching file util/configparser.y
   Hunk #2 succeeded at 173 (offset 2 lines).
   Hunk #3 succeeded at 217 (offset 2 lines).
   Hunk #4 succeeded at 367 (offset 6 lines).
   Hunk #5 succeeded at 380 (offset 6 lines).
   Hunk #6 succeeded at 1193 (offset 6 lines).
   Hunk #7 succeeded at 2774 (offset 73 lines).
   patching file util/module.h
   patching file util/netevent.h
   patching file yp_dns/config.cpp
   patching file yp_dns/config.h
   patching file yp_dns/service.cpp
   patching file yp_dns/service.h
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0013-log_start_of_yp_dns_service.patch
   patching file yp_dns/service.cpp
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0014-Add-new-ttl-randomization-algorithm.patch
   patching file daemon/worker.c
   Hunk #2 succeeded at 563 (offset 2 lines).
   Hunk #3 succeeded at 771 (offset 5 lines).
   Hunk #4 succeeded at 1848 (offset 8 lines).
   Hunk #5 succeeded at 1875 (offset 8 lines).
   Hunk #6 succeeded at 2067 (offset 8 lines).
   patching file daemon/worker.h
   patching file libunbound/libworker.c
   Hunk #1 succeeded at 198 (offset 3 lines).
   patching file services/authzone.c
   Hunk #1 succeeded at 3388 (offset 3 lines).
   patching file services/localzone.c
   Hunk #1 succeeded at 1263 (offset 44 lines).
   patching file services/mesh.c
   Hunk #1 succeeded at 1165 (offset 2 lines).
   Hunk #2 succeeded at 1292 (offset 2 lines).
   patching file util/configparser.y
   Hunk #1 succeeded at 1446 (offset 22 lines).
   patching file util/data/msgencode.c
   Hunk #3 succeeded at 506 (offset 4 lines).
   Hunk #4 succeeded at 544 (offset 4 lines).
   Hunk #5 succeeded at 600 (offset 4 lines).
   Hunk #6 succeeded at 639 (offset 4 lines).
   Hunk #7 succeeded at 657 (offset 4 lines).
   Hunk #8 succeeded at 672 (offset 4 lines).
   Hunk #9 succeeded at 685 (offset 4 lines).
   Hunk #10 succeeded at 774 (offset 4 lines).
   Hunk #11 succeeded at 832 (offset 4 lines).
   Hunk #12 succeeded at 847 (offset 4 lines).
   Hunk #13 succeeded at 866 (offset 4 lines).
   Hunk #14 succeeded at 883 (offset 4 lines).
   Hunk #15 succeeded at 991 (offset 39 lines).
   Hunk #16 succeeded at 1041 (offset 39 lines).
   patching file util/data/msgencode.h
   patching file util/data/msgparse.h
   Hunk #1 succeeded at 216 (offset 2 lines).
   patching file util/data/msgreply.c
   Hunk #1 succeeded at 834 (offset 3 lines).
   patching file util/module.h
   patching file util/random.c
   patching file util/random.h
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0016-Fix-enormous-ttl-in-some-cases.patch
   patching file util/data/msgencode.c
   Hunk #1 succeeded at 552 (offset 4 lines).
   Hunk #2 succeeded at 608 (offset 4 lines).
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0017-Add-arcadia-revision-to-version.patch
   patching file config.h
   Hunk #1 succeeded at 743 (offset 2 lines).
   patching file daemon/daemon.c
   patching file daemon/remote.c
   patching file daemon/unbound.c
   patching file smallapp/unbound-anchor.c
   Hunk #2 succeeded at 234 (offset 30 lines).
   Hunk #3 succeeded at 2315 (offset 3 lines).
   patching file smallapp/unbound-checkconf.c
   patching file smallapp/unbound-control.c
   Hunk #2 succeeded at 174 (offset 9 lines).
   Hunk #3 succeeded at 922 (offset 79 lines).
   patching file smallapp/unbound-host.c
   patching file util/version.c
   patching file util/version.h
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0018-Handle-usage-of-new-and-old-ttl-options.patch
   patching file daemon/unbound.c
   patching file util/config_file.c
   patching file util/config_file.h
   patching file util/configparser.y
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0019-Change-verbosity-level-for-recvfrom-failed-errors.patch
   patching file util/netevent.c
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0020-Depth-protect-for-crash-on-deleted-element-timeout.patch
   patching file services/outside_network.c
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0021-Fix-unused-attr-in-dnstap.patch
   patching file dnstap/dnstap.c
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0022-prevent-loops-in-the-reuse-rbtree.patch
   patching file services/outside_network.c
   Hunk #1 succeeded at 866 (offset -26 lines).
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0023-printout-internal-error-and-details.patch
   patching file services/outside_network.c
   Hunk #1 succeeded at 864 (offset -26 lines).
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/devtools/yamaker/projects/unbound/patches/0024-reset-the-dns-message-id-when-moving-queries.patch
   patching file services/authzone.c
   Hunk #1 succeeded at 5303 (offset -139 lines).
   Hunk #2 succeeded at 6153 (offset -139 lines).
   patching file services/outside_network.c
   Hunk #2 succeeded at 400 (offset -10 lines).
   Hunk #3 succeeded at 752 (offset -13 lines).
   Hunk #4 succeeded at 813 (offset -33 lines).
   Hunk #5 succeeded at 1776 (offset -37 lines).
   Hunk #6 succeeded at 2065 (offset -48 lines).
   Hunk #7 succeeded at 2086 (offset -48 lines).
   Hunk #8 succeeded at 2190 (offset -48 lines).
   patching file util/net_help.h
   Hunk #2 succeeded at 95 (offset 2 lines).
   + nix-shell -p dos2unix --run 'find /place/vartmp/yamaker/unbound/destdir -type f -exec dos2unix -k -q {} +'
   bash: warning: setlocale: LC_ALL: cannot change locale (en_US.UTF-8)
   + rsync -rLE --chmod u+w /home/dima-zakharov/arc/arcadia/contrib/tools/unbound/build/ /place/vartmp/yamaker/unbound/destdir/build
   + rsync -rLE --chmod u+w /home/dima-zakharov/arc/arcadia/contrib/tools/unbound/yp_dns/ /place/vartmp/yamaker/unbound/destdir/yp_dns
   + rsync -rLE --chmod u+w --del /place/vartmp/yamaker/unbound/destdir/ /home/dima-zakharov/arc/arcadia/contrib/tools/unbound/
   /home/dima-zakharov/arc/arcadia/contrib/tools/unbound/LICENSE
   ```

   {% endcut %}

1. Проверяем, что все приложилось правильно: смотрим дифф в `contrib/tools/unbound` и пробуем собрать:

   ```sh
   $ arc diff contrib/tools/unbound
   ...
   $ ya make -r contrib/tools/unbound
   Ok
   ```

1. Если все ок, то коммитим изменения вместе с патчем. Пример итогового pr: <https://a.yandex-team.ru/review/1837589>.

## Инструкция: приложение своего патча

1. Заходим в директорию с Unbound:

   ```sh
   cd contrib/tools/unbound
   ```

1. Правим код. Добавляем измененные файлы:

   ```sh
   arc add [changed/added/removed files...]
   ```

1. Сохраняем дифф в файл:

   ```sh
   arc diff --git --cached -U 3 > ../../../yamaker/projects/unbound/patches/<patch-id>-<patch-name>.patch
   ```

1. Добавляем созданный файл с патчем в коммит:

   ```sh
   arc add ../../../devtools/yamaker/projects/unbound/patches/<patch-id>-<patch-name>.patch
   ```

1. Проверяем, что `yamaker` работает корректно с патчем и что Unbound собирается (см. пункты 5 и 6 [предыдущей](#apply-github-patch) инструкции):

   ```sh
   ya make -r devtools/yamaker && ./devtools/yamaker/yamaker import contrib/tools/unbound -nb -la
   ya make -r contrib/tools/unbound
   ```

1. Коммитим и отправляем на ревью:

   ```sh
   arc commit -m <commit message>
   arc pr create -m <pr description> --push
   ```

   Пример итогового ревью: <https://a.yandex-team.ru/review/1906481/files>

## Инструкция: обновление Unbound на новую версию

На примере обновления с **1.13.1** до **1.13.2**.

1. Меняем версию и sha256 в [devtools/yamaker/projects/unbound/default.nix](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/yamaker/projects/unbound/default.nix?rev=r8821469#L4).
   Сделать это можно автоматически командой `bump`:

   ```sh
   ya make -r devtools/yamaker
   ./devtools/yamaker/yamaker bump -v 1.13.2 contrib/tools/unbound
   ```

1. Запускаем `import`:

   ```sh
   ya make -r devtools/yamaker
   ./devtools/yamaker/yamaker import contrib/tools/unbound -la
   ```

1. Исправляем конфликты при накладывании [Аркадийных патчей](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/yamaker/projects/unbound/patches). Аккуратно просматриваем изменения и правим патчи. На этом примере мы получили такую ошибку:

   {% cut "Текст ошибки" %}

   ```sh
   + patch --no-backup-if-mismatch -F0 -p1 -d /place/vartmp/yamaker/unbound/destdir -i /home/dima-zakharov/arc/arcadia/arcadia/devtools/yamaker/projects/unbound/patches/0004-Adding-response-ttl-aglorithm-selection.patch
   patching file daemon/worker.c
   Hunk #1 succeeded at 521 (offset -29 lines).
   Hunk #2 succeeded at 736 (offset -26 lines).
   Hunk #3 succeeded at 1944 (offset -1 lines).
   patching file services/authzone.c
   Hunk #1 succeeded at 3487 (offset 196 lines).
   patching file services/localzone.c
   Hunk #1 succeeded at 1273 (offset 56 lines).
   patching file services/mesh.c
   Hunk #1 succeeded at 1168 (offset 8 lines).
   Hunk #2 succeeded at 1295 (offset 8 lines).
   patching file util/config_file.c
   Hunk #2 succeeded at 572 (offset 19 lines).
   Hunk #3 succeeded at 1000 (offset 43 lines).
   Hunk #4 succeeded at 1515 (offset 56 lines).
   patching file util/config_file.h
   patching file util/configlexer.lex
   patching file util/configparser.y
   Hunk #3 succeeded at 243 (offset 6 lines).
   Hunk #4 succeeded at 1456 (offset 81 lines).
   patching file util/data/msgencode.c
   Hunk #3 succeeded at 475 (offset 4 lines).
   Hunk #4 succeeded at 509 (offset 4 lines).
   Hunk #5 succeeded at 557 (offset 3 lines).
   Hunk #6 succeeded at 588 (offset 2 lines).
   Hunk #7 succeeded at 605 (offset 2 lines).
   Hunk #8 succeeded at 619 (offset 2 lines).
   Hunk #9 succeeded at 631 (offset 2 lines).
   Hunk #10 succeeded at 719 (offset 2 lines).
   Hunk #11 succeeded at 772 (offset 2 lines).
   Hunk #12 succeeded at 788 (offset 2 lines).
   Hunk #13 succeeded at 806 (offset 2 lines).
   Hunk #14 succeeded at 823 (offset 2 lines).
   Hunk #15 succeeded at 928 (offset 37 lines).
   Hunk #16 succeeded at 970 (offset 37 lines).
   patching file util/data/msgencode.h
   patching file util/data/msgparse.h
   Hunk #1 succeeded at 209 (offset 2 lines).
   patching file util/data/msgreply.c
   Hunk #1 succeeded at 524 (offset 10 lines).
   Hunk #2 FAILED at 828.
   1 out of 2 hunks FAILED -- saving rejects to file util/data/msgreply.c.rej
   patching file util/data/msgreply.h
   Traceback (most recent call last):
   File "/home/dima-zakharov/arc/arcadia/arcadia/devtools/yamaker/main.py", line 175, in main
       a.action(a)
   File "/home/dima-zakharov/arc/arcadia/arcadia/devtools/yamaker/main.py", line 303, in do_import
       p.install(extra_args=run_args, dry_run=a.read_only)
   File "/home/dima-zakharov/arc/arcadia/arcadia/devtools/yamaker/project.py", line 571, in install
       super().install(extra_args=extra_args, **kwargs)
   File "/home/dima-zakharov/arc/arcadia/arcadia/devtools/yamaker/project.py", line 384, in install
       run(['patch', '--no-backup-if-mismatch', '-F0', f'-p{strip}', '-d', dstdir, '-i', path])
   File "/home/dima-zakharov/arc/arcadia/arcadia/devtools/yamaker/fileutil.py", line 65, in run
       subprocess.check_call(args)
   File "/home/dima-zakharov/arc/arcadia/arcadia/contrib/tools/python3/src/Lib/subprocess.py", line 373, in check_call
       raise CalledProcessError(retcode, cmd)
   subprocess.CalledProcessError: Command '['patch', '--no-backup-if-mismatch', '-F0', '-p1', '-d', '/place/vartmp/yamaker/unbound/destdir', '-i', '/home/dima-zakharov/arc/arcadia/arcadia/devtools/yamaker/projects/unbound/patches/0004-Adding-response-ttl-aglorithm-selection.patch']' returned non-zero exit status 1.
   ```

   {% endcut %}

   По логу видно, что не получилось наложить патч `0004-Adding-response-ttl-aglorithm-selection.patch` к файлу `util/data/msgreply.c`
   Смотрим, что именно не получилось приложить:

   {% cut "Подробнее" %}

   ```sh
   cat /place/vartmp/yamaker/unbound/destdir/util/data/msgreply.c.rej
   ```

   ```diff
   --- util/data/msgreply.c
   +++ util/data/msgreply.c
   @@ -828,7 +833,7 @@ log_dns_msg(const char* str, struct query_info* qinfo, struct reply_info* rep)
       sldns_buffer* buf = sldns_buffer_new(65535);
       struct regional* region = regional_create();
       if(!reply_info_encode(qinfo, rep, 0, rep->flags, buf, 0,
   -		region, 65535, 1, 0)) {
   +		region, 65535, 1, 0, 0, NULL)) {
           log_info("%s: log_dns_msg: out of memory", str);
       } else {
           char* s = sldns_wire2str_pkt(sldns_buffer_begin(buf),)
   ```

   {% endcut %}

   Скорее всего, что-то изменилось в этой области кода в новом релизе, контекст патча стал неактуален, поэтому не применяется.
   Идем смотреть что изменилось, сравниваем новый код и текущий код в Аркадии:

   {% cut "Подробнее" %}

   ```sh
   vim -d /place/vartmp/yamaker/unbound/destdir/util/data/msgreply.c contrib/tools/unbound/util/data/msgreply.c
   ```

   ![unbdiff](https://jing.yandex-team.ru/files/dima-zakharov/unbdiff.png)

   {% endcut %}

   Видим, что код действительно изменился.
   Также можно найти коммит на ГитХабе, где видны изменения в этом файле: <https://github.com/NLnetLabs/unbound/commit/e9a5f5ab3f387d5982bc36cd97044ce18bf99c3f#diff-b643a22bfbe36c13fd60166600ebc18bfdfaf9892a796a7f96eb859cb95c0ecb>.
   Правим [файл с патчем](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/yamaker/projects/unbound/patches/0004-Adding-response-ttl-aglorithm-selection.patch) так, чтобы контекст соответствовал новому коду.
   Изменения в патче в данном случае выглядят так:

   {% cut "Подробнее" %}

   ```sh
   arc diff devtools/yamaker/projects/unbound/patches/0004-Adding-response-ttl-aglorithm-selection.patch
   ```

   ```diff
   --- devtools/yamaker/projects/unbound/patches/0004-Adding-response-ttl-aglorithm-selection.patch        (index)
   +++ devtools/yamaker/projects/unbound/patches/0004-Adding-response-ttl-aglorithm-selection.patch        (working tree)
   @@ -504,12 +504,12 @@ index 19dfd3f..f055c77 100644
                   struct packed_rrset_data* data = (struct packed_rrset_data*)
                           rep->ref[i].key->entry.data;
   @@ -823,7 +828,7 @@ log_dns_msg(const char* str, struct query_info* qinfo, struct reply_info* rep)
   -       sldns_buffer* buf = sldns_buffer_new(65535);
   -       struct regional* region = regional_create();
   -       if(!reply_info_encode(qinfo, rep, 0, rep->flags, buf, 0,
   +               return;
   +       }
   +       if(!reply_info_encode(qinfo, rep, 0, rep->flags, buf, 0,
   -              region, 65535, 1, 0)) {
   +              region, 65535, 1, 0, 0, NULL)) {
   -               log_info("%s: log_dns_msg: out of memory", str);
   +               log_err("%s: log_dns_msg: out of memory", str);
           } else {
                   char* s = sldns_wire2str_pkt(sldns_buffer_begin(buf),
   diff --git a/util/data/msgreply.h b/util/data/msgreply.h
   ```

   {% endcut %}

   Готово. Перезапускаем `yamaker import` (можно с флагами `-nb`), ошибка применения этого патча должна уйти.
   Однако, теперь `import` может падать при попытке применения следующих патчей.
   Аналогичным образом фиксим остальные патчи, пока ошибок не станет.

1. После всех исправлений патчей нужно проверить сборку и запустить тесты:

   {% cut "Подробнее" %}

   ```sh
   $ ya make -r contrib/tools/unbound
   Ok
   $ ya make -rA infra/unbound/tests
   ...
   infra/unbound/tests <flake8.py3>
   ------ sole chunk ran 7 tests (total:1.14s - test:1.12s)
   [good] conftest.py::py3_flake8 [default-linux-x86_64-release] (0.00s)
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/flake8.py3/testing_out_stuff
   [good] helpers.py::py3_flake8 [default-linux-x86_64-release] (0.00s)
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/flake8.py3/testing_out_stuff
   [good] test_additional_in_query.py::py3_flake8 [default-linux-x86_64-release] (0.00s)
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/flake8.py3/testing_out_stuff
   [good] test_dynamic_zones.py::py3_flake8 [default-linux-x86_64-release] (0.00s)
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/flake8.py3/testing_out_stuff
   [good] test_soa.py::py3_flake8 [default-linux-x86_64-release] (0.00s)
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/flake8.py3/testing_out_stuff
   [good] test_start.py::py3_flake8 [default-linux-x86_64-release] (0.00s)
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/flake8.py3/testing_out_stuff
   [good] test_wildcards.py::py3_flake8 [default-linux-x86_64-release] (0.00s)
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/flake8.py3/testing_out_stuff
   ------ GOOD: 7 - GOOD infra/unbound/tests

   infra/unbound/tests <import_test>
   ------ sole chunk ran 1 test (total:2.56s - test:2.53s)
   [good] infra-unbound-tests::import_test [default-linux-x86_64-release] (1.97s)
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/import_test/testing_out_stuff
   Stdout: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/import_test/testing_out_stuff/infra-unbound-tests.import_test.out
   ------ GOOD: 1 - GOOD infra/unbound/tests

   infra/unbound/tests <py3test> [size:medium] nchunks:224
   ------ [test_additional_in_query.py 0/32] chunk ran 4 tests (total:82.00s - test:81.95s)
   [good] test_additional_in_query.py::TestQueryWithAdditional::test_query_with_unknown_rr[False-False] [tags: usefixtures, parametrize, ticket] [default-linux-x86_64-release] (75.62s)
   Log: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_additional_in_query/chunk0/testing_out_stuff/test_additional_in_query.py.TestQueryWithAdditional.test_query_with_unknown_rr.False-False.log
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_additional_in_query/chunk0/testing_out_stuff
   [good] test_additional_in_query.py::TestQueryWithAdditional::test_query_with_unknown_rr[False-True] [tags: usefixtures, parametrize, ticket] [default-linux-x86_64-release] (1.54s)
   Log: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_additional_in_query/chunk0/testing_out_stuff/test_additional_in_query.py.TestQueryWithAdditional.test_query_with_unknown_rr.False-True.log
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_additional_in_query/chunk0/testing_out_stuff
   [good] test_additional_in_query.py::TestQueryWithAdditional::test_query_with_unknown_rr[True-False] [tags: usefixtures, parametrize, ticket] [default-linux-x86_64-release] (1.42s)
   Log: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_additional_in_query/chunk0/testing_out_stuff/test_additional_in_query.py.TestQueryWithAdditional.test_query_with_unknown_rr.True-False.log
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_additional_in_query/chunk0/testing_out_stuff
   [good] test_additional_in_query.py::TestQueryWithAdditional::test_query_with_unknown_rr[True-True] [tags: usefixtures, parametrize, ticket] [default-linux-x86_64-release] (1.47s)
   Log: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_additional_in_query/chunk0/testing_out_stuff/test_additional_in_query.py.TestQueryWithAdditional.test_query_with_unknown_rr.True-True.log
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_additional_in_query/chunk0/testing_out_stuff
   ------ [test_dynamic_zones.py 0/32] chunk ran 1 test (total:91.57s - test:91.51s)
   [good] test_dynamic_zones.py::TestYpDynamicZones::test_dynamic_zones [tags: usefixtures] [default-linux-x86_64-release] (90.46s)
   Log: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_dynamic_zones/chunk0/testing_out_stuff/test_dynamic_zones.py.TestYpDynamicZones.test_dynamic_zones.log
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_dynamic_zones/chunk0/testing_out_stuff
   ------ [test_soa.py 0/32] chunk ran 1 test (total:91.97s - test:91.91s)
   [good] test_soa.py::TestSOASerialSubstWithYP::test_soa_serial_substitution [tags: usefixtures] [default-linux-x86_64-release] (90.25s)
   Log: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_soa/chunk0/testing_out_stuff/test_soa.py.TestSOASerialSubstWithYP.test_soa_serial_substitution.log
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_soa/chunk0/testing_out_stuff
   ------ [test_start.py 0/32] chunk ran 1 test (total:2.07s - test:2.04s)
   [good] test_start.py::TestStart::test_start [tags: timeout, usefixtures] [default-linux-x86_64-release] (0.51s)
   Log: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_start/chunk0/testing_out_stuff/test_start.py.TestStart.test_start.log
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_start/chunk0/testing_out_stuff
   ------ [test_start.py 1/32] chunk ran 1 test (total:78.18s - test:78.09s)
   [good] test_start.py::TestStartWithYP::test_ready_sensor [tags: usefixtures] [default-linux-x86_64-release] (76.42s)
   Log: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_start/chunk1/testing_out_stuff/test_start.py.TestStartWithYP.test_ready_sensor.log
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_start/chunk1/testing_out_stuff
   ------ [test_wildcards.py 0/32] chunk ran 1 test (total:77.94s - test:77.85s)
   [good] test_wildcards.py::TestAuthWildcardsWithYP::test_wildcards [tags: usefixtures] [default-linux-x86_64-release] (75.28s)
   Log: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_wildcards/chunk0/testing_out_stuff/test_wildcards.py.TestAuthWildcardsWithYP.test_wildcards.log
   Logsdir: /home/dima-zakharov/arc/arcadia/arcadia/infra/unbound/tests/test-results/py3test/test_wildcards/chunk0/testing_out_stuff
   ------ GOOD: 9 - GOOD infra/unbound/tests

   Total 3 suites:
       3 - GOOD
   Total 17 tests:
       17 - GOOD
   Ok
   ```

   {% endcut %}

1. Если все работает, то добавляем все измененные файлы через `arc add`. Коммитим и отправляем на ревью:

   ```sh
   arc commit -m "update to 1.13.2"
   arc pr create -m "[unbound] UNBOUNDREL-3: Update to 1.13.2" --push
   ```

   Итоговое ревью: <https://a.yandex-team.ru/review/2205552/files>
