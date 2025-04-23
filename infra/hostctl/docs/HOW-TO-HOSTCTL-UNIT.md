# HOW TO HOSTCTL UNIT

1. Собрать deb пакет со своим юнитом

    примеры
    * [SystemService HM-Reporter](https://a.yandex-team.ru/arc_vcs/infra/hmserver/pkg.json)
2. Заводим правило в orly "{kind}-{name}"

    правило в orly будет ограничивать скорость выкладки юнита
    примеры
    * [porto-daemon-juggler-agent-rtc](https://a.yandex-team.ru/arc_vcs/infra/orly/rules/porto-daemon-juggler-agent-rtc.yaml)
    * [system-service-yandex-hm-reporter](https://a.yandex-team.ru/arc_vcs/infra/orly/rules/system-service-yandex-hm-reporter.yaml)
3. Пишем спеку юнита

    подробнее почитать можно в
    * [PackageSet](https://a.yandex-team.ru/arc_vcs/infra/hostctl/docs/PackageSet.md)
    * [PortoDaemon](https://a.yandex-team.ru/arc_vcs/infra/hostctl/docs/PortoDaemon.md)
    * [SystemService](https://a.yandex-team.ru/arc_vcs/infra/hostctl/docs/SystemService.md)
    * [TimerJob](https://a.yandex-team.ru/arc_vcs/infra/hostctl/docs/TimerJob.md)
    * [UNIT](https://a.yandex-team.ru/arc_vcs/infra/hostctl/docs/UNIT.md)
    * [CONTEXT](https://a.yandex-team.ru/arc_vcs/infra/hostctl/docs/CONTEXT.md)
4. Делаем PR со spec юнита в один из репозиториев через который будем выкладывать юнит
    * [sysdev](https://bb.yandex-team.ru/projects/RTCSALT/repos/sysdev)
    * [core](https://bb.yandex-team.ru/projects/RTCSALT/repos/core)
5. После merge смотрим за выкладкой по графикам
    * [YASM](https://yasm.yandex-team.ru/template/panel/hostctl-unit/)
    * [HM-Reporter](http://hm-prestable.in.yandex.net/units)
