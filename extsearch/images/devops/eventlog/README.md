## Построение плана запросов к среднему из eventlog
    $ evlogdump mmeta-eventlog | python mmeta_stpd_queries_from_eventlog.py > mmeta.requests
    $ d-planner -l mmeta.requests -o mmeta.requests.plan -t phantom
