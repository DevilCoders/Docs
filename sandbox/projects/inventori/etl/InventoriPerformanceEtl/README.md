# InventoriPerformanceEtl

It's sandbox task that run built `inventori/pylibs/tasks/etl/performance_etl_collector.py` task (which prepared data and collect on the corresponding YT folder)
make `.tar` file of this folder and send him to deploy

> How to build this sandbox task?

## Steps how to run

1. Create product task InventoriPerformanceEtlBinary (using BuildInventoriTask on Sandbox)
2. Build this task using cli or Sanbox – build_binary_task. CLI command(run from ./bin):
```bash
cd ~/arcadia/sandbox/projects/inventori/etl/InventoriPerformanceEtl/bin

ya make && ./inventori-performance-etl run --type INVENTORI_PERFORMANCE_ETL  --enable-taskbox  --create-only --owner INVENTORI
```
3. In setting set up resource id which u get on the first step

Scheduler example:

https://sandbox.yandex-team.ru/scheduler/698826/view

St. ticket:

https://st.yandex-team.ru/INVENTORI-4243
