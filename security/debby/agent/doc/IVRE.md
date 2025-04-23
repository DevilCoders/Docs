[Official ivre repository](https://github.com/cea-sec/ivre)

# ivre scan examples
1. `ivre runscans --category id_0001 -r 5.255.255.5 5.255.255.5`
2. results saves to `<working_dir>/scans/id_0001`
3. save results to db `ivre scan2db -s id_0001 -r <working_dir>/scans/id_0001/up/`

# ivre export scan info and import scan info
1. Export `ivre scancli --source <task_uuid> --json > /tmp/<task_uuid>`
2. Import `ivre scan2db -s <task_uuid> /tmp/<task_uuid>`
3. I may not import repeatedly even if source changed
