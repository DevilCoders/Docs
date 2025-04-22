## Tarifficator

Хранение тарифов и сбор всей информации, необходимой для расчета стоимости доставки калькулятором.

### Настройка окружения

В проекте используется *Lombok*, поэтому для разработки необходимо установить *Lombok Plugin* для IDE
и включить в настройках компилятора *Annotation processing*.


### Локальный запуск через IDEA

1. Копируем стабовые проперти приложения.
    ```
    cd src/main/properties.d/local
    cp application-local.properties.dist application-local.properties
    ```

1. Поднимаем докер контейнер с базой данных.
    ```
    cd dependency-stubs
    docker-compose up -dV
    ```

1. Накатываем liquibase миграции.
    
    - Запускаем миграцию через скрипт `./liquibase.sh update`.

1. Создаем конфигурацию запуска Spring Boot.

    - *Main class*:         `ru.yandex.market.logistics.tarifficator.Tarifficator`. 
    - *Env vars*:           `PROPERTIES_DIR=<path_to_properties.d>`
    - *Active profiles*:    `local`

1. Запускаем конфигурацию.
