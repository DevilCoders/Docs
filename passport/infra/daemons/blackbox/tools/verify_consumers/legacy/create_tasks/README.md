Пример. Сначала надо подготовить тексты:
```
 ya make && ./create_tasks \
  --grants_file ~/work/tmp/PASSP-33701/grants.json \
  --yql_file ~/work/tmp/PASSP-33701/out_operations \
  --oauth_token $(cat ~/work/tmp/PASSP-33701/robot.token) \
  --prepared_tasks ~/work/tmp/PASSP-33701/prepared_tasks \
  --already_created ~/work/tmp/PASSP-33701/already_created \
  --tags blackbox,2021,notvm \
  --deadline '2021-10-01T18:00:00.00+0000'
```

Потом создать их на самом деле
```
 ya make && ./create_tasks \
  --grants_file ~/work/tmp/PASSP-33701/grants.json \
  --yql_file ~/work/tmp/PASSP-33701/out_operations \
  --oauth_token $(cat ~/work/tmp/PASSP-33701/robot.token) \
  --prepared_tasks ~/work/tmp/PASSP-33701/prepared_tasks \
  --already_created ~/work/tmp/PASSP-33701/already_created \
  --tags blackbox,2021,notvm \
  --deadline '2021-10-01T18:00:00.00+0000' \
  --limit 10 \
  --wet_run
```
