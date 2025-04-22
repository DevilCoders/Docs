# Goals
В RTC заведено множество проектов Wall-E с разной конфигурацией и требованиями.

Данный набор тестов обеспечивает соответствие заведённых проектов определённому набору правил, гарантирующих непротиворечивость созданной оператором конфигурации.

Настройки проектов читаются из папки [projects](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/walle_validator/projects) и обновляются планировщиком в Sandbox. Подробности доступны по ссылке.

Список тэгов доступен в [wiki](https://wiki.yandex-team.ru/runtime-cloud/walle-projects/), устарело.

# Tags:

В этом разделе можно найти краткий справочник тэгов и их значений:

* `rtc` - определяет все проекты на балансе RTC
* `yasm_monitored` - все хосты которые попадают в метагруппу ASEARCH Golovan
* `yasm_qloud_monitored` - все хосты которые попадают в метагруппу QLOUD Golovan
* `yt` - проекты YT, из них формируются группа gencfg `G@ALL_YT`
* `yp` - проекты YP, из них формируются группа gencfg `G@ALL_YP`
* `runtime` - проекты GenCfg, из них формируются группа gencfg `G@ALL_RUNTIME`
* `qloud` - проекты Qloud, из них формируются группа gencfg `G@ALL_QLOUD`
* `skynet_installed` - тэг для настройки skynet на хостах
* `rtc.isscacher-<value>` - указывает агенту iss какой cacher использовать
    * `adm` - админский iss cacher
    * etc
* `rtc.ypmaster-<value>` - указывает агенту iss какой yp master использовать
    * `sas`
    * `man`
    * `vla`
    * `iva`
    * `myt`
    * `sas_test`
    * `man_pre`
* `rtc.stage-<value>` - определяет принадлежность проекта к конкретному контуру
    * `experiment` - экспериментальные проекты без production
    * `prestable` - проекты prestable, production с SPI без LSR
    * `production` - боевые проекты
    * `core` - проекты админского контура, любые обновления должны быть развязаны с изменениями в production
* `rtc.reboot_segment-<segment>` - сегменты хостов, которые можно ребутать независимо
    * `experiment` - хосты экспериментального контура
    * `prestable-def` - хосты prestable контура без YT
    * `prestable-yt` - хосты YT в prestable контуре
    * etc
* `rtc.automation-<value>` - целевое состояние автоматики на проекте
    * `enabled` - на проекте должна быть включена автоматика
    * `disabled` - на проекте должна быть выключена автоматика
* `rtc.cohabitation-<value>` - сожительство GenCfg с подами YP
    * `enabled` - на проекте настроено сожительство подов gencfg и yp, https://st.yandex-team.ru/YP-2604
* `rtc.gencfg-<value>` - Если у хостов есть тег rtc.gencfg-${gencfg-group-name}, то все хосты этого wall-e
                         проекта не входящие в мастер группы (не считая ALL_UNSORTED_* и приравленных к ним)
                         будут автоматически переноситься в заданную группу.
                         Несмотря на то, что некоторые проекты имеют такие теги, по факту, описанная выше автоматика
                         не работает, и не факт, что уже будет.
                         Скорее всего, теги такого вида - кандидаты на удаление.
    * `reserve` - хосты распределяются в резерв gencfg ([SAS/MAN/VLA/MSK]_RESERVED + RESERVE_SELECTED по
                  алгоритму из ./utils/hardware/move_hosts.py (на самом деле - нет, см. RX-1062)
* `rtc.gpu-<value>` - определяет наличие / отсутствие GPU на хосте
    * `nvidia` - GPU используется в контейнерах, используется общий для всех контейнеров драйвер nvidia
    * `vfio` - GPU на хостах проекта будут прокинуты в qemu виртуалки, драйвер nvidia не устанавливается
    * `none` - ожидается что GPU на хостах проекта отсутствует
* `rtc.yt_cluster-<cluster_name>` - имя кластера [YT](https://yt.yandex-team.ru/)
    * `hahn` - например, кластер Hahn
    * etc
*  `rtc.infiniband-<value>` - 
    * `enabled` - означает наличие задействованных infiniband интерфейсов и соответствующей автоматизации починок
    * `none` - означает отсутствие IB интерфейсов и отключение соответствующей автоматики починок
Список разрешённых тэгов можно найти по [ссылке](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/walle_validator/lib/constants.py#L6).

# Roles

Логика выдачи ролей описана в [коде](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/walle_validator/lib/transform.py?rev=7259946#L64). Регламент выдачи доступов описан в [wiki](https://wiki.yandex-team.ru/runtime-cloud/access-regulations/).

## `noc_access`

Выдаётся на все проекты RTC группе [@svc_doortortc](https://abc.yandex-team.ru/services/doortortc/) для дебага сетевых проблем.

Пользователь получит доступ на хосты по SSH и беспарольный sudo или `cap_net_raw,cap_net_admin` на:
* /usr/sbin/tcpdump
* /sbin/ip
* /sbin/ethtool
* /bin/ping
* /bin/ping6
* /bin/netstat
* /usr/sbin/ya-hbf-*

Sudoers настраивается пакетом [yandex-rtc-duty-perms](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/packages/yandex-rtc-duty-perms).

## `user`

Используется поддержкой RTC и смежными командами для дебага и саппорта сервисов пользователей / sidecar-ов / инфраструктурных агентов.

Выдаётся на все проекты RTC группе [@svc_rtcsupport](http://abc.yandex-team.ru/services/rtcsupport) для любых действий с хостами и парольным sudo.

К проектам с тэгами `rtc.scheduler-yp` и `rtc.scheduler-gencfg` разрешён доступ для [@svc_logbroker_devops](https://abc.yandex-team.ru/services/logbroker?scope=devops), [@svc_ya_agent_devops](https://abc.yandex-team.ru/services/ya_agent?scope=devops) и [@svc_dutysearch_devops](https://abc.yandex-team.ru/services/dutysearch?scope=devops).

## `superuser`

Используется разработчиками RTC.

Выдаётся на все проекты RTC группе [@svc_srertc_devops](https://abc.yandex-team.ru/services/srertc/?scope=devops) для любых действий с хостами и беспарольным sudo.

# Automation scheme

Схемы автоматики позволяют показывать проверки с хоста прямо в Wall-E или реагировать на них автоматически.

В RTC используются следующие схемы:
* [rtc](https://wall-e.yandex-team.ru/automation_plots/rtc)
* [qloud](https://wall-e.yandex-team.ru/automation_plots/qloud)
* [rtc-incoming](https://wall-e.yandex-team.ru/automation_plots/rtc-incoming)
* [rtc-gpu](https://wall-e.yandex-team.ru/automation_plots/rtc-gpu)

Тесты описаны в [test_check_schemas.py](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/walle_validator/tests/test_check_schemas.py).

На текущий момент используются следующие проверки:
* [walle_clocksource](https://a.yandex-team.ru/arc/trunk/arcadia/infra/wall-e/checks/walle_clocksource.py) сообщает о том, что ядро использует некачественный источник времени
* [walle_fstab](https://a.yandex-team.ru/arc/trunk/arcadia/infra/wall-e/checks/walle_fstab.py) сообщает о том, что часть файловых систем не смонтирована
* `walle_firmware` проверяет наличие новых версий прошивок, пушится hw-watcher (из центральной точки)
* [ll_duplicate_addr](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/bundle/checks/ll_duplicate_addr/README.md) сообщает о том, что обнаружена коллизия контейнерных подсетей, требуется переткнуть порт вручную
* [net64_check](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/bundle/external/net64_check.sh) проверяет [корректность](https://wiki.yandex-team.ru/runtime-cloud/monitoring_fix/#net64) конфигурации сети на хосте (в том числе из контейнеров в mtn)
* `need_reboot_kernel` информирует о том, что установлено новое ядро и хост нужно перезагрузить, пушится host manager, используется [maxwell](http://maxwell.in.yandex-team.ru)
* `certman` сообщает о том, что сертификат на хосте истёк и хост должен быть переналит, пушится host manager
* `hostman-ready` показывает что хост успешно настроен host manager-ом в первый раз, пушится host manager
* `hostman-distrib` показывает что дистрибутив хоста устарел, пушится host manager
* [walle_hotfix](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/bundle/checks/walle_hotfix) перегружает хост если обнаружены известные и ещё не исправленные проблемы в ядрах
* [portod_tasks](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/bundle/checks/portod_tasks/README.md) показывает работоспособность porto
* [check_iss_agent](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/bundle/external/check_iss_agent.py) показывает работоспособность ISS Agent
* [check_skynet_procs](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/bundle/external/check_skynet_procs.py) показывает состояние SkyNet на хосте

# Projects

## RnD
Проекты, в которых предполагается тестирование железок совместно с RnD:
* [yp-testing-rnd](https://wall-e.yandex-team.ru/project/yp-testing-rnd) - experiment окружение YP
* [yp-prestable-rnd](https://wall-e.yandex-team.ru/project/yp-prestable-rnd) - prestable окружение YP
* [yp-iss-man-yt-hume-rnd](https://wall-e.yandex-team.ru/project/yp-iss-man-yt-hume-rnd) - prestable окружение YT в Hume
* [yp-iss-vla-yt-arnold-rnd](https://wall-e.yandex-team.ru/project/yp-iss-vla-yt-arnold-rnd) - prestable окружение YT в Arnold

В данных проектах специально отключена автоматика починки и выданы доступ команде RnD.

# CLI

CLI можно найти в папке [cli](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/walle_validator/cli).

Токены для:
* [Setup](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=7936b3deca204cd194b82b7db548a3b0)
* [Wall-E](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9e9702c0b7f54152ac339989d9039ccd)

# Monitoring

Juggler:
* [Выполнение](https://juggler.yandex-team.ru/check_details/?host=backup-walle-project&service=scheduler) задачи на обновление конфигов в репозитории
* [Прохождение](https://juggler.yandex-team.ru/check_details/?host=test-walle-project&service=scheduler) конфигами проектов набора тестов

# Cron

* Projects are periodically updated with [BACKUP_WALLE_PROJECTS](https://sandbox.yandex-team.ru/scheduler/15033/view).
* Tests are scheduled with [TEST_WALLE_PROJECTS](https://sandbox.yandex-team.ru/scheduler/15722/view).

# CI

Данный артефакт нужен для того, чтобы сдампить проекты в репозиторий в нужном формате. Будьте внимательны если меняете формат спеки проекта. Лучше сначала закоммитить изменение спеки, а затем уже коммитить тесты на новую часть спеки, если это возможно.

* [TestEnv](https://beta-testenv.yandex-team.ru/project/runtime_cloud/job/YANDEX_WALLE_VALIDATOR_CLI/history?limit=20)

# Workflow
Каждое изменение настроек проектов требует изменения в сохранённых конфигах проектов,
в тестах, которые проверяют корректность, и в настройках проектов в Wall-E.
Если изменять настройки и тесты независимо, то у нас гарантированно зазвенит мониторинг.
Чтобы снизить вероятность срабатывания мониторинга при работах, предлагается использовать
довольно простой workflow. Предлагаемый workflow использует даёт дополнительную защиту
от ошибок за счёт предварительной валидации изменений.

1. С большой долей вероятности изменения в настройках проекта потребуют изменения в тестах.
Перым делом, редактируем тест и запускаем его, чтобы увидеть, что текущие настройки проектов
_некорректные_ с точки зрения новой логики. Если нужного теста нет – его необходимо написать.
2. Вносим предполагаемые изменения в сохранённые конфигурационные файлы и запускаем тесты,
чтобы убедиться, что новые настройки _корректны_ с точки зрения новой логики.
3. Делаем изменения в настройках Wall-E-проектов.
4. Запускаем синхронизацию сохранённых конфигурационных файлов с Wall-E, чтобы в репозитории
были не изменённые вручную конфиги, а засинхронизированные настройки.
Синхронизация происводится с помощью `cli`
5. Запускаем тесты локально, чтобы убедиться, что _реальные_ настройки проектов соответствуют новой логике.
6. Делаем коммит со skip-check, чтобы новые изменения в логике тестов выкатились быстрее, уменьшив окно,
во время которого может сработать мониторинг.

Если во время работы мониторинг

# Configration changes

ВНИМАНИЕ! Заливка конфигураций проектов протестирована не полностью, стоит отревьювить код записи ещё раз.

В случае если требуется поменять конфигурацию множества проектов лучше воспользоваться следующим подходом. Для этого в файле [transform.py](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/walle_validator/lib/transform.py) следуюет написать нужные преобразования.

Запускаем трансормацию проектов:

    cd $ARCADIA_ROOT/infra/rtc/walle_validator/cli
    ./cli transform

Запускаем тесты на валидность конфигурации проектов:

    ya make -r -tt ../

Проверяем результаты трансформации:

    arc diff ../

Затем ревьювим diff с продом:

    ./cli upload

После чего пушим конфигурацию проектов:

    ./cli upload -p

# Test development

Запуск тестов ничем не отличается от запуска тестов в Аркадии:

    ya make -r -A

Чтобы протестировать настройки каждого проекта используйте фикстуру `project`, если же для теста нужны все проекты, то `all_projects`.

Для того чтобы тест запускался для определённого подмножества проектов используйте метку `pytest.mark.project_filter`, набор доступных условий можно посмотреть в модуле `infra.rtc.walle_validator.lib.filters`.

В случае если необходимо гарантировать что набор тестов покрывает все проекты, при этом используются вышиванки, нужно воспользоваться следующим рецептом:

```
import pytest

from infra.rtc.walle_validator.lib.filters import HasTag
from infra.rtc.walle_validator.lib.coverage import create_coverage
from infra.rtc.walle_validator.lib.constants import RUNTIME_TAG, YP_TAG

deploy_coverage = create_coverage()


@pytest.mark.project_filter(HasTag(RUNTIME_TAG), deploy_coverage)
def test_runtime_deploy_config(project):
    pass


@pytest.mark.project_filter(HasTag(YP_TAG), deploy_coverage)
def test_yp_deploy_config(project):
    pass


def test_deploy_coverage(all_projects):
    deploy_coverage.check(all_projects)
```

В случае если тестами покрыт не весь набор проектов то упадёт тест `test_deploy_coverage`.
