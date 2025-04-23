# cloud-mdb-mysql-api - Библиотека для взаимодействия с cloud mdb mysql api

### Что делает
Реализует два метода [cloud mdb mySQL api](https://docs.yandex-team.ru/cloud/managed-mysql/api-ref/grpc/) по протоколу gRPC:
1. Получение списка кластеров облака (Только имена, идентификаторы, тип окружение, здоровье и статусы)
2. Получение исходных записей логов заданного типа для указанного кластера

Для работы библиотеки нужен поставщик cloud iam-token'ов (например из libs/cloud-iam).
Вызывать методы api можно через инстанс класса GrpcCloudMdbMySqlApiImpl.
