# direct-db-models
## Генерация моделей jooq по базам директа

```bash
mvn clean install -Pts
```
доступные профили:
* dev7
* devtest
* ts

## Изменение версии

```bash
# выполнит команду mvn versions:set -DnewVersion=1.0-ts-SNAPSHOT versions:commit
bash v ts
# выполнит команду mvn versions:set -DnewVersion=1.0-SNAPSHOT versions:commit
bash v
```


