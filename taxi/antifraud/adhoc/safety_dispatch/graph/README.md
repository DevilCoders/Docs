## Безопасный диспатч

Проект содержит граф с offline оценкой эффекта уменьшения доли дтп от добавления штрафа в диспатчер такси.

Шаги:
* сбор выборки заказов для обучения с таргетами
* сбор фичей на заказе, известных в момент создания заказа
* обучение моделей прогнозирования вероятности дтп на заказе/дпт с пострадавшими/дтп в течении 1 часа после начала заказа/...
* сбор выборки заказов для имитации диспачра, обогащение фичами и предиктами моделей
* имитация диспатчера от добавления штрафа с оценкой эффекта
* публикация результата в [пульсар](https://pulsar.yandex-team.ru/instances/table?column=instance.username&column=instance.datetime&column=instance.description&column=metric.prob_injured_diff_when_rt_max&column=metric.auc_order_accident&column=metric.auc_order_injured&column=metric.auc_order_prod&column=metric.auc_executor_accident&column=metric.auc_executor_injured&column=metric.auc_executor_prod&dataset=safety-dispatch&tableState=48c81c8)

## Запуск чернового workflow

### Подготовка секретов

Подкладываем к себе в домашнюю дирректорию нирвановский токен в `~/.nirvana/token`([nirvana_token](https://wiki.yandex-team.ru/nirvana/components/api)).
Добавляем профиль в `~/.vh3/profile.yaml` с содержимым

```yaml
quota: 'taxiafs'
yt_token: 'my-yt-token' # - имя yt токена в секретнице нирваны
yql_token: 'my-yql-token' # - имя yql токена в секретнице нирваны
mr_account: 'taxi-fraud/users'
pulsar_token: 'my-pulsar-token' # - имя pulsar токена в секретнице нирваны
yav_oauth_token: 'my-yav-aouth-token' # - имя yav токена в секретнице нирваны
yt_secret_key: 'sec-my-yt-secret-from-vallet' # - ключ yt токена в секрентице нирваны вида sec-...
workflow: !object:vh3.Workflow
  id: 'my-workflow-id' # - workflow id в котором будет содаваться черновой граф
```

Получить токены можно постараться здесь:
* [yt_token](https://oauth.yt.yandex.net)
* [yql_token](https://wiki.yandex-team.ru/market/analytics/stackoverflow-analitiki-marketa/yt/gde-vzjat-token-dlja-yt/#gdevzjattokendljayql)
* [pulsar_token](https://wiki.yandex-team.ru/pulsar/kak-poluchit-oauth-token-dlja-pulsara)
* [yav_oauth_token](https://vault-api.passport.yandex.net/docs/#oauth)

[Как добавить секреты в нирвану?](https://docs.yandex-team.ru/nirvana/operations/security/create-secret)

Для возможности запускать jupyter ноутбуки в нирване добавляем ID секрета yt токена:
* на https://yav.yandex-team.ru ищем свой yt_token и берем его ID (строку вида sec-...)
* заходим на jupyter.yandex-team.ru c интерфейсом jupyterlab и создаем ноутбук с аркадийным ядром
* нажимаем на Manage Secrets и добавляем произвольное Name, а в UUID кладем ID секрета

### Запуск

```
ya make && ./graph draft safety_dispatch_imitation 
```
В результате выведется ссылка на граф. Переходим и жмем RUN.

## Тестированиe
```
ya make -t
```

## Разработка

### Добавление фичей

Пишем yql скрипт с шапкой
```
DECLARE $input1 AS String;
DECLARE $output1 AS String;
DECLARE $param_dict AS Dict<String, String>;
```
* на вход скрипту будет подаваться таблица `$input1`, в которой есть уникальный ключ заказа `order_id`
* через параметры `$param_dict['date_from']`, `$param_dict['date_to']`  передается диапозон дат, которому принадлежат заказы 
* в выход `$output1` нужно записать табличку с уникальным ключем `order_id` и столбцами - фичами

Кладем его в `features/<my-features-group-name>.sql`

Добавляем путь к скрипту в `ya.make` чтобы использоватеь еге через ресурсы

Добавляем тест на проверку корректноти синтаксиса скрипта в `features/ya.make`

В `main.py`
* у подграфа-функции `add_features` добавляем новую группу фичей
* у графа-функции `safety_dispath_imitation` в вызове `train_model` у параметров `features_{executor,order}_{,prod}_pattern` добавляем новые фичи
  * в `executor` для фичей водителя
  * в `order` для фичей заказа
  * в `prod` для фичей, которые мы будем использовать для расчета штрафа в диспатчере

После этого можем запустить граф с новой группой фичей
```
ya make && ./graph draft safety_dispatch_imitation 
```

### Аналитический дашборд

Влияние фичей на таргет можно посмотреть на дашборде: https://datalens.yandex-team.ru/sarkvi5ah9bwm-features-analyzer?state=20e06795313 
* в селектор table_path подсатвляем выход кубика `add_features` на обучающей выборке

