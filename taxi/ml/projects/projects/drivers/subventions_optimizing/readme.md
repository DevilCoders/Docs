
1. cubic_helpers.py - functions for calculating orders_kpi and bonus_sum
2. nile_jobs.py - functions for preprocessing a) july's table b) goasha's metrics
3. apply_macro_model.py - main script

step 1 - other feats on nile (from Gosha and me) - check with July or write by myself noe?
step 2 - regular applying for (tz, params?); filter general sample
step 3 - multiply by gmv exp!
step 4 - make all parameters itertools product() -> yt table
step 5 - retrain model

launch_params = [
    'days_long',
    'min_orders_kpi',
    'complexity',
    'reward',
    'country',
    'from_to_hours',
]    
    
    
    # Model: extra_orders_percent
    # + acceptance_rate_prev_week 	r2: 0.4839, 	coef=-0.19847
    # + country_others 	r2: 0.5072, 	coef=-0.04487
    # + from_to_hours_8-19 	r2: 0.5456, 	coef=-0.14214
    # + tph_prev_week 	r2: 0.5561, 	coef=0.03233
    # + from_to_hours_7-22 	r2: 0.5626, 	coef=0.04958
    # + rider_cancel_longwait_and_driverrequest_share_prev_week 	r2: 0.5694, 	coef=-0.49858
    # + workshift_gmv_share_prev_week 	r2: 0.5782, 	coef=-0.04793
    # + month_06 	r2: 0.5842, 	coef=0.01673
    # + month_03 	r2: 0.5877, 	coef=0.03465
    # + month_04 	r2: 0.5908, 	coef=0.02235
    # + from_to_hours_7-21 	r2: 0.5932, 	coef=-0.10859
    # + new_drivers_per_active_prev_week 	r2: 0.5957, 	coef=-0.35048
    # + month_05 	r2: 0.598, 	coef=0.01375
    # + surged_trips_share_prev_week 	r2: 0.6004, 	coef=0.0283
    # + completed_to_request_prev_week 	r2: 0.6023, 	coef=0.08099
    # + mph_prev_week 	r2: 0.6077, 	coef=-8e-0
    # + avg_order_cost_prev_week 	r2: 0.6122, 	coef=7e-05
    # + trips_per_active_drivers_prev_week 	r2: 0.6147, 	coef=0.00036
    # + from_to_hours_6-24 	r2: 0.6156, 	coef=-0.02887
    
    # TODO: create the following features
    # max_orders_kpi_per_control_prev_week 	r2: 0.6135, 	coef=0.00324
    # avg_bonus_per_avg_kpi_per_city_prev_week 	r2: 0.6093, 	coef=-0.17133
    # drivers_done_goal_control_prev_week 	r2: 0.6112, 	coef=1.82811
    # avg_travel_distance_km_control 	r2: 0.6043, 	coef=0.00363
    # avg_orders_kpi_per_control_prev_week 	r2: 0.5289, 	coef=0.05167
    # expected_sub_gmv_exp 	r2: 0.4378, 	coef=1.37058
    
    
    # Model: extra sub 2 gmv
    # + acceptance_rate_prev_week 	r2: 0.7434, 	coef=-0.04613
    # + from_to_hours_8-19 	r2: 0.7718, 	coef=-0.05064
    # + avg_trips_surge_rate_prev_week 	r2: 0.7911, 	coef=0.02961
    # + tph_prev_week 	r2: 0.7994, 	coef=0.00531
    # + completed_to_request_prev_week 	r2: 0.8068, 	coef=0.0277
    # + month_11 	r2: 0.8089, 	coef=-0.00496
    # + country_Казахстан 	r2: 0.8106, 	coef=0.00243
    # + month_05 	r2: 0.8142, 	coef=0.00342
    # + month_08 	r2: 0.8152, 	coef=0.0024
    # + from_to_hours_7-24 	r2: 0.816, 	coef=0.0016
    # + workshift_gmv_share_prev_week 	r2: 0.8167, 	coef=-0.00363
    # + rider_cancel_longwait_and_driverrequest_share_prev_week 	r2: 0.8176, 	coef=-0.04989
    
    # TODO: create the following features
    # expected_sub_gmv_exp 	r2: 0.7095, 	coef=0.47681
    # avg_orders_kpi_per_control_prev_week 	r2: 0.7856, 	coef=-0.01117
    # drivers_done_goal_control_prev_week 	r2: 0.7956, 	coef=0.77005
    # avg_trips_control_prev_week 	r2: 0.8038, 	coef=-0.00023
    # avg_travel_distance_km_control 	r2: 0.8123, 	coef=0.0009
    
    
    
    # Вопросы к Гоше
    # 1. что с  currency_rate? там 3 вложенности диста, но будто не препроцессится.
    # Проверить, как на Казахстане работает
    # 2. поле mean_cost_21_tariff_zone в метриках всегда NULL https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi_ml/dev/drivers/doxgety_macro_models/tmp
    # Это поле используется в кубике в назначении kpi!
    # 3. city_cost_factor можно изменять в конфиге - что это?
    # 4. в каком случае остальные поля null?
    # 5. зачем нужен фильтр nf.custom(
    # lambda x: config.get('min_kpi_cut', 0) <= x <= config.get(
    # 'max_kpi', 180), 'orders_kpi')
    # 6. tariff_zone_tariff_zone - что это за поле?
    # 7. city_multiplier = 1 + (mean_cost_city - 130) / (2 * 130.0)
    # TypeError: unsupported operand type(s) for -: 'NoneType' and 'int'
    # 8. https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi_ml/dev/drivers/doxgety_macro_models/tmp награды 59200. и еще есть большие
    # в фильтрах mean_cost_21_tariff_zone, в функциях пр подсчете кпи и бонусов - mean_cost_city
