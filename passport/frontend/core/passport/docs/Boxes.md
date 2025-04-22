# Как поднять тестовый бокс

Инструкция описана в https://github.yandex-team.ru/arhibot/passport-isolates/blob/master/boxes/passport-test/README

С использованием автоматики:

1. Узнать версию пакета, которая будет на боксе (см. ./Builds.md, "Как выбрать версию")
2. Запустить

```bash
cd /opt/boxes
bash /home/nchern/add-container.sh
```

3. Убить все пакеты, кроме yandex-passport-frontend
4. Прописать нужную версию пакета фронтенда: `yandex-passport-frontend=<version>`
5. После окончания сборки и запуска контейнера, приаттачиться на него, поменять, если нужно, конфиг и рестартовать фронтенд.

```bash
docker attach passport-test-%%BOXNAME%%
# два раза enter
vi /usr/lib/yandex/passport-frontend/configs/testing/index.js
ubic restart node.yandex-passport-frontend

# CTRL+P CTRL+Q
```

Сейчас необходимая правка одна — ```paths.internal``` нужно заменить на ```%%BOXNAME%%-internal.passport-box.yandex.ru```, чтобы работало редактирование адресов.
Также можно управлять мультиавторизацией через ```exports.multiauth```.

Чтобы сделать бокс с продакшеновым окружением без мультиавторизации, ставим питон и перл пакеты из прода и меняем файлы в `/usr/share/pyshared/passport_settings/`, откатывая вот такие правки: https://github.yandex-team.ru/passport/passport-settings/pull/267/files


# Как убить тестовый бокс

1. Найти docker image, соответствующий боксу
2. Остановить и убить контейнер, от которого зависит image
3. Убить image
4. Убить директорию
 
```bash
> docker images | fgrep <box-name>
< shevnv/passport-test-unified             latest              c3b2f562b08d        4 days ago           2.568 GB

> docker rmi c3b2f562b08d
< Error: Conflict, cannot delete c3b2f562b08d because the container 468770d00b8b is using it

> docker stop 468770d00b8b
< 468770d00b8b

> docker rm 468770d00b8b
< 468770d00b8b

> docker rmi c3b2f562b08d
< Deleted: ...

> rm -rf /opt/boxes/passport-test-<box-name>
```
