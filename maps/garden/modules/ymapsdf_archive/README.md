# ymapsdf_archive module

Store ymapsdf backup on YT at [//home/maps/core/garden/prod/ymapsdf_archive](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/ymapsdf_archive&).
Merge tables with the same name in all regions into one to save nodes in Cypress. Be careful with result data! Some objects can be duplicated, e.g. masstransit stops, poi, oceans.

Ymapsdf backups are needed to recalculate various statistics and analyze data retrospectively, e.g. in stat reports, [1](https://stat.yandex-team.ru/Maps.Wiki/KPI/AbsoluteValues/ItemsCount), [2](https://stat.yandex-team.ru/Maps.Wiki/KPI/AbsoluteValues/ItemsLength).
