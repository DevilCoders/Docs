# DOCKERFILE_RUNS_INIT

Requires `maps_init` to be invoked in the Dockerfile.

## Rationale
The special `maps_init` comand is used to bootstrap the infrastructure configs for your project on build-time. For example it prepares configs for monitorings, graphics and alerts.

## Solution
Add command `RUN maps_init` in your Dockerfile.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/arc/docker-file.test.ts#L63-68)_
