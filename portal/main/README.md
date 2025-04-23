[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=portal/main&vcs=arc)](https://oko.yandex-team.ru/arc/portal/main)

### Styleguide
- [Frontend](/arcadia/portal/main/tmpl/README.md)
- [Backend](https://wiki.yandex-team.ru/Morda/styleguide/)

### Обновить uatraits

Так же как и языки нужно вызвать `scripts/get_uatraits_data` и потом закоммитить изменения. Скрипт по умолчанию берет последний пакет из `stable/all/`. Если нужна специфичная версия, например из `testing/all/` то можно вызывать скрипт с аргументом: `scripts/get_uatraits_data 1.1.63-5`
