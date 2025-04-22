# Как релизить реконфигуратор.

До внедрения релизов sandbox тасок как сервисов реконфигуратор релизится в ручном режиме.

По коммиту собирается бинарная sandbox-таска с помощью action-а в новом [CI](https://a.yandex-team.ru/projects/maps-core-ecstatic-coordinator/ci/actions/launches?dir=maps%2Finfra%2Fecstatic%2Fecstatic_reconfigurer&id=build-ecstatic-reconfigurer)

Для релиза реконфигуратора необходимо:

1. Обновить id ресурса в sandbox-шедуллере
2. Обновить id ресурса в [ci registry](https://a.yandex-team.ru/arc_vcs/ci/registry/projects/maps/infra/ecstatic_reconfigurer.yaml)

