# Запуск ассесоров

1. Получить токен: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6d967b191847496a8a7077e2e636142f
2. `TESTPALM_OAUTH_TOKEN=<SECRET> npx testpalm-suite-runner ./assessors/release-collections-preset1.json --project-id=collections-dev --dry-run`

### Ссылки
- документация по регрессионному тестированию https://wiki.yandex-team.ru/crowd/testing/regress/
- документация по хитману https://wiki.yandex-team.ru/hitman/documentation/
- пример процесса в hitman https://hitman.yandex-team.ru/projects/testing_serp/united_assessors_adapter_collections-dev/
