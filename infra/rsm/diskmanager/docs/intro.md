# Disk manager service

**IMPORTANT this implementation should replace original python diskmanager service located [here](https://a.yandex-team.ru/infra/diskmanager)**

## About
diskmanager is host service for disk/LVM management similar to
[openstorage](https://github.com/libopenstorage/openstorage) or
[CSI](https://github.com/container-storage-interface/spec). Service

## Developments
Service is written on Golang, sources located in Arcadia

* [Sources](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rsm/diskmanager)
* [GPRC API](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rsm/diskmanager/api/diskman.proto)
* [TODO list](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rsm/diskmanager/TODO.org)
### Maintainers
* [Dmitry Monakhov](https://staff.yandex-team.ru/dmtrmonakhov)

## CI/CD
Packages as debian package, build with `ya package`, and deployed as saltstack component
* [main package spec] (https://a.yandex-team.ru/arc/trunk/arcadia/infra/rsm/nvgpu-manager/build/packages/yandex-diskmanager/pkg.json)
* [config package spec] (https://a.yandex-team.ru/arc/trunk/arcadia/infra/rsm/nvgpu-manager/build/packages/yandex-diskmanager-autoformat/pkg.json)
* [testenv job spec](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/runtime_cloud/BuildRuntimeCloudPackages.yaml)
* [testenv job](https://beta-testenv.yandex-team.ru/project/runtime_cloud/job/YANDEX_DISK_MANAGER/history)
* [saltstack deployment spec](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/browse/common/deploy/diskmanager/init.sls)
* [saltstack component versions](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/browse/common/components/diskmanager)

### Monitors
* [RTC service problems status panel](https://yasm.yandex-team.ru/template/panel/HOSTMAN-DAEMONS/-/1)
* [RTC fstrim stats](https://yasm.yandex-team.ru/template/panel/diskman_fstrim/?range=86400000&top_method=maxavg&top_signal=hsum(push-diskmanager_fstrim_errors_hgram)

**FIXME: replace links to diskman ones**
* [RTC_GPU yasm panel](https://yasm.yandex-team.ru/template/panel/rtc_gpu)
* [RTC GPU raw juggler check](https://juggler.yandex-team.ru/raw_events/?query=service%3Dgpumanager)
* [rtc_cpu juggler check](https://juggler.yandex-team.ru/check_details/?host=rtc_gpu&service=gpumanager&last=1DAY)

