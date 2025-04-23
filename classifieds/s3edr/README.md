# s3edr
*(rus. Сидр)*

**S3 External Data Registry**

Simple framework for storing and retrieving external data with a little help of S3 storage engine.

### s3edr-replicant
сервис, который возит Дататайпы(ДТ) из ЕДС в S3
- **сборка** в [team  city](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_S3edr_S3edrReplicantDeploy?branch=&buildTypeTab=overview&mode=builds), для сборки на ветке необходимо указывать `Transient release = true` 
- **рантайм** в номаде для [прода](https://nomad.vertis.yandex.net/nomad/global/jobs/s3edr-replicant/info) и [тестинга](https://nomad.test.vertis.yandex.net/nomad/global/jobs/s3edr-replicant/info)
- чтобы репликатор возил ДТ, сервис должен **добавить в датасорсы** путь до ЕДС и путь в S3, например [так](https://github.com/YandexClassifieds/vertis-ansible/pull/1339/)
- **деплоится** из дженкинса в [прод](https://j.vertis.yandex-team.ru/job/Deploys/job/S3EDR/job/production/job/s3edr-replicant/) и [тестинг](https://j.vertis.yandex-team.ru/job/Deploys/job/S3EDR/job/testing/job/s3edr-replicant/)
- **логи** смотрим [тут](https://admin.vertis.yandex-team.ru/logs?service=s3edr-replicant) 

по всем вопросам работы обращаться к команде https://github.com/YandexClassifieds/auto#our-team
  
### s3edr-client
подключаемая либа для подбора ДТ из S3

- метрики доставки ДТ смотрим [тут](https://grafana.vertis.yandex-team.ru/d/QHtEe_ymk/autoru-s3edr?orgId=1&refresh=5s&var-source=Prometheus&var-dc=All&var-job=auto2-shard&var-instance=All&var-datatype=All)

### Упрощённый вариант интеграции

Если нужно использовать в сервисе только последнюю версию дататайпа, то не обязательно подключать библиотеку s3edr-client. s3edr для каждого ДТ поддерживает файл latest.data, в котором всегда хранится последняя версия ДТ. Такие файлы имеют путь вида `autoru-extdata/REGIONS/6/latest.data`, и их можно выгрузить любым клиентом s3. Если требуется актуализировать ДТ во время работы приложения, можно смотреть на epoch обновления файла.

### Библиотека для scala 2.11.x
Форк библиотеки находится в отдельной [ветке](https://github.com/YandexClassifieds/s3edr/tree/master_scala_2.11_fork).