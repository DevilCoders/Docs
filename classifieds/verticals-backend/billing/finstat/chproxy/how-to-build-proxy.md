## Сборка chproxy

## Особенности

Текущая отличается от оригинального chproxy форматом логов и парсингом параметров в запросах. (chproxy не поддерживает их)

В chproxy есть свои юзеры, по которым происходит маппинг запросов на соответствующий кластер и использвоание кредов этого кластера.

### Проблемы
1. Для chproxy нужен github.com/DataDog/zstd, который не собирается под макосью с нужными флагами (GOOS=linux GOARCH=amd64)
Оригинальный xgo, который рекомендуется для кросс-компиляции, заброшен и последний билд не поддерживает нужны опции.
Есть несколько форков, наиболее похож на живой [techknowlogick/xgo](https://github.com/techknowlogick/xgo). На момент написания также не завёлся

2. В версии, которая используется в образе, есть зависимость на github.com/YandexClassifieds/go-common/log, лежащий в приватной репe

### Как собрать
0. Нужен докер залогиненый в yandex registry: [дока от опсов](https://wiki.yandex-team.ru/docker-registry)
1. Поставить golang:
```bash
wget -O /tmp/golang.tar.gz https://go.dev/dl/go1.18.4.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf /tmp/golang.tar.gz
export PATH=$PATH:/usr/local/go/bin
```
2. Для доступа к YandexClssifieds/go-common
```bash
git config --global url."git@github.com:".insteadOf "https://github.com/"
export GOPRIVATE=github.com/YandexClassifieds/*
```
NB: для этого на хосте должен быть ssh-ключ с доступом до github.
Альтернативный вариант -- через github token, но так чуть сложнее.
```bash
git config --global url."https://<GITHUB_USER>:<GITHUB_TOKEN>@github.com".insteadOf "https://github.com"
export GOPRIVATE=github.com/YandexClassifieds/*
```
3. Для сборки zstd поставить g++ (видимо, нужна какая-то специфичная версия плюсового компилятора)
```bash
sudo apt-get install g++
```
4. Обновить версию в Makefile
5. Собрать докер-образ и запушить его в docker registry
```bash
make env=<test|prod> build && make push
```

Теперь можно выкатить сервис в шиву.

### История изменений

По `arc log src` можно понять, какие изменения наши разработчики сделали относительно апстрима.
