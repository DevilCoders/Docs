# Nirvana

**[Операции на нирване](https://nirvana.yandex-team.ru/browse?selected=8479120):**

## Конфиги операций

- [upload_to_ml_storage_op.json](operations/upload_to_ml_storage_op.json) – загружает архив в ML Storage через клиент
- [preprocessor_ml_storage_op](operations/preprocessor_ml_storage_op.json) – предобработка архивов дампов ml_engine и генерация меты
- [model_processor_op](operations/model_processor_op.json) – скачивание драфта, валидация и отправка в ML Storage

## Как обновить операцию через UI

1. Найти [нужныю операцию в UI](https://nirvana.yandex-team.ru/browse?selected=8479120)
2. Открыть кубик внутри графа, склонировать, сделать изменения
  ![](https://jing.yandex-team.ru/files/dim-gonch/2021-06-11_13-23-43.png)
3. Провалидировать `Validate` и апрувнуть `Approve`, поставить optional deprecation
  ![](https://jing.yandex-team.ru/files/dim-gonch/2021-06-11_13-24-11.png)
  ![](https://jing.yandex-team.ru/files/dim-gonch/2021-06-11_13-25-55.png)
4. Экспортировать дамп и сохранить в аркадии в [`ads/emily/storage/libs/nirvana/operations`](https://a.yandex-team.ru/arc/trunk/arcadia/ads/emily/storage/libs/nirvana/operations)
  ![](https://jing.yandex-team.ru/files/dim-gonch/2021-06-11_13-33-34.png)
5. Склонировать и обновить все операции в которых используется этот кубик. Поставить optional deprecation.
6. Скопировать `operaion guid`
  ![](https://jing.yandex-team.ru/files/dim-gonch/2021-06-11_13-30-13.png)
7. Открыть [`ads/nirvana/blocks/ml_storage`](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/blocks/ml_storage.py#L20) и поменять `guid` и версию операции
8. [Протестировать](https://a.yandex-team.ru/arc/trunk/arcadia/ads/emily/storage/models/client/readme.md#protestirovat)
9. Сделать PR
10. [Катнуть релиз ML_ENGINE](https://a.yandex-team.ru/arc/trunk/arcadia/ads/emily/storage/models/client/readme.md#ml-engine-regular-task) (через дежурного)

## Как обновить операцию из кода

### Добавить новую операцию

1. Экспортировать дамп из созданной операции и положить в [`ads/emily/storage/libs/nirvana/operations`](https://a.yandex-team.ru/arc/trunk/arcadia/ads/emily/storage/libs/nirvana/operations)
2. Добавить **arc токен** [в секреты](https://nirvana.yandex-team.ru/secrets)
3. Открыть [страницу операций](https://nirvana.yandex-team.ru/operations) и импортировать из кода
  ![](https://jing.yandex-team.ru/files/dim-gonch/2021-07-09_17-52-33.png)
  ![](https://jing.yandex-team.ru/files/dim-gonch/2021-07-09_17-56-06.png)

### Обновить операцию

_для существующих_

1. Сделать изменение в конфиге операции, закоммитить
2. Открыть текущую операцию в GUI, нажать `Upgrade from VCS` и выбрать ревизию коммита
  ![](https://jing.yandex-team.ru/files/dim-gonch/2021-07-09_17-58-21.png)
