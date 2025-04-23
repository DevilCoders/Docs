# Autobetas

Автоматическое создание актуальной авто-беты на веб-хук в GitHub.

Сервис запускает задачу в Sandbox и добавляет ссылку на авто-бету в комментарий к задаче в Startrek.

## Установка

Переходим в настройки репозитория: Settings > Hooks > Add webhook

**Payload URL**

```
https://autobeta.mtrs.yandex-team.ru/webhooks/github
```

**Content type**
```
applications/json
```

**Which events would you like to trigger this webhook?**
```
Let me select individual events > Оставляем только Pull requests
```

## Требования для правильной работы сервиса

Имя ветки должно содержать название очереди, которое будет сопоставлено с сервисом.

Например, `gbiz-METR-37324`. Сервис определяется через RegExp `/([A-Z]+).?\d+/.exec(branch)[1]`

Сервисы, которые поддерживаются:
```
{
    METR: 'metrika-frontend',
    CDP: 'metrika-frontend',
    METRIKASUPP: 'metrika-frontend',
    AUDIENCE: 'audience-frontend',
    MOBMET: 'appmetrica-frontend',
    RADAR: 'radar-frontend',
    METRADV: 'mediametrika-frontend',
}
```

## Разработка

```
# установка зависимойстей из корня репозитория
npm run bootstrap:autobeta

# запуск сервиса из дирректории
cd services/autobeta
make compose-up
```

На данном этапе сервис поддерживает отладку только через HTTP запросы.

Поддерживается три типа событий (поле `action` в JSON)
- opened — открыт pull request
- synchronize — произошли изменения в ветке
- closed — pull request принят, авто-бету надо удалить

```
curl https://gbiz.dev.metrika.yandex.ru/webhooks/github -X POST -H "Content-Type: application/json" -d '{"action": "synchronize", "pull_request": {"head": {"ref": "gbiz-METR-39668"}}}'
```

## Как добавить новый сервис?

- Добавить название очереди в коллекции внутри файла `server/models/constants.ts`
- Обновить список сервисов в README.md
- Залить изменения в develop через PR и затем собрать релиз

## Релиз

1. Собрать новый образ в Sandbox при помощи задачи [BUILD_DOCKER_IMAGE_FROM_GIT](https://sandbox.yandex-team.ru/task/728372459/view)
<br>Надо увеличить версию в полях: `Tags to publish image with` и `Docker --build-arg option`
<br>Текущую версию можно узнать в [настройках stage](https://deploy.yandex-team.ru/stage/metrika-frontend-autobeta/config#Box1)
2. Обновить образ для сервиса в [Yandex Deploy](https://deploy.yandex-team.ru/stage/metrika-frontend-autobeta)
