## Inventory remove old folders or tables

Задача для удаления старых папок и таблиц inventori

### Input parameters

1. Environment type - тип окружения(prod, test, dev, custom)
2. Yt project directory - путь до директории проекта inventori в Yt. Свое значение параметра пользователь может определить только когда <i>Environment type = custom</i>. В остальных случаях значение предопределено и хранится в [файле](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/inventori/common/consts.py)
3. Relative paths that needs to be cleared - относительные от <i>Yt project directory</i> директории, внутри которых необходимо произвести очистку
4. Relative path to table with config - относительный от <i>Yt project directory</i> путь до таблицы, в которой хранится информация сколько дней должны хранииться таблицы и папки для каждой директории  
5. YT_TOKEN vault name - имя записи в [секретнице Sandbox'а](https://sandbox.yandex-team.ru/admin/vault), которя содержит YT токен для inventori
6. YT_TOKEN vault user - пользователь, от которого будет читаться секрет
7. YT_PROXY

#### How task works

1. Читает таблицу <i>Relative path to table with config</i>
2. Для каждого пути path из <i>Relative paths that needs to be cleared</i> выполяет:<br>
    a) Из конфигурационной таблицы из п.1 берется значение поля <i>days_of_storage</i><br>
    b) Получет список всех объектов(папок и таблиц), лежащих на верхнем уровне в path<br>
    c) Все объекты делит на те, у которых название представляет собой дату - valid_items, и другие - invalid_items<br>
    d) Находит максимальную дату из valid_items, из нее вычитается <i>days_of_storage</i><br>
    e) Все объекты, название которых меньше полученного в пункте d числа удаляются<br>
    f) Если invalid_items не пусто, то отправляется уведомляющее письмо 
