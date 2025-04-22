## Create stage in Deploy

#### Description

Создает stage в [Yandex Deploy](https://deploy.yandex-team.ru/)
из конфига в файле YAML.
Если stage с таким именем есть, то ничего не делает.

#### Environment variables

| Имя                |               Описание               | Обязательность |
| ------------------ | :----------------------------------: | -------------: |
| DEPLOY_STAGE_NAME  |          Имя stage в Deploy          |             да |
| DEPLOY_CONFIG_PATH | Путь до файла с конфигурацией в yaml |             да |
| DCTL_YP_TOKEN      |          Секрет для ya dctl          |             да |
| TRAVEL_CI_PATH     | Путь до папки с ci фронтенда портала |             да |
