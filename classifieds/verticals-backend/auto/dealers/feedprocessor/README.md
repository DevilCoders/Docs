Feedprocessor
=================
Process feeds loaded by Feedloader and put parsed offers to Kafka topic.
Read and aggregate offer statuses from another Kafka topic.

Design doc: [Wiki](https://wiki.yandex-team.ru/vertis/external-offer-loading-service/)
Testing: [API](feedprocessor-autoru-api-int.vrts-slb.test.vertis.yandex.net)
Grafana:
* [scheduler](https://grafana.vertis.yandex-team.ru/d/ukJlWXBmk/feedprocessor-autoru-scheduler)
* [prod dashboard](https://grafana.vertis.yandex-team.ru/d/_oM7mXfik/feedprocessor-autoru-scheduler-presentation)
* [consumer](https://grafana.vertis.yandex-team.ru/d/ScChJgnik/vos2-autoru-consumers) 

#### Maven config 
Make sure you have [mvn settings](https://github.com/YandexClassifieds/maven-settings/blob/master/settings.xml) copied to your home dir `~/.m2/settings.xml` 

#### Prepare and build
1. Build project:
   ```
   mvn clean install
   ```   

#### Deploy for testing
1. Merge your branch into testing branch
2. Start job from testing branch. It rolls out to the main testing.

    - Run [feedprocessor-autoru-api-release](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_Feedprocessor_FeedprocessorAutoruApiRelease?branch=refs%2Fheads%2Ftesting&buildTypeTab=overview&mode=builds) to roll out API
    - Run [feedprocessor-autoru-scheduler-release](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_Feedprocessor_MakeStableRelease?branch=refs%2Fheads%2Ftesting&buildTypeTab=overview&mode=builds) to roll out (guess what?) scheduler!

2. [check version in jenkins](https://j.vertis.yandex-team.ru/job/Deploys/job/feedprocessor-autoru/job/testing/) from testing branch it will be with a suffix like ":a7ae3d4"

#### Как интеграционно проверить свои изменения

Можно через фронт:
1. Заходим на cabinet.test.avto.ru/feeds
2. Логинимся из-под дилера (например, можно взять тестового: demo@auto.ru, пароль autoru)
3. На вкладке "История загрузок" можно найти примеры xml-фидов для загрузки.
4. На вкладке "Настройка фидов" можно загрузить новый фид.
5. После загрузки можно отследить прогресс загрузки в интерфейсе.
6. Если обработка фида залипла или сфейлилась, смотрим логи feedprocessor-autoru-scheduler и/или vos2-autoru-consumers на `logs-docker.vertis.yandex.net:/var/remote-docker-log/test` или в [админке логов](https://admin.vertis.yandex-team.ru/logs) (в админке только логи vos2-autoru-consumers).

#### Deploy to production
1. Start job from master branch.

    - Run [feedprocessor-autoru-api-release](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_Feedprocessor_FeedprocessorAutoruApiRelease?branch=%3Cdefault%3E&buildTypeTab=overview&mode=builds) to roll out API
    - Run [feedprocessor-autoru-scheduler-release](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_Feedprocessor_MakeStableRelease?branch=%3Cdefault%3E&buildTypeTab=overview&mode=builds) to roll out (guess what?) scheduler!

2. [check version in jenkins](https://j.vertis.yandex-team.ru/job/Deploys/job/feedprocessor-autoru/job/testing/) from testing branch it will be with a suffix like ":0.1.0"
Make sure you rolls out stable version like 0.1.0
 
3. Promote required build version on [Jenkins](https://j.vertis.yandex-team.ru/job/Deploys/job/feedprocessor-autoru/job/testing)

4. Look at the released version in production [Jenkins](https://j.vertis.yandex-team.ru/job/Deploys/job/feedprocessor-autoru/job/production/)

#### Known issues
1. Иногда по какой-то причине между дженкинсом и тимсити происходит рассинхрон, в проде оказывается версия, которой нет в тэгах гита и в итоге сборка падает.
Лечится ручным добавлением недостающего тэга (посмотреть можно в логе билда) - в сообщении релиза в таком случае будет указан оверрайд.
