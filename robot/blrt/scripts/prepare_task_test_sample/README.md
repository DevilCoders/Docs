## Как готовить семпл для тестов тасковоркера

1. Готовим таблички с профилями: запускаем extract_sampled_profiles.yql
2. Создаем qyt очереди и заполняем их: create_queues.sh
3. Скачиваем семпл: ./robot/blrt/scripts/prepare_test_sample/download_sample.sh //home/jupiter-test/blrt_users/alexanderplat_task_sample ~/sample_result
4. Копируем старый data_spec.json (там правильные схемы таблиц, нет лишних атрибутов yql): cp ~/old_sample/data_spec.json ~/sample_result/data_spec.json
5. Упаковываем и заливаем новый семпл: (cd ~/sample_result && tar -cf blrt_task_perf.tar *)
