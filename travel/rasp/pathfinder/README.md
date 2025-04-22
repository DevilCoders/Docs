pathfinder
==========

Сервис поиска маршрутов с пересадками


Как запустить пересадочник на dev стенде
----------------------------------------

Создаем директорию data в корне проекта, кладем в нее данные с продакшина
(на машинах в qloud они лежат в `targetpathfinder/data/pathfinder_data/`) выбираем либо main0_rasp либо main1_rasp.
Кладем их в data, переименовывая в default. Далее делаем так:

```bash
cd webpathfinder/targetpathfinder
./remake.sh
cd -
./restart.sh
```

Пример сборки и запуска через docker
------------------------------------
```
docker build -t pathfinder /Users/monitorius/work/rasp/pathfinder
rsync -avzPL admin01h.cloud.rasp.yandex.net:/var/lib/yandex-rasp/rasp/www/db/scripts/data/pathfinder/* ~/work/rasp/data/pathfinder/data
docker run -p 8801:80 -e YENV_TYPE=testing -e ENABLE_PRICES=0 -e QLOUD_HTTP_PORT=80 -e HTTP_PORT=8101 -e QLOUD_APPLICATION=pathfinder -e DATA_PATH=/targetpathfinder/data/pathfinder_data -e CURRENT_DB=main0_rasp -e LOGS_PATH=/targetpathfinder/logs/targetpathfinder.log -e PID_PATH=/targetpathfinder/targetpathfinder.pid -e PROCESS_NUMBER=1 --name=pathfinder --rm -it -v /Users/monitorius/work/rasp/data/yav:/etc/yav-secrets -v /Users/monitorius/work/rasp/data/pathfinder/data:/targetpathfinder/data/pathfinder_data  pathfinder
```


Интеграционные тесты
--------------------

Выполняются при помощи команды `./tests/test_pathfinder.sh`
