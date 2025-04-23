# @yandex-int/si.ci.telegraph-cli

CLI утилита для управления очередями внутренней телефонии.
Описание концепции, терминологии и способа получения токена см. в низкоуровневых пакетах:
[`@yandex-int/si.ci.telegraph-client`][telegraph-client] и [`@yandex-int/si.ci.telegraph`][telegraph].

[telegraph-client]: ../telegraph-client
[telegraph]: ../telegraph

## Установка

```bash
npm install -g @yandex-int/si.ci.telegraph-cli --registry=https://npm.yandex-team.ru
```

## Использование

Токен необходимо передать через переменную окружения `TELEGRAPH_TOKEN`.
Также через `TELEGRAPH_BASE_URL` можно переопределить базовую ссылку на Telegraph API.

```console
$ npx @yandex-int/si.ci.telegraph-cli --help
telegraph <command>

Commands:
  telegraph list <queue-name>               List present queue members' extens.
  telegraph replace-all <queue-name>        Replace all current members of the
  <extens..>                                queue with given extens optionally
                                            appending external prefix

Options:
  --help     Show help                                                 [boolean]
  --version  Show version number                                       [boolean]

Examples:
  telegraph list 76800-1                    Output extens of queue present
                                            members (one per line).
  telegraph replace-all 76800-1 2611 8462   Remove all members from queue
                                            76800-1 and add 2611, 8462.
  telegraph replace-all --external 76800-2  Remove all members from queue
  2611 8462                                 76800-2 and add 552611, 558462.
```

Пример автоматизации переключения номеров дежурных в интеграции с **ABC** и **Staff** с использованием `curl`, `jq` и, опционально, [`@yandex-int/si.ci.abc-cli`][abc-cli]:

```bash
#!/usr/bin/env bash

# Экспортировать необходимые токены:
export ABC_TOKEN="…"
export STAFF_TOKEN="…"
export TELEGRAPH_TOKEN="…"

# Получить список логинов (через запятую) участников ABC сервиса FEI с ролью "Дежурный":
service_slug="fei"
role_code="duty"
people_logins=$(abc members list --role=${role_code} --format=%l -- ${service_slug} | paste -sd, -)

# Получить со Стафф список номеров (через пробел) рабочих телефонов:
staff_auth="Authorization: OAuth ${STAFF_TOKEN}"
staff_url="https://staff-api.yandex-team.ru/v3/persons?login=${people_logins}&_fields=work_phone"
people_phones=$(curl -sSLH ${staff_auth} ${staff_url} | jq -r '.result | map(.work_phone) | join(" ")')

# На первую линию ставим номера рабочих телефонов дежурных:
telegraph replace-all 76800-1 ${people_phones}
# На вторую линию — их же с префиксом 55, означающим "звонить на мобильный":
telegraph replace-all 76800-2 ${people_phones} --external
```

Получить участников **ABC** сервиса можно также с помощью `curl` без использования клиента `@yandex-int/si.ci.abc-cli`:

```bash
abc_auth="Authorization: OAuth ${ABC_TOKEN}"
abc_url="https://abc-back.yandex-team.ru/api/v3/services/members/?service__slug=${service_slug}&role__code=${role_code}&fields=person.login"
people_logins=$(curl -sSLH ${abc_auth} ${abc_url} | jq -r '.results | map(.person.login) | join(",")')
```

[abc-cli]: ../abc-cli

## Отладка

Включить вывод отладочной информации можно с помощью переменной окружения:

```bash
export DEBUG=si:ci:telegraph,si:ci:telegraph-client,serp:env-utils
```
