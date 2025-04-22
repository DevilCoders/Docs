![](https://yastatic.net/q/logoaas/v1/Mappa.svg?size=48)

| | teamcity | nanny | site |
| ------------- | ------------- | ------------- | ------------- |
| **local-dev** | – | – | [mappa.tef.front.taxi.localhost.yandex-team.ru:8081](//mappa.tef.front.taxi.localhost.yandex-team.ru:8081) |
| **remote-dev** | – | – | [mappa.%username%.front.taxi.dev.yandex-team.ru](//mappa.%username%.front.taxi.dev.yandex-team.ru) |

> :warning: Сейчас нет бэка конфигов, поэтому они захардкожены
> * [mappa/cars](//mappa.eugenest.front.taxi.dev.yandex-team.ru/mappa/cars)
> 
> * [mappa/pins](//mappa.eugenest.front.taxi.dev.yandex-team.ru/mappa/pins)
>
> * [mappa/couriers](//mappa.eugenest.front.taxi.dev.yandex-team.ru/mappa/couriers)
>
> * [mappa/simple](//mappa.eugenest.front.taxi.dev.yandex-team.ru/mappa/simple)
> 
> * [mappa/blank](//mappa.eugenest.front.taxi.dev.yandex-team.ru/mappa/blank)

## Установка

- скачать архив с сертификатами из [yav](https://yav.yandex-team.ru/secret/sec-01g4f455x5nrh56hjjcc2kjhfp)
- распаковать архив в папку cert

## Запуск

> :information_source: Точно собирается под нодой 15.14.0

### Локально

```
git clone git@github.yandex-team.ru:taxi/frontend-monorepo.git fm-mappa
cd fm-mappa
npm i --force
npm run local
```

### На виртуалке

> Не забудь подключить конфиг nginx (сэмпл в /etc/nginx/sites-available/mappa.conf)

Из `/home/%username%/www/`

```
git clone git@github.yandex-team.ru:taxi/frontend-monorepo.git fm-mappa
cd fm-mappa/services/tef-mappa
npm i --force
npm start
```

## webpack-bundle-analyzer

Локально `npm run profile`
