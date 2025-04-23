## X-Ray

Wiki: https://wiki.yandex-team.ru/security/x-ray/
ST: https://st.yandex-team.ru/XRAY

## Состав

  - [grpc-api](cmd/grpc-api) - основной пользовательский API. Поддерживает OAuth/TVM аутентификацию. Авторизация производится на основе ролей на стейдж в YP
  - [stage-watcher](cmd/stage-watcher) - мониторилка новых стейджей и ревизий. Когда обнаруживает новую ревизию - шедулит её анализ. Использует YT-локи для выбора мастера
  - [worker](cmd/worker) - собственно сама выполнялка задач. Для работы нужен skynet (лучше хостовой) и writable-доступ к porto
  - [xray-cli](cmd/xray-cli) - CLI к сервису. Используется как внутри сервисов для мониторинга живости так и для внешних коммуникаций

### Необходимые дырки
  - grpc-api:
    * `tvm-api.yandex.net:443` - для серверных сетей уже должен быть
    * `blackbox.yandex-team.ru:443` - гранты `oauth`/`user_ticket`
    * `s3.mds.yandex.net:{80,443}` - если прод
    * `s3.mdst.yandex.net:{80,443}` - если dev
    * `_C_YDB_RU_:{31000-32000}`, `ydb-ru.yandex.net:2135` - базюлька
    * `sqs.yandex.net:{8771,443}` - SQS
    * `xdc.yp.yandex.net:8090`, `_YPMASTERSNETS_:8090` - xdc кластер YP + мастера
  - stage-watcher:
    * `_YTNETS_:{80,443,9013}`, `locke.yt.yandex.net:{80,443}` - локи
  - worker:
    * `s3.mds.yandex.net:{80,443}` - если прод
    * `s3.mdst.yandex.net:{80,443}` - если dev
    * `_C_YDB_RU_:{31000-32000}`, `ydb-ru.yandex.net:2135` - базюлька
    * `sqs.yandex.net:{8771,443}` - SQS
    * `dockinfo.yandex-team.ru:443` - резолв докер-образов
    * `storage-int.mds.yandex.net:{80,443}` - выкачивание докер-слоев
    * `proxy.sandbox.yandex-team.ru:443` - для выкачивания порто-слоев из SB, через проксю :/
    * TBD: дырки для выкачивания rbtorrent'ов
    * `xdc.yp.yandex.net:8090`, `_YPMASTERSNETS_:8090` - xdc кластер YP + мастера
    * `yadi.yandex-team.ru:{80,443}` - для работы yadi-os
    * `ant.sec.yandex-team.ru:80,443}` - для работы secret-search
    * `abc-back.yandex-team.ru:{80,443}` - для резолва ABC сервисов
  - xray-cli:
    * `man.sd.yandex.net:8081` - YP.SD (должна быть по дефолту, дополнительно заказывать не нужно)
    * `msk.sd.yandex.net:8081` - YP.SD (должна быть по дефолту, дополнительно заказывать не нужно)
    * `sas.sd.yandex.net:8081` - YP.SD (должна быть по дефолту, дополнительно заказывать не нужно)
    * `vla.sd.yandex.net:8081` - YP.SD (должна быть по дефолту, дополнительно заказывать не нужно)
    * `_XRAY_PROD_NETS_:{8443}` - если прод
    * `_XRAY_TEST_NETS_:{8443}` - если тест
