## Update icons and illustrations by Frigga

#### Description

Создает тикет на обновление иконок и иллюстраций с PR в арке

#### Environment variables

| Имя                       |                     Описание                     | Обязательность |
| ------------------------- | :----------------------------------------------: | -------------: |
| TRAVEL_CI_PATH            |       Путь до папки с ci фронтенда портала       |             да |
| STARTREK_TOKEN            |           Секретный токен доступа в ST           |             да |
| VAULT_AUTH_KEY            | Секретный токен для получения ключа от апи фигмы |             да |
| STARTREK_PARENT_TICKET_ID |          Родительская задача (процесс)           |             да |
| VERSION                   |          Порядковый номер запуска flow           |             да |
| TRIGGERED_BY              |                Кто запустил flow                 |             да |
| BRANCH_NAME               |              Имя создаваемой ветки               |             да |

#### Badges

```yaml
result_badges:
    - path: arcanum
    - path: startrek
```
