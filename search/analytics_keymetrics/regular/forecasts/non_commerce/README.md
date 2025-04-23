# Прогноз Некоммерции JulFC 2022

### Artifacts
1. Raw data
   - source tables:
     - https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/fact/yan/v7.1.1/latest/revenue
     - https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/product_money_light/v2/
   - [example query to collect fact](https://yql.yandex-team.ru/Operations/Ypx0FLq3kwWV5lddysAbKNGi0Il3OisPw-E6l4BAb0k=)
2. Fact
   - format `date, network_type, ownership_type, segment, revenue`
   - [table](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/special/2022_JulFC/v1/train/non_commerce)
   - [query for v0](https://yql.yandex-team.ru/Operations/YqNN0QVK8EMtACoT7TDZAAqhm-u7ksHas2gvYcvUSk0=)
3. Forecast
   - format `date, cutoff, series, network_type, ownership_type, segment, revenue`
   - [table](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/special/2022_JulFC/v1/forecast/non_commerce)


### Forecasting

1. Create virtual env
2. Create analyticskeymetrics symlink
3. Change model and config files if necessary:
   1. non_commerce.py
   2. non_commerce.yaml
4. Run forecast with command
   - calculate locally
    ```shell
       python -m analyticskeymetrics.forecasting --cutoff=2022-06-05 --model=non_commerce --session=some_name --version-name=non_commerce --no-cache --horizon=1315 --skip-fact-uploading --skip-pred-uploading
    ```
   - calculate and upload to yt
    ```shell
       python -m analyticskeymetrics.forecasting --cutoff=2022-06-12 --model=non_commerce --version-name=non_commerce --no-cache --horizon=4000
    ```
