## Docker

### Подготовка к работе с `docker`

1. Установить [docker for mac](https://download.docker.com/mac/stable/Docker.dmg)
2. Запустить и подождать пока он не перестанет стартовать.

### Работа с `docker`

### Надо получить токен и залогиниться
[Токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1)
`docker login  -u <login> -p <token_body> registry.yandex.net`

Подробнее про [docker distribution](https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/).

### Нужно запросить в idm роль
В https://idm.yandex-team.ru/ нужно запросить роль https://nda.ya.ru/3UV2zn и дождаться ее выдачи.

#### Сборка контейнера
У нас реализована двухуровневая сборка. В начале собирается отдельный docker-образ с зависимостями (baseimage), а после него уже образ с приложением. Контейнер с зависимостями надо пересобирать только при обновлении package-lock.json.

Сборка базового образа:
`npm run docker-build-baseimage`
Сборка основго образа:
`npm run docker-build`

Проставление тега:
* для публичной версии (тестинг) перед сборкой делаем `npm version minor` и `npm run docker-build`
* для разработческой версии задаем кастомный префикс `user=gela-d- npm run docker-build`

#### Заливка контейнера в репо
Заливка базового образа (если он пересобирался):
`npm run docker-push-baseimage`
Заливка основного образа:
`npm run docker-push`
Если собирали тег, то `user=gela-d- npm run docker-push`

#### Теги
* Просмотр всех тегов - `curl -H "Authorization: OAuth <TOKEN>" -v https://registry.yandex.net/v2/tycoon/frontend/tags/list`
* Удаление тега: https://packages.tools.yandex-team.ru/docker/tycoon%2Ffrontend/
* Удаление тега вручную:
```
curl -H "Authorization: OAuth <TOKEN>" -H "Accept: application/vnd.docker.distribution.manifest.v2+json" 'https://registry.yandex.net/v2/altay/frontend/manifests/v2.13.0' | shasum -a 256

—> aea34c91c3c49fad6828ec292b15f4888190376db15659f095cfff9e36dd8888

curl -H "Authorization: OAuth <TOKEN>" -H "Accept: application/vnd.docker.distribution.manifest.v2+json" 'https://registry.yandex.net/v2/altay/frontend/manifests/sha256:0bbb621f98aaf85219304e7750789f2d8713439715fe74b2033e792a9c7424cc' -X DELETE
```
* Удаление тега, созданного TeamCity:
```
curl -I -H "Authorization: OAuth <TOKEN>" 'https://registry.yandex.net/v2/tycoon/frontend/manifests/v2.8.7'  | grep Docker-Content-Digest

берешь строку sha256:.....

curl -H "Authorization: OAuth <TOKEN>" 'https://registry.yandex.net/v2/tycoon/frontend/manifests/sha256:c160021d940bc5655d98fe5d884b740016d411e1ec177e43f56f6e8dffdd7c10' -X DELETE

```


#### Локальная отладка
##### Запуск собранного контейнера
`docker run -p 8082:80 -e MAPS_NODEJS_PORT=8080 registry.yandex.net/tycoon/frontend`
или
`npm run docker-run`

##### Запуск терминала в собранном контейнере:
`docker run -i -t --entrypoint /bin/bash registry.yandex.net/tycoon/frontend`
или
`npm run docker-shell`
