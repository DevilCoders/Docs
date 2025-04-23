Создание ККТ
 - `/opt/venvs/balance-kkt-vfr/scripts/fr_ctl.sh create 10.0.0.2 00000003820034331903 9999078902000066 666666`

Запуск
 - `initctl start balance-vfrs`
 - `initctl start balance-vfr KKT_SN=<SN>`

Иное
 - `/opt/venvs/balance-kkt-vfr/scripts/fr_ctl.sh --list`
 - `/opt/venvs/balance-kkt-vfr/scripts/fr_ctl.sh list`
 - `/opt/venvs/balance-kkt-vfr/scripts/fr_ctl.sh remove <SN>`
 - `/opt/venvs/balance-kkt-vfr/scripts/fr_ctl.sh run <SN>`

Описание сборки в `docs`