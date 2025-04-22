Скриптик для отладки взаимодействия с Янгом
-------------------------------------------

Для работы использует environment variable `YANG_TOKEN`, токен взять можно в Янг (Профиль/Интеграции),
если зайти из-под (robot-yang-bizdir)(https://yav.yandex-team.ru/secret/sec-01f9kfqmhab7jsxb70c6yt7rhp)
(Там же, кстати, можно управлять доступами новых людей к проекту)

Команды
--------
- print-yang-input <pb|pbtext> — конвертирует `callcenter_pb2.Task` во входной формат Янга и печатает из него кусок только про данные
    ./yang_cli print-yang-input ../../yang/tests/data/pushkin.pbtext
- mock-submit <pb|pbtext> — конвертирует `callcenter_pb2.Task` во входной формат Янга и печатает его (в Янг не ходит)
    ./yang_cli mock-submit ../../yang/tests/data/pushkin.pbtext
- print-yang-output <json> - проверяет работоспособность обратной конвертации (конвертирует из ответа Янга proto и печатает его)
    ./yang_cli assignment 0002176100--61cb518fcbab571ada2cb796 > result.json
    ./yang_cli print-yang-output result.json
- poll <id> - запрашивает у Янг'а по id результат задания, конвертирует его в `callcenter_pb2.TaskResult` и печатает
    ./yang_cli poll 0002176100--61cb518fcbab571ada2cb796
- submit <fn.proto> - создает из proto задание в Янгe

- tasks - показывает текущее состояние пула (активные/неактивные задачи и их id)
    ./yang_cli tasks
- task <id> - запрашивает в Янге задание <id> и печатает его
    ./yang_cli task 0002176100--61cb518fcbab571ada2cb796
- delete-task <id> - выставляет у задания <id> overlap 0 (после чего оно больше не показывается контентам)
    ./yang_cli delete_task 0002176100--61cb518fcbab571ada2cb796
- solution <id> - запрашивает в Янге решение задания <id> и печатает его
    ./yang_cli solution 0002176100--61cb518fcbab571ada2cb796

- get-project <project_id> - печатает описание проекта <project_id>
    ./yang_cli get_project 14215
- update-project <project_id> - обновляет проект <project_id>, добавив `max_active_assignments_count = 10`,
  (нужно было, чтобы появилась кнопка 'Выполнить позже', я не нашёл, как сделать проще, см. TOLOKA-16772, https://wiki.yandex-team.ru/restlog/doc/)
