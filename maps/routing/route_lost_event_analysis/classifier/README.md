Здесь расположены инструменты для классификации сходов. Запустить бинарник можно следующим образом:

    ./bin/classifier/classifier --date YYYY-MM-DD --graph-version <version>

Бинарник передаёт данные из таблиц `//home/maps/jams/production/route-quality/route_lost/<date>` и `//home/maps/jams/production/route-quality/faster_route_lost/<date>` разным классификаторам, которые пытаются сопоставить каждому событию один или несколько классов.

В результате выполнения бинарника на экран будет напечатана статистика по классам в формате:

    info: MissedUTurn class:
    info:         count: 77986
    info:         percentage: 1.58008
    info: IgnoredForbiddenTurn class:
    info:         count: 39680
    info:         percentage: 0.803957
