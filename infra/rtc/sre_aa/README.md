# Usage

Скрипт для sre aa.

Запускать скрипт нужно со своего рабочего ноутбука, иначе не будет дырки по SSH. Дырки выданы на сервис [SRE AA](https://abc.yandex-team.ru/services/sreaa/). Зайти на созданную виртуалку можно из под **root**.

Написан довольно "прямолинейно", требует рефакторинга, обобщения логики и просто причёсывания. Но кое как работает.
В api qyp не ходит, пользуется локальным ya vmctl, т.к. стабильность api, в отличие от стабильности vmctl мне не пообещали.

**Директории, которые нужны скрипту.**

challenges/ - лежит там же в svn'е. Внутри sls-файлы с описанием задачи. Исполняются salt'ом на сервере. top.sls генерится скриптом автоматически, его создавать/коммитить не надо.
logs/ - создаётся сама, туда скрип скачивает скринкасты с уничтожаемой виртуалки.

**Команды:**

* aa_ctl create $challenge1,$challenge2,...,$challengeN - создаёт виртуалку, загружает на неё задания, перечисленные через запятую (без пробелов) на эту виртуалку, дёргает там salt-call state.apply.
* aa_ctl deallocate $vm_name | --all - уничтожает виртуалку, предварительно скачивая с неё скринкасты, которые кладутся в ./logs. Можно или указать имя инстанса, или ключ --all . Имя (то, что нужно указывать в аргументе) можно узнать в выхлопе aa_ctl list.
* aa_ctl list - показывает список активных собеседований и виртуалок в них (в "дизайн" заложена возможность поднимать несколько виртуалок для 1 задания).

> $ aa_ctl list
> vms_zkxo:
>     sre-aa-2019-12-12-zkxo-0 - (sre-aa-2019-12-12-zkxo-0.sas.yp-c.yandex.net)
Удалить:
> aa_ctl deallocate vms_zkxo
>  => Backuping logs from vm sre-aa-2019-12-12-zkxo-0
>  => Deallocating vm sre-aa-2019-12-12-zkxo-0
Текстовые файлы с данными о собеседованиях/созданных виртуалках хранятся в /.aactl .

# Links
* [SSH key](https://yav.yandex-team.ru/secret/sec-01dts7jh34p73w0zfncbpy0bm6/explore/versions)
* [ABC](https://abc.yandex-team.ru/services/sreaa/)
* [Zomb](https://staff.yandex-team.ru/zomb-pretender)
* [Постановка задачи](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/sre_aa/TASK.md)
