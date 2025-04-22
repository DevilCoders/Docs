# Пакет для автоматического обновления зависимостей

Пакет позволяет просмотреть и обновить список устаревших зависимостей в проекте, размещенном как в основном github, так и в монорепозитории

Данные о состоянии пакетов репозитория берутся из [ОКО](https://oko.yandex-team.ru)

При использовании пакета в режиме для монорепозитория учитываются рекомендации [depslint.json](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/.depslint.json)


##  Принцип работы

- Запрос в ОКО за списком устаревших пакетов

- Получение последней актуальной версии пакета из ОКО

- Если установлен режим монорепозитория, то последняя актуальная версия берется из [depslint.json](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/.depslint.json)

- Создание коммита для каждого обновления пакета и пуш в текущую ветку

##  Установка

Устанавливаем пакет глобально:

```
npm i -g @yandex-int/update-deps --registry http://npm.yandex-team.ru 
```

Для запросов к ОКО необходимо установить переменную окружения `OKO_OAUTH`

```shell script
export OKO_OAUTH={любой-валидный-oauth-ключ}
``` 

:heavy_exclamation_mark: Если OAuth ключ отсутствует, то его можно получить по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cdd999bbe04b4544897dee3436ece20a) 

##  Использование

`npx update-deps`

##  Параметры

`-t` - номер тикета для формирования названия коммита. Пример названия: `TICKET-123: webpack@4.24.0`

`-r` - репозиторий. Например `tools/collabedit`

`-d` - dry-run запуск. В этом режиме ничего не коммитится и не пушится. Выводится список зависимостей и версий, до которых их необходимо обновить

`-m` - режим монорепозитория. Актуальные версии берутся из [depslint.json](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/.depslint.json)

`-vcs` - `github` или `arcadia`. По-умолчанию `github`

`-rf` - фильтр для [монорепозитория](https://github.yandex-team.ru/search-interfaces/frontend). Если указан репозиторий `search-interfaces/frontend`, то для указания конкретного сервиса или пакета в нем нужно передать этот параметр.
Пример: `-r search-interfaces/frontend -rf services/vconf`

`-e` - перечисление через пробел пакетов, которые нужно исключить из списка обновления. Пример: `-e webpack babel ... react`

Пример запуска пакета:

```shell script
npx update-deps -r tools/collabedit -t CODE-239 -d -m
npx update-deps -r search-interfaces/frontend -rf services/vconf -t VCONF-555 -d -m
```
