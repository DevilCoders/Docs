# Утилита для генерации ip-адресов для железных хостов.
Пример использования:
Ищет свич по хостнейму сервера в eine, идет в racktables и берет оттуда нужную подсеть.
```
$ ./gen_ip --project_id 627 --fqdn trust2e.paysys.yandex.net
IP is 2a02:6b8:c04:299:0:627:792a:b1f7

        NOTICE: Please don't forget to check that ip is really avalivable. Use
        the following commands:

        host 2a02:6b8:c04:299:0:627:792a:b1f7
        ping6 2a02:6b8:c04:299:0:627:792a:b1f7
```
если хостнейма еще нет, можно использовать id хоста в eine:
```
$ ./gen_ip --project_id 627 --fqdn trust22e.paysys.yandex.net --inventory_id 107565365
IP is 2a02:6b8:c04:299:0:627:5cc9:b27

        NOTICE: Please don't forget to check that ip is really avalivable. Use
        the following commands:

        host 2a02:6b8:c04:299:0:627:5cc9:b27
        ping6 2a02:6b8:c04:299:0:627:5cc9:b27
```
или указать подсеть 333 влана свича, на котором живет хост эксплицитно
```
$ ./gen_ip --project_id 627 --fqdn trust22e.paysys.yandex.net  --project_id_location_prefix 2a02:6b8:c04:143::/64
IP is 2a02:6b8:c04:143:0:627:5cc9:b27

        NOTICE: Please don't forget to check that ip is really avalivable. Use
        the following commands:

        host 2a02:6b8:c04:143:0:627:5cc9:b27
        ping6 2a02:6b8:c04:143:0:627:5cc9:b27
```
