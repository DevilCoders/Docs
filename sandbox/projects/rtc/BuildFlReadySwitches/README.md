Что это
===
Задача для запуска скрипта [fl_ckecker](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/fl_checker/__main__.py)


Параметры задачи
===
  - wall-e projects - список wall-e проектов для которых строится список
  - check_diff - включить сравнение полученного результат с предыдущим;
  - thresholds - список порогов(ключ=значение) для сравнения с предыдщим результатом. При выходе за порог задача упадет, новый ресурс не будет загружен. Ключем является ключ словаре результатов для которого будет рассчитан порог, значение - порог, вещественное число [0..1].


Поставщики данных
===
  - [выгрузка из heartbeat](https://sandbox.yandex-team.ru/tasks?type=BUILD_KERNEL_INFO)
  - [топология netmon](https://sandbox.yandex-team.ru/tasks?type=BUILD_NETMON_TOPOLOGY)


Проверки juggler
===
  - [fl_ready_switches](https://juggler.yandex-team.ru/check_details/?host=sandbox&service=fl-ready-switches)
