### Генерация списка серверов для nginx-upstream

#### Abstract
Утилита узнает ДЦ мастера календарной базы, находит инстансы Календаря в этом ДЦ и 
добавляет их адреса в nginx-upstream. В итоге HTTP-нагрузка проксируется в ДЦ, локальный к мастеру БД.
Для инстансов, находящихся ДЦ-локально к мастеру БД, утилита ничего не делает.

Обычно запускается через crontab, чтобы отслеживать изменения мастера БД 

#### TLDR

##### Направить трафик в ДЦ, локальный к мастеру БД (обычно запускается cron-ом):
```bash
# qloud-nginx-gen-upstream
```
Можно заранее проверить результат через `--dry-run` режим.

##### Вернуть всё, как было:
```bash
# qloud-nginx-gen-upstream --restore
```
Последующие запуски скрипта (в том числе кроном) проходить не будут; результат `--restore` останется на месте.

##### Вновь направить трафик поближе к мастеру БД:
```bash
# qloud-nginx-gen-upstream --unlock
```

Подробнее об устройстве - ниже.

#### Configuration

См. конфиг утилиты, по-умолчанию используется `/opt/nginx_upstream_gen_config.yml`, [пример для Календаря](../../package/deploy/opt/nginx_upstream_gen_config.yml) 

#### How to
Начальное состояние upstream-а
```bash
# cat /etc/nginx/upstreams/primary.include
upstream primary-backend {
    least_conn;
    server [::1]:22400;
}
```

Dry-run режим: сгенерирует новые upstream-ы, подсунет их на место основного, 
 проверит работоспособность через `nginx -t`, вернет все на место
```bash
# qloud-nginx-gen-upstream --dry-run
INFO:mail.calendar.python.nginx_gen_upstream.main:Going to setup proxying to servers in database-local dc vla
INFO:mail.calendar.python.nginx_gen_upstream.main:Successfully created /etc/nginx/upstreams/primary.include.new
...
INFO:mail.python.qloud.nginx:Found changes in config files .include, backing up current config using prefix .include.bak and replacing it using prefix .include.new
INFO:mail.python.qloud.nginx:Copied .include to .include.bak for primary
...
INFO:mail.python.qloud.nginx:Copied .include.new to .include for primary
...
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
INFO:mail.python.qloud.nginx:Nginx config test successful
INFO:mail.python.qloud.nginx:Dry-run mode requested, returning previous config files using prefix .include.bak
INFO:mail.python.qloud.nginx:Copied .include.bak to .include for primary
...
INFO:mail.calendar.python.nginx_gen_upstream.main:All done


# cat /etc/nginx/upstreams/primary.include
upstream primary-backend {
    least_conn;
    server [::1]:22400;
}

# cat /etc/nginx/upstreams/primary.include.new
upstream primary-backend {
    least_conn;
    server [2a02:06b8:0c18:360d:0000:4601:aeed:63da]:22400;
    server [2a02:06b8:0c17:08a2:0000:4601:db61:8b9a]:22400;
    server [2a02:06b8:0c15:3511:0000:4601:1e4e:2d18]:22400;
    server [2a02:06b8:0c0d:328e:0000:4601:3c27:d3b8]:22400;
    server [2a02:06b8:0c18:360d:0000:4601:34a1:9c5e]:22400;
    server [::1]:22400 backup;
}

```

Основной режим: всё то же самое, но вместо возврата на место запускает nginx reload
 и оставляет новые конфиги upstream-ов
 
```bash
# qloud-nginx-gen-upstream
INFO:mail.calendar.python.nginx_gen_upstream.main:Going to setup proxying to servers in database-local dc vla
INFO:mail.calendar.python.nginx_gen_upstream.main:Successfully created /etc/nginx/upstreams/primary.include.new
...
INFO:mail.python.qloud.nginx:Found changes in config files .include, backing up current config using prefix .include.bak and replacing it using prefix .include.new
INFO:mail.python.qloud.nginx:Copied .include to .include.bak for primary
...
INFO:mail.python.qloud.nginx:Copied .include.new to .include for primary
...
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
INFO:mail.python.qloud.nginx:Nginx config test successful
INFO:mail.python.qloud.nginx:Some random sleep
INFO:mail.python.qloud.nginx:Nginx reloaded with status 0
INFO:mail.calendar.python.nginx_gen_upstream.main:All done

# cat /etc/nginx/upstreams/primary.include
upstream primary-backend {
    least_conn;
    server [2a02:06b8:0c18:360d:0000:4601:aeed:63da]:22400;
    server [2a02:06b8:0c17:08a2:0000:4601:db61:8b9a]:22400;
    server [2a02:06b8:0c15:3511:0000:4601:1e4e:2d18]:22400;
    server [2a02:06b8:0c0d:328e:0000:4601:3c27:d3b8]:22400;
    server [2a02:06b8:0c18:360d:0000:4601:34a1:9c5e]:22400;
    server [::1]:22400 backup;
}

# cat /etc/nginx/upstreams/primary.include.bak
upstream primary-backend {
    least_conn;
    server [::1]:22400;
}
```

Restore-режим: возвращает backup upstream-файлы на место, проверяет конфиги, релоадит nginx. 
Создает специальный lockfile, препятствующий последующим запускам скрипта, для автоматической остановки cron-ов (также доступно через --lock) 

```bash
# qloud-nginx-gen-upstream --restore
INFO:mail.calendar.python.nginx_gen_upstream.main:Locking script by lock-file /opt/nginx_upstream_gen_config.lock
INFO:mail.python.qloud.nginx:Found changes in config files .include, backing up current config using prefix .include.new and replacing it using prefix .include.bak
INFO:mail.python.qloud.nginx:Copied .include to .include.new for primary
...
INFO:mail.python.qloud.nginx:Copied .include.bak to .include for primary
...
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
INFO:mail.python.qloud.nginx:Nginx config test successful
INFO:mail.python.qloud.nginx:Some random sleep
INFO:mail.python.qloud.nginx:Nginx reloaded with status 0

# cat /etc/nginx/upstreams/primary.include
upstream primary-backend {
    least_conn;
    server [::1]:22400;
}
```

Чтобы снять блокировку (и вернуть обычный порядок вещей), нужно разово запустить скрипт с аргументом --lock:

```bash
# qloud-nginx-gen-upstream
ERROR:mail.calendar.python.nginx_gen_upstream.main:Lock-file exists at path /opt/nginx_upstream_gen_config.lock. Remove it with --unlock flag to proceed

# qloud-nginx-gen-upstream --unlock
INFO:mail.calendar.python.nginx_gen_upstream.main:Removing lock-file /opt/nginx_upstream_gen_config.lock
...
INFO:mail.calendar.python.nginx_gen_upstream.main:All done
```