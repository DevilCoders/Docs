# Образ контейнера с базой оракла и схемой BO
Для сборки с нуля потребуется пройти все круги ада. 
Начинаются они вот тут: [oracle-12c](https://github.com/wscherphof/oracle-12c). Ну а дальше как получится. 

# Работа с уже собранным образом
Готовый образ можно забрать к себе коммандой: `docker pull registry.ape.yandex.net/balance/oracle-bo`. 
Запускаем: `docker run --privileged -d -p 1521:1521 --name orcl registry.ape.yandex.net/balance/oracle-bo`

В базе есть следующие пользователи: `bo/balalancing, sys/change_on_install, system/manager`. Поднят сервис `orcl`. 
Проверить что всё запустилось: `sqlplus sys/change_on_install@localhost:1521/orcl as SYSDBA`

# Сборка образа из имеющегося образа
* Берём образ описанным выше способом и запускаем
* Вносим изменения которые нам необходимы
* Выполняем код
```bash
#на выходе получаем образ oracle-bo:tar с нужным содержимым
docker stop orcl && docker export orcl | docker import - oracle-bo:tar
#собираем образ
docker build -t oracle-bo .
docker tag -f oracle-bo registry.ape.yandex.net/balance/oracle-bo
docker push registry.ape.yandex.net/balance/oracle-bo
```

Почему так сложно? Ответ прост. В контейнере у нас лежат файлы с данными оракла и если использовать docker commit, то образ распухает и болит. 

# Возможные проблемы
Может закончиться место в экстенте. Его следует добавить

```ALTER TABLESPACE <ИМЯ СПЕЙСА> ADD DATAFILE SIZE 32M```
