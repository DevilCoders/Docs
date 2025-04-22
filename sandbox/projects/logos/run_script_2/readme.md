# Run Script 2

Универсальный запускатель скриптов и бинарей на sdk2.

## Использование

```yaml
# Любая shell команда
# {resource} - найденный ресурс, который подставится вместо заглушки
# также можно использовать ключи из sb_resources и arc_resources 
cmdline: DEBUG=$DEBUG {resource} --conf {resource_3} && echo "Done!"
```

## Ресурс

Можно использовать ресурс как executable бинарь, либо как файл.

### Достать по Resource ID

```yaml
resource: 2131485603    # key {resource} -> resource_id
```

### Найти по аттрибутам

```yaml
resource_search_conf: {     # key {resource} -> search_config
    DEFAULT_RESOURCE_SEARCH = {
    "type": "ARCADIA_PROJECT",
    "state": "READY",
    "attrs": {
        "released": "stable",
    },
}
```

## Аркадия

Можно достать файлы из аркадии. Доступен Arc и SVN.

### Arc

```yaml
# Использовать Arc
use_arc_fuse: True
# Ревизия маунта репозитория
arc_revision: r7312366  # либо users/dim-gonch/logos, trunk, fd6aa52239c
# Токен из yav, если не указан возьмется из секрета vault с ключом ARC_TOKEN 
arc_token: null
```

### SVN

```yaml
# Использовать SVN
use_arc_fuse: False
# SVN ревизия транка
svn_revision: 7312366
```

### Arcadia ресурсы

Перечислить ресурсы можно с помощью ключ - и путь до файла от корня. В `cmdline` можно достать файл по ключу.

```yaml
arc_resouces:  # key -> relative arcadia path
    resource_3: sandbox/projects/logos/config.json
```

## Переменные окружения и токены

```yaml
# Переменные окружения
#
# Достать токен из Sandbox Vault:
#    $(vault:owner:name)
#
# Достать токен из  Yav:
#    $(yav:version:name)
#
env_vars:
    DEBUG: 1
    SANDBOX_TOKEN: $(vault:robot-ml-logos:robot-ml-logos-sandbox-token)
    NIRVANA_TOKEN: $(yav:sec-01daxhrvak3kbcd6fxhydp3esp:nirvana-secret)
```

## Дополнительные Sandbox ресурсы

Sandbox ресурсы можно доставать по аналогии с [ресурсом](#resurs) по id, либо через аттрибуты.

```yaml
sb_resouces:  # key -> resource_id | search_config
    resource_1: 2131485603
    resource_2: {"type": "RESOURCE_TYPE", "state": "ready", "attrs": {"released": "stable"}}
```

## Перезапуск

```yaml
# Перезапускать выполнение команды при падении
retry_on_failure: true
# Количество перезапусков
retries: 3
# Время ожидания между перезапусками, в секундах
retry_interval: 3600
```

## Сохранять выходные ресурсы

Если результатом работы скрипта является файл, его можно выгрузить в ресурс.

```yaml
save_as_resource:
  local_path_1: RESOURCE_TYPE
  local_path_2: {"type": "RESOURCE_TYPE", "attrs": {"name": "value"}}

# Время хранения реурса, в днях
resources_ttl: 4
```

## TTL логов скрипта

По-умолчанию логи работы скрипта хранятся 14 дней, ttl можно поменять.

```yaml
# Хранить логи один год
task_logs_ttl: 365
```
