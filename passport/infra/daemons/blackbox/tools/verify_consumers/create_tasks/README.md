Пример. Сначала надо подготовить тексты:
```
 ya make && ./create_tasks \
  --grants_file ~/work/tmp/PASSP-33360/out_grants \
  --abc_file ~/work/tmp/PASSP-33360/out_abc \
  --yql_file ~/work/tmp/PASSP-33360/out_operations \
  --oauth_token $(cat ~/work/tmp/PASSP-33360/robot.token) \
  --prepared_tasks ~/work/tmp/PASSP-33360/prepared_tasks \
  --already_created ~/work/tmp/PASSP-33360/already_created \
  --tags blackbox,2021 \
  --deadline '2021-07-31T18:00:00.00+0000'
```

Потом создать их на самом деле
```
 ya make && ./create_tasks \
  --grants_file ~/work/tmp/PASSP-33360/out_grants \
  --abc_file ~/work/tmp/PASSP-33360/out_abc \
  --yql_file ~/work/tmp/PASSP-33360/out_operations \
  --oauth_token $(cat ~/work/tmp/PASSP-33360/robot.token) \
  --prepared_tasks ~/work/tmp/PASSP-33360/prepared_tasks \
  --already_created ~/work/tmp/PASSP-33360/already_created \
  --tags blackbox,2021 \
  --deadline '2021-07-31T18:00:00.00+0000' \
  --limit 10 \
  --wet_run
```
