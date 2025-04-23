Installing a local VEnv (optional):

`./install_venv.sh`

Use in the following order:

1. Create a workdir: `./prepare_wc.py`
2. Edit loadtestYYYYMMDD.yaml file, set your groups and services (you can use nanny service name instead of blinov calc)
3. Get a plan: `./prepare_plan.sh loadtestYYYYMMDD`
4. `./upload_wc.sh loadtestYYYYMMDD`
5. `./init_remote_wc.sh loadtestYYYYMMDD` (to revert this, use `state=0 ./init_remote_wc.sh`)
6. Start `./run_loadtest.sh loadtestYYYYMMDD`. It will be interactive :)

Cleaning up: to remove the deployed stuff, run:
1. state=0 ./init_remote_wc.sh loadtestYYYYMMDD
2. state=0 ./upload_wc.sh loadtestYYYYMMDD

Must read:
* https://st.yandex-team.ru/REFRESH-237 https://st.yandex-team.ru/REFRESH-153
* https://wiki.yandex-team.ru/users/yrum/refresh-kb/
* https://wiki.yandex-team.ru/jandekspoisk/sepe/dolbilka/
