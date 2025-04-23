# Доступы
## Основные понятия

Объекты, имеющие ACL и синхронизирующиеся с IDM:

* Tasklet
* Namespace

### Tasklet ACL

`Tasklet` является элементарным объектом, имеющим ACL.

Роли `Tasklet`'ов:

* `Tasklet Read` - Право на просмотр `builds`/`labels`/`executions`.
* `Tasklet Write` - Право на сздание `build`'ов тасклета и управление `label`'ами.
* `Tasklet Run` - Право на запуск `execution` `Tasklet`'а.
* `Tasklet Owner` - Право на редактирование метаинформации тасклета и управление выдачей ролей `Tasklet`'а.

### Namespace ACL

`Namespace` содержит в себе `Tasklet`'ы, однако права на `Namespace` не пересекаются с правами на `Tasklet`'ы и имеют свой смысл.

Роли namespace'ов:
* `Namespace Read` - Право на чтение метаинформации `Namespace`'а, просмотр его `Takslet`'ов.
* `Namesapce Owner` - Право на редактирование `Namespace`'а и управление выдачей ролей `Namespace`'а.
* `Create Tasklet` - Право на создание `Tasklet`'ов в `Namespace`'е.
