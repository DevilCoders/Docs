# mbo-card-api

Http сервис, хранящий в себе модели, позволяющий добавлять, удалять и изменять карточки на mbo, которые в последствии появятся в выгрузке.

## Локальный старт
- находим `MboCardApiMain` и запускаем в IDEA
- оно несколько раз упадёт - читайте и выполняйте команды:
  - work dir должен быть на `mbo-catalog` в Аркадии (скрипт это сам пофикисть может очень с трудом... пути есть, но чтобы надёжно было - надо проверять)
  - скажет, что не хватает разнообразных пропертей и даст `scp` команды, как их принести, можно просто выполнить
- чтобы запустить в testing окружении - добавляем явно в запуск `-Denvironment=testing -Dlocal=1` (это нужно чтобы машинерия локального запуска не активировалась в настоящем тестинге)
  - попросит принести чуть побольше файлов (даст команды, чтобы принести)

## Локальный запуск интеграционных тестов
Для запуска интеграционных тестов используется команда:
```bash
ya make -ttt
```

## Devops

### Дашборды

#### Прод
- [NGINX](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-card-api-autogeneration-production)
- [NGINX clusterizer](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-card-api-clusterizer-production)

#### Тестинг
- [NGINX](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-card-api-autogeneration-testing)
- [NGINX clusterizer](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-card-api-clusterizer-testing)
