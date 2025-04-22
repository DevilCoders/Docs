# Monitorado

это генератор конфигов для алертов. Нами используется для клиентских ошибок (error-booster -> golovan -> juggler).

## Установка

1. Поставить npm-пакет из внутренней репы.
```bash
npm i -g @yandex-int/monitorado --registry=https://npm.yandex-team.ru
```

2. Получить токен [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=171fcece39a04fd0a6b8b74950336008)
и положить в переменную окружения `MONITORADO_OAUTH_TOKEN`.

Также поддерживается загрузка из файла `.env`, который должен лежать в рабочей директории

## Использование
1. Смотрим, какие изменения будут сделаны:
```bash
monitorado diff -v
```

2. Настраиваем мониторинги:
```bash
monitorado exec -v
```
