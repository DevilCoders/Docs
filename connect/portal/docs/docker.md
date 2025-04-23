
## Локальная сборка релизного пакета

#### Установка docker

##### Docker for Mac

- см. [документацию Docker for Mac](https://docs.docker.com/engine/installation/mac/)

#### Сборка образа
- переключиться на ветку релиза и поставить в ней метку новой версии

```
$ npm version minor
```

- при первой сборке зайти в локальный [docker registry](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1), получить OAuth token и добавить его в репозиторий:

```
$ docker login  -u <login> -p <token_body> -e <email>@yandex-team.ru registry.yandex.net
```

- при первой сборке настройть сборку статики, как это сделать можно посмотреть [здесь](/docs/static.md)

- запустить скрипт сборки

```
$ npm run publish
```

Версия берется из `package.json`; скрипт клонирует ветку с меткой `<release_version>` из репозитория, устанавливает npm-пакеты, запускает `docker build` и `docker push`;

&nbsp;

## Выкладка образа на стенд

#### Qloud

- [Qloud](https://qloud-ext.yandex-team.ru/projects)&nbsp;&gt; Your projects&nbsp;&gt; workspace&nbsp;&gt; portal-yandex-team&nbsp;&gt; test; за доступом к проектам обратиться к @art

- выбрать версию сборки: docker-image&nbsp;&gt; Update

```
Tags: <release_version> (<build_hash>)
// <build_hash> указан в консоли при сборке пакета
Update
```

- проверить статус выкладки: docker-image&nbsp;&gt; Details

```
Status
NOT DEPLOYED > NOT STARTED > OK
// цикл обновления завершается в течение пары минут
```

- проверить [стенд](https://connect-test.ws.yandex-team.ru/)
