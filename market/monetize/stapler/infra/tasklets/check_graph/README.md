# Stapler Check Graph Tasklet

Должен взять ссылку на результат работы тасклета [Stapler Deploy Tasklet](../deploy_tasklet)
и чекать выполнение графа


## config

    input:
        ctx:
        deploy_result:
            link:
            workflow:
        config:
            sleep_timeout: # default 5 min
            check_timeout: # default 10 hours
            nirvana_token:
                uid:
                key:
