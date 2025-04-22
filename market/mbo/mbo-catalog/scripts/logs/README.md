Скрипты для чтения логов с дев машинок
--
Открыть mbo-tms.log в режиме `tail -f`
```bash
./scripts/logs/log-mbo-tms.sh
./scripts/logs/log-mbo-tms.sh --tail
./scripts/logs/log-mbo-tms.sh -t
```

Открыть mbo-gwt.log в режиме less
```bash
./scripts/logs/log-mbo-gwt.sh --less
./scripts/logs/log-mbo-gwt.sh -l
```

Открыть mbo-lite.log на callisto машинке
```bash
./scripts/logs/log-mbo-lite.sh --host callisto
./scripts/logs/log-mbo-lite.sh -h callisto
```

Открыть mbo-card-api.log.shell
```bash
./scripts/logs/log-mbo-lite.sh --file logs/mbo-card-api/mbo-card-api.log.shell
./scripts/logs/log-mbo-lite.sh -f logs/mbo-card-api/mbo-card-api.log.shell
```

Открыть mbo-tool.sh в режиме less на прод машине
```bash
./scripts/logs/log-mbo-tool.sh --host mbo01e.market.yandex.net --less
```

