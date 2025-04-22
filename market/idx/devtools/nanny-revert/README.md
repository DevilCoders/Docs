# Откатывалка пакетов в Nanny

## Мотивация
1. Откат релизов через ЦУМ активирует старый снепшот, который был в момент выкладки. Соответсвенно, берутся устаревшие данные из sandbox(например файлы геттера, релизи datasources и т.д.). Проблема в том, что некоторые SB ресурсы уже может быть удалены, тогда няня не сможет подготовить снепшот.
2. Перевыкладывать через хотфикс долго и не очень логично
3. Тыкать в UI няни неудобно. Может активироваться новый снепшот, тогда придется начать все сначала. Тыкать в каждом сервисе: testing, prestable, stable.

## Использование
1. Получаем OAUTH токен няни https://nanny.yandex-team.ru/ui/#/oauth/ и сохраняем его в файл
3. Определяем сервисы, которые хотим откатить, например ```testing_market_offersrobot2_sas```
4. Определяем ресурсы, которые хотим откатить, например [1154178824](https://sandbox.yandex-team.ru/resource/1154178824/view)
5. [Optional] Запускаем откатывалку в dry-run режиме ```python revert.py --service <список сервисов в RTC> --resource-id <список ресурсов> --comment <причина отката> --dry-run```
6. Запуск без dry-run создаст снепшот, но не активирует его
7. Переходим по ссылкам и активируем каждый снепшот руками

### Пример отката релиза робота
* Откатываем тестинг на релиз [2019.4.593](https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/robot-stages/release/5dc158da103b9d03cb61e1dc).
* Нас интересуют ресурсы тасок [Сборка архива FEEDPARSER](https://sandbox.yandex-team.ru/task/542054078/view) и [Сборка архива OFFERS_ROBOT2](https://sandbox.yandex-team.ru/task/542054081/view), это ресурсы 1197491779 MARKET_FEEDPARSER_APP и 1197491763 MARKET_OFFERS_ROBOT2_APP.
* Nanny сервисы testing_market_offersrobot2_sas и testing_market_offersrobot2_yellow_sas

```
python revert.py --service testing_market_offersrobot2_sas testing_market_offersrobot2_yellow_sas --resource-id 1197491779 --resource-id 1197491763 --comment "Revert example" --nanny-token ~/.nanny_token --dry-run

Will revert to the following sandbox resources:
{'task_type': u'MARKET_YA_PACKAGE', 'resource_type': u'MARKET_FEEDPARSER_APP', 'task_id': '542054078', 'resource_id': '1197491779'}
{'task_type': u'MARKET_YA_PACKAGE', 'resource_type': u'MARKET_OFFERS_ROBOT2_APP', 'task_id': '542054081', 'resource_id': '1197491763'}
Reverting service testing_market_offersrobot2_sas
Resource MARKET_OFFERS_ROBOT2_APP, 1199462911 => 1197491763
Resource MARKET_FEEDPARSER_APP, 1200164596 => 1197491779
Reverting service testing_market_offersrobot2_yellow_sas
Resource MARKET_OFFERS_ROBOT2_APP, 1199462911 => 1197491763
Resource MARKET_FEEDPARSER_APP, 1199462949 => 1197491779
```

```
python revert.py --service testing_market_offersrobot2_sas testing_market_offersrobot2_yellow_sas --resource-id 1197491779 --resource-id 1197491763 --comment "Revert example" --nanny-token ~/.nanny_token

Reverting service testing_market_offersrobot2_sas
Success, activate new snapshot: http://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_offersrobot2_sas
Reverting service testing_market_offersrobot2_yellow_sas
Success, activate new snapshot: http://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_offersrobot2_yellow_sas
```

## TODO
1. Автоматическая активация снепшота
