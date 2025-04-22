0) Нужно создать в директории json_files конфиг .json нужного формата

1) Подсчитываем статистики

Пример запуска: 
```bash
python -m calc_stats \
--config json_files/experiment_2019_02_04_upd.json \
--yt-work-dir //home/taxi_ml/dev/drivers_churn/experiments/
```

Возвращается табличка вида 
//home/taxi_ml/dev/drivers_churn/experiments/experiment_2019_04_23/unique_driver_id_calls_goals_group_cut_2019-03-27_2019-05-15, 
где unique_driver_id, 
bonus_sum, orders_kpi, tariff_zone (подтягиваются, если подать на вход табличку после отрабатывания скрипта taxiperssubv вида https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi-analytics/personal_subventions/TAXIPERSSUBV_251_drivers_exp_comm_1554462942&offsetMode=row)
и поля с названиями периодов времени (чтобы из одной таблицы смотреть и на AA-тесты)


2) Считаются p-value и доверительные интервалы для относительного прироста и стоимости заказв и SH

Пример запуска:

```bash
python -m significance \
--yt-work-dir //home/taxi_ml/dev/drivers_churn/experiment/tmp/experiments/ \
--period-of-interest "2019-02-06,2019-02-13" \
--period-of-interest-future "2019-02-06,2019-02-13" \
--config-path json_files/experiment_2019_02_04_upd.json \
--exp-group 'ml_group_cut' \
--control-group 'control_ml_group_cut' \
--type-of-exp 'goals_calls'
```

P.S. файлы _v0 - версия с переномировкой на прошлые недели
