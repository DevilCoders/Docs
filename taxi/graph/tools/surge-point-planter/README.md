# surge-point-planter

Приложение для расстановки фиксированных точек расчета суржа на графе

Подробности: https://st.yandex-team.ru/EFFICIENCYDEV-12393

## Запуск

```
Usage: ./surge-point-planter [OPTIONS]

Required parameters:
  --pins-file VAL        Path to pins data json

Optional parameters:
  --svnrevision          print svn version
  {-h|--help}            print usage
  --distances VAL        Maximum distance from fixed point to pin. Format:
                         <percentage1>:<max_value1>,<percentage2:max_value2>...
  --out-file VAL         Path to output fixed points json
                         (default: "fixed_points.json")
  --interactive          Do not close application after execution, waiting for
                         next input
  --tl VAL               Pins filter viewport top left [lon; lat] (example:
                         [37.5600142,55.7484789])
  --br VAL               Pins filter viewport bottom right [lon; lat] (example:
                         [37.5600142,55.7484789])
  --edge-info-radius VAL Print edge id to nearest fixed point detailed info to
                         edge_info.json. Considering edges within given radius
                         from every fixed point
  --edge_visualization_radius
                         Print visualization of edges to edge_visualization.yson, format is compatible with easyview. Considering edges within given radius
                         from every fixed point
  --concaveness          How concave should the concave hulls be (if edge_visualization_radius is given). Above 0. High values lead to more 
                         convex shapes, 1.0 is fairly concave and should probably be used. If not given, return convex hull.
  --length_threshold_    Segments below this length (meters) will not be considered for further detalization. Default is 0.01.
  --edge-visualization-input-file
                         Skip all other calculations and take edges info from this file.
  --fixed-points-input-file
                         Skip all other calculations and print centers of edges belonging to the fixed points.
  --early-exit VAL       Percentage of covered pins allowing early execution
                         ending (example 98.5)
  --precalc-edges-distance VAL
                         Distance to gather reverse edges in smart placing part
                         of algorithm (meters) (default: 3000)
  --graph-dir VAL        Path to graph data root dir
                         (default: "/usr/local/share/yandex/taxi/graph-test/graph3/")
```

Для запуска требуются данные графа дорог. Полный граф (который используется в тестинге и продакшене) занимает в оперативной памяти около 20гб и загружается порядка 10 минут  

Входной файл должен быть в формате json-lines – по 1 объекту на строку:
```
{"count":5608,"point":"[37.60490763739544,55.73199916260754]"}
{"count":3566,"point":"[37.53897944979584,55.74811575749375]"}
{"point":"[37.53178020818705,55.79116150172975]"}
```
Точки передаются в формате `[lon, lat]`.
`count` - количество пинов в данной точке (по умолчанию 1)

Если передана опция `interactive`, то после завершения расчетов приложение будет ждать новых опций командной строки. Таким образом можно сделать несколько расчетов без перезапуска приложения. Можно поменять любые параметры кроме `pins-file` и `graph-dir`.

Пример запуска в тестинге pin-storage:
`./surge-point-planter --pins-file=/var/cache/yandex/taxi-pin-storage/pins_totalpickup_moscow_month.txt --out-file=fixed_points.json --precalc-edges-distance=4200 --distances=30:500,50:1000,80:1500,90:2000,95:2500,98:4000 --early-exit=99 --interactive`
## Алгоритм работы

Предварительный этап:
1. Притягиваем пины из входного файла к ребрам графа
2. Для каждого ребра, на котором есть хоть один пин, находим набор ребер на расстоянии `<= precalc-edges-distance`, от которых можно добраться до этого ребра
3. Для каждого ребра с пинами находим точку, в которую чаще всего притягивались пины (наиболее популярное место для вызова такси с этого ребра)

Основной этап, повторяем пока на графе есть пины:
1. Рассчитываем радиус поиска, на основании процентного количества покрытых пинов и параметра `distances`
2. Если процент покрытых пинов больше значения `early-exit`, то завершаем работу
3. Основной шаг:
    3. Если радиус поиска не больше `precalc-edges-distance`, то по набору ребер, вычисленных в п.2 предварительного этапа, находим такое ребро, из которого достижим максимум пинов в данном радиусе
    4. Если радиус поиска больше `precalc-edges-distance`, то находим ребро с максимумом притянутых пинов
4. Ставим фиксированную точку в точку на ребре, найденную в п.3 предварительного этапа, либо в середину ребра
5. Запускаем поиск пути из поставленной фиксированной точки и убираем с графа все пины на расстоянии радиуса поиска
