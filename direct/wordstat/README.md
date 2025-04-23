Deploy
======


Prepare
-------

  * Set environment variables (USER - login, EMAIL - login@yandex-team.ru, DEBFULLNAME - 'Vasya Pupkin', DEBEMAIL - login@yandex-team.ru)
  * Create ssh and pgp keys and publish them on staff.yandex-team.ru
  * Make sure Skynet copier is installed and running.
  If it is not possible or desirable to install Skynet copier, then find server with installed, start sky-server.sh there
  and define SKYHOST environment variable like this:
    export SKYHOST="hostname:port"

Test build
----------

  To build deb package from working copy without signing it, run `./build.sh`.
  deb package will appear in parent directory (`ls -l ../*.deb`)

Get regions form from Direct
----------------------------

  `make --no-print-directory -C ./ -f ./bin/build/01_fetch_regions.mk clean build`
  
Deploy on new servers
---------------------

You need to deliver secrets: `sudo yav-deploy`

Build release and deploy
------------------------
  * Run `./build_release.sh $(dpkg-parsechangelog --show-field Version)` (this command can be used to build versions >=2.135)
  * Run `dupload -c ./`
  * Create conductor ticket for deploying `<tag>` version of packages `yandex-wordstat-frontend` and `yandex-wordstat-frontend-configs` in 'testing' branch
  * Test http://wordstat-test.yandex.ru
  * Create conductor ticket for deploying `<tag>` version of packages `yandex-wordstat-frontend` and `yandex-wordstat-frontend-configs` in 'stable' branch

---

## Локальная разработка

1. На локальной машине выполнить:
```(bash)
ssh-add
```
2. Зайти по `ssh` на `ppcdev6` (номер `ppcdev` важен, поскольку на других `ppcdev`-ах не удаётся скачать торренты через `skynet`):
```(bash)
ssh -A ppcdev6
```
3. Примонтировать аркадию (флаг `--allow-other` важен):
```(bash)
# по-умолчанию монтируем в директорию ~/arcadia
arc mount --allow-other
```
4. Перейти в директорию проекта:
```(bash)
cd arcadia/direct/wordstat
```
5. Запустить проксирование для `skynet`:
```(bash)
SKYHOST_PORT=${SKYHOST_PORT:-7075}
./sky-server.sh $SKYHOST_PORT &
SKYHOST=${SKYHOST:-"$(hostname --fqdn):$SKYHOST_PORT"}
echo "$SKYHOST" > ./docker_env/_common/skyhost
```
6. Собрать базовый образ:
```(bash)
docker build -t registry.yandex.net/wordstat/frontend__common ./docker_env/_common
```
7. Собрать dev-образ:
```(bash)
docker build -t registry.yandex.net/wordstat/frontend_dev ./docker_env/dev
```
8. Запустить dev-образ:
```(bash)
export PORT=8020; export YAV_TOKEN="$(yav oauth)"; docker run -e PORT -e USER -e YAV_TOKEN -v /home/${USER}/.ssh:/root/.ssh:ro -v /var/cache/geobase:/var/cache/geobase:ro -v "$(arc root)/direct/wordstat:/app/beta${PORT}" -p $PORT:$PORT -it registry.yandex.net/wordstat/frontend_dev
```
9. Запущенный проект будет доступен по адресу: https://ppcdev6.yandex.ru:8020/
10. Обойти проблему с сертификатом можно открыв в ЯБро и набрав `thisisunsafe` (да, прямо просто печатаем с клавиатуры вникуда, когда видим предупреждение про сертификат)
11. Меняем файлы на ppcdev в директории `/path/to/arcadia/direct/wordstat` или внутри docker-контейнера. Коммитим с ppcdev из директории `/path/to/arcadia/direct/wordstat`
12. Чтобы применить изменения внутри docker-контейнера выполняем `make beta_update`

## Разработка на ppcdev с проксированием через awacs

Может потребоваться если хочется посмотреть на капчу

1. Убираем в файле ssl https://a.yandex-team.ru/arc_vcs/direct/wordstat/beta/nginx.conf.tt2?rev=998aeec289477225f97146c5fee6ed46cec1914a#L37-38
```(bash)
http {
    ...
    server {
        listen      8020; # удалить ssl тут
        listen      [::]:8020 ipv6only=on;  # удалить ssl тут
        ...
```
2. Собираем бету по инструкции выше
3. Если используется не дефолтный порт редактируем порт на который проксируются запросы в аваксе в апстриме https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/test-wordstat.yandex.ru/upstreams/list/beta_ppcdev6_8020/show
4. Бета доступна по адресу https://beta-ppcdev6-8020.wordstat-test.direct.yandex.ru/
5. Так как мы отключили поддержку https бета по адресу http://ppcdev6.yandex.ru:8020 перестанет открываться из-за HSTS. Если вам нужно по какой-то причине ходить и на http://ppcdev6.yandex.ru:8020, нужно отключить HSTS: в ЯБро или в хроме нужно в строку поиска ввести browser://net-internals/hsts#hsts в поле `Delete domain security policies` ввести `yandex.ru`

### Как протестировать капчу

- https://st.yandex-team.ru/DIRECT-168359#627e6b19f3d6e133d0b00164

## Ссылки

- skynet https://doc.yandex-team.ru/Search/skynet-dg/concepts/introduction.html
- yav-deploy https://wiki.yandex-team.ru/users/volchkov/articles/yav-deploy
- tvmtool https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon
- логи тестового балансера https://test.direct.yandex.ru/logviewer/short/t3lBJJ1N55mD53
- сборщик фронта https://github.com/bem-archive/bem-tools/blob/dev/docs/commands/commands.ru.md#bem-build
- минификатор фронта https://wiki.yandex-team.ru/verstka/tools/ycssjs/

## Среды

- ТС https://deploy.yandex-team.ru/stages/advq-wordstat-testing
