## Description
Solves tasks of various sizes and saves execution times to `solve_time` table in `b2bgeo_metrics` database.
Results are used in datalens: https://datalens.yandex-team.ru/ctefq1r5k5fq5-solver-metrics
Sandbox scheduler: https://sandbox.yandex-team.ru/scheduler/698246/view


## Usage
`./solve_time [-h] [--sizes SIZES [SIZES ...]]`
Requires `DB_PASSWORD` ([secret](https://yav.yandex-team.ru/secret/sec-01fjhf4xw5g5rq4vnhn1hn3pdx/explore/versions)) and `APIKEY` environment variables.
`--sizes` specifies task sizes in thousands. All available sizes (see SIZES in main.py) are used by default.
