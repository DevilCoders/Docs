# Searcherline
Dev разворачивается на железе, testing и prod живут в докере.

## Начало работы
Создайте файл `upload.properties` в корне проекта с содержимым
```
ssh.host=<your dev host>
```

## Разработка
Для развертывания сервиса на dev машину запустите скрипт `./deploy.sh`.

Запуск:
```
ssh <your dev host>
cd ~/dist/autoru-searchline
sudo ./restart
```

## Выкладка
1. Собираем новый докер образ в [teamcity](https://t.vertis.yandex-team.ru/project.html?projectId=VerticalsBackend_Searchline).
2. Выкладываем его через Jenkins. Указываем версию и добавляем сообщение.   
[jenkins testing](https://j.vertis.yandex-team.ru/job/Deploys/job/Autoru/job/testing/job/yandex-autoru-searchline/)  

## Логи
Локально логи пишутся в `~/dist/autoru-searchline/log/autoru-searchline.log`. В этом их отличие от остальных сервисов auto, например серчера.   
Логи с тестинга или прода можно посмотреть в [Админке](https://admin.vertis.yandex-team.ru/logs?service=yandex-autoru-searchline).

## Мониторинги
https://grafana.vertis.yandex-team.ru/d/MBlyqxqiz/autoru-searchline?refresh=1m&orgId=1

## Swagger
Port 34580  
[Swagger in testing](http://autoru-searchline-int.vrts-slb.test.vertis.yandex.net)

## Тестирование
```
mvn test
```

Также можно сравнить различные версии searchline используя `checker.py`:
```
cd autoru-searchline

# launch searchline v0
./checker.py

# launch searchline v1
./checker.py

# show difference:
./checker.py responses_0.txt responses_1.txt
```

Чтобы подготовить searchline конкретной версии его нужно:  
1. задеплоить
2. запустить
3. пробросить порт (или исправьте в `checker.py` хост)
```
ssh -L34580:localhost:34580 YOUR_HOST_NAME
```

Если `python` на ноуте не настроен, то команды можно запускать как
```
python3 ./checker.py
```

Возможно придётся установить необходимые пакеты 
```
sudo pip3 install requests
```

## Antlr source recompile (after QueryParser.g changes for example)
```sh
cd autoru-searchline
./antlr-gen.sh
```

## Dataset
[code](https://github.yandex-team.ru/pnaydenov/my_utils/tree/master/python/searchline) 
[files](https://github.yandex-team.ru/pnaydenov/searchline_datasets)

## Benchmarking
You can benchmark application using [lunapark](https://lunapark.yandex-team.ru) and `autoru-searchline/ammo.txt`

## Periodical tasks (crontab)
```
40 14  * * 1 python3 scripts/publish_last_queries_from_yt.py --st_token `cat /etc/yandex/vertis-datasources/datasources.properties | grep "vertis-hubot.startrek.token" | cut -d ' ' -f 3` 

20 14  * * * python3 scripts/publish_last_queries_from_yt.py --days=1 --action=queries_log --st_token empty

30 14 * * 1 ./scripts/generate_verba_terms.sh
```