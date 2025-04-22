ZK-DELIVERY
===========

Программный комплекс, синхронизирующий содержимое нод в Zookeeper 
локальными файлами.


CONFIGURATION
=============

Конфиг в формате YAML, передаётся в программы параметром -c
Пример:

    ---
    servers: server1:2181,server2:2181,server3:2181
    local_server: 127.0.0.1:2181
    auth: user:password
    log: /path/common.log
    alive_file: /path/zk-delivery-ppc.alive
    acl:
      write:
        - 127.0.0.1
        - super:password
      read:
        - anyone
    files: 
      - zk_path: /test/db-config.json
        file: /path/db-config.json
        hooks_dir: /path/test/hooks
        hooks_status_file: /path/test/hooks.alive
      - zk_path: /test/hosts
        file: /path/test/yandex-direct-db-hosts
        hooks_dir:
        hooks_status_file:

* servers - список серверов кластера zookeeper
* local_server - сервер, к которому пойдут запросы set/create (для простоты acl)
* auth - авторизация, под которой проводятся все авторизации
* log - лог-файл
* alive_file - файл, который touch-ится раз в 30 сек для мониторинга живости
* acl - права доступа к создаваемым и изменяемым нодам, подробности в разделе ACL
* files - описания файлов для синхронизации
  * zk_path - нода в Zookeeper
  * file - локальный файл, куда будут попадать данные из ноды
  * hooks_dir - опционально, директория с хуками, вызываемыми при обновлениях файла
  * hooks_status_file - опционально, файл для мониторинга хуков


ACL
===

Если на верхнем уровне  указана авторизация auth - всегда, дополнительно к остальным правилам,
разрешаем себе запись в ноду

В правилах acl могут быть строки такого вида:
- anyone - пользователи с любой авторизацией или без авторизации
- ddd.ddd.ddd.ddd - авторизация по ip
- ddd.ddd.ddd.ddd/dd - авторизация по ip с указанием сети
- user:password - авторизация по паролю

Правила по умолчанию, если acl не указан
- указан local_server - read:anyone, write: 127.0.0.1
- не указан local_server - write:anyone


HOOKS STATUS FILE
=================

Порядок выполнения хуков (почему такие странные статус-файлы)
- пишем в статусный файл "running"
- пишем новые данные в файл на диске
- запускаем по-очереди хуки, отслеживаем exit-code каждого
- если хоть один хук вернул code > 0 - пишем в статусный файл "failed",
  иначе удаляем статусный файл

Итого - нормальная ситуация когда файла не существует, или он младше максимального времени 
выполнения всех хуков(30 сек по-умолчанию)
Для удобства мониторинга есть /usr/local/bin/zk-delivery-hooks-mon


MONITORING
==========

Пример мониторинга для monrun

    [zk-delivery-ppc]
    execution_interval=60
    execution_timeout=30
    command=[ $((`date +%s` - `stat -c %Z /var/run/zk-delivery-ppc.alive 2>/dev/null || echo 0`)) -le 90 ] && echo '0;Ok' || echo '2;Old monfile.'
    
    [zk-delivery-hooks-ppc]
    execution_interval=60
    execution_timeout=30
    command=/usr/local/bin/zk-delivery-hooks-mon -c /etc/zk-delivery/ppc.cfg


