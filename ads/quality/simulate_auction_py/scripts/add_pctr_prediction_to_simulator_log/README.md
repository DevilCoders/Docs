Добавляет колонки с предсказаниями ctr'а в симуляторный лог _desktop_russia_.

Как запускать:
```
./add_pctr_prediction_to_simulator_log --src {src} --dst {dst} --dumps pctr_pred_field:{task_id}/2021-06-14 --config config.yaml --start_date 2021-06-21 --end_date 2021-06-28
 ```

Параметры:
- src, dst &ndash; пути до таблиц в Хане;
- dumps: разделенные запятыми пары {predict_field}:{dump_path}
- start_date, end_date &ndash; даты в формате YYYY-MM-DD. Конечная дата end_date при этом не включается в рассмотрение.
- config &ndash; путь до yaml-конфига, содержащего ключи _formula_params_, _lmset_, _tsars_ (см. config_example.yaml)
