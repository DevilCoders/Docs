# down-tanker [![Build Status](https://drone.yandex-team.ru/api/badges/maxpon/down-tanker/status.svg?branch=master&style=flat)](https://drone.yandex-team.ru/maxpon/down-tanker)

Утилита для скачивания переводов из Танкера.

## Установка

```bash
npm install -g down-tanker --registry=http://npm.yandex-team.ru
```

## Конфигурация

Положите файл конфигурации `.tankerrc` в корень проекта.
```json
{
  "api": "https://tanker-api.yandex-team.ru",
  "token": "<OAuth token>",
  "endpoint": "./static/common.blocks/i-locale",
  "noBemify": true,
  "projects": [
    {
      "project": "company",
      "keysets": ["labels"]
    },
    {
      "project": "tanker",
      "keysets": ["months", "days"],
      "branch": "testing",
      "params": {
        "status": "unapproved",
        "safe": "true"
      }
    }
  ]
}
```

Также опционально можно указать время ожидание ответа и/или количество повторных запросов. Если они не были явно указаны, то время ожидание ответа по-умолчанию будет равно 2000 мс (2 секунды), а количество повторных запросов - 2. Пример конфига:
```json
{
    ...
    "timeout": 5000,
    "retries": 1,
    ...
}
```

По-умолчанию используется IPv6, но можно через конфиг явно указать использование IPv4:
```json
{
    ...
    "family": 4
    ...
}
```

**OAuth token**  
> Применяется только для https-соединений.  

OAuth-токен указывается  в `.tankerrc` в поле `token` или в переменной окружения `TANKER_OAUTH_TOKEN`.

Ссылка на пост-инструкцию: https://clubs.at.yandex-team.ru/tanker/729  
Ссылка для получения токена: https://nda.ya.ru/3SjQY7

**Поле `keysets` необязательное.** Принимает массив строк с именами кейсетов, которые хотим забрать из Танкера. Если поля нет или в него передать пустой массив, придут все переводы.

## Использование

```bash
$ down-tanker <options>
```

**Опции**

```bash
--verbose       Выводить подробную информацию
--no-bem        Не создавать БЭМ-специфичную структуру переводов
```
