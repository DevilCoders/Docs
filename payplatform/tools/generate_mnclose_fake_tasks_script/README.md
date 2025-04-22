### Генератор SQL-скриптов для работы с фейковыми задачами PyCron

#### Генерация SQL-скриптов
```bash
./generate-mnclose-fake-tasks-script \
    --tasks-filename=./t_tasks_test.csv \
    --create-template-filename=./create_fakes_template.sql \
    --delete-template-filename=./delete_fakes_template.sql \
    --create-output-filename=./create.sql \
    --delete-output-filename=./delete.sql \
    --host='6879df61f88e' \
    --owner='your_login' \
    --ignored='[328, 329, 1130]'
```

Создаст в `./create.sql` скрипт для создания фейковых PyCron задач для всех активных вершин из `./t_tasks_test.csv`, кроме тех, которые указаны в `ignored` (328, 329, 1130).

Также создаст в `./delete.sql` скрипт для удаления этих задач.

Параметры:
- `owner` – логин того, кто заводит фейковую задачу.
- `host` – хост, на котором запускать фейковые задачи. В настоящий момент скрипт для фейковых задач есть только в ветке `PAYPLATFORM-91`, её хост: `6879df61f88e`.
- `ignored` – список вершин, для которых не надо заводить фейковые задачи. Рекомендуется указывать как минимум `'[328, 329]'`, т.к. это служебные вершины начала/конца графа в MnClose. Если планируется, что какие-то вершины будут обрабатываться настоящими задачами, а не фейковыми, то их тоже следует указать тут.

#### Использование скриптов
Выполнить сгенерированный `create.sql` на `TEST_BALANCE_YANDEX_RU`, чтобы добавить фейковые вершины на тесте.

Выполнить сгенерированный `delete.sql` на `TEST_BALANCE_YANDEX_RU`, чтобы удалить фейковые вершины с теста.

#### Откуда брать данные t_tasks_test.csv
Выполнить на `TEST_BALANCE_YANDEX_RU`:
```sql
select * from mnclose.t_tasks where is_active=1
```
скопировать результат в CSV.