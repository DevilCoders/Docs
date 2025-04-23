# TVM tool docker image

## Описание

Сборка докер образа с бинарным файлом из sandbox **tvmtool**. Отправка в yandex Docker registry.

## Выполнение

Для сборки необходимо зарегистрировать приложение на yandex Oauth с правами на доступ к Sandbox API.
После получения токена с помощью Makefile возможно выполнить следуюющие операции.

### Собрать контейнер с TVM tool

```bash
make docker-build TOKEN=<OAuth токен>
```
