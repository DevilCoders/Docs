# Lavka Superapp

Документация по разработке на [Вики](https://wiki.yandex-team.ru/lavka/dev/front/monorep/)

## Хосты

[Сервис grocery-superapp](https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355571/info)

### Общие окружения

* testing - [grocery-authproxy.lavka.tst.yandex.net](https://grocery-authproxy.lavka.tst.yandex.net/4.0/grocery-superapp-testing/lavka)
* stable - [grocery-authproxy.lavka.yandex.net](https://grocery-authproxy.lavka.yandex.net/4.0/grocery-superapp/lavka)
* dev - [localhost:3400](http://localhost:3400/4.0/grocery-superapp-testing/lavka/)

### Окружения для тестирования

Можно выкатывать через метку [deploy:unstable](https://github.yandex-team.ru/taxi/frontend-monorepo/issues?q=is%3Aopen+label%3Alavka-grocery-superapp+label%3Adeploy%3Aunstable+)

* [unstable](https://grocery-authproxy.lavka.tst.yandex.net/4.0/grocery-superapp-unstable/lavka/)
* [afgan](https://grocery-authproxy.lavka.tst.yandex.net/4.0/grocery-superapp-afgan/lavka/)
* [fractal](https://grocery-authproxy.lavka.tst.yandex.net/4.0/grocery-superapp-fractal/lavka/)
* [indica](https://grocery-authproxy.lavka.tst.yandex.net/4.0/grocery-superapp-indica/lavka/)
* [sativa](https://grocery-authproxy.lavka.tst.yandex.net/4.0/grocery-superapp-sativa/lavka/)
* [notasha](https://grocery-authproxy.lavka.tst.yandex.net/4.0/grocery-superapp-notasha/lavka/)
* [rudus](https://grocery-authproxy.lavka.tst.yandex.net/4.0/grocery-superapp-rudus/lavka/)

## Установка и разработка

```bash
cd services/lavka-grocery-superapp/
npm ci
npm run dev
git checkout -b lavka-grocery-superapp/LAVKAFRONT-XXX
```

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Как посмотреть логи на машинке в окружении

- Заходим на страницу сервиса в админке [grocery-superapp](https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355571/branches?service_name=superapp), вкладка Окружения
- Находим нужное окружение и переходим в Няню 
- В няне выбираем Instances, жмем на облачко и копируем команду для ssh
- логи сервера stderr ``tail -f /var/log/supervisor/server-stderr.log``
- логи сервера stdout ``tail -f /var/log/supervisor/server-stdout.log``

## Геобаза
- Заходим сюда https://sandbox.yandex-team.ru/resources?type=GEODATA6BIN_XURMA_STABLE&limit=20
- Скачиваем геобазу
- Кладем сюда /var/cache/geobase/geodata6.bin
```
sudo mkdir -p /var/cache/geobase
sudo cp ~/Downloads/geodata6-xurma.bin /var/cache/geobase/geodata6.bin
```

## Полезно знать

* [Установка Arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
* [GAP конфиг в проде](https://tariff-editor.taxi.yandex-team.ru/authproxies/grocery-authproxy/show/LzQuMC9ncm9jZXJ5LXN1cGVyYXBwL2xhdmth)
* [Сервис grocery-superapp в админке](https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355571/info)
* [Эксперименты в проде](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments?enabled=enabled&active=active&order=action_from__action_to&consumers=lavka-frontend)
* [Конфиги в проде](https://tariff-editor.taxi.yandex-team.ru/experiments3/configs?enabled=enabled&active=active&order=action_from__action_to&consumers=lavka-frontend)
* [Работа с танкером](https://github.yandex-team.ru/taxi/frontend-monorepo/blob/master/services/lavka-grocery-superapp/.tanker/README.md)
