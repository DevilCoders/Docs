# NVIDIA GPU manager service

## About
Resource manager implementation for nvidia gpu devices. Design is heavily influanced by kubernetes/deviceplugin api.

## Developments
Service is written on Golang, sources located in Arcadia

* [Sources](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rsm/nvgpumanager)
* [GPRC API](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rsm/nvgpumanager/api/nvgpu.proto)
* [TODO list](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rsm/nvgpumanager/TODO.org)
### Maintainers
* [Dmitry Monakhov](https://staff.yandex-team.ru/dmtrmonakhov)

## CI/CD
Packages as debian package, build with `ya package`, and deployed as saltstack component

* [package spec](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rsm/nvgpumanager/build/packages/yandex-nvgpu-manager/pkg.json)
* [ci-flow-release](https://arcanum.yandex-team.ru/ci/infracloudnetwork/releases/timeline?dir=infra%2Frsm%2Fnvgpumanager&id=infra-rsm-nvgpumanager-release)
* ~~[testenv job spec](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/runtime_cloud/BuildRuntimeCloudPackages.yaml)~~
* ~~[testenv job yandex-nvgpu-manager](https://beta-testenv.yandex-team.ru/project/runtime_cloud/job/YANDEX_NVGPU_MANAGER/history?limit=20)~~
* [saltstack component](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/browse/common/components/nvidia)
* [saltstack deploy](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/browse/common/deploy/nvidia)

### Monitors
* [RTC_GPU yasm panel](https://yasm.yandex-team.ru/template/panel/rtc_gpu)
* [gpumanager juggler raw events](https://juggler.yandex-team.ru/raw_events/?query=service%3Dgpumanager)
* [gpumanager juggler aggregates](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Dgpumanager)
* [Version chart](https://oops.yandex-team.ru/?q=checkin+%3C+30+%26%26+versions.packages+!%3D+null+%26%26+versions.packages%5B%27yandex-nvgpu-manager%27%5D+!%3D+null+group+versions.packages%5B%27yandex-nvgpu-manager%27%5D)
