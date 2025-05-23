# Автостратегии в ДЦО

В этой директрии находится код модели, с которой будем проводить эксперимент в ДЦО. Результат этого кода - это воркфлоу,
из которого нужно будет скопировать кубики, находящие оптимальные цены для каждой категории товара, и кубики,
рассчитывающие корректировку маржи. Корректировка маржи нужна для того, чтобы попадать в контрльную маржу при
максимизации GMV.

`price_optimizer_task.py` - здесь находится оптимизатор цен. Класс `PriceOptimizerTask`.

`margin_correction_task.py` - а здесь происходит расчет корректировок маржи. Класс `MarginCorrectionTask`.

Аргументы `PriceOptimizerTask`:

|Аргумент   |Описание   |Допустиые значения   | Значение по умолчанию   |
|---|---|---|---|
|msku_data_path   |Путь до таблицы со списком мскю и их атрибутами  | путь на yt  | -  |
|opt_prices_dir   |Директория для таблиц с оптимальными ценами   |путь на yt | -  |
|manual_margin_correction   |Ручная корректировка маржи, чтобы учесть непопадание в предыдущий день   |int   |0   |
|margin_correction_table |Таблица с суммарной маржой по сегментам за предыдущий день. Используется для расчета корректировок |путь на yt |- |
|category |Название категории товара. Например, sport/kids |str |- |
|use_manual_corrections |Флаг, указывающий, нужно ли использовать ручные корректировки маржи. Может принимать строковые значения true или false. При true используются подаваемые на вход ручные корректировки, а автоматические игнорируются + выключается avg модель. При false используются автоматические корректировки на обеих моделях, ручные игнорируются. | true/false | -|
|timestamp|Таймстемп, по которому будет названа таблица |str: DD-MM-YYYYTHH:MM:SS | - |
|model_type| Модель эластичности, которой ищем оптимальные цены| linear, sigmoid| linear |
|model_parameters| параметрамы модели через знак `=`, разделенные запятыми. enable_avg_model - Вкл/выкл модель усреднений. sigmoid_model_path - путь до сигмоидной модели на YT  | `enable_avg_model=true`, `sigmoid_model_path=//yt/path`, `enable_avg_model=true,sigmoid_model_path=//yt/path`| str |
|price_lower_bound| Нижняя граница оптимальной цены | float | 0.9|
|price_upper_bound| Верхняя граница оптимальной цены | float | 1.07|
|experiment_split_size| Доля пользователей в экспериментальном сплите | float | 0.2 |
|optimize_gmv| Оптимизироваться под gmv или под cost (true - для gmv, false - для cost) | true/false | true |

Аргументы `MarginCorrectionTask`:

|Аргумент   |Описание   |Допустиые значения   | Значение по умолчанию   |
|---|---|---|---|
|result_path |Директория, куда запишем результат|путь на yt |- |
|timestamp |Таймстемп запуска |str %Y-%m-%dT%H:%M:%S |- |
|opt_prices_dir |Директория, в которой лежат оптимальные цены за прошлый запуск |путь на yt |- |
|category |Название категории товара. Например, sport/kids |str |- |
|path_to_dashboard |Путь до таблицы, используемой под дешбордом |str |- |
|experiment_split |Id экспериментального сплита |str |- |
|control_split |Id контрольного сплита |str |- |
|window_size_days |Размер окна в днях, по которым считаем среднюю коррекцию маржи |int |7 |
