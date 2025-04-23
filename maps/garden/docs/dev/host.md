# Как налить новую dev-машинку в QYP:

Поскольку dev-машинка используется не только разработчиками Огорода, но и для разработки модулей, рекомендуется использовать следующую конфигурацию: 56 CPU, 192 GB RAM, 4 TB SSD. В качестве базового образа можно использовать самую последнюю LTS-версию Ubuntu (bionic на момент написания текста).

## Выполняем первичную настройку образа:

  ```
  # удаляем кривую версию ya-fetcher, которая приводит к странным спецэффектам
  rm `which ya`

  # удаляем странные поисковые настройки для apt-a
  rm -r /etc/apt/preferences.d

  # добавляем репозиторий yandex-musl на машинку
  # Пишем следующее в /etc/apt/sources.list.d/yandex-musl.list
  deb http://yandex-musl.dist.yandex.ru/yandex-musl unstable/all/
  deb http://yandex-musl.dist.yandex.ru/yandex-musl unstable/$(ARCH)/
  deb http://yandex-musl.dist.yandex.ru/yandex-musl testing/all/
  deb http://yandex-musl.dist.yandex.ru/yandex-musl testing/$(ARCH)/
  deb http://yandex-musl.dist.yandex.ru/yandex-musl prestable/all/
  deb http://yandex-musl.dist.yandex.ru/yandex-musl prestable/$(ARCH)/
  deb http://yandex-musl.dist.yandex.ru/yandex-musl stable/all/
  deb http://yandex-musl.dist.yandex.ru/yandex-musl stable/$(ARCH)/

  # добавляем репозиторий pgdg на машинку
  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
  echo "deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main" > /etc/apt/sources.list.d/postgresql.list

  # добавляем репозиторий git-core на машинку
  add-apt-repository ppa:git-core/ppa

  # ставим необходимые и просто полезные пакеты
  apt-get install \
	devscripts \
	docker.io \
	fuse \
	ncdu \
	nginx \
	screen \
	zsh \
	yandex-arc-launcher \
	yandex-environment-unstable \
	yandex-maps-ecstatic-tool \
	yandex-maps-torrent-client \
	yandex-passport-vault-client \
  # FIXME: дописать про установку ecstatic-client и geobase, как только ecstatic заработает

  # устанавливаем пакет с инструментами для песочниц
  # (это нужно делать отдельной командой, так как тулам нужен файл `/etc/yandex/environment.type`)
  apt-get install yandex-maps-garden-playground-tools


  # настраиваем докер (это нужно делать для каждого пользователя)
  adduser $USER docker
  docker login registry.yandex.net -u $USER -p <your_token>

  # добавляем пользователя maps (сразу добавляем его в группу docker и www-data)
  apt-get install yandex-maps-user
  adduser maps docker
  usermod -a -G www-data maps

  # раскомментируем опцию user_allow_other в /etc/fuse.conf,
  # чтобы из докера можно было ходить в примонтированный арк
  vim /etc/fuse.conf
  ```

## Устанавливаем секреты, которые будут монтироваться в песочницы:

FIXME: все секреты, кроме `yav_token.json` вообще-то [должны браться](https://st.yandex-team.ru/MAPSGARDEN-15815) из Секретницы.

* `file_storage_s3.json`
* `postgresql_servers.json`
* `yav_token.json`
* `yt.json`

## Запускаем UI для песочниц:
Убеждаемся, что `tvmtool` запущен:
  ```
  sudo service yandex-passport-tvmtool status
  ```

Найти последнюю версию UI front-garden можно в поле `version` в файле [package.json](https://a.yandex-team.ru/arc_vcs/maps/front/services/garden/package.json).
Или в интерфейсе [Yandex Deploy](https://deploy.yandex-team.ru/stages/maps-front-garden_testing/history)

Запускаем UI:
  ```
  # запускаем докер-контейнер
  docker run -it -e DEPLOY_TVM_TOOL_URL="http://localhost:18080" -e TVMTOOL_LOCAL_AUTHTOKEN=`cat /var/lib/tvmtool/local.auth` -e APP_ENV=sandbox -e PORT=13500 --entrypoint "/start.sh" --net host --name garden_modern_ui registry.yandex.net/maps/front-garden:0.0.185

  # отключаемся от контейнера
  # запускаем контейнер в фоне:
  docker start garden_modern_ui
  ```

В команде выше вместо `0.0.185` можно указать последнюю версию


Если контейнер был остановлен по какой-либо причине, то запустить его повторно через `docker run` не получится.
Вместо этого нужно использовать команду:

  ```
  docker start garden_modern_ui
  ```

Если необходимо обновить UI, то сначала удаляем старый образ:
  ```
  docker stop garden_modern_ui
  docker rm garden_modern_ui
  ```
И заново запускаем UI с новой версией контейнера

## Добавляем DNS-алиасы в зоне `.dev.maps.yandex-team.ru`:

```
dns-monkey.pl --zone-update --expression "add-cname wicket.dev.maps.yandex-team.ru wicket.sas.yp-c.yandex.net"
dns-monkey.pl --zone-update --expression "add-cname *.wicket.dev.maps.yandex-team.ru wicket.sas.yp-c.yandex.net"
```

Через [Сертификатор](https://crt.yandex-team.ru) заказываем внутренний ssl-сертификат и складываем его в `/etc/ssl/yandex/server.pem`. В сертификате должны быть указаны хосты:

* `wicket.sas.yp-c.yandex.net`
* `wicket.dev.maps.yandex-team.ru`
* `*.wicket.dev.maps.yandex-team.ru`

Урезаем права доступа к сертификату и рестартуем nginx:

```
chmod 700 /etc/ssl/yandex/server.pem
chown www-data:www-data /etc/ssl/yandex/server.pem
systemctl restart nginx.service
```

## Стартуем uwsgi-сервис со списком песочниц:

```
sudo systemctl daemon-reload
sudo systemctl enable garden-playground.service
sudo systemctl start garden-playground.service
```
