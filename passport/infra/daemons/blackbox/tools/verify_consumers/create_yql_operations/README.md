Пример:
```
 ya make && ./create_yql_operations \
  --grants_file ~/work/tmp/PASSP-33360/out_grants \
  --oauth_token $(cat ~/work/tmp/PASSP-33360/yql.token) \
  --out_operations ~/work/tmp/PASSP-33360/out_operations \
  --date_from 20210601 \
  --date_to 20210701
```

Для перезапуска:
```
 ya make && ./create_yql_operations \
  --grants_file ~/work/tmp/PASSP-33360/out_grants \
  --oauth_token $(cat ~/work/tmp/PASSP-33360/yql.token) \
  --out_operations ~/work/tmp/PASSP-33360/out_operations \
  --date_from 20210601 \
  --date_to 20210701 \
  --rerun
```
