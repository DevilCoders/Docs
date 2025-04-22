# Monitoring

## YASM
  * `porto-daemon-{name}-ready_thhh` сигнал со значениями `1` и `0` обозначающий юнит в статусе ready или нет.
  * `package-set-{name}-ready_thhh`
  * `porto-daemon-{name}-respawn_count_thhh` сколько раз portod respawned контейнер с прошлой проверки.
  * `porto-daemon-{name}-restart_count_thhh` сколько раз hostman перезапускал контейнер с прошлой проверки.
  * `porto-daemon-{name}-running_thhh` сигнал со значениями `1` и `0` обозначающий демон запущен.
  * `system-service-{name}-ready_thhh` сигнал со значениями `1` и `0` обозначающий юнит в статусе ready или нет.
  * `system-service-{name}-restart_count_thhh` сколько раз hostman перезапускал systemd сервис с прошлой проверки.
  * `system-service-{name}-running_thhh` сигнал со значениями `1` и `0` обозначающий SubState=running.
  * `system-service-{name}-active_thhh` сигнал со значениями `1` и `0` обозначающий ActiveState in ['active', 'activating', 'deactivating'].

Все эти сигналы представлены вместе на панели [HOSTMAN-PORTODAEMONS](https://yasm.yandex-team.ru/template/panel/HOSTMAN-PORTODAEMONS).

## JUGGLER
  * `porto-daemon-{name}-ready` - OK когда ready, CRIT в остальных случаях
  * `porto-daemon-{name}-running` - OK когда запущен porto контейнер, CRIT в остальных случаях
  * `package-set-{name}-ready`
  * `system-service-{name}-ready` - OK когда ready, CRIT в остальных случаях

  Поверх указанных событий для каждого юнита автоматически строятся агрегаты.
  Для фильтрации агрегатов существует тег [category\_hostman\_unit](
  https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dcategory_hostman_unit).  
  Для отключения построения агрегатов или переопределения их опций необходимо
  выставить [дефолты на директорию или указать опции в юнит файле](
  https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/reconf/HOWTO.md#how-to-override-options-for-hostman-units-checks).
## HM-repporter
В HM-reporter отправляются репорты каждый запуск hostctl в manage режиме

В репорте:
* Name - имя юнита
* Kind - Package-Set или PortoDaemon
* Node - hostname
* Stage - выставляется пользователем meta.annotations.stage. Если пустая `stage=<default>`
* Version - выставляется пользователем meta.version
* LastTransition - время последнего изменения юнита
* ReportTime - время репорта
* Ready

[Как смотерть репорты в разных срезах](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hmserver/docs/HM_REPORTER.md)
