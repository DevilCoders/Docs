# its-client для Яндекс Деплоя

Временное решение, пока в деплое не поддержат ITS: [DEPLOY-1367](https://st.yandex-team.ru/DEPLOY-1367).

## Как добавить в свой сервис
1. Инклюдим в `package.json` своего сервиса `pkg.json`
2. Добавляем в настройки сервиса новый workload
   1. В init секцию добавляем генерацию конфига для its_client: `app/bin/gen_its_client_config.sh`
   2. Стартуем its_client со сгенеренным конфигом: `app/bin/its_client --console -c /app/conf/its_client/cfg.yaml`
   3. [пример](https://deploy.yandex-team.ru/stages/testing_market_datacamp-miner-external/config/du-miner/box-miner_box/wl-its_workload)
