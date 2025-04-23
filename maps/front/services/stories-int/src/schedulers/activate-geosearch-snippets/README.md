# activate-geosearch-snippets

-   Включает геопоисковый сниппет `stories_experimental/1.x` для всех организаций, у которых есть сторис
-   Запускается каждый будний день в 16:00
-   Длительность исполнения зависит от количества организаций, у которых есть сторис. Например, для 75000 организаций исполняется примерно 40 минут.
-   Сделан с помощью (@yandex-int/bean)[https://a.yandex-team.ru/arc_vcs/maps/front/packages/bean].

## Общая информация

| Key      | Value                                                                                                                      |
| -------- | -------------------------------------------------------------------------------------------------------------------------- |
| Nirvana  | https://nirvana.yandex-team.ru/flow/9e21896c-bb79-474f-938d-852d9e496876/                                                  |
| Reaction | https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/stories-int/activate-geosearch-snippets                     |
| Sandbox  | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/schedulers/binary/stories-int/activate-geosearch-snippets |

## Dashboards

| Key        | Value                                                                                                        |
| ---------- | ------------------------------------------------------------------------------------------------------------ |
| StoriesInt | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-stories-int_production |
| BvmInt     | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-adv-bvm-int_production       |

## Как это работает

1. Ходит в базу `StoriesInt`

-   получает список `bizId` тех организаций, у которых есть сторис
-   подклеивает к ответу историю с тегом `lastMile`, если она существует

4. Для каждого `bizId` получает `permalink` (делает http-запросы в `BvmInt`)
5. Для каждого `permalink` делает запрос в геопоисковый сниппет, чтобы его включить.

## Для запуска шедулера нужны переменные окружения

```
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

В карточках организаций (в БЯК, в МЯК) не отобразятся сторис.
