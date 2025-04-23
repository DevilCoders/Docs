# PackageSet

> Hostctl примитив позволяющий устанавливать deb пакеты и создавать текстовые файлы на хостах

Spec PackageSet'а состоит из packages и files [proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/ya_salt/proto/ya_salt.proto?rev=7177368#L391)

Пример:
```yaml
meta:
  kind: "PackageSet"
  version: "2.3.2001221352"
  name: "atop"
  delete_requested: False
spec:
  files:
    - path: /etc/logrotate.d/atop
      content: |
        # atop logrotate configuration file
        # this file is managed by salt DO NOT EDIT!

        /var/log/atop/atop.log {
            rotate 6
            daily
            size 400M
            nocompress
            nocreate
            missingok
            prerotate
        	if pidof atop 2>&1 > /dev/null; then
        	    invoke-rc.d atop stop 2>&1 > /dev/null
        	fi
            endscript
            postrotate
        	invoke-rc.d atop start 2>&1 > /dev/null
            endscript
        }
      user: root
      group: root
      mode: 644
    - path: /etc/default/atop
      content: |
        # Options for atop
        # this file is managed by salt DO NOT EDIT!

        ATOP_LOG='/var/log/atop/atop.log'
        ATOP_INTERVAL='60'
      user: root
      group: root
      mode: 644
  packages:
    - name: "atop"
      version: "1.27-3yandex4"
```

## Обновление спеки
  1. При обновлении конфигурации (sha1 от отрендеренной спеки отличается от предыдущей CURRENT ревизии) PortoDaemon'а hostctl'ем создается новая ревизия.
  2. Предыдущей CURRENT ревизия становится REMOVED, применяются действия для ее удаления
     * remove files
     * purge deb pkgs
  3. Из актуальной спеки создается CURRENT ревизия, применяются действия для ее применения
     * install deb pkgs
     * manage fales

## Поддержание юнита активным на хосте
  1. Проверка, что пакеты из спеки установлены
     * Ищем пакеты из спеки в `/var/dpkg/status`
     * Если пакет не установлен, делаем apt install
  2. Проверяем, что файлы из спеки в актуальном состоянии
     * Проверяем отличатся ли реальный файл от описанного в spec
     * Если отличается то атомарно пересоздаем файл

## Мониторинг
> YASM
> * `package-set-{name}-ready_thhh` сигнал со значениями `1` и `0` обозначающий юнит в статусе ready или нет.
>
> Панели
> [package-set](https://yasm.yandex-team.ru/template/panel/hostctl-unit/kind=package-set)

> Juggler
> * `package-set-{name}-ready` - OK когда ready, CRIT в остальных случаях
