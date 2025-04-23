CLI утилита для создания тайлсета из geojson/compiled датасетов или из таблиц в YT.  
Пример запуска:
```
export YT_PROXY=hahn
export YT_TOKEN=`cat ~/.yt/token`
export AWS_ACCESS_KEY_ID=`cat ~/.aws/aws_id`
export AWS_SECRET_ACCESS_KEY=`cat ~/.aws/aws_key`

./tilemill-cli mill --num-threads 32 --recipe-path recipe.yaml
```
Описание формата рецепта см. в [libs/mill/README.md](../libs/mill/README.md).
