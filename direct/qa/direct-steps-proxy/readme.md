Сервис - https://deploy.yandex-team.ru/stage/direct-apisteps-proxy

Джоба сборки - https://jenkins-new.qart.yandex-team.ru/job/direct-applications/job/apisteps-proxy/

Инструкция по обновлению - https://docs.yandex-team.ru/direct-dev/guide/jeri/ts-ext-tools-update

Пример работы:

1) Создаем апи степы, получаем токен:
*curl --data '{"direct_stage" : "TS"}' -v -X POST -H 'Content-Type:application/json' 127.0.0.1:8082/initStep*
**7dfa6b61-aac7-48b2-ad09-f4aa47276a4c**

2) Вызываем апи степы, получаем ответ:
*curl --data '{"token": "7dfa6b61-aac7-48b2-ad09-f4aa47276a4c", "stepPath": "campaignSteps.createDefaultCampaign", "params": [{"clazz": "java.lang.String", "value": "at-direct-backend-c"}]}' -v -X POST -H 'Content-Type:application/json' 127.0.0.1:8082/callStep*
**<Integer>82183723</Integer>**

3) Удаляем апи степы:
*curl -v -X DELETE -H 'Content-Type:application/json' '127.0.0.1:8082/removeStep?token=7dfa6b61-aac7-48b2-ad09-f4aa47276a4c'*

#TODO: не может работать на нескольких машинках из-за локального хранилища, необходимо вручную переключать, как здесь https://st.yandex-team.ru/DIRECT-126935#5f639a29437a2d293f7bf08e
