## Удаляем все ключи из кейсета

### Получить все ключи из ветки

```curl
curl --location --request GET 'https://tanker-beta.yandex-team.ru/api/v1/project/wfm/branch/<BRANCH>/export?sort=name' \
--header 'accept: application/json' \
--header 'Authorization: OAuth <TOKEN>'
```

Полученный ответ сохраняем в `./scripts/tanker/api/remove.json`

### Конвертнуть все ключи в формат для удаления

1. Запускаем скрипт `node ./scripts/tanker/api/remove.js`
2. Скрипт сгенерит файлы на каждый кейсет в `./scripts/tanker/api/for_remove_keyset_${keyset}.json`

### Удаляем ключи

```curl
curl --location --request POST 'https://tanker-beta.yandex-team.ru/api/v1/project/wfm/keyset/<KEYSET>/branch/<BRANCH>/batch' \
--header 'accept: */*' \
--header 'Content-Type: application/json' \
--header 'Authorization: OAuth <TOKEN>' \
--data-raw '{
    "commit_message": "feat: remove all from test branch",
    "delete": {
        "keys": [] // сюда вставлем массив из файлов выше по очереди
    }
}'
```

### PROFIT!!!
