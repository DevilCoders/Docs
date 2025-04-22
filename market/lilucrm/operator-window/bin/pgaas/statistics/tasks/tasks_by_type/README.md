### [OCRM-1835](https://st.yandex-team.ru/OCRM-1835): Сделать выгрузку в excel
`group_by_month_and_type.sh` - подсчитывает, за каждый месяц из указанного периода, число задач типов:
"отмена заказа", "перенос заказа" и "другое"

**Usage:** `./group_by_month_and_type.sh FROM_DT TO_DT`

```sh
./group_by_month_and_type.sh 2019-02-01 2019-03-01
```
Результат сохраняется в `tmp/group_by_month_and_type-${FROM_DT}_${TO_DT}.tsv`

### [OCRM-3421](https://st.yandex-team.ru/OCRM-3421): B2C - Выгрузка задач в Excel
`select_by_type.sh` - список задач определённого типа за период.

**Usage:** `./select_by_type.sh TYPE(s) FROM_DT TO_DT`
* `TYPES` - TaskType code or comma separated list
* `FROM_DT` - start of interval (ISO-8601 date/time)
* `TO_DT` - end of interval

```sh
./select_by_type.sh CANCEL_ORDER,CANCEL_CROSSDOC 2019-11-25 2019-12-13
```
Результат сохраняется в `tmp/select_by_type-${TYPE}-${FROM_DT}_${TO_DT}.tsv`

Структура результата:
* `id` - ID задачи
* `task_type_id` - ID типа задачи
* `task_type_code` - код типа задачи
* `task_type_description` - описание типа задачи
* `task_status_id` - ID статуса задачи
* `task_status_code` - код статуса задачи
* `task_status_description` - описание статуса задачи
* `order_id` - ID заказа
* `order_status_code` - код статуса заказа
* `order_status_description` - описание статуса заказа
* `created_date` - дата создания задачи
* `closed_date` - дата закрытия задачи
* `close_sub_topic_id` - ID причины (подтемы) закрытия
* `close_sub_topic_code` - код причины (подтемы) закрытия
* `close_sub_topic_description` - описание причины (подтемы) закрытия
* `assignee_uid` - паспортный UID исполнителя
* `assignee_login` - login исполнителя
* `assignee_fullname` - Имя и Фамилия исполнителя
