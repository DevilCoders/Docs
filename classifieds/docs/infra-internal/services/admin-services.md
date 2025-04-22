# Сервисы и батч-джобы группы эксплуатации

В этой документации собрана информация о сервисах и батч-джобах, поддерживаемых командой админов.

Сервис | Что делает | Мониторинг | Ответственный
:---: | :---: | :---: | :---:
[auto-scaling](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/auto-scaling.yml) | Метрики Prometheus -> Я.Облако для автоскейлинга | [logs](https://grafana.vertis.yandex-team.ru/goto/h6-mGn17z?orgId=1) [dashboard](https://grafana.vertis.yandex-team.ru/goto/h0nHwV17k?orgId=1) | [@mariausova](https://staff.yandex-team.ru/mariausova)
[geodata-transfer](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/geodata-transfer.yml) | Доставка geodata6.bin в s3 | [logs](https://grafana.vertis.yandex-team.ru/goto/gA2nM71nk?orgId=1) | [@mariausova](https://staff.yandex-team.ru/mariausova)
[github-actions-monitoring](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/github-actions-monitoring.yml) | Мониторинг использования внешних раннеров в github-actions | [logs](https://grafana.vertis.yandex-team.ru/goto/T5mHMn17z?orgId=1) | [@mariausova](https://staff.yandex-team.ru/mariausova)
[github-backup](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/github-backup.yml) | Бэкап гитхаба в s3 | [logs](https://grafana.vertis.yandex-team.ru/goto/WiUNG7Jnz?orgId=1) | [@mariausova](https://staff.yandex-team.ru/mariausova)
[github-metrics](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/github-metrics.yml) | Сбор метрик про Github Actions | [logs](https://grafana.vertis.yandex-team.ru/goto/-l8vMn1nz?orgId=1) | [@mariausova](https://staff.yandex-team.ru/mariausova)
[grafana-infra-sync](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/grafana-infra-sync.yml) | Синк аннотаций infra -> Grafana | [logs](https://grafana.vertis.yandex-team.ru/goto/3I8BM7J7k?orgId=1) [dashboard](https://grafana.vertis.yandex-team.ru/d/G7AUcZm7z/grafana-infra-sync?orgId=1&refresh=30s) | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman)
[nomad-metrics](hhttps://a.yandex-team.ru/arc_vcs/classifieds/services/maps/nomad-metrics.yml) | Сбор метрик про Nomad | [logs](https://grafana.vertis.yandex-team.ru/goto/xHuVM7J7z?orgId=1) | [@mariausova](https://staff.yandex-team.ru/mariausova)
[prolomon](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/prolomon.yml) | Метрики Solomon -> Prometheus | [logs](https://grafana.vertis.yandex-team.ru/goto/bVPpMnJnz?orgId=1) | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky)
[rudolfs](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/rudolfs.yml) | LFS | [logs](https://grafana.vertis.yandex-team.ru/goto/Fgz0M7J7z?orgId=1) | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky)
[teamcity-metrics](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/teamcity-metrics.yml) | Сбор метрик про TeamCity | [logs](https://grafana.vertis.yandex-team.ru/goto/vuEdGn1nz?orgId=1) | [@mariausova](https://staff.yandex-team.ru/mariausova)
[vertis-st-updater](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/vertis-st-updater.yml) | Проставление дежурного в VASUP | [logs](https://grafana.vertis.yandex-team.ru/goto/rDmFG7J7k?orgId=1) | [@mariausova](https://staff.yandex-team.ru/mariausova)
[yt-perelivka-form](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/yt-perelivka-form.yml) | Синхронизация списка сервисов для переливок в YT | [logs](https://grafana.vertis.yandex-team.ru/goto/wsNyM7Jnz?orgId=1) | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman)
