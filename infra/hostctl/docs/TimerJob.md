# TimerJob

> Hostctl примитив для организации периодических повторяющихся действий на машине.

Примеры:
  * настройка sysctl (и периодический enforce)
  * настройка timezone (и опять периодический enforce)

Т.к. `hostctl` занимается только **организацией**, то основные действия делегируются .deb пакетам и systemd. Конкретно:
  * `<unit-name>.service` юнит с типом `Type=oneshot`, который выполняет основные действия
  * `<unit-name>.timer` юнит, настроенный на нужную периодичность запуска основного сервиса
  * (опционально) .deb пакет(ы) с нужными исполняемыми файлами и юнитами systemd, описанными выше
  * (опционально) inline файлы для тонкой/оперативной настройки

Важно: файлы юнитов должны быть самостоятельно установлены (например, через .deb пакет).

**Важно: юнит запускаемый таймером должен быть kind=oneshot и выставлена опция RemainAfterExit=no**
https://stackoverflow.com/a/38377069/2576185

**Важно: монотонные таймеры OnUnitActiveSec и OnUnitInactiveSec**
* Монотонным таймерам основанным на `OnUnitActiveSec` и `OnUnitInactiveSec` необходимо прописывать
  `Requires=<запускаемый>.service` в секцию `[Unit]` чтобы избежать эпизодических переходов таймера в состояние `elapsed`
  в котором таймер перестает запускать сервис. Актуально для `systemd=229-4ubuntu21.27yandex1`.
  Детали в [HOSTMAN-1091](https://st.yandex-team.ru/HOSTMAN-1091) и [HOSTMAN-1044](https://st.yandex-team.ru/HOSTMAN-1044).
  Вероятно в более свежих версиях systemd этот пункт потеряет актуальность, т.к. это кажется [починили](https://github.com/systemd/systemd/pull/10778/commits/cf31f2747a6f9f916c917a85b172a1aaabc3e645).
* Дополнять их опциями `OnBootSec=` и `OnStartupSec=` для того чтобы стриггерить первый запуск сервиса не требуется
  т.к. сервис будет запущен при загрузке машины если в нем прописан `WantedBy=multi-user.target` или что-то подобное.

После этого hostctl берет ответственность за
 * контроль установленных пакетов и файлах на хостах
 * `systemctl daemon-reload`
 * `systemctl start <name>` для systemd юнита и таймера
 * `systemctl enable <name>` для systemd юнита и таймера

Spec TimerJob'а состоит из [proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/ya_salt/proto/ya_salt.proto?rev=7339199#L399)

Пример:
```yaml
# HOSTMAN-696
vars:
  - name: "stage"
    match:
      - exp: "default()"
        val: "stable"
---
meta:
  kind: "TimerJob"
  version: "default"
  name: "timezone-sync"
  annotations:
    stage: "{stage}"
    reconf-juggler: |+
      doc_url: "https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/docs/units/timezone-sync.md"
spec:
  files:
    - path: "/etc/systemd/system/timezone-sync.service"
      content: |+
        [Unit]
        Description=Set timezone via timedatectl
        After=time-sync.target

        [Service]
        Type=oneshot
        RemainAfterExit=no
        ExecStart=/usr/bin/timedatectl set-timezone Europe/Moscow

        [Install]
        WantedBy=multi-user.target
    - path: "/etc/systemd/system/timezone-sync.timer"
      content: |+
        [Unit]
        Description=Run timezone-sync dayly and on boot

        [Timer]
        OnBootSec=30sec
        OnUnitActiveSec=1d
        RandomizedDelaySec=30min

        [Install]
        WantedBy=timers.target
```

## Обновление спеки
  1. При обновлении конфигурации (sha1 от отрендеренной спеки отличается от предыдущей CURRENT ревизии) PortoDaemon'а hostctl'ем создается новая ревизия.
  2. Предыдущей CURRENT ревизия становится REMOVED, применяются действия для ее удаления
     * systemctl disable <name>.timer
     * systemctl stop <name>.timer
     * systemctl disable <name>.service
     * systemctl stop <name>.service
     * purge apt pkgs
  3. Из актуальной спеки создается CURRENT ревизия, применяются действия для ее применения
     * install deb pkgs
     * systemctl daemon-reload
     * systemctl start <name>.service
     * systemctl enable <name>.service
     * systemctl start <name>.timer
     * systemctl enable <name>.timer

## Поддержание юнита активным на хосте
  1. Проверка, что пакеты из спеки установлены
     * Ищем пакеты из спеки в `/var/dpkg/status`
     * Если пакет не установлен, делаем apt install
  2. Проверяем что systemd юнит и таймер active.
     * Проверяем, что systemctl сервис ActiveStatus in ['active', 'activating', 'deactivating']
     * Если не active, делаем
       * systemctl daemon-reload
       * systemctl start/restart
       * systemctl enable

## Мониторинг
> YASM
> * `timer-job-{name}-ready_thhh` сигнал со значениями `1` и `0` обозначающий юнит в статусе ready или нет.
> * `timer-job-{name}-restart_count_thhh` сколько раз hostman перезапускал systemd сервис с прошлой проверки.
> * `timer-job-{name}-running_thhh` сигнал со значениями `1` и `0` обозначающий SubState=running.
> * `timer-job-{name}-active_thhh` сигнал со значениями `1` и `0` обозначающий ActiveState in ['active', 'activating', 'deactivating'].
>
> Панели
> [timer-job](https://yasm.yandex-team.ru/template/panel/hostctl-unit/kind=timer-job)

> Juggler
> * `timer-job-{name}-ready` - OK когда ready, CRIT в остальных случаях
> * `timer-job-{name}-running` - OK когда running, CRIT в остальных случаях
