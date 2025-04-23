# Бэкапы данных в MDS

![backups](../img/backups.png "Бэкапы")

В ecstatic настроены регулярные бэкапы данных в mds. Для этого есть 3 sandbox-шедулера:

- [stable](https://sandbox.yandex-team.ru/scheduler/701360)
- [testing](https://sandbox.yandex-team.ru/scheduler/700863)
- [unstable](https://sandbox.yandex-team.ru/scheduler/700864)

## Восстановление бэкапа

Для распаковки необходимо запустить sandbox-template:

- [stable](https://sandbox.yandex-team.ru/template/MAPS_CORE_ECSTATIC_RESTORE_DATASETS_STABLE)
- [testing](https://sandbox.yandex-team.ru/template/MAPS_CORE_ECSTATIC_RESTORE_DATASETS_TESTING)
- [unstable](https://sandbox.yandex-team.ru/template/MAPS_CORE_ECSTATIC_RESTORE_DATASETS_UNSTABLE)

В параметры задачи необходимо передать id снэпшота, который можно получить в бэкапящей задачи, а также опционально можно указать список датасетов для распаковки.
