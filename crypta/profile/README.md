Main codebase for Crypta user profile builder

## Docs
https://wiki.yandex-team.ru/Crypta/ProfilesExport


## Testenv autobuild
https://testenv.yandex-team.ru/?screen=jobs&database=crypta

https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/crypta/profile.yaml

## Sandbox runners
https://sandbox.yandex-team.ru/schedulers?pageCapacity=50&tags=crypta_profile

https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/crypta/profile

## Deploy Jupyter with code
Clone and run task:

Testing
https://sandbox.yandex-team.ru/task/898891155/view

Production
https://sandbox.yandex-team.ru/task/898880177/view


## Luigi web control panels:

Testing
https://profile-luigi-test.crypta.yandex.net

Production
https://profile.luigi.crypta.yandex.net

## Jupyter:

Testing
http://crypta-profile.sas.yp-c.yandex.net:8085/

Production
http://crypta-profile.sas.yp-c.yandex.net/


## Plots

https://grafana.yandex-team.ru/dashboard/db/crypta-analytics

## Run separate task for debug ( rerun mode, ignoring existing output )

python manual_start_scripts/luigi_debug_starter.py <full_class_path> --class_param_1 <value_1> --class_param_2 <value_2>

Example:

python manual_start_scripts/luigi_debug_starter.py crypta.profile.runners.training.lib.train_socdem_model.TrainSocdemModels --date 2017-11-10

## Web Index TNS monitoring Statface path:

https://datalens.yandex-team.ru/uj0m556sqfoir-unifiedcryptastats?tab=Y1

## Web Index TNS pairs gender-age report path:

https://stat.yandex-team.ru/Crypta/PairsGAWebIndexTNS?scale=d&table_type=profiles_russia&gender=m&age=18_24&_incl_fields=accuracy&_period_distance=30
