# Api сервиса поиска авиабилетов

Устаревший проект, используется для:
- приложений на мобильных (ios, andriod)
- советника
- подписок на цены

#### Вики
https://wiki.yandex-team.ru/Raspisanija/mobileapps/avia/api

#### Для разработки

* Скопировать настройки `cp tools/samples/environments.sh tools/`
* Обновить секреты в environments.sh, секреты, можно посмотреть на запущенных в qloud инстанcах через `env`
* Запускать './tools/run-dev.sh'
* Если не настроен nginx, положить конфиг в /etc/nginx/sites-enabled/ https://github.yandex-team.ru/avia/ansible-avia-cluster-maker/blob/master/roles/nginx/templates/default.conf

##### Ручная сборка пакета

```
$ ya package --docker --docker-registry registry.yandex.net --docker-repository avia travel/avia/avia_api/pkg.json
```

#### Отправить строки для перевода в танкер
```
./tools/run-dev-manage-django.sh tankerupload -p avia-api xgettext
```

#### Забрать переводы из танкера
```
./tools/run-dev-manage-django.sh tankerdownload -p avia-api xgettext
```
