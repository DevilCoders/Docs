# SystemService

> Hostctl примитив позволяющий устанавливать deb пакеты и запускать systemd сервис
>
> hostctl берет ответственность за
> * контроль установленных пакетов на хостах
> * systemctl daemon-reload
> * systemctl start <name>
> * systemctl enable <name>

Spec SystemService'а состоит из packages [proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/ya_salt/proto/ya_salt.proto?rev=7339199#L399)

Пример:
```yaml
---
vars:
  # Run only on hosts of wall-e project 'rtc-mtn-hostman' except man1-9002.search.yandex.net
  - name: "stage"
    match:
      - exp: "prj('rtc-mtn-hostman') && !h('man1-9002.search.yandex.net')"
        val: "hostman"
      - exp: "default()"
        val: "absent"
  # Choose version based on stage
  - name: "ver"
    match:
      - exp: "stage == 'hostman'"
        val: "1.0-7345743"
---
meta:
  kind: "SystemService"
  version: "{ver}"
  name: "yandex-hm-reporter"
  #delete_requested: True
  annotations:  # Annotation stage == absent is interpreted as "remove requested"
    stage: "{stage}"
spec:
  packages:
    - name: "yandex-hm-reporter"
      version: "{ver}"
  update_policy:
    method: restart # oneof ['restart', 'reload'] default(restart)
```

## Обновление спеки
  1. При обновлении конфигурации (sha1 от отрендеренной спеки отличается от предыдущей CURRENT ревизии) создается новая ревизия.
  2. Предыдущей CURRENT ревизия становится REMOVED, применяются действия для ее удаления
     * systemctl disable
     * systemctl stop
     * purge apt pkgs
  3. Из актуальной спеки создается CURRENT ревизия, применяются действия для ее применения
     * install deb pkgs
     * systemctl daemon-reload
     * systemctl start
     * systemctl enable

## Поддержание юнита активным на хосте
  1. Проверка, что пакеты из спеки установлены
     * Ищем пакеты из спеки в `/var/dpkg/status`
     * Если пакет не установлен, делаем apt install
  2. Проверяем что systemd сервис active.
     * Проверяем, что systemctl сервис ActiveStatus in ['active', 'activating', 'deactivating']
     * Если не active, делаем
       * systemctl daemon-reload
       * systemctl start/restart
       * systemctl enable

## Мониторинг
> YASM
> * `system-service-{name}-ready_thhh` сигнал со значениями `1` и `0` обозначающий юнит в статусе ready или нет.
> * `system-service-{name}-restart_count_thhh` сколько раз hostman перезапускал systemd сервис с прошлой проверки.
> * `system-service-{name}-running_thhh` сигнал со значениями `1` и `0` обозначающий SubState=running.
> * `system-service-{name}-active_thhh` сигнал со значениями `1` и `0` обозначающий ActiveState in ['active', 'activating', 'deactivating'].
>
> Панели
> [system-service](https://yasm.yandex-team.ru/template/panel/hostctl-unit/kind=system-service)

> Juggler
> * `system-service-{name}-ready` - OK когда ready, CRIT в остальных случаях
> * `system-service-{name}-running` - OK когда running, CRIT в остальных случаях
