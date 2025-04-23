Скрипт, создающий граф большого обхода при помощи либы "Вальгалла" и выкладывающий его в нирвану. Для локального запуска необходимо положить в ~/.yt/token токен для YT и в ~/.yql/token токен для YQL. Запуск производить при помощи утилиты ya.make предварительно заменив  ya.make на ya.make.local и изменив в нем передаваемые параметры по аналогии с приведенными:

    --yt-token robot-mrk-rbtms-test-yt-token
    --yql-token robot-mrk-rbtms-test-yql-token
    --mr-account market/development/ir/danilptashnik/work_dir
    --work-dir //home/market/development/ir/danilptashnik/work_dir
    --input-table-name //home/market/testing/ir/edlp/watson_sample/04062019_50K
    --uc-result-dir //home/market/development/ir/danilptashnik/test
    --output-table //home/market/development/ir/danilptashnik/test/result
    --output-table-dir //home/market/development/ir/danilptashnik/test
    --stats-dir //home/market/development/ir/danilptashnik/work_dir/stats
    --current-stats-dir //home/market/development/ir/danilptashnik/work_dir/stats/current
    --errors-dir //home/market/development/ir/danilptashnik/work_dir/errors
    --ref-shops //home/market/production/monetize/dynamic_pricing/reference_shops/latest
    --juggler-host edlp.watson.testing
    --juggler-src danilptashnik.edlp
    --workflow 21b8f873-f9f3-4cbe-a78f-0c8564575309
По умолчанию основной кластер - arnold, а вторичный - hahn. Можно указать и другие (при наличии на них нужных таблиц) при помощи:

    --cluster cluster
    --backup-cluster backup_cluster

Информация о проекте:
https://wiki.yandex-team.ru/users/inenakhov/projects/dynamic-pricing/
https://wiki.yandex-team.ru/users/danilptashnik/dynpricingparsingdeploy/
