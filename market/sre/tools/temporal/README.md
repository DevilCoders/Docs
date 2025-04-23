1. start server
```
cd cmd/server
SERVICES=frontend:matching:history:worker ./server --config conf/temporal --acl-config conf/temporal/acl.yaml start
```

2. start worker
```
cd cmd/worker
./worker -namespace user-discord -taskqueue nanny -nanny-token /home/dspushkin/.nanny.token
```

commands:
1. запустить workflow в cron режиме
```
./tctl --address localhost:7233 --namespace user-discord workflow start -tq nanny -wt nanny-list-workflow  --cron "* * * * *"
```

2. список workflow
```
./tctl --address localhost:7233 --namespace user-discord workflow listall
     WORKFLOW TYPE    |             WORKFLOW ID              |                RUN ID                | TASK QUEUE | START TIME | EXECUTION TIME | END TIME  
  nanny-list-workflow | d957d43e-6b70-44d0-a729-42c4f2ff6faa | 57819274-9585-41b4-bc1d-e6dda6141111 |            | 22:42:27   | 22:42:27       | 22:42:28 
```

3. запустить workflow разово
```
./tctl --address localhost:7233 --namespace user-discord workflow start -tq nanny -wt nanny-list-workflow --wtt 3
```

4. посмотреть статус задачи
```
./tctl --address localhost:7233 --namespace user-discord workflow showid d957d43e-6b70-44d0-a729-42c4f2ff6faa 57819274-9585-41b4-bc1d-e6dda6141111
```
