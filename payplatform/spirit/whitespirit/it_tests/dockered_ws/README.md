### WS в докере
Собрать образ можно вот так (из этой папки):
```shell script
docker build ../.. -f Dockerfile
```
Запустить:
```shell script
docker run ${image_tag} python3 run.py
```
Ну или сразу и сборка и запуск:
```shell script
docker run $(docker build ../.. -f Dockerfile -q) python3 run.py
```
-------------
От образа в корне проекта принципиально отличается наличием файла с конфигом и вспомогательного скриптика run.py (за основу взят kkt_srv_run.py), который запускает приложение с environment=tests. 
