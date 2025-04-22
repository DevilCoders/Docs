# TSD app
У проекта много имён

**Polka** - всё на стороне пользователей и инфраструктуры Яндекса.
Apk-приложение на устройствах, имена в Няне, релизных тикетах, Графане и тд

**Picker** - так называем всё на стороне кодобазы. Репозиторий, CI.

### Установка окружения
```
make install
```

### Запуск в локальном режиме
```
npm run serve
npm run serve-device //для запуска на устройстве
```

### Сборка
```
npm run build
```

### Повышение версии
```
sh scripts/release.sh [major | minor | patch]
git push --follow-tags
```
Или
```
1.
npm version [major | minor | patch]

2.
Правка файла public/version.json с актуализацией версией.
```


### Выкладка в Няню
```
Тестинг:
  make deploy-testing-picker-ui
Прод:
  make deploy-prestable-picker-ui
  make deploy-stable-picker-ui

Для деплоя в s3 необходимо:
  1. Перенести из собранного образа папку с собранной статики на локальную машину.
  для этого делаем:
    1.1 Смотрим название собранного образа
    docker images
    ищем последний собранный, копируем его ид
    1.2 запускаем контейнер
    docker run -p 80:80 --net=host -it --rm {ид}
    1.3 смотрим запущенные контейнеры
    docker ps -a
    копируем имя контейнера
    1.3 копируем статику из контейнера
    docker cp  {имя}:/app/build ./
  2. Из папки ./build нужно выполнить команду
  aws --profile=test-polka-uploader --endpoint-url=http://s3.mdst.yandex.net s3 cp --recursive {version}/ s3://polka-ui/{version}/
  aws --profile=prod-polka-uploader --endpoint-url=http://s3.mds.yandex.net s3 cp --recursive {version}/ s3://polka-ui/{version}/
  где version === git describe

3.
Ждем перехода сборки до статуса active
Тестинг
  https://nanny.yandex-team.ru/ui/#/services/catalog/lavka_polka_testing/
Престейбл
  https://nanny.yandex-team.ru/ui/#/services/catalog/lavka_polka_pre_stable/
Стейбл
  https://nanny.yandex-team.ru/ui/#/services/catalog/lavka_polka_stable/

4.
Проверяем версию в проде
```

### При использовании с докером
```
yarn install
npm run build
docker-compose up -d
```

### Запуск девтулзов в cypress
```
npm install -g @vue/devtools
vue-devtools
```

## Как работает CI
* Делаем пуш в PR в Пикере
* Тимсити Пикера пуллит основную репу Лавки
* Репу Пикера пуллит тоже как один из сабмодулей Лавки
* Переключается на текущий ПР внутри сабмодуля Пикера
* Пускает рецепт |make test-picker-teamcity|
  * Сам рецепт лежит в репе Лавки
* Подымает сервисы из репы Лавки
* Тесты пускает из репы Пикера |make -C modules/lavka-picker test|

### Versions
Работа с Версиями
* Используются для статики
* Разные для Тестинга, Прода и Локала
  * Тестинг
    * Формат `1.2.75testing366`
    * Версию проставляет ТимСити при деплое
  * Прод (и Пре тоже)
    * Формат `1.2.75`
    * Версию проставляет ТимСити при деплое
  * CI
    * Формат `5965337a-andrew-zak`
    * Версию проставляет ТимСити при катке CI
  * Локал (dev-машина)
    * Формат `5965337a-andrew-zak`
    * Версию можно получить командой `make version`


### arc hooks

нужно скопировать
`/arc-hooks/arcconfig` в `~/.arcconfig`
