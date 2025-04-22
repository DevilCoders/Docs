## Сервис доставки наружу [Nesu]

### Локальный запуск через IDEA

1. Копируем стабовые проперти приложения.
    ```
    cd src/main/properties.d/local
    cp application-local.properties.dist application-local.properties
    ```

1. Поднимаем докер контейнер с базой данных.
    ```
    cd dependency-stubs
    docker-compose up -d
    ```

1. Прописываем Environments:
    ```
   PROPERTIES_DIR=/<absolute_path_to_project>/nesu/nesu-app/src/main/properties.d;
   ENVIRONMENT=local;
   ```

1. Запускаем метод `main` в классе `ru.yandex.market.logistics.nesu.Nesu`.

### Что делать, если не работает TVM

1.  Также необходимо указать рабочий `nesu.tvm.secret` в свойствах `application-local.properties` из секретов тестинга.
