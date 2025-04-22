# Компонент [Logistic Gateway](https://wiki.yandex-team.ru/delivery/development/apps/lgw/)

## Запуск интеграционных large тестов testcontainers

Перед запуском large тестов, необхододимо сначала спулить нужные docker образы:

```
docker pull registry.yandex.net/market/delivery/elastic-mq-custom:0.0.1
docker pull registry.yandex.net/market/delivery/fake-s3:0.0.1
```
Об авторизации в docker registry описано здесь: https://wiki.yandex-team.ru/qloud/docker-registry/#authorization

Запуск тестов: ```$ ya make -ttt```

Документация: https://wiki.yandex-team.ru/delivery/development/apps/lgw/

#  Запуск приложения
1. Устанавливаем [Docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/).
2. [Авторизуемся](https://wiki.yandex-team.ru/qloud/docker-registry/#avtorizacija) на registry.yandex.net.
3. Затем запускаем зависимости-заглушки (sqs, postgres, ...): в папке dependency-stubs ```docker-compose up -d```. __На linux-е может понадобиться ```sudo```__.
4. В Intellij добавить Spring Boot конфигурацию, в которой в поле Environment variables прописать ```log.dir=log;environment=local;PROPERTIES_DIR={абсолютный путь до папки properties.d}```.
- переименновать локальные конфиги:
  - ```cp logistic-gateway/logistic-gateway-app/src/main/conf/local/logback.xml.dist logistic-gateway/logistic-gateway-app/src/main/conf/local/logback.xml```
  - ```cp logistic-gateway-app/src/main/properties.d/application-local.properties.dist logistic-gateway-app/src/main/properties.d/application-local.properties```
  - ```cp logistic-gateway-app/src/main/properties.d/lgw-secrets.properties.dist logistic-gateway-app/src/main/properties.d/lgw-secrets.properties```

## TVM локально

Чтобы протестить локально работу приложения с TVM и Spring Security нужно добавить spring профиль security-test. Как это можно сделать:

- В Intellij в поле  Environment variables ```spring.profiles.active=local,security-test```

## Необходимые тулзы

- [aws-cli](https://aws.amazon.com/ru/cli/), для работы нужен конфиг, aws-config.zip, распаковать в home.
- [команды sqs](https://docs.aws.amazon.com/cli/latest/reference/sqs/index.html)
