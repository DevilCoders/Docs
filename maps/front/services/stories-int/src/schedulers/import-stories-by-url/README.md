# import-stories-by-url

-   Шедулер для добавления/удаления/редактирования большого количества сториз
-   Запускается каждый будний день в 00:00.
-   Сделан с помощью (@yandex-int/bean)[https://a.yandex-team.ru/arc_vcs/maps/front/packages/bean].

## Общая информация

| Key      | Value                                                                                                                |
| -------- | -------------------------------------------------------------------------------------------------------------------- |
| Nirvana  | https://nirvana.yandex-team.ru/flow/9e21896c-bb79-474f-938d-852d9e496876/                                            |
| Reaction | https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/stories-int/import-stories-by-url                     |
| Sandbox  | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/schedulers/binary/stories-int/import-stories-by-url |

## Сервисы, которые нагружаются запросами из шедулера

| Key        | Value                                                                                                        |
| ---------- | ------------------------------------------------------------------------------------------------------------ |
| StoriesInt | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-stories-int_production |
| BvmInt     | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-adv-bvm-int_production       |

## Как это работает

1. Ходит по внешнему урлу партнёра и забирает файл с данными для сториз
2. Парсит, чтобы из этих данных
    - получить `permalinks` организаций
    - получить внешние урлы к изображениям (должны лежать во внешнем открытом для всех хранилище)
3. Для каждого найденного `permalink` получает `bizId` (делает http-запросы в `BvmInt`)
4. Каждой изображение перекладывает в Аватарницу (делает http-запросы в `AvatarsInt`)
5. Потом отправляет все эти данные в ручку импорта сториз в `StoriesInt`

## Для запуска шедулера нужны переменные окружения

```
PARTNER_NAME
PARTNER_TAGS
STORIES_URL
ENVIRONMENT
POSTGRES_PORT
POSTGRES_USER
POSTGRES_DATABASE
```

Их необходимо указать в глобальных переменных в Реакции (см. `lama.yaml`):

```
POSTGRES_PASSWORD
TVM_SECRET
```

Эти уже сохранены в Секретнице: [`maps-front-stories-int_scheduler-activate-geosearch-snippets_production`](https://yav.yandex-team.ru/secret/sec-01g4wk2j0b3rz1g2b4b4f42ekr). Значения этих секретов идентичны проектным [`maps-front-stories-int_production`](https://yav.yandex-team.ru/secret/sec-01en60rkjnqvb7aagtjcrq47rx), но в шедулере используются не проектные, потому что шедулеру нужен особый тип секрета (где имя — `nirvana_secret`, а значение — пары `TVM_SECRET=<значение1> DB_PASSWORD=<значение2>`)

```
YA
YA_TOKEN
```

Уже заданы на уровне кода Нирвана-кубика с кодом `@yandex-int/bean`, не нужно указывать отдельно.

## Что случится, если шедуллер упадёт

-   В базе данных Сториз не обновятся партнерские сториз.
-   Пользователи Бекенда Сториз увидят в сториз устаревшие изображения.
