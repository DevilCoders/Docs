### Пример приложения реализующего сценарий консьержа.

Приложение имплементирует [сценарий](https://wiki.yandex-team.ru/taxi/ml/supportai/voice-protocol/)

### переменные окружения необходимые для запуска

| переменная            | описание                                                                        |
| --------------------- | ------------------------------------------------------------------------------- |
| ENV                   | окружение ats с которым будет вестись работа (production, preproduction, local) |
| S3_ACCESS_KEY_ID      |                                                                                 |
| S3_SECRET_ACCESS_KEY  |                                                                                 |
| S3_BUCKET             |бакет в s3 из которого надо брать аудиозаписи для проигрывания                   |
| LOGBROKER_READER      |ридер для топика LB в который ATS льет входящие вызовы                           |
| SUPPORTAI_PROJECT_ID  |id проекта в supportai (_default=concierge_incoming_call_)                       |
| SUPPORTAI_HOST        |адрес балансера supportai                                                        |
| IAM_KEYS              |json с ключами iam авторизации                                                   |
| EXTERNAL_CALLS_NUMBER |номер с которого будут осуществляться исходящие вызовы при переадресации звонков |
| SELF_TVM_ID           |tvm_id этого приложения                                                          |
| SELF_TVM_SECRET       |tvm-секрет этого приложения (автоматически кладется в секретницу)                |
| SUPPORTAI_TVM_ID      |tvm_id приложения supportai (_production: 2024769; testing: 2024767_)            |

### Как собрать docker образ
`ya package package-dcoker.json --docker --docker-repository {repo} [--custom-version {version}]`

### Как собрать сборку в Облалко
1. `cd build/cloud && python3 generate_bundle.py && cd ../..`
2. Выбрать новую версию NEW_VERSION
3. `ya package package-cloud.json --docker --docker-registry cr.yandex/crpnq1h4legv4n8hqcgt --custom-version NEW_VERSION`
4. `docker push cr.yandex/crpnq1h4legv4n8hqcgt/supportai-telephony-integration:NEW_VERSION`
5. Обновить build/cloud/deployments/production.yaml - проставить новую версию образа
6. Авторизоваться в docker registry
7. `kubectl apply -f build/cloud/deployments/production.yaml`

### Разработка
Если вдруг захочется посмотреть на код сгенеренного клиента к supportai:
`ya make -r --add-result=py`

для того чтобы можно было выполнять весь код локально без постоянно пересборки в бинарь:
1. генерим фейковый интерпретатор
   `ARCADIA_ROOT=~/arc/arcadia python3 ~/arc/arcadia/junk/sulim/tools/python-debug-generator/py-debug-generator.py`
2. используем его как интерпетаро для запуска `__main__.py`
