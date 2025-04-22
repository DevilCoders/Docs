## Как готовить семпл для тестов

1. Готовим табличку с таскоофферами. Можно запустить yql как в prepare_input_tasks_and_offers.yql
2. Запускаем local_blrt над этими таскоофферами с sample_config'ом:

    2.1. Правим local_blrt_config.json: добавляем "blrt_config_override_sample.pb.txt" к worker_config.config_overrides

    2.2. Запускаем из-под robot-jupiter-night: ./robot/blrt/test/local/run.py -t perf -b ./robot/blrt/test/local/local_blrt_config.json -i //home/robot-dev/alexanderplat/sample_task_and_offers
3. Ждем, пока local_blrt отработает
4. Запускаем экспорт табличек для итогого семпла: берем yql из export_sample_tables.yql
5. Скачиваем семпл: ./robot/blrt/scripts/prepare_test_sample/download_sample.sh //home/robot-dev/alexanderplat/sample_result ~/sample_result
6. Копируем старый data_spec.json (там правильные схемы таблиц, нет лишних атрибутов yql): cp ~/old_sample/data_spec.json ~/sample_result/data_spec.json
7. Упаковываем и заливаем новый семпл: (cd ~/sample_result && tar -cf blrt_perf.tar *)
