# ML Pipeline

```sh
ya make
```

# *I. Чаты*

## 1. Data Preprocessing

* Получение изначальной выборки из таблицы с тикетами
  * Станция
  ```sh
  ./chats/data/bin/extract/extract \
      --input_data //home/samsara/prod_private/ticket \
      --output_data //home/sp/ml/station/data/raw/data \
      -q 100480 \
      --start_dt 2021-03-01
  ```
  * Услуги
  ```sh
  ./chats/data/bin/extract/extract \
      --input_data //home/samsara/prod_private/ticket
      --output_data //home/sp/ml/uslugi/data/raw/data \
      -q 101093 \
      --start_dt 2021-03-01
  ```
  * Geoproduct
  ```sh
  ./chats/data/bin/extract/extract \
      --input_data //home/samsara/prod_private/ticket
      --output_data //home/sp/ml/geoproduct/data/raw/data \
      -q 100081 \
      --start_dt 2021-03-01
  ``` 

* Обработка изначальных таблиц: схлопывание нескольких артиклов в один
  * Станция
  ```sh
  ./chats/data/bin/preprocess/preprocess \
      --input_data //home/sp/ml/station/data/raw/data \
      --output_data //home/sp/ml/station/data/preprocessed/data
  ```
  * Услуги
  ```sh
  ./chats/data/bin/preprocess/preprocess \
      --input_data //home/sp/ml/uslugi/data/raw/data \
      --output_data //home/sp/ml/uslugi/data/preprocessed/data
  ```
  * Geoproduct
  ```shßß
  ./chats/data/bin/extract/extract \
      --input_data //home/sp/ml/geoproduct/data/raw/data \
      --output_data //home/sp/ml/geoproduct/data/preprocessed/data
  ``` 

* Матчинг знаний и подготовка таргетов
  * Станция
  ```sh
  ./chats/data/bin/prepare/prepare \
    --input_data //home/sp/ml/station/data/preprocessed/data \
      --output_data //home/sp/ml/station/data/preprocessed/prepared \
      --product_tag station
  ```
  * Услуги
  ```sh
  ./chats/data/bin/prepare/prepare \
      --input_data //home/sp/ml/uslugi/data/preprocessed/data \
      --output_data //home/sp/ml/uslugi/data/preprocessed/prepared \
      --product_tag uslugi
  ```
  * Geoproduct
  ```sh
  ./chats/data/bin/prepare/prepare \
      --input_data //home/sp/ml/geoproduct/data/preprocessed/data \
      --output_data //home/sp/ml/geoproduct/data/preprocessed/prepared \
      --product_tag advertisement
  ```

* Train-test split пока в [ноутбуке](https://a.yandex-team.ru/arc/trunk/arcadia/junk/vmt29/jupyter/OpenFromYT/050-generate_targets.ipynb?rev=9227894) из-за долгого отрабатывания подготовки данных.  
Подготовленные данные хранятся вот [здесь](https://yt.yandex-team.ru/hahn/navigation?path=//home/sp/ml/station/data).


## 2. Training

в процессе 

* Baseline (FastText + CatBoost)
* Search Bert
* SupportAI (DeepPavlov Bert)
  

