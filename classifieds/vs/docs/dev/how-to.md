## How to ...

### Использовать Docker

Docker Desktop хорошо греет воздух, платный и запрещенный, используем докер на виртуалке.

1. Удаляем Docker for Mac с корнями
2. Убеждаемся, что на дев виртуалке установлен и запущен докердемон версии 18.09+
3. На локальной машине выполняем:
```
brew install docker docker-compose
docker context create dev --docker host=ssh://<username>@<username>-01-dev.sas.yp-c.yandex.net
docker context use dev
```

### Локально запускать тесты, зависимых от docker

1. Плагин для запуска ZIO тестов не поддерживает запуск на удаленной машине, поэтому переделываем **ZIO test RunConfiguration**
в **Application RunConfiguration**.

2. Добавляем Target с указанием своей виртуалки (у меня получилось только через agent)
3. Обязательно устанавливаем на виртуалку(удобно через sdkman) и в Java Configuration одну и ту же версию Java.
![Пример настроек](/docs/dev/docker-test.png)
4. Если при запуске теста летят ошибки вида:
```
com.github.dockerjava.api.exception.InternalServerErrorException: Status 500: {"message":"Get https://registry.yandex.net/v2/yandex-docker-local-ydb/manifests/stable: no basic auth credentials"}
```
то можно руками запулить отсутствующий образ на виртуалке:
```shell
docker login -u <login> -p <ya_token>  registry.yandex.net
docker pull registry.yandex.net/yandex-docker-local-ydb:stable
```

_ya_token_ брать из [отсюда](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1)