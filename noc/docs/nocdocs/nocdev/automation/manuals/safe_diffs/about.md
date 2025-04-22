# Safe Diff

В этой статье приведена информация по добавлению safe acl в генераторы **ann**, а также инструкция по устранению safe diff.

## Safe Acl

Как известно, область действия генератора в **ann** определяется специальной сущностью под названием `_acl`. Также для явного указания какая область конфигурации является **safe** в генераторе определяется сущность `acl_safe`, который определяется как метод класса генератора. По умолчанию этот метод не определен, поэтому его необходимо явно указывать в генераторе.

{% note warning %}

Название метода обязательно должно начинаться с `acl_safe`.

{% endnote %}

Давайте рассмотрим пример определения safe acl на примере генератора snmp.

```python
class Snmp(Generator):
    TAGS = ["snmp", "mgmt"]

    def acl_huawei(self, _):
        return """
            snmp-agent$
            snmp-agent community
            snmp-agent sys-info
            snmp-agent mib-view
            snmp-agent protocol
            #!snmp-agent local-engineid
            ifindex constant
            set if-mib discard-statistics enable
            snmp protocol server
        """

    def acl_safe_huawei(self, _):
        """
        BE CAREFUL! All the commands which are allowed by the ACL will be applied automatically!!!
        """
        return """
            snmp-agent$
            snmp-agent community
            snmp-agent sys-info
            snmp-agent mib-view
            snmp-agent protocol
            ifindex constant
            set if-mib discard-statistics enable
            snmp protocol server
        """
```

Как мы видим класс SNMP содержит обычный acl для Huawei, а также определен метод `acl_safe_huawei`, в котором приведены безопасные строки конфигурации оборудования. Как видно `acl_huawei` равен `acl_safe_huawei`, таким образом вся конфигурация полученная данным генератором для устройств Huawei является безопасной и может быть применена на устройстве в полностью автоматическом режиме.

### Список генераторов с safe acl

На текущий момент следующие генераторы содержат методы `acl_safe`:
- aaa.py
- dns.py
- icmp.py
- ifstat.py
- lldp.py
- local_users.py
- mgmt.py
- mgmt_acl.py
- ntp.py
- snmp.py
- snmp_acl.py
- snmp_trap.py
- syslog.py
- vty.py
- yattl.py

### Генерация safe diff

Для генерации safe diff для устройства используя `./ann` необходимо использовать флаг `--acl-safe`. Пример:
```
./ann diff iva6-s49 --acl-safe
```

## Процесс устранения Safe Diff

Рассмотрим подходы к устранению safe diff. Выделяем несколько методов:
- ручное устранение
- автоматическое

### Ручное устранение

Протестированым методом устранения safe diff является ручной метод. В нём сотрудник эксплуатации сети вручную устраняет diff используя [UI:diffs](http://noc.yandex-team.ru/diffs).

Рассмотрим этот процесс более подробно.

#### Шаг 1

Переходим в [UI:diffs](http://noc.yandex-team.ru/diffs). Проверяем `current revision`, чтобы убедиться, что мы работаем с последней версией **ann**. Нажимаем на галочку `Only safe acl`.

Если версия **ann** не последняя, то стоит отложить изменения конфигурации, сообщить в nocdev и завести тикет в соответствующую очередь.

Если все хорошо, то видим такую картинку:

![](_images/img1.png)

#### Шаг 2

Выбираем необходимые нам устройства с помощью фильтров и галочек. Также можно воспользоваться кнопкой `SELECT ALL/DESELECT ALL`. Нажимаем на кнопку `CREATE`.

![](_images/img2.png)

#### Шаг 3

Попадаем в меню планировщика job. Обычно мы хотим запустить задачи сразу, поэтому нам достаточно указать номер NOCRFCS тикета (это обязательно). Если тикета NOCRFCS еще нет, то его можно создать по ссылке слева снизу.

Нажимаем `CREATE JOBS`.

![](_images/img3.png)

#### Шаг 4

Если job были созданы успешно, то мы их можем наблюдать во вкладке [UI:Jobs](https://noc.yandex-team.ru/jobs).

#### Шаг 5

to be continued...