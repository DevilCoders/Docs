# Учим tlm - dump task

## Получаем таск графа

Команда запуска

    ./tenfifty_tool ../example_tasks/train_catboost.yaml dump_task -o dump_task.yaml

{% cut "dump_task.yaml" %}

``` yaml
graph:
  get_table:
    action: get_dataset
    output:
      default_name_output: dataset
    parameters:
      tables:
      - //home/ads/tenfifty/examples/simple_pool
  split_pool:
    action: run_yql
    do_after: get_table
    input:
      default_name_input: dataset
    output:
      default_name_output:
      - train_dataset
      - test_dataset
    parameters:
      query: 'INSERT INTO $$output[0] WITH TRUNCATE

        SELECT * FROM $$input[0]

        WHERE f3 <= 0.5;


        INSERT INTO $$output[1] WITH TRUNCATE

        SELECT * FROM $$input[0]

        WHERE f3 > 0.5;

        '
  prepare_pools:
    action: prepare_catboost_pool
    do_after: split_pool
    input:
      default_name_input:
      - train_dataset
      - test_dataset
    output:
      default_name_output:
      - train_pool
      - test_pool
    parameters:
      column_description:
        f1: Num
        f2: Num
        f3: Num
        group_id: GroupId
        target: Label
      feature_order:
      - f1
      - f2
      - f3
  train_model:
    action: train_catboost_model
    do_after: prepare_pools
    input:
      test: test_pool
      train: train_pool
    output:
      default_name_output: model
    parameters:
      gpu_type: NONE
      iterations: 100
      loss_function: Logloss
      master_gpu_max_ram: 80000
      slave_gpu_max_ram: 80000
  upload_to_yt:
    action: upload_model_to_yt
    do_after: train_model
    input:
      default_name_input: model
    parameters:
      path: trained_catboost_model
  apply_model:
    action: apply_catboost_model
    do_after:
    - split_pool
    - train_model
    input:
      dataset:
      - train_dataset
      - test_dataset
      model: model
    output:
      default_name_output:
      - train_dataset
      - test_dataset
    parameters:
      output_column: RawPrediction
  eval_metrics:
    action: eval_metrics
    do_after: apply_model
    input:
      default_name_input:
      - train_dataset
      - test_dataset
    output:
      default_name_output:
      - train_dataset
      - test_dataset
    parameters:
      metrics:
      - rmse
      prediction: RawPrediction
      target: target
```

{% endcut %}
