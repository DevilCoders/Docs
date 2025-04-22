#Квоты, использующиеся в автосборочных сендбокс задачах

1. квоты logbroker:
    - используем аккаунт [/autocheck_sandbox_tasks](https://logbroker.yandex-team.ru/logbroker/accounts/autocheck_sandbox_tasks?page=browser&type=account&metricsFrom=1597648966791&metricsTo=1597735366792) в инстансе logbroker с дефолтной квотой
    - для прокачки stages.json завели топик /autocheck_sandbox_tasks/stages
2. квота logfeller:
    - для хранения логов используем yt квоту аккаунта autocheck_sandbox_tasks на hahn. Конфиги можно найти в common_hahn_logs.json в записи autocheck_sandbox_tasks-stages-log и common_hahn_streams.json в записи autocheck_sandbox_tasks/stages
    - сохраняем [1d и 30min таблицы](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/autocheck_sandbox_tasks-stages-log&) в нашей квоте autocheck_sandbox_tasks на yt с временем жизни соответсвено 3650 дней и 2 дня
    - [дашборд](https://solomon.yandex-team.ru/?project=logfeller&cluster=hahn&service=indexing&dashboard=logfeller-log-life-index&autorefresh=y&l.stream-name=autocheck_sandbox_tasks-stages)
3. квота yt:
    - завели [квоту в yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/autocheck_sandbox_tasks&) для логов. Текущая квота 5 TiB.
