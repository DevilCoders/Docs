
# Комфортная разработка в PyCharm

## Запуск тестов через Pycharm

1. Запустить
```
make rebuild-testrunner
```
также это надо запускать каждый раз при изменении зависимостей или правок в модуле wiki -- правки тестов подгрузятся так.

2. Указать файлик `./devtools/python.sh` как [system interpreter](https://jing.yandex-team.ru/files/i-dyachkov/Screen%20Shot%202019-09-12%20at%208.22.06%20PM.png)

3. Указать корень [аркадии в Working Dir](https://jing.yandex-team.ru/files/smosker/2020-04-09_12-23-36.png)

4. Сделать `Pytest` [Default Tests Runner](https://jing.yandex-team.ru/files/i-dyachkov/Screen%20Shot%202019-09-12%20at%208.25.58%20PM.png)

5. В корне запустить "окружение" -- postgres и mongo через
```
docker-compose up
```

6. Попробовать запустить [любой тест через Pycharm](https://jing.yandex-team.ru/files/smosker/2020-04-09_12-34-56.png)
должен пройти

7. Пользоваться. Если появились новые миграции - закоментить строчку выше и запустить тест
любой чтобы накатились миграции.
