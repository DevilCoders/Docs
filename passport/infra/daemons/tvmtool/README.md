[Документация](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/).

Тестовый стейдж:
  * [в тестинге Yandex.Deploy](https://test.deploy.yandex-team.ru/project/passp-yandexdeploy-test-stage) - тут можно отлаживаться
  * [в престейбле Yandex.Deploy](https://man-pre.deploy.yandex-team.ru/project/ydeploy-tvmtool-test-stage) - ут отношение как к проду
  * [в проде Yandex.Deploy](https://deploy.yandex-team.ru/project/passp-yandexdeploy-test-stage)

Сборка проекта:
1. [Porto-слой для Yandex.Deploy](https://sandbox.yandex-team.ru/scheduler/18245/view) - следует катить через атрибуты sandbox-ресурса, содержащего слой ([договорённости с Yandex.Deploy](https://st.yandex-team.ru/PASSP-25256#5db96662a2b79e001eac5ba3)):
   * testing - released_sas_test == "True"
   * prestable#1 - released_man_pre == "True"
   * prestable#2 - released_xdc_acceptance == "True"
   * stable - released_xdc == "True"
   * stable - released == "stable" - [договорённость](https://st.yandex-team.ru/PASSPORTSUPPORT-14#611160f30ed23204061529a0)
2. [debian-пакет](https://sandbox.yandex-team.ru/scheduler/14682/view) - следует катить через Кондуктор
3. [Sandbox-ресурс, nmp, pypi, etc...](https://sandbox.yandex-team.ru/scheduler/15211/view) - просто собрать

Куда задавать вопросы
-------------
passport-dev@yandex-team.ru
