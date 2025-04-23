## Утилита для генерации графа в Nirvana из графа в MNClose.

### Использование:

```
./generate-nirvana-workflow-from-mnclose \
    --nirvana-server=test.nirvana.yandex-team.ru \
    --token-filename=./oauth_token.txt \
    --project tmp_ematirov \
    --label 'MNClose graph' \
    --tasks-filename=./t_tasks_test.csv \
    --tasks-relations-filename=./t_tasks_relations_test.csv \
    --month='08.19' \
    --check-delay=4 \
    --generation=10 \
    --keep-going=True \
    --with-offsets=True \
    --workflow-id='cda85a88-4cda-4650-a366-89b1dacaaa7c' \
    --scale=2.0 \
    --startrek-secret-name='ematirov_st_oauth_token' \
    --startrek-environment='SANDBOX' \
    --startrek-notify-recipients='["ematirov@yandex-team.ru", "null@yandex-team.ru"]' \
    --fcm-environment='test' \
    --fcm-tvm-src-id=2015305 \
    --fcm-tvm-dst-id=2014198 \
    --fcm-tvm-token-name='fcm_mnclose_nirvana_intergation_test_tvm_secret' \
    --test-graph-config-filename='./test_graph_config.json'
```

Аргументы:
1. `nirvana-server`: адрес API Nirvana. По-умолчанию – прод, для теста надо указать `test.nirvana.yandex-team.ru`.
2. `token-filename`: путь к файлу с OAuth-токеном для Nirvana.
3. `project`: проект в Nirvana, в котором будет создан Workflow.
4. `label`: Название нового Workflow в Nirvana.
5. `tasks-filename`: путь к файлу с описанием задач в MnClose.
    Формат: 
    ```
    "ID","NAME_ID","NAME","TERMINAL_SIGN","TD_SHIFT","TD_DURATION","TD_OVERDUE","IS_ACTIVE","NEED_AUTOOPEN","ALWAYS_STATE_NOTICE","WEIGHT"
    402,"t200910_acts_check","Проверить и устранить расхождения в актах",1,691200,172800,0,0,1,0,0
    ```
    Используются только поля ID, NAME, NAME_ID, IS_ACTIVE, TD_SHIFT.
    
    Можно получить запросом:
    ```sql
    select * from mnclose.t_tasks where is_active=1
    ```
6. `tasks-relations-filename`: путь к файлу с описанием связей в графе MnClose.
    Формат:
    ```
    "TASK_SOURCE_ID","TASK_DESTINATION_ID","TASK_REL_TYPE_ID","TD_SHIFT"
    437,441,1,0
    421,419,1,0
    ```
    Используются только поля TASK_SOURCE_ID и TASK_DESTINATION_ID.
    
    Можно получить запросом:
    ```sql
    select r.* from mnclose.t_task_relations r
    join mnclose.t_tasks t1 on t1.ID = r.TASK_SOURCE_ID
    join mnclose.t_tasks t2 on t2.ID = r.TASK_DESTINATION_ID
    where t1.is_active=1 and t2.is_active=1
    ```
7. (Опционально) `tasks-relations-override-filename`: путь к файлу с перепределением связей.
    Формат:
    ```
    "TASK_SOURCE_ID","TASK_DESTINATION_ID","ACTION"
    603,527,add
    534,527,add
    666,527,add
    ```
    `add` - добавить связь, `remove` - удалить связь.
8. `month` – месяц, в котором происходит закрытие. Используется для настройки запуска вершин по времени.
9. `check-delay` – интервал проверки состояния задачи – как часто биллинг-процессор будет проверять, не завершилась ли задача (и синхронизировать статус с MnClose).
10. `generation` – поколение, нужно для того, чтобы инвалидировать кэш детерминированных вершин Nirvana.
11. `keep-going` – продолжать ли выполнение графа при возникновении ошибок. Если выставлено в True, то соответствует "Error handling policy", установленной в "Ignore errors". По-умолчанию: True.
12. `with-offsets` – добавлять кубики "Wait offset" в зависимости задач по времени. Добавление такого кубика отсрочит начало выполнения задачи до определенного момент с начала закрытия. Дефолтное значение – добавлять. Время смещения берется из поля TD_SHIFT в `tasks_filename`.
14. (Опционально) `workflow-id` – id Workflow, в котором создать новый Instance. Если ID не указано, то будет создано новое Workflow.
15. (Опционально) `scale`: масштабирование визуализации, чем выше значение – тем больше будет пространства между кубиками. По-умолчанию равно `2`.
16. `startrek-secret-name='ematirov_st_oauth_token'` – имя токена для StarTrek.
17. `startrek-environment='SANDBOX'` – окружение StarTrek (SANDBOX – тестовое, PRODUCTION – прод).
18. `startrek-notify-recipients='["ematirov@yandex-team.ru", "null@yandex-team.ru"]'` – список email-адресов, на которые будут приходить оповещение о созданных тикетах.
19. `fcm-environment` - окружение FCM. Возможные варианты - `[prod, test, dev]`
20. `fcm-tvm-src-id` - id TVM приложения-источника при интеграции с FCM
21. `fcm-tvm-dst-id` - id TVM приложения-назначения при интеграции с FCM
22. `fcm-tvm-token-name` - имя токена TVM между приложениями, хранится в https://nirvana.yandex-team.ru/secrets
22. `test-graph-config-filename` – путь к файлу с конфигом, настраивающим тестовый граф.

## Конфиг тестового графа
Пример:
```json
{
  "whitelist": {
    "monthly_auto_overdraft": {
      "prepare_operations": [
        {
          "name_id": "monthly_auto_overdraft_prepare_something",
          "title": "Подготовка чего-то",
          "offset": 0,
          "dependencies": [],
          "nirvana_operation": "some_prepare_operation",
          "params": {
            "some_parameter": "value"
          }
        },
        {
          "name_id": "monthly_auto_overdraft_prepare_something_2",
          "title": "Подготовка чего-то",
          "offset": 0,
          "dependencies": [
            "monthly_auto_overdraft_prepare_something"
          ],
          "nirvana_operation": "some_prepare_operation_2",
          "params": {
          }
        }
      ],
      "test_operations": [
        {
          "name_id": "monthly_auto_overdraft_test_something",
          "title": "Проверка чего-то",
          "offset": 0,
          "dependencies": [],
          "nirvana_operation": "some_test_operation",
          "params": {
          }
        },
        {
          "name_id": "monthly_auto_overdraft_test_something_2",
          "title": "Проверка ещё чего-то",
          "offset": 0,
          "dependencies": [
            "monthly_auto_overdraft_test_something_3"
          ],
          "nirvana_operation": "some_test_operation_2",
          "params": {
          }
        }
      ]
    },
    "monthly_invoices": {
    }
  }
}  
```
1. Заменит все задачи кроме `monthly_auto_overdraft` и `monthly_invoices` на фейковые.
2. Вставит перед `monthly_auto_overdraft` (но после всех её зависимостей) операцию `some_prepare_operation` с именем `monthly_auto_overdraft_prepare_something` и параметром `some_parameter` равным `value`.
2. Вставит перед `monthly_auto_overdraft` (но после всех её зависимостей) и после `monthly_auto_overdraft_prepare_something` операцию `some_prepare_operation_2` с именем `monthly_auto_overdraft_prepare_something_2`.
3. Вставит после `monthly_auto_overdraft` (но перед всеми её зависимостями) операцию `some_test_operation` с именем `monthly_auto_overdraft_test_something`.
3. Вставит после `monthly_auto_overdraft` (но перед всеми её зависимостями) и после `monthly_auto_overdraft_test_something` операцию `some_test_operation_2` с именем `monthly_auto_overdraft_test_something_2`.

## Данные

### Прод
Описание, как получить доступ к продовым данным будет добавлено в тикете https://st.yandex-team.ru/PAYPLATFORM-55.

Текущие данные:
- [t_tasks_relations_jule.csv](https://jing.yandex-team.ru/files/ematirov/t_tasks_relations_jule.csv)
- [t_tasks.csv](https://jing.yandex-team.ru/files/ematirov/t_tasks.csv)
### Данные с теста:
#### tasks (информация о задачах)
Можно получить запросом:
```sql
select * from mnclose.t_tasks where is_active=1
```
#### tasks_relations (информация о связях)
Можно получить запросом:
```sql
select r.* from mnclose.t_task_relations r
join mnclose.t_tasks t1 on t1.ID = r.TASK_SOURCE_ID
join mnclose.t_tasks t2 on t2.ID = r.TASK_DESTINATION_ID
where t1.is_active=1 and t2.is_active=1
```
