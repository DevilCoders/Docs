# API DNS-хостинга

**Текущий релиз:** 0.13.0

## Подготовка окружения

```bash
pip install -r requirements.txt
pip install .
```

*Тестовое/девелоперское окружение*

```bash
pip install -r requirements.txt
pip install -r requirements.dev.txt
pip install -e .
```

## Запуск юнит-тестов локально

```bash
export APPLICATION_PROFILES_ACTIVE=unittest 
dnscli pgmigrate migrate -t latest
python -m unittest discover
```

Для тестов необходима БД со последними миграциями.

Тесты автоматически запускаются при сборке образов командой:

```bash
./build_images.sh
```

## Миграция БД локально

```bash
dnscli pgmigrate [OPTIONS] [ARGS]
```

Команда представляет собой обертку над 
[pgmigrate](https://github.com/yandex/pgmigrate/), которая для удобства
подставляет настройки соединения и путь к файлам миграции.

## Обновление цепочки доверенных корневых сертификатов

Вряд ли это понадобится, но это можно сделать так:

```bash
curl https://crls.yandex.net/allCAs.pem -o docker/base/certificates/yandex.crt
```

Затем скачать YandexCA с [этой вики-страницы](https://wiki.yandex-team.ru/security/ssl/pinning/.files/yandexca.pem).
И добавить его к `docker/base/certificates/yandex.crt`:

```bash
cat ~/Downloads/YandexCA.pem >> docker/base/certificates/yandex.crt
```

## Сборка образов

```bash
./build_images.sh
```

Во время сборки также генерится файл `push_images.sh`, который содержит
все необходимые команды для пуша образов в docker-registry. Чтобы 
опубликовать все образы достуточно его вызвать:

```bash
./push_images.sh
```

## Запуск интерактивной Python-консоли

```bash
dnscli py-shell
```

## Запуск сервера API

```bash
dnscli run-server
```

## Запуск DNS-мастера для AXFR

```bash
dnscli dnsmaster dns
```

## Запуск DNS-мастера для списка зон

```bash
dnscli dnsmaster http
```

## Запуск DNS-слейва

```bash
dnscli nsd dns-server
```

## Запуск stat-сервера для DNS-слейва

```bash
dnscli nsd stat-server
```

## Запуск мигратора ПДД-зон

```bash
dnscli pdd migrate
```

# Настройки

Настройки для сервисов можно задавать двумя способами:
1. Через файлы настроек (профили) - удобно для манипулирования настройками 
по умолчанию и компановке различных групп насроек.
2. Переменные окружения - удобно для переопределения настроек по умолчанию 
для тестовых окружений.
