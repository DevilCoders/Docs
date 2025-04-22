**Последовательность**
Обучение:
mk_train_features_and_targets.py
mk_train_val_mxnet_datasets.py
fit_mse_models.py
Применение:
mk_features.py
apply_mse_models.py

**Общее** 

model_class_base.py
- BaseModelConfig 
Базовый класс конфига модели. Хранит описание фичей, умеет доставать из рекорда фичи и таргет.
- BaseModel 
Базовый класс модели. Умеет скачивать модель с YT и заружать из локальной директории.

model_class_mse_qs.py
- MseQsModelConfig
 Класс конфига MseQs модели. Дополнительно хранит инфу об окне и оффсете, а отдавая фичи, досчитывает день недели и фичу-эвристику с лагом.
- MseQsModel
 Класс модели MseQs. Дополнительно хранит инфу о функции потерь, умеет делать predict(record) и отдавать разные индексы для строки фичей (ignore, categorical).
 
config_mse.py
Основной конфиг

my_mse_model_config.json
Конфиг фичей
 
mk_features.py
Готовит фичи на одну дату.
 
apply_mse_models.py
Применяет все модели, выдает одну таблицу с предсказаниями и эвристиками для MSE.


**Парсер конфигов**

config_parser.config_parser.py
- JsonConfigParser
а) Парсит готовые конфиги фичей для модели и отдает словарь {название фичи: тип фичи}.
б) Парсит сырой конфиг фичей из экстрактора и сохраняет конфиг фичей для модели, используя SOURCES, FEATURE_WINDOW_SIZES и т.д.
(готовый конфиг - фичи вида 21_success_orders, сырой - {aggr}_success_orders)

config_parser.features_config.json
Сырой конфиг возможных фичей из экстрактора. TODO: должен быть сырой конфиг ВСЕХ фичей из экстрактора.

**Параметры**

zoo.drivers.extractors.py
- DAILY_WINDOW Максимальное окно для подсчета ежедневного кол-ва поездок success_orders_-{n}. Нужно для дальнейшего подсчета lagged_success_orders: кол-во поездок из окна в прошлом, равному окну таргета и с таким же набором дней недели.

config_mse.py
- FEATURE_WINDOW_SIZES
- LOG_SOURCES
- TARGET_FIELD Шаблон для таргета (NB: этот параметр пока лучше не трогать!)

pipeline_apply.py
- date Дата, на которую применяем модель
- predictions_city_field Поле города, которое оставить с таблице с пердсказаниями.


 
 
 
 


