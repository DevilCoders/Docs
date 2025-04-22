### Как перегенерировать шаблоны алертов и графиков
     ya make
     ./bin/yasm_generate -p furita -r alexandr21 -o alexandr21
***-p  List of projects to regenerate checks***\
***-r List of people to set as responsibles. This list will be set for phone escalation***\
***-o Panel owner name***

Проект, для которого Вы собираетесь сгенерировать метрики, называется так же, как и папка, где для него находятся jinja-панели.

### Что добавить для нового проекта, чтобы дежурный менялся каждую неделю
[добавить проект вот тут](https://a.yandex-team.ru/arc/trunk/arcadia/mail/duty/rotate_maildev_duty/lib/rotator.py?rev=5271890#L29)\
Но в этом случае ротация дежурных будет происходить среди сотрудников, входящих в группу maildev, 
поэтому если Вы хотите другой список дежурных, то нужно модифицировать библиотеку.

Ротация происходит посредством этого sandbox scheduler'a\
[код](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/mail/RotateMaildevDuty/__init__.py)\
[sandbox scheduler](https://sandbox.yandex-team.ru/scheduler/12002/view)

### Как добавить новый проект
* добавляем [сюда](https://a.yandex-team.ru/arc/trunk/arcadia/mail/yasm/lib) папочку и называем ее как проект, обновляем ya.make
* внутри каждой папки находится папка **alerts** **panels** и ***__init__.py***, который копируется из папки в папку
* **alerts** - тут хранится шаблон панели для алертов
* **panels** - тут хранятся панели для самих графиков
* внутри как папки с алертами, так и папки с графиками должен быть файлик **primary.py** (он может называться и по-другому), 
в нем непосредственно должен быть описан шаблон и функция, которая возращает пару - название панели и непосредственно jinja-шаблон [например](https://a.yandex-team.ru/arc/trunk/arcadia/mail/yasm/lib/reminders/panels/primary.py?rev=5352531#L315)

**P.S** Очень много полезных макросов для генерации графиков Вы можете найти в других проектах, например, в **calendar**.

### Почему это смесь python и jinja-шаблонов
В голован нельзя заливать новый список дежурных (они меняются каждую неделю) и при этом не модифицировать панель.
Поэтому каждую неделю приходится заливать новую панельку алертов с новыми дежурными. 