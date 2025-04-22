## MapReduce Transfer

[Скрипт](./map_reduce_transfer) обкачивает mapreduce продовые модели, лежащие на yt, и переносит их на сендбокс в формате ML_STORAGE.

## Check Models Uploaded

[Скрипт](./check_models_uploaded) проверяет, все ли продовые модели map_reduce/ml_engine находятся на сэндбоксе в формате ML_STORAGE.

## Get Prod LM Models Config

[Скрипт](./get_prod_lm_models_config) вытаскиывает конфиги продовых линейных моделей из MySQL.

## Generate LM validation options

[Скрипт](./generate_lm_validation_options) генерирует опции валидации для линейки и добавляет их в существующий конфиг. Генерация производится согласно опциям генерации каждого отдельного dump part-а. Аналог `AutoGenerate` в `experiment-switcher.pl`.
