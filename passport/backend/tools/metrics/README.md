# passport-metrics
## Что это
Скрипт для парсинга логов и агрегации их в метрики, совместимые с пуш-апи голованом.

Воркфлоу предполагается следующий:
```
curl -d "`timetail -n 60 filename | passport-metrics -c project.conf`" http://localhost:11005 --connect-timeout 5
```

Последние 60 (например) секунд лога подаются на stdin скрипта, который запущен с конкретным конфигом.
Вывод работы скрипта уходит в агент голована через курл.

## Конфигурация
### Голован
```ini
[golovan]
itype=passport  # должен быть указан
prj=passport.passport-api  # должен быть указан
geo=myt  # если не указан, то будет вычислен автоматически по имени хоста, иначе none
ctype=testing  # если не указан, то будет вычислен автоматически через yenv.type
ttl=90  # по умолчанию 90, измеряется в секундах
```

### Метрика
```ini
[человеко-читаемое описание метрики, вместо комментария]
# Имя метрики, может быть шаблоном.
# Вместо ключей будут подставляться значения соответствующих столбцов из tskv.
# Все значения в логе, указанные в имени шаблона, должны быть не пустые.
# В качетсве переменной в шаблоне имени можно использовать {__aggregate__},
# куда подставится название агрегационной функции.
metric=builder.{service}.{http_code}.{response}_tmmm
# Будут отобраны записи в логе с service=blackbox или service=market.
filters.service=blackbox,market
# Будут отобраны записи в логе с http_code=200 или http_code=500.
filters.http_code=200,500
# Значением метрики будет не количество строк в логе, попавших
# под фильтры, а значение столбца duration из лога.
metric.value=duration
# Итоговое значение метрики будет поделено на значение этого параметра
# Можно использовать, например, для вычисления RPS.
scale_to_seconds_interval=60
# функции агрегации метрики
aggregate=min,max,avg
# Для работы с табличными логами, а не с tskv.
# Можно перечислить здесь имена столбцов и далее применять к ним фильтры,
# использовать их в имени метрики и т.п.
columns=column1,column2,column3
# разделитель, пробел - значение по умолчанию
columns.delimiter=" "
# игнорировать пустые столцбы или нет - например, подряд идущие пробелы - это пустота или несколько пустых столбцов?
columns.ignore_empty = t # t, true, yes, 1 для True, остальное False; по умолчанию True
# столбцы определяются регуляркой, параметр не применяется с другими параметрами columns*
columns.re=^(?P<column1>.+?) (?P<column2>.+?)$
# перепись значений столбцов 200 -> 2xx, 400 -> 4xx, 500 -> 5xx, т.д.
rewrite.http_code.re=^(\d)\d\d
rewrite.http_code.sub=\1xx
```

### Агрегационные функции

| Функция                 | Описание                |
| ----------------------- | ----------------------- |
| min                     | Минимум                 |
| max                     | Максимум                |
| sum                     | Сумма                   |
| avg                     | Среднее                 |
| median                  | 0.5 процентиль          |
| p_50                    | 0.5 процентиль          |
| p_90                    | 0.9 процентиль          |
| p_95                    | 0.95 процентиль         |
| p_98                    | 0.98 процентиль         |
| p_99                    | 0.99 процентиль         |
| non_negative_derivative | max(max(x) - min(x), 0) |
