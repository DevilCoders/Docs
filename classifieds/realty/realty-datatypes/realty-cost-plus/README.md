# Cost+ 

### Сделать локальный конфиг

```bash
./gradlew :realty-cost-plus:makeLocalConfig
```

### Обновить дашборд

```bash
./scripts/grafana/export.sh realty-datatypes/realty-cost-plus/dashboards.py 
```

#### Работа с ветками
[Общая информация](../realty-datatypes-shiva-core/README.md)

Cost+ из ветки будет доступен в s3 по пути ```export/landings_{BRANCH_NAME}/```
