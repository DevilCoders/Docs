## Delivery Tracker
Трекер нужен для отслеживания статусов заказов Маркета в службах доставки, сортировочных центрах и фулфилментах.
 
[Полная документация на Вики](https://wiki.yandex-team.ru/market/development/delivery-tracker/)
### Настройки IDEA
 - Установить Lombok плагин
 - Добавить флаг "`-parameters`" в настройки компилятора (`Preferences -> Build, Execution, Deployment -> Compiler -> Java Compiler -> Additional command line parameters`).
   Нужно для Jackson'a, чтобы не писать кучу аннотаций, подробнее можно почитать [тут](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html)

### Как запустить локально
1. Устанавливаем [docker](https://www.docker.com/). Возможно, придется авторизоваться в яндексовом [registry](https://wiki.yandex-team.ru/qloud/docker-registry/)
2. Приложение живет в модуле `delivery-tracker-app`, переходим туда 
`cd delivery-tracker-app`.
3. Копируем конфиг логов из шаблона
`cp src/main/conf/local/logback.xml.dist src/main/conf/local/logback.xml`.
4. Копируем проперти приложения из шаблона
`cp src/main/properties.d/local/application-local.properties.dist src/main/properties.d/local/application-local.properties`.  
5. Поднимаем контейнер PostgreSQL, например, командой `cd 'dependency-stubs' && docker-compose up -d`. 
Настройки образа (порт, юзер, пароль) лежат в файлике `dependency-stubs/docker-compose.yaml`.
Liquibase автоматически накатит миграции из `src/main/resources/sql`.
6. Запускаем `ru.yandex.market.delivery.tracker.DeliveryTrackerApp`, предварительно заполняем Environment variables
    ```
    LOG_DIR=logs
    ENVIRONMENT=local
    PROPERTIES_DIR=<абсолютный путь до директории src/main/properties.d>
    ```
7. Приложение доступно по умолчанию на порту 35700

### Запуск с поддержкой TVM
[Про TVM](https://wiki.yandex-team.ru/passport/tvm2/)

Для простоты запуска на локальной машине поддержка TVM выключена, если нужно включить то:
 
1. VM options: `-Dspring.profiles.active=local,tvm -Dlogback.configurationFile=logback.xml -Denvironment=local -Dlog.dir=logs -Djava.library.path=/usr/local/lib/`
1. в `application-local.properties`, положить в `tracker.tvm.secret` tvm секрет из секретницы 

### Деплой
Конфиг деплоя лежит в файле `delivery-tracker-app/package.json`

Каждый коммит в транк это новый релиз (CI/CD).

Релизная машина в [ЦУМе](https://tsum.yandex-team.ru/pipe/projects/logistics/delivery-dashboard/deliveryTracker_release).

### Миграции БД
Любые изменения схемы или данных должны быть сделаны через миграции. Файлы миграции находятся в папочке `resources/sql/migrations`. 
При создании новой миграции необходимо в `--changeset`е указать свой логин и через двоеточие номер задачи и краткое описание. 
При релизе приложения новые миграции накатываются автоматически. Какие новые определяется по табличке `databasechangelog`.
