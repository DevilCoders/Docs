Подсмотрел здесь: https://a.yandex-team.ru/arc_vcs/grut/tools/ci?rev=r9303295

Просто выполнить команду из корня Аркадии:
1. saas2: `ya make ./ads/quality/adv_machine/tools/ci/ -r && ./ads/quality/adv_machine/tools/ci/am_configure_ci --mode saas2 > ./ads/quality/adv_machine/saas2/a.yaml`
2. common: `ya make ./ads/quality/adv_machine/tools/ci/ -r && ./ads/quality/adv_machine/tools/ci/am_configure_ci --mode common > ./ads/quality/adv_machine/a.yaml`
