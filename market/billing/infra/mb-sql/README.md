# Установка

## Mac OS X

В директории делаем `ya make`, на полученный `./bin/mb-sql` делаем симлинк из привычного нам пути, содержащегося в PATH, например:
```
cd ~/bin
ln -s ~/arcadia/market/billing/infra/mb-sql mb-sql
```
или можно скопировать

Прописываем настройки
```
cp ~/arcadia/market/billing/infra/mb-sql/mb-sql.conf.yaml ~/.mb-sql.conf.yaml
```
Открываем  `~/.mb-sql.conf.yaml` и `staff-login` меняем на свой логин по стафу, а `***` на пароль к соответствующей системе (см. почту, спрашивай коллег);

Для работы c Oracle потребуется sqlcl, поставить можно так
`brew install sqlcl`
или альтернативный вариант в [документации](https://docs.yandex-team.ru/market-billing/guide/basics/install-sqlcl)

Для работы с PG потребуется pgsql поставить можно так
`brew install postgresql`
подробнее в [документации]((https://docs.yandex-team.ru/market-billing/guide/basics/db-queries#psql))



