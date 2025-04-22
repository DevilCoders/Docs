## Скрипт для очистки данных miner & snippets (Cleaner)

Параметры:

* "base_path": путь до daps каталога в YT (например, //home/maps/carparks/testing/daps)

* "mined_hard_delete_age": через какой промежуток времени (дни) будут удалены все данные по пути /daps/mined

* "mined_soft_delete_age": через какой промежуток времени (дни) будут удалены все данные по пути /daps/mined
    за исключением suggested_points для каждого дня и полного набора таблиц за 1 день в месяц

* "snippets_delete_age": через какой промежуток времени (дни) будут удалены все данные по пути /daps/snippets

* "dry_run": распечатывает информацию о потенциально удаленных таблицах без реального удаления

Для работы скрипта необходимо иметь переменную окружения "YT_TOKEN"

Sandbox tasks:

* [Testing](https://sandbox.yandex-team.ru/scheduler/700685/view)

* [Production](https://sandbox.yandex-team.ru/scheduler/700689/view)
