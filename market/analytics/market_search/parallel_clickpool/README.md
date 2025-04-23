#### Сбор пула для обучения кликовой формулы колдунщиков

Хитман: https://hitman.yandex-team.ru/projects/market_click_pool_prod/market_parallel_clickpool
Тикет: https://st.yandex-team.ru/MSA-1368


Пайплайн:
1. collect_docs.sql
    * джоиним parallel-report-log, market_wizards_squeeze, market-shows-log
    * собираем метрики (заказы, dwelltime и т.п.) за кликами по врезке
    * дебаг потерянных reqid, офферов при джоинах
    * параметры:
        - $date_from, $date_to - период сбора
        - $output_table_path_prefix - в какую папку сохранять результат, таблицы и статистику для дебага
        - $rewrite_existing_tables - если true, то при наличии реультирующей таблицы в папке по пути $output_table_path_prefix не будет пересчета. Сделано на всякий случай, если кеш в YQL и Нирване умрет
    * Результат - таблица pool/docs, в которой строка - это пара запрос-документ
2. append_features.sql
    * к результату 1. джоиним фичи
    * дебаг потерянных reqid, офферов и моделей при джоинах
    * параметры:
        - $date_start, $date_to - период сбора
        - $output_table_path_prefix - в какую папку сохранять результат, таблицы и статистику для дебага
        - $rewrite_existing_tables - если true, то при наличии реультирующей таблицы в папке по пути $output_table_path_prefix не будет пересчета. Сделано на всякий случай, если кеш в YQL и Нирване умрет
        - $interval_size - если это число короче длины периода сбора, то джоин делится на несколько подинтервалов длины $interval_size, чтобы MapReduce операции не падали по памяти.
    * Результат: pool/docs_with_features


* sampling.sql - deprecated. Был нужен, когда модели и оффера писались в feature-log по-разному. Сейчас это не так. Если вдруг нужно просемплирвать, лучше написать скрипт самостоятельно.
