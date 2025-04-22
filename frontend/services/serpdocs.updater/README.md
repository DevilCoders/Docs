# Serpdocs.Updater
Сервис обновления данных документации конструктора web4 (serpdocs)

## Обновление документации
Для обновления нужно отправить POST запрос на /update с следующими полями

* pull_request - пулл-реквест. Допустима строка вида pull/12345. Извлекаются только цифры.
* base_commit - хэш коммита в деве, на котором гоняются проверки. Только для дева
* merge_commit - хэш коммита пулл-реквеста. Только для пулл-реквестов
* serpdocs - json файл со списокм всех блоков и фич по платформам
* desktop-blocks-usage - json файл список использованных адаптеров для платформы desktop
* touch-pad-blocks-usage - json файл список использованных адаптеров для платформы touch-pad
* touch-phone-blocks-usage - json файл список использованных адаптеров для платформы touch-phone

Пример запроса через curl
```bash
curl -X POST \
    -F "pull_request=pull-1234" \
    -F "serpdocs=@serpdocs.json" \
    -F "desktop-blocks-usage=@desktop-blocks-usage.json" \
    -F "touch-pad-blocks-usage=@touch-pad-blocks-usage.json" \
    -F "touch-phone-blocks-usage=@touch-phone-blocks-usage.json" \
    http://localhost:3000/update
```

## Быстрый старт

``` (bash)
git clone git@github.yandex-team.ru:search-interfaces/serpdocs.updater.git
npm i
npm run start:local
```

> Требуется локальная mongodb ([инструкция по установке](https://docs.mongodb.com/v3.4/tutorial/install-mongodb-on-os-x/))

Убедиться, что сервис работает: http://localhost:3000/

## Deploy

Приложение собирается и выкладывается в Qloud.

### Production

Находится в [qloud](https://qloud.yandex-team.ru/projects/search-interfaces/serpdocs/production) (компонент `updater`) https://serpdocs.si.yandex-team.ru/updater.

#### Обновить контейнер

```(bash)
# разработческая бета
$ make docker-publish
```

```(bash)
# общая бета
$ YENV=beta make docker-publish
```

```(bash)
# продакшн версия
$ YENV=production make docker-publish
```
