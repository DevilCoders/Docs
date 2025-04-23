Описание
====
Утилита для сбора данных по денежным потерям из-за неиспользуемых карт GPU

 - Данные складываются в [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/gpu_idle/not_used_res)
и выводятся на [дашборд](https://datalens.yandex-team.ru/lcrmgc4ctcsse-gpu-unused?tab=xn)
 - Тарифы по GPU берутся [здесь](https://yt.yandex-team.ru/hahn/navigation?path=//home/cloud-dwh/data/prod_internal/ods/billing) и обновляются еженедельно


--------
Запуск
====
Автоматический
--
Утилита автоматически запускается каждый час в [Nirvane](https://nirvana.yandex-team.ru/flow/46bc966c-182c-4212-a79c-35e8f16af606/829bfeed-b56d-4717-95e3-225203eb1e61/graph).

Локально
----
Для запуска утилиты необходимо из папки arcadia/infra/capacity_planning/utils/hardware_utilization/dont_used_res/  вызвать:
```
ya make
./dont_used_res
```
