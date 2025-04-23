### BLRT-79

Как поскорить баннера в YT?

./am_bl_sr_tool run-sr-mr -s //home/advquality/users/shevkunov/BLRT-79_100k_samples -d //home/advquality/users/shevkunov/BLRT-79_100k_samples_trans -c sr_config.json (-c [2356059370](https://sandbox.yandex-team.ru/resource/2356059370/view))

Как сделать пул для CatBoost по SR?

Убеждаемся что в исходной таблице выставлен таргет, скорим её, потом делаем пул так (для теста есть опция)

./am_bl_sr_tool run-make-pool -s //home/advquality/users/shevkunov/BLRT-79_100k_samples_trans -d //home/advquality/users/shevkunov/BLRT-79_100k_samples_trans_pool -m (model_id)


Какие есть пулы?

https://yt.yandex-team.ru/hahn/navigation?path=//home/advquality/users/shevkunov/BLRT-79_2.2M_samples (**deprecated**)
[0.8417 AUC граф](https://nirvana.yandex-team.ru/flow/7c19f410-1e23-4c31-8b14-6133fb5215d3/171844e5-e1d3-4ed6-914e-9cfe2771e476/graph)

https://yt.yandex-team.ru/hahn/navigation?path=//home/advquality/users/shevkunov/BLRT-79_10M_pool_train
https://yt.yandex-team.ru/hahn/navigation?path=//home/advquality/users/shevkunov/BLRT-79_10M_pool_val
[0.8409 AUC граф](https://nirvana.yandex-team.ru/flow/7c19f410-1e23-4c31-8b14-6133fb5215d3/ac7a5f5f-0bb6-4536-adf0-6b1144d61146/graph)

[0.855 AUC граф](https://nirvana.yandex-team.ru/flow/7c19f410-1e23-4c31-8b14-6133fb5215d3/02e00cfc-eced-4a69-ba72-dff2b1c07eb2/graph)

[0.888 AUC граф (тест)](https://nirvana.yandex-team.ru/flow/ee469bd8-1668-4c13-9f51-801c96475d5e/cdc68e18-f209-4e7d-8c10-bf6af579a4f9/graph)


https://yt.yandex-team.ru/hahn/navigation?path=//home/advquality/users/shevkunov/BLRT-79_20M_pool_train
https://yt.yandex-team.ru/hahn/navigation?path=//home/advquality/users/shevkunov/BLRT-79_20M_pool_val
[0.897 AUC граф](https://nirvana.yandex-team.ru/flow/3b17b85c-5809-4714-859c-96f7aca6135e/9bff380d-9f36-4381-8634-8223f1b9c8ff/graph)

https://yt.yandex-team.ru/hahn/navigation?path=//home/advquality/users/shevkunov/BLRT-79_10M_dyn_pool_train
https://yt.yandex-team.ru/hahn/navigation?path=//home/advquality/users/shevkunov/BLRT-79_10M_dyn_pool_val
[0.726 AUC граф](https://nirvana.yandex-team.ru/flow/3b17b85c-5809-4714-859c-96f7aca6135e/3499ff41-fab8-4c98-9633-4bf24d60c982/graph)

Как теперь модельку-то обучить?

https://nirvana.yandex-team.ru/flow/7c19f410-1e23-4c31-8b14-6133fb5215d3/fadba4ba-4363-4e9e-a0ba-c323498f7239/graph

Не забудьте подставить свои таблички

#### Сборка cb-пула по фактор-логам

Берём собранные с помощью run-collect-blrt-flog факторлоги, собираются в https://hitman.yandex-team.ru/projects/blsr-tools/blsr-flog-collector/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20 и для динамиков и для смартов (пока что пишутся в //home/advquality/users/shevkunov/blsrflogs и //home/advquality/users/shevkunov/blsrflog_dyn)

Собираем пул за конкретные даты (сегодняшний день не брать), указываем нужный префикс (//home/bannerland/perf/full_state/archive для смартов, //home/bannerland/dyn/full_state/archive для динамиков) и модель (сейчас - 1 для смартов, 2 для динамиков)
> ya make -r && ./am_bl_sr_tool run-join-blrt-flog  --src-flog //home/advquality/users/shevkunov/blsrflogs -d your_awesome_table --lower-date 20211107 --upper-date 20211108 -vvv --src-bid-info-pref //home/bannerland/perf/full_state/archive -m 2


Выкидываем баннера у которых не было показов (можно ещё посемплировать сверху нули и единицы через -n 0.1 -z 0.05 чтобы пул был полечге)
> ./am_bl_sr_tool run-sample-pool -s your_awesome_table -d your_awesome_table_train -o true

Собираем аналогично val и test (если нужно не для статистик) за **последующие** даты, семплируем до нужного размера.


### BLRT-87

Запустить шайтан-пайплайн с генерацией и SR:
./am_bl_sr_tool run-gen-mr -s //home/advquality/users/shevkunov/BLRT-87_perf_distillation_pool_v0_flat -d //home/advquality/users/shevkunov/BLRT-87_perf_distillation_pool_v0_flat_dst -c gen_config.json

Сварить из поскоренных ассетов пул для дистилляции:
./am_bl_sr_tool run-make-gen-distil-pool -s //home/advquality/users/shevkunov/BLRT-87_perf_distillation_pool_v0_flat_dst -d //home/advquality/users/shevkunov/BLRT-87_perf_distillation_pool_v0_flat_dst_distil -l 8192

Собрать ресурс для генерации:

1. Запустим pipeline генерации как описано выше ya make -r && ./am_bl_sr_tool run-gen-mr -s //home/advquality/users/shevkunov/BLRT_114_dyn_tao_1m_parsed_noperlc_v3 -d //home/advquality/users/shevkunov/BLRT_114_dyn_tao_1m_parsed_noperlc_v3_clean -c gen_config.json -m
39999 -vvv --just-clean true
2. Появится строчка "New blgen_resource.bin resource created."
3. Ресурс готов и лежит папке запуска
4. Если не хватает какие-то ресурсов из конфига называющихся как ...sbr123456789... - это номер ресурса в sandbox, их нужно скачать и положить в папку запуска

