## notes

Нужно создавать контейнер в иерархии звездолёта:
    ISS-AGENT--32451_sas_jupiter_base_geX4Yg2NLFR/iss_hook_start/supercontainer
Для задачи обстрела шарда нужна аналогичная конструкция

basesearch: разный cpu, mem, выключить turboboost
    thread affinity: улучшить показатели базового не удалось
    турбобуст вместо небезопасного выключения можно считывать и нормировать
    также можно считывать портовский счётчик выделенных наносекунд
d-executor: гарантированные ресурсы, чтобы он не тормозил


формат запуска:
/place/sandbox-data/tasks/0/9/148933490/pack/d-executor
    --plan-file /place/sandbox-data/tasks/3/1/183878513/basesearch_search.plan
    --output /place/sandbox-data/tasks/8/3/184154738/test_basesearch_session_2.dump
    --queries-limit 100000
    --mode finger
    --timeout 600
    --simultaneous 28
    --replace-host localhost
    --replace-port 17171
    --circular
