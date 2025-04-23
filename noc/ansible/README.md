# Тут лежат плейбуки и роли для ansible


**Интеграция с RackTables**
Скрипт hosts.py создан для генерации inventory. По-умолчанию он выдает данные из кэша. Чтобы обновить кэш надо выполнить ./hosts.py --recache. 
Пример плейбука для hosts.py:

```yaml
  hosts: iva-nms
  vars:
    inventory_filter: '{$cn_iva-nms}'
```
Из этого плейбука скрипт сделает группу хостов iva-nms которая будет содержать все хосты из фильтра '{$cn_iva-nms}'

Если в env будет определена переменна FILTER, hosts.py будет фильтровать хосты в соотвествии с этим фильтром. В нем можно писать выражение RT или список хостов.

**Пример выкатывавния**
```shell
FILTER="man1-4fw8.yndx.net" ansible-playbook -f 1 -vvv playbooks/deploy-zabbix.yml
```
Через Makefile:
```shell
make FILTER="hbf9.haze.yandex.net" PLAYBOOK=playbooks/deploy-hbf.yml gen_configs deploy
```
Выкатить на сервер у которого не совпадает ip и fqdn
```shell
FILTER="man1-hbf1.yndx.net" ansible-playbook -k -vvv -f 1 -e 'man1-hbf1.yndx.net ansible_user=root ansible_host=2a02:6b8:b000:6034:92e2:baff:fe74:7a38' playbooks/deploy-hbf.yml
```

