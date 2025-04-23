# infraduty

Микросервис для поддержки механизма эскалации обращений в INDRAFUTY.

Сервис отвечает:

- `200 ESCALATE`, если есть обращения в статусе `Escalate` по определенному фильтру
- `200 OK`, если таких обращений нет
- `503 OK`, если не удалось получить обращения от трекера

Механизм эскалации полностью описан в [документации дежурства](https://doc.yandex-team.ru/si-infra/duty_knowledge_base/eskalaciya.html).

## Разработка

```sh
npm i
cp .env.example .env
```

В `.env` нужно задать все пустые переменные, а комментарии удалить.

Запуск сервера:

```sh
npm run dev
```

## Публикация новой версии

После влития пулл-реквеста выполнить на актуальной ветке trunk:
```
make docker-publish
```

Для деплоя стоит использовать следующую команду dctl:
```
$(arc root)/ya tool dctl release docker search-interfaces/infraduty -t $(jq -r .version package.json)
```

После выполнения команды в [Deploy tickets](https://deploy.yandex-team.ru/stages/infraduty/deploy-tickets) вкладке
окружения нажать Commit.

## Развертывание

[Окружение](https://deploy.yandex-team.ru/stage/infraduty). Образ – `registry.yandex.net/search-interfaces/infraduty`.

## Генерация проверок для дежурства

В ручки сервиса ходят [проверки](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dinfraduty) Juggler. Для автоматической перегенерации проверок выполните команду:

```
npm run juggler-checks
```

результат команды надо будет скопировать в Juggler вручную.

## Мониторинги сервиса

Мониторинги лежат в [.config/infraduty.monitorado.yml](./.config/infraduty.monitorado.yml), после изменений посмотреть дифф можно командой:

```
npm run monitoring:diff
```

Залить в yasm командой:

```
npm run monitoring:upload
```
