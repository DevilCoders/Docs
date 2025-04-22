# Тесты для проверки таргетов ТВ

тикет -  https://st.yandex-team.ru/QUASARINFRA-670

## тестовый запуск из терминала

### cv9632
Список ресурсов - [ANDROID_TV_MT_9632_CV_REPORT](https://sandbox.yandex-team.ru/resources?type=ANDROID_TV_MT_9632_CV_REPORT)
```
# сборка
ya make sandbox/projects/tv/target_check/mt9632_cv

# запуск
./sandbox/projects/tv/target_check/mt9632_cv/target_check_mt9632_cv run \
--type TARGET_CHECK_CV_9632 \
--enable-taskbox '{"custom_fields": [{"name":"report_resource", "value":"3200555611"}]}'
```

### cv6681
Список ресурсов - [ANDROID_TV_MT_6681_CV_REPORT](https://sandbox.yandex-team.ru/resources?type=ANDROID_TV_MT_6681_CV_REPORT)
```
# сборка
ya make sandbox/projects/tv/target_check/mt6681_cv

# запуск
./sandbox/projects/tv/target_check/mt6681_cv/target_check_mt6681_cv run \
--type TARGET_CHECK_CV_6681 \
--enable-taskbox '{"custom_fields": [{"name":"report_resource", "value":"3245708080"}]}'
```

### cvte9632
Список ресурсов - [ANDROID_TV_MT_9632_CVTE_REPORT](https://sandbox.yandex-team.ru/resources?type=ANDROID_TV_MT_9632_CVTE_REPORT)
```
# сборка
ya make sandbox/projects/tv/target_check/mt9632_cvte

# запуск
./sandbox/projects/tv/target_check/mt9632_cvte/target_check_mt9632_cvte run \
--type TARGET_CHECK_CVTE_9632 \
--enable-taskbox '{"custom_fields": [{"name":"report_resource", "value":"3245620149"}]}'
```

### cvte6681
Список ресурсов - [ANDROID_TV_MT_6681_CVTE_REPORT](https://sandbox.yandex-team.ru/resources?type=ANDROID_TV_MT_6681_CVTE_REPORT)
```
# сборка
ya make sandbox/projects/tv/target_check/mt6681_cvte

# запуск
./sandbox/projects/tv/target_check/mt6681_cvte/target_check_mt6681_cvte run \
--type TARGET_CHECK_CVTE_6681 \
--enable-taskbox '{"custom_fields": [{"name":"report_resource", "value":"3245625365"}]}'
```

### cvte9632_11
Список ресурсов - [ANDROID_TV_MT_9632_11_CVTE_REPORT](https://sandbox.yandex-team.ru/resources?type=ANDROID_TV_MT_9632_11_CVTE_REPORT)
```
# сборка
ya make sandbox/projects/tv/target_check/mt9632_11_cvte

# запуск
./sandbox/projects/tv/target_check/mt9632_11_cvte/target_check_mt9632_11_cvte run \
--type TARGET_CHECK_CVTE_9632_11 \
--enable-taskbox '{"custom_fields": [{"name":"report_resource", "value":"3245640668"}]}'
```

### cvte9256
Список ресурсов - [ANDROID_TV_MT_9256_CVTE_REPORT](https://sandbox.yandex-team.ru/resources?type=ANDROID_TV_MT_9256_CVTE_REPORT)
```
# сборка
ya make sandbox/projects/tv/target_check/mt9256_cvte

# запуск
./sandbox/projects/tv/target_check/mt9256_cvte/target_check_mt9256_cvte run \
--type TARGET_CHECK_CVTE_9256 \
--enable-taskbox '{"custom_fields": [{"name":"report_resource", "value":"3245635574"}]}'
```

### cvte351
Список ресурсов - [ANDROID_TV_HISI_351_CVTE_REPORT](https://sandbox.yandex-team.ru/resources?type=ANDROID_TV_HISI_351_CVTE_REPORT)
```
# сборка
ya make sandbox/projects/tv/target_check/hisi351_cvte

# запуск
./sandbox/projects/tv/target_check/hisi351_cvte/target_check_hisi351_cvte run \
--type TARGET_CHECK_CVTE_351 \
--enable-taskbox '{"custom_fields": [{"name":"report_resource", "value":"3245556980"}]}'
```

### rt2842
Список ресурсов - [ANDROID_TV_RT_2842_HIKEEN_REPORT](https://sandbox.yandex-team.ru/resources?type=ANDROID_TV_RT_2842_HIKEEN_REPORT)
```
# сборка
ya make sandbox/projects/tv/target_check/rt2842_hikeen

# запуск
./sandbox/projects/tv/target_check/rt2842_hikeen/target_check_rt2842_hikeen run \
--type TARGET_CHECK_HIKEEN_2842 \
--enable-taskbox '{"custom_fields": [{"name":"report_resource", "value":"3248439882"}]}'
```

### rt2871
Список ресурсов - [ANDROID_TV_RT_2871_HIKEEN_REPORT](https://sandbox.yandex-team.ru/resources?type=ANDROID_TV_RT_2871_HIKEEN_REPORT)
```
# сборка
ya make sandbox/projects/tv/target_check/rt2871_hikeen

# запуск
./sandbox/projects/tv/target_check/rt2871_hikeen/target_check_rt2871_hikeen run \
--type TARGET_CHECK_HIKEEN_2871 \
--enable-taskbox '{"custom_fields": [{"name":"report_resource", "value":"3245502227"}]}'
```
