# Релизный процесс

1. [Подготовка конфига](#подготовка-конфига)
2. [Сборка и выкладка docker образа](#сборка-и-выкладка-docker-образа)
3. [Выкладка в тестинг](#выкладка-в-тестинг)

## Подготовка конфига

Перед сборкой релиза необходимо прописать в `env.production.yml` логин и пароль для доступа к продовой базе данных

```
dbConfig:
    username: [db-user]
    password: [db-password]
```

Логин с паролем можно взять из [секретницы](https://yav.yandex-team.ru/secret/sec-01fvf2b8sajxbjhf0sv653k2af)

## Сборка и выкладка docker образа

Собираем новую версию докер образа:

```
docker build . -f ./Dockerfile.shopper -t registry.yandex.net/shopper:<version>
```

Для выкладки новой версии докер образа в `registry.yandex.net/shopper` необходимо запросить роль `contributor` через
[IDM](https://nda.ya.ru/t/Jc6yuYcu4sczPG)

![Docker-registry → Repositories → shopper → contributor](https://jing.yandex-team.ru/files/maximshilov/img_1.png)

После получения апрува выкладываем собранный образ:

```
docker push registry.yandex.net/shopper:<version>
```

## Выкладка в тестинг

Чтобы выложить новую версию в тестинг нужно обновить `Docker image` в
[конфиге тестового стейджа](https://deploy.yandex-team.ru/stages/shopper-testing/config/du-application/box-nodejs#resources)

![Docker image tag](https://jing.yandex-team.ru/files/maximshilov/Снимок%20экрана%202022-03-23%20в%2013.59.21.png)
