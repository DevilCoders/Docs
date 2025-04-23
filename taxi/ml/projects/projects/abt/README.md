### Как заполнить конфиг

#### Описание входных данных для расчета прекомпьютов

Путь до таблицы с наблюдениями на YT:
- наличие схемы обязательно
- каждая строчка соответствует одному наблюдению – заказ, сессия, клик, пользователь-день, ...
```yaml
input_path: //home/taxi_ml/production/abt/observations/taxi_orders
```

Путь для хранения прекомпьютов. Может быть любым, но для единообразия лучше пока класть в `//home/taxi_ml/dev/abt/precomputes/`
```yaml
output_path: //home/taxi_ml/dev/abt/precomputes/users_ml_taxi_orders
```

Список ответственных за данные и метрики. 
```yaml
owners:
  - tilgasergey
  - sergeytilga
```

Название колонки с временем в UTC в формате iso 8601 (строчка). Возможные варианты: "2020-01-01", "2020-01-01 11:22:33", "2020-01-01T11:22:33.456".
```yaml
time: utc_dttm
```

Названия колонок с "фичами", например, числители и знаменатели для расчетам метрик. Важно, что это не названия финальных метрик, а именно базовые статистики для их расчета.
```yaml
measures:
  - orders
  - success_orders
  - unsuccess_orders
```

#### Описание метрик

Список групп метрик. Названия на русском необязательны, но очень желательны.
```yaml
metrics_groups:
  - group_name: taxi_orders_ml
    group_name_rus: Метрики заказов Такси (ML)
    metrics:
      ...
```

Каждая метрика собирается из доступных фичей (measures).
Сейчас поддерживаются только метрики вида `x` и `x/y`. Для первого варианта нужно указать только num, для второго — num и denom.
```yaml
...
    - name: orders
      name_rus: Количество заказов
      num: orders
      greater_is_better: true

    - name: success_orders_rate
      name_rus: Конверсия из заказа в успешный заказ
      num: success_orders
      denom: orders
      greater_is_better: true
```

Поле `greater_is_better` влияет на цвет прокраски в дашборде. Например, если `true` и метрика значимо увеличилась, то прокрасится в зеленый цвет.
Если характер изменения неизвестен, то можно не указывать. В этом случае будет прокрашиваться в желтый цвет.

Также можно объединять фичи и суммировать значения.
```yaml
...
    - name: driving_waiting_time
      name_rus: Среднее время подачи + ожидания
      num: [driving_time, waiting_time]
      denom: [success_orders, unsuccess_orders]
```
