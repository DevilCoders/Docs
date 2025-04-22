Описание
====
Утилита для выгрузки данных по утилизации GPU ABC сервисами

Данные складываются в [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/hardware_utilization/gpu_runtime)
и выводятся на [дашборд](https://datalens.yandex-team.ru/5tclf89zbaecy-gpu-runtime)


--------
Запуск
====
Автоматический
--
Утилита автоматически запускается каждый день в 01:00 в [Nirvane](https://nirvana.yandex-team.ru/flow/d634b2b0-0ac4-4cfd-91de-d1d47c94fec3/f4f16117-86b5-4b12-b98b-3ef6dec582f6/graph), собирая данные за предыдущее сутки.

Локально
----
Для запуска утилиты необходимо положить токен в ~/.abc/token и из папки arcadia/infra/capacity_planning/utils/hardware_utilization/gpu_runtime/  вызвать:
```
ya make
./gpu_runtime
```
Либо можно передать токен при запуске в качестве параметра --abc-token 
```
ya make
./gpu_runtime --abc-token ABC-token
```
Токен можно получить по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=23db397a10ae4fbcb1a7ab5896dc00f6)

