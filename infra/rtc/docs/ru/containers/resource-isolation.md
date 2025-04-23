# Изоляция по ресурсам

## Как узнать сколько ресурсов доступно?

В Аркадии есть соответствующие библиотеки.

### Go
Библиотека называется [a.yandex-team.ru/library/go/maxprocs](https://a.yandex-team.ru/arc/trunk/arcadia/library/go/maxprocs).
[подробнее](https://clubs.at.yandex-team.ru/infra-cloud/2211)


### C++
Функция `NSystemInfo::NumberOfCpus` из [util/system/info.h](https://a.yandex-team.ru/arc_vcs/util/system/info.h?rev=9a79ac6142f516f705adf66b96436e7957c055b3#L6) корректно учитывает кол-во доступных ресурсов.
[подробнее](https://clubs.at.yandex-team.ru/infra-cloud/2211)


### Java
Поддержка в Аркадии доступна из коробки.
[подробнее](https://clubs.at.yandex-team.ru/infra-cloud/2135)

### Блокеры
* [SWAT-7892](https://st.yandex-team.ru/SWAT-7892)
