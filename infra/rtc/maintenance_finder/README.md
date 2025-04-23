# Goals
С помощью этой утилиты можно пометить тэгом `rtc_maintenance_expired` забытые тикеты на которых висят в maintenance хосты RTC.

Тикеты можно найти на [дашборде](https://st.yandex-team.ru/dashboard/39751#209246).

# Examples

Навесить тэг `rtc_maintenance_expired` на подвисшие тикеты:

    ./find --no-dry-run maintenance

Найти подвисшие хосты в тикете:

    ./find hosts RNDSUPPORT-750

# Monitoring

Juggler:
* [Выполнение](https://juggler.yandex-team.ru/check_details/?host=find-walle-maintenance&service=scheduler) задача на поиск подвисших тикетов

# Cron

* Tickets are finded with [FIND_WALLE_MAINTENANCE](https://sandbox.yandex-team.ru/scheduler/24503/view).

# CI

* [TestEnv](https://beta-testenv.yandex-team.ru/project/runtime_cloud/job/YANDEX_WALLE_FIND_MAINTENANCE/history?limit=20)
