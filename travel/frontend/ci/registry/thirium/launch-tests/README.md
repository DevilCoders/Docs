## Run e2e tests in Thirium

#### Description

https://th.yandex-team.ru/

-   [API DOCS](https://doc.yandex-team.ru/thirium/project-launch/api/index.html)
-   [Swagger](https://backend-prod.thirium.yandex-team.ru/api/docs-tp/?url=/api/openapi-tp.yaml#/launch/searchTestLaunches)

Вызывает API для запуска тестов в Тириуме.

#### Environment variables

| Имя                 |                                               Описание                                                | Обязательность |
| ------------------- | :---------------------------------------------------------------------------------------------------: | -------------: |
| TRAVEL_CI_PATH      |                                 Путь до папки с ci фронтенда портала                                  |             да |
| THIRIUM_TOKEN       |                                   Секретный токен доступа в Thirium                                   |             да |
| THIRIUM_PRESET      |                               Имя предварительно захаркоженного конфига                               |             да |
| THIRIUM_TEST_FAILED | Блокировать ли флоу при падении тестов. Доступные значения 'ERROR' или 'IGNORE'. По умолчанию 'ERROR' |    опционально |

```yaml
result_badges:
    - path: common
```
