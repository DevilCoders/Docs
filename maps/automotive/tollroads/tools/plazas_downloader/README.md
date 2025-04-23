# Скачиватель слоя РВП для сервиса ЦКАДа

Утилита скачивает актуальный слой РВП (проксируя запрос через [наш сервис](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tollroads)) и сравнивает полученные данные с теми, что лежат в navi_s3 (откуда их берет навигатор).
Обновление данных осуществляется вручную.  
Проверяются только данные в директориях `prod`, директория `test` используется для тестирования данных (обновляется вручную).  

## Данные
| Тип данных | Исходники в GIT | Выкладка в S3 |
| ---- | ---- | --- |
| Тестовые | [dev ветка](https://bb.yandex-team.ru/projects/NAVI/repos/navi_s3/browse?at=refs%2Fheads%2Fdev) | [yandexnavi-testing.s3.yandex.net](https://yandexnavi-testing.s3.yandex.net/toll_road_checkpoints/prod/toll_road_checkpoints.json) |
| Продовые | [master ветка](https://bb.yandex-team.ru/projects/NAVI/repos/navi_s3/browse) | [yandexnavi.s3.yandex.net](https://yandexnavi.s3.yandex.net/toll_road_checkpoints/prod/toll_road_checkpoints.json) |

## Проверка актуальности данных 

 * ENV_TYPE=testing или stable - проверка тестовых или продовых данных  
 * SSH_PRIVATE_KEY - опционально содержит приватный SSH ключ (используется для запуска в SANDBOX)  
 * STORE_SSH_AT_HOME=true - для сохранения кастомного приватного SSH ключа в ~/.ssh/id_rsa.pub (используется для запуска в SANDBOX)  


```
$ export TVM_SECRET=$(ya vault get version ver-01eqdx96qjmt4q6khkyhhcgr18 --only-value client_secret -n)
$ ENV_TYPE=testing ./plazas_downloader
```

Для повторного запуска директорию `./navi_s3` нужно удалить.
