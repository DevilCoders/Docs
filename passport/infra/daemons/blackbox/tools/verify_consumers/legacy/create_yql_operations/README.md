Пример:
```
 ya make && ./create_yql_operations \
  --grants_file ~/work/tmp/PASSP-33701/grants.json \
  --oauth_token $(cat ~/work/tmp/PASSP-33701/yql.token) \
  --out_operations ~/work/tmp/PASSP-33701/out_operations \
  --date_from 20210701 \
  --date_to 20210815
```

Для перезапуска:
```
 ya make && ./create_yql_operations \
  --grants_file ~/work/tmp/PASSP-33701/grants.json \
  --oauth_token $(cat ~/work/tmp/PASSP-33701/yql.token) \
  --out_operations ~/work/tmp/PASSP-33701/out_operations \
  --date_from 20210701 \
  --date_to 20210815 \
  --rerun
```
