# Иерархия конфигов rules
## Разделение update\_from\_profile и update\_from\_action на 4 файла каждый
* `*\_entity` - работа с энтити
* `*\_online` - то что нужно только в online
* `*\_offline` - то что нужно только в offline
* `*` (без суффикса) то что нужно и в online и в offline

## Использование конфигов
* train: `*` + `*\_online`
* online processing: `*` + `*\_online` + `*\_entity`
* offline processing: `*` + `*\_offline`
