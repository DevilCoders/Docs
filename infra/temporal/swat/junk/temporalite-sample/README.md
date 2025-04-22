```
ya make ./vendor/go.temporal.io/server/cmd/tools/cli/
ya make ./vendor/github.com/DataDog/temporalite/cmd/temporalite
ya make ./infra/temporal/swat/junk/temporalite-sample/worker/

./vendor/github.com/DataDog/temporalite/cmd/temporalite/temporalite start -n default --filename ./sqlite.db
./vendor/go.temporal.io/server/cmd/tools/cli/cli --ad localhost:7233 wf run --tq default --wt Workflow
./infra/temporal/swat/junk/temporalite-sample/worker/worker
```

http://localhost:8233
