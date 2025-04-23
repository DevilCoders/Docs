# logrotate

**logrotate** предназначен для упрощения администрирования систем, с большим количеством лог файлов. Он позволяет автоматически ротировать, сжимать, удалять и отправлять файлы логов по почте. Каждый файл логов можно ротировать ежедневно, еженедельно, ежемесячно или когда он становится слишком большим.

{% note warning %}

Logrotate имеет ограничения!
При скорости записи >= 2 Mb/s logrotate не успевает отротировать старый лог, в то время как новый лог уже становился больше размера ротации.
С каждой итерацией logrotate все больше отстает от скорости заполнения лога.
В итоге лог разрастается, это будет повторяться пока не кончится место на диске.

{% endnote %}


## Реализация в Ya.Deploy {#implementation}

При использовании **logrotate** в контейнере необходимые компоненты поставляются отдельным слоем вне зависимости от их наличия в базовом слое контейнера.
Конфигурация поставляются по стандартному пути, а именно `/etc/logrotate.d/box`.
Запуск **logrotate** осуществляется как запуск еще одного **workload**, периодичность определяется конфигурацией.

Для использования logrotate можно использовать механику слоев. 
1. Создать собственный слой с конфигом. Пример слоя [https://proxy.sandbox.yandex-team.ru/1813087536](https://proxy.sandbox.yandex-team.ru/1813087536)
1. Добавить в спеку конфигурацию logrotate с пустым конфигом для ротации.
1. Добавить слой с конфигом.
1. Удостовериться, что в системе есть пользователь syslog, если нет - создать.

Пример:

```yaml
spec:
  deploy_units:
    DeployUnit1:
      logrotate_configs:
        Box1:
          raw_config: ''
          run_period_millisecond: 10000
      ...
      replica_set:
       ...
          pod_template_spec:
            spec:
	      ...
              pod_agent_payload:
                spec:
                  boxes:
                  - id: Box1
                    rootfs:
                      layer_refs:
                      - base-layer-0
                      - logrotate_config
                  mutable_workloads:
                  - workload_ref: Box1-Workload1
                  resources:
                    layers:
                    - checksum: 'EMPTY:'
                      id: base-layer-0
                      url: rbtorrent:49969bbdbc58134227a8e3276e92d843f0f904b2
                    - checksum: 'EMPTY:'
                      id: logrotate_config
                      url: rbtorrent:0f82327979a9f107876779aa27b52a34a300231c
```

## Конфигурирование {#config}

Как выглядит конфигурация с точки зрения **dctl** или **ui**.
Объекты TDeployUnitSpec содержат в себе конфигурации logrotate на каждый box.

[https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/stage.proto?rev=6852309#L156](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/stage.proto?rev=6852309#L156)

Конфигурация состоит из двух полей, непосредственно сама конфигурация logrotate и периодичность в миллисекундах.

Конфигурация самого инструмента имеет стандартную схему, примеры можно найти в линукс мануале к logrotate.

```yaml
...
spec:
  account_id: abc:service:
  deploy_units:
    DeployUnit1:
      logrotate_configs:
        box_id:
          raw_config: 'config'
          run_period_millisecond: 10000
...
```

**box_id** - идентификатор бокса из спеки стейджа

Пример:

```yaml
spec:
  account_id: abc:service:3494
  deploy_units:
    DeployUnit1:
      logrotate_configs:
        Box1:
          raw_config: 'config'
          run_period_millisecond: 10000
      ...
      replica_set:
        per_cluster_settings:
          ...
        replica_set_template:
	  ...
          pod_template_spec:
            spec:
            ...
              pod_agent_payload:
                spec:
                  boxes:
                  - id: Box1
                    ...
```

**logrotate_configs** - поле, в котором хранятся значения структуры в формате yml, со структурой можно познакомиться в протосхеме [https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/stage.proto?rev=7319450#L336](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/stage.proto?rev=7319450#L336)

**raw_config** - одно из полей типа string, в котором описывается конфигурация в формате конфига logrotate ([https://linux.die.net/man/8/logrotate](https://linux.die.net/man/8/logrotate))
После выкладки в вашем поде по пути `/etc/logrotate.d/box` будет создан файл с содержанием этой переменной.


```yaml
...
spec:
  account_id: abc:service:
  deploy_units:
    DeployUnit1:
      logrotate_configs:
        kebox_idy:
          raw_config: "/var/log/messages {\n    rotate 5\n    weekly\n    postrotate\n        /usr/bin/killall -HUP syslogd\n    endscript\n}\n"
          run_period_millisecond: 10000
...
```

Результат:

```txt
/var/log/messages {
    rotate 5
    weekly
    postrotate
        /usr/bin/killall -HUP syslogd
    endscript
}
```

Должен появится еще один **workload** с **logrotate_\<box-name>**.

Полная поддержка в UI будет сделана в рамках тикета [https://st.yandex-team.ru/DEPLOY-2587](https://st.yandex-team.ru/DEPLOY-2587)

