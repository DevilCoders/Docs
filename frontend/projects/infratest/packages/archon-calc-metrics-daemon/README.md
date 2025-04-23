# archon-calc-metrics-daemon

Компонент [calc_metrics_daemon](https://wiki.yandex-team.ru/logs/calcmetricsdaemon/) для [Archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html)

## Компоненты Archon

### CalcMetricsDaemon

Компонент, запускающий calc_metrics_daemon.

* `init`: запуск calc_metrics_daemon
  * при успешном запуске сервера `init` компонента будет `fulfilled` с объектом, содержащим номер порта сервера в
    поле `port`
  * при неуспехе запуска сервера `init` компонента будет `rejected` с ошибкой-причиной
* `shutdown`: отправка SIGINT calc_metrics_daemon'у
* `terminate`: отправка SIGKILL calc_metrics_daemon'у

Компонент зависит от следующих компонентов:

* `sb-resource-calc-metrics-daemon` - компонент, загружающий `calc_metrics_daemon`
* `sb-resource-blockstat-dict` - компонент, загружающий `blockstat_dict`
* `sb-resource-sessions-geo-helper` - компонент, загружающий `sessions_geo_helper`
* `sb-resource-sessions-user-type-resolver` - компонент, загружающий `sessions_user_type_resolver`
