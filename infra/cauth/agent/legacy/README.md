# yandex-cauth

Пакет для debian собирается автоматически таской YA_PACKAGE силами аркадийного CI (a.yaml, UI - https://a.yandex-team.ru/projects/hostmanager/ci/actions/launches?dir=infra%2Fcauth%2Fagent%2Flegacy&id=build) при мерже PR в trunk и заливается в common/unstable.
Пакет для rpm можно собрать руками на хосте с centos (проверил на centos 7) командой `ya package --rpm rpm.json`.

После тестирования релиза его нужно не забыть dmove'нуть в stable.

