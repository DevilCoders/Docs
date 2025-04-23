Скрипты для графа в нирване для определения стадии потерь документов (в частности cpa -- пока только их)

Граф работает следующим образом:
1) На вход получает json корзинку оффлайна
2) Скрипт from_offline_to_daas.py преобразует json в tsv для подачи на вход простукиванию
3) Выполняется простукивание на даасе c  rgb=blue
4) Для выхода этого скрипта анализируются найденные офферы или модели скриптом
get_doc_ids_from_daas_db.py

Вариант запуска:
python3 get_doc_ids_from_daas_db.py --input 33d7b44d-059c-4b96-9934-7e473ee88e77.db --with-rearr 'cpa_panther_blue_offer_tpsz=800;cpa_market_knn_blue_offers_top=500;market_cpa_search_mn_algo=MNA_fml_formula_0625_order_yeti_715651x0375_binary_logloss_715653_-4;market_cpa_textless_search_mn_algo=MNA_blue_textless_catboost_26653;market_cpa_enable_meta_head_rearrange=0' --add-offer-ids  > offer_on_white_trace_blue_formulas

--add-offer-ids -- добавляет id офферов
--add-model-ids -- добавляет к запросам id моделей для трейса
--with-rearr -- дополнительные rearr флаги

5) Выполняется простукивание со списокм урлов из предыдущего пункта, затем его результат проходит через декодер дааса

6) Далее рисуется статистика скриптом count_percentages.py

Пример:
python3 count_percentages.py --input offers_pool_tsv --output-counts counts.json --chart-title "Стадии потерь cpa документов" --output-chart chart.png
