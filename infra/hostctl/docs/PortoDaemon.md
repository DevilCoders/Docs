# PortoDaemon

> Hostctl примитив позволяющий устанавливать deb пакеты и запускать porto контейнер на хостах

Spec PortoDaemon'а состоит из properties и packages [proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/ya_salt/proto/ya_salt.proto?rev=7177368#L167)

Пример:
```yaml
meta:
  kind: "PortoDaemon"
  version: "2.3.2001221352"
  name: "juggler-agent-rtc"
  delete_requested: False
spec:
  properties:
    virt_mode: "host"
    cmd:
      - "/usr/bin/juggler-client"
      - "--pid-file"
      - "/var/run/juggler-client.pid"
      - "--lock-file"
      - "/var/run/juggler-client.pid"
      - "--config-dir"
      - "/etc/juggler/"
    isolate: "false"
    user: "monitor"
    group: "monitor"
    controllers:
      devices: "false"
    memory_guarantee: "600Mb"
    memory_limit: "2Gb"
    cpu_guarantee: "0.5c"
    cpu_limit: "3c"
  packages:
    - name: "juggler-client-core"
      version: "2.3.2001221352"
    - name: "yandex-rtc-juggler-config"
      version: "1.0-6238270"
```

## Обновление спеки
  1. При обновлении конфигурации (sha1 от отрендеренной спеки отличается от предыдущей CURRENT ревизии) PortoDaemon'а hostctl'ем создается новая ревизия.
  2. Предыдущей CURRENT ревизия становится REMOVED, применяются действия для ее удаления
     * porto disable
     * porto kill
     * porto destroy
     * purge apt pkgs
  3. Из актуальной спеки создается CURRENT ревизия, применяются действия для ее применения
     * install apt pkgs
     * porto start

## Поддержание юнита активным на хосте
  1. Проверка, что пакеты из спеки установлены
     * Ищем пакеты из спеки в `/var/dpkg/status`
     * Если пакет не установлен, делаем apt install
  2. Проверяем, что porto контейнер запущен.
     * Смотрим статус porto контейнера
     * Если контейнер запущен не в актуальной конфигурации или не запущен, запускаем контейнер

## Мониторинг
> YASM
> * `porto-daemon-{name}-ready_thhh` сигнал со значениями `1` и `0` обозначающий юнит в статусе ready или нет.
> * `porto-daemon-{name}-respawn_count_thhh` сколько раз portod respawned контейнер с прошлой проверки.
> * `porto-daemon-{name}-restart_count_thhh` сколько раз hostman перезапускал контейнер с прошлой проверки.
> * `porto-daemon-{name}-running_thhh` сигнал со значениями `1` и `0` обозначающий демон запущен.
>
> Панели
> [porto-daemon](https://yasm.yandex-team.ru/template/panel/hostctl-unit/kind=porto-daemon)

> Juggler
> * `porto-daemon-{name}-ready` - OK когда ready, CRIT в остальных случаях
> * `porto-daemon-{name}-running` - OK когда running, CRIT в остальных случаях
