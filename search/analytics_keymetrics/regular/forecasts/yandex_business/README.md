# Прогноз Я.Бизнес для JulFC 2022

### Artifacts
1. Raw data
   - [table](https://yt.yandex-team.ru/hahn/navigation?path=//home/comdep-dwh/users/lgdavtyan/product_money/ya_business_all)
   - [query](https://yql.yandex-team.ru/Operations/YqCv7K5ODyxPiYCMUpxwG0dJSwXrnEWU42VRXWCd2SU=)
   - responsible @lgdavtyan
2. Fact
   - [table](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/special/2022_JulFC/v1/train/yandex_business)
   - [query for v0](https://yql.yandex-team.ru/Operations/YqNk_Lq3k4fbwcC0-Dw_L4kxQFBkKFMIdHULWoyAldw=)
4. Forecast
   - [table](https://yt.yandex-team.ru/hahn/navigation?path=//home/analyticskeymetrics/export/forecasts/special/2022_JulFC/v1/forecast/yandex_business)


### Forecasting

1. Create virtual env
2. Create analyticskeymetrics symlink
3. Change model and config files if necessary:
   1. yandex_business.py
   2. yandex_business.yaml
4. Run forecast with command
   - calculate locally
    ```shell
       python -m analyticskeymetrics.forecasting --cutoff=2022-06-05 --model=yandex_business --session=some_name --version-name=yandex_business --no-cache --horizon=1315 --skip-fact-uploading --skip-pred-uploading
    ```
   - calculate and upload to yt
    ```shell
       python -m analyticskeymetrics.forecasting --cutoff=2022-06-12 --model=yandex_business --version-name=yandex_business --no-cache --horizon=4000
    ```
